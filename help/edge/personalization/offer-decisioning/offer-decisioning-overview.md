---
title: Offer Decisioning - Overzicht
seo-title: Offer Decisioning en Adobe Experience Platform Web SDK
description: Adobe Experience Platform Web SDK kan gepersonaliseerde aanbiedingen leveren en weergeven die in Offer Decisioning worden beheerd. U kunt uw aanbiedingen en andere gerelateerde objecten maken met de gebruikersinterface of API van Offer Decisioning.
seo-description: Adobe Experience Platform Web SDK kan gepersonaliseerde aanbiedingen leveren en weergeven die in Offer Decisioning worden beheerd. U kunt uw aanbiedingen en andere gerelateerde objecten maken met de gebruikersinterface of API van Offer Decisioning.
keywords: bied besluit aan;het besluit;Web SDK;Platform Web SDK;gepersonaliseerde aanbiedingen;lever aanbiedingen;bied levering aan;bied verpersoonlijking aan;
translation-type: tm+mt
source-git-commit: 05049025bdfc67af4d811e90218bf6e2613fab51
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 4%

---


# [!DNL Offer Decisioning] Overzicht

>[!NOTE]
>
>Het gebruik van Offer Decisioning in Adobe Experience Platform Web SDK is momenteel beschikbaar in een vroeg stadium om gebruikers te selecteren. Deze functionaliteit is niet beschikbaar voor alle IMS-organisaties.

Adobe Experience Platform [!DNL Web SDK] kan persoonlijke aanbiedingen leveren en weergeven die in Offer Decisioning worden beheerd. U kunt uw aanbiedingen en andere verwante objecten maken met de gebruikersinterface (UI) of API&#39;s van Offer Decisioning.

## Vereisten

* IMS-organisatie is ingeschakeld voor randbeslissingen
* Aanbiedingen, gemaakte activiteiten
* Edge config wordt gepubliceerd

## Terminologie

Het is belangrijk dat u de volgende terminologie begrijpt wanneer u met Offer Decisioning werkt. Voor meer informatie en om extra termijnen te bekijken, gelieve [Offer Decisioning verklarende woordenlijst](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html).

* **Container:** Een container is een isolatiemechanisme om verschillende zorgen van elkaar te onderscheiden. De container-id is het eerste padelement voor alle gegevensopslagruimte-API&#39;s. Alle beslissingsobjecten bevinden zich in een container.

* **Beslissingsbereiken:** Voor Offer Decisioning, zijn dit de Base64 gecodeerde koorden van JSON die de activiteit en plaatsings IDs bevatten u de dienst van de aanbiedingsbeslissing wilt gebruiken om aanbiedingen voor te stellen.

   *Reikwijdte van de beschikking JSON:*

   ```json
   {
     "activityId":"xcore:offer-activity:11cfb1fa93381aca",
     "placementId":"xcore:offer-placement:1175009612b0100c"
   }
   ```

   *Base64-gecodeerde tekenreeks met beslissingsbereik:*

   ```json
   "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
   ```

   >[!TIP]
   >
   >U kunt de waarde van het beslissingswerkingsgebied van **Overzicht van de Activiteit** pagina in UI kopiëren.

   ![](assets/decision-scope-copy.png)

* **Edge Configuration:** Lees de documentatie over de  [Edge-](../../fundamentals/edge-configuration.md) configuratie voor meer informatie.

* **Identiteit**: Lees voor meer informatie deze documentatie waarin wordt beschreven hoe de Identiteitsservice [ van ](../../identity/overview.md)Platform Web SDK wordt gebruikt.

## Offer Decisioning inschakelen

Als u Offer Decisioning wilt inschakelen, moet u de volgende stappen uitvoeren:

1. Adobe Experience Platform ingeschakeld in uw [Edge-configuratie](../../fundamentals/edge-configuration.md) en schakel het vakje &quot;Offer Decisioning&quot; in
   ![aanbieding-beslist-rand-config](./assets/offer-decisioning-edge-config.png)
2. Volg de instructies om de SDK [te installeren ](../../fundamentals/installing-the-sdk.md) (De SDK kan standalone of door [Adobe Experience Platform Launch](http://launch.adobe.com/) worden geïnstalleerd. Hier volgt een [snelstartgids voor het starten van het Platform](https://docs.adobe.com/content/help/en/launch/using/intro/get-started/quick-start.html)).
3. [Configureer de ](../../fundamentals/configuring-the-sdk.md) SDK voor Offer Decisioning. Hieronder vindt u aanvullende specifieke Offer Decisioning-stappen.
   * Zelfstandige geïnstalleerde SDK
      1. Vorm de &quot;sendEvent&quot;actie met uw `decisionScopes`

      ```javascript
      alloy("sendEvent", {
          ...
          "decisionScopes": [
              "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIwOWMxM2JkZDIyNCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMDZhODRkMDViMTEifQ==",
              "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIyNWI5NTUwNWIxZiIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMjFmOTQzMDE0MmIifQ=="
          ]
      })
      ```
   * Geïnstalleerde SDK voor Platform starten
      1. [Een Platform starten-eigenschap maken](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html)
      2. [De Platform Insluitcode starten toevoegen](https://docs.adobe.com/content/help/en/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html)
      3. Installeer en vorm de uitbreiding van SDK van het Web AEP met de Configuratie van de Rand u enkel door de configuratie van de drop-down &quot;Configuratie van de Rand&quot;te selecteren creeerde. Nuttige documentatie op [extensions](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html).
         ![install-aep-web-sdk-extension](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk-extension](./assets/configure-aep-web-sdk-extension.png)
      4. Maak de benodigde [Data Elements](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/data-elements.html). Bij het absolute minimum, zult u een Identiteitskaart van SDK van het Web van het Platform en een gegevenselement van de Objecten van SDK van het Web van het Platform XDM moeten tot stand brengen.
         ![identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)
      5. Maak uw [Regels](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/rules.html).
         * Voeg een Platform SDK toe verzendt de actie van de Gebeurtenis en voeg relevante `decisionScopes` aan de configuratie van die actie toe
            ![send-event-action-decisionsScopes](./assets/send-event-action-decisionScopes.png)
      6. [Creeer en publiceer een bibliotheek ](https://docs.adobe.com/content/help/en/launch/using/reference/publish/libraries.html) die alle relevante Regels, de Elementen van Gegevens, en Uitbreidingen bevat u hebt gevormd


## Voorbeeldverzoeken en reacties

### Eén `decisionScopes`-waarde

**Verzoek**

```json
{
  "events": [
    {
      "xdm": {
        "identityMap": {
          "ECID": [
            {
              "id": "91133425615229052182584359620783097099"
            }
          ]
        }
      },
      "query": {
        "personalization": {
          "decisionScopes": [
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
          ]
        }
      }
    }
  ]
}
```

| Eigenschap | Vereist | Beschrijving | Limieten | Voorbeeld |
|---|---|---|---|---|
| `identityMap` | Ja | Raadpleeg deze [Identiteitsdocumentatie](../../identity/overview.md). | Eén identiteit per aanvraag. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
| `decisionScopes` | Ja | Een array met Base64-gecodeerde tekenreeksen van JSON die de activiteit- en plaatsings-id&#39;s bevatten. | Maximaal 30 `decisionScopes` per verzoek. | `"decisionScopes": ["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="]` |

**Antwoord**

```json
{
  "requestId": "94c4f2f1-9218-43ce-afd3-eb0d853c5174",
  "handle": [
    {
      "payload": [
        {
          "id": "2862bb89-5df2-4bc6-85c2-d8f7e1a091de",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381aca",
            "etag": "2"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b0100c",
            "etag": "1"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:124cc332095cfa74",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-html",
              "etag": "1",
              "data": {
                "id": "xcore:personalized-offer:124cc332095cfa74",
                "format": "text/html",
                "language": [
                  "en-US"
                ],
                "content": "<p>20% Off on shipping</p>",
                "characteristics": {
                  "foo": "bar",
                  "foo1": "bar1"
                }
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

| Eigenschap | Beschrijving | Voorbeeld |
|---|---|---|
| `scope` | De reikwijdte van de beslissing die tot de voorgestelde aanbiedingen heeft geleid. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | De unieke id van de aanbiedingsactiviteit. | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | De unieke id van de plaatsing van de aanbieding. | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | De id van de voorgestelde aanbieding. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | Het schema van de inhoud verbonden aan de voorgestelde aanbieding. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | De id van de voorgestelde aanbieding. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | Het formaat van de inhoud die aan de voorgestelde aanbieding is gekoppeld. | `"format": "text/html"` |
| `language` | Een array met talen die zijn gekoppeld aan de inhoud van het voorgestelde aanbod. | `"language": [ "en-US" ]` |
| `content` | De inhoud die aan de voorgestelde aanbieding in het formaat van een koord wordt geassocieerd. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | De afbeeldingsinhoud die aan de voorgestelde aanbieding is gekoppeld, wordt weergegeven in de vorm van een URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Kenmerken van de voorgestelde aanbieding in de vorm van een JSON-object. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

### Meerdere `decisionScopes` waarden

**Verzoek**

```json
{
  "events": [
    {
      "xdm": {
        "identityMap": {
          "ECID": [
            {
              "id": "91133425615229052182584359620783097099"
            }
          ]
        }
      },
      "query": {
        "personalization": {
          "decisionScopes": [
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ==",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyYzkxMzg1Mjc2MDE4YyIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMzMxZjU2MTYyYWEyZjcifQ=="
          ]
        }
      }
    }
  ]
}
```

| Eigenschap | Vereist | Beschrijving | Limieten | Voorbeeld |
|---|---|---|---|---|
| `identityMap` | Ja | Raadpleeg deze [Identiteitsdocumentatie](../../identity/overview.md). | Eén identiteit per aanvraag. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
| `decisionScopes` | Ja | Een array met Base64-gecodeerde tekenreeksen van JSON die de activiteit- en plaatsings-id&#39;s bevatten. | Maximaal 30 `decisionScopes` per verzoek. | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

**Antwoord**

```json
{
  "requestId": "94c4f2f1-9218-43ce-afd3-eb0d853c5174",
  "handle": [
    {
      "payload": [
        {
          "id": "a2804dfb-a0ec-4df9-8311-59d3ecdeb642",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MTEyMyIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDExMjMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381123",
            "etag": "1"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b01123",
            "etag": "3"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:11e36d4a22954123",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-text",
              "etag": "2",
              "data": {
                "id": "xcore:personalized-offer:11e36d4a22954123",
                "format": "text/text",
                "language": [
                  "en"
                ],
                "content": "20% Off on shipping",
                "characteristics": {
                  "foo2": "bar2"
                }
              }
            }
          ]
        },
        {
          "id": "a2804dfb-a0ec-4df9-8311-59d3ecdeb642",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381aca",
            "etag": "2"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b0100c",
            "etag": "1"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:11e36d4a2295415d",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-imagelink",
              "etag": "1",
              "data": {
                "id": "xcore:personalized-offer:11e36d4a2295415d",
                "format": "image/png",
                "language": [
                  "en"
                ],
                "deliveryURL": "https://image.jpeg",
                "characteristics": {
                  "foo": "bar",
                  "foo1": "bar1"
                }
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

| Eigenschap | Beschrijving | Voorbeeld |
|---|---|---|
| `scope` | De reikwijdte van de beslissing die tot de voorgestelde aanbiedingen heeft geleid. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | De unieke id van de aanbiedingsactiviteit. | `"id": "xcore:offer-activity:11cfb1fa93381123"` |
| `placement.id` | De unieke id van de plaatsing van de aanbieding. | `"xcore:offer-placement:1175009612b01123"` |
| `items.id` | De id van de voorgestelde aanbieding. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `schema` | Het schema van de inhoud verbonden aan de voorgestelde aanbieding. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-text"` |
| `data.id` | De id van de voorgestelde aanbieding. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `format` | Het formaat van de inhoud die aan de voorgestelde aanbieding is gekoppeld. | `"format": "text/text"` |
| `language` | Een array met talen die zijn gekoppeld aan de inhoud van het voorgestelde aanbod. | `"language": [ "en-US" ]` |
| `content` | De inhoud die aan de voorgestelde aanbieding in het formaat van een koord wordt geassocieerd. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | De afbeeldingsinhoud die aan de voorgestelde aanbieding is gekoppeld, wordt weergegeven in de vorm van een URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Kenmerken van de voorgestelde aanbieding in de vorm van een JSON-object. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |
