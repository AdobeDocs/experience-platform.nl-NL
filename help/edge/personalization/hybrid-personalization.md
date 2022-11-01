---
title: Hybride verpersoonlijking die Web SDK en de Server API van het Netwerk van Edge gebruikt
description: Dit artikel toont aan hoe u SDK van het Web samen met de Server API kunt gebruiken om hybride verpersoonlijking op uw Webeigenschappen op te stellen.
keywords: personalisatie; hybride; server-API; serverzijde; hybride uitvoering;
source-git-commit: f280d4cbcde434ccf36df37e95f1902cfd02c96c
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 2%

---


# Hybride verpersoonlijking die Web SDK en de Server API van het Netwerk van Edge gebruikt

## Overzicht {#overview}

De verpersoonlijking van Hybdrid beschrijft het proces om de server-kant van de verpersoonlijkingsinhoud terug te winnen, gebruikend [Edge Network Server-API](../..//server-api/overview.md)en renderen op de client, met de [Web SDK](../home.md).

U kunt hybride personalisatie met verpersoonlijkingsoplossingen zoals Adobe Target of Offer decisioning gebruiken, het verschil is de inhoud van [!UICONTROL Server API] lading.

## Vereisten {#prerequisites}

Controleer of u aan de volgende voorwaarden voldoet voordat u hybride personalisatie gaat implementeren op uw webeigenschappen:

* U hebt besloten welke personalisatieoplossing u wilt gebruiken. Dit heeft gevolgen voor de inhoud van de [!UICONTROL Server API] lading.
* U hebt toegang tot een toepassingsserver die u kunt gebruiken om [!UICONTROL Server API] oproepen.
* U hebt toegang tot de [Edge Network Server-API](../../server-api/authentication.md).
* U hebt de juiste [geconfigureerd en geïmplementeerd](../fundamentals/configuring-the-sdk.md) Web SDK op de pagina&#39;s die u wilt personaliseren.

## Stroomdiagram {#flow-diagram}

In het onderstaande stroomdiagram wordt de volgorde beschreven van de stappen die zijn genomen om hybride personalisatie te leveren.

![Visueel stroomdiagram dat de orde van de genomen stappen toont om hybride verpersoonlijking te leveren.](assets/hybrid-personalization-diagram.png)

1. Bestaande cookies die eerder door de browser zijn opgeslagen, vooraf ingesteld op `kndctr_`, worden opgenomen in de browseraanvraag.
1. De clientwebbrowser vraagt de webpagina op van uw toepassingsserver.
1. Wanneer de toepassingsserver de paginaaanvraag ontvangt, wordt een `POST` verzoek aan de [Interactieve de gegevensinzamelingspunten van de Server API](../../server-api/interactive-data-collection.md) om personalisatie-inhoud op te halen. De `POST` verzoek bevat een `event` en `query`. De cookies uit de vorige stap, indien beschikbaar, worden opgenomen in de `meta>state>entries` array.
1. De server-API retourneert de personalisatie-inhoud naar uw toepassingsserver.
1. De toepassingsserver retourneert een HTML-reactie op de clientbrowser die de [identiteits- en clustercookies](#cookies).
1. Op de clientpagina [!DNL Web SDK] `applyResponse` wordt aangeroepen, waarbij de koppen en de hoofdtekst van de opdracht worden doorgegeven [!UICONTROL Server API] antwoord van de vorige stap.
1. De [!DNL Web SDK] Hiermee wordt de pagina geladen [[!DNL Visual Experience Composer (VEC)]](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=en) voorstellen automatisch, omdat de `renderDecisions` markering is ingesteld op `true`.
1. Op formulier gebaseerd [!DNL JSON] aanbiedingen worden handmatig toegepast via de `applyPersonalization` om de [!DNL DOM] op basis van het aanbod voor personalisatie.
1. Voor op formulieren gebaseerde activiteiten moeten weergavegebeurtenissen handmatig worden verzonden om aan te geven wanneer de aanbieding is weergegeven. Dit gebeurt via de `sendEvent` gebruiken.

## Cookies {#cookies}

Cookies worden gebruikt om de gebruikersidentiteit en clusterinformatie voort te zetten.  Wanneer het gebruiken van een hybride implementatie, behandelt de de toepassingsserver van het Web het opslaan en verzenden van deze koekjes tijdens de verzoeklevenscyclus.

| Cookie | Doel | Opgeslagen door | Verzonden door |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | Bevat identiteitsgegevens van gebruikers. | Applicatieserver | Applicatieserver |
| `kndctr_AdobeOrg_cluster` | Wijst op welke cluster van het Netwerk van de Rand zou moeten worden gebruikt om de verzoeken te vervullen. | Applicatieserver | Applicatieserver |

## Verzoek om plaatsing {#request-placement}

Server-API-aanvragen zijn vereist om proposities op te halen en een weergavemelding te verzenden. Wanneer u een hybride implementatie gebruikt, doet de toepassingsserver deze aanvragen aan de server-API.

| Verzoek | Gemaakt door |
|---|---|
| Interactief verzoek om voorstellen terug te winnen | Applicatieserver |
| Interactief verzoek om weergavemeldingen te verzenden | Applicatieserver |

## Analytische implicaties {#analytics}

Bij het implementeren van hybride personalisatie moet u speciale aandacht besteden aan het tellen van pagina&#39;s in Analytics.

Wanneer u [configureren, gegevensstroom](../datastreams/overview.md) voor Analytics worden gebeurtenissen automatisch doorgestuurd, zodat de paginareeksen worden vastgelegd.

Het voorbeeld van deze implementatie gebruikt twee verschillende gegevensstromen:

* Een gegevensstroom die voor Analytics wordt gevormd. Deze gegevensstroom wordt gebruikt voor de interactie van SDK van het Web.
* Een tweede gegevensstroom zonder een configuratie Analytics. Deze gegevensstroom wordt gebruikt voor server API verzoeken.

Op deze manier registreert de server-side aanvraag geen Analytics-gebeurtenissen, maar de client-side aanvragen wel. Dit leidt ertoe dat de verzoeken van de Analyse nauwkeurig worden geteld.


## Verzoek op de server {#server-side-request}

De voorbeeldaanvraag hieronder illustreert een Server API-aanvraag die uw toepassingsserver kan gebruiken om de personalisatie-inhoud op te halen.

>[!IMPORTANT]
>
>In dit voorbeeldverzoek wordt Adobe Target gebruikt als een oplossing voor personalisatie. Uw verzoek kan afhankelijk van uw gekozen personalisatieoplossing variëren.


**API-indeling**

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
| `dataStreamId` | `String` | Ja. | Identiteitskaart van de gegevensstroom die u gebruikt om de interactie tot het Netwerk van de Rand over te gaan. Zie de [datastreams, overzicht](../datastreams/overview.md) om te leren hoe te om een gegevensstroom te vormen. |
| `requestId` | `String` | Nee | Een willekeurige id voor correlerende interne serveraanvragen. Als niets wordt verstrekt, zal het Netwerk van de Rand één produceren en zal het in de reactie terugkeren. |

### Reactie op de server {#server-response}

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

Op de clientpagina [!DNL Web SDK] `applyResponse` wordt het bevel geroepen, die in de kopballen en het lichaam van de server-zijreactie overgaan.

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

Op formulier gebaseerd [!DNL JSON] aanbiedingen worden handmatig toegepast via de `applyPersonalization` om de [!DNL DOM] op basis van het aanbod voor personalisatie. Voor op formulieren gebaseerde activiteiten moeten weergavegebeurtenissen handmatig worden verzonden om aan te geven wanneer de aanbieding is weergegeven. Dit gebeurt via de `sendEvent` gebruiken.

```js
function sendDisplayEvent(decision) {
    const { id, scope, scopeDetails = {} } = decision;

    alloy("sendEvent", {
        xdm: {
            eventType: "decisioning.propositionDisplay",
            _experience: {
                decisioning: {
                    propositions: [
                        {
                            id: id,
                            scope: scope,
                            scopeDetails: scopeDetails,
                        },
                    ],
                },
            },
        },
    });
}
```

## Voorbeeldtoepassing {#sample-app}

Om u te helpen experimenteren en meer te leren over dit type van verpersoonlijking, verstrekken wij een steekproeftoepassing die u voor het testen kunt downloaden en gebruiken. U kunt de toepassing vanuit deze [GitHub-opslagplaats](https://github.com/adobe/alloy-samples).






