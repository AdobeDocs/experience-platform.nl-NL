---
title: Aanpassing op server met de Edge Network Server-API
description: In dit artikel wordt getoond hoe u de Edge Network Server-API kunt gebruiken om serverpersonalisatie op uw wegeigenschappen te implementeren.
keywords: personalisatie; server-API; randnetwerk; serverzijde;
source-git-commit: 3e7084953a5e158059074c857bfce4940a83661b
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 1%

---


# Aanpassing op server met de Edge Network Server-API

## Overzicht {#overview}

De verpersoonlijking aan de serverzijde impliceert het gebruiken van [Edge Network Server-API](../../server-api/overview.md) om de klantervaring op uw Web-eigenschappen te personaliseren.

In het voorbeeld dat in dit artikel wordt beschreven, wordt de verpersoonlijkingsinhoud teruggewonnen server-kant, gebruikend de Server API. Dan, wordt de HTML teruggegeven server-kant, die op de teruggewonnen verpersoonlijkingsinhoud wordt gebaseerd.

In de onderstaande tabel ziet u een voorbeeld van gepersonaliseerde en niet-gepersonaliseerde inhoud.

| Voorbeeldpagina zonder personalisatie | Voorbeeldpagina met personalisatie |
|---|---|
| ![Voorbeeld van webpagina zonder personalisatie](assets/plain.png) | ![Voorbeeld van webpagina met personalisatie](assets/personalized.png) |

## Overwegingen {#considerations}

### Cookies {#cookies}

Cookies worden gebruikt om de gebruikersidentiteit en clusterinformatie voort te zetten.  Wanneer u een serverimplementatie gebruikt, handelt de toepassingsserver het opslaan en verzenden van deze cookies tijdens de levenscyclus van de aanvraag af.

| Cookie | Doel | Opgeslagen door | Verzonden door |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | Bevat identiteitsgegevens van gebruikers. | Applicatieserver | Applicatieserver |
| `kndctr_AdobeOrg_cluster` | Wijst op welke cluster van het Netwerk van de Rand zou moeten worden gebruikt om de verzoeken te vervullen. | Applicatieserver | Applicatieserver |

### Verzoek om plaatsing {#request-placement}

Aanvragen voor personalisatie zijn vereist voor het ophalen van voorstellen en het verzenden van een weergavemelding. Wanneer u een serverimplementatie gebruikt, doet de toepassingsserver deze aanvragen aan de Edge Network Server-API.

| Verzoek | Gemaakt door |
|---|---|
| Interactief verzoek om voorstellen terug te winnen | Toepassingsserver die de Edge Network Server-API aanroept. |
| Interactief verzoek om weergavemeldingen te verzenden | Toepassingsserver die de Edge Network Server-API aanroept. |

## Voorbeeldtoepassing {#sample-app}

Het hieronder beschreven proces gebruikt een steekproeftoepassing die u als uitgangspunt kunt gebruiken om te experimenteren en meer over dit type van verpersoonlijking te leren.

U kunt dit voorbeeld downloaden en het aan uw eigen behoeften aanpassen. U kunt bijvoorbeeld omgevingsvariabelen wijzigen zodat de voorbeeld-app aanbiedingen vanuit uw eigen configuratie van het Experience Platform invoegt.

Om dit te doen, open `.env` bestand in de hoofdmap van de opslagplaats en wijzig de variabelen volgens uw configuratie. Start de voorbeeldtoepassing opnieuw en u kunt experimenteren met uw eigen personalisatie-inhoud.

### Het voorbeeld uitvoeren {#running-sample}

Voer de onderstaande stappen uit om de voorbeeld-app uit te voeren.

1. Klonen [deze opslagplaats](https://github.com/adobe/alloy-samples) naar uw lokale computer.
2. Open een terminal en navigeer naar de `personalization-server-side` map.
3. Uitvoeren `npm install`.
4. Uitvoeren `npm start`.
5. Webbrowser openen en naar `http://localhost`.

## Procesoverzicht {#process}

In deze sectie worden de stappen beschreven die worden gebruikt voor het ophalen van de inhoud van de personalisatie.

1. [Express](https://expressjs.com/) wordt gebruikt voor een slanke server-zijimplementatie. Dit behandelt basisserververzoeken en het verpletteren.
2. De browser vraagt om de webpagina. Alle cookies die eerder door de browser zijn opgeslagen, vooraf vastgelegd met `kndctr_`, worden opgenomen.
3. Wanneer de pagina bij de toepassingsserver wordt aangevraagd, wordt een gebeurtenis verzonden naar [interactief eindpunt gegevensverzameling](../../../server-api/interactive-data-collection.md) om personalisatie-inhoud op te halen. De voorbeeldtoepassing gebruikt hulpmethoden om het samenstellen en verzenden van aanvragen naar de API te vereenvoudigen (zie [aepEdgeClient.js](https://github.com/adobe/alloy-samples/blob/main/common/aepEdgeClient.js)). De `POST` verzoek bevat een `event` en `query`. De cookies uit de vorige stap, indien beschikbaar, worden opgenomen in de `meta>state>entries` array.

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

6. [!DNL Visual Experience Composer (VEC)] aanbiedingen worden genegeerd, omdat ze alleen via Web SDK kunnen worden weergegeven.
7. Wanneer de HTML-reactie wordt geretourneerd, worden de identiteits- en clustercookies ingesteld op de reactie van de toepassingsserver.