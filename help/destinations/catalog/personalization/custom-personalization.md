---
keywords: aangepaste personalisatie; bestemming; ervaring met aangepaste bestemming van platform;
title: Aangepaste Personalization-verbinding
description: Leer hoe u de aangepaste Personalization-bestemming instelt om publieksgegevens van Adobe Experience Platform op te halen voor realtime on-site personalisatie.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 3779531814cbf7e5718db0ac88aca266f14a1b21
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 1%

---


# Aangepaste Personalization-verbinding {#custom-personalization-connection}

## Doelwijziging {#changelog}

Gebruik deze wijziging om updates bij te houden voor de bestemming Aangepaste Personalization.

| Releasedatum | Type bijwerken | Beschrijving |
| --- | --- | --- |
| Mei 2023 | Bijwerken van functionaliteit en documentatie | Vanaf Mei 2023, steunt de **[!UICONTROL Custom personalization]** verbinding [ op attribuut-gebaseerde verpersoonlijking ](/help/destinations/ui/activate-edge-personalization-destinations.md#map-attributes) en is over het algemeen beschikbaar aan alle klanten. |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>Profielkenmerken kunnen vertrouwelijke gegevens bevatten. Om deze gegevens te beschermen, gebruik [ Edge Network API ](https://developer.adobe.com/data-collection-apis/docs/) wanneer het vormen van de **[!UICONTROL Custom Personalization]** bestemming voor op attribuut-gebaseerde verpersoonlijking. Alle Edge Network API vraag moet in een [ voor authentiek verklaarde context ](https://developer.adobe.com/data-collection-apis/docs/getting-started/authentication) worden gemaakt.
>
>Haal profielattributen via [ Edge Network API ](https://developer.adobe.com/data-collection-apis/docs/) terug door een server-zijintegratie toe te voegen die de zelfde gegevensstroom gebruikt u reeds voor uw implementatie van het Web of Mobiele SDK gebruikt.
>
>Als u de bovenstaande vereisten niet opvolgt, is personalisatie alleen gebaseerd op het lidmaatschap van het publiek.

## Overzicht {#overview}

Stel deze bestemming in zodat externe personalisatieplatforms, contentbeheersystemen en servers en andere toepassingen die op websites van klanten worden uitgevoerd, publieksgegevens kunnen ophalen uit [!DNL Adobe Experience Platform] .

## Vereisten {#prerequisites}

Deze bestemming vereist één van de volgende methodes van de gegevensinzameling, afhankelijk van uw implementatie:

* Gebruik [ SDK van het Web van Adobe Experience Platform ](/help/collection/js/js-overview.md) om gegevens van uw website te verzamelen.
* Gebruik [ Adobe Experience Platform Mobile SDK ](https://developer.adobe.com/client-sdks/documentation/) om gegevens van uw mobiele toepassing te verzamelen.
* Gebruik [ Edge Network API ](https://developer.adobe.com/data-collection-apis/docs/) als u niet het Web SDK of Mobiele SDK gebruikt, of als u de gebruikerservaring wilt personaliseren die op profielattributen wordt gebaseerd.

>[!IMPORTANT]
>
>**op attributen-gebaseerde verpersoonlijkingsvereisten:** om zich te personaliseren gebaseerd op profielattributen (niet alleen publiekslidmaatschap), moet u **** gebruiken [ Edge Network API ](https://developer.adobe.com/data-collection-apis/docs/) met voor authentiek verklaarde server-zijintegratie, ongeacht of u ook SDK van het Web of Mobiele SDK voor gegevensinzameling gebruikt.
>
>Web SDK en Mobile SDK alleen ondersteunen personalisatie op basis van alleen het lidmaatschap van een publiek. Edge Network API wordt vereist **** om profielattributen voor verpersoonlijking veilig terug te winnen.

>[!IMPORTANT]
>
>Alvorens een verbinding van Personalization van de Douane te creëren, lees de gids op hoe te [ publieksgegevens aan de bestemmingen van de randverpersoonlijking ](/help/destinations/ui/activate-edge-personalization-destinations.md) activeren. Deze handleiding begeleidt u door de vereiste configuratiestappen voor het gebruik van dezelfde pagina en volgende pagina&#39;s voor personalisatie, voor meerdere Experience Platform-componenten.

## Ondersteunde doelgroepen {#supported-audiences}

De volgende lijst maakt een lijst van de publiekstypes u naar deze bestemming kunt uitvoeren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [ ](/help/segmentation/home.md). |
| Alle andere doelgroepen | Ja | Deze categorie omvat alle oorsprong van het publiek buiten het publiek dat via [!DNL Segmentation Service] wordt gegenereerd. Lees over de [ diverse publieksoorsprong ](/help/segmentation/ui/audience-portal.md#customize). Voorbeelden zijn: <ul><li>de douane uploadt publiek [ ingevoerde ](/help/segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers,</li><li>gelijksoortige doelgroepen,</li><li>federaal publiek,</li><li>publiek dat wordt gegenereerd in andere Experience Platform-toepassingen, zoals [!DNL Adobe Journey Optimizer] ,</li><li>en meer.</li></ul> |

{style="table-layout:auto"}

Ondersteund publiek per type publieksgegevens:

| Gegevenstype Publiek | Ondersteund | Beschrijving | Gebruiksscenario&#39;s |
|--------------------|-----------|-------------|-----------|
| [ het publiek van Mensen ](/help/segmentation/types/people-audiences.md) | Ja | Doelspecifieke groepen van personen op basis van klantprofielen. | Frequente kopers, winkeliers |
| [ publiek van de Rekening ](/help/segmentation/types/account-audiences.md) | Nee | Doelpersonen binnen specifieke organisaties voor marketingstrategieën op basis van account. | B2B-marketing |
| [ Het publiek van het Vooruitzicht ](/help/segmentation/types/prospect-audiences.md) | Nee | De individuen van het doel die nog geen klanten zijn maar eigenschappen met uw doelpubliek delen. | Waarschuwing met gegevens van derden |
| [ de uitvoer van de Dataset ](/help/catalog/datasets/overview.md) | Nee | Verzamelingen gestructureerde gegevens die zijn opgeslagen in het [!DNL Adobe Experience Platform] Data Lake. | Rapportage, workflows voor gegevenswetenschap |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

In de volgende tabel worden het exporttype en de exportfrequentie voor deze bestemming beschreven.

| Item | Type | Notities |
| --- | --- | --- |
| Exporttype | **[!UICONTROL Profile request]** | Verzoekt alle publiek dat in de bestemming van de Aangepaste Personalization aan één enkel profiel wordt toegewezen. De verschillende bestemmingen van de Douane Personalization kunnen opstelling voor verschillende [ de gegevensstromen van de Inzameling van Gegevens van Adobe ](/help/datastreams/overview.md) zijn. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn altijd op API gebaseerde verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Gegevensstromen"
>abstract="Met deze optie bepaalt u in welke gegevensverzamelingsgegevensstroom het publiek wordt opgenomen in het antwoord op de pagina. Het drop-down menu toont slechts gegevensstromen die de toegelaten bestemmingsconfiguratie hebben. U moet een gegevensstroom vormen alvorens u uw bestemming kunt vormen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html" text="Leer hoe u een gegevensstroom configureert"

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](/help/destinations/ui/connect-destination.md) worden beschreven.

### Verbindingsparameters {#parameters}

Terwijl [ vestiging ](/help/destinations/ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* **[!UICONTROL Name]**: vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Description]**: voer een beschrijving in voor uw doel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken. Dit veld is optioneel.
* **[!UICONTROL Integration alias]**: Een vereiste tekenreeks die deze bestemming identificeert in de verpersoonlijkingsreactie. De aliaswaarde wordt samen met het publiek (en, indien geconfigureerd, de kenmerken) dat aan deze bestemming is gekoppeld, geretourneerd naar uw website of toepassing. Gebruik de alias in uw cliënt-kant of server-zijcode om van het correcte verpersoonlijkingsvoorwerp de plaats te bepalen en te verwerken wanneer de veelvoudige verpersoonlijkingsbestemmingen op de zelfde gegevensstroom actief zijn. De alias moet uniek zijn binnen een sandbox voor alle aangepaste Personalization-doelen.
* **[!UICONTROL Datastream]**: hiermee bepaalt u in welke gegevensstroom voor gegevensverzameling het publiek wordt opgenomen in de reactie op de pagina. Het drop-down menu toont slechts gegevensstromen die de toegelaten bestemmingsconfiguratie hebben. Zie [ Vormend een datastream ](/help/datastreams/overview.md) voor meer details.

### Waarschuwingen inschakelen {#enable-alerts}

Schakel waarschuwingen in om meldingen te ontvangen over de status van uw gegevensstroom naar deze bestemming. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](/help/destinations/ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
>
>Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Lees [ activeer profielen en publiek aan de bestemmingen van de randverpersoonlijking ](/help/destinations/ui/activate-edge-personalization-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

## Geëxporteerde gegevens {#exported-data}

Als u [ Markeringen in Adobe Experience Platform ](/help/tags/home.md) gebruikt om het Web SDK van Experience Platform op te stellen, gebruik [ verzendt gebeurtenis volledige ](/help/tags/extensions/client/web-sdk/event-types.md) functionaliteit. De aangepaste code-actie heeft een `event.destinations` -variabele die u kunt gebruiken om de geëxporteerde gegevens weer te geven.

Hier volgt een voorbeeldwaarde voor de variabele `event.destinations` :

```json
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

Als u niet [ Markeringen ](/help/tags/home.md) gebruikt om het Web SDK van Experience Platform op te stellen, gebruik [ bevelreacties ](/help/collection/js/commands/command-responses.md) om de uitgevoerde gegevens te zien.

Analyseer het JSON-antwoord van [!DNL Adobe Experience Platform] om de alias voor integratie te zoeken van de toepassing die u integreert met [!DNL Adobe Experience Platform] . Geef de gebruikers-id&#39;s als doelparameters door aan de code van de toepassing. Hieronder ziet u een voorbeeld van hoe dit er specifiek uitziet voor de doelrespons.

```js
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

### Voorbeeld van reactie voor Aangepaste Personalization met kenmerken {#example-response-attributes}

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

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [ overzicht van het Beleid van Gegevens ](/help/data-governance/home.md).
