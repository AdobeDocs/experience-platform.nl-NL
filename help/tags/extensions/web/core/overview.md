---
title: Overzicht van Core Extension
description: Meer informatie over de uitbreiding van de tag Core in Adobe Experience Platform.
source-git-commit: 41a394974153883dc300bdd8a00fc3106c4f0ac6
workflow-type: tm+mt
source-wordcount: '4895'
ht-degree: 0%

---

# Overzicht van kernextensies

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

De extensie van de tag Core is de standaardextensie die wordt vrijgegeven met Adobe Experience Platform.

Dit document bevat informatie over de beschikbare opties wanneer u de extensie Core gebruikt om een regel te maken.

## Gebeurtenistypen van de kernextensie {#core-extension-event-types}

Dit onderwerp beschrijft de gebeurtenistypen beschikbaar in de uitbreiding van de Kern. Zie de sectie [Opties](#options) voor informatie over de opties die voor verschillende gebeurtenistypen kunnen worden ingesteld.

### Gebeurtenissen op basis van browser

#### Tab vervagen

De gebeurtenis tab-blur activeert de handeling wanneer een tab de focus verliest. Er zijn geen instellingen voor dit gebeurtenistype.

#### Tabfocus

De gebeurtenis tab-focus activeert de actie wanneer een tab de focus krijgt. Er zijn geen instellingen voor dit gebeurtenistype.

### Formulier

#### Vervagen

De gebeurtenis blur activeert de actie wanneer een formulier de focus verliest. Zie de sectie [Opties](#options) voor meer informatie over aanpasbare gebeurtenisinstellingen.

#### Focus

De focusgebeurtenis activeert de actie wanneer een formulier de focus krijgt. Zie de sectie [Opties](#options) voor meer informatie over aanpasbare gebeurtenisinstellingen.

#### Verzenden

De verzendgebeurtenis activeert de actie wanneer een formulier wordt verzonden. Zie de sectie [Opties](#options) voor meer informatie over aanpasbare gebeurtenisinstellingen.

### Keyboard-gebeurtenissen

#### Toetsdruk

De gebeurtenis wordt geactiveerd wanneer op een toets wordt gedrukt. Zie de sectie [Opties](#options) voor meer informatie over aanpasbare gebeurtenisinstellingen.

### Gebeurtenissen op basis van media

#### Media beëindigd

De gebeurtenis wordt geactiveerd wanneer het medium wordt beëindigd. Zie de sectie [Opties](#options) voor meer informatie over aanpasbare gebeurtenisinstellingen.

#### Gegevens die met media zijn geladen

De gebeurtenis wordt geactiveerd wanneer de media gegevens laden. Zie de sectie [Opties](#options) voor meer informatie over aanpasbare gebeurtenisinstellingen.

#### Media pauzeren

De gebeurtenis wordt geactiveerd wanneer het medium wordt gepauzeerd. Zie de sectie [Opties](#options) voor meer informatie over aanpasbare gebeurtenisinstellingen.

#### Media afspelen

De gebeurtenis wordt geactiveerd wanneer de media wordt afgespeeld. Zie de sectie [Opties](#options) voor meer informatie over aanpasbare gebeurtenisinstellingen.

#### Media geïnstalleerd

De gebeurtenis wordt geactiveerd wanneer de media stagneren. Zie de sectie [Opties](#options) voor meer informatie over aanpasbare gebeurtenisinstellingen.

#### Media-tijd afgespeeld

De gebeurtenis wordt geactiveerd wanneer de media gedurende een bepaalde periode wordt afgespeeld. U moet de duur opgeven waarvoor de media moeten worden afgespeeld om de gebeurtenis te activeren. Zie de sectie [Opties](#options) voor meer informatie over aanpasbare gebeurtenisinstellingen.


#### Gewijzigd media-volume

De gebeurtenis wordt geactiveerd als het volume wordt verhoogd of verlaagd. Zie de sectie [Opties](#options) voor meer informatie over aanpasbare gebeurtenisinstellingen.

### Mobiel-apparaatgeoriënteerde gebeurtenissen

#### Wijziging van richting

De gebeurtenis wordt geactiveerd als de oriëntatie van het apparaat verandert. U moet de duur opgeven waarvoor de oriëntatie moet wijzigen om de gebeurtenis te activeren. Er zijn geen instellingen voor dit gebeurtenistype.

#### Zoomwijziging

De gebeurtenis wordt geactiveerd wanneer de gebruiker in- of uitzoomt. Er zijn geen instellingen voor dit gebeurtenistype.

### Gebeurtenissen met muisbediening

#### Klikken

De gebeurtenis wordt geactiveerd als het opgegeven element is geselecteerd (erop geklikt). U kunt ook eigenschapswaarden opgeven die waar moeten zijn voor het element voordat de gebeurtenis wordt geactiveerd.

Als het element een ankermarkering (`<a>`) aan verbonden inhoud is, kunt u ook specificeren of om navigatie voor een periode te vertragen. Dit kan handig zijn als uw regel extra tijd nodig heeft om uit te voeren en normaal gesproken niet zou zijn voltooid voordat paginanavigatie plaatsvindt.

>[!WARNING]
>
>Deze optie moet uiterst voorzichtig worden gebruikt vanwege de mogelijke negatieve gevolgen voor de gebruikerservaring indien deze onjuist wordt gebruikt.

Wanneer u koppelingsvertraging gebruikt, voorkomt Platform eigenlijk dat de browser van de pagina af navigeert. Vervolgens wordt er een JavaScript-omleiding uitgevoerd naar de oorspronkelijke bestemming na de opgegeven time-out. Dit is vooral gevaarlijk wanneer uw paginamarkering `<a>` markeringen heeft waar de voorgenomen functionaliteit niet de gebruiker weg van de pagina werkelijk navigeert. Als u uw probleem niet op een andere manier kunt oplossen, zou u met uw selecteursdefinitie uiterst nauwkeurig moeten zijn zodat deze gebeurtenis precies teweegbrengt waar u het nodig hebt en nergens anders.

De standaardwaarde voor de vertraging van de koppeling is 100 milliseconden. Tags wachten altijd op de opgegeven tijd en zijn op geen enkele wijze verbonden met de uitvoering van de handelingen van de regel. Het is mogelijk dat de vertraging de gebruiker zal dwingen langer te wachten dan noodzakelijk is, en ook de mogelijkheid dat de vertraging niet lang genoeg voor alle acties van de regel met succes zal zijn voltooid. Langere vertragingen verstrekken meer tijd voor regeluitvoering maar ook verslechteren de gebruikerservaring.

Om de vertraging in te voeren is het nodig om zowel het geselecteerde element te verstrekken dat de gebeurtenis teweegbrengt, als de specifieke hoeveelheid tijd alvorens de gebeurtenis wordt teweeggebracht.

Zie de sectie [Opties](#options) voor meer informatie voor de geavanceerde opties.

#### Hover

De gebeurtenis wordt geactiveerd wanneer de gebruiker de muisaanwijzer op een opgegeven element plaatst. U moet ook vormen of de regel onmiddellijk of na een gespecificeerd aantal milliseconden wordt teweeggebracht. Zie de sectie [Opties](#options) voor meer informatie over aanpasbare gebeurtenisinstellingen.

### Andere gebeurtenissen

#### Aangepaste gebeurtenis

De gebeurtenis wordt geactiveerd als een aangepast gebeurtenistype optreedt. Benoemde JavaScript-functies die elders in de codebase zijn gedefinieerd, kunnen worden gebruikt als een aangepast gebeurtenistype. U moet de naam van het type van douanegebeurtenis specificeren en om het even welke andere montages vormen zoals die in [sectie ](#options) hieronder worden beschreven.

#### Gegevenselement gewijzigd

De gebeurtenis wordt geactiveerd wanneer een opgegeven gegevenselement verandert. U moet een naam opgeven voor het gegevenselement. U kunt het gegevenselement selecteren door de naam ervan in het tekstveld te typen of door het pictogram voor het gegevenselement rechts van het tekstveld te selecteren en een keuze te maken in een lijst in het dialoogvenster dat verschijnt.

#### Directe oproep

De direct-vraaggebeurtenis overslaat gebeurtenisopsporing en raadplegingssystemen. De direct-vraagregels zijn ideaal voor situaties waar u Platform precies wilt vertellen wat gebeurt. Bovendien zijn ze ideaal wanneer Platform een gebeurtenis niet kan detecteren in het DOM, zoals met Adobe Flash. Geef de tekenreeks `_satellite.track` op in het tekstveld Id.

#### Element bestaat

De gebeurtenis activeert of een opgegeven element bestaat. Zie de sectie [Opties](#options) voor meer informatie over aanpasbare gebeurtenisinstellingen.

#### Viewport invoeren

De gebeurtenis wordt geactiveerd als de gebruiker een opgegeven viewport invoert. U moet een CSS-kiezer opgeven als criteria om overeenkomende elementen als doel in te stellen. U moet ook vormen of de regel onmiddellijk of na een gespecificeerd aantal milliseconden wordt teweeggebracht, en of de gebeurtenis zou moeten teweegbrengen telkens als de gebeurtenis of slechts de eerste keer voorkomt.

Zie de sectie [Opties](#options) voor meer informatie over aanpasbare gebeurtenisinstellingen.

#### Geschiedeniswijziging

De gebeurtenis wordt geactiveerd als een pushState- of hashchange-gebeurtenis plaatsvindt. Er zijn geen instellingen voor dit gebeurtenistype.

#### Tijd besteed op pagina

De gebeurtenis wordt geactiveerd wanneer de gebruiker gedurende een opgegeven aantal seconden op de pagina blijft. U moet het aantal seconden opgeven dat moet worden doorgegeven voordat de gebeurtenis wordt geactiveerd.

### Gebeurtenissen bij laden van pagina

#### gereed voor DOM

De gebeurtenis wordt geactiveerd wanneer het DOM gereed is en de gebruiker kan communiceren met de pagina. Er zijn geen instellingen voor dit gebeurtenistype.

#### Bibliotheek geladen (pagina boven) {#library-loaded-page-top}

De gebeurtenis wordt gestart zodra de tagbibliotheek is geladen. Er zijn geen instellingen voor dit gebeurtenistype.

#### Pagina onder {#page-bottom}

De gebeurtenis wordt geactiveerd zodra `_satellite.pageBottom();` is aangeroepen. Wanneer de tagbibliotheek asynchroon wordt geladen, mag dit gebeurtenistype niet worden gebruikt. Er zijn geen instellingen voor dit gebeurtenistype.

#### Venster geladen

De gebeurtenis wordt geactiveerd wanneer onLoad wordt aangeroepen door de browser en de pagina klaar is met laden. Er zijn geen instellingen voor dit gebeurtenistype.

### Opties {#options}

Voor elk type formuliergebeurtenis worden de volgende instellingen gebruikt:

#### Specifieke elementen \| Willekeurig element

* Als u **[!UICONTROL Specific Elements]** kiest, verschijnen de opties om de elementen en bezitswaarden te selecteren.
* Als u **[!UICONTROL Any Element]** kiest, zijn er geen verdere opties vereist om de elementen te beperken.

#### Elementen die overeenkomen met de CSS-kiezer

Voer de CSS-kiezer in die de elementen identificeert die de gebeurtenis activeren.

#### En met bepaalde eigenschapswaarden

Als u deze optie selecteert, worden de volgende parameters beschikbaar:

* `property=value`

   Geef de waarde voor de eigenschap op

* Regex

   Schakel deze optie in als de `property=value` een reguliere expressie is.

* Toevoegen

   Voeg nog een `property=value` paar toe.

#### Geavanceerde opties (Bubbling)

* Deze regel zelfs uitvoeren wanneer de gebeurtenis van een afstammend element afkomstig is
* Laat deze regel lopen zelfs als de gebeurtenis reeds een regel teweegbracht die een afstammend element richt
* Nadat de regel is uitgevoerd, voorkomt u dat de gebeurtenis regels activeert die gericht zijn op bovenliggende elementen

## Type voorwaarde voor kernextensie

In deze sectie worden de voorwaardetypen beschreven die beschikbaar zijn in de extensie Core. Deze voorwaardetypes kunnen met of het regelmatige of type van uitzonderingslogica worden gebruikt.

### Gegevens

#### Cookie

Geef de naam en waarde van het cookie op die moeten bestaan voordat een gebeurtenis een handeling activeert.

1. Geef een naam voor de cookie op.
1. Voer de waarde in die in het cookie moet bestaan als de gebeurtenis een handeling moet activeren.
1. (Optioneel) Schakel Regex in als dit een reguliere expressie is.

#### Aangepaste code

Geef aangepaste code op die als voorwaarde voor de gebeurtenis moet bestaan. Gebruik de ingebouwde code-editor om de aangepaste code in te voeren.

1. Selecteer **[!UICONTROL Open Editor]**.
1. Typ de aangepaste code.
1. Selecteer **[!UICONTROL Save]**.

Er wordt automatisch een variabele met de naam `event` beschikbaar, waarnaar u in uw aangepaste code kunt verwijzen. Het object `event` bevat nuttige informatie over de gebeurtenis die de regel heeft geactiveerd. De gemakkelijkste manier om te bepalen welke gebeurtenisgegevens beschikbaar zijn is `event` aan de console van binnen uw douanecode te registreren:

```javascript
console.log(event);
return true;
```

Voer de regel in een browser uit en inspecteer het geregistreerde gebeurtenisobject in de browserconsole. Zodra u begrijpt welke informatie beschikbaar is, kunt u het voor programmatic beslissing binnen uw douanecode gebruiken.

*Voorwaardenvolgorde*

Wanneer de optie &quot;Regelcomponenten in volgorde uitvoeren&quot; van eigenschapinstellingen is ingeschakeld, kunt u volgende regelcomponenten laten wachten terwijl uw voorwaarde een asynchrone taak uitvoert.

Wanneer de voorwaarde [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) terugkeert, zal de volgende voorwaarde in de regel niet uitvoeren tot de teruggekeerde belofte wordt opgelost. Als de belofte wordt verworpen, zijn de markeringen van mening dat de voorwaarde ontbroken en geen verdere voorwaarden of acties van die regel zullen worden uitgevoerd.

Een voorbeeld van een voorwaarde die een belofte terugkeert:

```javascript
return new Promise(function(resolve, reject) {
  setTimeout(function() {
    if (new Date().getDay() === 5) {
      resolve();
    } else {
      reject();
    }
  }, 1000);
});
```

#### Waardevergelijking {#value-comparison}

Vergelijkt twee waarden om te bepalen of deze voorwaarde waar terugkeert.

Als u een regel met veelvoudige voorwaarden hebt, is het mogelijk dat deze voorwaarde waar zal terugkeren, maar de regel zal nog niet in brand steken omdat de andere voorwaarden als vals evalueren of één van de uitzonderingen als waar evalueert.

1. Geef een waarde op.
1. Selecteer de operator. Raadpleeg de lijst met vergelijkingsoperatoren voor waarden hieronder voor meer informatie.
1. (Indien vereist) Geef aan of de vergelijking niet hoofdlettergevoelig moet zijn.
1. Geef een andere waarde op voor de vergelijking.

De volgende vergelijkingsoperatoren voor waarden zijn beschikbaar:

**Gelijk:** de voorwaarde keert waar terug als de twee waarden gelijk zijn gebruikend een niet-strikte vergelijking (in JavaScript, == exploitant). De waarden kunnen van elk type zijn. Wanneer u een woord als _true_, _false_, _null_ of _undefined_ in een waardeveld typt, wordt het woord vergeleken als een tekenreeks en wordt het niet omgezet in het JavaScript-equivalent ervan.

**Niet gelijk:** de voorwaarde retourneert true als de twee waarden niet gelijk zijn met een niet-strikte vergelijking (in JavaScript, de != operator). De waarden kunnen van elk type zijn. Wanneer u een woord als _true_, _false_, _null_ of _undefined_ in een waardeveld typt, wordt het woord vergeleken als een tekenreeks en wordt het niet omgezet in het JavaScript-equivalent ervan.

**Bevat:** de voorwaarde retourneert true als de eerste waarde de tweede waarde bevat. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die false retourneert.

**Bevat niet:** de voorwaarde retourneert true als de eerste waarde niet de tweede waarde bevat. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die true retourneert.

**Begint met:** de voorwaarde retourneert true als de eerste waarde met de tweede waarde begint. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die false retourneert.

**Begint niet met:** de voorwaarde retourneert true als de eerste waarde niet begint met de tweede waarde. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die true retourneert.

**Eindigt met:** de voorwaarde retourneert true als de eerste waarde eindigt met de tweede waarde. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die false retourneert.

**Niet eindigen met:** de voorwaarde retourneert true als de eerste waarde niet eindigt met de tweede waarde. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die true retourneert.

**Komt overeen met Regex:** De voorwaarde retourneert true als de eerste waarde overeenkomt met de reguliere expressie. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die false retourneert.

**Komt niet overeen met Regex:** de voorwaarde retourneert true als de eerste waarde niet overeenkomt met de reguliere expressie. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die true retourneert.

**Is minder dan:** De voorwaarde retourneert true als de eerste waarde kleiner is dan de tweede waarde. Tekenreeksen die getallen vertegenwoordigen, worden omgezet in getallen. Een andere waarde dan een getal of een convertibele tekenreeks resulteert in de voorwaarde die false retourneert.

**Is kleiner dan of gelijk aan:** de voorwaarde retourneert true als de eerste waarde kleiner dan of gelijk is aan de tweede waarde. Tekenreeksen die getallen vertegenwoordigen, worden omgezet in getallen. Een andere waarde dan een getal of een convertibele tekenreeks resulteert in de voorwaarde die false retourneert.

**Is groter dan:** de voorwaarde keert waar terug als de eerste waarde groter is dan de tweede waarde. Tekenreeksen die getallen vertegenwoordigen, worden omgezet in getallen. Een andere waarde dan een getal of een convertibele tekenreeks resulteert in de voorwaarde die false retourneert.

**Is groter dan of gelijk aan:** de voorwaarde keert waar terug als de eerste waarde groter dan of gelijk aan de tweede waarde is. Tekenreeksen die getallen vertegenwoordigen, worden omgezet in getallen. Een andere waarde dan een getal of een convertibele tekenreeks resulteert in de voorwaarde die false retourneert.

**Is Waar:** de voorwaarde keert waar terug als de waarde een booleaanse waarde met de waarde waar is. De waarde die u opgeeft, wordt niet omgezet in een Booleaanse waarde als het een ander type betreft. Elke andere waarde dan een booleaanse waarde met de waarde true resulteert in de voorwaarde die false retourneert.

**Is Truthy:** De voorwaarde retourneert true als de waarde waar is na de conversie naar een booleaanse waarde. Zie [Truthy-documentatie van MDN](https://developer.mozilla.org/en-US/docs/Glossary/Truthy) voor voorbeelden van waarheidswaarden.

**Is Onwaar:** de voorwaarde retourneert true als de waarde een booleaanse waarde is met de waarde false. De waarde die u opgeeft, wordt niet omgezet in een Booleaanse waarde als het een ander type betreft. Elke andere waarde dan een booleaanse waarde met de waarde false resulteert in de voorwaarde die false retourneert.

**Is Falsy:** de voorwaarde retourneert true als de waarde false is nadat deze is omgezet in een Booleaanse waarde. Zie [Falsy documentation](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) voor voorbeelden van valse waarden.

#### Variabele

Geef de naam en waarde van de JavaScript-variabele op die moeten bestaan voordat een gebeurtenis een handeling activeert.

1. Geef de naam van de JavaScript-variabele op.
1. Geef de waarde op van de variabele die als voorwaarde voor de gebeurtenis moet bestaan.
1. (Optioneel) Schakel Regex in als dit een reguliere expressie is.

### Engagement

#### Openingspagina

Geef de pagina op waarop de gebruiker moet landen om de gebeurtenis te activeren.

1. Geef de bestemmingspagina op.
1. (Optioneel) Schakel Regex in als dit een reguliere expressie is.

#### Nieuwe/Terugkerende bezoeker

Geef op of de bezoeker een nieuwe bezoeker of een terugkerende bezoeker moet zijn voor een gebeurtenis om een actie te activeren.

Selecteer een van de volgende opties:

* Nieuwe bezoeker
* Bezoeker terugsturen

#### Paginaweergaven

Configureer het aantal keren dat de bezoeker de pagina moet weergeven voordat de actie wordt geactiveerd.

1. Selecteer of het aantal paginaweergaven groter dan, gelijk aan of kleiner dan de opgegeven waarde moet zijn.
1. Geef het aantal paginaweergaven op dat bepaalt of aan de voorwaarde wordt voldaan.
1. Configureer wanneer de paginaweergaven worden geteld door een van de volgende opties te selecteren:
   * Levensduur
   * Huidige sessie

#### Sessies

Trigger de actie als het aantal zittingen van de gebruiker aan de gespecificeerde criteria voldoet.

1. Selecteer of het aantal sessies groter dan, gelijk aan of kleiner dan de opgegeven waarde moet zijn.
1. Geef het aantal sessies op dat bepaalt of aan de voorwaarde wordt voldaan.

#### Tijd op de site

Trigger de actie als het aantal zittingen van de gebruiker aan de gespecificeerde criteria voldoet.

Configureer hoe lang de bezoeker op de site moet zijn voordat de handeling wordt gestart.

1. Geef op of het aantal minuten dat de bezoeker op de site heeft, groter moet zijn dan, gelijk aan of kleiner dan de opgegeven waarde.
1. Geef het aantal minuten op dat bepaalt of aan de voorwaarde wordt voldaan.

#### Verkeersbron

Trigger de actie als het aantal zittingen van de gebruiker aan de gespecificeerde criteria voldoet.

Geef de bron van het verkeer van de bezoeker op die waar moet zijn om de actie te activeren.

1. Specificeer de verkeersbron.
1. (Optioneel) Schakel Regex in als dit een reguliere expressie is.

### Technologie

#### Browser

Selecteer de browser die de bezoeker moet gebruiken om de actie te activeren.

Selecteer een of meer van de volgende browsers:

* Chroom
* Firefox
* Internet Explorer/Edge
* Internet Explorer Mobile
* Mobile Safari
* UniverseelWeb
* Opera
* Opera Mini
* Opera Mobile
* Safari

#### Apparaattype

Selecteer het apparaattype dat de bezoeker moet gebruiken om de actie te activeren.

Selecteer een of meer van de volgende apparaattypen:

* Android
* Blackberry
* Desktop
* iPad
* iPhone
* iPod
* Nokia
* Windows-telefoon

#### Besturingssysteem

Selecteer het besturingssysteem dat de bezoeker moet gebruiken om de actie te activeren.

Selecteer een of meer van de volgende besturingssystemen:

* Android
* Blackberry
* iOS
* Linux
* MacOS
* Maemo
* Symbian OS
* Unix
* Windows

#### Schermresolutie

Selecteer de schermresolutie die bezoekers op hun apparaten moeten gebruiken om de actie te activeren.

1. Selecteer of de breedte van de schermresolutie van het apparaat van de bezoeker groter moet zijn dan, gelijk aan of kleiner dan de opgegeven waarde.
1. Geef het aantal pixels op dat nodig is voor de breedte van de schermresolutie.
1. Selecteer of de schermresolutiehoogte van het apparaat van de bezoeker groter dan, gelijk aan of kleiner dan de opgegeven waarde moet zijn.
1. Geef het aantal pixels op dat nodig is voor de hoogte van de schermresolutie.

#### Venstergrootte

Selecteer de venstergrootte die bezoekers op hun apparaten moeten gebruiken om de actie te activeren.

1. Selecteer of de breedte van het vensterformaat van het apparaat van de bezoeker groter moet zijn dan, gelijk aan of kleiner dan de opgegeven waarde.
1. Geef het aantal pixels op dat nodig is voor de breedte van het vensterformaat.
1. Selecteer of de hoogte van het vensterformaat van het apparaat van de bezoeker groter moet zijn dan, gelijk aan of kleiner dan de opgegeven waarde.
1. Geef het aantal pixels op dat nodig is voor de hoogte van het vensterformaat.

### URL

#### Domein

Geef het domein van de bezoeker op.

#### Hash

Geef een of meer hashpatronen op die in de URL moeten voorkomen.

>[!NOTE]
>
>Meerdere hashpatronen worden samengevoegd door een OR.

1. Geef het hashpatroon op.
1. (Optioneel) Schakel Regex in als dit een reguliere expressie is.
1. Voeg andere hashpatronen toe.

#### Pad- en queryreeks

Geef een of meer paden op die in de URL moeten voorkomen.  Dit omvat de weg en het vraagkoord.

>[!NOTE]
>
>Meerdere paden worden verbonden door een OR.

1. Geef het pad op.
1. (Optioneel) Schakel Regex in als dit een reguliere expressie is.
1. Voeg andere paden toe.

#### Pad zonder queryreeks

Geef een of meer paden op die in de URL moeten voorkomen.  Dit omvat de weg, maar omvat niet het vraagkoord.

>[!NOTE]
>
>Meerdere paden worden verbonden door een OR.

1. Geef het pad op.
1. (Optioneel) Schakel Regex in als dit een reguliere expressie is.
1. Voeg andere paden toe.

#### Protocol

Geef het protocol op dat in de URL wordt gebruikt.

Selecteer een van de volgende opties:

* HTTP
* HTTPS

#### Parameter querytekenreeks

Geef de URL-parameter op die in de URL wordt gebruikt.

1. Geef een naam voor een URL-parameter op.
1. Geef de waarde op die voor de URL-parameter wordt gebruikt.
1. (Optioneel) Schakel Regex in als dit een reguliere expressie is.

#### Subdomein

Geef een of meer subdomeinen op die in de URL moeten voorkomen.

>[!NOTE]
>
>De veelvoudige subdomeinen worden aangesloten bij door OF.

1. Geef het subdomein op.
1. (Optioneel) Schakel Regex in als dit een reguliere expressie is.
1. Voeg andere subdomeinen toe.

### Overige

#### Datumbereik

Geef een datumbereik op. Kies de datum en het tijdstip waarop de gebeurtenis zich na, de datum vóór en de tijdzone voordoet.

#### Max. frequentie

Geef het maximale aantal keren op dat de voorwaarde true retourneert. U kunt uit de volgende opties selecteren:

* Paginaweergave
* Sessies
* Bezoeker
* Seconden
* Minuten
* Dagen
* Weken
* Maanden

Voor de voorwaarde maximum frequentie 1 per zitting, worden deze twee `localStorage` punten vergeleken. Als de `visitorTracking.sessionCount` groter is dan de `maxFrequency.session` telling, dan is de steekproefvoorwaarde waar. Als ze gelijk zijn, is de voorwaarde onwaar.

`sessionCount` is een  `visitorTracking` item, dus de bezoeker-API moet zijn ingeschakeld om de samplingvoorwaarde te laten werken.

#### Monster

Geef het percentage op van de tijd waarop de voorwaarde true retourneert.

## Typen handelingen voor kernextensies

Deze sectie beschrijft de actietypes beschikbaar in de uitbreiding van de Kern.

### Aangepaste code

Geef de code op die wordt uitgevoerd nadat de gebeurtenis is geactiveerd en de voorwaarden zijn geëvalueerd.

1. Geef de actiecode een naam.
1. Selecteer de taal die wordt gebruikt om de handeling te definiëren:
   * JavaScript
   * HTML
1. Selecteer of de actiecode globaal moet worden uitgevoerd.
1. Selecteer **[!UICONTROL Open Editor]**.
1. Bewerk de code en selecteer **[!UICONTROL Save]**.

Wanneer JavaScript als taal wordt geselecteerd, zal een variabele genoemd `event` automatisch beschikbaar zijn, die u van binnen uw douanecode kunt van verwijzingen voorzien. Het object `event` bevat nuttige informatie over de gebeurtenis die de regel heeft geactiveerd. De gemakkelijkste manier om te bepalen welke gebeurtenisgegevens beschikbaar zijn is `event` aan de console van binnen uw douanecode te registreren:

```javascript
console.log(event);
```

Voer de regel in een browser uit en inspecteer het geregistreerde gebeurtenisobject in de browserconsole. Nadat u begrijpt welke informatie beschikbaar is, kunt u het voor programmatic besluit binnen uw douanecode gebruiken, een deel van het `event` voorwerp naar een server verzenden, etc.

### Verwerking van aangepaste code

De Core-extensie, die beschikbaar is voor alle Adobe Experience Platform-gebruikers, bevat een aangepaste code voor het uitvoeren van door de gebruiker opgegeven JavaScript of HTML. Het is vaak nuttig voor gebruikers om te begrijpen hoe de regels met de acties van de Code van de Douane worden verwerkt.

#### Regels die gebeurtenissen boven of onder op de pagina gebruiken

Code uit aangepaste handelingen wordt ingesloten in de hoofdtagbibliotheek. De code wordt naar het document geschreven met document.write. Als een regel veelvoudige acties van de Code van de Douane heeft, wordt de code geschreven in de orde die in de regel wordt gevormd.

#### Regels voor elke andere gebeurtenis dan de boven- of onderzijde van de pagina

Code uit aangepaste handelingen wordt vanaf de server geladen en naar het document geschreven met [Postscript](https://github.com/krux/postscribe). Als een regel veelvoudige acties van de Code van de Douane heeft, wordt de code geladen parallel van de server, maar in de orde geschreven die in de regel wordt gevormd.

Tijdens het gebruik van document.write nadat een pagina is geladen, zouden er doorgaans problemen optreden. Dit is echter geen probleem voor code die via aangepaste code-handelingen wordt geleverd. U kunt document.write binnen acties van de Code van de Douane ongeacht gebruiken wanneer de code zal worden uitgevoerd.

#### Aangepaste codevalidatie

De validator die in de tagcode-editor wordt gebruikt, is ontworpen om problemen met door ontwikkelaars geschreven code te identificeren. De code die door een minificatieproces-zoals code AppMeasurement.js is gegaan die van de Manager van de Code wordt gedownload-zou verkeerd kunnen worden gemarkeerd als hebbend kwesties door validator, die gewoonlijk kan worden genegeerd.

#### Handelingvolgorde

Wanneer de optie &quot;Regelcomponenten in volgorde uitvoeren&quot; van eigenschapinstellingen is ingeschakeld, kunt u volgende regelcomponenten laten wachten terwijl uw handeling een asynchrone taak uitvoert.  Dit werkt anders voor aangepaste JavaScript- en HTML-code.

*JavaScript*

Wanneer u een aangepaste JavaScript-code maakt, kunt u een [Belofing](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) uit uw handeling retourneren. De volgende actie in de regel zal slechts worden uitgevoerd wanneer de teruggekeerde belofte wordt opgelost. Als de belofte wordt verworpen, zullen de volgende acties van de regel niet worden uitgevoerd.

>[!NOTE]
>
>Dit werkt alleen als uw JavaScript niet is ingesteld op globaal uitvoeren. Als u uw actie van de douanecode in het globale werkingsgebied uitvoert, zullen de markeringen de belofte behandelen zoals onmiddellijk opgelost en zich op het volgende punt in de verwerkingsrij bewegen.

Een voorbeeld van een aangepaste JavaScript-codehandeling die een belofte retourneert:

```javascript
return new Promise(function(resolve, reject) {
  setTimeout(function() {
    if (new Date().getDay() === 5) {
      resolve();
    } else {
      reject();
    }
  }, 1000);
});
```

*HTML*

Wanneer u een aangepaste HTML-codehandeling maakt, is een functie met de naam `onCustomCodeSuccess()` beschikbaar voor gebruik in uw aangepaste code. U kunt deze functie aanroepen om aan te geven dat de aangepaste code is voltooid en dat tags kunnen worden toegepast bij het uitvoeren van volgende handelingen. Aan de andere kant, als uw douanecode op één of andere manier ontbrak, kunt u `onCustomCodeFailure()` roepen. Hiermee wordt aangegeven dat tags de volgende handelingen uit die regel niet mogen uitvoeren.

Een voorbeeld van een aangepaste HTML-codehandeling die de nieuwe callbacks gebruikt:

```html
<script>
setTimeout(function() {
  if (new Date().getDay() === 5) {
    onCustomCodeSuccess();
  } else {
    onCustomCodeFailure();
  }
}, 1000);
</script>
```

## Gegevenstelelementtypen van de kernextensie

Gegevenselementen worden bepaald door de extensie. Er is geen limiet aan de typen die kunnen worden gemaakt.

De volgende secties beschrijven de types van gegevenselementen beschikbaar in de uitbreiding van de Kern. Andere extensies gebruiken andere typen gegevenselementen.

### Cookie

In het veld cookie naam kan naar een beschikbaar domeincookie worden verwezen.

#### Voorbeeld:

`cookieName`

### Constante

Elke constante tekenreekswaarde waarnaar vervolgens in handelingen of voorwaarden kan worden verwezen.

#### Voorbeeld:

`string`

### Aangepaste code

U kunt aangepaste JavaScript invoeren in de gebruikersinterface door Editor openen te selecteren en code in te voegen in het editorvenster.

Een terugkeerverklaring is noodzakelijk in het redacteursvenster om erop te wijzen welke waarde als waarde van het gegevenselement zou moeten worden gebruikt. Als een retourinstructie niet wordt opgenomen of als de waarde `null` of `undefined` wordt geretourneerd, wordt de standaardwaarde van het gegevenselement gebruikt als de waarde van het gegevenselement.

**Voorbeeld:**

```javascript
var pageType = $('div.page-wrapper').attr('class').split('')[1];
if (window.location.pathname == '/') {
  return 'homepage';
} else {
  return pageType;
}
```

Als het element van de douanecodegegevens als deel van een regeluitvoering wordt teruggewonnen, wordt een variabele genoemd `event` automatisch beschikbaar, die u van binnen uw douanecode kunt van verwijzingen voorzien. Het object `event` bevat nuttige informatie over de gebeurtenis die de regel heeft geactiveerd. De gemakkelijkste manier om te bepalen welke gebeurtenisgegevens beschikbaar zijn is `event` aan de console van binnen uw douanecode te registreren:

```javascript
console.log(event);
return true;
```

Voer de regel in een browser uit en inspecteer het geregistreerde gebeurtenisobject in de browserconsole. Zodra u begrijpt welke informatie onder de diverse regels beschikbaar is die uw gegevenselement kunnen gebruiken, kunt u het voor programmatic besluit binnen uw douanecode gebruiken of een stuk van het `event` voorwerp als waarde van het gegevenselement terugkeren.

### DOM-kenmerk

Elke elementwaarde kan worden opgehaald, zoals een div- of H1-tag.

#### Voorbeeld:

CSS-selectieketen:

`id#dc logo img`

Hiermee wordt de waarde opgehaald van:

`src`

### JavaScript-variabele

Met behulp van het padveld kan naar elk beschikbaar JavaScript-object of -variabele worden verwezen.

Taggegevenselementen kunnen worden gebruikt om uw opmaak van JavaScript-variabelen of objecteigenschappen vast te leggen. Deze waarden kunnen vervolgens worden gebruikt binnen uw extensies of aangepaste regels door te verwijzen naar de elementen met taggegevens. Als de bron van de gegevens verandert, is het slechts noodzakelijk om de verwijzing naar de bron binnen UI van de Inzameling van Gegevens bij te werken.

In het onderstaande voorbeeld bevat de markering een JavaScript-variabele met de naam `Page_Name`.

```markup
<script>
  //data layer
  var Page_Name = "Homepage"
</script>
```

Wanneer u het gegevenselement in de UI van de Inzameling van Gegevens creeert, verstrek eenvoudig de weg aan die variabele.

Als u een gegevensverzamelingsobject gebruikt als onderdeel van uw gegevenslaag, gebruikt u puntnotatie in het pad om te verwijzen naar het object en de eigenschap die u in het gegevenselement wilt vastleggen, zoals `_myData.pageName` of `digitalData.pageName`, enzovoort.

#### Voorbeeld:

`window.document.title`

### Lokale opslag

Geef de naam van uw lokale opslagitem op in het veld Itemnaam lokale opslag.

Lokale opslag biedt browsers een manier om informatie van pagina tot pagina op te slaan ([https://www.w3schools.com/html/html5\_webstorage.asp](https://www.w3schools.com/html/html5_webstorage.asp)). Lokale opslag werkt veel zoals cookies, maar is veel groter en flexibeler.

Gebruik het opgegeven veld om de waarde op te geven die u hebt gemaakt voor een lokaal opslagitem, zoals `lastProductViewed.`

### Pagina-info

Gebruik deze gegevenspunten om pagina-info vast te leggen voor gebruik in uw regellogica of om informatie te verzenden naar Analytics of externe volgsystemen.

U kunt een van de volgende paginakenmerken selecteren voor gebruik in het gegevenselement:

* URL
* Hostnaam
* Pathname
* Protocol
* Referrer
* Titel

### Tekenreeksparameter van query

Geef één URL-parameter op in het veld URL-parameter.

Alleen de naamsectie is nodig en speciale aanduidingen zoals &quot;?&quot; of &quot;=&quot;moet worden weggelaten

#### Voorbeeld:

`contentType`

### Willekeurig getal

Gebruik dit gegevenselement om een willekeurig getal te genereren. Deze wordt vaak gebruikt voor het nemen van monsters van gegevens of het maken van id&#39;s, zoals een Actief-id. Het willekeurige getal kan ook worden gebruikt om vertrouwelijke of salt-gevoelige gegevens te verkrijgen. Voorbeelden hiervan zijn:

* Een hoogte-id genereren
* Plaats het nummer in een gebruikerstoken of tijdstempel om ervoor te zorgen dat het uniek is
* Voer een unidirectionele knoeiboel op PII gegevens uit
* Willekeurig beslissen wanneer een enquêteverzoek op de plaats moet tonen

Geef de minimum- en maximumwaarden voor het willekeurige getal op.

**Standaardwaarden:**

Minimaal: 0

Maximaal: 1000000000

### Sessieopslag

Geef de naam van het opslagitem voor de sessie op in het veld Naam opslagitem voor sessie.

Sessieopslag is vergelijkbaar met lokale opslag, behalve dat de gegevens worden verwijderd nadat de sessie is beëindigd, terwijl lokale opslag of een cookie de gegevens kan behouden.

### Bezoekergedrag

Net als Pagina-info gebruikt dit gegevenselement gangbare gedragstypen om logica binnen regels en andere oplossingen voor Platforms te verrijken.

Selecteer een van de volgende kenmerken voor bezoekersgedrag:

* Landingspagina
* Verkeersbron
* Minuten op site
* Aantal sessies
* Aantal sessiepagina&#39;s
* Aantal LiveTime-paginaweergaven
* Is nieuwe bezoeker

Enkele gangbare gebruiksgevallen zijn:

* Een enquête weergeven nadat een bezoeker vijf minuten op de site is geweest
* Als dit de landingspagina voor het bezoek is, vult u een metrische analyse in
* Nieuwe aanbieding weergeven aan bezoeker na X-aantal aantal aantal sessies
* Een nieuwsbrief weergeven als dit een eerste bezoeker is
