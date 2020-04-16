---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Overzicht van gegevensverwerking in Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 2f0f155beacbc6a4ba2892ae211a9c0305e969ac

---


# Overzicht van gegevensinname

Met het Adobe Experience Platform worden gegevens uit meerdere bronnen bijeengebracht om marketers te helpen het gedrag van hun klanten beter te begrijpen. De Ingestie van de Gegevens van het Platform van de Ervaring van Adobe vertegenwoordigt de veelvoudige methodes waardoor Platform gegevens uit deze bronnen opneemt, evenals hoe die gegevens binnen het meer van Gegevens voor gebruik door de stroomafwaartse diensten van het Platform worden voortgeduurd.

In dit document worden de drie belangrijkste manieren geïntroduceerd waarop gegevens worden opgenomen in Platform. De koppelingen naar de bijbehorende overzichtsdocumentatie bevatten meer gedetailleerde informatie.

## Inname in batch

Door de batch in te voeren kunt u gegevens als batchbestanden in het Experience Platform opnemen. Batches zijn gegevenseenheden die bestaan uit een of meer bestanden die als één eenheid moeten worden ingevoerd. Als de batches eenmaal zijn opgenomen, bieden ze metagegevens die het aantal records beschrijven dat is opgenomen, evenals eventuele mislukte records en bijbehorende foutberichten.

Met deze methode moeten handmatig geüploade gegevensbestanden, zoals platte CSV-bestanden (toegewezen aan XDM-schema&#39;s) en Parquet-dataframes, worden opgenomen.

Zie het [batchoverzicht](./batch-ingestion/overview.md) voor meer informatie.

## Streaming opname

Met streaming opname kunt u gegevens van client- en server-side apparaten naar het Platform verzenden in real-time. Het platform steunt het gebruik van gegevensinlaten om inkomende ervaringsgegevens te stromen, die in streaming-toegelaten datasets binnen het meer van Gegevens wordt voortgeduurd. De inlaten van gegevens kunnen worden gevormd om de gegevens automatisch voor authentiek te verklaren die zij verzamelen, ervoor zorgen dat de gegevens uit een vertrouwde op bron komen.

Zie het [streamingoverzicht](./streaming-ingestion/overview.md) voor meer informatie.

## Bronnen

Met het Experience Platform kunt u bronverbindingen instellen met verschillende gegevensproviders. Deze verbindingen laten u toe om aan uw externe gegevensbronnen voor authentiek te verklaren, tijden voor inname looppas te plaatsen, en innamevervoer te beheren.

Bronverbindingen kunnen worden geconfigureerd om gegevens te verzamelen van andere Adobe-toepassingen (zoals Adobe Analytics en Adobe Audience Manager), bronnen voor cloudopslag van derden (zoals Azure Blob, Amazon S3, FTP-servers en SFTP-servers) en CRM-systemen van derden (zoals Microsoft Dynamics en Salesforce).

Zie het [Bronoverzicht](../sources/home.md) voor meer informatie.

## Volgende stappen

Dit document bevatte een korte inleiding op de verschillende aspecten van gegevensinname in het ervaringsplatform. Lees verder de overzichtsdocumentatie voor elke innamemethode om vertrouwd te raken met hun verschillende mogelijkheden, gebruiksgevallen en beste praktijken. Voor informatie over hoe het Platform van de Ervaring de meta-gegevens voor ingebedde verslagen volgt, zie het overzicht [van de Dienst van de](../catalog/home.md)Catalogus.