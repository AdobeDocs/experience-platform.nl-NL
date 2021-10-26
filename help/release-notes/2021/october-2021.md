---
title: Opmerkingen bij de release van Adobe Experience Platform
description: De meest recente releaseopmerkingen voor Adobe Experience Platform.
source-git-commit: 0c507a26f551af1eb17889e8e77a036e3c106240
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 1%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 27 oktober 2021**

Updates voor bestaande functies in Adobe Experience Platform:

- [Bronnen](#sources)

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

| Functie | Beschrijving |
| --- | --- |
| [!DNL Amazon S3] bronverbeteringen | U kunt nu de opdracht `s3SessionToken` parameter om uw [!DNL Amazon S3] account aan Platform met tijdelijke beveiligingsgegevens. Met dit token kunt u op korte termijn tijdelijke toegang tot uw [!DNL Amazon S3] bronnen voor gebruikers in niet-vertrouwde omgevingen. Zie de [[!DNL Amazon S3] documentatie](../../sources/connectors/cloud-storage/s3.md#prerequisites) voor meer informatie . |
| [!DNL Generic REST API] (bèta) | U kunt nu een [!DNL Generic REST API] bronverbinding met de [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) of de [gebruikersinterface](../../sources/tutorials/ui/create/protocols/generic-rest.md) gegevens van een generieke REST-toepassing naar het Platform te brengen. Zie de [[!DNL Generic REST API] overzicht](../../sources/connectors/protocols/generic-rest.md) voor meer informatie . |
| [!DNL Zoho CRM] (bèta) | U kunt nu een [!DNL Zoho CRM] bronverbinding met de [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) of de [gebruikersinterface](../../sources/tutorials/ui/create/crm/zoho.md) om gegevens van uw [!DNL Zoho CRM] aan Platform. Zie de [[!DNL Zoho CRM] overzicht](../../sources/connectors/crm/zoho.md) voor meer informatie . |

Zie voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).
