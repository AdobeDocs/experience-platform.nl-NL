---
title: Opmerkingen bij de release Core Extension
description: De nieuwste release bevat informatie over de Core-extensie in Adobe Experience Platform.
exl-id: a049b2d5-7a00-435d-bcc7-112658a53a1e
source-git-commit: 5441c6ca0c15996ee06afa2c795ec5ae6e030f35
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 1%

---

# Opmerkingen bij de release Core Extension

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

## 4 januari 2022

v3.3.0

* Hiermee wijzigt u de [De Actie van de Vraag van de trekker Directe](./overview.md#direct-call-action) zodat u de informatie van de douanegebeurtenis kunt leveren om naar directe vraagregels te verzenden.

## 8 oktober 2021

v3.2.2

* Het JSON-schema voor voorwaardelijke-waardengegevens corrigeren voor alle beschikbare operatoren.
* https://github.com/adobe/reactor-extension-core/issues/64 herstellen.

## 23 september 2021

v3.2.1

* Probleem verholpen waarbij de initialisatie van de weergave van het element met voorwaardelijke waarde niet goed werkte als de veldwaarden 0 waren.

## 23 september 2021

v3.2.0

De volgende wijzigingen zijn aangebracht in het gegevenselement Voorwaardelijke waarde:

* Voeg een selectievakje voor de voorwaardelijke en terugvalwaarden toe waarmee de gebruiker kan kiezen of niet-gedefinieerde waarde de geretourneerde waarde moet zijn.
* Getalwaarden worden weergegeven als getallen in het instellingenobject.
* Voorwaardelijke waarde is niet meer vereist, zodat deze zich op dezelfde manier kan gedragen als de terugvalwaarde.

## 17 september 2021

v3.1.1

* Corrigeer een JS-fout waardoor de weergave van de datumbereikvoorwaarde niet kon worden geladen.

## 16 september 2021

v3.1.0

Er zijn nieuwe gegevenselementen toegevoegd:

* Samengevoegd object - selecteer meerdere gegevenselementen die elk een object leveren. Deze objecten worden diep (recursief) samengevoegd om een nieuw object te maken.
* Voorwaardelijke waarde - Retourneer een van twee waarden (conditionalValue of fallbackValue) op basis van het resultaat van de vergelijking.
* Runtime Environment - Retourneer een van de volgende Launch-omgevingsvariabelen: het milieustadium, bibliotheek bouwt datum, bezitsnaam, bezits identiteitskaart, regelnaam, regel identiteitskaart, gebeurtenistype, gebeurtenisdetaillading, directe vraagherkenningsteken.
* JavaScript-gereedschappen - Omsluitend voor veelgebruikte JavaScript-bewerkingen: eenvoudige tekenreeksmanipulatie (vervangen, subtekenreeks, regex-overeenkomst, eerste en laatste index, splitsen, segment), eenvoudige arraybewerkingen (segment, samenvoeging, pop, shift) en universele basisbewerkingen (segment, lengte).
* Apparaatkenmerken - Retourapparaatkenmerken zoals venstergrootte of schermgrootte.

## 11 augustus 2021

v3.0.0

* PDCL-6153: Hiermee voegt u ondersteuning toe om de volledig gekwalificeerde URL voor aangepaste codehandelingen in de cache op betrouwbare wijze te verkrijgen.

v3.0.0 van de Core-extensie is gekoppeld aan wijzigingen in [v27.2.0 van de webruntime van Turbine](https://github.com/adobe/reactor-turbine/releases/tag/v27.2.0), waarmee gebruikers hun bibliotheek kunnen laden onder vele hostinggebieden met Adobe-beheer als het bedrijf van de gebruiker Premium CDN ondersteunt.

Deze upgrade is optioneel en achterwaarts compatibel voor gebruikers zonder Premium CDN en is verplicht voor klanten die Premium CDN op hun bedrijf hebben ingeschakeld.

## 20 mei 2021

v2.0.7

* Hiermee wordt een probleem verholpen waarbij muisinteractie op tekstinvoer niet meer correct werkte.
* Hiermee wordt het gebruik van de voorwaarden van de browser en het besturingssysteem afgekeurd.

## 4 mei 2021

v2.0.6

* Kleine update voor het corrigeren van pictogrammen die worden vervormd wanneer de schermgrootte verandert.

## 11 maart 2021

v2.0.5

* Bijgewerkte code in de runtime evaluatie voor gebeurtenissen en acties die een vertragingsoptie hebben, die nu waarden van gegevenselementen die in versie 2.0.4 worden toegevoegd, aan behoorlijk dwingen koorden aan aantallen steunen.

## 9 maart 2021

v2.0.4

* Ondersteuning voor gegevenselement toegevoegd voor verschillende velden - Ondersteuning voor gegevenselement is toegevoegd aan de volgende gebeurtenissen: &#39;Time on Page&#39;, &#39;Enters Viewport&#39;, &#39;Hover&#39; en &#39;Media Time Played&#39;. alsmede de volgende voorwaarden: &#39;Time on Site&#39; en &#39;Value Comparison&#39;
* Hiermee voegt u ondersteuning toe voor standaardgedrag voor ctrl/cmd + klikken en middenmuisklikken bij gebruik van Vertraging koppeling
* **De vertraging van de gemarkeerde koppeling bij de klikgebeurtenis wordt niet meer ondersteund.** - meer informatie is te vinden op de [Blog gegevensverzameling](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/explainer-link-delay/ba-p/398403) voor Adobe Experience Platform

## 6 januari 2021

v1.9.0

* **Nieuwe actie &quot;Rechtstreekse aanroep activeren&quot;** - De extensie Core bevat nu een nieuw handelingstype met de naam `Trigger Direct Call`.  Dit kan worden gebruikt wanneer u een directe vraagregel via een actie van een verschillende regel wilt teweegbrengen. Deze wordt rechtstreeks toegewezen aan de `_satellite.track()` methode. Hartelijk dank [Jan Exner](https://twitter.com/jexner) voor deze bijdrage.

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

* Probleem verholpen waarbij aangepaste HTML-entiteiten binnen kenmerken van `script` en `style` tags zijn niet correct gedecodeerd voordat ze naar de pagina zijn geschreven.&quot;
* Probleem verholpen waarbij een fout optreedt wanneer een externe aangepaste code-actie geen inhoud bevat. Externe aangepaste code-actie is de actie die wordt geladen vanuit een ander bestand dan de bibliotheek (dit gebeurt wanneer de gebeurtenis die de regel veroorzaakt, niet libraryLoaded of pageBottom is)

## 6 juli 2020

v1.8.0

* **Promises in aangepaste code** - Aangepaste codevoorwaarden en JavaScript-handelingen die niet worden uitgevoerd in het algemene bereik, kunnen nu Promises retourneren.  U kunt deze gebruiken om volgende voorwaarden en handelingen te laten wachten tot een asynchroon proces in de aangepaste code is voltooid voordat u naar het volgende item gaat.
* **Callbacks in HTML Custom Code-handelingen** - U kunt hetzelfde bereiken in Aangepaste code HTML-handelingen met de opdracht `onCustomCodeSuccess()` en `onCustomCodeFailure()` callbacks.

Raadpleeg de [Referentie voor kernextensie](./overview.md) in de Voorwaarden > de Code van de Douane en Acties > de Code van de Douane voor meer gedetailleerde informatie.

## 7 april 2020

v1.7.3

* **Verlengde tekstveld** - De velden voor tekstinvoer zijn gewijzigd in een flex-indeling om de schermbreedte van de gebruiker beter te kunnen gebruiken en om meer ruimte te bieden voor langere tekstreeksen.

## 1 november 2019

v1.7.0

* **Toegang tot `event` Variabele binnen aangepast code-gegevenselement** - U kunt nu naar de gebeurtenis verwijzen vanuit een aangepast code-gegevenselement wanneer deze binnen de context van een regel wordt uitgevoerd. Het object bevat nuttige informatie over de gebeurtenis die de regel heeft geactiveerd. Hartelijk dank [Stewart Schilling](https://twitter.com/sdi_stewart) voor deze bijdrage.

## 7 oktober 2019

v1.6.2

* **Nieuw gegevenstype &quot;Constant&quot;** - De extensie Core bevat nu een nieuw gegevenstype voor gegevenselementen, genaamd `Constant`.  Dit kan worden gebruikt wanneer u een constante waarde wilt opslaan waarnaar in diverse voorwaarden, handelingen of aangepaste code wordt verwezen. Hartelijk dank [Jan Exner](https://twitter.com/jexner) voor deze bijdrage.

## 11 september 2019

v1.6.1

* **Ondersteuning voor CSP Nonce** - De extensie Core heeft nu een optionele configuratieparameter. U kunt een gegevenselement toevoegen dat naar één keer verwijst. Als dit is geconfigureerd, gebruiken alle inlinescripts die door een tag aan de pagina worden toegevoegd de nonce die u hebt geconfigureerd. Deze wijziging ondersteunt het gebruik van een Content Security Policy met een nonce, zodat tagscripts nog steeds in een CSP-omgeving kunnen worden geladen. U kunt meer lezen over het gebruik van labels met een CSP [hier](../../../ui/client-side/content-security-policy.md).

## 18 juni 2019

v1.5.0

* **Direct Call Logging** - Browser het registreren voor directe vraagregels zal extra details nu verstrekken wanneer het wordt overgegaan.

## 8 mei 2019

v1.4.3

* **Invoervelden** - Invoervelden zijn nu veel langer!
* **Aangepaste gebeurtenis** - Aangepast gebeurtenistype kan nu worden gebruikt bij gebeurtenissen die buiten het venster worden verzonden.
* **Bug Fix** - Een probleem verholpen waarbij de voorwaarde voor waardevergelijking geen waarde 0 zou bevatten.
* **Bug Fix** - Het veld Exchange\_url is bijgewerkt, zodat u nu de lijst Core Extension in Adobe Exchange kunt bekijken.

## 8 januari 2019

v1.4.2

* **De gebeurtenis Enters Viewport** - Eerder werd de gebeurtenis Enters Viewer slechts één keer per pagina geactiveerd. Dit gedrag kan nu worden gevormd om telkens als het element viewport ingaat te teweegbrengen.
* **Aangepaste gebeurtenis** - Aangepaste gebeurtenissen kunnen nu contextuele gegevens bevatten die kunnen worden gebruikt binnen voorwaarden en handelingen.
* **De gebeurtenis Click** - Wanneer u een koppelingsvertraging instelt voor de gebeurtenis Click, wordt dit nu correct geregistreerd voor de onderliggende elementen van het anker en niet alleen voor het anker zelf.

## 8 november 2018

* **Cohort behouden, optie** - De optie om een cohort te behouden is toegevoegd aan de bemonsteringsvoorwaarde. Dit heeft het effect dat een gebruiker in- of uitgaat van de voorbeeldcohort tijdens sessies. Als bijvoorbeeld het selectievakje &#39;persnel blijven&#39; is ingeschakeld en de voorwaarde de eerste keer true retourneert wanneer deze voor een bepaalde bezoeker wordt uitgevoerd, retourneert deze waarde true op alle volgende reeksen van de voorwaarde voor dezelfde bezoeker. Op dezelfde manier als het selectievakje &#39;persnel blijven&#39; is ingeschakeld en de voorwaarde de eerste keer dat deze voor een bepaalde bezoeker wordt uitgevoerd false retourneert, retourneert deze false op alle volgende reeksen van de voorwaarde voor dezelfde bezoeker.
* **Bug Fix** - Probleem verholpen waarbij een regel met een gebeurtenis Onder aan pagina en een handeling Aangepaste code op een pagina een regel bevatte waarin tags synchroon maar onjuist werden geladen (geen aanroep van `_satellite.pageBottom()`) wordt de inhoud van de website gewist.
* **Bug Fix** - Oplossing voor een probleem waarbij de invoerviewport niet zou werken als de tagbibliotheek asynchroon was geladen en klaar was met laden nadat de DOMContentLoaded-gebeurtenis van de browser was gestart.

## 24 mei 2018

* **Functie** - Toegevoegd een voorwaarde van de Vergelijking van de Waarde, vergelijkt dit twee waarden gebruikend om het even welke verscheidene beschikbare exploitanten. Dit vervangt de functionaliteit van verscheidene oudere voorwaarden die veel te specifiek waren.
* **Functie** - Toegevoegd een Max voorwaarde van de Frequentie, staat deze voorwaarde u toe om het aantal tijden te specificeren de voorwaarde binnen een tijdspanne of gebeurtenis waar zou moeten terugkeren. Voorbeelden: 5 keer per dag, 2 keer per bezoek.

## 11 april 2018

* **Functie** - Gegevenselementen kunnen nu verwijzen naar andere gegevenselementen.

## 20 maart 2018

* **Opgeloste problemen** - Aangepaste coevensters genereren `document.write` fouten en niet uitvoeren in asynchrone implementaties
* **Opgeloste problemen** - Hoofdmodules zijn niet opgenomen in een bibliotheek
* **Opgeloste problemen** - Er zijn problemen opgetreden met minimale en maximale waarden in het gegevenselement Willekeurig getal

## 10 januari 2018

* **Functie** - Gegevenselement willekeurige getallen
* **Functie** - Gegevenselement pagina-info
* **Functie** - Datumvoorwaarde
* **Functie** - Bemonsteringsconditie
