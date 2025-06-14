---
title: Google Data Layer Extension
description: Meer informatie over de tagextensie Google Client Data Layer in Adobe Experience Platform.
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: c61afdc2c3df98a0ef815d7cb034ba2907c52908
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 0%

---

# Google Data Layer-extensie

Met de extensie Google-gegevenslaag kunt u een Google-gegevenslaag gebruiken in de implementatie van Tags. De uitbreiding kan onafhankelijk of gelijktijdig met de oplossingen van Google en met Google worden gebruikt open bron [ de Bibliotheek van de Helper van de Laag van Gegevens 0&rbrace; ](https://github.com/google/data-layer-helper).

De Helperbibliotheek verstrekt gelijkaardige gebeurtenis-gedreven functionaliteit aan de Laag van de Gegevens van de Cliënt van de Adobe (ACDL). De gegevenselementen, de regels, en de acties van de uitbreiding van de Laag van de Gegevens van Google verstrekken gelijkaardige functionaliteit aan die in de [ uitbreiding ACDL ](../client-data-layer/overview.md).

## Installatie

Als u de extensie wilt installeren, navigeert u naar de extensiecatalogus in de gebruikersinterface voor gegevensverzameling en selecteert u **[!UICONTROL Google Data Layer]** .

Nadat de extensie is geïnstalleerd, wordt een gegevenslaag gemaakt of geopend bij elke keer dat de Adobe Experience Platform-tagbibliotheek wordt geladen.

## Extensieweergave

De extensieconfiguratie kan worden gebruikt om de naam te definiëren van de gegevenslaag die de extensie gebruikt. Als geen gegevenslaag met de gevormde naam aanwezig is wanneer de Markeringen van Adobe Experience Platform wordt geladen, leidt de uitbreiding tot één.

De standaardinstelling voor de naam van de gegevenslaag is de Google-standaardnaam `dataLayer` .

>[!NOTE]
>
>Het maakt niet uit of Google- of Adobe-code het eerst wordt geladen en of de gegevenslaag wordt gemaakt. Beide systemen gedragen zich het zelfde - creeer de gegevenslaag als het niet aanwezig is of gebruik de bestaande gegevenslaag.

## Gebeurtenissen

>[!NOTE]
>
>Het woord _gebeurtenis_ wordt overbelast wanneer een gebeurtenis-gedreven gegevenslaag in de Markeringen van Adobe Experience Platform wordt gebruikt. _Gebeurtenissen_ kunnen zijn:
> - Gebeurtenissen van Adobe Experience Platform-tags (Bibliotheek geladen enzovoort).
> - JavaScript-gebeurtenissen.
> - Gegevens die aan de gegevenslaag met het _worden geduwd gebeurtenis_ sleutelwoord.

De extensie biedt u de mogelijkheid te luisteren naar wijzigingen in de gegevenslaag.

>[!NOTE]
>
>Het is belangrijk om het gebruik van het _gebeurtenis_ sleutelwoord te begrijpen wanneer het gegeven aan een de gegevenslaag van Google wordt geduwd, gelijkaardig aan de Laag van de Gegevens van de Cliënt van de Adobe. Het _gebeurtenis_ sleutelwoord verandert het gedrag van de de gegevenslaag van Google en daarom deze uitbreiding.\
> Lees de documentatie van Google of doe onderzoek als u op dit punt onzeker bent.

### Google-gebeurtenistypen

Google ondersteunt twee manieren om gebeurtenissen te verdringen: Google Tag Manager, met de methode `push()` en Googles Analytics 4, met de methode `gtag()` .

Google Data Layer extension versions before 1.2.1 supported only events created by `push()`, as displayed in the code examples on this page.

Versies 1.2.1 en hoger ondersteunen gebeurtenissen die met `gtag()` zijn gemaakt.  Dit is optioneel en kan worden ingeschakeld in het dialoogvenster voor extensieconfiguratie.

Voor meer informatie over `push()` en `gtag()` gebeurtenissen, zie de [ documentatie van Google ](https://developers.google.com/analytics/devguides/collection/ga4/reference/events?client_type=gtag).  De informatie wordt ook verstrekt in de configuratie en regeldialogen van de uitbreiding.

### Luisteren naar alle markeringen op de gegevenslaag

Als u deze optie selecteert, luistert uw gebeurtenislistener naar elke wijziging die in de gegevenslaag is aangebracht.

### Luisteren naar pushberichten, gebeurtenissen uitsluiten

Als u deze optie selecteert, luistert uw gebeurtenislistener naar een willekeurige druk op de gegevens in de gegevenslaag, gebeurtenissen niet inbegrepen.

De volgende voorbeeldpushgebeurtenissen worden door de listener bijgehouden:

```js
dataLayer.push({"data":"something"})
```

De volgende voorbeeldpushgebeurtenissen worden niet door de listener bijgehouden:

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

### Luisteren naar alle gebeurtenissen

Als u deze optie selecteert, luistert uw gebeurtenislistener naar elke gebeurtenis die naar de gegevenslaag wordt geduwd.

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

Als u een gebeurtenis opgeeft, houdt de gebeurtenislistener alle gebeurtenissen bij die overeenkomen met een bepaalde tekenreeks.

Als u bijvoorbeeld `myEvent` instelt wanneer u deze configuratie gebruikt, wordt in de listener alleen de volgende pushgebeurtenis gevolgd:

```js
dataLayer.push({"event":"myEvent"})
```

Een regex (ECMAScript / JavaScript) kan worden gebruikt om gebeurtenisnamen aan te passen.

Als u bijvoorbeeld &#39;myEvent\d&#39; instelt, wordt `myEvent` gevolgd door een cijfer (\d):

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## Acties

### Naar gegevenslaag duwen {#push-to-data-layer}

De extensie biedt u twee acties om JSON naar de gegevenslaag te duwen, een vrij tekstveld om handmatig de JSON te maken die moet worden geduwd en een sleutelwaardevenster van versie 1.2.0.

#### Vrije tekst JSON

Met de actie Vrije tekst kunt u gegevenselementen rechtstreeks in de JSON gebruiken. Binnen de redacteur JSON, gegevenselementen zouden moeten worden van verwijzingen voorzien gebruikend percentenaantekening. Bijvoorbeeld `%dataElementName%` .

```json
{
  "page": {
    "url": "%url%",
    "previous_url": "%previous_url%",
    "concatenated_values": "static string %dataElement%"
  }
}
```

#### Sleutelwaarde multifield

De nieuwere zeer belangrijke multifield dialoog is een gebruikersvriendelijker interface die een duw om toestaat worden gevormd zonder JSON manueel te schrijven.

### Google DL Herstellen naar computerstatus

De extensie biedt u een handeling om de gegevenslaag opnieuw in te stellen. Indien gebruikt in een regel die een verandering van de gegevenslaag van Google verwerkt, wordt de gegevenslaag teruggesteld aan de gegevens verwerkte staat van de gegevenslaag op het tijdstip dat de regel werd teweeggebracht. Als de handeling wordt gebruikt in een regel die geen wijziging in een Google-gegevenslaag verwerkt, wordt de gegevenslaag gewist door de handeling.

## Gegevenselementen

Het opgegeven gegevenselement kan worden gebruikt tijdens de uitvoering van een regel die wordt geactiveerd door een wijziging in de Google-gegevenslaag (push-gebeurtenis) of in een niet-gerelateerde regel zoals Bibliotheek geladen. In het eerste geval retourneert het gegevenselement een waarde die is ontleend aan de berekende status op het moment van de wijziging van de gegevenslaag. In het laatste geval wordt de berekende status op het tijdstip van de uitvoering van de regel gebruikt.

Een knevelschakelaar staat u toe om te selecteren of het gegevenselement waarden van de volledige gegevens verwerkte staat, of slechts van gebeurtenisinformatie zou moeten terugkeren (als gebruikt in een regel die door een verandering van de gegevenslaag wordt teweeggebracht).

Het gegevenselement kan daarom worden geretourneerd:

- Leeg veld: toestand van gegevenslaag berekend.
- Veld met sleutel (zoals page.previous_url in het bovenstaande voorbeeld): waarde van de sleutel in het gebeurtenisobject of de berekende status.

## Aanvullende informatie

Het gegevenselement en de gebeurtenisdialoogvensters van de extensie bevatten gedetailleerde gebruiksinformatie en voorbeelden.

De extra algemene informatie is in [ project README ](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md)
