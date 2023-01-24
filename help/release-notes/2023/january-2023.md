---
title: Opmerkingen bij de release van Adobe Experience Platform Januari 2023
description: In de releaseopmerkingen van januari 2023 voor Adobe Experience Platform.
source-git-commit: 01c220147312108649e036d93288823df5389235
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 1%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 25 januari 2023**

Updates voor bestaande functies in Adobe Experience Platform:

- [Bronnen](#sources)

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren en maakt het mogelijk die gegevens te structureren, te labelen en te verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

| Functie | Beschrijving |
| --- | --- |
| Toegang van gebruikers tot submappen van bronnen voor cloudopslag toestaan | U kunt nu toegang definiëren tot een specifieke submap van de bron voor cloudopslag wanneer u een nieuw account maakt. Zodra gecreeerd, zullen de gebruikers tot gegevens van toegelaten subfolder kunnen slechts toegang hebben. Deze functie is beschikbaar voor de volgende bronnen voor cloudopslag: [Azure Blob Storage](../../sources/connectors/cloud-storage/blob.md), [Google Cloud Storage](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md), en [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Beta beschikbaarheid van [!DNL SugarCRM] | [!DNL SugarCRM] bronnen zijn nu beschikbaar in bèta . Gebruik de [!DNL SugarCRM Accounts & Contacts] en de [!DNL SugarCRM Events] bronnen om gegevens van uw [!DNL SugarCRM] aan Experience Platform. Lees voor meer informatie de [[!DNL SugarCRM] overzicht](../../sources/connectors/crm/sugarcrm.md). |