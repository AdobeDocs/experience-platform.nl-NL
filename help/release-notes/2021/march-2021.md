---
title: Opmerkingen bij de release van Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform voor 31 maart 2021.
doc-type: release notes
last-update: March 31, 2021
author: ens72741
translation-type: tm+mt
source-git-commit: 8d4270d9168a570fcf92ba60d70dbc8e9af98136
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---


# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 31 maart 2021**

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Sources]](#sources)

## [!DNL Sources] {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

De volgende updates van bronnen zijn opgenomen in de release van Experience Platform van maart 2021:

| Functie | Beschrijving |
| ------- | ----------- |
| Bètabronnen die naar GA gaan | De volgende bronnen zijn gepromoveerd van bèta naar GA: <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| API-ondersteuning voor gecomprimeerde bestandsopname | U kunt nu gecomprimeerde JSON- of gescheiden bestanden voorvertonen en opnemen met bronnen voor cloudopslag. Zie de zelfstudie over [gegevens voor cloudopslag verzamelen met API&#39;s](../../sources/tutorials/api/collect/cloud-storage.md) voor meer informatie. |
| UI-ondersteuning voor het uploaden van recursieve bestanden | U kunt nu volledige mappen recursief invoeren wanneer u een bron voor cloudopslag gebruikt. Wanneer u een volledige map opgeeft, moet u ervoor zorgen dat de inhoud ervan hetzelfde schema deelt. Voor meer informatie, zie de zelfstudie over [het vormen van een gegevensstroom voor de schakelaars van de wolkenopslag in UI](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Meer over bronnen leren, zie [bronnen overzicht](../../sources/home.md).
