---
title: Weergaven in webextensies
description: Leer hoe u weergaven voor bibliotheekmodules definieert in uw Adobe Experience Platform-webextensies.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '2063'
ht-degree: 0%

---

# Weergaven in webextensies

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Elke gebeurtenis, voorwaarde, actie, of het type van gegevenselement kan een mening verstrekken die een gebruiker toestaat om montages te leveren. De extensie kan ook een [configuratieweergave voor extensies hebben](../configuration.md) waarmee gebruikers algemene instellingen voor de volledige extensie kunnen opgeven. Het proces om een mening te bouwen is identiek over alle soorten meningen.

## Een documenttype opnemen

Zorg ervoor dat u een tag `doctype` in uw HTML-bestand opneemt. Doorgaans betekent dit dat u het volgende begint met uw HTML-bestand:

```xml
<!DOCTYPE html>
```

## Het iframe-script voor tags opnemen

Neem het iFrame-script voor tags op in de HTML van de weergave:

```html
<script src="https://assets.adobedtm.com/activation/reactor/extensionbridge/extensionbridge.min.js"></script>
```

Dit script bevat een communicatie-API waarmee uw weergave kan communiceren met de toepassing Tags.

## Registreren met de communicatie-API van de Extension Bridge

Nadat het iframe-script is geladen, moet u enkele methoden opgeven voor de tags die worden gebruikt voor communicatie. Roep `window.extensionBridge.register` aan en geef het als volgt een object door:

```js
window.extensionBridge.register({
  init: function(info) {
    // Populate view with info.settings which will exist if the user is editing something
    // that was previously saved.
    if (info.settings) {
      document.getElementById('name').value = info.settings.name;
    }
  },
  validate: function() {
    // Return whether the view is valid.
    return document.getElementById('name').value.length > 0;
  },
  getSettings: function() {
    // Return user-provided settings.
    return {
      name: document.getElementById('name').value
    };
  }
});
```

De inhoud van elk van de methoden moet worden aangepast aan uw specifieke weergavevereisten.

### [!DNL init]

De methode `init` wordt aangeroepen door tags zodra de weergave in het iframe is geladen. Het zal één enkel argument (`info`) worden overgegaan dat een voorwerp moet zijn dat de volgende eigenschappen bevat:

| Eigenschap | Beschrijving |
| --- | --- |
| `settings` | Een object met instellingen die eerder in deze weergave zijn opgeslagen. Als `settings` `null` is, geeft dit aan dat de gebruiker de begininstellingen maakt in plaats van een opgeslagen versie te laden. Als `settings` een voorwerp is, zou u het moeten gebruiken om uw mening te bevolken aangezien de gebruiker verkiest om de eerder voortgeduurde montages uit te geven. |
| `extensionSettings` | Instellingen die zijn opgeslagen in de configuratieweergave van de extensie. Dit kan nuttig zijn om tot uitbreidingsmontages in meningen toegang te hebben die niet de mening van de uitbreidingsconfiguratie zijn. Als de huidige mening de mening van de uitbreidingsconfiguratie is, gebruik `settings`. |
| `propertySettings` | Een object met instellingen voor de eigenschap. Zie [turbineobjecthulplijn](../turbine.md#property-settings) voor meer informatie over wat zich in dit object bevindt. |
| `tokens` | Een object met API-tokens. Voor toegang tot Adobe APIs van binnen de mening zult u een symbolisch IMS onder `tokens.imsAccess` gewoonlijk moeten gebruiken. Dit token wordt alleen beschikbaar gesteld voor extensies die door Adobe zijn ontwikkeld. Als u een medewerker van de Adobe die een uitbreiding vertegenwoordigt door Adobe wordt geschreven, gelieve [het team van de gegevensverzamelingstechniek ](mailto:reactor@adobe.com) te e-mailen en de naam van de uitbreiding te verstrekken zodat wij het aan de lijst van gewenste personen kunnen toevoegen. |
| `company` | Een object met één eigenschap, `orgId`, die zelf uw Adobe Experience Cloud-id vertegenwoordigt (een alfanumerieke tekenreeks van 24 tekens). |
| `schema` | Een object in de notatie [JSON-schema](http://json-schema.org/). Dit object komt van het [extensiemanifest](../manifest.md) en kan nuttig zijn voor het valideren van het formulier. |

Uw mening zou deze informatie moeten gebruiken om zijn vorm terug te geven en te beheren. U hoeft waarschijnlijk alleen `info.settings` aan te pakken, maar de andere informatie wordt gegeven als dat nodig is.

### [!DNL validate]

De methode `validate` wordt aangeroepen nadat de gebruiker op de knop &quot;Opslaan&quot; klikt. Het zou één van het volgende moeten terugkeren:

* Een Booleaanse waarde die aangeeft of de invoer van de gebruiker geldig is.
* Een belofte om later te worden opgelost met een Booleaanse waarde die aangeeft of de invoer van de gebruiker geldig is.

Het is aan u als uitbreidingsontwikkelaar om te bepalen wat geldige input vormt aangezien uw bibliotheekmodule op die input zal handelen.

Als de invoer van de gebruiker ongeldig is, moet u dit in uw weergave aangeven, zodat gebruikers weten wat ze moeten corrigeren.

### [!DNL getSettings]

De methode `getSettings` wordt aangeroepen nadat de gebruiker op de knop &quot;Opslaan&quot; drukt en de weergave is gevalideerd. De functie moet een van de volgende waarden retourneren:

* Een object dat instellingen bevat die zijn gebaseerd op gebruikersinvoer.
* Een belofte om later te worden opgelost met een object dat instellingen bevat die zijn gebaseerd op gebruikersinvoer.

Dit instellingsobject wordt later weergegeven in de tagruntime-bibliotheek. U bepaalt zelf welke inhoud dit object bevat. Het object moet serialiseerbaar en deserialiseerbaar zijn voor en vanuit JSON. Waarden zoals functies of [RegExp](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp) instanties voldoen niet aan deze criteria en zijn daarom niet toegestaan.

## Gedeelde weergaven gebruiken

Het `window.extensionBridge` voorwerp heeft verscheidene methodes die u toestaan om uit bestaande meningen voordeel te halen beschikbaar door markeringen zodat moet u hen niet binnen uw mening reproduceren. De beschikbare methoden zijn als volgt:

### [!DNL openCodeEditor]

```js
window.extensionBridge.openCodeEditor().then(function(code) { 
  console.log(code);
});
```

Als deze methode wordt aangeroepen, wordt een modaal teken weergegeven waarmee een gebruiker een codefragment kan bewerken. Wanneer de gebruiker klaar is met het bewerken van de code, wordt de belofte opgelost met de bijgewerkte code. Als de gebruiker de coderedacteur sluit zonder te verkiezen om veranderingen te bewaren, zal de belofte nooit worden opgelost. Het `options`-object moet als volgt zijn gestructureerd:

| Eigenschap | Beschrijving |
| --- | --- |
| `code` | Code die in de redacteur zou moeten worden getoond. Dit wordt doorgaans opgegeven wanneer de gebruiker bestaande code bewerkt. Als dit niet wordt verstrekt, zal de coderedacteur leeg zijn wanneer geopend. |
| `language` | De taal van de code die wordt bewerkt. Geldige opties zijn `javascript`, `html`, `css`, `json` en `plaintext`. Als dit niet is opgegeven, wordt `javascript` aangenomen. |

### [!DNL openRegexTester]

```js
window.extensionBridge.openRegexTester().then(function(pattern) { 
  console.log(pattern);
});
```

Als deze methode wordt aangeroepen, wordt een modaal teken weergegeven waarmee een gebruiker een reguliere-expressiepatroon kan testen en wijzigen. Wanneer de gebruiker klaar is met het bewerken van de reguliere expressie, wordt de promise opgelost met het bijgewerkte reguliere-expressiepatroon. Als de gebruiker de regex tester sluit zonder ervoor te kiezen om veranderingen te bewaren, zal de belofte nooit worden opgelost. Het object `options` moet de volgende eigenschappen bevatten:

| Eigenschap | Beschrijving |
| --- | --- |
| `pattern` | Het reguliere-expressiepatroon dat moet worden gebruikt als de beginwaarde van het patroonveld in het meetapparaat. Dit wordt meestal opgegeven wanneer de gebruiker een bestaande reguliere expressie bewerkt. Als dit niet is opgegeven, is het patroonveld aanvankelijk leeg. |
| `flags` | De reguliere-expressiemarkeringen die moeten worden gebruikt door de tester. Als voorbeeld, `gi` zou op de globale gelijke vlag en de negeer gevalvlag wijzen. Deze markeringen kunnen niet worden gewijzigd door de gebruiker in de tester, maar worden gebruikt om de specifieke markeringen aan te tonen die de extensie zal gebruiken bij het uitvoeren van de reguliere expressie. Als dit niet is opgegeven, worden er geen vlaggen gebruikt binnen de tester. Zie [RegExp-documentatie van MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp) voor meer informatie over reguliere-expressiemarkeringen.<br><br>Een veelvoorkomend scenario is een extensie waarmee gebruikers hoofdlettergevoeligheid voor een reguliere expressie kunnen in- en uitschakelen. Om dit te steunen, zou de uitbreiding typisch checkbox binnen zijn uitbreidingsmening verstrekken die, wanneer gecontroleerd, geval-ongevoeligheid toelaat (die door de `i` vlag wordt vertegenwoordigd). Het instellingenobject dat door de weergave wordt opgeslagen, moet aangeven of het selectievakje is ingeschakeld, zodat de bibliotheekmodule die de reguliere expressie uitvoert, kan weten of de markering `i` moet worden gebruikt. Wanneer de extensieweergave de reguliere-expressietestster wil openen, moet de markering `i` worden doorgegeven als het selectievakje hoofdletterongevoeligheid is ingeschakeld. Hierdoor kan de gebruiker de reguliere expressie op de juiste manier testen waarbij hoofdlettergevoeligheid is ingeschakeld. |

### [!DNL openDataElementSelector] {#open-data-element}

```js
window.extensionBridge.openDataElementSelector().then(function(dataElement) { 
  console.log(dataElement);
});
```

Als deze methode wordt aangeroepen, wordt een modaal element weergegeven waarmee een gebruiker een gegevenselement kan selecteren. Wanneer de gebruiker klaar is met het selecteren van een gegevenselement, zal de belofte met de naam van het geselecteerde gegevenselement worden opgelost (door gebrek zal de naam in percentagetekens worden verpakt). Als de gebruiker de elementenkiezer sluit zonder te selecteren om veranderingen te bewaren, zal de belofte nooit worden opgelost.

Het `options`-object moet één booleaanse eigenschap bevatten, `tokenize`. This property indicates whether the name of the selected data element should be wrapped in percent sign before resolving the promise. Zie de sectie over [ondersteunende gegevenselementen](#supporting-data-elements) voor waarom dit nuttig is. Deze optie is standaard `true`.

## Ondersteunende gegevenselementen {#supporting-data-elements}

Uw weergaven hebben waarschijnlijk formuliervelden waarin gebruikers gegevenselementen willen gebruiken. Als uw weergave bijvoorbeeld een tekstveld bevat waarin de gebruiker een productnaam moet invoeren, heeft het voor de gebruiker niet altijd zin om een hard-gecodeerde waarde in het veld te typen. In plaats daarvan willen ze mogelijk dat de waarde van het veld dynamisch is (bepaald bij uitvoering) en kunnen ze dit bereiken met behulp van een gegevenselement.

Als voorbeeld, veronderstel wij een uitbreiding bouwen die een baken verzendt om een omzetting te volgen. Laten we er ook van uitgaan dat een van de gegevens die ons baken verstuurt een productnaam is. Onze uitbreidingsmening die de gebruiker toestaat om het baken te vormen zou waarschijnlijk een tekstgebied voor de productnaam hebben. Normaal gesproken zou het voor de gebruiker van het Platform weinig zin hebben om een statische productnaam zoals &quot;Calzone Oven XL&quot; in te voeren omdat de productnaam waarschijnlijk afhankelijk is van de pagina waarvan het baken wordt verzonden. Dit is een goed geval voor een gegevenselement.

Als een gebruiker het gegevenselement genoemd `productname` voor de waarde van de productnaam wilde gebruiken, kunnen zij de naam van het gegevenselement met percententekens op beide kanten (`%productname%`) typen. We verwijzen naar de naam van het data-element met een procentteken als een &#39;data-element token&#39;. Gebruikers van Platforms zijn vaak vertrouwd met dit concept. Uw extensie slaat op zijn beurt het token voor het gegevenselement op in het object `settings` dat het exporteert. Het instellingsobject kan er dan als volgt uitzien:

```js
{
  productName: '%productname%'
}
```

Voordat het instellingsobject tijdens runtime wordt doorgegeven aan de module Bibliotheek, wordt het instellingsobject gescand en worden eventuele tokens voor gegevenselementen vervangen door hun respectievelijke waarden. Als tijdens runtime de waarde van het `productname` gegevenselement `Ceiling Medallion Pro 2000` was, zou het montagesobject dat in uw bibliotheekmodule zou worden overgegaan als volgt zijn:

```js
{
  productName: 'Ceiling Medallion Pro 2000'
}
```

Om aan te geven waar het nuttig kan zijn voor gebruikers om gegevenselementen te gebruiken en het voor gebruikers gemakkelijk te maken om een gegevenselement in te voeren, adviseren wij hoogst toevoegend een pictogramknoop naast dergelijke gebieden zoals hier getoond:

![gegevenselementveld](../images/data-element-field.png)

Wanneer de knoop naast het tekstgebied door een gebruiker wordt geselecteerd, vraag `window.extensionBridge.openDataElementSelector` als [hierboven geschetst](#open-data-element). Hiermee wordt een lijst weergegeven met de gegevenselementen van de gebruiker die de gebruiker kan kiezen in plaats van deze te dwingen de naam en het type procent-teken te onthouden. Nadat de gebruiker een gegevenselement heeft geselecteerd, ontvangt u de naam van het geselecteerde gegevenselement met procenttekens (tenzij u de optie `tokenize` hebt ingesteld op `false`). We raden u aan het tekstveld te vullen met het resultaat.

### Tokens voor gegevenselementen vervangen

Zoals eerder beschreven, als een voortgeduurd montagesobject uit het volgende bestond:

```js
{
  productName: '%productname%'
}
```

En bij uitvoering was de waarde van het `productname`-gegevenselement `Ceiling Medallion Pro 2000`, dan zou het instellingenobject dat in uw bibliotheekmodule wordt doorgegeven als volgt zijn:

```js
{
  productName: 'Ceiling Medallion Pro 2000'
}
```

Wanneer een waarde binnen een montagesobject wordt ontmoet die uit een percententeken, toen een koord, toen een percententeken, _en niets meer_ bestaat, wordt het vervangen door de waarde _zonder het type van de waarde van het gegevenselement te veranderen_.

Als de waarde van `productname` bij uitvoering bijvoorbeeld het getal `538` (geen tekenreeks) was, wordt het instellingenobject dat aan de module Bibliotheek wordt doorgegeven, als volgt weergegeven:

```js
{
  productName: 538
}
```

De resulterende `538` is hier een getal en geen tekenreeks. Als de waarde van het gegevenselement tijdens runtime een functie was (een zeldzaam maar mogelijk geval van gebruik), zou het resulterende montagesobject als volgt zijn:

```js
{
  productName: function() { … }
}
```

Anderzijds, veronderstellen wij het voortgeduurde montagesvoorwerp als volgt was:

```js
{
  productName: '%productname% - %modelnumber%'
}
```

In dit geval is het resultaat altijd een tekenreeks, omdat de waarde van `productName` meer is dan één gegevenselement-token. Elk gegevenselement teken zal door zijn respectieve waarde worden vervangen na wordt gegoten aan een koord. Als bij uitvoering de waarde van `productname` `Ceiling Medallion Pro` (een tekenreeks) en `modelnumber` `2000` (een getal) waren, zou het resulterende instellingenobject dat in de module van de bibliotheek wordt doorgegeven, als volgt zijn:

```js
{
  productName: 'Ceiling Medallion Pro - 2000'
}
```

## Navigatie voorkomen

De communicatie tussen de uitbreidingsmening en het bevattende gebruikersinterface van de Inzameling van Gegevens is afhankelijk van geen navigatie die binnen de uitbreidingsmening voorkomt. Als zodanig hoeft u niets toe te voegen aan de extensieweergave, zodat de gebruiker kan navigeren buiten de HTML-pagina van de extensieweergave. Als u bijvoorbeeld een koppeling opgeeft in de extensieweergave, moet u ervoor zorgen dat er een nieuw browservenster wordt geopend (meestal door `target="_blank"` toe te voegen aan de ankertag). Als u ervoor kiest om een `form` element binnen uw uitbreidingsmening te gebruiken, zorg ervoor dat het formulier nooit wordt voorgelegd. Het verzenden van het formulier kan per ongeluk plaatsvinden als u een `button`-element in het formulier hebt en `type="button"` er niet aan toevoegt. Als u een formulier verzendt in de extensieweergave, wordt het HTML-document vernieuwd. Dit leidt tot een verbroken gebruikerservaring.
