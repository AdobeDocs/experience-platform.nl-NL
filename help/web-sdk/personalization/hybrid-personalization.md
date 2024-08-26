---
title: Hybride verpersoonlijking die Web SDK en de Server API van de Edge Network gebruikt
description: Dit artikel toont aan hoe u SDK van het Web samen met de Server API kunt gebruiken om hybride verpersoonlijking op uw Webeigenschappen op te stellen.
keywords: personalisatie; hybride; server-API; server-side; hybride implementatie;
exl-id: 506991e8-701c-49b8-9d9d-265415779876
source-git-commit: 9489b5345c2b13b9d05b26d646aa7f1576840fb8
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 1%

---

# Hybride verpersoonlijking die Web SDK en de Server API van de Edge Network gebruikt

## Overzicht {#overview}

Hybdrid verpersoonlijking beschrijft het proces om verpersoonlijkingsinhoud server-kant terug te winnen, gebruikend de [ Server API van de Edge Network ](../../server-api/overview.md), en het terug te geven cliënt-kant, gebruikend [ Web SDK ](../home.md).

U kunt hybride personalisatie met verpersoonlijkingsoplossingen zoals Adobe Target, Adobe Journey Optimizer, of Offer decisioning gebruiken, het verschil is de inhoud van de [!UICONTROL Server API] lading.

## Vereisten {#prerequisites}

Controleer of u aan de volgende voorwaarden voldoet voordat u hybride personalisatie gaat implementeren op uw webeigenschappen:

* U hebt besloten welke personalisatieoplossing u wilt gebruiken. Dit is van invloed op de inhoud van de [!UICONTROL Server API] payload.
* U hebt toegang tot een toepassingsserver waarmee u [!UICONTROL Server API] aanroepen kunt uitvoeren.
* U hebt toegang tot [ de Server API van de Edge Network ](../../server-api/authentication.md).
* U hebt correct [ gevormd ](/help/web-sdk/commands/configure/overview.md) en opgesteld SDK van het Web op de pagina&#39;s die u wilt personaliseren.

## Stroomdiagram {#flow-diagram}

In het onderstaande stroomdiagram wordt de volgorde beschreven van de stappen die zijn genomen om hybride personalisatie te leveren.

![ Visueel stroomdiagram dat de orde van de genomen stappen toont om hybride verpersoonlijking te leveren.](assets/hybrid-personalization-diagram.png)

1. Eventuele bestaande cookies die eerder door de browser zijn opgeslagen, vooraf ingesteld door `kndctr_` , worden opgenomen in de browseraanvraag.
1. De clientwebbrowser vraagt de webpagina op van uw toepassingsserver.
1. Wanneer de toepassingsserver het paginaverzoek ontvangt, doet het a `POST` verzoek aan het [ de interactieve eindpunt van de gegevensinzameling van de Server API ](../../server-api/interactive-data-collection.md) om verpersoonlijkingsinhoud te halen. De aanvraag `POST` bevat een `event` en een `query` . De cookies uit de vorige stap, indien beschikbaar, worden opgenomen in de array `meta>state>entries` .
1. De server-API retourneert de verpersoonlijkingsinhoud naar uw toepassingsserver.
1. De toepassingsserver keert een reactie van HTML op cliëntbrowser terug, die de [ identiteit en clusterkoekjes ](#cookies) bevatten.
1. Op de clientpagina wordt de opdracht [!DNL Web SDK] `applyResponse` aangeroepen, waarbij de koppen en de hoofdtekst van het [!UICONTROL Server API] -antwoord uit de vorige stap worden doorgegeven.
1. [!DNL Web SDK] geeft de aanbiedingen van het Doel [[!DNL Visual Experience Composer (VEC)] ](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) en de punten van het Kanaal van Journey Optimizer automatisch terug, omdat de `renderDecisions` vlag aan `true` wordt geplaatst.
1. Doelformuliergebaseerde [!DNL HTML]/[!DNL JSON] -aanbiedingen en Journey Optimizer-ervaringen op basis van code worden handmatig toegepast via de `applyProposition` -methode om de [!DNL DOM] bij te werken op basis van de personalisatie-inhoud in het voorstel.
1. Voor op vorm-gebaseerde [!DNL HTML]/ [!DNL JSON] aanbiedingen van het Doel en op code-gebaseerde ervaringen van Journey Optimizer, moeten de vertoningsgebeurtenissen manueel worden verzonden om erop te wijzen wanneer de teruggekeerde inhoud is getoond. Dit gebeurt via de opdracht `sendEvent` .

## Cookies {#cookies}

Cookies worden gebruikt om de gebruikersidentiteit en clusterinformatie voort te zetten.  Wanneer het gebruiken van een hybride implementatie, behandelt de de toepassingsserver van het Web het opslaan en verzenden van deze koekjes tijdens de verzoeklevenscyclus.

| Cookie | Doel | Opgeslagen door | Verzonden door |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | Bevat identiteitsgegevens van de gebruiker. | Applicatieserver | Applicatieserver |
| `kndctr_AdobeOrg_cluster` | Geeft aan welke Edge Network-cluster moet worden gebruikt om aan de aanvragen te voldoen. | Applicatieserver | Applicatieserver |

## Verzoek om plaatsing {#request-placement}

Server-API-aanvragen zijn vereist om proposities op te halen en een weergavemelding te verzenden. Wanneer u een hybride implementatie gebruikt, doet de toepassingsserver deze aanvragen aan de server-API.

| Verzoek | Door |
|---|---|
| Interactief verzoek om voorstellen terug te winnen | Applicatieserver |
| Interactief verzoek om weergavemeldingen te verzenden | Applicatieserver |

## Analytische implicaties {#analytics}

Bij het implementeren van hybride personalisatie moet u speciale aandacht besteden aan het tellen van pagina&#39;s in Analytics.

Wanneer u [ een gegevensstroom ](../../datastreams/overview.md) voor Analytics vormt, door:sturen de gebeurtenissen automatisch zodat de paginareeksen worden gevangen.

Het voorbeeld van deze implementatie gebruikt twee verschillende gegevensstromen:

* Een gegevensstroom die voor Analytics wordt gevormd. Deze gegevensstroom wordt gebruikt voor de interactie van SDK van het Web.
* Een tweede gegevensstroom zonder een configuratie Analytics. Deze gegevensstroom wordt gebruikt voor server API verzoeken. U moet deze gegevensstroom met de zelfde bestemmingsconfiguratie vormen zoals de gegevensstroom die u voor Analytics vormde.

Op deze manier registreert de server-side aanvraag geen Analytics-gebeurtenissen, maar de client-side aanvragen wel. Dit leidt ertoe dat de verzoeken van de Analyse nauwkeurig worden geteld.


## Verzoek op de server {#server-side-request}

De voorbeeldaanvraag hieronder illustreert een Server API-aanvraag die uw toepassingsserver kan gebruiken om de personalisatie-inhoud op te halen.

>[!IMPORTANT]
>
>In dit voorbeeldverzoek wordt Adobe Target gebruikt als een oplossing voor personalisatie. Uw verzoek kan afhankelijk van uw gekozen personalisatieoplossing variëren.


**API formaat**

```http
POST /ee/v2/interact
```

### Verzoek {#request}

```shell
curl -X POST "https://edge.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" 
-H "Content-Type: text/plain" 
-d '{
   "event":{
      "xdm":{
         "web":{
            "webPageDetails":{
               "URL":"http://localhost/"
            },
            "webReferrer":{
               "URL":""
            }
         },
         "identityMap":{
            "FPID":[
               {
                  "id":"xyz",
                  "authenticatedState":"ambiguous",
                  "primary":true
               }
            ]
         },
         "timestamp":"2022-06-23T22:21:00.878Z"
      },
      "data":{
         
      }
   },
   "query":{
      "identity":{
         "fetch":[
            "ECID"
         ]
      },
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/default-content-item",
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "__view__",
            "sample-json-offer"
         ]
      }
   },
   "meta":{
      "state":{
         "domain":"localhost",
         "cookiesEnabled":true,
         "entries":[
            {
               "key":"kndctr_XXX_AdobeOrg_identity",
               "value":"abc123"
            },
            {
               "key":"kndctr_XXX_AdobeOrg_cluster",
               "value":"or2"
            }
         ]
      }
   }
}'
```

| Parameter | Type | Vereist | Beschrijving |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Ja. | De id van de gegevensstroom die u gebruikt om de interacties door te geven aan de Edge Network. Zie het [ overzicht van gegevensstromen ](../../datastreams/overview.md) leren hoe te om een gegevensstroom te vormen. |
| `requestId` | `String` | Nee | Een willekeurige id voor correlerende interne serveraanvragen. Als niets wordt verstrekt, zal de Edge Network één produceren en zal het in de reactie terugkeren. |

### Serverreactie {#server-response}

De voorbeeldreactie hieronder laat zien hoe de API-reactie van de server eruit zou kunnen zien.


```json
{
   "requestId":"5c539bd0-33bf-43b6-a054-2924ac58038b",
   "handle":[
      {
         "payload":[
            {
               "id":"XXX",
               "namespace":{
                  "code":"ECID"
               }
            }
         ],
         "type":"identity:result"
      },
      {
         "payload":[
            {
               "..."
            },
            {
               "..."
            }
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      }
   ]
}
```

## Aanvraag op de client {#client-request}

Op de clientpagina wordt de opdracht [!DNL Web SDK] `applyResponse` aangeroepen, waarbij de koppen en de hoofdtekst van de reactie van de server worden doorgegeven.

```js
   alloy("applyResponse", {
      "renderDecisions": true,
      "responseHeaders": {
         "cache-control": "no-cache, no-store, max-age=0, no-transform, private",
         "connection": "close",
         "content-encoding": "deflate",
         "content-type": "application/json;charset=utf-8",
         "date": "Mon, 11 Jul 2022 19:42:01 GMT",
         "server": "jag",
         "strict-transport-security": "max-age=31536000; includeSubDomains",
         "transfer-encoding": "chunked",
         "vary": "Origin",
         "x-adobe-edge": "OR2;9",
         "x-content-type-options": "nosniff",
         "x-konductor": "22.6.78-BLACKOUTSERVERDOMAINS:7fa23f82",
         "x-rate-limit-remaining": "599",
         "x-request-id": "5c539bd0-33bf-43b6-a054-2924ac58038b",
         "x-xss-protection": "1; mode=block"
      },
      "responseBody": {
         "requestId": "5c539bd0-33bf-43b6-a054-2924ac58038b",
         "handle": [
         {
            "payload": [
               {
               "id": "XXX",
               "namespace": {
                  "code": "ECID"
               }
               }
            ],
            "type": "identity:result"
         },
         {
            "payload": [
               {...}, 
               {...}
            ],
            "type": "personalization:decisions",
            "eventIndex": 0
         }
         ]
      }
   }
   ).then(applyPersonalization("sample-json-offer"));
```

[!DNL JSON] -aanbiedingen op basis van formulieren worden handmatig toegepast via de methode `applyPersonalization` om de [!DNL DOM] bij te werken op basis van de aanpassingsaanbieding. Voor op formulieren gebaseerde activiteiten moeten weergavegebeurtenissen handmatig worden verzonden om aan te geven wanneer de aanbieding is weergegeven. Dit gebeurt via de opdracht `sendEvent` .

```js
function sendDisplayEvent(decision) {
    const { id, scope, scopeDetails = {} } = decision;

    alloy("sendEvent", {
        "xdm": {
            "eventType": "decisioning.propositionDisplay",
            "_experience": {
                "decisioning": {
                    "propositions": [{
                        "id": id,
                        "scope": scope,
                        "scopeDetails": scopeDetails
                    }],
                    "propositionEventType": {
                        "display": 1
                    }
                }
            }
        }
    });
}
```

## Voorbeeldtoepassing {#sample-app}

Om u te helpen experimenteren en meer te leren over dit type van verpersoonlijking, verstrekken wij een steekproeftoepassing die u voor het testen kunt downloaden en gebruiken. U kunt de toepassing, samen met gedetailleerde instructies op downloaden hoe te om het te gebruiken, van deze [ bewaarplaats GitHub ](https://github.com/adobe/alloy-samples).
