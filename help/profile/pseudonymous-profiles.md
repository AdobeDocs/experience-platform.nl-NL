---
keywords: Experience Platform;huis;populaire onderwerpen;dataset;Dataset;tijd om te leven;ttl;tijd-aan-levende;pseudoniem;pseudoniem profielen;gegevensvervaldatum;vervaldatum;
solution: Experience Platform
title: Vervaldatum van gegevens van pseudoniem profiel
description: Dit document biedt algemene richtlijnen voor het configureren van gegevensvervaldatum voor Pseudoniem-profielen in Adobe Experience Platform.
exl-id: e8d31718-0b50-44b5-a15b-17668a063a9c
source-git-commit: 9489156617f29d4aab2038b74f75a832ff4dc8eb
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 0%

---

# Verlopen gegevens van pseudoniem-profielen

In Adobe Experience Platform kunt u de vervaltijden van gegevens configureren voor Pseudoniem-profielen. Zo kunt u automatisch gegevens verwijderen uit het profielarchief die niet meer geldig of nuttig zijn voor uw gebruiksgevallen.

## Pseudoniem profiel {#pseudonymous-profile}

Een profiel wordt overwogen voor Pseudoniem gegevensvervaldatum als het aan de volgende voorwaarden voldoet:

- De identiteitsnaamruimten van het verbonden profiel komen overeen met de naamruimte die de klant heeft opgegeven als een pseudoniem of onbekend naamgebied.
   - Als de naamruimte van de identiteit van het profiel bijvoorbeeld `ECID`, `GAID` of `AAID` is. Het gekoppelde profiel heeft geen id&#39;s van een andere naamruimte. In dit voorbeeld, heeft een vastgemaakt profiel **** of geen e-mail of identiteit van CRM.
- Er heeft zich geen activiteit voorgedaan in een door de gebruiker gedefinieerde hoeveelheid tijd. De activiteit wordt bepaald of door om het even welke Gebeurtenissen van de Ervaring die of klant-in werking gestelde updates aan de profielattributen worden opgenomen.
   - Bijvoorbeeld, wordt een nieuwe gebeurtenis van de paginamening of de update van het paginakenmerk beschouwd als een activiteit. Nochtans, wordt een niet-gebruiker-in werking gestelde update van het publiekslidmaatschap **niet** beschouwd als een activiteit. Op dit moment is het bijhouden van gegevens op profielniveau gebaseerd op de tijd van de gebeurtenis voor Experience Events en de tijd van inname voor profielkenmerken om de gegevensvervaldatum te berekenen.

## Toegang {#access}

De vervaldatum van gegevens van het Pseudoniem Profiel kan niet door Platform UI of APIs worden gevormd. In plaats daarvan moet u contact opnemen met ondersteuning om deze functie in te schakelen. Neem de volgende gegevens op wanneer u contact opneemt met de ondersteuningsafdeling:

- De naamruimten die in overweging moeten worden genomen voor het Pseudoniem-profiel, worden verwijderd.
   - Bijvoorbeeld: `ECID` alleen, `AAID` alleen of een combinatie van `ECID` en `AAID` .
- De hoeveelheid tijd die moet worden gewacht voordat een pseudoniem profiel wordt verwijderd. De standaardaanbeveling voor klanten is 14 dagen. Deze waarde kan echter afwijken, afhankelijk van uw gebruiksscenario.

## Veelgestelde vragen {#faq}

In de volgende sectie worden vaak gestelde vragen over de vervaldatum van gegevens van Pseudoniem-profielen weergegeven:

### Hoe verschilt de vervaldatum van Pseudoniem Profiel van de gegevens van de Gebeurtenis van de Ervaring?

De gegevensvervaldatum en de gegevensvervaldatum van de Gebeurtenis van het Pseudoniem Profiel zijn complementaire eigenschappen.

#### Korreligheid

De pseudoniem gegevens van het Profiel vervalsen werken op a **zandbak** niveau. Als gevolg hiervan is het verlopen van de gegevens van invloed op alle profielen in de sandbox.

De gegevensvervaldatum van de Gebeurtenis van de ervaring werkt op het niveau van de a **dataset**. Dientengevolge, kan elke dataset een verschillende gegevensvervalbepaling hebben.

#### Identiteitstypen

De pseudoniem gegevens van het Profiel verlopen **slechts** overweegt profielen die identiteitsgrafieken hebben die identiteitsnamespaces bevatten die door de klant, zoals `ECID`, `AAID`, of andere soorten koekjes werden geselecteerd. Als het profiel **om het even welke** extra identiteitsnamespace bevat die **niet** in de geselecteerde lijst van de klant was, zal het profiel **** niet worden geschrapt.

De gegevensvervaldatum van de Gebeurtenis van de ervaring verwijdert gebeurtenissen **slechts** die op timestamp van het gebeurtenisverslag wordt gebaseerd. De inbegrepen identiteitsnamespaces zijn **genegeerd** voor vervaldoeleinden.

#### Verwijderde items

De pseudoniem gegevensvervaldatum van het Profiel verwijdert **zowel** gebeurtenis als profielverslagen. Hierdoor worden ook de profielklassegegevens verwijderd.

De gegevensvervaldatum van de Gebeurtenis van de ervaring **slechts** verwijdert gebeurtenissen en **verwijdert** geen gegevens van de profielklasse. De gegevens van de profielklasse worden slechts verwijderd wanneer alle gegevens over **alle** datasets worden verwijderd en er **geen** dossiers van de profielklasse blijven voor het profiel.

### Hoe kan de gegevensvervaldatum van het Pseudoniem Profiel samen met de gegevensvervaldatum van de Gebeurtenis van de Ervaring worden gebruikt?

De gegevensvervaldatum van het Pseudoniem Profiel en de gegevensvervaldatum van de Gebeurtenis van de Ervaring kunnen worden gebruikt om elkaar aan te vullen.

U zou **altijd** de gegevensvervalsing van de Gebeurtenis van de opstellingsErvaring in uw datasets, die op uw behoeften worden gebaseerd om gegevens over uw bekende klanten te behouden. Zodra de gegevensvervaldatum van de Gebeurtenis van de Ervaring opstelling is, kunt u Pseudoniem de gegevensvervaldatum van het Profiel gebruiken om Pseudoniem Profielen automatisch te verwijderen. Doorgaans is de gegevensvervalperiode voor Pseudoniem Profielen korter dan de periode waarin de gegevens verlopen voor Experience Events.

Voor een typisch gebruiksgeval, kunt u uw de gegevensvervaldatum van de Gebeurtenis van de Ervaring plaatsen die op de waarden van uw bekende gebruikersgegevens wordt gebaseerd en u kunt uw Pseudoniem gegevensvervaldatum van het Profiel aan een veel kortere duur plaatsen om het effect van Pseudoniem profielen op uw de vergunningsnaleving van het Platform te beperken.

### Welke gebruikers zouden de vervaldatum van Pseudoniem profielgegevens moeten gebruiken?

- Als u Web SDK gebruikt om gegevens rechtstreeks naar Platform te verzenden.
- Als u een website hebt die ongeautoriseerde klanten massaal bedient.
- Als u buitensporige profieltellingen in uw datasets hebt en bevestigd dat deze bovenmatige profieltelling wegens anonieme op koekje-gebaseerde identiteitsnaamruimte is.
   - Om dit te bepalen, zou u het overlappende rapport van de identiteitsnaamruimte moeten gebruiken. Meer informatie over dit rapport kan in de [ sectie van het het overlappingsrapport van de identiteitsoverlapping ](./api/preview-sample-status.md#identity-overlap-report) van de gids van de voorproefstatus API worden gevonden.

### Wat zijn sommige bedenkingen u zich van zou moeten bewust zijn alvorens de gegevensvervaldatum van de Pseudoniem- profielenprofielen te gebruiken?

- De pseudoniem looppas van profielgegevens op a **zandbak** niveau. U kunt kiezen voor verschillende configuraties voor productie- en ontwikkelingssandboxen.
- Zodra u deze eigenschap hebt geactiveerd, is de schrapping van profielen **permanent**. Er is **geen** manier om de geschrapte profielen terug te rollen of te herstellen.
- Dit is **niet** eenmalig opschoontaak. De vervaldatum van Pseudoniem-profielgegevens wordt eenmaal per dag uitgevoerd en er worden profielen verwijderd die overeenkomen met de invoer van de klant.
- **Alle** profielen die als Pseudoniem profielen worden bepaald zullen door de Pseudoniem vervaldatum van profielgegevens worden beïnvloed. Het doet **niet** van belang als het profiel de Gebeurtenis van de Ervaring slechts is of als het slechts profielattributen bevat.
- Deze schoonmaakbeurt zal **slechts** in Profiel voorkomen. De identiteitsdienst kan de verwijderde identiteiten in de grafiek na de opschoonbewerking blijven weergeven in gevallen waarin het profiel twee of meer gekoppelde pseudoniem-identiteiten heeft (zoals `AAID` en `ECID` ). Deze discrepantie zal in de nabije toekomst worden aangepakt.
- De pseudoniem vervaldatum van profielgegevens **loopt niet** onmiddellijk, en kan tot drie dagen aan proces vergen.

### Hoe wisselt de vervaldatum van Pseudoniem-profielgegevens met de instructies voor de identiteitsdienstgegevens?

- De Dienst van de Identiteit [ &quot;eerste-binnen, eerste-uit&quot;schrappingssysteem ](../identity-service/guardrails.md) kon ECIDs van de identiteitsgrafiek schrappen, die in de Dienst van de Identiteit worden opgeslagen.
- Als dit verwijderingsgedrag ertoe leidt dat een ECID-profiel wordt opgeslagen in het Real-Time Klantprofiel (Profielarchief), verwijdert de vervaldatum van de Pseudoniem-profielgegevens dit profiel uit het profielarchief.
