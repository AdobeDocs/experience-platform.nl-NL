---
title: Bibliotheken van derden implementeren
description: Leer meer over de verschillende methoden om bibliotheken van derden te hosten in uw Adobe Experience Platform-tagextensies.
exl-id: d8eaf814-cce8-499d-9f02-b2ed3c5ee4d0
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '1330'
ht-degree: 0%

---

# Bibliotheken van derden implementeren

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Een van de belangrijkste doelen van tagextensies in Adobe Experience Platform is om u in staat te stellen bestaande marketingtechnologieën (bibliotheken) eenvoudig op uw website te implementeren. Door extensies te gebruiken, kunt u bibliotheken implementeren die worden geleverd door CDN&#39;s (Content Delivery Networks) van derden zonder dat u de HTML van uw website handmatig hoeft te bewerken.

Er zijn verschillende methoden om bibliotheken van derden (leveranciers) in uw extensies te hosten. Dit document biedt een overzicht van deze verschillende implementatiemethoden, inclusief de voor- en nadelen van beide.

## Vereisten

Dit document vereist een goed begrip van extensies binnen tags, inclusief wat ze kunnen doen en hoe ze zijn samengesteld. Zie de [overzicht van extensieontwikkeling](./overview.md) voor meer informatie .

## Laden van basiscode

Buiten de context van tags is het belangrijk om te begrijpen hoe marketingtechnologieën doorgaans op een website worden geladen. Externe leveranciers van bibliotheken verschaffen een codefragment (ook wel basiscode genoemd) dat moet worden ingesloten in de HTML van uw website om de functies van de bibliotheek te kunnen laden.

Over het algemeen worden bij het laden op uw site een aantal verschillende basiscodes voor marketingtechnologieën uitgevoerd:

1. Opstelling een globale functie die kan worden gebruikt om met de verkopersbibliotheek in wisselwerking te staan.
1. Laad de leveranciersbibliotheek.
1. Maak een reeks een rij gevormde aanvankelijke vraag aan de globale functie voor configuratie en het volgen doeleinden.

Wanneer de algemene functie voor het eerst is ingesteld, kunt u nog steeds aanroepen naar de functie voordat de bibliotheek klaar is met laden. Om het even welke vraag u maakt wordt toegevoegd aan het een rij vormen van de basiscode mechanisme en dan uitgevoerd in opeenvolgende orde zodra de bibliotheek laadt.

Wanneer de bibliotheek klaar is met laden, wordt de algemene functie vervangen door een nieuwe die de wachtrij omzeilt en in plaats daarvan onmiddellijk alle toekomstige aanroepen naar de functie verwerkt.

### Voorbeeld van basiscode

Het volgende JavaScript is een voorbeeld van een ongeminificeerde basiscode voor de [Pinterest-conversietag](https://developers.pinterest.com/docs/ad-tools/conversion-tag/?), waarnaar verderop in dit document wordt verwezen om aan te tonen hoe de basiscode kan worden aangepast voor verschillende implementatiestrategieën met codes:

```js
!function(scriptUrl) {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = '3.0';
    var scriptElement = document.createElement('script');
    scriptElement.async = true;
    scriptElement.src = scriptUrl;
    var firstScriptElement = 
      document.getElementsByTagName('script')[0];
    firstScriptElement.parentNode.insertBefore(
      scriptElement, firstScriptElement
    );
  }
}('https://s.pinimg.com/ct/core.js');
pintrk('load', 'YOUR_TAG_ID');
pintrk('page');
```

Samengevat bevat de bovenstaande basiscode een [onmiddellijk aangeroepen functie-expressie (IIFE)](https://developer.mozilla.org/en-US/docs/Glossary/IIFE) dat een algemene functie maakt voor interactie met de bibliotheek (`window.pintrk`). Tevens wordt een `scriptURL` variabele de waarde van `https://s.pinimg.com/ct/core.js`, waar de bibliotheek zich bevindt. Zoals eerder uitgelegd, worden alle functies die worden aangeroepen voordat de bibliotheek is geladen, in een wachtrij geplaatst (`window.pintrk.queue`) achtereenvolgens worden uitgevoerd zodra de bibliotheek beschikbaar is.

Het volgende gedeelte van de basiscode is het meest relevant voor het begrijpen van de manier waarop de bibliotheek op uw site wordt geladen:

```js
var scriptElement = document.createElement("script");
scriptElement.async = true;
scriptElement.src = scriptUrl;
var firstScriptElement = 
  document.getElementsByTagName("script")[0];
firstScriptElement.parentNode.insertBefore(
  scriptElement, firstScriptElement
);
```

De basiscode maakt een scriptelement, stelt dit in op asynchroon laden en stelt de `src` URL naar `https://s.pinimg.com/ct/core.js`. Het voegt dan het manuscriptelement aan het document toe door het vóór het eerste manuscriptelement reeds in het document op te nemen.

## Implementatieopties voor tags

In de onderstaande secties ziet u de verschillende manieren waarop u bibliotheken van leveranciers in uw extensies kunt laden. Hierbij wordt gebruikgemaakt van de basiscode van Pinterest die eerder als voorbeeld is weergegeven. Elk van deze voorbeelden omvat het maken van een [actietype voor een webextensie](./web/action-types.md) waarmee de bibliotheek op uw website wordt geladen.

>[!NOTE]
>
>In de onderstaande voorbeelden worden actietypen gebruikt voor demonstratiedoeleinden, maar u kunt dezelfde principes toepassen op elke functie die de tagbibliotheek op uw site laadt.


De volgende methoden worden behandeld:

- [Bibliotheken van derden implementeren](#implementing-third-party-libraries)
   - [Vereisten](#prerequisites)
   - [Laden van basiscode](#base-code-loading-process)
      - [Voorbeeld van basiscode](#base-code-example)
   - [Implementatieopties voor tags](#tags-implementation-options)
      - [Laden bij uitvoering vanaf de host van de leverancier {#vendor-host}](#load-at-runtime-from-the-vendor-host-vendor-host)
      - [Laden bij uitvoering vanaf de host van de tagbibliotheek](#load-at-runtime-from-the-tag-library-host)
      - [De bibliotheek rechtstreeks insluiten](#embed-the-library-directly)
   - [Volgende stappen](#next-steps)

### Laden bij uitvoering vanaf de host van de leverancier {#vendor-host}

De gemeenschappelijkste methode voor het ontvangen van de verkopersbibliotheek is CDN van de verkoper te gebruiken.  Aangezien de basiscode voor de meeste verkopersbibliotheken reeds wordt gevormd om de bibliotheek van CDN van de verkoper te laden, kunt u opstelling uw uitbreiding om de bibliotheek van de zelfde plaats te laden.

Deze benadering is gewoonlijk het gemakkelijkst te handhaven aangezien om het even welke updates die aan het dossier op CDN worden gemaakt automatisch door de uitbreiding zullen worden geladen.

Wanneer u deze methode gebruikt, kunt u gewoon de volledige basiscode rechtstreeks in een handelingstype plakken, zoals:

```js
module.exports = function() {
  !function(scriptUrl) {
    if (!window.pintrk) {
      window.pintrk = function() {
        window.pintrk.queue.push(
          Array.prototype.slice.call(arguments)
        );
      };
      window.pintrk.queue = []; 
      window.pintrk.version = "3.0";
      var scriptElement = document.createElement("script");
      scriptElement.async = true;
      scriptElement.src = scriptUrl;
      var firstScriptElement = 
        document.getElementsByTagName("script")[0];
      firstScriptElement.parentNode.insertBefore(
        scriptElement, firstScriptElement
      );
    }
  }("https://s.pinimg.com/ct/core.js");
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

U kunt desgewenst aanvullende stappen nemen om deze implementatie te vernieuwen. Aangezien de variabelen `scriptElement` en `firstScriptElement` U kunt de IIFE verwijderen omdat deze variabelen niet het risico lopen globals te worden.

Daarnaast bevatten de tags verschillende [kernmodules](./web/core.md) Dit zijn hulpprogramma&#39;s die elke extensie kan gebruiken. In het bijzonder de `@adobe/reactor-load-script` laadt een script vanaf een externe locatie door een scriptelement te maken en dit aan het document toe te voegen. Door deze module voor het scriptlaadproces te gebruiken, kunt u de actiecode nog verder weergeven:

```js
var loadScript = require('@adobe/reactor-load-script');
var scriptUrl = 'https://s.pinimg.com/ct/core.js';
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    loadScript(scriptUrl);   
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

### Laden bij uitvoering vanaf de host van de tagbibliotheek

Het gebruik van een leverancier-CDN voor het hosten van bibliotheken brengt verschillende risico&#39;s met zich mee: CDN kan ontbreken, kan het dossier met een kritieke fout op elk ogenblik worden bijgewerkt, of het dossier zou voor nefarieuze doeleinden kunnen worden gecompromitteerd.

U kunt deze problemen verhelpen door de bibliotheek van leveranciers op te nemen als een afzonderlijk bestand in uw extensie. De extensie kan vervolgens zo worden geconfigureerd dat het bestand naast de hoofdtagbibliotheek wordt gehost. Tijdens de uitvoering wordt de bibliotheek van de leverancier geladen vanaf dezelfde server die de hoofdbibliotheek naar de website heeft geleverd.

>[!IMPORTANT]
>
>In sommige gevallen kan de leverancier extra code laden van servers van derden, zoals in de Pinterest-leveranciersbibliotheek. In deze gevallen kan het bundelen van de leveranciersbibliotheek met uw extensie niet alle risico-gerelateerde problemen volledig wegnemen.

Als u dit wilt implementeren, moet u eerst de bibliotheek van de leverancier downloaden naar uw computer. In het geval van Pinterest is de leveranciersbibliotheek te vinden op [https://s.pinimg.com/ct/core.js](https://s.pinimg.com/ct/core.js). Nadat u het bestand hebt gedownload, moet u het in uw extensieproject plaatsen. In het onderstaande voorbeeld krijgt het bestand de naam `pinterest.js` en bevindt zich binnen een `vendor` in de projectdirectory.

Wanneer het bibliotheekbestand zich in uw project bevindt, moet u uw [extensiemanifest](./manifest.md) (`extension.json`) om aan te geven dat de bibliotheek van de leverancier naast de hoofdtagbibliotheek moet worden geleverd. Dit doet u door het pad naar het bibliotheekbestand toe te voegen binnen een `hostedLibFiles` array:

```json
{
  "hostedLibFiles": ["vendor/pinterest.js"]
}
```

Tot slot moet u uw actiecode vormen om de verkopersbibliotheek van de zelfde server te laden die gastheren de belangrijkste bibliotheek. In het onderstaande voorbeeld wordt de actiecode gebruikt die is ingebouwd in het dialoogvenster [vorige sectie](#vendor-host) als uitgangspunt. Met de [turbineobject](./turbine.md), moet u de bestandsnaam (zonder pad) van het leverancierbestand als volgt doorgeven:

```js
var loadScript = require('@adobe/reactor-load-script');
var scriptUrl = turbine.getHostedLibFileUrl('pinterest.js');
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    loadScript(scriptUrl);   
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

Het is belangrijk om op te merken dat wanneer het gebruiken van deze methode, u uw gedownloade verkopersdossier manueel moet bijwerken wanneer de bibliotheek op hun CDN wordt bijgewerkt, en de veranderingen in een nieuwe versie van uw uitbreiding vrijgeven.

### De bibliotheek rechtstreeks insluiten

U kunt omzeilen dat u de bibliotheek van de leverancier volledig moet laden door de bibliotheekcode rechtstreeks in te sluiten in de actiecode zelf, waardoor deze in feite deel uitmaakt van de hoofdtagbibliotheek. Met deze methode wordt de hoofdbibliotheek groter, maar hoeft u geen extra HTTP-aanvraag meer in te dienen om een afzonderlijk bestand op te halen.

De in de [vorige sectie](#vendor-host) Als uitgangspunt kunt u de lijn vervangen waar het manuscript met de inhoud van het manuscript zelf wordt geladen:

```js
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    // Paste the full vendor library code here.
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

## Volgende stappen

Dit document bevat een overzicht van de verschillende methoden voor het hosten van bibliotheken van derden in uw tagextensies. Hoewel de gegeven voorbeelden zich toespitsten op bibliotheken, zijn deze technieken van toepassing op elk stukje code dat uw extensie kan gebruiken.

Verwijs naar de documentatie verbonden aan door deze gids om meer over de hulpmiddelen te leren om uw uitbreidingen, met inbegrip van actietypes, uitbreidingsmanifest, kernmodules, en het turbinevoorwerp te vormen.
