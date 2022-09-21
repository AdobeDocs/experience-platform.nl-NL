---
title: Gegevensvoorvoegsel voor gegevensverzameling
description: Leer hoe u uw gegevens aan een XDM-gebeurtenisschema (Experience Data Model) toewijst bij het configureren van een gegevensstroom voor Adobe Experience Platform Web en Mobile SDK's.
exl-id: 87a70d56-1093-445c-97a5-b8fa72a28ad0
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '887'
ht-degree: 0%

---

# Gegevensvoorvoegsel voor gegevensverzameling

Data Prep is een Adobe Experience Platform-service waarmee u gegevens kunt toewijzen, transformeren en valideren van en naar [Experience Data Model (XDM)](../../xdm/home.md). Bij het configureren van een Platform ingeschakeld [datastream](./overview.md), kunt u de mogelijkheden van de Prep van Gegevens gebruiken om uw brongegevens aan XDM in kaart te brengen wanneer het verzenden van het naar het Netwerk van de Rand van het Platform.

>[!NOTE]
>
>Raadpleeg de volgende documentatie voor uitgebreide informatie over alle mogelijkheden van Data Prep, inclusief transformatiefuncties voor berekende velden:
>
>* [Overzicht van Data Prep](../../data-prep/home.md)
>* [Toewijzingsfuncties van Data Prep](../../data-prep/functions.md)
>* [Gegevensindelingen verwerken met Data Prep](../../data-prep/data-handling.md)


In deze handleiding wordt uitgelegd hoe u uw gegevens in de gebruikersinterface kunt toewijzen. Als u de stappen wilt volgen, start u het proces voor het maken van een gegevensstroom tot (en met) de [basisconfiguratiestap](./overview.md#create).

Raadpleeg de volgende video voor een snelle demonstratie van het proces Gegevensvoorbereiding voor gegevensverzameling:

>[!VIDEO](https://video.tv.adobe.com/v/342120?quality=12&enable10seconds=on&speedcontrol=on)

## [!UICONTROL Select data] {#select-data}

Selecteren **[!UICONTROL Save and Add Mapping]** na de voltooiing van de basisconfiguratie voor een datastream, en **[!UICONTROL Select data]** wordt weergegeven. Van hier, moet u een steekproefJSON voorwerp verstrekken dat de structuur van de gegevens vertegenwoordigt die u bij het verzenden naar Platform van plan bent.

Als u eigenschappen rechtstreeks vanaf uw gegevenslaag wilt vastleggen, moet het JSON-object één basiseigenschap hebben `data`. De subeigenschappen van de `data` Het object moet vervolgens zo worden samengesteld dat het wordt toegewezen aan de eigenschappen van de gegevenslaag die u wilt vastleggen. Selecteer de onderstaande sectie om een voorbeeld weer te geven van een JSON-object met de juiste indeling `data` hoofdmap.

+++Voorbeeld-JSON-bestand met `data` basis

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

Als u eigenschappen wilt vastleggen van een gegevenselement van een XDM-object, zijn dezelfde regels van toepassing op het JSON-object, maar moet de eigenschap root worden ingesteld op `xdm` in plaats daarvan. Selecteer de onderstaande sectie om een voorbeeld weer te geven van een JSON-object met de juiste indeling `xdm` hoofdmap.

+++Voorbeeld-JSON-bestand met `xdm` basis

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

U kunt de optie selecteren om het object als een bestand te uploaden of het onbewerkte object in het tekstvak dat wordt weergegeven plakken. Als de JSON geldig is, wordt een voorvertoningsschema weergegeven in het rechterdeelvenster. Selecteren **[!UICONTROL Next]** om door te gaan.

![JSON-voorbeeld van verwachte binnenkomende gegevens](../images/datastreams/data-prep/select-data.png)

## [!UICONTROL Mapping]

De **[!UICONTROL Mapping]** wordt weergegeven, zodat u de velden in uw brongegevens kunt toewijzen aan die van het doelgebeurtenisschema in Platform. Van hier, kunt u de afbeelding op twee manieren vormen:

* [Nieuwe toewijzingsregels maken](#create-mapping) voor deze gegevensstroom door middel van een handmatig proces.
* [Toewijzingsregels importeren](#import-mapping) uit een bestaande gegevensstroom.

### Nieuwe toewijzing maken {#create-mapping}

Selecteer **[!UICONTROL Add new mapping]** om een nieuwe toewijzingsrij te maken.

![Nieuwe toewijzing toevoegen](../images/datastreams/data-prep/add-new-mapping.png)

Selecteer het bronpictogram (![Bronpictogram](../images/datastreams/data-prep/source-icon.png)) en selecteert u in het dialoogvenster dat wordt weergegeven het bronveld dat u wilt toewijzen in het beschikbare canvas. Als u een veld hebt gekozen, gebruikt u de opdracht **[!UICONTROL Select]** om door te gaan.

![Het veld selecteren dat moet worden toegewezen in het bronschema](../images/datastreams/data-prep/source-mapping.png)

Selecteer vervolgens het schemapictogram (![Schema, pictogram](../images/datastreams/data-prep/schema-icon.png)) om een vergelijkbaar dialoogvenster voor het doelgebeurtenisschema te openen. Kies het veld waaraan u de gegevens wilt toewijzen voordat u bevestigt met **[!UICONTROL Select]**.

![Het veld selecteren dat moet worden toegewezen in het doelschema](../images/datastreams/data-prep/target-mapping.png)

De toewijzingspagina wordt opnieuw weergegeven met de voltooide veldtoewijzing weergegeven. De **[!UICONTROL Mapping progress]** sectie wordt bijgewerkt met het totale aantal velden dat is toegewezen.

![Veld is toegewezen met voortgang weergegeven](../images/datastreams/data-prep/field-mapped.png)

>[!TIP]
>
>Als u een array van objecten (in het bronveld) wilt toewijzen aan een array van verschillende objecten (in het doelveld), voegt u `[*]` na de arraynaam in de bron- en doelveldpaden, zoals hieronder wordt weergegeven.
>
>![Array-objecttoewijzing](../images/datastreams/data-prep/array-object-mapping.png)

### Bestaande toewijzingsregels importeren {#import-mapping}

Als u eerder een gegevensstroom hebt gecreeerd, kunt u zijn gevormde toewijzingsregels voor een nieuwe gegevensstroom opnieuw gebruiken.

>[!WARNING]
>
>Als u toewijzingsregels uit een andere gegevensstroom importeert, worden alle veldtoewijzingen die u vóór het importeren hebt toegevoegd, overschreven.

Selecteer **[!UICONTROL Import Mapping]**.

![Afbeelding die de [!UICONTROL Import Mapping] knop die wordt geselecteerd](../images/datastreams/data-prep/import-mapping-button.png)

Selecteer in het dialoogvenster dat wordt weergegeven de gegevensstroom waarvan u de toewijzingsregels wilt importeren. Wanneer de gegevensstroom is gekozen, selecteert u **[!UICONTROL Preview]**.

![Afbeelding met een bestaande gegevensstroom die wordt geselecteerd](../images/datastreams/data-prep/select-mapping-rules.png)

>[!NOTE]
>
>Gegevensstromen kunnen alleen worden geïmporteerd binnen dezelfde [sandbox](../../sandboxes/home.md). Met andere woorden, u kunt geen gegevensstroom van één zandbak in een andere invoeren.

In het volgende scherm ziet u een voorvertoning van de opgeslagen toewijzingsregels voor de geselecteerde gegevensstroom. Zorg ervoor dat de weergegeven toewijzingen zijn wat u verwacht en selecteer **[!UICONTROL Import]** om de toewijzingen aan de nieuwe gegevensstroom te bevestigen en toe te voegen.

![Afbeelding met de toewijzingsregels die moeten worden geïmporteerd](../images/datastreams/data-prep/import-mapping-rules.png)

>[!NOTE]
>
>Als een bronveld in de geïmporteerde toewijzingsregels niet is opgenomen in de JSON-voorbeeldgegevens die u opgeeft [eerder verstrekt](#select-data), worden deze veldtoewijzingen niet opgenomen in de importbewerking.

### De toewijzing voltooien

Ga verder met de bovenstaande stappen om de overige velden toe te wijzen aan het doelschema. Hoewel u niet alle beschikbare brongebieden moet in kaart brengen, om het even welke gebieden in het doelschema die zoals vereist worden geplaatst moeten worden in kaart gebracht om deze stap te voltooien. De **[!UICONTROL Required fields]** teller geeft aan hoeveel vereiste velden nog niet zijn toegewezen in de huidige configuratie.

Als het aantal vereiste velden nul bereikt en u tevreden bent met de toewijzing, selecteert u **[!UICONTROL Save]** om uw wijzigingen te voltooien.

![Toewijzing voltooid](../images/datastreams/data-prep/mapping-complete.png)

## Volgende stappen

In deze handleiding wordt beschreven hoe u uw gegevens aan XDM kunt toewijzen bij het instellen van een gegevensstroom in de gebruikersinterface. Als u de algemene zelfstudie voor gegevensstromen hebt gevolgd, kunt u nu terugkeren naar de volgende stap [gegevensstroomdetails weergeven](./overview.md).
