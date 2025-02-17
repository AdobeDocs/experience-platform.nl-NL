---
title: Offer Decisioning gebruiken met de Platform Web SDK
description: De Adobe Experience Platform Web SDK kan gepersonaliseerde aanbiedingen leveren en teruggeven die in Offer Decisioning worden beheerd. U kunt uw aanbiedingen en andere gerelateerde objecten maken met de gebruikersinterface of API van Offer Decisioning.
keywords: aanbieden besluit;beslissing;Web SDK;Platform Web SDK;gepersonaliseerde aanbiedingen;leveren aanbiedingen;aanbieding levering levering;aanbieden verpersoonlijking aan;
exl-id: 4ab51f9d-3c44-4855-b900-aa2cde673a9a
source-git-commit: b2c3b1160782a81ea66f42e21e494e0a7d90e037
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 0%

---

# Offer Decisioning gebruiken met de Platform Web SDK

Adobe Experience Platform [!DNL Web SDK] kan persoonlijke aanbiedingen die in Offer Decisioning worden beheerd, aanbieden en weergeven. U kunt uw aanbiedingen en andere verwante objecten maken met de gebruikersinterface (UI) of API&#39;s van Offer Decisioning.

## Vereisten

* Organisatie is ingeschakeld voor randbesluitvorming
* Aanbiedingen, gemaakte activiteiten
* DataStream wordt gepubliceerd

## Terminologie

Het is belangrijk dat u de volgende terminologie begrijpt wanneer u met Offer Decisioning werkt. Voor meer informatie en om extra termijnen te bekijken, gelieve de [ verklarende woordenlijst van Offer Decisioning ](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html) te bezoeken.

* **Scopes van het Besluit:** voor Offer Decisioning, zijn het besluitvormingswerkingsgebied Base64 gecodeerde koorden van JSON die de activiteit en plaatsings IDs bevatten u de dienst van de aanbiedingsbeslissing wilt gebruiken om aanbiedingen voor te stellen.

  *werkingsgebied JSON van het Besluit:*

  ```json
  {
    "activityId":"xcore:offer-activity:11cfb1fa93381aca",
    "placementId":"xcore:offer-placement:1175009612b0100c"
  }
  ```

  *het werkingsgebied Base64 van het Besluit gecodeerde koord:*

  ```json
  "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
  ```

  >[!TIP]
  >
  >U kunt de waarde van het besluitvormingswerkingsgebied van de **pagina van het Overzicht van de Activiteit** in UI kopiëren.

  ![ montages van het Beslissingsexemplaar.](assets/decision-scope-copy.png)

* **Datastreams:** voor meer informatie, te lezen gelieve de [ gegevensstromen ](/help/datastreams/overview.md) documentatie.

* **Identiteit**: Voor meer informatie, te lezen gelieve deze documentatie die schetst hoe [ het Web SDK van het Platform de Dienst van de Identiteit ](../../identity/overview.md) gebruikt.

## Offer Decisioning inschakelen

Voer de volgende stappen uit om Offer Decisioning in te schakelen:

1. Toegelaten Adobe Experience Platform in uw [ datastream ](/help/datastreams/overview.md) en controleer de &quot;Offer Decisioning&quot;doos

   ![ aanbod-besluit-rand-config ](./assets/offer-decisioning-edge-config.png)

1. Volg de instructies om [ SDK ](/help/web-sdk/install/overview.md) te installeren (SDK kan standalone of door UI worden geïnstalleerd. Zie de [ snel begingids van markeringen ](/help/tags/quick-start/quick-start.md)) voor meer informatie.
1. Configureer de SDK for Offer Decisioning met `personalization.decisionScopes` . Hieronder vindt u aanvullende specifieke Offer Decisioning-stappen.

   * De zelfstandige SDK installeren

      1. De handeling &quot;sendEvent&quot; configureren met `personalization.decisionScopes`

     ```javascript
     alloy("sendEvent", {
       ...
       "personalization": {
         "decisionScopes": [
           "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIwOWMxM2JkZDIyNCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMDZhODRkMDViMTEifQ==",
           "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIyNWI5NTUwNWIxZiIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMjFmOTQzMDE0MmIifQ=="
         ]
       }
     });
     ```

   * De SDK installeren via tags

      1. [Een tag-eigenschap maken](/help/tags/ui/administration/companies-and-properties.md)
      1. [ voeg de ingebedde code ](https://experienceleague.adobe.com/docs/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html) toe
      1. Installeer en vorm de uitbreiding van het Web SDK van het Platform met de Datstream u door de configuratie van &quot;Datstream&quot;dropdown te selecteren creeerde. Zie de documentatie op [ uitbreidingen ](/help/tags/ui/managing-resources/extensions/overview.md).

         ![ install-a-web-sdk-uitbreiding ](./assets/install-aep-web-sdk-extension.png)

         ![ vorm-sep-web-sdk-uitbreiding ](./assets/configure-aep-web-sdk-extension.png)

      1. Creeer de noodzakelijke [ Elementen van Gegevens ](/help/tags/ui/managing-resources/data-elements.md). Bij het absolute minimum, moet u een Identiteitskaart van het Web van het Platform van SDK en een het gegevenselement van de Objecten van SDK XDM van het Web van het Platform tot stand brengen XDM.

         ![ identiteit-kaart-gegeven-element ](./assets/identity-map-data-element.png)

         ![ xdm-voorwerp-gegeven-element ](./assets/xdm-object-data-element.png)

      1. Creeer uw [ Regels ](/help/tags/ui/managing-resources/rules.md).

         * Voeg een actie van de Gebeurtenis van de Gebeurtenis van het Web van het Platform toe SDK verzendt en voeg relevant `decisionScopes` aan de configuratie van die actie toe

         ![ send-event-action-DecisionScopes ](./assets/send-event-action-decisionScopes.png)

      1. [ creeer en publiceer een bibliotheek ](/help/tags/ui/publishing/libraries.md) die alle relevante Regels, Elementen van Gegevens, en Uitbreidingen bevat u hebt gevormd

## Voorbeeldverzoeken en -antwoorden

### Eén `decisionScopes` -waarde

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
| `identityMap` | Ja | Verwijs naar deze [ documentatie van de Dienst van de Identiteit ](../../identity/overview.md). | Eén identiteit per aanvraag. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`. <br><br> Opmerking: gebruikers hoeven de parameter `ECID` niet op te nemen in de API-aanroep. Deze parameter wordt automatisch toegevoegd aan de vraag indien nodig. |
| `decisionScopes` | Ja | Een array met Base64-gecodeerde tekenreeksen van JSON die de activiteit- en plaatsings-id&#39;s bevatten. | Maximaal 30 `decisionScopes` per aanvraag. | `"decisionScopes": ["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="]` |

**Reactie**

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
| `identityMap` | Ja | Verwijs naar deze [ documentatie van de Dienst van de Identiteit ](../../identity/overview.md). | Eén identiteit per aanvraag. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`. <br><br> Opmerking: gebruikers hoeven de parameter `ECID` niet op te nemen in de API-aanroep. Deze parameter wordt automatisch toegevoegd aan de vraag indien nodig. |
| `decisionScopes` | Ja | Een array met Base64-gecodeerde tekenreeksen van JSON die de activiteit- en plaatsings-id&#39;s bevatten. | Maximaal 30 `decisionScopes` per aanvraag. | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

**Reactie**

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

## Beperkingen

Sommige aanbiedingsbeperkingen worden momenteel niet ondersteund door de mobiele Edge Network-workflows, bijvoorbeeld Afdekkingen. De waarde van het gebied van de Plak specificeert het aantal tijden een aanbieding over alle gebruikers kan worden voorgesteld. Voor meer details, zie [ de geschiktheidsregels en beperkingsdocumentatie van de Aanbieding ](https://experienceleague.adobe.com/docs/offer-decisioning/using/managing-offers-in-the-offer-library/creating-personalized-offers.html#eligibility).
