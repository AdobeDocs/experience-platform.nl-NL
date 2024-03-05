---
title: Edge-profielen
description: Meer informatie over Edge-profielen en de bijbehorende terminologie, beschikbare gebieden voor randprofielen en de beschikbare services voor randprofielen.
exl-id: dcae267f-1d5a-4e90-b634-afd42b0d4edc
source-git-commit: 16e49628df73d5ce97ef890dbc0a6f2c8e7de346
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# Randprofielen

In Adobe Experience Platform is Real-Time Customer Profile de enige waarheidsbron voor entiteitsgegevens. Deze profielgegevens bevinden zich in een centraal knooppunt en kunnen gevallen gebruiken die afhankelijk zijn van de volledigheid en volledigheid van uw gegevens. In meer real-time gebruiksgevallen, waarbij tijdgevoeligheid belangrijker is, hebben randprofielen echter de voorkeur. Edge-profielen zijn lichtgewicht profielen die zich aan de randen bevinden en u helpen bij het gebruik van realtime-personalisatie.

Bijvoorbeeld, gebruiken de toepassingen van de Adobe zoals Adobe Target, de Bestemming van de Aanpassing, en Adobe Campaign randen om gepersonaliseerde klantenervaringen in real time te verstrekken. De gegevens worden verpletterd aan een rand door een projectie, met een projectiebestemming die de rand bepaalt waarnaar de gegevens zullen worden verzonden, en een projectieconfiguratie die de specifieke informatie bepaalt die op de rand beschikbaar zal worden gemaakt.

## Terminologie {#terminology}

Zorg ervoor dat u de volgende concepten begrijpt wanneer u met randen werkt:

- **Rand**: Een rand is een geografisch geplaatste server die gegevens opslaat en deze gemakkelijk toegankelijk maakt voor toepassingen.
- **Projectconfiguratie**: Een projectieconfiguratie beschrijft hoe een bepaalde entiteit aan de randen voor een bepaalde klant zou moeten worden herhaald en onder welke voorwaarden. Bijvoorbeeld, voor Luma (een steekproefklant), slechts zouden de gebieden leeftijd en het geslacht van de dataset na het schema van het Profiel aan de randen moeten verspreiden.
- **Randprojectie**: Een randprojectie is de toepassing van een projectieconfiguratie op een specifieke rand op één stuk gegevens met unieke identiteitskaart die aan een bepaald schema voor een bepaalde klant in overeenstemming is. Bijvoorbeeld een entiteit die het schema Profiel met identiteitskaart respecteert `CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8`, bezoeker van de Luma-website, gerepliceerd naar het VA6-datacenter, dat de velden bevat `age = 35` en `gender = male`.

Met andere woorden, gegevens worden door een projectie naar een rand geleid, met de **projectiebestemming** definiëren **die** rand waarnaar de gegevens worden verzonden en de **projectieconfiguratie** definiëren **wat** gegevens worden naar de opgegeven rand verzonden.

## Beschikbare gebieden {#regions}

De volgende gebieden zijn beschikbaar voor gebruik met rand:

- VA6
- OR2
- IRL1
- AUS3
- SGP3
- JPN3
- IND1

Al deze gebieden zijn geldige opties voor profielen om binnen te landen.

## Beschikbare services {#services}

De volgende services zijn ingeschakeld voor het opzoeken van profielen aan de rand:

- [Edge Profile Configuration Service](#edge-profile-configuration-service)
- [Projectiewerkerservice](#mepw)
- [Express Profile Service](#xps)

### Edge Profile Configuration Service {#edge-profile-configuration-service}

De Edge Profile Configuration Service stelt API&#39;s voor downstreamoplossingen en toepassingen beschikbaar om projectieconfiguraties te maken. U kunt deze API&#39;s gebruiken om de kenmerken en het publiek op te geven van een profiel dat naar de randen moet worden verzonden, en de randgebieden waar de projectie moet worden verzonden. U kunt nu **alle** van de randgebieden voor projecties.

### Projectiewerkerservice {#mepw}

De service Projectiewerker (MEPW) bewaakt wijzigingen die zich voordoen in de hub op profielen. Na onderzoek van de veranderingen in de configuraties, bereidt deze dienst de projecties voor en verzendt hen uit naar de eerder gespecificeerde randgebieden. Bovendien, verwerkt deze dienst de entiteit verfrist verzoeken en verzendt de vereiste projecties naar de noodzakelijke gebieden. Entiteitsvernieuwingen worden gebruikt om ervoor te zorgen dat de entiteit met hoge beschikbaarheid toegankelijk is.

### Express Profile Service {#xps}

Met de Express Profile Service (XPS) worden de profielen aan de verschillende randen opgehaald. Deze dienst ontvangt verzoeken van stroomafwaartse oplossingen, zoals Adobe Target of de bestemmingen van de Aanpassing van de Aanpassing, en kijkt omhoog de profielen van de gegevensbestanden op de randen, en verzendt het gevraagde profiel naar de het vragen oplossing. Als het profiel niet wordt gevonden, vernieuw verzoek wordt verzonden naar de bijbehorende hub.

## Volgende stappen

Nadat u deze handleiding hebt gelezen, hebt u een basiskennis van de randprofielen, waaronder informatie over de beschikbare gebieden en services voor randprofielen. Lees voor meer informatie over Adobe Experience Edge de [Overzicht van Edge Network](../web-sdk/home.md).

## Bijlage

In de volgende sectie worden veelgestelde vragen over randprofielen weergegeven:

### In welke gebieden kunnen randprofielen worden geland?

Randprofielen kunnen in verschillende regio&#39;s landen, afhankelijk van de huidige situatie.

Voor projectieconfiguraties worden alle wijzigingen in het profiel doorgegeven aan alle gebieden die in de profielconfiguratie worden vermeld.

Bovendien heeft elk Edge-profiel een schemakenmerk dat het UAR-gebied (User Activity Region) wordt genoemd. Alle randen die dit profiel de afgelopen 14 dagen heeft bezocht, worden vermeld in dit profielkenmerk. Als dit kenmerk aanwezig is in een profiel, worden wijzigingen in het profiel daarom ook verzonden naar alle gebieden die in de UAR worden vermeld.

### Hoe werkt gegevensvervaltijden met randprofielen?

Voor randprofielen bepaalt de vervaldatum van de gegevens hoe lang het profiel op de rand blijft voordat het wordt verwijderd. Vervaldatum gegevens **rollen**, wat betekent dat telkens als het profiel op rand wordt betreden, de tijd van de gegevensvervaldatum terugstelt. De gegevensvervaldatum duurt standaard 14 dagen.
