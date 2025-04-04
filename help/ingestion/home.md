---
keywords: Experience Platform;home;populaire onderwerpen;gegevensinvoer;gegevenslocatie;Gegevenslocatie;Gegevensbeheer;gegevensbeheer;Lineaire;line;batch;Geëxtraheerde gegevens
solution: Experience Platform
title: Overzicht van gegevensinscriptie
description: In dit document worden de drie belangrijkste manieren geïntroduceerd waarop gegevens in Experience Platform worden ingevoerd. In koppelingen naar de desbetreffende overzichtsdocumentatie vindt u meer gedetailleerde informatie.
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---

# Overzicht van gegevensinname

Adobe Experience Platform brengt gegevens uit meerdere bronnen samen om marketers te helpen het gedrag van hun klanten beter te begrijpen. De Ingestie van Gegevens van Adobe Experience Platform vertegenwoordigt de veelvoudige methodes waardoor Experience Platform gegevens uit deze bronnen opneemt, evenals hoe die gegevens binnen het meer van Gegevens voor gebruik door de stroomafwaartse diensten van Experience Platform worden voortgeduurd.

In dit document worden de drie belangrijkste manieren geïntroduceerd waarop gegevens in Experience Platform worden ingevoerd. In koppelingen naar de desbetreffende overzichtsdocumentatie vindt u meer gedetailleerde informatie.

## Inname in batch

Met batch-opname kunt u gegevens in [!DNL Experience Platform] invoeren als batchbestanden. Batches zijn gegevenseenheden die bestaan uit een of meer bestanden die als één eenheid moeten worden ingevoerd. Als de batches eenmaal zijn opgenomen, bieden ze metagegevens die het aantal records beschrijven dat is opgenomen, evenals eventuele mislukte records en bijbehorende foutberichten.

Met deze methode moeten handmatig geüploade gegevensbestanden, zoals platte CSV-bestanden (toegewezen aan XDM-schema&#39;s) en Parquet-dataframes, worden opgenomen.

Zie het [ overzicht van partijingestie ](./batch-ingestion/overview.md) voor meer informatie.

>[!TIP]
>
>Gebruik Single-line JSON in plaats van multi-line JSON als invoer voor batch-opname. Single-line JSON biedt betere prestaties omdat het systeem één invoerbestand in meerdere delen kan verdelen en parallel kan verwerken, terwijl JSON met meerdere regels niet kan worden gesplitst. Dit kan de kosten voor gegevensverwerking aanzienlijk verlagen en de latentie voor batchverwerking aanzienlijk verbeteren.

## Streaming opname

Met streaming opname kunt u gegevens van client- en server-side apparaten in real-time naar [!DNL Experience Platform] verzenden. Experience Platform steunt het gebruik van gegevensinlaten om inkomende ervaringsgegevens te stromen, die in streaming-toegelaten datasets binnen het meer van Gegevens wordt voortgeduurd. De inlaten van gegevens kunnen worden gevormd om de gegevens automatisch voor authentiek te verklaren die zij verzamelen, ervoor zorgen dat de gegevens uit een vertrouwde op bron komen.

Zie [ het stromen ingegaan overzicht ](./streaming-ingestion/overview.md) voor meer informatie.

## Bronnen

Met [!DNL Experience Platform] kunt u bronverbindingen instellen met verschillende gegevensproviders. Deze verbindingen laten u toe om aan uw externe gegevensbronnen voor authentiek te verklaren, tijden voor inname looppas te plaatsen, en innamevervoer te beheren.

Source-verbindingen kunnen worden geconfigureerd om gegevens te verzamelen van andere Adobe-toepassingen (zoals Adobe Analytics en Adobe Audience Manager), bronnen voor cloudopslag van derden (zoals [!DNL Azure Blob] , [!DNL Amazon] S3, FTP-servers en SFTP-servers) en CRM-systemen van derden (zoals [!DNL Microsoft Dynamics] en [!DNL Salesforce] ).

Zie het [ Overzicht van Bronnen ](../sources/home.md) voor meer informatie.

### Met ML ondersteund schema maken {#ml-assisted-schema-creation}

Om nieuwe gegevensbronnen snel te integreren, kunt u machine het leren algoritmen nu gebruiken om een schema van steekproefgegevens te produceren. Deze automatisering vereenvoudigt het creëren van nauwkeurige schema&#39;s, vermindert fouten, en versnelt het proces van gegevensinzameling aan analyse en inzichten.

Zie de [ ML-Geassisteerde gids van de schemaverwezenlijking ](../xdm/ui/ml-assisted-schema-creation.md) voor meer informatie over dit werkschema.

## Volgende stappen en extra bronnen

In dit document vindt u een korte inleiding over de verschillende aspecten van [!DNL Data Ingestion] in [!DNL Experience Platform] . Lees verder de overzichtsdocumentatie voor elke innamemethode om vertrouwd te raken met hun verschillende mogelijkheden, gebruiksgevallen en beste praktijken. U kunt het leren ook aanvullen door de onderstaande video met het ingesloten overzicht te bekijken. Voor informatie over hoe [!DNL Experience Platform] de meta-gegevens voor opgenomen verslagen volgt, zie het [ overzicht van de Dienst van de Catalogus ](../catalog/home.md).

>[!WARNING]
>
>De term &quot;Verenigd Profiel&quot;die in de volgende video wordt gebruikt is verouderd. De termen [!DNL "Profile"] of [!DNL "Real-Time Customer Profile"] zijn de juiste termen die worden gebruikt in de documentatie van [!DNL Experience Platform] . Raadpleeg de documentatie voor de meest recente functionaliteit.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
