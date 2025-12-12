---
title: Opmerkingen bij de release Core Extension
description: De nieuwste release bevat informatie over de Core-extensie in Adobe Experience Platform.
exl-id: a049b2d5-7a00-435d-bcc7-112658a53a1e
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 1%

---

# Opmerkingen bij de release Core Extension

## vrijdag 25 september 2025

v3.4.4

* Voeg het veld `releaseNotesUrl` toe aan extension.json met deze pagina als waarde.
* Afhankelijkheden controleren.
* Verwijder Yarn en breng het bouwproces in overeenstemming met onze andere open-source bewaarplaatsen.


## vrijdag 8 mei 2025

v3.4.3

* Verhelpt een kwestie waar **Elementen van Gegevens** > **Hulpmiddelen Javascript** > **Eenvoudige Vervangen** een checkbox aan **toont vervangen allen** maar veroorzaakt een fout wanneer het proberen om de Regel met toegelaten checkbox te bewaren.
* Hiermee wordt @adobe/response-spectrum bijgewerkt naar v3.41.0.
* Hiermee wordt @adobe/reactor-sandbox bijgewerkt naar 13.2.1.

## donderdag 23 oktober 2024

v3.4.2

* Schema-validatiefout voor formulier corrigeren -> Gebeurtenis wijzigen wanneer &quot;en bepaalde eigenschapswaarden hebben..&quot; actief is.

## 29 maart 2023

v3.4.1

* Nieuwe native gedelegeerde webgebeurtenissen toevoegen:
   * Keydown
   * KeyUp
* Voegt de capaciteit toe om tegen vele waarden (&quot;Voeg nog&quot;opties) tegen de volgende afgevaardigden te testen:
   * Gebeurtenissen
      * Wijzigen
   * Voorwaarden
      * Cookie
      * Openingspagina
      * Parameter querytekenreeks
      * Traffic Source
      * Variabele
* Verandert de gebeurtenissen/de afgevaardigde EntersViewport om [&#x200B; API van de Waarnemer van de Intersectie te gebruiken &#x200B;](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API) in plaats van handopsporing van elementen die viewport ingaan.
* Verwijdert code die DTM koekjes aan LocalStorage migreerde.
* Logs een waarschuwing aan de console wanneer LocalStorage en SessionStorage APIs niet beschikbaar zijn.

## woensdag 4 januari 2022

v3.3.0

* Verandert de [&#x200B; Actie van de Vraag van de Trekker Direct &#x200B;](./overview.md#direct-call-action) zodat u de informatie van de douanegebeurtenis kunt leveren om naar directe vraagregels te verzenden.

## zaterdag 8 oktober 2021

v3.2.2

* Het JSON-schema voor voorwaardelijke-waardengegevens corrigeren voor alle beschikbare operatoren.
* https://github.com/adobe/reactor-extension-core/issues/64 herstellen.

## vrijdag 23 september 2021

v3.2.1

* Probleem verholpen waarbij de initialisatie van de weergave van het element met voorwaardelijke waarde niet goed werkte als de veldwaarden 0 waren.

## vrijdag 23 september 2021

v3.2.0

De volgende wijzigingen zijn aangebracht in het gegevenselement Voorwaardelijke waarde:

* Voeg een selectievakje voor de voorwaardelijke en terugvalwaarden toe waarmee de gebruiker kan kiezen of niet-gedefinieerde waarde de geretourneerde waarde moet zijn.
* Getalwaarden worden weergegeven als getallen in het instellingenobject.
* Voorwaardelijke waarde is niet meer vereist, zodat deze zich op dezelfde manier kan gedragen als de terugvalwaarde.

## zaterdag 17 september 2021

v3.1.1

* Corrigeer een JS-fout waardoor de weergave van de datumbereikvoorwaarde niet kon worden geladen.

## vrijdag 16 september 2021

v3.1.0

Er zijn nieuwe gegevenselementen toegevoegd:

* Samengevoegd object - selecteer meerdere gegevenselementen die elk een object leveren. Deze objecten worden diep (recursief) samengevoegd om een nieuw object te maken.
* Voorwaardelijke waarde - Retourneer een van twee waarden (conditionalValue of fallbackValue) op basis van het resultaat van de vergelijking.
* Runtime Environment - Return one of the following Launch environment variables: environment stage, library build date, property name, property ID, rule name, rule id, event type, event detail payload, direct call identifier.
* JavaScript Tools - Wrapper voor algemene JavaScript-bewerkingen: eenvoudige tekenreeksmanipulatie (vervangen, subtekenreeks, regex match, eerste en laatste index, split, slice), eenvoudige arraybewerkingen (segment, samenvoeging, pop, shift) en universele basisbewerkingen (segment, lengte).
* Apparaatkenmerken - Retourapparaatkenmerken zoals venstergrootte of schermgrootte.

## donderdag 11 augustus 2021

v3.0.0

* PDCL-6153: Voegt steun toe om volledig - gekwalificeerde URL voor caching acties van de douanecode betrouwbaar te trekken.

v3.0.0 van de uitbreiding van de Kern wordt gekoppeld aan veranderingen in [&#x200B; v27.2.0 van het Web van Turbines runtime &#x200B;](https://github.com/adobe/reactor-turbine/releases/tag/v27.2.0), die gebruikers toestaat om hun bibliotheek onder vele Adobe-Beheerde ontvangende gebieden te laden als het bedrijf van de gebruiker Premium CDN steunt.

Deze upgrade is optioneel en achterwaarts compatibel voor gebruikers zonder Premium CDN en is verplicht voor klanten die Premium CDN op hun bedrijf hebben ingeschakeld.

## vrijdag 20 mei 2021

v2.0.7

* Hiermee wordt een probleem verholpen waarbij muisinteractie op tekstinvoer niet meer correct werkte.
* Hiermee wordt het gebruik van de voorwaarden van de browser en het besturingssysteem afgekeurd.

## woensdag 4 mei 2021

v2.0.6

* Kleine update voor het corrigeren van pictogrammen die worden vervormd wanneer de schermgrootte verandert.

## vrijdag 11 maart 2021

v2.0.5

* Bijgewerkte code in de runtime evaluatie voor gebeurtenissen en acties die een vertragingsoptie hebben, die nu waarden van gegevenselementen die in versie 2.0.4 worden toegevoegd, aan behoorlijk dwingen koorden aan aantallen steunen.

## woensdag 9 maart 2021

v2.0.4

* Ondersteuning voor gegevenselement toegevoegd voor verschillende velden - Ondersteuning voor gegevenselement is toegevoegd aan de volgende gebeurtenissen: &#39;Tijd op pagina&#39;, &#39;Weergave voor invoer&#39;, &#39;Aanwijzer&#39; en &#39;Afspeeltijd media&#39;. alsmede de volgende voorwaarden: &#39;Time on Site&#39; en &#39;Value Comparison&#39;
* Hiermee voegt u ondersteuning toe voor standaardgedrag voor ctrl/cmd + klikken en middenmuisklikken bij gebruik van Vertraging koppeling
* **Gemarkeerde verbindingsvertraging op de klikgebeurtenis als &quot;niet meer gesteund&quot;.** - meer informatie kan op het [&#x200B; Blog van de Inzameling van Gegevens &#x200B;](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/explainer-link-delay/ba-p/398403) voor Adobe Experience Platform worden gevonden

## donderdag 6 januari 2021

v1.9.0

* **Nieuwe &quot;Vraag van de Trekker de Directe&quot;Actie** - de uitbreiding van de Kern omvat nu een nieuw geroepen actietype `Trigger Direct Call`.  Dit kan worden gebruikt wanneer u een directe vraagregel via een actie van een verschillende regel wilt teweegbrengen. Deze wordt rechtstreeks toegewezen aan de methode `_satellite.track()` . Hartelijk dank aan Jan Exner voor deze bijdrage.

## 8 december 2020

v1.8.4

* Probleem verholpen waarbij een gebruiker de instelling van het CDV niet één keer kon wissen of ongedaan maken.

## 28 juli 2020

v1.8.3

* Probleem verholpen waarbij de CSP één keer werd gelezen bij het opstarten van de extensie in plaats van vers te worden opgehaald tijdens het aanroepen van aangepaste code.

## 13 juli 2020

v1.8.2

* Probleem verholpen waarbij de aangepaste code-actie een fout genereerde voor HTML-code die tokens zonder tagnaam bevat (bijvoorbeeld opmerkingen).

## 10 juli 2020

v1.8.1

* Probleem verholpen waarbij aangepaste HTML-entiteiten binnen kenmerken van `script` - en `style` -tags niet correct werden gedecodeerd voordat ze naar de pagina werden geschreven.&quot;
* Probleem verholpen waarbij een fout optreedt wanneer een externe aangepaste code-actie geen inhoud bevat. Externe aangepaste code-actie is de actie die wordt geladen vanuit een ander bestand dan de bibliotheek (dit gebeurt wanneer de gebeurtenis die de regel veroorzaakt, niet libraryLoaded of pageBottom is)

## 6 juli 2020

v1.8.0

* **Verbintenissen in de Code van de Douane** - de voorwaarden van de Code van de Douane en de acties van JavaScript die niet in het globale werkingsgebied uitvoeren kunnen nu Beloften terugkeren.  U kunt deze gebruiken om volgende voorwaarden en handelingen te laten wachten tot een asynchroon proces in de aangepaste code is voltooid voordat u naar het volgende item gaat.
* **Callbacks in de Acties van de Code van de Douane van HTML** - u kunt het zelfde ding in de acties van de Code van de Douane van HTML bereiken gebruikend `onCustomCodeSuccess()` en `onCustomCodeFailure()` callbacks.

Gelieve te verwijzen naar de [&#x200B; Verwijzing van de Uitbreiding van de Kern &#x200B;](./overview.md) in de Voorwaarden > de Code van de Douane en de Acties > de Code van de Douane voor meer gedetailleerde informatie.

## 7 april 2020

v1.7.3

* &lbrace;de verhoging van de het gebiedslengte van de Tekst **- de inputgebieden van de Tekst werden veranderd in een flex lay-out om het het schermbreedte van de gebruiker beter te gebruiken, en meer ruimte voor langere tekstkoorden te geven.**

## 1 november 2019

v1.7.0

* **Toegang tot `event` Variabele binnen het Element van de Gegevens van de Code van de Douane** - u kunt de gebeurtenis van binnen een element van de douanecodegegevens nu van verwijzingen voorzien wanneer looppas binnen de context van een regel. Het object bevat nuttige informatie over de gebeurtenis die de regel heeft geactiveerd. Ik dank Stewart Schilling voor deze bijdrage.

## 7 oktober 2019

v1.6.2

* **Nieuw &quot;Constant&quot;Type van Element van Gegevens** - de uitbreiding van de Kern omvat nu een nieuw genoemd type van gegevenselement `Constant`.  Dit kan worden gebruikt wanneer u een constante waarde wilt opslaan waarnaar in diverse voorwaarden, handelingen of aangepaste code wordt verwezen. Hartelijk dank aan Jan Exner voor deze bijdrage.

## donderdag 11 september 2019

v1.6.1

* **Steun voor CSP één keer** - de uitbreiding van de Kern heeft nu een facultatieve configuratieparameter. U kunt een gegevenselement toevoegen dat naar één keer verwijst. Indien gevormd, gebruiken alle gealigneerde manuscripten die een markering aan de pagina toevoegt nonce die u hebt gevormd. Deze wijziging ondersteunt het gebruik van een Content Security Policy met een nonce, zodat tagscripts nog steeds in een CSP-omgeving kunnen worden geladen. U kunt meer over het gebruiken van markeringen met CSP [&#x200B; hier &#x200B;](../../../ui/client-side/content-security-policy.md) lezen.

## woensdag 18 juni 2019

v1.5.0

* **het Directe Loggen van de Vraag** - Browser het registreren voor directe vraagregels zal nu extra details verstrekken wanneer het wordt overgegaan.

## donderdag 8 mei 2019

v1.4.3

* **Gebieden van de Input** - de gebieden van de Input zijn nu veel langer!
* **de Gebeurtenis van de Douane** - het gebeurtenistype van de Douane kan nu met gebeurtenissen worden gebruikt die van venster worden verzonden.
* **Bug Fix** - herstelde een insect waar de Voorwaarde van de Vergelijking van de Waarde geen 0 waarde zou houden.
* **Bug Fix** - uitwisseling \_url gebied is bijgewerkt, zodat kunt u de lijst van de Uitbreiding van de Kern in Adobe Exchange nu zien.

## woensdag 8 januari 2019

v1.4.2

* **gaat gebeurtenis Viewport van Ingangen** in - eerder zou de gebeurtenis van Viewport van Inters slechts één keer per pagina teweegbrengen. Dit gedrag kan nu worden gevormd om telkens als het element viewport ingaat te teweegbrengen.
* **gebeurtenis van de Gebeurtenis van de Douane** - de Gebeurtenissen van de Douane kunnen contextuele gegevens nu bevatten die binnen van voorwaarden en acties kunnen worden gebruikt.
* **klik gebeurtenis** - wanneer u een verbindingsvertraging op de gebeurtenis van de Klik plaatst, die nu behoorlijk voor nakomelingen van het anker en niet alleen op het anker zelf zal registreren.

## vrijdag 8 november 2018

* **de optie van de Cohort van de Persistent** - de optie om een cohort voort te zetten is toegevoegd aan de Voorwaarde van de Steekproef. Dit heeft het effect dat een gebruiker in- of uitgaat van de voorbeeldcohort tijdens sessies. Als bijvoorbeeld het selectievakje &#39;persnel blijven&#39; is ingeschakeld en de voorwaarde de eerste keer true retourneert wanneer deze voor een bepaalde bezoeker wordt uitgevoerd, retourneert deze waarde true op alle volgende reeksen van de voorwaarde voor dezelfde bezoeker. Op dezelfde manier als het selectievakje &#39;persnel blijven&#39; is ingeschakeld en de voorwaarde de eerste keer dat deze voor een bepaalde bezoeker wordt uitgevoerd false retourneert, retourneert deze false op alle volgende reeksen van de voorwaarde voor dezelfde bezoeker.
* **Bug Fix** - Vaste een kwestie waar een regel die een gebeurtenis van de Onderkant van de Pagina en een actie van de Code van de Douane op een pagina gebruikt waar de markeringen synchroon maar incorrect werden geladen (geen vraag aan `_satellite.pageBottom()`) website inhoud zou ontruimen.
* **Bug Fix** - Vaste een kwestie waar de Kijker van Ingangen niet zou functioneren als de markeringsbibliotheek asynchroon werd geladen en volledig ladend nadat de browser gebeurtenis DOMContentLoaded werd in brand gestoken.

## vrijdag 24 mei 2018

* **Eigenschap** - voegde een voorwaarde van de Vergelijking van de Waarde toe, vergelijkt dit twee waarden gebruikend om het even welke verscheidene beschikbare exploitanten. Dit vervangt de functionaliteit van verscheidene oudere voorwaarden die veel te specifiek waren.
* **Eigenschap** - Toegevoegd een Max voorwaarde van de Frequentie, staat deze voorwaarde u toe om het aantal tijden te specificeren de voorwaarde waar binnen een tijdspanne of gebeurtenisvoorkomen zou moeten terugkeren. Voorbeelden: 5 keer per dag, 2 keer per bezoek.

## donderdag 11 april 2018

* **Eigenschap** - de elementen van Gegevens kunnen andere gegevenselementen nu van verwijzingen voorzien.

## woensdag 20 maart 2018

* **de moeilijke situatie van het insect** - de codevensters van de Douane werpen `document.write` fouten en niet uitvoeren in asynchrone plaatsingen
* **Bug moeilijke situatie** - de Belangrijkste modules waren niet inbegrepen in een bibliotheek
* **Bug bevestigt** - de Problemen kwamen met min en maximumwaarden op het Willekeurige gegevenselement van het Aantal voor

## donderdag 10 januari 2018

* **Eigenschap** - het Willekeurige Element van Gegevens van het Aantal
* **Eigenschap** - het Element van de Gegevens van Info van de Pagina
* **Eigenschap** - de Voorwaarde van de Datum
* **Eigenschap** - de Voorwaarde van de Steekproef
