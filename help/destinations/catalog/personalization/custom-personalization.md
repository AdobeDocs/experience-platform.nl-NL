---
keywords: aangepaste personalisatie; bestemming; ervaring met aangepaste bestemming van platform;
title: Aangepaste verpersoonlijkingsverbinding
description: Deze bestemming verstrekt externe verpersoonlijking, inhoudsbeheersystemen, en servers, en andere toepassingen die op uw plaats lopen een manier om publieksinformatie van Adobe Experience Platform terug te winnen. Deze bestemming verstrekt verpersoonlijking in real time die op het gebruikersprofiellidmaatschap wordt gebaseerd.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: d252fc30d93fa4440c6ef47146830d0423e1839a
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 1%

---


# Aangepaste verpersoonlijkingsverbinding {#custom-personalization-connection}

## Doelwijziging {#changelog}

| Releasedatum | Type bijwerken | Beschrijving |
|---|---|---|
| Mei 2023 | Bijwerken van functionaliteit en documentatie | Vanaf Mei 2023, steunt de **[!UICONTROL Custom personalization]** verbinding [&#x200B; op attribuut-gebaseerde verpersoonlijking &#x200B;](../../ui/activate-edge-personalization-destinations.md#map-attributes) en is over het algemeen beschikbaar aan alle klanten. |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>Profielkenmerken kunnen vertrouwelijke gegevens bevatten. Om dit gegeven te beschermen, moet u [&#x200B; Edge Network API &#x200B;](https://developer.adobe.com/data-collection-apis/docs/) gebruiken wanneer het vormen van de **[!UICONTROL Custom Personalization]** bestemming voor op attribuut-gebaseerde verpersoonlijking. Alle Edge Network API vraag moet in een [&#x200B; voor authentiek verklaarde context &#x200B;](https://developer.adobe.com/data-collection-apis/docs/getting-started/authentication) worden gemaakt.
>
><br> u kunt profielattributen via [&#x200B; Edge Network API &#x200B;](https://developer.adobe.com/data-collection-apis/docs/) terugwinnen door een server-zijintegratie toe te voegen die de zelfde gegevensstroom gebruikt die u reeds voor uw implementatie van het Web of Mobiele SDK gebruikt.
>
><br> als u niet de hierboven vereisten volgt, zal de verpersoonlijking op publiekslidmaatschap slechts gebaseerd zijn.

## Overzicht {#overview}

Stel deze bestemming in om externe personalisatieplatforms, contentbeheersystemen en servers en andere toepassingen die op websites van klanten worden uitgevoerd, toe te staan om publieksinformatie van Adobe Experience Platform op te halen.

## Vereisten {#prerequisites}

Deze bestemming vereist het gebruik van één van de volgende methodes van de gegevensinzameling, afhankelijk van uw implementatie:

* Gebruik [&#x200B; SDK van het Web van Adobe Experience Platform &#x200B;](/help/collection/js/js-overview.md) als u gegevens van uw website wilt verzamelen.
* Gebruik [&#x200B; Adobe Experience Platform Mobile SDK &#x200B;](https://developer.adobe.com/client-sdks/documentation/) als u gegevens van uw mobiele toepassing wilt verzamelen.
* Gebruik [&#x200B; Edge Network API &#x200B;](https://developer.adobe.com/data-collection-apis/docs/) als u niet het Web SDK of Mobiele SDK gebruikt, of als u de gebruikerservaring wilt personaliseren die op profielattributen wordt gebaseerd.

>[!IMPORTANT]
>
>**op attributen-gebaseerde verpersoonlijkingsvereisten:** Als u gebaseerd op profielattributen (niet alleen publiekslidmaatschap) wilt personaliseren, moet u **&#x200B;**&#x200B;gebruiken [&#x200B; Edge Network API &#x200B;](https://developer.adobe.com/data-collection-apis/docs/) met voor authentiek verklaarde server-zijintegratie, ongeacht of u ook SDK van het Web of Mobiele SDK voor gegevensinzameling gebruikt.
>
>Web SDK en Mobile SDK alleen ondersteunen personalisatie op basis van het lidmaatschap van een publiek. Edge Network API wordt vereist **&#x200B;**&#x200B;om profielattributen voor verpersoonlijking veilig terug te winnen.

>[!IMPORTANT]
>
>Alvorens een verbinding van de douaneverpersoonlijking tot stand te brengen, lees de gids op hoe te [&#x200B; publieksgegevens aan de bestemmingen van de randverpersoonlijking &#x200B;](../../ui/activate-edge-personalization-destinations.md) activeren. Deze handleiding begeleidt u door de vereiste configuratiestappen voor het gebruik van dezelfde pagina en volgende pagina&#39;s voor personalisatie, voor meerdere Experience Platform-componenten.

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#x200B; &#x200B;](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!DNL Profile request]** | U vraagt om alle soorten publiek die voor één profiel zijn toegewezen in de aangepaste verpersoonlijkingsbestemming. De verschillende bestemmingen van de douaneverpersoonlijking kunnen opstelling voor verschillende [&#x200B; de gegevensstromen van de Inzameling van Gegevens van Adobe &#x200B;](../../../datastreams/overview.md) zijn. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations). |

## Verbinden met de bestemming {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Gegevensstromen"
>abstract="Met deze optie bepaalt u in welke gegevensverzamelingsgegevensstroom het publiek wordt opgenomen in het antwoord op de pagina. Het drop-down menu toont slechts gegevensstromen die de toegelaten bestemmingsconfiguratie hebben. U moet een gegevensstroom vormen alvorens u uw bestemming kunt vormen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=nl-NL" text="Leer hoe u een gegevensstroom configureert"

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven.

### Verbindingsparameters {#parameters}

Terwijl [&#x200B; vestiging &#x200B;](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* **[!UICONTROL Name]**: vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Description]**: voer een beschrijving in voor uw doel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken. Dit veld is optioneel.
* **[!UICONTROL Integration alias]**: deze waarde wordt als een JSON-objectnaam verzonden naar de Experience Platform Web SDK.
* **[!UICONTROL Datastream]**: hiermee bepaalt u in welke gegevensstroom voor gegevensverzameling het publiek wordt opgenomen in de reactie op de pagina. Het drop-down menu toont slechts gegevensstromen die de toegelaten bestemmingsconfiguratie hebben. Zie [&#x200B; Vormend een datastream &#x200B;](../../../datastreams/overview.md) voor meer details.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Lees [&#x200B; activeer profielen en de de verpersoonlijkingsbestemmingen van de doelpubliek van de doelgroep &#x200B;](../../ui/activate-edge-personalization-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

## Geëxporteerde gegevens {#exported-data}

Als u [&#x200B; Markeringen in Adobe Experience Platform &#x200B;](/help/tags/home.md) gebruikt om het Web SDK van Experience Platform op te stellen, gebruik [&#x200B; verzendt gebeurtenis volledige &#x200B;](/help/tags/extensions/client/web-sdk/event-types.md) functionaliteit en uw actie van de douanecode zal een `event.destinations` variabele hebben die u kunt gebruiken om de uitgevoerde gegevens te zien.

Hier volgt een voorbeeldwaarde voor de variabele `event.destinations` :

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

Als u niet [&#x200B; Markeringen &#x200B;](/help/tags/home.md) gebruikt om het Web SDK van Experience Platform op te stellen, gebruik [&#x200B; bevelreacties &#x200B;](/help/collection/js/commands/command-responses.md) om de uitgevoerde gegevens te zien.

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

Wanneer u **[!UICONTROL Custom Personalization With Attributes]** gebruikt, ziet de API-reactie eruit zoals in het onderstaande voorbeeld.

Het verschil tussen **[!UICONTROL Custom Personalization With Attributes]** en **[!UICONTROL Custom Personalization]** is de opname van de sectie `attributes` in de API-reactie.

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

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](../../../data-governance/home.md).
