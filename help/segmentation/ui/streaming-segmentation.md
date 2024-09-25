---
solution: Experience Platform
title: UI-gids voor streamingsegmentatie
description: Dankzij streamingsegmentatie op Adobe Experience Platform kunt u segmentering uitvoeren in bijna real-time terwijl u zich richt op gegevensrijkdom. Met het stromen segmentatie, gebeurt de segmentkwalificatie nu aangezien de gegevens in Platform landen, die de behoefte verlichten om segmentatietaken te plannen en in werking te stellen. Met dit vermogen, kunnen de meeste segmentregels nu worden geëvalueerd aangezien de gegevens in Platform worden overgegaan, betekenend zal het segmentlidmaatschap bijgewerkt zonder geplande segmentatietaken in werking te stellen worden gehouden.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
source-git-commit: a1c9003a1b219325daf8fa38cda8bb1a019a55c6
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 0%

---

# Streaming segmentering

>[!NOTE]
>
>In het volgende document wordt aangegeven hoe u streamingsegmentatie kunt gebruiken met behulp van de gebruikersinterface. Voor informatie bij het gebruiken van het stromen segmentatie die API gebruiken, te lezen gelieve de [ het stromen segmentatie API gids ](../api/streaming-segmentation.md).

Door segmentatie te streamen op [!DNL Adobe Experience Platform] kunnen klanten segmentering uitvoeren in de buurt van realtime en tegelijk de nadruk leggen op gegevensrijkdom. Met streamingsegmentatie gebeurt segmentkwalificatie nu als streaminggegevens in [!DNL Platform] terechtkomen, waardoor de noodzaak om segmentatietaken te plannen en uit te voeren, wordt verminderd. Met dit vermogen, kunnen de meeste segmentregels nu worden geëvalueerd aangezien de gegevens in [!DNL Platform] worden overgegaan, betekenend zal het segmentlidmaatschap bijgewerkt zonder geplande segmentatietaken in werking te stellen worden gehouden.

>[!NOTE]
>
>Streaming segmentatie werkt op alle gegevens die via een streaming bron zijn ingeslikt. Gegevens die worden ingevoerd met behulp van een op batch gebaseerde bron worden elke avond geëvalueerd, zelfs als deze in aanmerking komen voor streamingsegmentatie.
>
>Bovendien, kunnen de segmenten die met het stromen segmentatie worden geëvalueerd tussen ideaal en daadwerkelijke lidmaatschap vervagen als de segmentdefinitie van een andere segmentdefinitie wordt gebaseerd die gebruikend partijsegmentatie wordt geëvalueerd. Bijvoorbeeld, als Segment A van Segment B wordt gebaseerd, en Segment B wordt geëvalueerd gebruikend partijsegmentatie, aangezien Segment B slechts om de 24 uur bijwerkt, zal Segment A zich verder van de daadwerkelijke gegevens bewegen tot het met de update van Segment B hersynchroniseert.

## Streaming segmenteringsquerytypen {#query-types}

>[!NOTE]
>
>Opdat het stromen segmentatie aan het werk is, zult u geplande segmentatie voor de organisatie moeten toelaten. Voor details bij het toelaten van geplande segmentatie, gelieve te verwijzen naar [ het Poortoverzicht van het Poort van het Publiek ](./audience-portal.md#scheduled-segmentation).

Een query wordt automatisch geëvalueerd met streaming segmentatie als deze aan een van de volgende criteria voldoet:

| Type query | Details |
| ---------- | ------- |
| Eén gebeurtenis binnen een tijdsvenster van minder dan 24 uur | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis binnen een tijdvenster van minder dan 24 uur. |
| Alleen profiel | Elke segmentdefinitie die alleen naar een profielkenmerk verwijst. |
| Eén gebeurtenis met een profielkenmerk binnen een relatief tijdvenster van minder dan 24 uur | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis, met een of meer profielkenmerken, en die optreedt binnen een relatief tijdvenster van minder dan 24 uur. |
| Segment van segmenten | Elke segmentdefinitie die een of meer batch- of streaming segmenten bevat. **Nota:** als een segment van segmenten wordt gebruikt, zal de profielontzetting **elke 24 uren** gebeuren. |
| Meerdere gebeurtenissen met een profielkenmerk | Om het even welke segmentdefinitie die naar veelvoudige gebeurtenissen **binnen de laatste 24 uren** verwijst en (naar keuze) heeft één of meerdere profielattributen. |

Een segmentdefinitie zal **** niet voor het stromen segmentatie in de volgende scenario&#39;s worden toegelaten:

- De segmentdefinitie omvat Adobe Audience Manager (AAM)-segmenten of -kenmerken.
- De segmentdefinitie omvat meerdere entiteiten (vragen van meerdere entiteiten).
- De segmentdefinitie bevat een combinatie van één gebeurtenis en een `inSegment` -gebeurtenis.
   - Nochtans, als de segmentdefinitie in de `inSegment` gebeurtenis profiel slechts is, zal de segmentdefinitie **** voor het stromen segmentatie worden toegelaten.
- In de segmentdefinitie wordt &quot;Jaar negeren&quot; gebruikt als onderdeel van de tijdbeperkingen.

Houd rekening met de volgende richtlijnen bij het uitvoeren van streaming segmentatie:

| Type query | Richtsnoer |
| ---------- | -------- |
| Single-event-query | Er gelden geen limieten voor het terugzoekvenster. |
| Query uitvoeren met gebeurtenisgeschiedenis | <ul><li>Het raadplegingsvenster is beperkt tot **één dag**.</li><li>Een strikte tijd-opdracht gevend voorwaarde **moet** tussen de gebeurtenissen bestaan.</li><li>Query&#39;s met ten minste één genegeerde gebeurtenis worden ondersteund. Nochtans, kan de volledige gebeurtenis **niet** een negatie zijn.</li></ul> |

Als een segmentdefinitie wordt gewijzigd zodat deze niet meer voldoet aan de criteria voor het streamen van segmentatie, schakelt de segmentdefinitie automatisch over van &quot;Streaming&quot; naar &quot;Batch&quot;.

Bovendien, segmentonkwalificatie, zo gelijkaardig aan segmentkwalificatie, gebeurt in real time. Als een publiek niet langer in aanmerking komt voor een segment, is het dus onmiddellijk niet gekwalificeerd. Bijvoorbeeld, als de segmentdefinitie &quot;Alle gebruikers vraagt die rode schoenen in de laatste drie uren&quot;kochten, na drie uren, zullen alle profielen die aanvankelijk voor de segmentdefinitie kwalificeerden ongekwalificeerd zijn.

## Definiedetails van segmentatiesegment streamen

Nadat u een segment hebt gemaakt dat geschikt is voor streaming, kunt u details van dat segment weergeven.

![ de pagina van de de details van de segmentdefinitie wordt getoond.](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

Specifiek, wordt metrisch **[!UICONTROL Total qualified]** getoond, die het totale aantal gekwalificeerde publiek toont, dat op partij en het stromen evaluaties voor dit segment wordt gebaseerd.

Onderliggende lijn is een lijngrafiek die het aantal nieuwe doelgroepen toont die in de laatste 24 uur werden bijgewerkt gebruikend de het stromen evaluatiemethode. De vervolgkeuzelijst kan worden aangepast om de laatste 24 uur, vorige week of 30 dagen weer te geven. **[!UICONTROL New audience updated]** metrisch is gebaseerd op de verandering in publieksgrootte tijdens de geselecteerde tijdwaaier, zoals die door het stromen segmentatie wordt geëvalueerd. Deze metrisch omvat niet het totale gekwalificeerde publiek van de dagelijkse evaluatie van de segmentpartij.

>[!NOTE]
>
>Een segmentdefinitie wordt als gekwalificeerd beschouwd wanneer deze van een status zonder status naar gerealiseerd gaat of wanneer deze van een verlaten naar een gerealiseerde definitie gaat. Een segmentdefinitie wordt als niet-gekwalificeerd beschouwd als deze van gerealiseerde naar verlaten gaat.
>
>Meer informatie over deze statussen kan in de statuslijst binnen het [ Poortoverzicht van het Poortpubliek van het publiek ](./audience-portal.md#customize) worden gevonden.

![ De Profielen over tijdkaart wordt benadrukt, die een lijngrafiek van de profielen in tijd tonen.](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Aanvullende informatie over de laatste segmentevaluatie kunt u vinden door de informatiballon naast **[!UICONTROL Total qualified]** te selecteren.

![ de informatiebel voor het Totaal gekwalificeerde profielen wordt geselecteerd. Dit toont informatie over de laatste tijd van de segmentevaluatie.](../images/ui/streaming-segmentation/info-bubble.png)

Voor meer informatie over segmentdefinities, te lezen gelieve de vorige sectie over [ details van de segmentdefinitie ](#segment-details).

## Volgende stappen

In deze gebruikershandleiding wordt uitgelegd hoe definities van streaming-ingeschakelde segmenten werken op Adobe Experience Platform en hoe u voor streaming geschikte segmenten kunt controleren.

Om meer over het gebruiken van het gebruikersinterface van Adobe Experience Platform te leren, te lezen gelieve de [ gebruikersgids van de Segmentatie ](./overview.md).

## Bijlage

In de volgende sectie worden veelgestelde vragen over streamingsegmentatie weergegeven:

### Vindt streaming segmentatie ook &#39;onkwalificatie&#39; plaats in real-time?

Doorgaans gebeurt een onkwalificatie van streamingsegmentatie in real-time. Nochtans, die segmenten stromen die segmenten van segmenten gebruiken **niet** in real time niet kwalificeren, in plaats daarvan het niet kwalificeren na 24 uren.

### Aan welke gegevens werkt streaming segmentatie?

Streaming segmentatie werkt op alle gegevens die via een streaming bron zijn ingeslikt. Segmenten die worden ingevoerd met behulp van een op batch gebaseerde bron, worden elke avond geëvalueerd, zelfs als deze in aanmerking komt voor streaming segmentatie. Gebeurtenissen die naar het systeem worden gestreamd met een tijdstempel die ouder is dan 24 uur, worden verwerkt in de volgende batchtaak.

### Hoe worden segmenten gedefinieerd als batch- of streaming-segmentatie?

Een segmentdefinitie wordt gedefinieerd als batch, streaming of randsegmentatie op basis van een combinatie van het type query en de duur van de gebeurtenisgeschiedenis. Een lijst waarvan de segmenten als het stromen segmentdefinitie zullen worden geëvalueerd kan in de [ het stromen sectie van de segmenteringsvraagtypes ](#query-types) worden gevonden.

Gelieve te merken op dat als een segmentdefinitie **zowel** een `inSegment` uitdrukking als een directe enige-gebeurtenisketting bevat, het niet voor het stromen segmentatie kan kwalificeren. Als u deze segmentdefinitie voor het stromen segmentatie wilt kwalificeren, zou u de directe enige-gebeurtenisketen zijn eigen segment moeten maken.

### Waarom blijft het aantal &quot;totaal gekwalificeerde&quot;segmenten stijgen terwijl het aantal onder &quot;Laatste X dagen&quot;nul binnen de sectie van de segmentdefinitiedetails blijft?

Het aantal in totaal gekwalificeerde segmenten wordt ontleend aan de dagelijkse segmentatietaak, die publiek omvat dat voor zowel partij als het stromen segmenten kwalificeert. Deze waarde wordt weergegeven voor zowel batch- als streaming segmenten.

Het aantal onder de &quot;Laatste dagen van X&quot;**slechts** omvat publiek dat in het stromen segmentatie wordt gekwalificeerd, en **slechts** verhogingen als u gegevens in het systeem hebt gestroomd en het telt naar die het stromen definitie. Deze waarde is **slechts** getoond voor het stromen segmenten. Dientengevolge, kan deze waarde **** als 0 voor partijsegmenten tonen.

Dientengevolge, als u ziet dat het aantal onder &quot;Laatste dagen van X&quot;nul is, en de lijngrafiek ook nul meldt, hebt u **** gestroomd geen profielen in het systeem dat voor dat segment zou kwalificeren.

### Hoe lang duurt het voordat een segmentdefinitie beschikbaar is?

Het duurt tot één uur voordat een segmentdefinitie beschikbaar is.

### Zijn er beperkingen aan de gegevens waarin wordt gestreamd?

Opdat de gestroomde gegevens in het stromen segmentatie worden gebruikt, moet **** het uit elkaar plaatsen tussen de gebeurtenissen zijn die binnen worden gestroomd. Als er te veel gebeurtenissen binnen dezelfde seconde worden gestreamd, behandelt Platform deze gebeurtenissen als door beide gegenereerde gegevens en worden ze genegeerd. Als beste praktijken, zou u **minstens** vijf seconden tussen gebeurtenisgegevens moeten hebben om ervoor te zorgen dat het gegeven behoorlijk wordt gebruikt.
