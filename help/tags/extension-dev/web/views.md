---
title: Weergaven in webextensies
description: Leer hoe u weergaven voor bibliotheekmodules definieert in uw Adobe Experience Platform-webextensies.
exl-id: 4471df3e-75e2-4257-84c0-dd7b708be417
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '2063'
ht-degree: 0%

---

# Weergaven in webextensies

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Elke gebeurtenis, voorwaarde, actie, of het type van gegevenselement kan een mening verstrekken die een gebruiker toestaat om montages te leveren. De extensie kan ook een hoofdniveau hebben [extensieconfiguratieweergave](../configuration.md) Hiermee kunnen gebruikers algemene instellingen opgeven voor de volledige extensie. Het proces om een mening te bouwen is identiek over alle soorten meningen.

## Een documenttype opnemen

Zorg ervoor dat u een `doctype` in uw HTML-bestand. Doorgaans betekent dit dat u het HTML-bestand begint met het volgende:

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

Nadat het iframe-script is geladen, moet u enkele methoden opgeven voor de tags die worden gebruikt voor communicatie. Bellen `window.extensionBridge.register` en geeft het als volgt een object door:

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

De `init` Deze methode wordt aangeroepen door tags zodra de weergave in het iframe is geladen. Er wordt één argument aan toegevoegd (`info`) die een object moet zijn dat de volgende eigenschappen bevat:

| Eigenschap | Beschrijving |
| --- | --- |
| `settings` | Een object met instellingen die eerder in deze weergave zijn opgeslagen. Indien `settings` is `null`, geeft dit aan dat de gebruiker de eerste instellingen maakt in plaats van een opgeslagen versie te laden. Indien `settings` Als dit een object is, kunt u dit beter gebruiken om de weergave te vullen, aangezien de gebruiker ervoor kiest om de vorige instellingen te bewerken. |
| `extensionSettings` | Instellingen die zijn opgeslagen in de configuratieweergave van de extensie. Dit kan nuttig zijn om tot uitbreidingsmontages in meningen toegang te hebben die niet de mening van de uitbreidingsconfiguratie zijn. Als de huidige mening de mening van de uitbreidingsconfiguratie is, gebruik `settings`. |
| `propertySettings` | Een object met instellingen voor de eigenschap. Zie de [hulplijn turbineobject](../turbine.md#property-settings) voor meer informatie over wat er in dit object staat. |
| `tokens` | Een object met API-tokens. Voor toegang tot Adobe API&#39;s vanuit de weergave moet u doorgaans een IMS-token gebruiken onder `tokens.imsAccess`. Dit token wordt alleen beschikbaar gesteld voor extensies die door Adobe zijn ontwikkeld. Als u een medewerker van Adobe bent die een uitbreiding vertegenwoordigt die door Adobe wordt geschreven, gelieve [e-mail naar het technische team voor gegevensverzameling](mailto:reactor@adobe.com) en geef de naam van de extensie op, zodat we deze aan de lijst van gewenste personen kunnen toevoegen. |
| `company` | Een object dat één eigenschap bevat, `orgId`, die zelf uw Adobe Experience Cloud-id vertegenwoordigt (een alfanumerieke tekenreeks van 24 tekens). |
| `schema` | Een object in [JSON Schema](https://json-schema.org/) gebruiken. Dit object komt van het [extensiemanifest](../manifest.md) en kan nuttig zijn voor het valideren van uw formulier. |

Uw mening zou deze informatie moeten gebruiken om zijn vorm terug te geven en te beheren. Waarschijnlijk hoeft u alleen maar om te gaan `info.settings`, maar de overige informatie wordt verstrekt indien dit noodzakelijk is.

### [!DNL validate]

De `validate` Deze methode wordt aangeroepen nadat de gebruiker op de knop Opslaan klikt. Het zou één van het volgende moeten terugkeren:

* Een Booleaanse waarde die aangeeft of de invoer van de gebruiker geldig is.
* Een belofte om later te worden opgelost met een Booleaanse waarde die aangeeft of de invoer van de gebruiker geldig is.

Het is aan u als uitbreidingsontwikkelaar om te bepalen wat geldige input vormt aangezien uw bibliotheekmodule op die input zal handelen.

Als de invoer van de gebruiker ongeldig is, moet u dit in uw weergave aangeven, zodat gebruikers weten wat ze moeten corrigeren.

### [!DNL getSettings]

De `getSettings` Deze methode wordt aangeroepen nadat de gebruiker op de knop Opslaan klikt en de weergave is gevalideerd. De functie moet een van de volgende waarden retourneren:

* Een object dat instellingen bevat die zijn gebaseerd op gebruikersinvoer.
* Een belofte om later te worden opgelost met een object dat instellingen bevat die zijn gebaseerd op gebruikersinvoer.

Dit instellingsobject wordt later weergegeven in de tagruntime-bibliotheek. U bepaalt zelf welke inhoud dit object bevat. Het object moet serialiseerbaar en deserialiseerbaar zijn voor en vanuit JSON. Waarden zoals functies of [RegExp](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp) instanties voldoen niet aan deze criteria en zijn daarom niet toegestaan.

## Gedeelde weergaven gebruiken

De `window.extensionBridge` Het object heeft verschillende methoden waarmee u gebruik kunt maken van bestaande weergaven die beschikbaar zijn via tags, zodat u deze niet in de weergave hoeft te reproduceren. De beschikbare methoden zijn als volgt:

### [!DNL openCodeEditor]

```js
window.extensionBridge.openCodeEditor().then(function(code) { 
  console.log(code);
});
```

Als deze methode wordt aangeroepen, wordt een modaal teken weergegeven waarmee een gebruiker een codefragment kan bewerken. Wanneer de gebruiker klaar is met het bewerken van de code, wordt de belofte opgelost met de bijgewerkte code. Als de gebruiker de coderedacteur sluit zonder te verkiezen om veranderingen te bewaren, zal de belofte nooit worden opgelost. De `options` Het object moet als volgt worden gestructureerd:

| Eigenschap | Beschrijving |
| --- | --- |
| `code` | Code die in de redacteur zou moeten worden getoond. Dit wordt doorgaans opgegeven wanneer de gebruiker bestaande code bewerkt. Als dit niet wordt verstrekt, zal de coderedacteur leeg zijn wanneer geopend. |
| `language` | De taal van de code die wordt bewerkt. Geldige opties zijn `javascript`, `html`, `css`, `json`, en `plaintext`. Indien dit niet wordt vermeld, `javascript` wordt aangenomen. |

### [!DNL openRegexTester]

```js
window.extensionBridge.openRegexTester().then(function(pattern) { 
  console.log(pattern);
});
```

Als deze methode wordt aangeroepen, wordt een modaal teken weergegeven waarmee een gebruiker een reguliere-expressiepatroon kan testen en wijzigen. Wanneer de gebruiker klaar is met het bewerken van de reguliere expressie, wordt de promise opgelost met het bijgewerkte reguliere-expressiepatroon. Als de gebruiker de regex tester sluit zonder ervoor te kiezen om veranderingen te bewaren, zal de belofte nooit worden opgelost. De `options` -object moet de volgende eigenschappen bevatten:

| Eigenschap | Beschrijving |
| --- | --- |
| `pattern` | Het reguliere-expressiepatroon dat moet worden gebruikt als de beginwaarde van het patroonveld in het meetapparaat. Dit wordt meestal opgegeven wanneer de gebruiker een bestaande reguliere expressie bewerkt. Als dit niet is opgegeven, is het patroonveld aanvankelijk leeg. |
| `flags` | De reguliere-expressiemarkeringen die moeten worden gebruikt door de tester. Als voorbeeld: `gi` zou de markering van de global match en de markering van de ignore case aangeven. Deze markeringen kunnen niet worden gewijzigd door de gebruiker in de tester, maar worden gebruikt om de specifieke markeringen aan te tonen die de extensie zal gebruiken bij het uitvoeren van de reguliere expressie. Als dit niet is opgegeven, worden er geen vlaggen gebruikt binnen de tester. Zie [RegExp-documentatie van MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp) voor meer informatie over reguliere-expressiemarkeringen.<br><br>Een veelvoorkomend scenario is een extensie waarmee gebruikers hoofdlettergevoeligheid voor een reguliere expressie kunnen in- en uitschakelen. Om dit te ondersteunen, zou de extensie doorgaans een selectievakje binnen de extensieweergave bieden dat, wanneer deze optie is ingeschakeld, niet-hoofdlettergevoeligheid inschakelt (weergegeven door de `i` markering). Het instellingenobject dat door de weergave wordt opgeslagen, moet aangeven of het selectievakje is ingeschakeld, zodat de module van de bibliotheek die de reguliere expressie uitvoert, kan weten of de optie `i` markering. Als de extensieweergave de algemene-expressietestster wil openen, moet deze ook worden doorgegeven aan `i` markeren als het selectievakje hoofdlettergevoeligheid is ingeschakeld. Hierdoor kan de gebruiker de reguliere expressie op de juiste manier testen waarbij hoofdlettergevoeligheid is ingeschakeld. |

### [!DNL openDataElementSelector] {#open-data-element}

```js
window.extensionBridge.openDataElementSelector().then(function(dataElement) { 
  console.log(dataElement);
});
```

Als deze methode wordt aangeroepen, wordt een modaal element weergegeven waarmee een gebruiker een gegevenselement kan selecteren. Wanneer de gebruiker klaar is met het selecteren van een gegevenselement, zal de belofte met de naam van het geselecteerde gegevenselement worden opgelost (door gebrek zal de naam in percentagetekens worden verpakt). Als de gebruiker de elementenkiezer sluit zonder te selecteren om veranderingen te bewaren, zal de belofte nooit worden opgelost.

De `options` object moet één booleaanse eigenschap bevatten, `tokenize`. This property indicates whether the name of the selected data element should be wrapped in percent sign before resolving the promise. Zie de sectie over [ondersteunende gegevenselementen](#supporting-data-elements) waarom is dit nuttig ? Deze optie is standaard ingesteld op `true`.

## Ondersteunende gegevenselementen {#supporting-data-elements}

Uw weergaven hebben waarschijnlijk formuliervelden waarin gebruikers gegevenselementen willen gebruiken. Als uw weergave bijvoorbeeld een tekstveld bevat waarin de gebruiker een productnaam moet invoeren, heeft het voor de gebruiker niet altijd zin om een hard-gecodeerde waarde in het veld te typen. In plaats daarvan willen ze mogelijk dat de waarde van het veld dynamisch is (bepaald bij uitvoering) en kunnen ze dit bereiken met behulp van een gegevenselement.

Als voorbeeld, veronderstel wij een uitbreiding bouwen die een baken verzendt om een omzetting te volgen. Laten we er ook van uitgaan dat een van de gegevens die ons baken verstuurt een productnaam is. Onze uitbreidingsmening die de gebruiker toestaat om het baken te vormen zou waarschijnlijk een tekstgebied voor de productnaam hebben. Normaal gesproken zou het voor de gebruiker van het Platform weinig zin hebben om een statische productnaam zoals &quot;Calzone Oven XL&quot; in te voeren omdat de productnaam waarschijnlijk afhankelijk is van de pagina waarvan het baken wordt verzonden. Dit is een goed geval voor een gegevenselement.

Als een gebruiker het gegevenselement met de naam `productname` voor de productnaamwaarde kunnen ze de naam van het gegevenselement typen met procenttekens aan beide zijden (`%productname%`). We verwijzen naar de naam van het data-element met een procentteken als een &#39;data-element token&#39;. Gebruikers van Platforms zijn vaak vertrouwd met dit concept. Uw extensie slaat op zijn beurt het token voor het gegevenselement op in het dialoogvenster `settings` -object dat wordt geëxporteerd. Het instellingsobject kan er dan als volgt uitzien:

```js
{
  productName: '%productname%'
}
```

Voordat het instellingsobject tijdens runtime wordt doorgegeven aan de module Bibliotheek, wordt het instellingsobject gescand en worden eventuele tokens voor gegevenselementen vervangen door hun respectievelijke waarden. Indien bij uitvoering, de waarde van `productname` data-element was `Ceiling Medallion Pro 2000`Het instellingenobject dat in de bibliotheekmodule wordt doorgegeven, ziet er als volgt uit:

```js
{
  productName: 'Ceiling Medallion Pro 2000'
}
```

Om aan te geven waar het nuttig kan zijn voor gebruikers om gegevenselementen te gebruiken en het voor gebruikers gemakkelijk te maken om een gegevenselement in te voeren, adviseren wij hoogst toevoegend een pictogramknoop naast dergelijke gebieden zoals hier getoond:

![gegevenselementveld](../images/data-element-field.png)

Wanneer een gebruiker de knop naast het tekstveld selecteert, roept u `window.extensionBridge.openDataElementSelector` als [hierboven geschetst](#open-data-element). Hiermee wordt een lijst weergegeven met de gegevenselementen van de gebruiker die de gebruiker kan kiezen in plaats van deze te dwingen de naam en het type procent-teken te onthouden. Zodra de gebruiker een gegevenselement heeft geselecteerd, zult u de naam van het geselecteerde gegevenselement ontvangen dat in percentagetekens wordt verpakt (tenzij u hebt geplaatst `tokenize` optie voor `false`). We raden u aan het tekstveld te vullen met het resultaat.

### Tokens voor gegevenselementen vervangen

Zoals eerder beschreven, als een voortgeduurd montagesobject uit het volgende bestond:

```js
{
  productName: '%productname%'
}
```

En bij uitvoering de waarde van de `productname` gegevenselement `Ceiling Medallion Pro 2000`Het instellingenobject dat wordt doorgegeven aan de module Bibliotheek ziet er als volgt uit:

```js
{
  productName: 'Ceiling Medallion Pro 2000'
}
```

Wanneer een waarde binnen een instellingsobject wordt aangetroffen die bestaat uit een procentteken, dan een tekenreeks en vervolgens een procentteken, _en niets meer_, wordt deze vervangen door de waarde van het gegevenselement _zonder het type van de waarde van het gegevenselement te wijzigen_.

Als bijvoorbeeld de waarde van `productname` bij uitvoering het nummer `538` (geen tekenreeks), wordt het instellingenobject dat aan de module Bibliotheek wordt doorgegeven als volgt weergegeven:

```js
{
  productName: 538
}
```

Let erop dat het resultaat `538` is een getal hier en geen tekenreeks. Als de waarde van het gegevenselement tijdens runtime een functie was (een zeldzaam maar mogelijk geval van gebruik), zou het resulterende montagesobject als volgt zijn:

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

In dit geval, omdat de waarde van `productName` Het resultaat is altijd een tekenreeks. Elk gegevenselement teken zal door zijn respectieve waarde worden vervangen na wordt gegoten aan een koord. Indien bij uitvoering, de waarde van `productname` waren `Ceiling Medallion Pro` (een tekenreeks) en `modelnumber` waren `2000` (een getal), wordt het resulterende instellingenobject dat aan de module Bibliotheek wordt doorgegeven, doorgegeven:

```js
{
  productName: 'Ceiling Medallion Pro - 2000'
}
```

## Navigatie voorkomen

De communicatie tussen de uitbreidingsmening en het bevattende gebruikersinterface van de Inzameling van Gegevens is afhankelijk van geen navigatie die binnen de uitbreidingsmening voorkomt. Als zodanig moet u vermijden dat er iets aan de extensieweergave wordt toegevoegd waarmee de gebruiker kan navigeren van de HTML-pagina van de extensieweergave. Als u bijvoorbeeld een koppeling opgeeft in de extensieweergave, moet u ervoor zorgen dat deze een nieuw browservenster opent (meestal door `target="_blank"` op de ankertag). Als u ervoor kiest een `form` in de extensieweergave moet u ervoor zorgen dat het formulier nooit wordt verzonden. Het formulier kan per ongeluk worden verzonden als u een `button` -element in het formulier en kan niet worden toegevoegd `type="button"` aan het. Als u een formulier verzendt in de extensieweergave, wordt het HTML-document vernieuwd. Dit leidt tot een verbroken gebruikerservaring.
