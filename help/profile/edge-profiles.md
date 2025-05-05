---
title: Edge-profielen
description: Meer informatie over Edge-profielen en de bijbehorende terminologie, beschikbare gebieden voor randprofielen en de beschikbare services voor randprofielen.
exl-id: dcae267f-1d5a-4e90-b634-afd42b0d4edc
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# Edge-profielen

In Adobe Experience Platform is Real-Time Customer Profile de enige waarheidsbron voor entiteitsgegevens. Deze profielgegevens bevinden zich in een centraal knooppunt en kunnen gevallen gebruiken die afhankelijk zijn van de volledigheid en volledigheid van uw gegevens. In meer real-time gebruiksgevallen, waarbij tijdgevoeligheid belangrijker is, hebben randprofielen echter de voorkeur. Edge-profielen zijn lichtgewicht profielen die zich aan de randen bevinden en u helpen bij het gebruik van realtime-personalisatie.

Bijvoorbeeld, gebruiken de toepassingen van de Adobe zoals Adobe Target, de Bestemming van Personalization van de Douane, en Adobe Campaign randen om gepersonaliseerde klantenervaringen in real time te verstrekken. Gegevens worden met een projectie naar een rand omgeleid, waarbij een projectiebestemming de rand definieert waarnaar gegevens worden verzonden.

## Terminologie {#terminology}

Zorg ervoor dat u de volgende concepten begrijpt wanneer u met randen werkt:

- **Edge**: Een rand is een geografisch geplaatste server die gegevens opslaat en het gemakkelijk toegankelijk voor toepassingen maakt.
- **de projectie van Edge**: Een randprojectie is de systeemprojectiemening van profiel op een specifieke rand om profielgegevens met unieke identiteitskaart te vertegenwoordigen die aan een bepaald schema voor een bepaalde klant in overeenstemming is. Bijvoorbeeld, een entiteit die het schema van het Profiel met identiteitskaart `CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8` eerbiedigt, bezoeker van de website van de Luma, die aan het VA6 gegevenscentrum wordt herhaald, die de gebieden `age = 35` en `gender = male` bevat.

In andere termen, wordt het gegeven verpletterd aan een rand door een projectie, met de **projectiebestemming** bepalend **die** rand de gegevens zullen worden verzonden naar.

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

- [Projectiewerkerservice](#mepw)
- [Express Profile Service](#xps)

### Projectiewerkerservice {#mepw}

De service Projectiewerker (MEPW) bewaakt wijzigingen die zich voordoen in de hub op profielen. Na onderzoek van de veranderingen in de configuraties, bereidt deze dienst de projecties voor en verzendt hen uit naar de eerder gespecificeerde randgebieden. Bovendien, verwerkt deze dienst de entiteit verfrist verzoeken en verzendt de vereiste projecties naar de noodzakelijke gebieden. Entiteitsvernieuwingen worden gebruikt om ervoor te zorgen dat de entiteit met hoge beschikbaarheid toegankelijk is.

### Express Profile Service {#xps}

Met de Express Profile Service (XPS) worden de profielen aan de verschillende randen opgehaald. Deze dienst ontvangt verzoeken van stroomafwaartse oplossingen, zoals de bestemmingen van Adobe Target of van de Douane Personalization, en kijkt omhoog de profielen van de gegevensbestanden op de randen, en verzendt het gevraagde profiel naar de het vragen oplossing. Als het profiel niet wordt gevonden, vernieuw verzoek wordt verzonden naar de bijbehorende hub.

## Volgende stappen

Nadat u deze handleiding hebt gelezen, hebt u een basiskennis van de randprofielen, waaronder informatie over de beschikbare gebieden en services voor randprofielen. Voor meer informatie over de Ervaring Edge van de Adobe, te lezen gelieve het [ overzicht van de Edge Network ](../web-sdk/home.md#edge-network).

## Bijlage

In de volgende sectie worden veelgestelde vragen over randprofielen weergegeven:

### In welke gebieden kunnen randprofielen worden geland?

Edge-profielen kunnen in verschillende regio&#39;s landen, afhankelijk van de huidige situatie.

Bovendien heeft elk Edge-profiel een schemakenmerk dat het UAR-gebied (User Activity Region) wordt genoemd. Alle randen die dit profiel de afgelopen 14 dagen heeft bezocht, worden vermeld in dit profielkenmerk. Als dit kenmerk aanwezig is in een profiel, worden wijzigingen in het profiel daarom ook verzonden naar alle gebieden die in de UAR worden vermeld.

### Hoe werkt gegevensvervaltijden met randprofielen?

Voor randprofielen bepaalt de vervaldatum van de gegevens hoe lang het profiel op de rand blijft voordat het wordt verwijderd. Het verstrijken van gegevens is het rollen **&#x200B;**, zo betekent het dat telkens als het profiel op rand wordt betreden, de tijd van de gegevensvervalsing terugstelt. De gegevensvervaldatum duurt standaard 14 dagen.

### Welke gegevens zijn opgeslagen in het randprofiel?

In Edge Profile worden de profielkenmerken, profiel-id&#39;s en gekwalificeerde gebruikers-id&#39;s opgeslagen. De gegevensvervaldatum duurt standaard 14 dagen.
