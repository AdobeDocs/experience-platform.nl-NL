---
title: Het gebruiken van Offer decisioning met het Web SDK van het Platform
description: De SDK van het Web van Adobe Experience Platform kan gepersonaliseerde aanbiedingen leveren en teruggeven die in Offer decisioning worden beheerd. U kunt uw aanbiedingen en andere gerelateerde objecten maken met de gebruikersinterface of API van de Offer decisioning.
keywords: offer decisioning;het besluit;Web SDK;het Web SDK van het Platform Web;gepersonaliseerde aanbiedingen;lever aanbiedingen;bied levering aan;bied verpersoonlijking aan;
exl-id: 4ab51f9d-3c44-4855-b900-aa2cde673a9a
source-git-commit: 5a688fed26a8f641347ed1c625bfe448004f75b0
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 1%

---

# Het gebruiken van Offer decisioning met het Web SDK van het Platform

>[!NOTE]
>
>Het gebruik van Offer decisioning in de SDK van het Web van Adobe Experience Platform is beschikbaar in vroege toegang om gebruikers te selecteren. Deze functionaliteit is niet beschikbaar voor alle IMS-organisaties.

Adobe Experience Platform [!DNL Web SDK] kan gepersonaliseerde aanbiedingen leveren en teruggeven die in Offer decisioning worden beheerd. U kunt uw aanbiedingen en andere verwante objecten maken met de gebruikersinterface (UI) of API&#39;s van de Offer decisioning.

## Vereisten

* IMS-organisatie is ingeschakeld voor randbeslissingen
* Aanbiedingen, gemaakte activiteiten
* DataStream wordt gepubliceerd

## Terminologie

Het is belangrijk om de volgende terminologie te begrijpen wanneer het werken met Offer decisioning. Voor meer informatie en om extra termijnen te bekijken, te bezoeken gelieve [verklarende woordenlijst van de Offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html).

* **Container:** Een container is een isolatiemechanisme om verschillende zorgen van elkaar te onderscheiden. De container-id is het eerste padelement voor alle gegevensopslagruimte-API&#39;s. Alle beslissingsobjecten bevinden zich in een container.

* **Beslissingsbereiken:** Voor Offer decisioning, zijn besluitvormingswerkingsgebied Base64 gecodeerde koorden van JSON die de activiteit en plaatsings IDs bevatten u de dienst van de offer decisioning wilt gebruiken om aanbiedingen voor te stellen.

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

* **Gegevensstromen:** Lees de documentatie over  [](../../fundamentals/datastreams.md) gegevensstromen voor meer informatie.

* **Identiteit**: Voor meer informatie, gelieve deze documentatie te lezen die schetst hoe het Web SDK van het  [Platform de Dienst](../../identity/overview.md) van de Identiteit gebruikt.

## Offer decisioning inschakelen

Voer de volgende stappen uit om Offer decisioning in te schakelen:

1. Adobe Experience Platform ingeschakeld in uw [datastream](../../fundamentals/datastreams.md) en schakel het vakje &quot;Offer decisioning&quot; in

   ![aanbieding-beslist-rand-config](./assets/offer-decisioning-edge-config.png)

1. Volg de instructies om [SDK](../../fundamentals/installing-the-sdk.md) te installeren (De SDK kan standalone of door [UI van de Inzameling van Gegevens](https://experience.adobe.com/#/data-collection/) worden geïnstalleerd. Zie de [Tags quick start guide](../../../tags/quick-start/quick-start.md)) voor meer informatie.
1. [Vorm ](../../fundamentals/configuring-the-sdk.md) SDK voor Offer decisioning. Hieronder vindt u aanvullende specifieke stappen voor Offer decisioning.

   * De zelfstandige SDK installeren

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
   * De SDK installeren via tags

      1. [Een tag-eigenschap maken](../../../tags/ui/administration/companies-and-properties.md)
      1. [De insluitcode toevoegen](https://experienceleague.adobe.com/docs/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html)
      1. Installeer en vorm de uitbreiding van SDK van het Web van het Platform met de Datastream u door de configuratie van &quot;Datstream&quot;dropdown te selecteren creeerde. Zie de documentatie op [extensions](../../../tags/ui/managing-resources/extensions/overview.md).

         ![install-aep-web-sdk-extension](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk-extension](./assets/configure-aep-web-sdk-extension.png)

      1. Maak de benodigde [Data Elements](../../../tags/ui/managing-resources/data-elements.md). Bij het absolute minimum, moet u een Identiteitskaart van SDK van het Web van het Platform en een gegevenselement van de Objecten van SDK van het Web van het Platform XDM tot stand brengen.

         ![identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)

      1. Maak uw [Regels](../../../tags/ui/managing-resources/rules.md).

         * Voeg een Platform SDK toe verzendt de actie van de Gebeurtenis en voeg relevante `decisionScopes` aan de configuratie van die actie toe

            ![send-event-action-decisionsScopes](./assets/send-event-action-decisionScopes.png)
      1. [Creeer en publiceer een bibliotheek ](../../../tags/ui/publishing/libraries.md) die alle relevante Regels, de Elementen van Gegevens, en Uitbreidingen bevat u hebt gevormd



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

## Beperkingen

Sommige aanbodbeperkingen worden momenteel niet ondersteund door de mobiele Edge-workflows voor beleving, bijvoorbeeld Afdekkingen. De waarde van het gebied van het Afschilderen specificeert het aantal tijden een aanbieding over alle gebruikers kan worden voorgesteld. Zie [Subsidiabiliteitsregels en beperkingen aanbieden in documentatie](https://experienceleague.adobe.com/docs/offer-decisioning/using/managing-offers-in-the-offer-library/creating-personalized-offers.html#eligibility) voor meer informatie.
