---
title: Server-kant personalisatie die de Server API van de Edge Network gebruikt
description: Dit artikel toont aan hoe u de server-API van de Edge Network kunt gebruiken om verpersoonlijking op de server op uw Webeigenschappen op te stellen.
keywords: personalisatie; server-api; edge-network; server-side;
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 1%

---


# Server-kant personalisatie die de Server API van de Edge Network gebruikt

## Overzicht {#overview}

De server-zijverpersoonlijking impliceert het gebruiken van [ de Server API van de Edge Network ](../../server-api/overview.md) om de klantenervaring op uw Webeigenschappen te personaliseren.

In het voorbeeld dat in dit artikel wordt beschreven, wordt de verpersoonlijkingsinhoud teruggewonnen server-kant, gebruikend de Server API. Vervolgens wordt de HTML op de server weergegeven, op basis van de opgehaalde personalisatie-inhoud.

In de onderstaande tabel ziet u een voorbeeld van gepersonaliseerde en niet-gepersonaliseerde inhoud.

| Voorbeeldpagina zonder personalisatie | Voorbeeldpagina met personalisatie |
|---|---|
| ![ Web-pagina van het voorbeeld zonder verpersoonlijking ](assets/plain.png) | ![ Web-pagina van het voorbeeld met verpersoonlijking ](assets/personalized.png) |

## Overwegingen {#considerations}

### Cookies {#cookies}

Cookies worden gebruikt om de gebruikersidentiteit en clusterinformatie voort te zetten.  Wanneer u een serverimplementatie gebruikt, handelt de toepassingsserver het opslaan en verzenden van deze cookies tijdens de levenscyclus van de aanvraag af.

| Cookie | Doel | Opgeslagen door | Verzonden door |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | Bevat identiteitsgegevens van de gebruiker. | Applicatieserver | Applicatieserver |
| `kndctr_AdobeOrg_cluster` | Geeft aan welke Edge Network-cluster moet worden gebruikt om aan de aanvragen te voldoen. | Applicatieserver | Applicatieserver |

### Verzoek om plaatsing {#request-placement}

Personalization-verzoeken zijn vereist om voorstellen op te halen en een weergavemelding te verzenden. Wanneer het gebruiken van een server-zijimplementatie, doet de toepassingsserver deze verzoeken aan de Server API van de Edge Network.

| Verzoek | Door |
|---|---|
| Interactief verzoek om voorstellen terug te winnen | Toepassingsserver die de Edge Network Server-API aanroept. |
| Interactief verzoek om weergavemeldingen te verzenden | Toepassingsserver die de Edge Network Server-API aanroept. |

## Voorbeeldtoepassing {#sample-app}

Het hieronder beschreven proces gebruikt een steekproeftoepassing die u als uitgangspunt kunt gebruiken om te experimenteren en meer over dit type van verpersoonlijking te leren.

U kunt dit voorbeeld downloaden en het aan uw eigen behoeften aanpassen. U kunt bijvoorbeeld omgevingsvariabelen wijzigen zodat de voorbeeld-app aanbiedingen vanuit uw eigen configuratie van het Experience Platform invoegt.

Open hiertoe het `.env` -bestand in de hoofdmap van de opslagplaats en wijzig de variabelen volgens uw configuratie. Start de voorbeeldtoepassing opnieuw en u kunt experimenteren met uw eigen personalisatie-inhoud.

### Het voorbeeld uitvoeren {#running-sample}

Voer de onderstaande stappen uit om de voorbeeld-app uit te voeren.

1. Kloon [ deze bewaarplaats ](https://github.com/adobe/alloy-samples) aan uw lokale machine.
2. Open een terminal en navigeer naar de map `personalization-server-side` .
3. Voer `npm install` uit.
4. Voer `npm start` uit.
5. Open uw webbrowser en navigeer naar `http://localhost` .

## Procesoverzicht {#process}

In deze sectie worden de stappen beschreven die worden gebruikt voor het ophalen van de inhoud van de personalisatie.

1. [ Uitdrukkelijke ](https://expressjs.com/) wordt gebruikt voor een lee server-kant implementatie. Dit behandelt basisserververzoeken en het verpletteren.
2. De browser vraagt om de webpagina. Alle cookies die eerder door de browser zijn opgeslagen, vooraf ingesteld door `kndctr_` , worden opgenomen.
3. Wanneer de pagina van de toepassingsserver wordt gevraagd, wordt een gebeurtenis verzonden naar het [ interactieve eindpunt van de gegevensinzameling ](../../../server-api/interactive-data-collection.md) om verpersoonlijkingsinhoud te halen. De steekproef app gebruikt helpermethodes om het bouwen van en het verzenden van verzoeken naar API (zie [ aepEdgeClient.js ](https://github.com/adobe/alloy-samples/blob/main/common/aepEdgeClient.js)) te vereenvoudigen. De aanvraag `POST` bevat een `event` en een `query` . De cookies uit de vorige stap, indien beschikbaar, worden opgenomen in de array `meta>state>entries` .

   ```js
   fetch(
   "https://edge.adobedc.net/ee/v2/interact?dataStreamId=abc&requestId=123",
   {
      headers: {
         accept: "*/*",
         "accept-language": "en-US,en;q=0.9",
         "cache-control": "no-cache",
         "content-type": "text/plain; charset=UTF-8",
         pragma: "no-cache",
         "sec-fetch-dest": "empty",
         "sec-fetch-mode": "cors",
         "sec-fetch-site": "cross-site",
         "sec-gpc": "1",
         "Referrer-Policy": "strict-origin-when-cross-origin",
         Referer: "http://localhost/",
      },
      body: JSON.stringify({
         event: {
         xdm: {
            web: {
               webPageDetails: {
               URL: "http://localhost/",
               },
               webReferrer: {
               URL: "",
               },
            },
            identityMap: {
               FPID: [
               {
                  id: "xyz",
                  authenticatedState: "ambiguous",
                  primary: true,
               },
               ],
            },
            timestamp: "2022-06-23T22:21:00.878Z",
         },
         data: {},
         },
         query: {
         identity: {
            fetch: ["ECID"],
         },
         personalization: {
            schemas: [
               "https://ns.adobe.com/personalization/default-content-item",
               "https://ns.adobe.com/personalization/html-content-item",
               "https://ns.adobe.com/personalization/json-content-item",
               "https://ns.adobe.com/personalization/redirect-item",
               "https://ns.adobe.com/personalization/dom-action",
            ],
            decisionScopes: ["__view__", "sample-json-offer"],
         },
         },
         meta: {
         state: {
            domain: "localhost",
            cookiesEnabled: true,
            entries: [
               {
               "key": "kndctr_XXX_AdobeOrg_identity",
               "value": "abc123"
               },
               {
               "key": "kndctr_XXX_AdobeOrg_cluster",
               "value": "or2"
               }
            ],
         },
         },
      }),
      method: "POST",
   }
   ).then((res) => res.json());
   ```

4. De aanbieding van het Doel van de op vorm-gebaseerde activiteit wordt gelezen van de reactie en gebruikt wanneer het veroorzaken van de reactie van de HTML.
5. Voor op vorm-gebaseerde activiteiten, moeten de vertoningsgebeurtenissen in de implementatie manueel worden verzonden om erop te wijzen wanneer de aanbieding is getoond. In dit voorbeeld wordt het bericht tijdens de levenscyclus van de aanvraag naar de server verzonden.

   ```js
   function sendDisplayEvent(aepEdgeClient, req, propositions, cookieEntries) {
   const address = getAddress(req);
   
   aepEdgeClient.interact(
      {
         event: {
         xdm: {
            web: {
               webPageDetails: { URL: address },
               webReferrer: { URL: "" },
            },
            timestamp: new Date().toISOString(),
            eventType: "decisioning.propositionDisplay",
            _experience: {
               decisioning: {
               propositions: propositions.map((proposition) => {
                  const { id, scope, scopeDetails } = proposition;
   
                  return {
                     id,
                     scope,
                     scopeDetails,
                  };
               }),
               },
            },
         },
         },
         query: { identity: { fetch: ["ECID"] } },
         meta: {
         state: {
            domain: "",
            cookiesEnabled: true,
            entries: [...cookieEntries],
         },
         },
      },
      {
         Referer: address,
      }
   );
   }
   ```

6. [!DNL Visual Experience Composer (VEC)] -aanbiedingen worden genegeerd, omdat ze alleen via Web SDK kunnen worden gerenderd.
7. Wanneer de HTML-reactie wordt geretourneerd, worden de identiteits- en clustercookies ingesteld op de reactie van de toepassingsserver.