---
solution: Experience Platform
title: Edge Network- en hubvergelijking
description: Meer informatie over de verschillende verwerkingspaden die beschikbaar zijn voor Adobe Experience Platform.
exl-id: 3e9c63d2-c798-44b4-870d-bf1551f29690
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 2%

---

# Edge Network- en hubvergelijking

Adobe Experience Platform is het krachtigste, meest flexibele en open systeem op de markt voor het ontwikkelen en beheren van volledige oplossingen die de ervaring van klanten stimuleren. U kunt Experience Platform gebruiken om klantgegevens en inhoud van elk systeem te centraliseren en te standaardiseren en om datamanagement en machinaal leren toe te passen om het ontwerp en de levering van rijke, gepersonaliseerde ervaringen drastisch te verbeteren. Als gevolg hiervan kan Experience Platform uw gegevens op verschillende manieren verwerken, zodat u uw gegevens op de best mogelijke manier kunt beoordelen.

## Servertypen

In Experience Platform kunnen gegevens op twee verschillende manieren worden verwerkt: Adobe Experience Platform-hub voor batch- en streaming-workflows en Edge Network voor real-time ervaringen.

### Adobe Experience Platform hub

De hub is een belangrijkste gegevenscentrum dat centraal wordt gevestigd en alle historische gegevens en rijke profielcontext bevat die in Adobe Experience Platform is verzameld. Dit staat u toe om robuustere en volledige gegevens naar uw stroomafwaartse diensten te verzenden en te ontvangen. Dientengevolge, zou de hub in scenario&#39;s moeten worden gebruikt waar de **gronheid** van de gegevens belangrijker is.

De beschikbare diensten op hub omvatten het volgende:

- Batchsegmentatie
- Streaming segmentering
- Profielen
- Bestemmingen
- Naamgrafiek
- Data Distiller - Query-service
- Source-connectors

### Experience Platform Edge Network

Edge Network is een server die zich fysiek dichter bij verschillende geografische locaties bevindt. Deze datacenters verwerken alle gegevens die zijn verzameld via de SDK-extensies en Edge Network-API&#39;s. De enige gegevens die op de Edge Network aanwezig zijn, zijn het gebruikerslidmaatschap, de profielidentiteiten en de kenmerken die nodig zijn voor personalisatie.

Met Edge Network kunt u sneller gegevens naar uw klanten verzenden en ontvangen, omdat deze dichter bij de eindgebruiker staan. Bovendien kunt u Edge Network gebruiken om verzoeken voor het doorsturen van gebeurtenissen en verzoeken voor tagbeheer te verwerken. Nochtans, verwerkt Edge Network slechts **gedrags** gegevens. Dientengevolge, zou Edge Network in scenario&#39;s moeten worden gebruikt waar de **snelheid** van de gegevens belangrijker is.

De volgende services zijn beschikbaar voor Edge Network:

- Edge-segmentatie
- Edge-profielen
- Edge-bestemmingen
- Dataverzameling
- SDK-extensies

## Locaties

De volgende sectie maakt een lijst van de plaatsen voor zowel hub als Edge Network.

![&#x200B; een diagram dat van de verschillende plaatsen voor zowel hub als servers van Edge Network een lijst maakt.](./images/servers/platform-server-locations.png)

**Hub**

- VA7 (Virginia, VS)
- NLD2 (Nederland)
- AUS5 (Australië)
- CAN2 (Canada)
- GBR9 (Verenigd Koninkrijk)
- IND1 (India)

**Edge Network**

- OR2 (Oregon, VS)
- VA6 (Virginia, VS)
- IRL1 (Ierland)
- IND1 (India)
- SGP3 (Singapore)
- AUS3 (Australië)
- JPN3 (Japan)

De meer gedetailleerde informatie over de beschikbare serverplaatsen kan in het [&#x200B; multi-wolkenoverzicht &#x200B;](./multi-cloud.md#available-cloud-regions) worden gevonden.

## Volgende stappen

Na het lezen van dit overzicht, begrijpt u nu de verschillen tussen verwerkingsgegevens op de hub van Adobe Experience Platform en Adobe Experience Platform Edge Network.

## Bijlage

In de volgende sectie wordt aanvullende informatie weergegeven over het verwerken van gegevens in Adobe Experience Platform.

### Veelgestelde vragen

In de volgende sectie worden veelgestelde vragen over hub en Edge Network weergegeven:

#### Welke scenario&#39;s het meest aangewezen voor hub zijn?

De hub is best geschikt in scenario&#39;s waar de **gronheid** van de gegevens belangrijker is. Bijvoorbeeld, zeggen u een marketing campagne wilt creëren om alle klanten te richten die winkelwagentjes hebben verlaten. In dat gebruiksgeval, kon u partijsegmentatie gebruiken, die tot een publiek leidt dat de verlaten kartgebruikers aanpast, en het uitvoeren naar een partijbestemming.

#### Welke scenario&#39;s zijn het meest geschikt voor Edge Network?

Edge Network is best geschikt voor scenario&#39;s waar **snelheid** van de gegevens belangrijker is. Stel bijvoorbeeld dat u een beperkte Flash-uitverkoop moet maken voor een klant die op uw site bladert met een product in zijn winkelwagentje. In dat geval kunt u Edge-segmentatie gebruiken, zodat u direct een gepersonaliseerde melding kunt sturen naar gebruikers met een product in hun winkelwagentje met een &quot;flash-verkoop&quot;.

#### Welke gegevens gaan van hub naar Edge Network?

Alleen gegevens die nodig zijn om real-time ervaringen aan de rand te bieden, worden van hub naar Edge Network geladen. Deze gegevens worden automatisch van hub naar Edge Network verzonden om het uiteindelijk verenigbaar te houden, en slechts voor maximaal 14 dagen bewaard. Nochtans, betekent dit **niet** dat het gegeven perfect in synchronisatie met gegevens in hub wordt gehouden. Dientengevolge, kunnen er verschillen in beschikbare gegevens tussen hub en Edge Network zijn.
