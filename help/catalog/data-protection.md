---
keywords: Experience Platform;home;popular topics;catalog;data protection;encryption data lake
solution: Experience Platform
title: Gegevensbescherming in Adobe Experience Platform
topic: data protection
description: Alle gegevens die in het meer van Gegevens worden voortgeduurd worden gecodeerd, opgeslagen, en beheerd in een geïsoleerde rekening van de Opslag van de Gegevens van Microsoft Azure die voor uw organisatie uniek is. Het volgende stroomdiagram van het proces illustreert hoe het gegeven wordt opgenomen, verwerkt, gecodeerd en door Experience Platform voortgeduurd.
translation-type: tm+mt
source-git-commit: 14f99c23cd82894fee5eb5c4093b3c50b95c52e8
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# Gegevensbescherming in Adobe Experience Platform

Alle gegevens die door Adobe Experience Platform worden ingepakt en gebruikt, worden opgeslagen in de [!DNL Data Lake], zeer granulaire gegevensopslag die alle gegevens bevat die door worden beheerd, ongeacht de oorsprong [!DNL Platform]of bestandsindeling. Alle gegevens die in het bestand [!DNL Data Lake] blijven staan, worden gecodeerd, opgeslagen en beheerd in een geïsoleerde [!DNL Microsoft Azure Data Lake] opslagaccount die uniek is voor uw organisatie.

In het volgende stroomdiagram wordt getoond hoe gegevens worden opgenomen, verwerkt, gecodeerd en door [!DNL Experience Platform]:

![](images/data-protection/flow.png)

Zie het document over [!DNL Data Lake Storage]gegevenscodering in Azure Data Lake Storage voor meer informatie over hoe gegevens in rust worden gecodeerd [](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption). Zie het document over [!DNL Cosmos DB]gegevenscodering in Azure Cosmos DB [](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)voor informatie over hoe gegevens in rust worden gecodeerd.