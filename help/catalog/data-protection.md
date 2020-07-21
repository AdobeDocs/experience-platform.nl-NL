---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Gegevensbescherming in Adobe Experience Platform
topic: data protection
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# Gegevensbescherming in Adobe Experience Platform

Alle gegevens die door Adobe Experience Platform worden opgenomen en gebruikt, worden opgeslagen in de [!DNL Data Lake], een hoogst korrelige gegevensopslag die alle gegevens bevat die door, ongeacht oorsprong [!DNL Platform]of dossierformaat worden beheerd. Alle gegevens die in het bestand [!DNL Data Lake] blijven staan, worden gecodeerd, opgeslagen en beheerd in een geïsoleerde [!DNL Microsoft Azure Data Lake] opslagaccount die uniek is voor uw organisatie.

In het volgende stroomdiagram wordt getoond hoe gegevens worden opgenomen, verwerkt, gecodeerd en door [!DNL Experience Platform]:

![](images/data-protection/flow.png)

Zie het document over [!DNL Data Lake Storage]gegevenscodering in Azure Data Lake Storage voor meer informatie over hoe gegevens in rust worden gecodeerd [](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption). Zie het document over [!DNL Cosmos DB]gegevenscodering in Azure Cosmos DB [](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)voor informatie over hoe gegevens in rust worden gecodeerd.