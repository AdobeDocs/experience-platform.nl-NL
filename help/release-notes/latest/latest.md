---
title: Opmerkingen bij de release van Adobe Experience Platform
description: De meest recente releaseopmerkingen voor Adobe Experience Platform.
source-git-commit: 0209d7ef1c82915bc11f07518194e3dd68c63de9
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 2%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 27 oktober 2021**

## Updates to Experience Platform

Updates voor Experience Platform.

### Gebruikersinterface {#ui}

The user interface has been updated with the following changes:

| Functie | Beschrijving |
| --- | --- |
| Donker thema | Met de themakeuze Donker schakelt u tussen lichte en donkere thema&#39;s in de interface van het Platform. The switch is located in the user profile below user name and email. |
| Linkernavigatie in-/uitschakelen | Met de verbeterde navigatieknop boven aan de toepassingskop kunt u het menu met de mogelijkheden van uw Experience Platform weergeven of verbergen. Het systeem onthoudt uw laatste selectie en geeft alleen de mogelijkheden weer waartoe u toegang hebt. |
| Toegangszichtbaarheid | Op de linkernavigatiebalk ziet u alleen de functies waartoe u toegang hebt. In previous versions of Adobe Experience Platform, unavailable items were visible, even if you were not able to access them. |

Zie de [UI-gids voor Platform](../../landing/ui-guide.md) voor meer informatie.

## Updates to existing features

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [Bronnen](#sources)

### [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om, gegevens aan en van het Model van Gegevens van de Ervaring in kaart te brengen om te zetten en te bevestigen (XDM).

**Updated features**

| Functie | Beschrijving |
| --- | --- |
| `contains_key` -functie | De `contains_key` functie is geïntroduceerd, waarmee u kunt controleren of het object in de bron bestaat. Deze functie vervangt de `is_set` functie, die nu is afgekeurd. |
| Foutberichten | Foutberichten die door de `/mappingSets/preview` eindpunt in de Prep API van Gegevens zijn nu verenigbaar met de foutenmeldingen die tijdens runtime worden geproduceerd. |

Zie de [[!DNL Data Prep] overzicht](../../data-prep/home.md) voor meer informatie over deze service.

### Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform provides a RESTful API and an interactive UI that lets you set up source connections for various data providers with ease. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

| Functie | Beschrijving |
| --- | --- |
| [!DNL Amazon S3] bronverbeteringen | U kunt nu de opdracht `s3SessionToken` parameter om uw [!DNL Amazon S3] account aan Platform met tijdelijke beveiligingsgegevens. This token allows you to provide short-term, temporary access to your [!DNL Amazon S3] resources to users in untrusted environments. Zie de [[!DNL Amazon S3] documentatie](../../sources/connectors/cloud-storage/s3.md#prerequisites) voor meer informatie . |
| [!DNL Generic REST API] (bèta) | U kunt nu een [!DNL Generic REST API] bronverbinding met de [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) of de [gebruikersinterface](../../sources/tutorials/ui/create/protocols/generic-rest.md) gegevens van een generieke REST-toepassing naar het Platform te brengen. Zie de [[!DNL Generic REST API] overzicht](../../sources/connectors/protocols/generic-rest.md) voor meer informatie . |
| [!DNL Zoho CRM] (Beta) | You can now create a [!DNL Zoho CRM] source connection using the [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) or the [user interface](../../sources/tutorials/ui/create/crm/zoho.md) to bring data from your [!DNL Zoho CRM] account to Platform. See the [[!DNL Zoho CRM] overview](../../sources/connectors/crm/zoho.md) for more information. |

Zie voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).
