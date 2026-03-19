---
title: Analyses verzamelen en personalisatie toepassen in ChatGPT Apps (MCP-gegevensverzameling)
description: Gebruik een hybride MCP server + Web SDK applyResponse patroon om gebeurtenissen naar Adobe Experience Platform Edge Network te verzenden en verpersoonlijking binnen een ChatGPT App UI terug te geven.
keywords: Adobe Experience Platform, Web SDK, Edge Network, MCP, ChatGPT Apps, applyResponse, interact eindpunt, personalization, analytics
source-git-commit: c848f821ea911c82531c6784a17df0116572cd86
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 0%

---

# Analyses verzamelen en personalisatie toepassen in ChatGPT Apps (MCP-gegevensverzameling)

In deze gebruiksaanwijzing ziet u hoe u een ChatGPT-toepassing (modelcontextprotocol-server + optionele UI-componenten) koppelt aan de Adobe Experience Platform Edge Network. Met dit type gegevensverzameling kunt u analyses opnemen voor conversatie-interacties die uw gereedschappen aanroepen en persoonlijke beslissingen van de Edge Network overbrengen naar een widget die wordt gerenderd door ChatGPT.

>[!NOTE]
>
>Dit document wordt onderhouden op basis van de meest recente updates die beschikbaar zijn van zowel Adobe-gegevensverzamelingsteams als de meest recente technologische updates van OpenAI. Als zodanig verwacht Adobe dat dit document zich in de loop der tijd zal ontwikkelen en raadt het aan te controleren op updates.

Dit gebruiksgeval verkiest een hybride benadering, die zowel een server-zijimplementatie voor het verzamelen van gegevens als een cliënt-zijimplementatie voor het teruggeven van gepersonaliseerde inhoud gebruikt. Deze benadering is ideaal, aangezien het MCP hulpmiddel aanroeping het meest betrouwbare moment is om analyses te verzamelen. De widget wordt uitgevoerd in een browsercontext en is de juiste plaats om identiteit (in een cookie) op te slaan en beslissingen over personalisatie toe te passen.

Dit gebruiksgeval heeft een begeleidend volledig operationeel codevoorbeeld. Zie [ ChatGPT App + Adobe Experience Platform Edge ](https://github.com/adobe/alloy-samples/tree/main/chatgpt-app) in de `alloy-samples` bewaarplaats op GitHub voor steekproefcode en implementatieinstructies.

>[!IMPORTANT]
>
>Deze pagina schetst een verwijzingsimplementatie bedoeld om een integratiepatroon te illustreren. Controleer de beveiligings-, privacy-, toestemming- en productievereisten voordat u de benadering in uw toepassing toepast.

## Architectuur

Op een hoog niveau zijn er vijf bewegende delen:

1. **gastheer MCP (ChatGPT)**: ChatGPT haalt hulpmiddelen aan die door uw server MCP worden blootgesteld en verstrekt een stabiel pseudoniem gebruikersidentificatiecode in verzoekmeta-gegevens.
1. **server MCP (achterste)**: Bezit door uw organisatie. Er worden gereedschappen geïmplementeerd, zoals aanbiedingsobjecten, het ophalen van details of het verzenden van aanvragen.
1. **IMS van Adobe IMS**: De toegangstoken van kwesties die door uw server MCP worden gebruikt om de gegevensinzameling APIs van Adobe te roepen.
1. **Adobe Experience Platform Edge Network**: Ontvangt ervaringsgebeurtenissen die door uw server MCP worden verzonden en keert analytische erkenning, staatsupdates (zoals identiteit), en verpersoonlijkingsbesluiten terug.
1. **Ingebed Web UI (frontend widget die door de gastheer MCP wordt teruggegeven)**: Vertoningen gestructureerde resultaten en past de meta-gegevens van Adobe toe die van de MCP serverachtergrond worden ontvangen.

## Gegevensstroom

1. **herinneringen van de Gebruiker** ChatGPT **gebruikend uw server MCP.**
1. **ChatGPT** interpreteert de intent van de herinnering en roept het aangewezen **achterste hulpmiddel MCP**.
1. **De achtergrond MCP server** gebruikt de Inzameling APIs van Gegevens (`interact` eindpunt) om een ervaringsgebeurtenis naar **Edge Network** voor de inzameling van de Analytics en facultatieve verpersoonlijking te verzenden.
1. **Edge Network** keert reactiehandvatten, met inbegrip van staatsupdates en verpersoonlijkingsbesluiten, aan het **achterste MCP hulpmiddel** terug.
1. **het Achterste MCP hulpmiddel** keert een hulpmiddelresultaat terug dat bedrijfsgegevens in `structuredContent` bevat en de meta-gegevens van Adobe in `_meta` aan **ChatGPT**.
1. **ChatGPT** levert het hulpmiddelresultaat aan **vooraf ingestelde widget**, die de bedrijfsgegevens teruggeeft en de meta-gegevens van Adobe gebruikend het 4} bevel van JavaScript van het Web van SDK toepast bibliotheek. `applyResponse` Dit bevel drijft cliënt-zijstaat en geeft in aanmerking komende verpersoonlijkingsbesluiten in UI terug.

In de volgende secties wordt gedetailleerd ingegaan op elke stap.

## Stap 1: Gebruiker vraagt ChatGPT met uw MCP-server

Deze stap is het ingangspunt voor de workflow. De gebruiker geeft de intentie voor natuurlijke talen:

```text
"Use the Adobe Office Information Tool to show me details about which office that is the most pet-friendly."
```

Zie [ bouwen uw server MCP ](https://developers.openai.com/apps-sdk/build/mcp-server/) in de documentatie van Ontwikkelaars OpenAI voor meer informatie.

## Stap 2: ChatGPT interpreteert intent en roept een MCP hulpmiddel aan

Gebaseerd op de meta-gegevens van uw server MCP, interpreteert ChatGPT intent en haalt de aangewezen hulpmiddelmanager op uw server aan MCP. Deze hulpmiddelvraag leidt tot een server-zijpunt van waarheid voor de interactie die onafhankelijk van UI is die succes teruggeeft. Een van uw gereedschappen kan de volgende metagegevens bevatten:

```json
{
  "name": "office_details",
  "description": "Fetch details for a single office by ID and return personalization handles for the UI.",
  "inputSchema": {
    "type": "object",
    "properties": {
      "sessionId": { "type": "string", "description": "Server-issued session identifier." },
      "officeId": { "type": "string", "description": "Office identifier." }
    },
    "required": ["sessionId", "officeId"],
    "additionalProperties": false
  },
  "_meta": {
    "ui": {
      "visibility": ["model", "app"]
    }
  }
}
```

Zie [ bepalen hulpmiddelen ](https://developers.openai.com/apps-sdk/plan/tools/) in de documentatie van Ontwikkelaars OpenAI voor meer informatie over hoe te om ChatGPT te vertellen wat elk hulpmiddel MCP doet.

## Stap 3: Uw MCP-server verzendt een ervaringsgebeurtenis naar de Edge Network

Wanneer uw server MCP een verzoek ontvangt, brengt het een vraag aan Adobe Experience Platform Edge Network in werking om analysegegevens te registreren en naar keuze om besluit/personalisatie te verzoeken. Aangezien dit verzoek server-aan-server is, gebruik het voor authentiek verklaarde [`interact` ](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/) eindpunt als deel van [ de Inzameling APIs van Gegevens ](https://developer.adobe.com/data-collection-apis/docs/). Adobe adviseert het gebruiken van a [ douanenamespace ](https://experienceleague.adobe.com/en/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities) om langs het unieke herkenningsteken over te gaan OpenAI. Zorg ervoor dat namespace u in de Identiteiten UI en identiteitsnamespace creeert die u in uw vraaggelijke (case-sensitive) bepaalt.

```sh
curl -X POST "https://server.adobedc.net/ee/v2/interact?datastreamId={DATASTREAM_ID}"
  -H "Authorization: Bearer {TOKEN}"
  -H "x-gw-ims-org-id: {ORG_ID}"
  -H "x-api-key: {API_KEY}"
  -H "Content-Type: application/json"
  -d '{
    "event": {
      "xdm": {
        "eventType": "office.details.view",
        "identityMap": {
          "{IDENTITY_NAMESPACE}": [
            { "id": "{PSEUDONYMOUS_SUBJECT_ID}", "primary": true }
          ]
        },
        "timestamp": "YYYY-02-20T19:00:00.000Z"
      }
    },
    "query": {
      "personalization": {
        "decisionScopes": ["__view__"]
      }
    },
    "meta": {
      "state": {
        "entries": [
          { "key": "kndctr_orgid_cluster", "value": "{CLUSTER_HINT_IF_KNOWN}" },
          { "key": "kndctr_orgid_identity", "value": "{ECID_BLOB_IF_KNOWN}" }
        ]
      }
    }
  }'
```

## Stap 4: De Edge Network retourneert handgrepen

Wanneer de Edge Network de `interact` -aanroep ontvangt, reageert deze met een `handle` -array. Deze array kan beslissingen over identiteit en personalisatie bevatten, afhankelijk van uw configuratie van de gegevensstroom. Een voorbeeldreactie zou als het volgende kunnen kijken:

```json
{
  "requestId": "60a2f...2294d",
  "handle": [
    {
      "type": "locationHint:result",
      "payload": [
        { "scope": "EdgeNetwork", "hint": "or2", "ttlSeconds": 1800 }
      ]
    },
    {
      "type": "state:store",
      "payload": [
        { "key": "kndctr_..._identity", "value": "CiYzM...snTI=", "maxAge": 34128000 },
        { "key": "kndctr_..._cluster", "value": "or2", "maxAge": 1800 }
      ]
    }
  ]
}
```

Uw MCP server kan dan informatie uit de reactie van Edge Network halen om identiteitsinformatie voort te zetten:

```ts
type EdgeHandle = { type: string; payload?: Array<{ key?: string; value?: string }> };

export function extractStateStore(handles: EdgeHandle[]) {
  const store = handles.find(h => h.type === "state:store");
  const entries = store?.payload ?? [];

  const identity = entries.find(e => e.key?.includes("_identity"))?.value;
  const cluster  = entries.find(e => e.key?.includes("_cluster"))?.value;

  return { identity, cluster };
}
```

## Stap 5: MCP-server retourneert gestructureerde tooloutput plus Adobe-metagegevens naar ChatGPT

Uw MCP hulpmiddelreactie omvat zowel de gestructureerde hulpmiddeloutput als verpersoonlijking van Edge Network.

* Het `structuredContent` -object bevat bedrijfsgegevens die ChatGPT veilig kan lezen en van commentaar kan voorzien.
* Het `_meta` -object bevat Adobe-reactiehandgrepen en de serverberekend `identityMap` , zodat de widget deze kan lezen zonder die gegevens aan ChatGPT bloot te stellen. Door deze informatie in `_meta.adobe` te houden, kunt u consistent zijn met de locatie van die gegevens. Als u dezelfde `identityMap` forward doorgeeft, kan de widget dezelfde aangepaste identiteit gebruiken voor latere gebruikersinterfacegebeurtenissen.

```json
{
  "content": "Displayed details for office seattle.",
  "structuredContent": {
    "office": {
      "id": "seattle",
      "name": "Seattle",
      "amenities": ["Pet Friendly", "Cafe", "Bike Storage"]
    }
  },
  "_meta": {
    "adobe": {
      "identityMap": {
        "{IDENTITY_NAMESPACE}": [
          { "id": "{PSEUDONYMOUS_SUBJECT_ID}", "primary": true }
        ]
      },
      "handles": [
        {
          "type": "state:store",
          "payload": [
            { "key": "kndctr_..._identity", "value": "..." }
          ]
        },
        {
          "type": "personalization:decisions",
          "payload": [
            { "id": "..." }
          ]
        }
      ]
    }
  }
}
```

Zie [ Resultaten van het Hulpmiddel ](https://developers.openai.com/apps-sdk/reference/#tool-results) in de verwijzing van de Ontwikkelaar OpenAI voor meer informatie.

## Stap 6: Widget geeft het resultaat weer en past `_adobe.handles` toe met `applyResponse`

De widget rendert de bedrijfsgegevens uit `structuredContent` en leest vervolgens de Adobe-metagegevens uit `_meta.adobe` . In ChatGPT zijn dezelfde gegevens beschikbaar voor de widget via de compatibiliteitslaag:

* `window.openai.toolOutput` contains `structuredContent`
* `window.openai.toolResponseMetadata` contains `_meta`

De widget gebruikt het [`applyResponse`](../../js/commands/applyresponse.md) bevel van de bibliotheek van SDK van het Web JavaScript om cliënt-zijstaat te drijven en verpersoonlijkingsbesluiten terug te geven die door de server-kant `interact` vraag zijn teruggekeerd. Roep de opdracht [`configure`](../../js/commands/configure/overview.md) aan voordat u `applyResponse` aanroept. Aangezien uw MCP-server een `interact` -aanroep heeft uitgevoerd, hoeft u de opdracht [`sendEvent`](../../js/commands/sendevent/overview.md) niet onmiddellijk aan te roepen voor de interactie van de gereedschapsaanroep.

```js
// Configure the Web SDK before any other commands.
alloy("configure", {
  datastreamId: "YOUR_DATASTREAM_ID",
  orgId: "YOUR_EXPERIENCE_CLOUD_ORG_ID"
});

// Business data exposed to ChatGPT and the widget.
const { office } = window.openai?.toolOutput ?? {};

// Adobe metadata available only to the widget.
const adobe = window.openai?.toolResponseMetadata?.adobe ?? {};
const { identityMap, handles } = adobe;

// Hydrate client-side state and render personalization decisions from the
// server-side interact response.
alloy("applyResponse", {
  renderDecisions: true,
  responseBody: { handle: handles ?? [] }
});
```

Als de widget later aanvullende UI-side gebeurtenissen verzendt, kunt u dezelfde `identityMap` gebruiken voor deze aanroepen:

```js
alloy("sendEvent", {
  xdm: {
    eventType: "office.details.widgetView",
    identityMap
  }
});
```

Met dit patroon blijven het identiteitsgebruik aan de serverzijde en UI-zijde uitgelijnd, terwijl de aanroep van `interact` aan de serverzijde de bron van de waarheid blijft voor het verzamelen en beslissen van analyses.

## Validatie

Zodra alle bovengenoemde stappen worden gevormd, kunt u het volgende bevestigen:

* **de inzameling van Gegevens:** verifieer dat de gebeurtenissen de gewenste dataset bereiken en dat elke gebeurtenis zoals verwacht wordt verwerkt.
* **Personalization:** verifieer dat de besluiten door Edge Network zijn teruggekeerd, en dat die besluiten door uw widget worden teruggegeven.

## Beveiligings- en privacyoverwegingen

* Behandel de id&#39;s van ChatGPT als gevoelig, ook al zijn ze pseudoniem.
* Zorg ervoor dat u de toestemming van uw organisatie en de praktijken van het gegevensbeheer op deze werkschema toepast.
* Adobe raadt aan om OAuth 2.1-workflows te gebruiken voor autorisatie.
* Zorg ervoor dat de toegangstokens en geheimen nooit de cliënt of UI bereiken.
