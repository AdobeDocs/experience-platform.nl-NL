---
title: Google Data Layer Extension
description: Meer informatie over de tagextensie Google Client Data Layer in Adobe Experience Platform.
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 0%

---

# Google Data Layer extension (bèta)

>[!IMPORTANT]
>
>Deze extensie is momenteel in bèta en is nog niet volledig getest in productie.

Met de extensie Google-gegevenslaag kunt u een Google-gegevenslaag gebruiken in de implementatie van tags. De extensie kan onafhankelijk of gelijktijdig worden gebruikt met Google-oplossingen en met open source uit Google [Helpbibliotheek gegevenslaag](https://github.com/google/data-layer-helper).

De Helper Library biedt functionaliteit die door gebeurtenissen wordt aangestuurd en die vergelijkbaar is met die van de Adobe Client Data Dayer (ACDL). De gegevenselementen, regels en handelingen van de extensie Google Data Layer bieden vergelijkbare functionaliteit als in de [ACDL-extensie](../client-data-layer/overview.md).

## Looptijd

Versie 1.0.x van de extensie is een bètaversie. Deze uitbreiding is niet volledig getest in productie.

## Installatie

Als u de extensie wilt installeren, navigeert u naar de extensiecatalogus in de gebruikersinterface van het Experience Platform of de gebruikersinterface van de gegevensverzameling en selecteert u **Google-gegevenslaag**.

Nadat de extensie is geïnstalleerd, wordt elke keer dat de tagbibliotheek op uw website wordt geladen, een gegevenslaag gemaakt of geopend.

## Extensieweergave

Wanneer u de extensie configureert (tijdens de installatie van de extensie of door **[!UICONTROL Configure]** in de extensiecatalogus) moet u de naam definiëren van de gegevenslaag die de extensie gebruikt. Als er geen gegevenslaag met de geconfigureerde naam aanwezig is wanneer de bibliotheek wordt geladen, maakt de extensie er een.

>[!NOTE]
>
>Het maakt niet uit of Google- of Adobe-code het eerst wordt geladen en dat de gegevenslaag wordt gemaakt. Beide systemen zullen tot de gegevenslaag leiden indien niet aanwezig, of gebruiken de bestaande gegevenslaag.

Standaard gebruikt de gegevenslaag de Google-standaardnaam `dataLayer`.

## Gebeurtenissen

Met de extensie kunt u luisteren naar wijzigingen (gebeurtenissen) in de gegevenslaag. Een gebeurtenis kan een van de volgende zijn:

* Taggebeurtenissen (zoals een bibliotheek die wordt geladen)
* JavaScript-gebeurtenissen
* Gegevens die met de `event` trefwoord.

Het is belangrijk om het gebruik van het [`event` trefwoord](https://developers.google.com/tag-platform/devguides/datalayer#use_a_data_layer_with_event_handlers) wanneer de gegevens aan een de gegevenslaag van Google, gelijkaardig aan de Laag van de Gegevens van de Cliënt van Adobe worden geduwd. De `event` trefwoord wijzigt het gedrag van de Google-gegevenslaag en het gedrag van de extensie wordt daarom dienovereenkomstig bijgewerkt.

In de onderstaande secties worden de verschillende gebeurtenistypen beschreven waarnaar de extensie kan luisteren.

### Luisteren naar alle markeringen op de gegevenslaag

Als u deze optie selecteert, luistert de extensie naar elke wijziging die in de gegevenslaag wordt aangebracht.

### Luisteren naar pushberichten, gebeurtenissen uitsluiten

Als u deze optie selecteert, luistert de extensie naar alles wat naar de gegevenslaag wordt geduwd, met uitzondering van gebeurtenissen.

De volgende voorbeeldpushgebeurtenis wordt door de listener bijgehouden:

```js
dataLayer.push({"data":"something"})
```

De volgende voorbeeldpushgebeurtenissen worden niet door de listener bijgehouden:

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

### Luisteren naar alle gebeurtenissen

Als u deze optie selecteert, luistert de extensie naar gebeurtenissen die naar de gegevenslaag worden geduwd.

De volgende voorbeeldpushgebeurtenissen worden door de listener bijgehouden:

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

De volgende voorbeeldpushgebeurtenis wordt niet door de listener bijgehouden:

```js
dataLayer.push({"data":"something"})
```

### Luisteren naar specifieke gebeurtenis

Als u naar een specifieke gebeurtenis wilt luisteren, selecteert u deze optie zodat de gebeurtenislistener gebeurtenissen bijhoudt die overeenkomen met een specifieke tekenreeks.

Stel bijvoorbeeld `myEvent` wanneer u deze configuratie gebruikt, wordt in de listener alleen de volgende pushgebeurtenis bijgehouden:

```js
dataLayer.push({"event":"myEvent"})
```

U kunt ook een regex-tekenreeks gebruiken om namen van gebeurtenissen aan te passen. Stel bijvoorbeeld `myEvent\d` zou gebeurtenissen volgen die beginnen met `myEvent` gevolgd door een cijfer:

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## Acties

In de volgende secties worden de verschillende acties beschreven die de extensie kan uitvoeren wanneer deze deel uitmaakt van een [regel](../../../ui/managing-resources/rules.md).

### Naar gegevenslaag duwen {#push-to-data-layer}

Met deze actie wordt JSON-inhoud naar de gegevenslaag zelf verplaatst, zodat gegevenselementen rechtstreeks in JSON-ladingen kunnen worden gebruikt. Binnen de verstrekte redacteur JSON, kunt u gegevenselementen van verwijzingen voorzien gebruikend percentenaantekening (bijvoorbeeld `%dataElementName%`).

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

### Google DL Herstellen naar computerstatus

>[!NOTE]
>
>Deze actie is beschikbaar vanaf v1.0.5.

Met deze handeling wordt de gegevenslaag opnieuw ingesteld. Indien gebruikt in een regel die een verandering van de gegevenslaag van Google verwerkt, wordt de gegevenslaag teruggesteld aan de gegevens verwerkte staat van de gegevenslaag op het tijdstip dat de regel werd teweeggebracht. Als de handeling wordt gebruikt in een regel die geen wijziging in een Google-gegevenslaag verwerkt, wordt de gegevenslaag gewist door de handeling.

## Gegevenselementen

De extensie biedt een uniek gegevenselement dat de gegevenslaag benadert met behulp van een sleutel (bijvoorbeeld `page.url` in de [fragment boven](#push-to-data-layer)).

Het gegevenselement kan het volgende bieden:

* Een specifieke waarde uit de gegevenslaag (bijvoorbeeld `page.url`)
* De volledige array met gegevenslagen (leeg veld toets)
* Waarden van een gegevenslaaggebeurtenis met de toets (als de `event` trefwoord gebruikt)
* Het gehele gebeurtenisobject (leeg toetsveld)

De extensie geeft altijd prioriteit aan gebeurtenisinformatie. Als een gegevenslaag `event` worden verwerkt, worden waarden altijd gelezen van die gebeurtenis. Als een `event` niet aanwezig is, worden de waarden gelezen van de directe gegevenslaag.

## Aanvullende informatie

Aanvullende informatie is beschikbaar in het dialoogvenster [project README](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md) en in de dialoogvensters voor gegevenselementen en gebeurtenissen van de extensie.
