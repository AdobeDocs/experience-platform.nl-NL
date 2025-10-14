---
title: Aanvullende informatie van oktober 2021 voor Adobe Experience Platform
description: Aanvullende informatie van oktober 2021 voor Adobe Experience Platform.
exl-id: 8f8bcb24-6478-4281-9362-9559158384af
source-git-commit: 2e41a1716e057cd33e4635c11ba9c3cfc185418a
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 19%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum: donderdag 27 oktober 2021**

## Updates voor Experience Platform

Updates voor Experience Platform.

### Gebruikersinterface {#ui}

De gebruikersinterface is bijgewerkt met de volgende wijzigingen:

| Functie | Beschrijving |
| --- | --- |
| Donker thema | Met de themakeuze Donker schakelt u tussen lichte en donkere thema&#39;s in de Experience Platform-interface. De switch staat in het gebruikersprofiel onder gebruikersnaam en e-mail. |
| Linkernavigatie in-/uitschakelen | Met de verbeterde navigatieknop boven aan de toepassingskop kunt u het menu met uw Experience Platform-mogelijkheden weergeven of verbergen. Het systeem onthoudt uw laatste selectie en geeft alleen de mogelijkheden weer waartoe u toegang hebt. |
| Toegangszichtbaarheid | Op de linkernavigatiebalk ziet u alleen de functies waartoe u toegang hebt. In eerdere versies van Adobe Experience Platform waren niet-beschikbare items zichtbaar, zelfs als u deze niet kon openen. |

Zie de [&#x200B; Gids UI van Experience Platform &#x200B;](../../landing/ui-guide.md) om meer te leren.

## Updates voor bestaande functies

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [Bronnen](#sources)

### [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om gegevens in kaart te brengen, om te zetten en te bevestigen aan en van het Model van de Gegevens van de Ervaring (XDM).

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| `contains_key` functie | De functie `contains_key` is geïntroduceerd, waarmee u kunt controleren of het object binnen de bron bestaat. Deze functie vervangt de functie `is_set` , die nu is vervangen. |
| Foutberichten | Foutberichten die door het `/mappingSets/preview` -eindpunt in de Data Prep API worden geretourneerd, zijn nu consistent met de foutberichten die tijdens runtime worden gegenereerd. |

Zie het [[!DNL Data Prep]  overzicht &#x200B;](../../data-prep/home.md) om meer over deze dienst te leren.

### Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens opnemen uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

| Functie | Beschrijving |
| --- | --- |
| [!DNL Amazon S3] bronverbeteringen | U kunt de parameter `s3SessionToken` nu gebruiken om uw [!DNL Amazon S3] -account aan te sluiten op Experience Platform met behulp van tijdelijke beveiligingsgegevens. Met dit token kunt u gebruikers in niet-vertrouwde omgevingen op korte termijn tijdelijke toegang geven tot uw [!DNL Amazon S3] -bronnen. Zie de [[!DNL Amazon S3]  documentatie &#x200B;](../../sources/connectors/cloud-storage/s3.md#prerequisites) voor meer informatie. |
| [!DNL Generic REST API] (Beta) | U kunt een [!DNL Generic REST API] bronverbinding nu tot stand brengen gebruikend [[!DNL Flow Service]  API &#x200B;](../../sources/tutorials/api/create/protocols/generic-rest.md) om gegevens van een generische toepassing van REST aan Experience Platform te brengen. Zie het [[!DNL Generic REST API]  overzicht &#x200B;](../../sources/connectors/protocols/generic-rest.md) voor meer informatie. |

Meer over bronnen leren, zie het [&#x200B; overzicht van bronnen &#x200B;](../../sources/home.md).
