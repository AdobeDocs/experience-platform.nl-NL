---
title: Aanvullende informatie van maart 2021 voor Adobe Experience Platform
description: Aanvullende informatie van maart 2021 voor Adobe Experience Platform.
doc-type: release notes
last-update: March 31, 2021
author: ens72741
exl-id: 027cd7b1-1651-4939-bc97-968a41824117
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 31%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum:donderdag 31 maart 2021**

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

Voor meer informatie, gelieve te zien het [[!DNL Data Prep]  overzicht &#x200B;](../../data-prep/home.md).

## Segmentatieservice {#segmentation}

Adobe Experience Platform Segmentation Service biedt een gebruikersinterface en RESTful-API waarmee u segmenten kunt samenstellen en doelgroepen kunt genereren op basis van uw [!DNL Real-Time Customer Profile] -gegevens. Deze segmenten worden centraal geconfigureerd en onderhouden op [!DNL Experience Platform], zodat ze gemakkelijk toegankelijk zijn voor alle Adobe-toepassingen.

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| (Beta) Edge-segmentatie | Edge-segmentatie evalueert segmenten in real-time, zodat dezelfde pagina en volgende pagina kunnen worden gebruikt. Meer informatie over randsegmentatie kan in het [&#x200B; overzicht van de Segmentatie UI &#x200B;](../../segmentation/ui/overview.md) worden gevonden. |
| (Beta) Incrementele segmentatie | Verhoogt de versheid van bestaande segmentdefinities die in partijsegmentatie worden geëvalueerd tot een uur. |

Voor meer informatie over [!DNL Segmentation Service], raadpleegt u het [overzicht van segmentatie](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens opnemen uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

| Functie | Beschrijving |
| ------- | ----------- |
| Beta-bronnen die naar GA gaan | De volgende bronnen zijn gepromoveerd van bèta naar GA: <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| API-ondersteuning voor gecomprimeerde bestandsopname | U kunt nu gecomprimeerde JSON- of gescheiden bestanden voorvertonen en opnemen met bronnen voor cloudopslag. Voor meer informatie, zie het leerprogramma over [&#x200B; het verzamelen van gegevens van de wolkenopslag gebruikend APIs &#x200B;](../../sources/tutorials/api/collect/cloud-storage.md). |
| UI-ondersteuning voor het uploaden van recursieve bestanden | U kunt nu volledige mappen recursief invoeren wanneer u een bron voor cloudopslag gebruikt. Wanneer u een volledige map opgeeft, moet u ervoor zorgen dat de inhoud ervan hetzelfde schema deelt. Voor meer informatie, zie het leerprogramma op [&#x200B; vormend een dataflow voor de schakelaars van de wolkenopslag in UI &#x200B;](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Meer over bronnen leren, zie het [&#x200B; overzicht van bronnen &#x200B;](../../sources/home.md).
