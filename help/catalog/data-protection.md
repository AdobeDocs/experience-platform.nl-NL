---
keywords: Experience Platform;thuis;populaire onderwerpen;catalogus;gegevensbescherming;encryptiegegevens meer
solution: Experience Platform
title: Gegevensbeveiliging in Adobe Experience Platform
topic: data protection
description: Alle gegevens die in het meer van Gegevens worden voortgeduurd worden gecodeerd, opgeslagen, en beheerd in een geïsoleerde rekening van de Opslag van de Gegevens van Microsoft Azure die voor uw organisatie uniek is. Het volgende stroomdiagram van het proces illustreert hoe het gegeven wordt opgenomen, verwerkt, gecodeerd en door Experience Platform voortgeduurd.
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---


# Gegevensbescherming in Adobe Experience Platform

Alle gegevens die door Adobe Experience Platform worden ingevoerd en gebruikt, worden opgeslagen in [!DNL Data Lake], een zeer granulaire gegevensopslag die alle gegevens bevat die door [!DNL Platform] worden beheerd, ongeacht de oorsprong of bestandsindeling. Alle gegevens die in [!DNL Data Lake] worden voortgeduurd, worden gecodeerd, opgeslagen en beheerd in een geïsoleerde [!DNL Microsoft Azure Data Lake] opslagaccount die uniek is voor uw organisatie.

In het volgende stroomdiagram wordt getoond hoe gegevens worden opgenomen, verwerkt, gecodeerd en geduurd door [!DNL Experience Platform]:

![](images/data-protection/flow.png)

Zie het document over [gegevenscodering in Azure Data Lake Storage](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption) voor meer informatie over hoe gegevens in rust worden gecodeerd in [!DNL Data Lake Storage]. Zie het document over [gegevenscodering in Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest) voor informatie over hoe gegevens in rust worden gecodeerd in [!DNL Cosmos DB].