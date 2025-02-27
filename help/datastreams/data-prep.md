---
title: Gegevensvoorvoegsel voor gegevensverzameling
description: Leer hoe u uw gegevens aan een XDM-gebeurtenisschema (Experience Data Model) toewijst bij het configureren van een gegevensstroom voor Adobe Experience Platform Web en Mobile SDK's.
exl-id: 87a70d56-1093-445c-97a5-b8fa72a28ad0
source-git-commit: e90bd5abe502a7638ae54fca5eb0f051a925a2d8
workflow-type: tm+mt
source-wordcount: '1171'
ht-degree: 0%

---

# Gegevensvoorvoegsel voor gegevensverzameling

Prep van gegevens is de dienst van Adobe Experience Platform die u toestaat om, gegevens in kaart te brengen en te bevestigen aan en van [ het Model van Gegevens van de Ervaring (XDM) ](../xdm/home.md). Wanneer het vormen van een platform-toegelaten [ datastream ](./overview.md), kunt u de mogelijkheden van de Prep van Gegevens gebruiken om uw brongegevens aan XDM in kaart te brengen wanneer het verzenden van het naar Platform Edge Network.

Alle gegevens die vanaf een webpagina worden verzonden, moeten in Experience Platform als XDM worden geland. Er zijn drie manieren om gegevens van een op pagina gegevenslaag te vertalen naar de XDM die door Experience Platform wordt geaccepteerd:

1. Hervorm de gegevenslaag in XDM op de Web-pagina zelf.
2. Met de functionaliteit voor eigen gegevenselementen van tags kunt u de bestaande indeling van een webpagina voor gegevenslagen opnieuw opmaken in XDM.
3. De bestaande indeling van een gegevenslaag van een webpagina via de Edge Network opnieuw indelen in XDM, met Data Prep voor gegevensverzameling.

Deze handleiding is gericht op de derde optie.

## Wanneer wordt Data Prep gebruikt voor gegevensverzameling {#when-to-use-data-prep}

Er zijn twee gebruiksgevallen waarin Data Prep voor gegevensverzameling nuttig is:

1. De website heeft een goed gevormde, bestuurde en onderhouden gegevenslaag en er is een voorkeur voor het rechtstreeks naar de Edge Network verzenden van de laag in plaats van JavaScript-bewerking te gebruiken om de laag om te zetten in XDM op de pagina (ofwel via de gegevenselementen van tags of via handmatige JavaScript-manipulatie).
2. Op de site wordt een ander coderingssysteem dan Tags geïmplementeerd.

## Een bestaande gegevenslaag via WebSDK naar de Edge Network verzenden {#send-datalayer-via-websdk}

De bestaande gegevenslaag moet worden verzonden met het object [`data`](/help/web-sdk/commands/sendevent/data.md) binnen de opdracht `sendEvent` .

Als u Markeringen gebruikt, moet u het **[!UICONTROL Data]** gebied van het **[!UICONTROL Send Event]** actietype gebruiken, zoals die in de [ documentatie van de de marktextensie van SDK van het Web ](/help/tags/extensions/client/web-sdk/action-types.md) wordt beschreven.

De rest van deze gids zal zich op hoe te om de gegevenslaag aan normen in kaart te brengen XDM nadat het door WebSDK is verzonden.

>[!NOTE]
>
>Raadpleeg de volgende documentatie voor uitgebreide informatie over alle mogelijkheden van Data Prep, inclusief transformatiefuncties voor berekende velden:
>
>* [ Prep overzicht van Gegevens ](../data-prep/home.md)
>* [ de kaartfuncties van de Prep van Gegevens ](../data-prep/functions.md)
>* [ Behandelend gegevensformaten met Gegevens prep ](../data-prep/data-handling.md)

In deze handleiding wordt uitgelegd hoe u uw gegevens in de gebruikersinterface kunt toewijzen. Om samen met de stappen te volgen, begin het proces om een datastream tot (en met inbegrip van) de [ basisconfiguratiestap ](./overview.md#create) tot stand te brengen.

Raadpleeg de volgende video voor een snelle demonstratie van het proces Gegevensvoorbereiding voor gegevensverzameling:

>[!VIDEO](https://video.tv.adobe.com/v/342120?quality=12&enable10seconds=on&speedcontrol=on)

## [!UICONTROL Select data] {#select-data}

Selecteer **[!UICONTROL Save and Add Mapping]** nadat u de basisconfiguratie voor een gegevensstroom hebt voltooid en de stap **[!UICONTROL Select data]** wordt weergegeven. Van hier, moet u een steekproefJSON voorwerp verstrekken dat de structuur van de gegevens vertegenwoordigt die u bij het verzenden naar Platform van plan bent.

Als u eigenschappen rechtstreeks vanaf uw gegevenslaag wilt vastleggen, moet het JSON-object één basiseigenschap `data` hebben. De subeigenschappen van het `data` -object moeten vervolgens zo worden geconstrueerd dat ze zijn toegewezen aan de eigenschappen van de gegevenslaag die u wilt vastleggen. Selecteer de onderstaande sectie om een voorbeeld weer te geven van een JSON-object met de juiste opmaak en een `data` root.

+++JSON-voorbeeldbestand met `data` hoofdmap

```json
{
  "data": {
    "eventMergeId": "cce1b53c-571f-4f36-b3c1-153d85be6602",
    "eventType": "view:load",
    "timestamp": "2021-09-30T14:50:09.604Z",
    "web": {
      "webPageDetails": {
        "siteSection": "Product section",
        "server": "example.com",
        "name": "product home",
        "URL": "https://www.example.com"
      },
      "webReferrer": {
        "URL": "https://www.adobe.com/index2.html",
        "type": "external"
      }
    },
    "commerce": {
      "purchase": 1,
      "order": {
        "orderID": "1234"
      }
    },
    "product": [
      {
        "productInfo": {
          "productID": "123"
        }
      },
      {
        "productInfo": {
          "productID": "1234"
        }
      }
    ],
    "reservation": {
      "id": "anc45123xlm",
      "name": "Embassy Suits",
      "SKU": "12345-L",
      "skuVariant": "12345-LG-R",
      "priceTotal": "112.99",
      "currencyCode": "USD",
      "adults": 2,
      "children": 3,
      "productAddMethod": "PDP",
      "_namespace": {
        "test": 1,
        "priceTotal": "112.99",
        "category": "Overnight Stay"
      },
      "freeCancellation": false,
      "cancellationFee": 20,
      "refundable": true
    }
  }
}
```

+++

Als u eigenschappen van een XDM-objectelement wilt vastleggen, zijn dezelfde regels van toepassing op het JSON-object, maar in plaats daarvan moet de eigenschap root worden ingesteld op `xdm` . Selecteer de onderstaande sectie om een voorbeeld weer te geven van een JSON-object met de juiste indeling en de hoofdmap van `xdm` .

+++JSON-voorbeeldbestand met `xdm` hoofdmap

```json
{
  "xdm": {
    "environment": {
      "type": "browser",
      "browserDetails": {
        "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_5) AppleWebkit/537.36 (KHTML, like Gecko) Chrome/49.0.2623.112 Safari/537.36",
        "javaScriptEnabled": true,
        "javaScriptVersion": "1.8.5",
        "cookiesEnabled": true,
        "viewportHeight": 900,
        "viewportWidth": 1680,
        "javaEnabled": true
      },
      "domain": "adobe.com",
      "colorDepth": 24,
      "viewportHeight": 1050,
      "viewportWidth": 1680
    },
    "device": {
      "screenHeight": 1050,
      "screenWidth": 1680
    }
  }
}
```

+++

U kunt de optie selecteren om het object als een bestand te uploaden of het onbewerkte object in het tekstvak dat wordt weergegeven plakken. Als de JSON geldig is, wordt een voorvertoningsschema weergegeven in het rechterdeelvenster. Selecteer **[!UICONTROL Next]** om door te gaan.

![ JSON steekproef van verwachte inkomende gegevens.](assets/data-prep/select-data.png)

>[!NOTE]
>
> Gebruik een voorbeeld-JSON-object dat elk element in een gegevenslaag vertegenwoordigt dat op elke pagina kan worden gebruikt. Niet alle pagina&#39;s gebruiken bijvoorbeeld de gegevenslaagelementen van winkelwagentjes. De elementen voor de laag met winkelwagengegevens moeten echter wel worden opgenomen in dit voorbeeld van het JSON-object.

## [!UICONTROL Mapping]

De stap **[!UICONTROL Mapping]** wordt weergegeven, zodat u de velden in uw brongegevens kunt toewijzen aan die van het doelgebeurtenisschema in Platform. Van hier, kunt u de afbeelding op twee manieren vormen:

* [ creeer toewijzingsregels ](#create-mapping) voor deze gegevensstroom door een handproces.
* [ de toewijzingsregels van de Invoer ](#import-mapping) van een bestaande datastream.

>[!IMPORTANT]
>
>Gegevensprep-toewijzing heeft voorrang op `identityMap` XDM-ladingen, wat invloed kan hebben op profielovereenkomsten met Real-Time CDP-doelgroepen.

### Toewijzingsregels maken {#create-mapping}

Selecteer **[!UICONTROL Add new mapping]** om een toewijzingsregel te maken.

![ Toevoegend een nieuwe afbeelding.](assets/data-prep/add-new-mapping.png)

Selecteer het bronpictogram (![ het pictogram van Source ](/help/images/icons/source.png)), en in de dialoog die verschijnt selecteer het brongebied dat u in kaart wilt brengen in het verstrekte canvas. Nadat u een veld hebt gekozen, drukt u op de knop **[!UICONTROL Select]** om door te gaan.

![ Selecterend het gebied dat in het bronschema moet worden in kaart gebracht.](assets/data-prep/source-mapping.png)

Daarna, selecteer het schemapictogram (![ pictogram van het Schema ](/help/images/icons/schema.png)) om een gelijkaardige dialoog voor het schema van de doelgebeurtenis te openen. Kies het veld waaraan u de gegevens wilt toewijzen voordat u bevestigt met **[!UICONTROL Select]** .

![ Selecterend het gebied dat in het doelschema moet worden in kaart gebracht.](assets/data-prep/target-mapping.png)

De toewijzingspagina wordt opnieuw weergegeven met de voltooide veldtoewijzing weergegeven. De sectie **[!UICONTROL Mapping progress]** wordt bijgewerkt op basis van het totale aantal velden dat is toegewezen.

![ Gebied met succes in kaart gebracht met weerspiegelde vooruitgang.](assets/data-prep/field-mapped.png)

>[!TIP]
>
>Als u een array van objecten (in het bronveld) wilt toewijzen aan een array van verschillende objecten (in het doelveld), voegt u `[*]` toe na de arraynaam in de bron- en doelveldpaden, zoals hieronder wordt weergegeven.
>
>![ de objecten van de Serie afbeelding.](assets/data-prep/array-object-mapping.png)

### Bestaande toewijzingsregels importeren {#import-mapping}

Als u eerder een gegevensstroom hebt gecreeerd, kunt u zijn gevormde toewijzingsregels voor een nieuwe gegevensstroom opnieuw gebruiken.

>[!WARNING]
>
>Als u toewijzingsregels uit een andere gegevensstroom importeert, worden alle veldtoewijzingen die u vóór het importeren hebt toegevoegd, overschreven.

Selecteer **[!UICONTROL Import Mapping]** om te beginnen.

![ de knoop die van de Toewijzing van de Invoer wordt geselecteerd.](assets/data-prep/import-mapping-button.png)

Selecteer in het dialoogvenster dat wordt weergegeven de gegevensstroom waarvan u de toewijzingsregels wilt importeren. Wanneer de gegevensstroom is gekozen, selecteert u **[!UICONTROL Preview]** .

![ Selecterend een bestaande gegevensstroom.](assets/data-prep/select-mapping-rules.png)

>[!NOTE]
>
>De stromen van gegevens kunnen slechts binnen de zelfde [ zandbak ](../sandboxes/home.md) worden ingevoerd. Met andere woorden, u kunt geen gegevensstroom van één zandbak in een andere invoeren.

In het volgende scherm ziet u een voorvertoning van de opgeslagen toewijzingsregels voor de geselecteerde gegevensstroom. Zorg ervoor dat de weergegeven toewijzingen zijn wat u verwacht en selecteer vervolgens **[!UICONTROL Import]** om de toewijzingen te bevestigen en toe te voegen aan de nieuwe gegevensstroom.

![ de regels van de Afbeelding die moeten worden ingevoerd.](assets/data-prep/import-mapping-rules.png)

>[!NOTE]
>
>Als om het even welke brongebieden in de ingevoerde kaartregels niet inbegrepen in de steekproefJSON gegevens zijn die u [ vroeger ](#select-data) verstrekte, zullen die gebiedsafbeeldingen niet in de invoer inbegrepen zijn.

### De toewijzing voltooien

Ga verder met de bovenstaande stappen om de rest van de velden toe te wijzen aan het doelschema. Hoewel u niet alle beschikbare brongebieden moet in kaart brengen, om het even welke gebieden in het doelschema die zoals vereist worden geplaatst moeten worden in kaart gebracht om deze stap te voltooien. De teller **[!UICONTROL Required fields]** geeft aan hoeveel vereiste velden nog niet zijn toegewezen in de huidige configuratie.

Als het vereiste aantal velden nul heeft bereikt en u tevreden bent met de toewijzing, selecteert u **[!UICONTROL Save]** om de wijzigingen te voltooien.

![ Volledige Afbeelding van de afbeelding ](assets/data-prep/mapping-complete.png)

## Volgende stappen

In deze handleiding wordt beschreven hoe u uw gegevens aan XDM kunt toewijzen bij het instellen van een gegevensstroom in de gebruikersinterface. Als u algemene datastreams leerprogramma volgde, kunt u aan de stap op [ nu terugkeren het bekijken van datastreamdetails ](./overview.md).
