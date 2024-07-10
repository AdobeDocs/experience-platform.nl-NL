---
keywords: aangepaste personalisatie; bestemming; ervaring met aangepaste bestemming van platform;
title: Aangepaste verpersoonlijkingsverbinding
description: Deze bestemming verstrekt externe verpersoonlijking, inhoudsbeheersystemen, en servers, en andere toepassingen die op uw plaats lopen een manier om publieksinformatie van Adobe Experience Platform terug te winnen. Deze bestemming verstrekt verpersoonlijking in real time die op het gebruikersprofiellidmaatschap wordt gebaseerd.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 0%

---


# Aangepaste verpersoonlijkingsverbinding {#custom-personalization-connection}

## Doelwijziging {#changelog}

| Releasedatum | Type bijwerken | Beschrijving |
|---|---|---|
| Mei 2023 | Bijwerken van functionaliteit en documentatie | Vanaf mei 2023 **[!UICONTROL Custom personalization]** verbinding wordt ondersteund [kenmerkgebaseerde personalisatie](../../ui/activate-edge-personalization-destinations.md#map-attributes) en is algemeen beschikbaar voor alle klanten. |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>Profielkenmerken kunnen vertrouwelijke gegevens bevatten. Om deze gegevens te beschermen, moet u [Edge Network Server-API](/help/server-api/overview.md) wanneer het vormen van **[!UICONTROL Custom Personalization]** doel voor op attribuut-gebaseerde verpersoonlijking. Alle API-aanroepen van de server moeten in een [geverifieerde context](../../../server-api/authentication.md).
>
><br>Als u reeds SDK van het Web of Mobiele SDK voor uw integratie gebruikt, kunt u attributen via de Server API terugwinnen door een server-zijintegratie toe te voegen.
>
><br>Als u de bovenstaande vereisten niet opvolgt, wordt de personalisatie alleen gebaseerd op het lidmaatschap van het publiek.

## Overzicht {#overview}

Stel deze bestemming in om externe personalisatieplatforms, contentbeheersystemen en servers en andere toepassingen die op websites van klanten worden uitgevoerd, toe te staan om publieksinformatie van Adobe Experience Platform op te halen.

## Vereisten {#prerequisites}

Deze integratie wordt aangedreven door de [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) of de [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/). U moet één van deze SDKs gebruiken om deze bestemming te gebruiken.

>[!IMPORTANT]
>
>Lees voordat u een aangepaste verpersoonlijkingsverbinding maakt de handleiding over het [activeer publieksgegevens aan randverpersoonlijkingsbestemmingen](../../ui/activate-edge-personalization-destinations.md). Deze gids neemt u door de vereiste configuratiestappen voor zelfde-pagina en volgende-paginagrootte het gebruiksgevallen van het verpersoonlijkingsgebruik, over veelvoudige Experience Platform componenten.

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Door het Experience Platform gegenereerde soorten publiek [Segmenteringsservice](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Soorten publiek [geïmporteerd](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van CSV-bestanden. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!DNL Profile request]** | U vraagt om alle soorten publiek die voor één profiel zijn toegewezen in de aangepaste verpersoonlijkingsbestemming. Verschillende aangepaste verpersoonlijkingsdoelen kunnen worden ingesteld voor verschillende [Gegevensverzamelingsgegevensstromen Adoben](../../../datastreams/overview.md). |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

## Verbinden met de bestemming {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Informatie over gegevensstroom-id&#39;s"
>abstract="Met deze optie bepaalt u in welke gegevensverzamelingsgegevensstroom het publiek wordt opgenomen in het antwoord op de pagina. Het drop-down menu toont slechts gegevensstromen die de toegelaten bestemmingsconfiguratie hebben. U moet een gegevensstroom vormen alvorens u uw bestemming kunt vormen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html" text="Leer hoe u een gegevensstroom configureert"

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Verbindingsparameters {#parameters}

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

* **[!UICONTROL Name]**: Vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Description]**: Voer een beschrijving in voor uw doel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken. Dit veld is optioneel.
* **[!UICONTROL Integration alias]**: Deze waarde wordt als een JSON-objectnaam verzonden naar de Web SDK van het Experience Platform.
* **[!UICONTROL Datastream ID]**: Dit bepaalt in welke gegevensstroom van de Inzameling van Gegevens het publiek in de reactie op de pagina zal worden omvat. Het drop-down menu toont slechts gegevensstromen die de toegelaten bestemmingsconfiguratie hebben. Zie [Een gegevensstroom configureren](../../../datastreams/overview.md) voor meer informatie .

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Lezen [Profielen en doelen voor Edge-verpersoonlijking voor doelgroepen activeren](../../ui/activate-edge-personalization-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

## Geëxporteerde gegevens {#exported-data}

Als u [Tags in Adobe Experience Platform](../../../tags/home.md) om SDK van het Web van het Experience Platform op te stellen, gebruik [De gebeurtenis send voltooid](../../../tags/extensions/client/web-sdk/event-types.md) functionaliteit en uw aangepaste code-actie heeft een `event.destinations` variabele die u kunt gebruiken om de geëxporteerde gegevens weer te geven.

Hier volgt een voorbeeldwaarde voor het dialoogvenster `event.destinations` variabele:

```
[
   {
      "type":"profileLookup",
      "destinationId":"7bb4cb8d-8c2e-4450-871d-b7824f547111",
      "alias":"personalizationAlias",
      "segments":[
         {
            "id":"399eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         },
         {
            "id":"499eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         }
      ]
   }
]
```

Als u dit niet gebruikt [Tags](/help/tags/home.md) om het Web SDK van het Experience Platform op te stellen, gebruik [opdrachtreacties](/help/web-sdk/commands/command-responses.md) om de geëxporteerde gegevens weer te geven.

Het JSON-antwoord van Adobe Experience Platform kan worden geparseerd om de bijbehorende integratiealias te zoeken van de toepassing die u integreert met Adobe Experience Platform. De gebruikers-id&#39;s kunnen als doelparameters worden doorgegeven aan de code van de toepassing. Hieronder ziet u een voorbeeld van hoe dit er specifiek uitziet voor de doelrespons.

```
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function(result) {
    if(result.destinations) { // Looking to see if the destination results are there
 
        // Get the destination with a particular alias
        var personalizationDestinations = result.destinations.filter(x => x.alias == "personalizationAlias")
        if(personalizationDestinations.length > 0) {
             // Code to pass the audience IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == "adServerAlias")
        if(adServerDestinations.length > 0) {
            // Code to pass the audience IDs into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

### Voorbeeld van reactie voor [!UICONTROL Custom Personalization With Attributes]

Wanneer u **[!UICONTROL Custom Personalization With Attributes]** De API-reactie zal er ongeveer zo uitzien als in het onderstaande voorbeeld.

Het verschil tussen **[!UICONTROL Custom Personalization With Attributes]** en **[!UICONTROL Custom Personalization]** is de opname van `attributes` in de API-reactie.

```json
[
    {
        "type": "profileLookup",
        "destinationId": "7bb4cb8d-8c2e-4450-871d-b7824f547130",
        "alias": "personalizationAlias",
        "attributes": {
             "countryCode": {
                   "value" : "DE"
              },
             "membershipStatus": {
                   "value" : "PREMIUM"
              }
         },         
        "segments": [
            {
                "id": "399eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
            },
            {
                "id": "499eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
            }
        ]
    }
]
```

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] dwingt gegevensbeheer af, lees de [Overzicht van gegevensbeheer](../../../data-governance/home.md).
