---
title: Opmerkingen bij de release van Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform voor 31 maart 2021.
doc-type: release notes
last-update: March 31, 2021
author: ens70167
translation-type: tm+mt
source-git-commit: 7af082de034166e3a8a3971728d5743eaeec67ae
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 2%

---


# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 31 maart 2021**

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Sandboxes]](#sandboxes)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om, gegevens aan en van het Model van Gegevens van de Ervaring in kaart te brengen om te zetten en te bevestigen (XDM).

| Functie | Beschrijving |
| ------- | ----------- |
| `add_to_array` -functie | Bijgewerkte functionaliteit om arrays als parameter te ondersteunen. |
| `to_array` -functie | Bijgewerkte functionaliteit om objecten als parameter te ondersteunen. |

Zie [[!DNL Data Prep] overzicht](../../data-prep/home.md) voor meer informatie.

## [!DNL Sandboxes] {#sandboxes}

Adobe Experience Platform is ontworpen om toepassingen voor digitale beleving wereldwijd te verrijken. Bedrijven voeren vaak meerdere digitale-ervaringstoepassingen parallel uit en moeten rekening houden met de ontwikkeling, het testen en de implementatie van deze toepassingen en tegelijk de operationele compatibiliteit garanderen.

Om aan deze behoefte tegemoet te komen, biedt Experience Platform sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

| Functie | Beschrijving |
| ------- | ----------- |
| (Bèta) Meerdere productiesandboxen | U kunt nu meerdere productiesandboxen maken en beheren in uw IMS-organisatie en specifieke productiesandboxen toewijzen aan afzonderlijke bedrijfsonderdelen, merken, projecten of regio&#39;s. Zie de zelfstudies over het maken van een productiestandaard [in de gebruikersinterface](../../sandboxes/ui/user-guide.md) of [met behulp van de API](../../sandboxes/api/create-sandbox.md) voor meer informatie. |

Zie het [overzicht van sandboxen](../../sandboxes/home.md) voor meer informatie over sandboxen.

## Segmenteringsservice {#segmentation}

Adobe Experience Platform Segmentation Service biedt een gebruikersinterface en RESTful API waarmee u segmenten kunt bouwen en doelgroepen kunt genereren op basis van uw [!DNL Real-time Customer Profile]-gegevens. Deze segmenten worden centraal gevormd en gehandhaafd op [!DNL Platform], die hen gemakkelijk toegankelijk maken door om het even welke toepassing van de Adobe.

[!DNL Segmentation Service] definieert een bepaalde subset van profielen door de criteria te beschrijven die een verhandelbare groep personen binnen uw klantenbasis onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| (bèta) segmentatie van randen | De segmentatie van de rand evalueert segmenten in real time, die voor de zelfde pagina en volgende het verpersoonlijkingsgebruiksgevallen van de paginagrootte toestaan. Meer informatie over randsegmentatie kan in [Overzicht van segmentatie UI](../../segmentation/ui/overview.md) worden gevonden. |
| (bèta) Incrementele segmentatie | Verhoogt de versheid van bestaande segmentdefinities die in partijsegmentatie worden geëvalueerd tot een uur. |

Voor meer informatie over [!DNL Segmentation Service], te zien gelieve [Segmentatieoverzicht](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

| Functie | Beschrijving |
| ------- | ----------- |
| Bètabronnen die naar GA gaan | De volgende bronnen zijn gepromoveerd van bèta naar GA: <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| API-ondersteuning voor gecomprimeerde bestandsopname | U kunt nu gecomprimeerde JSON- of gescheiden bestanden voorvertonen en opnemen met bronnen voor cloudopslag. Zie de zelfstudie over [gegevens voor cloudopslag verzamelen met API&#39;s](../../sources/tutorials/api/collect/cloud-storage.md) voor meer informatie. |
| UI-ondersteuning voor het uploaden van recursieve bestanden | U kunt nu volledige mappen recursief invoeren wanneer u een bron voor cloudopslag gebruikt. Wanneer u een volledige map opgeeft, moet u ervoor zorgen dat de inhoud ervan hetzelfde schema deelt. Voor meer informatie, zie de zelfstudie over [het vormen van een gegevensstroom voor de schakelaars van de wolkenopslag in UI](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Meer over bronnen leren, zie [bronnen overzicht](../../sources/home.md).
