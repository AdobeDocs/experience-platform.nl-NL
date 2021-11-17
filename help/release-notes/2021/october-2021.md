---
title: Opmerkingen bij de release van Adobe Experience Platform
description: De meest recente releaseopmerkingen voor Adobe Experience Platform.
source-git-commit: da9204f1581832d6885acd64387cf7e83c4b012a
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 2%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 27 oktober 2021**

## Updates voor Experience Platform

Updates voor Experience Platform.

### Gebruikersinterface {#ui}

De gebruikersinterface is bijgewerkt met de volgende wijzigingen:

| Functie | Beschrijving |
| --- | --- |
| Donker thema | Met de themakeuze Donker schakelt u tussen lichte en donkere thema&#39;s in de interface van het Platform. De switch staat in het gebruikersprofiel onder gebruikersnaam en e-mail. |
| Linkernavigatie in-/uitschakelen | Met de verbeterde navigatieknop boven aan de toepassingskop kunt u het menu met de mogelijkheden van uw Experience Platform weergeven of verbergen. Het systeem onthoudt uw laatste selectie en geeft alleen de mogelijkheden weer waartoe u toegang hebt. |
| Toegangszichtbaarheid | Op de linkernavigatiebalk ziet u alleen de functies waartoe u toegang hebt. In eerdere versies van Adobe Experience Platform waren niet-beschikbare items zichtbaar, zelfs als u deze niet kon openen. |

Zie de [UI-gids voor Platform](../../landing/ui-guide.md) voor meer informatie.

## Updates voor bestaande functies

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [Bronnen](#sources)

### [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om, gegevens aan en van het Model van Gegevens van de Ervaring in kaart te brengen om te zetten en te bevestigen (XDM).

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| `contains_key` -functie | De `contains_key` functie is geïntroduceerd, waarmee u kunt controleren of het object in de bron bestaat. Deze functie vervangt de `is_set` functie, die nu is afgekeurd. |
| Foutberichten | Foutberichten die door de `/mappingSets/preview` eindpunt in de Prep API van Gegevens zijn nu verenigbaar met de foutenmeldingen die tijdens runtime worden geproduceerd. |

Zie de [[!DNL Data Prep] overzicht](../../data-prep/home.md) voor meer informatie over deze service.

### Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

| Functie | Beschrijving |
| --- | --- |
| [!DNL Amazon S3] bronverbeteringen | U kunt nu de opdracht `s3SessionToken` parameter om uw [!DNL Amazon S3] account aan Platform met tijdelijke beveiligingsgegevens. Met dit token kunt u op korte termijn tijdelijke toegang tot uw [!DNL Amazon S3] bronnen voor gebruikers in niet-vertrouwde omgevingen. Zie de [[!DNL Amazon S3] documentatie](../../sources/connectors/cloud-storage/s3.md#prerequisites) voor meer informatie . |
| [!DNL Generic REST API] (bèta) | U kunt nu een [!DNL Generic REST API] bronverbinding met de [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) gegevens van een generieke REST-toepassing naar het Platform te brengen. Zie de [[!DNL Generic REST API] overzicht](../../sources/connectors/protocols/generic-rest.md) voor meer informatie . |
| [!DNL Zoho CRM] (bèta) | U kunt nu een [!DNL Zoho CRM] bronverbinding met de [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) of de [gebruikersinterface](../../sources/tutorials/ui/create/crm/zoho.md) om gegevens van uw [!DNL Zoho CRM] aan Platform. Zie de [[!DNL Zoho CRM] overzicht](../../sources/connectors/crm/zoho.md) voor meer informatie . |

Zie voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).