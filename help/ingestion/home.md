---
keywords: Experience Platform;home;populaire onderwerpen;gegevensinvoer;gegevenslocatie;Gegevenslocatie;Gegevensbeheer;gegevensbeheer;Lineaire;line;batch;Geëxtraheerde gegevens
solution: Experience Platform
title: Overzicht van gegevensinname
description: Dit document introduceert de drie belangrijkste manieren waarop gegevens in Platform worden opgenomen, met koppelingen naar hun respectieve overzichtsdocumentatie voor meer gedetailleerde informatie.
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# Overzicht van gegevensinname

Adobe Experience Platform brengt gegevens uit meerdere bronnen samen om marketers te helpen het gedrag van hun klanten beter te begrijpen. Adobe Experience Platform Data Ingestie vertegenwoordigt de veelvoudige methodes waardoor [!DNL Platform] neemt gegevens uit deze bronnen op en hoe die gegevens binnen het Data Lake voor gebruik door stroomafwaarts worden geduurd [!DNL Platform] diensten.

In dit document worden de drie belangrijkste manieren geïntroduceerd waarop gegevens worden opgenomen [!DNL Platform], met links naar hun respectieve overzichtsdocumentatie voor meer gedetailleerde informatie.

## Inname in batch

Door inname in batch kunt u gegevens in [!DNL Experience Platform] als batchbestanden. Batches zijn gegevenseenheden die bestaan uit een of meer bestanden die als één eenheid moeten worden ingevoerd. Als de batches eenmaal zijn opgenomen, bieden ze metagegevens die het aantal records beschrijven dat is opgenomen, evenals eventuele mislukte records en bijbehorende foutberichten.

Met deze methode moeten handmatig geüploade gegevensbestanden, zoals platte CSV-bestanden (toegewezen aan XDM-schema&#39;s) en Parquet-dataframes, worden opgenomen.

Zie de [overzicht van batch-opname](./batch-ingestion/overview.md) voor meer informatie .

## Streaming opname

Met streaming invoer kunt u gegevens van client- en serverapparaten naar [!DNL Experience Platform] in real time. [!DNL Platform] steunt het gebruik van gegevensinlaten om inkomende ervaringsgegevens te stromen, die in streaming-toegelaten datasets binnen het meer van Gegevens wordt voortgeduurd. De inlaten van gegevens kunnen worden gevormd om de gegevens automatisch voor authentiek te verklaren die zij verzamelen, ervoor zorgen dat de gegevens uit een vertrouwde op bron komen.

Zie de [overzicht van streaming opname](./streaming-ingestion/overview.md) voor meer informatie .

## Bronnen

[!DNL Experience Platform] kunt u bronverbindingen instellen met verschillende gegevensleveranciers. Deze verbindingen laten u toe om aan uw externe gegevensbronnen voor authentiek te verklaren, tijden voor inname looppas te plaatsen, en innamevervoer te beheren.

Bronverbindingen kunnen worden geconfigureerd om gegevens te verzamelen van andere Adobe-toepassingen (zoals Adobe Analytics en Adobe Audience Manager), bronnen voor cloudopslag van derden (zoals [!DNL Azure Blob], [!DNL Amazon] S3, FTP-servers en SFTP-servers) en CRM-systemen van derden (zoals [!DNL Microsoft Dynamics] en [!DNL Salesforce]).

Zie de [Overzicht van bronnen](../sources/home.md) voor meer informatie .

## Volgende stappen en extra bronnen

Dit document bevatte een korte inleiding over de verschillende aspecten van [!DNL Data Ingestion] in [!DNL Experience Platform]. Lees verder de overzichtsdocumentatie voor elke innamemethode om vertrouwd te raken met hun verschillende mogelijkheden, gebruiksgevallen en beste praktijken. U kunt het leren ook aanvullen door de onderstaande video met het ingesloten overzicht te bekijken. Voor informatie over hoe [!DNL Experience Platform] traceert de meta-gegevens voor opgenomen verslagen, zie [Overzicht van Catalog Service](../catalog/home.md).

>[!WARNING]
>
>De term &quot;Verenigd Profiel&quot;die in de volgende video wordt gebruikt is verouderd. De voorwaarden [!DNL "Profile"] of [!DNL "Real-Time Customer Profile"] worden de juiste termen gebruikt in de [!DNL Experience Platform] documentatie. Raadpleeg de documentatie voor de meest recente functionaliteit.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
