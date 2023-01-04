---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API
title: Voorbeeld-PQL-expressies voor berekende kenmerken
topic-legacy: guide
type: Documentation
description: Berekende kenmerken zijn functies die worden gebruikt om gegevens op gebeurtenisniveau samen te voegen tot kenmerken op profielniveau. Deze functies vereisen het gebruik van geldige PQL-expressies (Profile Query Language). In deze handleiding worden enkele van de meestgebruikte PQL-expressies voor berekende kenmerken beschreven.
exl-id: 7c80e2d3-919a-47f9-a59f-833a70f02a8f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 0%

---

# (Alpha) Voorbeeld-PQL-expressies voor berekende kenmerken

>[!IMPORTANT]
>
>De functie voor berekende kenmerken bevindt zich momenteel in alfa en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

In Adobe Experience Platform zijn berekende kenmerken functies die worden gebruikt om gegevens op gebeurtenisniveau samen te voegen tot kenmerken op profielniveau. Deze functies worden automatisch berekend zodat zij over segmentatie, activering, en verpersoonlijking kunnen worden gebruikt. Elk berekend attribuut wordt bepaald met basisinformatie, zoals een naam en een beschrijving, de schemaklasse en weg aan het gebied waarin de waarde zal worden gehouden, en een uitdrukking, de waarvan gegevens verwerkte waarde de waarde is die u in de gegevens verwerkte attributen zou willen opslaan.

De expressies die worden gebruikt in berekende kenmerken worden gemaakt met [!DNL Profile Query Language] (PQL), een XDM-compatibele querytaal (Experience Data Model) die is ontworpen om de definitie en uitvoering van query&#39;s voor gegevens in real-time klantprofiel te ondersteunen.

De berekende kenmerken ondersteunen momenteel de volgende functies: som, aantal, min, max en boolean. In deze handleiding worden enkele van de meestgebruikte PQL-expressies beschreven die u kunt gebruiken bij het definiëren van uw eigen berekende kenmerken voor uw organisatie. Ga voor meer informatie over PQL en koppelingen naar aanvullende opmaakrichtlijnen en voorbeelden van ondersteunde query&#39;s naar de [PQL-overzicht](../../segmentation/pql/overview.md).

## Streaming expressies

De volgende tabel bevat details voor veelgebruikte query-expressies die worden ondersteund in de streamingmodus.

| Beschrijving | PQL-expressie | Invoertype:<br/>Profiel- of ervaringsgebeurtenis (EE[]) | Type resultaat |
|---|---|---|---|
| Aantal downloads van afbeeldingen in de afgelopen 7 dagen. | xEvent[(timestamp komt &lt; 7 dagen vóór nu voor) en eventType=&quot;download&quot; en contentType = &quot;image&quot;].count() | Profiel en EE[] | Geheel |
| Som van de uitgaven van klanten aan sportartikelen in de afgelopen 7 dagen. | xEvent[(tijdstempel komt &lt; 7 dagen voor nu voor) en eventType=&quot;transaction&quot; en category = &quot;sportwedstrijen&quot;].sum(commerce.order.priceTotal) | Profiel en EE[] | Geheel getal of dubbel |
| Gemiddelde uitgaven van de klant voor sportartikelen in de afgelopen 7 dagen.<br/><br/>**Opmerking:** Hiervoor moeten drie berekende kenmerken worden gemaakt. | **ca1:** xEvent[(tijdstempel komt &lt; 7 dagen voor nu voor) en eventType=&quot;transaction&quot; en category = &quot;sportwedstrijen&quot;].sum(commerce.order.priceTotal)<br/><br/>**ca2:** xEvent[(tijdstempel komt &lt; 7 dagen voor nu voor) en eventType=&quot;transaction&quot; en category = &quot;sportwedstrijen&quot;].count()<br/><br/>**ca3:** ca1 / ca2 | Profiel en EE[] | Dubbel |
| Heeft de klant de afgelopen zeven dagen meer dan 100 dollar uitgegeven aan sportartikelen?<br/><br/>**Opmerking:** Hiervoor moeten twee berekende kenmerken worden gemaakt. | **ca1:** xEvent[(tijdstempel komt &lt; 7 dagen voor nu voor) en eventType=&quot;transaction&quot; en category = &quot;sportwedstrijen&quot;].sum(commerce.order.priceTotal)<br/><br/>**ca2:** ca1 > 100 | Profiel en EE[] | Boolean |
| Heeft de klant in de afgelopen 7 dagen een aankoop gedaan? | chain(xEvent, timestamp, [A: WAT(eventType = &quot;transaction&quot;) WHEN(&lt; 7 dagen daarvoor)]) | Profiel en EE[] | Boolean |
| Laagste bestedingen van gebruikers aan sportartikelen in de afgelopen 7 dagen. | xEvent[(tijdstempel komt &lt; 7 dagen voor nu voor) en eventType=&quot;transaction&quot; en category = &quot;sportwedstrijen&quot;].min(commerce.order.priceTotal) | Profiel en EE[] | Geheel getal of dubbel |
| Hoogste bestedingen van de gebruiker aan sportartikelen in de afgelopen 7 dagen. | xEvent[(tijdstempel komt &lt; 7 dagen voor nu voor) en eventType=&quot;transaction&quot; en category = &quot;sportwedstrijen&quot;].max(commerce.order.priceTotal) | Profiel en EE[] | Geheel getal of dubbel |
| Aantal downloads van elk gedownload product in de afgelopen 7 dagen, geïndexeerd op product. | xEvent[(timestamp komt &lt; 7 dagen vóór nu voor) en eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.count()) | Profiel en EE[] | Kaart[String, geheel getal] |
| De som van de numerieke eigenschap over de downloads van elk gedownload product in de laatste 7 dagen, geïndexeerd op product. | xEvent[(timestamp komt &lt; 7 dagen vóór nu voor) en eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal)) | Profiel en EE[] | Kaart[String, geheel getal] of Kaart[String, dubbel] |
| Gemiddelde numerieke eigenschap over downloads van elk gedownload product, in de laatste 7 dagen, geïndexeerd op product.<br/><br/>**Opmerking:** Hiervoor moeten drie berekende kenmerken worden gemaakt. | **ca1:** xEvent[(timestamp komt &lt; 7 dagen vóór nu voor) en eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal))<br/><br/>**ca2:** xEvent[(timestamp komt &lt; 7 dagen vóór nu voor) en eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.count())<br/><br/>**ca3:** ca2 / ca1 | Profiel en EE[] | Kaart[String, dubbel] |
| Minimum voor numerieke eigenschap boven downloads van elk gedownload product, in de laatste 7 dagen, geïndexeerd op product. | xEvent[(timestamp komt &lt; 7 dagen vóór nu voor) en eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.min(commerce.order.priceTotal)) | Profiel en EE[] | Kaart[String, geheel getal] of Kaart[String, dubbel] |
| Maximum aantal numerieke eigenschappen over downloads van elk gedownload product, in de laatste 7 dagen, die door product wordt geïndexeerd. | xEvent[(timestamp komt &lt; 7 dagen vóór nu voor) en eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.max(commerce.order.priceTotal)) | Profiel en EE[] | Kaart[String, geheel getal] of Kaart[String, dubbel] |
| Numerieke expressie in profiel, niet verwijzen naar gebeurtenissen. | if(person.gender = &quot;vrouwelijk&quot;, 60, 65) | Profiel | Geheel getal of dubbel |
| Booleaanse expressie in profiel, niet verwijzen naar gebeurtenissen. | person.bornYear >= 2000 | Profiel | Boolean |
| Tekenreeksexpressie op profiel, niet verwijzen naar gebeurtenissen. | if(homeAddress.countryCode in [&quot;US&quot;,&quot;MX&quot;,&quot;CA&quot;], &quot;NA&quot;, &quot;ROW&quot;) | Profiel | Tekenreeks |

## Batchexpressies

De volgende tabel bevat details voor query-expressies die alleen beschikbaar zijn in de batchmodus. Dit betekent dat deze momenteel niet beschikbaar zijn in streaming.

| Beschrijving | PQL-expressie | Invoertype:<br/>Profiel- of ervaringsgebeurtenis (EE[]) | Type resultaat |
|---|---|---|---|
| Of de som van de numerieke expressie over productdownloads in de laatste 7 dagen meer dan 100 bedraagt, geïndexeerd op product. | xEvent[(timestamp komt &lt; 7 dagen vóór nu voor) en eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal) > 100) | Profiel en EE[] | Kaart[String, Boolean] |
| Of de gemiddelde numerieke expressie tijdens productdownloads in de laatste 7 dagen groter is dan 100, geïndexeerd op product. | xEvent[(timestamp komt &lt; 7 dagen vóór nu voor) en eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.average(commerce.order.priceTotal) > 100) | Profiel en EE[] | Kaart[String, Boolean] |
| De optelling van verschillende metriek voor elk gedownload product, in de laatste 7 dagen, die door product wordt geïndexeerd. | xEvent[(timestamp komt &lt; 7 dagen vóór nu voor) en eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, {&quot;count&quot;: G.count(), &quot;sum&quot;: G.sum(commerce.order.priceTotal)) | Profiel en EE[] | Kaart[String, Object] waarbij Object een aangepast XDM-type is |
