---
title: Opmerkingen bij de release van Adobe Experience Platform, oktober 2021
description: Aanvullende informatie voor de versie van oktober 2021 voor Adobe Experience Platform.
exl-id: 8f8bcb24-6478-4281-9362-9559158384af
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 4%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: donderdag 27 oktober 2021**

## Updates voor Experience Platform

Updates voor Experience Platform.

### Gebruikersinterface {#ui}

De gebruikersinterface is bijgewerkt met de volgende wijzigingen:

| Functie | Beschrijving |
| --- | --- |
| Donker thema | Gebruik de Donkere themakeuze om te schakelen tussen lichte en donkere thema&#39;s in de interface van het Platform. De switch staat in het gebruikersprofiel onder gebruikersnaam en e-mail. |
| Linkernavigatie in-/uitschakelen | Met de verbeterde navigatieknop boven aan de toepassingskop kunt u het menu met de mogelijkheden van uw Experience Platform weergeven of verbergen. Het systeem onthoudt uw laatste selectie en geeft alleen de mogelijkheden weer waartoe u toegang hebt. |
| Toegangszichtbaarheid | Op de linkernavigatiebalk ziet u alleen de functies waartoe u toegang hebt. In eerdere versies van Adobe Experience Platform waren niet-beschikbare items zichtbaar, zelfs als u deze niet kon openen. |

Zie de [ Gids UI van het Platform ](../../landing/ui-guide.md) om meer te leren.

## Updates voor bestaande functies

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [Bronnen](#sources)

### [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om gegevens in kaart te brengen, om te zetten en te bevestigen aan en van het Model van de Gegevens van de Ervaring (XDM).

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| `contains_key` functie | De functie `contains_key` is geïntroduceerd, waarmee u kunt controleren of het object binnen de bron bestaat. Deze functie vervangt de functie `is_set` , die nu is vervangen. |
| Foutberichten | Foutberichten die door het `/mappingSets/preview` -eindpunt in de Data Prep API worden geretourneerd, zijn nu consistent met de foutberichten die tijdens runtime worden gegenereerd. |

Zie het [[!DNL Data Prep]  overzicht ](../../data-prep/home.md) om meer over deze dienst te leren.

### Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van de platformservices. U kunt gegevens van een verscheidenheid van bronnen zoals de toepassingen van de Adobe, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

| Functie | Beschrijving |
| --- | --- |
| [!DNL Amazon S3] bronverbeteringen | U kunt de parameter `s3SessionToken` nu gebruiken om uw [!DNL Amazon S3] -account te verbinden met Platform met behulp van tijdelijke beveiligingsreferenties. Met dit token kunt u gebruikers in niet-vertrouwde omgevingen op korte termijn tijdelijke toegang geven tot uw [!DNL Amazon S3] -bronnen. Zie de [[!DNL Amazon S3]  documentatie ](../../sources/connectors/cloud-storage/s3.md#prerequisites) voor meer informatie. |
| [!DNL Generic REST API] (Beta) | U kunt een [!DNL Generic REST API] bronverbinding nu tot stand brengen gebruikend [[!DNL Flow Service]  API ](../../sources/tutorials/api/create/protocols/generic-rest.md) om gegevens van een generische toepassing van REST aan Platform te brengen. Zie het [[!DNL Generic REST API]  overzicht ](../../sources/connectors/protocols/generic-rest.md) voor meer informatie. |
| [!DNL Zoho CRM] (Beta) | U kunt een [!DNL Zoho CRM] bronverbinding nu tot stand brengen gebruikend [[!DNL Flow Service]  API ](../../sources/tutorials/api/create/crm/zoho.md) of het [ gebruikersinterface ](../../sources/tutorials/ui/create/crm/zoho.md) om gegevens van uw [!DNL Zoho CRM] rekening aan Platform te brengen. Zie het [[!DNL Zoho CRM]  overzicht ](../../sources/connectors/crm/zoho.md) voor meer informatie. |

Meer over bronnen leren, zie het [ overzicht van bronnen ](../../sources/home.md).
