---
keywords: Experience Platform;thuis;populaire onderwerpen;het stromen segmentatie;Segmentatie;de Dienst van de segmentatie;de segmenteringsdienst;ui gids;
solution: Experience Platform
title: UI-gids voor streamingsegmentatie
topic-legacy: ui guide
description: Dankzij streamingsegmentatie op Adobe Experience Platform kunt u segmentering uitvoeren in bijna real-time terwijl u zich richt op gegevensrijkdom. Met het stromen segmentatie, gebeurt de segmentkwalificatie nu aangezien de gegevens in Platform landen, die de behoefte verlichten om segmentatietaken te plannen en in werking te stellen. Met dit vermogen, kunnen de meeste segmentregels nu worden geëvalueerd aangezien de gegevens in Platform worden overgegaan, betekenend zal het segmentlidmaatschap bijgewerkt zonder geplande segmentatietaken in werking te stellen worden gehouden.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
source-git-commit: 1fa7663cc8bebca98f284593e98163315acda478
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 0%

---

# Streaming segmentering

>[!NOTE]
>
>In het volgende document wordt aangegeven hoe u streamingsegmentatie kunt gebruiken met behulp van de gebruikersinterface. Voor informatie over het gebruik van streamingsegmentatie met behulp van de API leest u de [API-handleiding voor streaming](../api/streaming-segmentation.md).

Segmentering streamen op [!DNL Adobe Experience Platform] staat klanten toe om segmentatie in bijna real time te doen terwijl het concentreren op gegevensrijkdom. Met streaming segmentering gebeurt segmentkwalificatie nu als streaming gegevens binnenkomen [!DNL Platform], om de noodzaak om segmentatietaken te plannen en uit te voeren te verlichten. Met dit vermogen, kunnen de meeste segmentregels nu worden geëvalueerd aangezien het gegeven wordt overgegaan in [!DNL Platform]Dit betekent dat segmentlidmaatschap up-to-date blijft zonder geplande segmentatietaken uit te voeren.

>[!NOTE]
>
>
>Segmenten die met streaming segmentatie worden geëvalueerd, kunnen tussen ideaal en feitelijk lidmaatschap verschuiven als het segment is gebaseerd op een ander segment dat met batchsegmentatie wordt geëvalueerd. Bijvoorbeeld, als Segment A van Segment B wordt gebaseerd, en Segment B wordt geëvalueerd gebruikend partijsegmentatie, aangezien Segment B slechts om de 24 uur bijwerkt, zal Segment A zich verder van de daadwerkelijke gegevens bewegen tot het met de update van Segment B hersynchroniseert.

## Streaming segmenteringsquerytypen {#query-types}

>[!NOTE]
>
>Opdat het stromen segmentatie aan het werk is, zult u geplande segmentatie voor de organisatie moeten toelaten. Voor meer informatie over het inschakelen van geplande segmentatie raadpleegt u [de het stromen segmenteringssectie in de de gebruikersgids van de Segmentatie](./overview.md#scheduled-segmentation).

Een query wordt automatisch geëvalueerd met streaming segmentatie als deze aan een van de volgende criteria voldoet:

| Type query | Details | Voorbeeld |
| ---------- | ------- | ------- |
| Eén gebeurtenis | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis zonder tijdbeperking. | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| Eén gebeurtenis binnen een relatief tijdvenster | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis. | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Eén gebeurtenis met een tijdvenster | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis met een tijdvenster. | ![](../images/ui/streaming-segmentation/historic-time-window.png) |
| Alleen profiel | Elke segmentdefinitie die alleen naar een profielkenmerk verwijst. |  |
| Eén gebeurtenis met een profielkenmerk | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis, zonder tijdbeperking, en een of meer profielkenmerken. **Opmerking:** De query wordt onmiddellijk geëvalueerd wanneer de gebeurtenis plaatsvindt. In het geval van een profielgebeurtenis moet de opname echter 24 uur wachten. | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| Eén gebeurtenis met een profielkenmerk binnen een relatief tijdvenster | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis en een of meer profielkenmerken. | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Segment van segmenten | Elke segmentdefinitie die een of meer batch- of streaming segmenten bevat. **Opmerking:** Als een segment van segmenten wordt gebruikt, zal de profielontzetting gebeuren **om de 24 uur**. | ![](../images/ui/streaming-segmentation/two-batches.png) |
| Meerdere gebeurtenissen met een profielkenmerk | Elke segmentdefinitie die verwijst naar meerdere gebeurtenissen **in de laatste 24 uur** en (optioneel) heeft een of meer profielkenmerken. | ![](../images/ui/streaming-segmentation/event-history-success.png) |

Een segmentdefinitie zal **niet** voor het stromen segmentatie in de volgende scenario&#39;s worden toegelaten:

- De segmentdefinitie omvat Adobe Audience Manager (AAM)-segmenten of -kenmerken.
- De segmentdefinitie omvat meerdere entiteiten (vragen van meerdere entiteiten).

Houd rekening met de volgende richtlijnen bij het uitvoeren van streaming segmentatie:

| Type query | Richtsnoer |
| ---------- | -------- |
| Query voor één gebeurtenis | Er gelden geen limieten voor het terugzoekvenster. |
| Query uitvoeren met gebeurtenisgeschiedenis | <ul><li>Het terugzoekvenster is beperkt tot **één dag**.</li><li>Een strikte voorwaarde voor de tijdvolgorde **moet** tussen de gebeurtenissen bestaan.</li><li>Query&#39;s met ten minste één genegeerde gebeurtenis worden ondersteund. De gehele gebeurtenis **kan** een negatie zijn.</li></ul> |

Als een segmentdefinitie wordt gewijzigd zodat deze niet meer voldoet aan de criteria voor het streamen van segmentatie, schakelt de segmentdefinitie automatisch over van &quot;Streaming&quot; naar &quot;Batch&quot;.

Bovendien, segmentonkwalificatie, zo gelijkaardig aan segmentkwalificatie, gebeurt in real time. Als een publiek niet langer in aanmerking komt voor een segment, is het dus onmiddellijk niet gekwalificeerd. Bijvoorbeeld, als de segmentdefinitie &quot;Alle gebruikers vraagt die rode schoenen in de laatste drie uren&quot;kochten, na drie uren, zullen alle profielen die aanvankelijk voor de segmentdefinitie kwalificeerden ongekwalificeerd zijn.

## Segmentdetails streaming

Nadat u een voor streaming geschikt segment hebt gemaakt, kunt u details van dat segment weergeven.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

Meer bepaald, details over de **[!UICONTROL total qualified audience size]** worden weergegeven. De **[!UICONTROL Total qualified audience size]** toont het totale aantal gekwalificeerde publiek van de laatste voltooide looppas van de segmentbaan. Als een segmentbaan niet binnen de laatste 24 uren werd voltooid, zal het aantal publiek van een raming in plaats daarvan worden genomen.

Onderaan ziet u een lijngrafiek met het aantal segmenten dat in de afgelopen 24 uur is gekwalificeerd en gediskwalificeerd. De vervolgkeuzelijst kan worden aangepast om de laatste 24 uur, vorige week of 30 dagen weer te geven.

>[!NOTE]
>
>Een segment wordt als gekwalificeerd beschouwd als het van het hebben van geen status naar gerealiseerde gaat of als het van verlaten naar gerealiseerde gaat. Een segment wordt als ongekwalificeerd beschouwd als het van gerealiseerde naar verlaten gaat of van bestaand naar verlaten.
>
>Meer informatie over deze statussen vindt u in de statustabel in het dialoogvenster [segmentatieoverzicht](./overview.md#browse).

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

De extra informatie over de laatste segmentevaluatie kan worden gevonden door de informatiebel te selecteren.

![](../images/ui/streaming-segmentation/info-bubble.png)

Lees voor meer informatie over segmentdefinities het vorige gedeelte over [segmentdefinitiedetails](#segment-details).

## Volgende stappen

In deze gebruikershandleiding wordt uitgelegd hoe definities van streaming-ingeschakelde segmenten werken op Adobe Experience Platform en hoe u voor streaming geschikte segmenten kunt controleren.

Voor meer informatie over het gebruik van de Adobe Experience Platform-gebruikersinterface leest u de [Gebruikershandleiding voor segmentatie](./overview.md).

## Aanhangsel

In de volgende sectie worden veelgestelde vragen over streamingsegmentatie weergegeven:

### Vindt streaming segmentatie ook &#39;onkwalificatie&#39; plaats in real-time?

Doorgaans gebeurt een onkwalificatie van streamingsegmentatie in real-time. Bij streaming segmenten die segmenten van segmenten gebruiken, gebeurt dit echter wel **niet** in real time niet in aanmerking komen, in plaats daarvan na 24 uur niet in aanmerking.

### Aan welke gegevens werkt streaming segmentatie?

Streaming segmentatie werkt op alle gegevens die via een streaming bron zijn ingeslikt. Segmenten die worden ingevoerd met behulp van een op batch gebaseerde bron, worden elke avond geëvalueerd, zelfs als deze in aanmerking komt voor streaming segmentatie.

### Hoe worden segmenten gedefinieerd als batch- of streaming-segmentatie?

Een segment wordt gedefinieerd als batch- of streaming segmentatie op basis van een combinatie van het type query en de duur van de gebeurtenisgeschiedenis. Een lijst met segmenten die als streaming segment worden geëvalueerd, kunt u vinden in het dialoogvenster [sectie met querytypen voor streamingsegmentering](#query-types).

### Kan een gebruiker een segment definiëren als batch- of streaming-segmentatie?

Op dit ogenblik, kan de gebruiker niet bepalen of een segment gebruikend partij of het stromen opname wordt geëvalueerd, aangezien het systeem automatisch zal bepalen met welke methode het segment zal worden geëvalueerd.

### Waarom neemt het aantal &quot;totaal gekwalificeerde&quot; segmenten toe terwijl het aantal onder &quot;Laatste X dagen&quot; nul blijft binnen de sectie met segmentdetails?

Het aantal in totaal gekwalificeerde segmenten wordt ontleend aan de dagelijkse segmentatietaak, die publiek omvat dat voor zowel partij als het stromen segmenten kwalificeert. Deze waarde wordt weergegeven voor zowel batch- als streaming segmenten.

Het getal onder de &quot;Laatste X dagen&quot; **alleen** omvat publiek dat in het stromen segmentatie gekwalificeerd is, en **alleen** neemt toe als u gegevens in het systeem hebt gestreamd en het telt naar die het stromen definitie. Deze waarde is **alleen** weergegeven voor streaming segmenten. Dientengevolge, deze waarde **kan** weergeven als 0 voor batchsegmenten.

Als u dus ziet dat het getal onder &quot;Laatste X dagen&quot; nul is en dat de lijngrafiek ook nul rapporteert, hebt u **niet** profielen naar het systeem gestreamd die voor dat segment in aanmerking zouden komen.