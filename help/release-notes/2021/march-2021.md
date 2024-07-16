---
title: Opmerkingen bij de release van Adobe Experience Platform maart 2021
description: Aanvullende informatie van maart 2021 voor Adobe Experience Platform.
doc-type: release notes
last-update: March 31, 2021
author: ens72741
exl-id: 027cd7b1-1651-4939-bc97-968a41824117
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 4%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: donderdag 31 maart 2021**

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om gegevens in kaart te brengen, om te zetten en te bevestigen aan en van het Model van de Gegevens van de Ervaring (XDM).

| Functie | Beschrijving |
| ------- | ----------- |
| `add_to_array` functie | Bijgewerkte functionaliteit om arrays als parameter te ondersteunen. |
| `to_array` functie | Bijgewerkte functionaliteit om objecten als parameter te ondersteunen. |

Voor meer informatie, gelieve te zien het [[!DNL Data Prep]  overzicht ](../../data-prep/home.md).

## Segmenteringsservice {#segmentation}

Adobe Experience Platform Segmentation Service biedt een gebruikersinterface en RESTful-API waarmee u segmenten kunt samenstellen en doelgroepen kunt genereren op basis van uw [!DNL Real-Time Customer Profile] -gegevens. Deze segmenten worden centraal geconfigureerd en onderhouden op [!DNL Platform], zodat ze gemakkelijk toegankelijk zijn voor elke Adobe.

[!DNL Segmentation Service] definieert een bepaalde subset van profielen door de criteria te beschrijven die een verhandelbare groep personen binnen uw klantenbasis onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| (Beta) Edge-segmentatie | Edge-segmentatie evalueert segmenten in real-time, zodat dezelfde pagina en volgende pagina kunnen worden gebruikt. Meer informatie over randsegmentatie kan in het [ overzicht van de Segmentatie UI ](../../segmentation/ui/overview.md) worden gevonden. |
| (Beta) Incrementele segmentatie | Verhoogt de versheid van bestaande segmentdefinities die in partijsegmentatie worden geëvalueerd tot een uur. |

Voor meer informatie over [!DNL Segmentation Service], gelieve te zien het [ overzicht van de Segmentatie ](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van de platformservices. U kunt gegevens van een verscheidenheid van bronnen zoals de toepassingen van de Adobe, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

| Functie | Beschrijving |
| ------- | ----------- |
| Beta-bronnen die naar GA gaan | De volgende bronnen zijn gepromoveerd van bèta naar GA: <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| API-ondersteuning voor gecomprimeerde bestandsopname | U kunt nu gecomprimeerde JSON- of gescheiden bestanden voorvertonen en opnemen met bronnen voor cloudopslag. Voor meer informatie, zie het leerprogramma over [ het verzamelen van gegevens van de wolkenopslag gebruikend APIs ](../../sources/tutorials/api/collect/cloud-storage.md). |
| UI-ondersteuning voor het uploaden van recursieve bestanden | U kunt nu volledige mappen recursief invoeren wanneer u een bron voor cloudopslag gebruikt. Wanneer u een volledige map opgeeft, moet u ervoor zorgen dat de inhoud ervan hetzelfde schema deelt. Voor meer informatie, zie het leerprogramma op [ vormend een dataflow voor de schakelaars van de wolkenopslag in UI ](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Meer over bronnen leren, zie het [ overzicht van bronnen ](../../sources/home.md).
