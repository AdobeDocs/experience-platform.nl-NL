---
solution: Experience Platform
title: UI-gids voor streamingsegmentatie
description: Dankzij streamingsegmentatie op Adobe Experience Platform kunt u segmentering uitvoeren in bijna real-time terwijl u zich richt op gegevensrijkdom. Met het stromen segmentatie, gebeurt de segmentkwalificatie nu aangezien de gegevens in Platform landen, die de behoefte verlichten om segmentatietaken te plannen en in werking te stellen. Met dit vermogen, kunnen de meeste segmentregels nu worden geëvalueerd aangezien de gegevens in Platform worden overgegaan, betekenend zal het segmentlidmaatschap bijgewerkt zonder geplande segmentatietaken in werking te stellen worden gehouden.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
source-git-commit: 88f2c8723ef16ff5601dc7e45a9f77b25f45acfd
workflow-type: tm+mt
source-wordcount: '1522'
ht-degree: 0%

---

# Streaming segmentering

>[!NOTE]
>
>In het volgende document wordt aangegeven hoe u streamingsegmentatie kunt gebruiken met behulp van de gebruikersinterface. Voor informatie over het gebruik van streamingsegmentatie met behulp van de API leest u de [API-handleiding voor streaming](../api/streaming-segmentation.md).

Segmentering streamen op [!DNL Adobe Experience Platform] staat klanten toe om segmentatie in bijna real time te doen terwijl het concentreren op gegevensrijkdom. Met streaming segmentering gebeurt segmentkwalificatie nu als streaming gegevens binnenkomen [!DNL Platform], om de noodzaak om segmentatietaken te plannen en uit te voeren te verlichten. Met dit vermogen, kunnen de meeste segmentregels nu worden geëvalueerd aangezien het gegeven wordt overgegaan in [!DNL Platform]Dit betekent dat segmentlidmaatschap up-to-date blijft zonder geplande segmentatietaken uit te voeren.

>[!NOTE]
>
>Streaming segmentatie werkt op alle gegevens die via een streaming bron zijn ingeslikt. Gegevens die worden ingevoerd met behulp van een op batch gebaseerde bron worden elke avond geëvalueerd, zelfs als deze in aanmerking komen voor streamingsegmentatie.
>
>Bovendien, kunnen de segmenten die met het stromen segmentatie worden geëvalueerd tussen ideaal en daadwerkelijke lidmaatschap vervagen als de segmentdefinitie van een andere segmentdefinitie wordt gebaseerd die gebruikend partijsegmentatie wordt geëvalueerd. Bijvoorbeeld, als Segment A van Segment B wordt gebaseerd, en Segment B wordt geëvalueerd gebruikend partijsegmentatie, aangezien Segment B slechts om de 24 uur bijwerkt, zal Segment A zich verder van de daadwerkelijke gegevens bewegen tot het met de update van Segment B hersynchroniseert.

## Streaming segmenteringsquerytypen {#query-types}

>[!NOTE]
>
>Opdat het stromen segmentatie aan het werk is, zult u geplande segmentatie voor de organisatie moeten toelaten. Raadpleeg voor meer informatie over het inschakelen van geplande segmentatie [de het stromen segmenteringssectie in de de gebruikersgids van de Segmentatie](./overview.md#scheduled-segmentation).

Een query wordt automatisch geëvalueerd met streaming segmentatie als deze aan een van de volgende criteria voldoet:

| Type query | Details | Voorbeeld |
| ---------- | ------- | ------- |
| Eén gebeurtenis | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis zonder tijdbeperking. | ![Er wordt een voorbeeld van één gebeurtenis weergegeven.](../images/ui/streaming-segmentation/incoming-hit.png) |
| Eén gebeurtenis binnen een relatief tijdvenster | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis. | ![Er wordt een voorbeeld van één gebeurtenis in een relatief tijdvenster weergegeven.](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Eén gebeurtenis met een tijdvenster | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis met een tijdvenster. | ![Er wordt een voorbeeld van één gebeurtenis met een tijdvenster weergegeven.](../images/ui/streaming-segmentation/historic-time-window.png) |
| Alleen profiel | Elke segmentdefinitie die alleen naar een profielkenmerk verwijst. | |
| Eén gebeurtenis met een profielkenmerk binnen een relatief tijdvenster van minder dan 24 uur | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis, met een of meer profielkenmerken, en die optreedt binnen een relatief tijdvenster van minder dan 24 uur. | ![Er wordt een voorbeeld weergegeven van één gebeurtenis met een profielkenmerk binnen een relatief tijdvenster.](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Segment van segmenten | Elke segmentdefinitie die een of meer batch- of streaming segmenten bevat. **Opmerking:** Als een segment van segmenten wordt gebruikt, zal de profielontzetting gebeuren **om de 24 uur**. | ![Een voorbeeld van een segment van segmenten wordt getoond.](../images/ui/streaming-segmentation/two-batches.png) |
| Meerdere gebeurtenissen met een profielkenmerk | Elke segmentdefinitie die verwijst naar meerdere gebeurtenissen **in de laatste 24 uur** en (optioneel) heeft een of meer profielkenmerken. | ![Er wordt een voorbeeld weergegeven van meerdere gebeurtenissen met een profielkenmerk.](../images/ui/streaming-segmentation/event-history-success.png) |

Een segmentdefinitie zal **niet** voor het stromen segmentatie in de volgende scenario&#39;s worden toegelaten:

- De segmentdefinitie omvat Adobe Audience Manager (AAM)-segmenten of -kenmerken.
- De segmentdefinitie omvat meerdere entiteiten (vragen van meerdere entiteiten).
- De segmentdefinitie omvat een combinatie van één gebeurtenis en een `inSegment` gebeurtenis.
   - Als de segmentdefinitie in de `inSegment` gebeurtenis is alleen profiel, de segmentdefinitie **zal** is ingeschakeld voor streamingsegmentatie.

Houd rekening met de volgende richtlijnen bij het uitvoeren van streaming segmentatie:

| Type query | Richtsnoer |
| ---------- | -------- |
| Single-event-query | Er gelden geen limieten voor het terugzoekvenster. |
| Query uitvoeren met gebeurtenisgeschiedenis | <ul><li>Het terugzoekvenster is beperkt tot **één dag**.</li><li>Een strikte voorwaarde voor de tijdvolgorde **moet** tussen de gebeurtenissen bestaan.</li><li>Query&#39;s met ten minste één genegeerde gebeurtenis worden ondersteund. De gehele gebeurtenis **kan** een negatie zijn.</li></ul> |

Als een segmentdefinitie wordt gewijzigd zodat deze niet meer voldoet aan de criteria voor het streamen van segmentatie, schakelt de segmentdefinitie automatisch over van &quot;Streaming&quot; naar &quot;Batch&quot;.

Bovendien, segmentonkwalificatie, zo gelijkaardig aan segmentkwalificatie, gebeurt in real time. Als een publiek niet langer in aanmerking komt voor een segment, is het dus onmiddellijk niet gekwalificeerd. Bijvoorbeeld, als de segmentdefinitie &quot;Alle gebruikers vraagt die rode schoenen in de laatste drie uren&quot;kochten, na drie uren, zullen alle profielen die aanvankelijk voor de segmentdefinitie kwalificeerden ongekwalificeerd zijn.

## Definiedetails van segmentatiesegment streamen

Nadat u een segment hebt gemaakt dat geschikt is voor streaming, kunt u details van dat segment weergeven.

![De pagina met segmentdefinitiedetails wordt weergegeven.](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

In het bijzonder de **[!UICONTROL Total qualified]** De metrische waarde wordt weergegeven. Hiermee wordt het totale aantal gekwalificeerde doelgroepen weergegeven op basis van batch- en streaming-evaluaties voor dit segment.

Onderliggende lijn is een lijngrafiek die het aantal nieuwe doelgroepen toont die in de laatste 24 uur werden bijgewerkt gebruikend de het stromen evaluatiemethode. De vervolgkeuzelijst kan worden aangepast om de laatste 24 uur, vorige week of 30 dagen weer te geven. De **[!UICONTROL New audience updated]** De metrische waarde is gebaseerd op de verandering in publieksgrootte tijdens de geselecteerde tijdwaaier, zoals die door het stromen segmentatie wordt geëvalueerd. Deze metrisch omvat niet het totale gekwalificeerde publiek van de dagelijkse evaluatie van de segmentpartij.

>[!NOTE]
>
>Een segmentdefinitie wordt als gekwalificeerd beschouwd wanneer deze van een status zonder status naar gerealiseerd gaat of wanneer deze van een verlaten naar een gerealiseerde definitie gaat. Een segmentdefinitie wordt als niet-gekwalificeerd beschouwd als deze van gerealiseerde naar verlaten gaat.
>
>Meer informatie over deze statussen vindt u in de statustabel in het dialoogvenster [segmentatieoverzicht](./overview.md#browse).

![De profielen worden gemarkeerd met een lijngrafiek van de profielen in de loop der tijd.](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

De extra informatie over de laatste segmentevaluatie kan worden gevonden door de informatiebel naast te selecteren **[!UICONTROL Total qualified]**.

![De informatiballon voor het Totaal gekwalificeerde profielen is geselecteerd. Dit toont informatie over de laatste tijd van de segmentevaluatie.](../images/ui/streaming-segmentation/info-bubble.png)

Lees voor meer informatie over segmentdefinities het vorige gedeelte over [segmentdefinitiedetails](#segment-details).

## Volgende stappen

In deze gebruikershandleiding wordt uitgelegd hoe definities van streaming-ingeschakelde segmenten werken op Adobe Experience Platform en hoe u voor streaming geschikte segmenten kunt controleren.

Voor meer informatie over het gebruik van de Adobe Experience Platform-gebruikersinterface leest u de [Gebruikershandleiding voor segmentatie](./overview.md).

## Bijlage

In de volgende sectie worden veelgestelde vragen over streamingsegmentatie weergegeven:

### Vindt streaming segmentatie ook &#39;onkwalificatie&#39; plaats in real-time?

Doorgaans gebeurt een onkwalificatie van streamingsegmentatie in real-time. Bij streaming segmenten die segmenten van segmenten gebruiken, gebeurt dit echter wel **niet** in real time niet in aanmerking komen, in plaats daarvan na 24 uur niet in aanmerking.

### Aan welke gegevens werkt streaming segmentatie?

Streaming segmentatie werkt op alle gegevens die via een streaming bron zijn ingeslikt. Segmenten die worden ingevoerd met behulp van een op batch gebaseerde bron, worden elke avond geëvalueerd, zelfs als deze in aanmerking komt voor streaming segmentatie. Gebeurtenissen die naar het systeem worden gestreamd met een tijdstempel die ouder is dan 24 uur, worden verwerkt in de volgende batchtaak.

### Hoe worden segmenten gedefinieerd als batch- of streaming-segmentatie?

Een segmentdefinitie wordt gedefinieerd als batch, streaming of randsegmentatie op basis van een combinatie van het type query en de duur van de gebeurtenisgeschiedenis. Een lijst van welke segmenten als het stromen segmentdefinitie zal worden geëvalueerd kan in worden gevonden [sectie met querytypen voor streamingsegmentering](#query-types).

Houd er rekening mee dat als een segmentdefinitie een segment bevat **beide** een `inSegment` en een directe &#39;single-event&#39;-keten, kan deze niet in aanmerking komen voor streamingsegmentatie. Als u deze segmentdefinitie voor het stromen segmentatie wilt kwalificeren, zou u de directe enige-gebeurtenisketen zijn eigen segment moeten maken.

### Waarom blijft het aantal &quot;totaal gekwalificeerde&quot;segmenten stijgen terwijl het aantal onder &quot;Laatste X dagen&quot;nul binnen de sectie van de segmentdefinitiedetails blijft?

Het aantal in totaal gekwalificeerde segmenten wordt ontleend aan de dagelijkse segmentatietaak, die publiek omvat dat voor zowel partij als het stromen segmenten kwalificeert. Deze waarde wordt weergegeven voor zowel batch- als streaming segmenten.

Het getal onder de &quot;Laatste X dagen&quot; **alleen** omvat doelgroepen die zijn gekwalificeerd in streamingsegmentatie, en **alleen** neemt toe als u gegevens in het systeem hebt gestreamd en het telt naar die het stromen definitie. Deze waarde is **alleen** weergegeven voor streaming segmenten. Dientengevolge, deze waarde **kan** weergeven als 0 voor batchsegmenten.

Als u dus ziet dat het getal onder &quot;Laatste X dagen&quot; nul is en dat de lijngrafiek ook nul rapporteert, hebt u **niet** profielen naar het systeem gestreamd die voor dat segment in aanmerking zouden komen.

### Hoe lang duurt het voordat een segmentdefinitie beschikbaar is?

Het duurt tot één uur voordat een segmentdefinitie beschikbaar is.

### Zijn er beperkingen aan de gegevens waarin wordt gestreamd?

Voor het gebruik van gestreamde gegevens in streamingsegmentatie is er **moet** moet ruimte zijn tussen de gebeurtenissen die worden gestreamd. Als er te veel gebeurtenissen binnen dezelfde seconde worden gestreamd, behandelt Platform deze gebeurtenissen als door beide gegenereerde gegevens en worden ze genegeerd. Als beste praktijken, zou u moeten hebben **ten minste** vijf seconden tussen gebeurtenisgegevens om ervoor te zorgen dat de gegevens correct worden gebruikt.
