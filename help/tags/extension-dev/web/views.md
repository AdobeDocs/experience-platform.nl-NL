---
title: Weergaven in webextensies
description: Leer hoe u weergaven voor bibliotheekmodules definieert in uw Adobe Experience Platform-webextensies.
exl-id: 4471df3e-75e2-4257-84c0-dd7b708be417
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '2103'
ht-degree: 0%

---

# Weergaven in webextensies

Elke gebeurtenis, voorwaarde, actie, of het type van gegevenselement kan een mening verstrekken die een gebruiker toestaat om montages te leveren. De uitbreiding kan ook een top-level [ mening van de uitbreidingsconfiguratie ](../configuration.md) hebben die gebruikers toestaat om globale montages voor de volledige uitbreiding te leveren. Het proces om een mening te bouwen is identiek over alle soorten meningen.

## Een documenttype opnemen

Zorg ervoor dat u een `doctype` -tag opneemt in uw HTML-bestand. Doorgaans betekent dit dat u het volgende HTML-bestand begint:

```xml
<!DOCTYPE html>
```

## Het iframe-script voor tags opnemen

Neem het iFrame-script voor tags op in de HTML van uw weergave:

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

De inhoud van elk van de methoden moet worden gewijzigd om aan uw specifieke weergavevereisten te voldoen.

### [!DNL init]

De methode `init` wordt aangeroepen door tags zodra de weergave in het iframe is geladen. Het zal één enkel argument (`info`) worden overgegaan dat een voorwerp moet zijn dat de volgende eigenschappen bevat:

| Eigenschap | Beschrijving |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `settings` | Een object met instellingen die eerder in deze weergave zijn opgeslagen. Als `settings` wel `null` is, wordt hiermee aangegeven dat de gebruiker de eerste instellingen maakt in plaats van een opgeslagen versie te laden. Als `settings` een object is, moet u het gebruiken om de weergave te vullen, aangezien de gebruiker ervoor kiest om de eerder blijvend instellingen te bewerken. |
| `extensionSettings` | Instellingen die zijn opgeslagen in de configuratieweergave van de extensie. Dit kan nuttig zijn om tot uitbreidingsmontages in meningen toegang te hebben die niet de mening van de uitbreidingsconfiguratie zijn. Gebruik `settings` als de huidige weergave de configuratieweergave van de extensie is. |
| `propertySettings` | Een object met instellingen voor de eigenschap. Zie de [ turbineobjecten gids ](../turbine.md#property-settings) voor details op wat in dit voorwerp bevat is. |
| `tokens` | Een object met API-tokens. Als u Adobe API&#39;s vanuit de weergave wilt openen, moet u doorgaans een IMS-token gebruiken onder `tokens.imsAccess` . Deze token wordt alleen beschikbaar gesteld voor extensies die door Adobe zijn ontwikkeld. Als u een werknemer van Adobe die een uitbreiding vertegenwoordigen door Adobe wordt authored, gelieve [ het team van de de ingenieurswetenschappen van de gegevensinzameling ](mailto:reactor@adobe.com) te e-mailen en de naam van de uitbreiding te verstrekken zodat kunnen wij het aan de lijst van gewenste personen toevoegen. |
| `company` | Een object dat de volgende tekens bevat: `orgId` (uw 24-letterige Adobe Experience Cloud-id), `id` (de unieke id van uw bedrijf in de Reactor-API) en `tenantId` (de unieke id voor een organisatie in het Adobe Identity Management-systeem). |
| `schema` | Een voorwerp in [ JSON Schema ](https://json-schema.org/) formaat. Dit voorwerp zal uit [ uitbreidingsmanifest ](../manifest.md) komen en kan in het bevestigen van uw vorm nuttig zijn. |
| `apiEndpoints` | Een object met `reactor` dat een verwijzing bevat naar het webadres van de Reactor-API. |
| `userConsentPermissions` | Een voorwerp dat toestemmingsvlaggen van de Gegevens van het Gebruik van het Product van Adobe [ ](https://experienceleague.adobe.com/en/docs/core-services/interface/features/account-preferences#product-usage-data) bevat. Gebruik opgeslagen in `globalDataCollectionAndUsage` vlag om te begrijpen als uw uitbreiding *om het even welke* klantengegevens mag verzamelen. |
| `preferredLanguages` | Een array van taaltekenreeksen. |

Uw mening zou deze informatie moeten gebruiken om zijn vorm terug te geven en te beheren. Waarschijnlijk hoeft u alleen met `info.settings` om te gaan, maar voor het geval dat dat nodig is, wordt de andere informatie wel gegeven.

>[!IMPORTANT]
>
>Als u de extensie GDPR compatibel wilt houden, moet u de markering `userConsentPermissions.globalDataCollectionAndUsage` gebruiken om te bepalen of uw extensie gegevens over de gebruiker mag verzamelen.

### [!DNL validate]

De methode `validate` wordt aangeroepen nadat de gebruiker op de knop Opslaan klikt. Het zou één van het volgende moeten terugkeren:

* Een Booleaanse waarde die aangeeft of de invoer van de gebruiker geldig is.
* Een belofte om later te worden opgelost met een Booleaanse waarde die aangeeft of de invoer van de gebruiker geldig is.

Het is aan u als uitbreidingsontwikkelaar om te bepalen wat geldige input vormt aangezien uw bibliotheekmodule op die input zal handelen.

Als de invoer van de gebruiker ongeldig is, moet u dit in uw weergave aangeven, zodat gebruikers weten wat ze moeten corrigeren.

### [!DNL getSettings]

De methode `getSettings` wordt aangeroepen nadat de gebruiker op de knop Opslaan klikt en de weergave is gevalideerd. De functie moet een van de volgende waarden retourneren:

* Een object dat instellingen bevat die zijn gebaseerd op gebruikersinvoer.
* Een belofte om later te worden opgelost met een object dat instellingen bevat die zijn gebaseerd op gebruikersinvoer.

Dit instellingsobject wordt later weergegeven in de tagruntime-bibliotheek. U bepaalt zelf welke inhoud dit object bevat. Het object moet serialiseerbaar zijn en van en naar JSON kunnen worden gedeserializeerd. De waarden zoals functies of [ RegExp ](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp) instanties voldoen niet aan deze criteria en daarom niet toegestaan.

## Gedeelde weergaven gebruiken

Het `window.extensionBridge` -object heeft verschillende methoden waarmee u gebruik kunt maken van bestaande weergaven die beschikbaar zijn via tags, zodat u deze niet in de weergave hoeft te reproduceren. De beschikbare methoden zijn als volgt:

### [!DNL openCodeEditor]

```js
window.extensionBridge.openCodeEditor().then(function(code) { 
  console.log(code);
});
```

Als deze methode wordt aangeroepen, wordt een modaal teken weergegeven waarmee een gebruiker een codefragment kan bewerken. Wanneer de gebruiker klaar is met het bewerken van de code, wordt de belofte opgelost met de bijgewerkte code. Als de gebruiker de coderedacteur sluit zonder te verkiezen om veranderingen te bewaren, zal de belofte nooit worden opgelost. Het `options` -object moet als volgt zijn gestructureerd:

| Eigenschap | Beschrijving |
| --- | --- |
| `code` | Code die in de redacteur zou moeten worden getoond. Dit wordt doorgaans opgegeven wanneer de gebruiker bestaande code bewerkt. Als dit niet wordt verstrekt, zal de coderedacteur leeg zijn wanneer geopend. |
| `language` | De taal van de code die wordt bewerkt. Geldige opties zijn `javascript` , `html` , `css` , `json` en `plaintext` . Als dit niet is opgegeven, wordt `javascript` aangenomen. |

### [!DNL openRegexTester]

```js
window.extensionBridge.openRegexTester().then(function(pattern) { 
  console.log(pattern);
});
```

Als deze methode wordt aangeroepen, wordt een modaal teken weergegeven waarmee een gebruiker een reguliere-expressiepatroon kan testen en wijzigen. Wanneer de gebruiker klaar is met het bewerken van de reguliere expressie, wordt de promise opgelost met het bijgewerkte reguliere-expressiepatroon. Als de gebruiker de regex tester sluit zonder ervoor te kiezen om veranderingen te bewaren, zal de belofte nooit worden opgelost. Het `options` -object moet de volgende eigenschappen bevatten:

| Eigenschap | Beschrijving |
| --- | --- |
| `pattern` | Het reguliere-expressiepatroon dat moet worden gebruikt als de beginwaarde van het patroonveld in het meetapparaat. Dit wordt meestal opgegeven wanneer de gebruiker een bestaande reguliere expressie bewerkt. Als dit niet is opgegeven, is het patroonveld aanvankelijk leeg. |
| `flags` | De reguliere-expressiemarkeringen die moeten worden gebruikt door de tester. `gi` geeft bijvoorbeeld de markering voor algemene overeenkomst en de markering voor negeren van hoofdletters en kleine letters aan. Deze markeringen kunnen niet worden gewijzigd door de gebruiker in de tester, maar worden gebruikt om de specifieke markeringen aan te tonen die de extensie zal gebruiken bij het uitvoeren van de reguliere expressie. Als dit niet is opgegeven, worden er geen vlaggen gebruikt binnen de tester. Zie {de documentatie van RegExp van 0} MDN [ voor meer informatie over regelmatige uitdrukkingsvlaggen.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp)<br><br> een gemeenschappelijk scenario is een uitbreiding die gebruikers toestaat om gevalgevoeligheid voor een regelmatige uitdrukking van een knevel te voorzien. Om dit te ondersteunen, zou de extensie doorgaans een selectievakje binnen de extensieweergave bieden dat, als deze optie is ingeschakeld, niet-hoofdlettergevoeligheid inschakelt (weergegeven door de markering `i` ). Het instellingenobject dat door de weergave wordt opgeslagen, moet aangeven of het selectievakje is ingeschakeld, zodat de bibliotheekmodule die de reguliere expressie uitvoert, kan weten of de markering `i` moet worden gebruikt. Wanneer de extensieweergave het algemene expressietestbestand wil openen, moet de markering `i` ook worden doorgegeven als het selectievakje voor hoofdlettergevoeligheid is ingeschakeld. Hierdoor kan de gebruiker de reguliere expressie op de juiste manier testen waarbij hoofdletterongevoeligheid is ingeschakeld. |

### [!DNL openDataElementSelector] {#open-data-element}

```js
window.extensionBridge.openDataElementSelector().then(function(dataElement) { 
  console.log(dataElement);
});
```

Als deze methode wordt aangeroepen, wordt een modaal element weergegeven waarmee een gebruiker een gegevenselement kan selecteren. Wanneer de gebruiker klaar is met het selecteren van een gegevenselement, zal de belofte met de naam van het geselecteerde gegevenselement worden opgelost (door gebrek zal de naam in percentagetekens worden verpakt). Als de gebruiker de elementenkiezer sluit zonder te selecteren om veranderingen te bewaren, zal de belofte nooit worden opgelost.

Het `options` -object moet één booleaanse eigenschap bevatten, `tokenize` . This property indicates whether the name of the selected data element should be wrapped in percent sign before resolving the promise. Zie de sectie over [ ondersteunende gegevenselementen ](#supporting-data-elements) voor waarom dit nuttig is. Deze optie is standaard ingesteld op `true` .

## Ondersteunende gegevenselementen {#supporting-data-elements}

Uw weergaven hebben waarschijnlijk formuliervelden waarin gebruikers gegevenselementen willen gebruiken. Als uw weergave bijvoorbeeld een tekstveld bevat waarin de gebruiker een productnaam moet invoeren, heeft het voor de gebruiker niet altijd zin om een hard-gecodeerde waarde in het veld te typen. In plaats daarvan willen ze mogelijk dat de waarde van het veld dynamisch is (bepaald bij uitvoering) en kunnen ze dit bereiken met behulp van een gegevenselement.

Als voorbeeld, veronderstel wij een uitbreiding bouwen die een baken verzendt om een omzetting te volgen. Laten we er ook van uitgaan dat een van de gegevens die ons baken verstuurt een productnaam is. Onze uitbreidingsmening die de gebruiker toestaat om het baken te vormen zou waarschijnlijk een tekstgebied voor de productnaam hebben. Normaal gesproken zou het voor de Experience Platform-gebruiker weinig zin hebben om een statische productnaam in te voeren, zoals &quot;Calzone Oven XL&quot;, omdat de productnaam waarschijnlijk afhankelijk is van de pagina vanwaar het baken wordt verzonden. Dit is een goed geval voor een gegevenselement.

Als een gebruiker het gegevenselement genoemd `productname` voor de waarde van de productnaam wilde gebruiken, kunnen zij de naam van het gegevenselement met percententekens op beide kanten typen (`%productname%`). We verwijzen naar de naam van het data-element met een procentteken als een &#39;data-element token&#39;. Experience Platform-gebruikers zijn vaak vertrouwd met dit concept. Uw extensie slaat op zijn beurt het token voor het gegevenselement op in het `settings` -object dat het exporteert. Het instellingsobject kan er dan als volgt uitzien:

```js
{
  productName: '%productname%'
}
```

Voordat het instellingsobject tijdens runtime wordt doorgegeven aan de module Bibliotheek, wordt het instellingsobject gescand en worden eventuele tokens voor gegevenselementen vervangen door hun respectievelijke waarden. Als tijdens de runtime de waarde van het `productname` data-element `Ceiling Medallion Pro 2000` was, zou het instellingenobject dat in de module Library zou worden doorgegeven, er als volgt uitzien:

```js
{
  productName: 'Ceiling Medallion Pro 2000'
}
```

Om aan te geven waar het nuttig kan zijn voor gebruikers om gegevenselementen te gebruiken en het voor gebruikers gemakkelijk te maken om een gegevenselement in te voeren, adviseren wij hoogst toevoegend een pictogramknoop naast dergelijke gebieden zoals hier getoond:

![ gebied van het gegevenselement ](../images/data-element-field.png)

>[!NOTE]
>
>Om het aangewezen pictogram te downloaden, navigeer aan de [ pictogrammen pagina op het Spectrum van Adobe ](https://spectrum.adobe.com/page/icons/) en onderzoek naar &quot;[!DNL Data]&quot;.

Wanneer de knoop naast het tekstgebied door een gebruiker wordt geselecteerd, vraag `window.extensionBridge.openDataElementSelector` zoals [ hierboven geschetst ](#open-data-element). Hiermee wordt een lijst weergegeven met de gegevenselementen van de gebruiker die de gebruiker kan kiezen in plaats van deze te dwingen de naam en het type procent-teken te onthouden. Nadat de gebruiker een gegevenselement heeft geselecteerd, ontvangt u de naam van het geselecteerde gegevenselement met procenttekens (tenzij u de optie `tokenize` op `false` hebt ingesteld). We raden u aan het tekstveld te vullen met het resultaat.

### Tokens voor gegevenselementen vervangen

Zoals eerder beschreven, als een voortgeduurd montagesobject uit het volgende bestond:

```js
{
  productName: '%productname%'
}
```

En bij uitvoering was de waarde van het `productname` data-element `Ceiling Medallion Pro 2000` , dan zou het settings-object dat in de module van de bibliotheek wordt doorgegeven, er als volgt uitzien:

```js
{
  productName: 'Ceiling Medallion Pro 2000'
}
```

Wanneer een waarde binnen een montagesvoorwerp wordt ontmoet die uit een percententeken, toen een koord, toen een percenteken, _en niets meer_ bestaat, wordt het vervangen door de waarde van het gegevenselement _zonder het type van de waarde van het gegevenselement te veranderen_.

Als de waarde van `productname` bij uitvoering bijvoorbeeld het getal `538` (geen tekenreeks) is, wordt het instellingenobject dat aan de module Bibliotheek wordt doorgegeven, als volgt doorgegeven:

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

In dit geval is het resultaat altijd een tekenreeks, omdat de waarde van `productName` meer is dan één gegevenselementoken. Elk gegevenselement teken zal door zijn respectieve waarde worden vervangen na wordt gegoten aan een koord. Als bij uitvoering de waarde van `productname` `Ceiling Medallion Pro` (een tekenreeks) en `modelnumber` `2000` (een getal) was, wordt het resulterende instellingenobject dat in de module Library wordt doorgegeven, als volgt weergegeven:

```js
{
  productName: 'Ceiling Medallion Pro - 2000'
}
```

## Navigatie voorkomen

De communicatie tussen de uitbreidingsmening en het bevattende gebruikersinterface van de Inzameling van Gegevens is afhankelijk van geen navigatie die binnen de uitbreidingsmening voorkomt. Voeg daarom niets toe aan de extensieweergave waarmee de gebruiker kan navigeren van de HTML-pagina van de extensieweergave. Als u bijvoorbeeld een koppeling opgeeft in de extensieweergave, moet u ervoor zorgen dat er een nieuw browservenster wordt geopend (meestal door `target="_blank"` aan de ankertag toe te voegen). Als u ervoor kiest om een `form` -element te gebruiken in de extensieweergave, moet u ervoor zorgen dat het formulier nooit wordt verzonden. Het verzenden van het formulier kan per ongeluk plaatsvinden als u een `button` -element in het formulier hebt en er `type="button"` niet aan toevoegt. Als u een formulier verzendt in de extensieweergave, wordt het HTML-document vernieuwd. Dit leidt tot een verbroken gebruikerservaring.
