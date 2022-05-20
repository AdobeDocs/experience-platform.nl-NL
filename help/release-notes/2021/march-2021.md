---
title: Opmerkingen bij de release van Adobe Experience Platform maart 2021
description: In de release van maart 2021 staat een opmerking voor Adobe Experience Platform.
doc-type: release notes
last-update: March 31, 2021
author: ens72741
exl-id: 027cd7b1-1651-4939-bc97-968a41824117
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 2%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 31 maart 2021**

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om, gegevens aan en van het Model van Gegevens van de Ervaring in kaart te brengen om te zetten en te bevestigen (XDM).

| Functie | Beschrijving |
| ------- | ----------- |
| `add_to_array` -functie | Bijgewerkte functionaliteit om arrays als parameter te ondersteunen. |
| `to_array` -functie | Bijgewerkte functionaliteit om objecten als parameter te ondersteunen. |

Zie voor meer informatie de [[!DNL Data Prep] overzicht](../../data-prep/home.md).

## Segmenteringsservice {#segmentation}

Adobe Experience Platform Segmentation Service biedt een gebruikersinterface en RESTful API waarmee u segmenten kunt samenstellen en doelgroepen kunt genereren op basis van uw [!DNL Real-time Customer Profile] gegevens. Deze segmenten worden centraal geconfigureerd en onderhouden op [!DNL Platform], zodat ze gemakkelijk toegankelijk zijn voor elke Adobe-toepassing.

[!DNL Segmentation Service] definieert een bepaalde subset van profielen door de criteria te beschrijven die een verhandelbare groep personen binnen uw klantenbasis onderscheiden. De segmenten kunnen op verslaggegevens (zoals demografische informatie) of tijdreeksgebeurtenissen worden gebaseerd die klanteninteractie met uw merk vertegenwoordigen.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| (bèta) segmentatie van randen | De segmentatie van de rand evalueert segmenten in real time, die voor de zelfde pagina en volgende het verpersoonlijkingsgebruiksgevallen van de paginagrootte toestaan. Meer informatie over de segmentatie van de randen vindt u in de [Overzicht van de segmenteringsinterface](../../segmentation/ui/overview.md). |
| (bèta) Incrementele segmentatie | Verhoogt de versheid van bestaande segmentdefinities die in partijsegmentatie worden geëvalueerd tot een uur. |

Voor meer informatie over [!DNL Segmentation Service], zie de [Overzicht van segmentatie](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

| Functie | Beschrijving |
| ------- | ----------- |
| Bètabronnen die naar GA gaan | De volgende bronnen zijn gepromoveerd van bèta naar GA: <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| API-ondersteuning voor gecomprimeerde bestandsopname | U kunt nu gecomprimeerde JSON- of gescheiden bestanden voorvertonen en opnemen met bronnen voor cloudopslag. Raadpleeg de zelfstudie voor meer informatie [gegevens voor cloudopslag verzamelen met behulp van API&#39;s](../../sources/tutorials/api/collect/cloud-storage.md). |
| UI-ondersteuning voor het uploaden van recursieve bestanden | U kunt nu volledige mappen recursief invoeren wanneer u een bron voor cloudopslag gebruikt. Wanneer u een volledige map opgeeft, moet u ervoor zorgen dat de inhoud ervan hetzelfde schema deelt. Raadpleeg de zelfstudie voor meer informatie [een gegevensstroom configureren voor cloudopslagconnectors in de gebruikersinterface](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Zie voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).
