---
keywords: Experience Platform;home;populaire onderwerpen;controle;monitor;gegevensstromen;controle opname;gegevensopname;gegevensopname;gegevensopname;meningsverslagen;meningspartijen;
solution: Experience Platform
title: Gegevensinname controleren
description: Deze gebruikershandleiding bevat een aantal stappen voor het controleren van uw gegevens in de gebruikersinterface van Adobe Experience Platform. Voor deze handleiding hebt u een Adobe ID nodig en hebt u toegang tot Adobe Experience Platform.
exl-id: 85711a06-2756-46f9-83ba-1568310c9f73
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 0%

---

# Inname van gegevens controleren

Met gegevensinvoer kunt u uw gegevens opnemen in Adobe Experience Platform. U kunt batch-opname gebruiken, waardoor u gegevens kunt invoegen met verschillende bestandstypen (zoals CSV&#39;s), of streaming opname, waardoor u uw gegevens in [!DNL Experience Platform] kunt invoeren met streaming eindpunten in real-time.

Deze gebruikershandleiding bevat stappen voor het controleren van gegevens in de gebruikersinterface van Adobe Experience Platform. Voor deze handleiding hebt u een Adobe ID nodig en hebt u toegang tot Adobe Experience Platform.

## Doorlopende gegevensinvoer controleren {#monitor-streaming-end-to-end-data-ingestion}

>[!CONTEXTUALHELP]
>id="platform_ingestion_streaming_ingestionrate"
>title="Inktsnelheid"
>abstract="Het aantal gebeurtenissen dat per seconde correct wordt verwerkt."
>text="Learn more in the documentation"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dataflows/ui/monitor-sources.html?lang=nl-NL" text="Dataflows controleren voor bronnen in de gebruikersinterface"

>[!TIP]
>
>Als u het totaal van de gebeurtenissen op een bepaalde datum wilt berekenen, gebruikt u de expressie: `total events / day = ingestion rate * 60 * 60 * 24` .

In [ Experience Platform UI ](https://platform.adobe.com), uitgezochte **[!UICONTROL Monitoring]** op het linkernavigatiemenu, die door **[!UICONTROL Streaming end-to-end]** wordt gevolgd.

De controlepagina van **[!UICONTROL Streaming end-to-end]** wordt weergegeven. Deze werkruimte biedt een grafiek die de snelheid weergeeft van gestreamde gebeurtenissen die worden ontvangen door [!DNL Experience Platform] , een grafiek die de snelheid weergeeft van gestreamde gebeurtenissen die zijn verwerkt door [[!DNL Real-Time Customer Profile]](../../profile/home.md) , en een gedetailleerde lijst met binnenkomende gegevens.

![](../images/quality/monitor-data-flows/list-streams.png)

Standaard toont de bovenste grafiek de mate van inname in de afgelopen zeven dagen. U kunt dit datumbereik aanpassen om verschillende tijdsperioden weer te geven door de gemarkeerde knop te selecteren.

![](../images/quality/monitor-data-flows/events-received.png)

In de onderste grafiek wordt de snelheid van de gestreamde gebeurtenissen van [!DNL Profile] in de afgelopen zeven dagen weergegeven. U kunt dit datumbereik aanpassen om verschillende tijdsperioden weer te geven door de gemarkeerde knop te selecteren.

>[!NOTE]
>
>Opdat de gegevens op deze grafiek verschijnen, moeten de gegevens **uitdrukkelijk** worden toegelaten voor [!DNL Profile]. Leren hoe te om het stromen gegevens voor [!DNL Profile] toe te laten, lees de [ gids van de datasetgebruiker ](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile).

![](../images/quality/monitor-data-flows/ingested-by-profile.png)

Onder de grafieken bevindt zich een lijst met alle streaming opname-records die overeenkomen met het hierboven weergegeven datumbereik. Elke vermelde partij toont zijn identiteitskaart, datasetnaam, toen het het laatst werd bijgewerkt, het aantal verslagen in de partij, evenals het aantal fouten (als om het even welk bestaan). U kunt om het even welke verslagen voor meer gedetailleerde informatie over dat verslag selecteren.

![](../images/quality/monitor-data-flows/streams.png)

### Streaming records weergeven

Wanneer u de details van een gestreamde record weergeeft, wordt informatie weergegeven zoals het aantal records dat wordt opgenomen, de bestandsgrootte en de begin- en eindtijd van de opname.

![](../images/quality/monitor-data-flows/successful-streaming.png)

De details van een mislukte streamingrecord geven dezelfde informatie weer als een geslaagde record.

![](../images/quality/monitor-data-flows/failed-batch.png)

Bovendien bevatten mislukte records details over de fouten die zijn opgetreden tijdens het verwerken van de batch. In het onderstaande voorbeeld is een parseringsfout opgetreden bij het converteren of valideren van de gegevens.

>[!NOTE]
>
>Als er fouten in opgenomen rijen zijn, zullen deze rijen **niet** worden gelaten vallen tenzij het resulterende bericht in ongeldige XDM resulteert.

![](../images/quality/monitor-data-flows/failed-batch-error.png)

## Gegevens van begin tot einde bijhouden in batch

Selecteer **[!UICONTROL Monitoring]** in het navigatiemenu links van [[!DNL Experience Platform UI] ](https://platform.adobe.com) .

De controlepagina van **[!UICONTROL Batch end-to-end]** verschijnt, die een lijst van de eerder opgenomen partijen toont. U kunt elke gewenste batch selecteren voor meer gedetailleerde informatie over die record.

![](../images/quality/monitor-data-flows/batch-monitoring.png)

### Batches weergeven

Wanneer u de details van een geslaagde batch bekijkt, wordt informatie weergegeven zoals het aantal records dat wordt opgenomen, de bestandsgrootte en de begin- en eindtijd van de opname.

![](../images/quality/monitor-data-flows/successful-batch.png)

De details van een mislukte partij tonen de zelfde informatie zoals een succesvolle partij, met de toevoeging van het aantal ontbroken verslagen.

![](../images/quality/monitor-data-flows/failed-batch.png)

Bovendien bevatten mislukte batches details over de fouten die zijn opgetreden tijdens de verwerking van de batch. In het onderstaande voorbeeld is er een fout opgetreden met de ingevoerde batch omdat deze het maximumaantal identiteiten voor de persoon heeft.

>[!NOTE]
>
>Als er fouten in opgenomen rijen zijn, zullen deze rijen **niet** worden gelaten vallen tenzij het resulterende bericht in ongeldige XDM resulteert.

![](../images/quality/monitor-data-flows/failed-streaming-error.png)
