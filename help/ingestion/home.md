---
keywords: Experience Platform;home;populaire onderwerpen;gegevensinvoer;gegevenslocatie;Gegevenslocatie;Gegevensbeheer;gegevensbeheer;Lineaire;line;batch;Geëxtraheerde gegevens
solution: Experience Platform
title: Overzicht van gegevensinname
topic: ' - overzicht'
description: Dit document introduceert de drie belangrijkste manieren waarop gegevens in Platform worden opgenomen, met koppelingen naar hun respectieve overzichtsdocumentatie voor meer gedetailleerde informatie.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# Overzicht van gegevensinname

Adobe Experience Platform brengt gegevens uit meerdere bronnen samen om marketers te helpen het gedrag van hun klanten beter te begrijpen. De Ingestie van Gegevens van Adobe Experience Platform vertegenwoordigt de veelvoudige methodes waardoor [!DNL Platform] gegevens uit deze bronnen inneemt, evenals hoe die gegevens binnen het meer van Gegevens voor gebruik door stroomafwaartse [!DNL Platform] diensten worden voortgeduurd.

In dit document worden de drie belangrijkste manieren geïntroduceerd waarop gegevens worden opgenomen in [!DNL Platform], met koppelingen naar hun respectieve overzichtsdocumentatie voor meer gedetailleerde informatie.

## Inname in batch

Door de batch in te voeren kunt u gegevens als batchbestanden in [!DNL Experience Platform] invoeren. Batches zijn gegevenseenheden die bestaan uit een of meer bestanden die als één eenheid moeten worden ingevoerd. Als de batches eenmaal zijn opgenomen, bieden ze metagegevens die het aantal records beschrijven dat is opgenomen, evenals eventuele mislukte records en bijbehorende foutberichten.

Met deze methode moeten handmatig geüploade gegevensbestanden, zoals platte CSV-bestanden (toegewezen aan XDM-schema&#39;s) en Parquet-dataframes, worden opgenomen.

Zie [batchverwerking overzicht](./batch-ingestion/overview.md) voor meer informatie.

## Streaming opname

Met streaming opname kunt u gegevens van client- en server-side apparaten in real-time naar [!DNL Experience Platform] verzenden. [!DNL Platform] steunt het gebruik van gegevensinlaten om inkomende ervaringsgegevens te stromen, die in streaming-toegelaten datasets binnen het meer van Gegevens wordt voortgeduurd. De inlaten van gegevens kunnen worden gevormd om de gegevens automatisch voor authentiek te verklaren die zij verzamelen, ervoor zorgen dat de gegevens uit een vertrouwde op bron komen.

Zie [streamingopname overview](./streaming-ingestion/overview.md) voor meer informatie.

## Bronnen

[!DNL Experience Platform] kunt u bronverbindingen instellen met verschillende gegevensleveranciers. Deze verbindingen laten u toe om aan uw externe gegevensbronnen voor authentiek te verklaren, tijden voor inname looppas te plaatsen, en innamevervoer te beheren.

Bronverbindingen kunnen worden geconfigureerd om gegevens te verzamelen van andere Adobe-toepassingen (zoals Adobe Analytics en Adobe Audience Manager), bronnen voor cloudopslag van derden (zoals [!DNL Azure Blob], [!DNL Amazon] S3, FTP-servers en SFTP-servers) en CRM-systemen van derden (zoals [!DNL Microsoft Dynamics] en [!DNL Salesforce]).

Zie [Bronoverzicht](../sources/home.md) voor meer informatie.

## Volgende stappen en extra bronnen

In dit document wordt een korte inleiding gegeven op de verschillende aspecten van [!DNL Data Ingestion] in [!DNL Experience Platform]. Lees verder de overzichtsdocumentatie voor elke innamemethode om vertrouwd te raken met hun verschillende mogelijkheden, gebruiksgevallen en beste praktijken. U kunt het leren ook aanvullen door de onderstaande video met het ingesloten overzicht te bekijken. Voor informatie over hoe [!DNL Experience Platform] de meta-gegevens voor ingebedde verslagen volgt, zie [Overzicht van de Dienst van de Catalogus](../catalog/home.md).

>[!WARNING]
>
>De term &quot;Verenigd Profiel&quot;die in de volgende video wordt gebruikt is verouderd. De termen [!DNL "Profile"] of [!DNL "Real-time Customer Profile"] zijn de juiste termen die worden gebruikt in de documentatie [!DNL Experience Platform]. Raadpleeg de documentatie voor de meest recente functionaliteit.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)