---
keywords: Experience Platform;huis;populaire onderwerpen;dataset;Dataset;tijd om te leven;ttl;tijd-aan-levende;pseudoniem;pseudoniem profielen;gegevensvervaldatum;vervaldatum;
solution: Experience Platform
title: Vervaldatum van gegevens van pseudoniem profiel
description: Dit document biedt algemene richtlijnen voor het configureren van gegevensvervaldatum voor Pseudoniem-profielen in Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: 3f776255ca858a86f501fd587c44fe176c45e103
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 0%

---


# Verlopen gegevens van pseudoniem-profielen [!BADGE Beperkte release]

In Adobe Experience Platform wordt een profiel voor het verlopen van Pseudoniem-gegevens overwogen als het aan de volgende voorwaarden voldoet:

- De identiteitstypen van het gekoppelde profiel komen overeen met het door de klant opgegeven pseudoniem of onbekend identiteitstype.
   - Als het identiteitstype van het profiel bijvoorbeeld `ECID`, `GAID`, of `AAID`. Het gekoppelde profiel heeft geen id&#39;s van een ander type identiteit. In dit voorbeeld wordt een vast profiel wel **niet** beschikken over een e-mail- of CRM-identiteit.
- Er heeft zich geen activiteit voorgedaan in een door de gebruiker gedefinieerde hoeveelheid tijd. De activiteit wordt bepaald of door om het even welke Gebeurtenissen van de Ervaring die of klant-in werking gestelde updates aan de profielattributen worden opgenomen.
   - Bijvoorbeeld, wordt een nieuwe gebeurtenis van de paginamening of de update van het paginakenmerk beschouwd als een activiteit. Nochtans, is een niet gebruiker-in werking gestelde update van het segmentlidmaatschap **niet** beschouwd als een activiteit. Op dit moment is het bijhouden van gegevens op profielniveau gebaseerd op de tijd van inname om de gegevensvervaldatum te berekenen.

## Toegang {#access}

De vervaldatum van gegevens van het Pseudoniem Profiel kan niet door de Platform UI of APIs worden gevormd. In plaats daarvan moet u contact opnemen met ondersteuning om deze functie in te schakelen. Neem de volgende gegevens op wanneer u contact opneemt met de ondersteuningsafdeling:

- De identiteitstypen die voor het Pseudoniem-profiel moeten worden gebruikt, worden verwijderd.
   - Bijvoorbeeld: `ECID` alleen, `AAID` alleen, of een combinatie van `ECID` en `AAID`.
- De hoeveelheid tijd die moet worden gewacht voordat een pseudoniem profiel wordt verwijderd. De standaardaanbeveling voor klanten is 30 dagen. Deze waarde kan echter afwijken, afhankelijk van uw gebruiksscenario.
- Het huidige aantal profielen in vergelijking met het aantal licentieprofielen.

## Veelgestelde vragen {#faq}

In de volgende sectie worden vaak gestelde vragen over de vervaldatum van gegevens van Pseudoniem-profielen weergegeven:

### Welke gebruikers zouden de vervaldatum van Pseudoniem profielgegevens moeten gebruiken?

- Als u een schakelaar gebruikt die direct gegevens van hun bron naar Platform verzendt.
- Als u een website hebt die ongeautoriseerde klanten massaal bedient.
- Als u buitensporige profieltellingen in uw datasets hebt en bevestigd dat dit bovenmatige profieltelling wegens anonieme op koekje-gebaseerde identiteitstype is.
   - Om dit te bepalen, zou u het identiteitstype overlappende rapport moeten gebruiken. Meer informatie over dit rapport vindt u in LINK

### Wat zijn sommige bedenkingen u zich van zou moeten bewust zijn alvorens de gegevensvervaldatum van de Pseudoniem- profielenprofielen te gebruiken?

- De vervaldatum van pseudoniem profielgegevens wordt uitgevoerd op de **productie** sandbox.
- Als u deze functie hebt geactiveerd, wordt het verwijderen van profielen **permanent**. Er is **nee** een manier om de verwijderde profielen terug te draaien of te herstellen.
- Dit is **niet** een eenmalige opschoningstaak. De vervaldatum van Pseudoniem-profielgegevens wordt voortdurend één keer per dag uitgevoerd en er worden profielen verwijderd die overeenkomen met de invoer van de klant.
- **Alles** De vervaldatum van de Pseudoniem-profielgegevens heeft invloed op profielen die zijn gedefinieerd als Pseudoniem. Het doet het **niet** Het maakt niet uit of het profiel alleen Experience Event is of alleen profielkenmerken bevat.
- Deze opruiming zal **alleen** komt voor in Profiel. De identiteitsdienst kan de verwijderde identiteiten in de grafiek na de opruiming blijven weergeven in gevallen waarin het profiel twee of meer geassocieerde pseudoniem-identiteiten heeft (zoals `AAID` en `ECID`). Deze discrepantie zal in de nabije toekomst worden aangepakt.

### Hoe verschilt de vervaldatum van Pseudoniem Profile-gegevens van de bestaande Experience Event-gegevens?

Vervaldatum van Pseudoniem Profielgegevens en Vervaldatum van ervaringsgegevens zijn complementaire functies.

#### Granulariteit

Ervaar de gegevensvervaldatum van de Gebeurtenis werkt op een **gegevensset** niveau. Dientengevolge, kan elke dataset een verschillende het aflopen van gegevens hebben plaatsen.

De vervaldatum van gegevens van het Pseudoniem Profiel werkt op een **sandbox** niveau. Als gevolg hiervan is het verlopen van de gegevens van invloed op alle profielen in de sandbox.

#### Identiteitstypen

Ervaring gebeurtenisgegevens verlopen verwijdert gebeurtenissen **alleen** op basis van de tijdstempel van de gebeurtenisrecord. De opgenomen identiteitstypen zijn **genegeerd** voor vervaldoeleinden.

Vervaldatum van gegevens van pseudoniem profiel **alleen** overweegt profielen met identiteitsgrafieken die identiteitstypes bevatten die door de klant werden geselecteerd, zoals `ECID`, `AAID`of andere soorten cookies. Als het profiel **alle** aanvullend identiteitstype **niet** in de geselecteerde lijst van de klant, zal het profiel **niet** worden geschrapt.

#### Verwijderde items

Ervaring gebeurtenisgegevens verlopen **alleen** verwijdert gebeurtenissen en doet **niet** profielklassegegevens verwijderen. De profielklassegegevens worden alleen verwijderd wanneer alle gegevens over het profiel zijn verwijderd **alles** gegevenssets en er zijn **nee** nog resterende profielklassecords voor het profiel.

Vervaldatum van gegevens van pseudoniem profiel wordt verwijderd **beide** gebeurtenis- en profielrecords. Hierdoor worden ook de profielklassegegevens verwijderd.

### Hoe kan de gegevensvervaldatum van het Pseudoniem Profiel samen met de gegevensvervaldatum van de Gebeurtenis van de Ervaring worden gebruikt?

De vervaldatum van Pseudoniem Profielgegevens en Experience Event-gegevens kunnen worden gebruikt om elkaar aan te vullen.

U moet **altijd** De gegevensvervaldatum van de de Ervaring van de opstelling Gebeurtenis in uw datasets, die op uw behoeften wordt gebaseerd om gegevens over uw bekende klanten te behouden. Als de geldigheids-gebeurtenisgegevensvervaldatum is ingesteld, kunt u de gegevensvervaldatum van het Pseudoniem-profiel gebruiken om automatisch Pseudoniem-profielen te verwijderen. Doorgaans is de vervalperiode van de gegevens voor Pseudoniem Profielen korter dan de vervalperiode van de gegevens voor Experience Events.

Voor een typisch geval van gebruik, kunt u de gegevensvervaldatum van de Gebeurtenis van de Ervaring plaatsen gebaseerd op de waarden van uw bekende gebruikersgegevens en u kunt uw Pseudoniem gegevensvervaldatum van het Profiel aan een veel kortere duur plaatsen om de invloed van Pseudoniem profielen op uw Platform vergunningsnaleving te beperken.
