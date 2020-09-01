---
keywords: Experience Platform;home;popular topics;streaming segmentation;Segmentation;Segmentation Service;segmentation service;ui guide;
solution: Experience Platform
title: Streaming segmentering
topic: ui guide
description: Dankzij streamingsegmentatie op Adobe Experience Platform kunt u segmentering uitvoeren in bijna real-time terwijl u zich richt op gegevensrijkdom. Met het stromen segmentatie, gebeurt de segmentkwalificatie nu aangezien de gegevens in Platform landen, die de behoefte verlichten om segmentatietaken te plannen en in werking te stellen. Met dit vermogen, kunnen de meeste segmentregels nu worden geëvalueerd aangezien de gegevens in Platform worden overgegaan, betekenend zal het segmentlidmaatschap bijgewerkt zonder geplande segmentatietaken in werking te stellen worden gehouden.
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---


# Streaming segmentering

>[!NOTE]
>
>In het volgende document wordt aangegeven hoe u streamingsegmentatie kunt gebruiken met behulp van de gebruikersinterface. Voor informatie over het gebruik van streamingsegmentatie met behulp van de API leest u de API-handleiding voor [streamingsegmentatie](../api/streaming-segmentation.md).

Streaming segmentering op [!DNL Adobe Experience Platform] staat klanten toe om segmentatie in bijna real time te doen terwijl het concentreren op gegevensrijkdom. Met het stromen segmentatie, gebeurt de segmentkwalificatie nu aangezien het stromen gegevens in [!DNL Platform]landt, die de behoefte verlichten om segmentatietaken te plannen en in werking te stellen. Met dit vermogen, kunnen de meeste segmentregels nu worden geëvalueerd aangezien de gegevens worden overgegaan in [!DNL Platform], betekenend zal het segmentlidmaatschap bijgewerkt zonder geplande segmentatietaken in werking te stellen worden gehouden.

>[!NOTE]
>
>Streaming segmentatie kan alleen worden gebruikt om gegevens te evalueren die in het Platform worden gestreamd. Met andere woorden, gegevens die via batch-opname worden ingevoerd, worden niet geëvalueerd door streamingsegmentatie en vereisen dat batchevaluatie wordt geactiveerd.

## Streaming segmenteringsquerytypen

>[!NOTE]
>
>Opdat het stromen segmentatie aan het werk is, zult u geplande segmentatie voor de organisatie moeten toelaten. Voor details bij het toelaten van geplande segmentatie, gelieve te verwijzen naar [de het stromen segmenteringssectie in de de gebruikersgids](./overview.md#scheduled-segmentation)van de Segmentatie.

Een query wordt automatisch geëvalueerd met streaming segmentatie als deze aan een van de volgende criteria voldoet:

| Type query | Details | Voorbeeld |
| ---------- | ------- | ------- |
| Binnenkomende hit | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis zonder tijdbeperking. | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| Binnenkomende hit binnen relatief tijdvenster | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis **in de laatste zeven dagen**. | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Alleen profiel | Elke segmentdefinitie die alleen naar een profielkenmerk verwijst. |  |
| Binnenkomende hit die verwijst naar een profiel | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis, zonder tijdbeperking, en een of meer profielkenmerken. | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| Binnenkomende hit die verwijst naar een profiel binnen een relatief tijdvenster | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis en een of meer profielkenmerken, **binnen de afgelopen zeven dagen**. | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Meerdere gebeurtenissen die naar een profiel verwijzen | Elke segmentdefinitie die verwijst naar meerdere gebeurtenissen **in de afgelopen 24 uur** en (optioneel), heeft een of meer profielkenmerken. | ![](../images/ui/streaming-segmentation/event-history-success.png) |

In de volgende sectie worden voorbeelden van segmentdefinities weergegeven die **niet** zijn ingeschakeld voor streamingsegmentatie.

| Type query | Details | Voorbeeld |
| ---------- | ------- | ------- |
| Binnenkomende hit binnen relatief tijdvenster | Als de segmentdefinitie naar een inkomende gebeurtenis verwijst die **niet** binnen de **laatste zeven-dagperiode** valt. Bijvoorbeeld binnen de **laatste twee weken**. | ![](../images/ui/streaming-segmentation/relative-hit-failure.png) |
| Binnenkomende hit die verwijst naar een profiel binnen een relatief venster | De volgende opties bieden **geen** ondersteuning voor streamingsegmentatie:<ul><li>Een binnenkomende gebeurtenis **die zich niet** binnen de **laatste periode** van zeven dagen bevindt.</li><li>Een segmentdefinitie die [!DNL Adobe Audience Manager (AAM)] segmenten of kenmerken bevat.</li></ul> | ![](../images/ui/streaming-segmentation/profile-relative-failure.png) |
| Meerdere gebeurtenissen die naar een profiel verwijzen | De volgende opties bieden **geen** ondersteuning voor streamingsegmentatie:<ul><li>Een gebeurtenis die **niet** optreedt binnen **de laatste 24 uur**.</li><li>Een segmentdefinitie die Adobe Audience Manager (AAM)-segmenten of -kenmerken bevat.</li></ul> | ![](../images/ui/streaming-segmentation/event-history-failure.png) |
| Vragen over meerdere entiteiten | Vraagstukken met meerdere entiteiten worden over het geheel genomen **niet** ondersteund door streamingsegmentatie. |  |

Daarnaast zijn enkele richtlijnen van toepassing wanneer streamingsegmentatie wordt uitgevoerd:

| Type query | Richtsnoer |
| ---------- | -------- |
| Query voor één gebeurtenis | Het terugkijkvenster is beperkt tot **zeven dagen**. |
| Query uitvoeren met gebeurtenisgeschiedenis | <ul><li>Het terugkijkvenster is beperkt tot **één dag**.</li><li>Tussen de gebeurtenissen **moet** een strikte voorwaarde voor de tijdvolgorde bestaan.</li><li>Slechts worden de eenvoudige tijdorden (vóór en na) tussen de gebeurtenissen toegestaan.</li><li>De afzonderlijke gebeurtenissen **kunnen niet** worden genegeerd. De gehele query **kan** echter worden genegeerd.</li></ul> |

## Segmentdetails streaming

Nadat u een voor streaming geschikt segment hebt gemaakt, kunt u details van dat segment weergeven.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

Specifiek, worden de details over de **[!UICONTROL totale gekwalificeerde publieksgrootte]** getoond. De **[!UICONTROL Totale gekwalificeerde publieksgrootte]** toont het totale aantal gekwalificeerde publiek van de laatste voltooide looppas van de segmentbaan. Als een segmentbaan niet binnen de laatste 24 uren werd voltooid, zal het aantal publiek van een raming in plaats daarvan worden genomen.

Onderaan ziet u een lijngrafiek met het aantal segmenten dat in de afgelopen 24 uur is gekwalificeerd en gediskwalificeerd. De vervolgkeuzelijst kan worden aangepast om de laatste 24 uur, vorige week of 30 dagen weer te geven.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

De extra informatie over de laatste segmentevaluatie kan worden gevonden door de informatiebel te selecteren.

![](../images/ui/streaming-segmentation/info-bubble.png)

Voor meer informatie over segmentdefinities, gelieve de vorige sectie over de details [van de](#segment-details)segmentdefinitie te lezen.

## Videodemo voor streamingsegmentatie

De volgende video is bedoeld om uw begrip van het stromen segmentatie te steunen. Het toont een voorbeeldervaring van de klant gevolgd door een snelle rondreis van zeer belangrijke eigenschappen in de [!DNL Platform] interface.

>[!VIDEO](https://video.tv.adobe.com/v/36184?quality=12&learn=on)

## Volgende stappen

In deze gebruikershandleiding wordt uitgelegd hoe definities van streaming-ingeschakelde segmenten werken op Adobe Experience Platform en hoe u voor streaming geschikte segmenten kunt controleren.

Lees voor meer informatie over het gebruik van de Adobe Experience Platform-gebruikersinterface de gebruikershandleiding voor [segmentatie](./overview.md).