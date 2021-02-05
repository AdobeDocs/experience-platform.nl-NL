---
keywords: Experience Platform;thuis;populaire onderwerpen;controle;monitor;gegevensstromen;monitoringestie;gegevensopname;gegevensopname;meningsverslagen;meningspartijen;
solution: Experience Platform
title: Gegevensinname controleren
topic: overview
description: Deze gebruikershandleiding bevat een aantal stappen voor het controleren van uw gegevens in de gebruikersinterface van Adobe Experience Platform. Voor deze handleiding hebt u een Adobe ID nodig en hebt u toegang tot Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---


# Inname van gegevens controleren

Met gegevensinvoer kunt u uw gegevens opnemen in Adobe Experience Platform. U kunt batch-opname gebruiken, waarmee u gegevens kunt invoegen met verschillende bestandstypen (zoals CSV&#39;s), of streaming opname, waardoor u uw gegevens kunt opnemen in [!DNL Platform] met streaming eindpunten in real-time.

Deze gebruikershandleiding bevat een aantal stappen voor het controleren van uw gegevens in de gebruikersinterface van Adobe Experience Platform. Voor deze handleiding hebt u een Adobe ID nodig en hebt u toegang tot Adobe Experience Platform.

## Doorlopende gegevensinvoer controleren

In [Experience Platform UI](https://platform.adobe.com), klik **[!UICONTROL Controle]** op het linkernavigatiemenu, dan klik **[!UICONTROL het stromen van begin tot eind]**.

![](../images/quality/monitor-data-flows/click-streaming-end-to-end.png)

De **[!UICONTROL Streaming end-to-end]** controlepagina verschijnt. Deze werkruimte biedt een grafiek die de snelheid weergeeft van gestreamde gebeurtenissen die worden ontvangen door [!DNL Platform], een grafiek die de snelheid weergeeft van gestreamde gebeurtenissen die zijn verwerkt door [[!DNL Real-time Customer Profile]](../../profile/home.md), en een gedetailleerde lijst met binnenkomende gegevens.

![](../images/quality/monitor-data-flows/list-streams.png)

Standaard toont de bovenste grafiek de mate van inname in de afgelopen zeven dagen. U kunt dit datumbereik aanpassen om verschillende tijdsperioden weer te geven door op de gemarkeerde knop te klikken.

![](../images/quality/monitor-data-flows/list-streams-focus-on-top-graph.png)

In de onderste grafiek wordt de snelheid van gestreamde gebeurtenissen van [!DNL Profile] in de afgelopen zeven dagen weergegeven. U kunt dit datumbereik aanpassen om verschillende tijdsperioden weer te geven door op de gemarkeerde knop te klikken.

>[!NOTE]
>
>Gegevens worden alleen in deze grafiek weergegeven als **expliciet** is ingeschakeld voor [!DNL Profile]. Lees de [gebruikershandleiding voor datasets](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile) voor meer informatie over het inschakelen van streaminggegevens voor [!DNL Profile].

![](../images/quality/monitor-data-flows/list-streams-focus-on-bottom-graph.png)

Onder de grafieken bevindt zich een lijst met alle streaming opname-records die overeenkomen met het hierboven weergegeven datumbereik. Elke vermelde partij toont zijn identiteitskaart, datasetnaam, toen het het laatst werd bijgewerkt, het aantal verslagen in de partij, evenals het aantal fouten (als om het even welk bestaan). U kunt op een van de records klikken voor meer informatie over die record.

![](../images/quality/monitor-data-flows/list-streams-focus-on-streams.png)

### Streaming records weergeven

Wanneer u de details van een gestreamde record weergeeft, wordt informatie weergegeven zoals het aantal records dat wordt opgenomen, de bestandsgrootte en de begin- en eindtijd van de opname.

![](../images/quality/monitor-data-flows/successful-streaming-record.png)

De details van een mislukte streamingrecord geven dezelfde informatie weer als een geslaagde record.

![](../images/quality/monitor-data-flows/failed-batch.png)

Bovendien bevatten mislukte records details over de fouten die zijn opgetreden tijdens het verwerken van de batch. In het onderstaande voorbeeld is er een systeemfout opgetreden tijdens het valideren van de datasetId uit de catalogus.

![](../images/quality/monitor-data-flows/failed-batch-details.png)

## Gegevens van begin tot einde bijhouden in batch

In [[!DNL Experience Platform UI]](https://platform.adobe.com), klik **[!UICONTROL Controle]** op het linkernavigatiemenu.

![](../images/quality/monitor-data-flows/click-monitoring.png)

De **[!UICONTROL Batch van begin tot eind]** controlepagina verschijnt, die een lijst van de eerder opgenomen partijen toont. U kunt op een van de batches klikken voor meer informatie over de record.

![](../images/quality/monitor-data-flows/list-batches.png)

### Batches weergeven

Wanneer u de details van een geslaagde batch bekijkt, wordt informatie weergegeven zoals het aantal records dat wordt opgenomen, de bestandsgrootte en de begin- en eindtijd van de opname.

![](../images/quality/monitor-data-flows/successful-batch.png)

De details van een mislukte partij tonen de zelfde informatie zoals een succesvolle partij, met de toevoeging van het aantal ontbroken verslagen.

![](../images/quality/monitor-data-flows/failed-streaming-record.png)

Bovendien bevatten mislukte batches details over de fouten die zijn opgetreden tijdens de verwerking van de batch. In het onderstaande voorbeeld is er een fout opgetreden met de opgenomen batch omdat deze een onbekend veld van `_experience` heeft gebruikt.

![](../images/quality/monitor-data-flows/failed-streaming-record-details.png)