---
title: Opmerkingen bij de release van Adobe Experience Platform, april 2021
description: In de release van april 2021 staat een opmerking voor Adobe Experience Platform.
doc-type: release notes
last-update: April 21, 2021
author: ens72741
exl-id: cc78e48a-3578-4c55-ae86-1946d62bddb9
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 8%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 21 april 2021**

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Experience Data Model (XDM)]](#xdm)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om, gegevens aan en van het Model van Gegevens van de Ervaring in kaart te brengen om te zetten en te bevestigen (XDM).

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Ondersteuning voor het bewerken van toewijzingen voor bestaande gegevensstromen | U kunt nu de sets met toewijzingen van een bestaande gegevensstroom bijwerken. U kunt geen toewijzingssets bijwerken voor gegevensstromen die voor eenmalig gebruik waren gepland. Deze functie wordt niet ondersteund voor HTTP API, Adobe Analytics, Adobe Audience Manager en [!DNL Marketo Engage]. Raadpleeg de zelfstudie voor meer informatie [het bijwerken van bronnen dataflows in UI](../../sources/tutorials/ui/update-dataflows.md). |
| Ondersteuning voor streaming-opname | U kunt nu functies van het gegevensvoorvoegsel gebruiken wanneer u een streamingbronverbinding maakt. Raadpleeg de zelfstudie voor meer informatie [het creëren van een het stromen bronverbinding in UI](../../sources/tutorials/ui/create/streaming/http.md). |

Zie voor meer informatie de [[!DNL Data Prep] overzicht](../../data-prep/home.md).

## [!DNL Experience Data Model (XDM)] {#xdm}

Het Model van Gegevens van de ervaring (XDM) is een open-bronspecificatie die wordt ontworpen om de kracht van digitale ervaringen te verbeteren. Het verstrekt gemeenschappelijke structuren en definities voor om het even welke toepassing om met de diensten op Adobe Experience Platform te communiceren. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

| Functie | Beschrijving |
| --- | --- |
| Aanbevelingen van het bedrijfsleven inzake schema | Wanneer het selecteren van klassen en groepen van het schemagebied in de Redacteur UI van het Schema, kunt u een nieuw filter gebruiken om geadviseerde standaardcomponenten te bekijken die op uw specifieke industrie worden gebaseerd. Zie de documentatie op [bedrijfsgegevensmodellen](https://www.adobe.com/go/xdm-industry-erds-en) voor meer informatie over hoe deze componenten op elkaar betrekking hebben voor verschillende gevallen van gebruik in de industrie . |

## [!DNL Intelligent Services] {#intelligent-services}

Intelligente services stellen marketinganalisten en praktijkmensen in staat om gebruik te maken van de kracht van kunstmatige intelligentie en het leren van machines in gebruiksgevallen van de klantervaring. Dit staat voor marketing analisten toe om voorspellingen op te zetten specifiek voor de behoeften van een bedrijf gebruikend zaken-vlakke configuraties zonder de behoefte aan de deskundigheid van de gegevenswetenschap.

### Customer AI

De in Real-time Customer Data Platform beschikbare AI van de klant wordt gebruikt om aangepaste eigenschapscores zoals kurn en conversie voor individuele profielen op schaal te produceren. Dit wordt bereikt zonder de bedrijfsbehoeften te hoeven omzetten in een machine learning-probleem, een algoritme te kiezen, te trainen of te implementeren.

| Functie | Beschrijving |
| ------- | ----------- |
| Ondersteuning voor Adobe Analytics-gegevens | Bijgewerkte functionaliteit om de datasets van Adobe Analytics via de bron van Analytics schakelaar zonder de behoefte te steunen om uw gegevens te ETL om aan het schema van de Gebeurtenis van de Consumentenervaring (CEE) in overeenstemming te zijn. |
| Ondersteuning voor Adobe Audience Manager-gegevens | Bijgewerkte functionaliteit om de datasets van Adobe Audience Manager via de Audience Manager bronschakelaar zonder de behoefte te steunen om uw gegevens te ETL om aan het schema van de Gebeurtenis van de Consumentenervaring (CEE) in overeenstemming te zijn. |
| Overzicht van modelprestaties | AI van klant heeft nu een [overzicht van modelprestaties, tabblad](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics) binnen de pagina van de Inzichten van de de dienstinstantie. Op het tabblad Modelprestaties worden alle werkelijke conversie- en koelingssnelheden weergegeven. Hierdoor kun je ontcijferen en begrijpen wat er gebeurt in elk van je nevenemmers. |

Voor meer informatie over ondersteunde gegevenssets raadpleegt u de [[!DNL Intelligent Services] documentatie over gegevensvoorbereiding](../../intelligent-services/data-preparation.md).

### Attribution AI

Attribution AI wordt gebruikt om credits toe te wijzen aan touchpoints die leiden tot conversiegebeurtenissen. Dit kan door marketeers worden gebruikt om de marketingimpact van elk individueel marketing-touchpoint in journeys van de klant te kwantificeren.

| Functie | Beschrijving |
| ------- | ----------- |
| Ondersteuning voor Adobe Analytics-gegevens | Bijgewerkte functionaliteit om de datasets van Adobe Analytics via de bron van Analytics schakelaar zonder de behoefte te steunen om uw gegevens te ETL om aan het schema van de Gebeurtenis van de Consumentenervaring (CEE) in overeenstemming te zijn. |

Voor meer informatie over ondersteunde gegevenssets raadpleegt u de [[!DNL Intelligent Services] documentatie over gegevensvoorbereiding](../../intelligent-services/data-preparation.md).

## Segmenteringsservice {#segmentation}

Adobe Experience Platform Segmentation Service biedt een gebruikersinterface en RESTful API waarmee u segmenten kunt samenstellen en doelgroepen kunt genereren op basis van uw [!DNL Real-Time Customer Profile] gegevens. Deze segmenten worden centraal gevormd en gehandhaafd op Platform, die hen gemakkelijk toegankelijk maken door om het even welke toepassing van de Adobe.

[!DNL Segmentation Service] definieert een bepaalde subset van profielen door de criteria te beschrijven die een verhandelbare groep personen binnen uw klantenbasis onderscheiden. De segmenten kunnen op verslaggegevens (zoals demografische informatie) of tijdreeksgebeurtenissen worden gebaseerd die klanteninteractie met uw merk vertegenwoordigen.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Aanvullende aggregatiefuncties | De functies van de telling zijn toegevoegd in de Bouwer van het Segment. Met telfuncties kunt u tellen hoe vaak de opgegeven gebeurtenis is uitgevoerd. Meer informatie over de telfuncties vindt u in de sectie voor telfuncties van het dialoogvenster [Handleiding Segment Builder](../../segmentation/ui/segment-builder.md#count-functions) |

Voor meer informatie over [!DNL Segmentation Service], zie de [Overzicht van segmentatie](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

| Functie | Beschrijving |
| ------- | ----------- |
| [!DNL Marketo Engage] (bèta) | U kunt nu een [!DNL Marketo Engage] bronverbinding die UI gebruikt om B2B- gegevens aan Platform te brengen en deze gegevens bijgewerkt te houden gebruikend Platform-verbonden toepassingen. Zie voor meer informatie de [[!DNL Marketo Engage] documentatie van bronaansluiting](../../sources/connectors/adobe-applications/marketo/marketo.md). |
| Bètabronnen die naar GA gaan | De volgende bronnen zijn gepromoveerd van bèta naar GA: <ul><li>[[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure EventHubs]](../../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../../sources/connectors/streaming/http.md)</li><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL Microsoft SQL Server]](../../sources/connectors/databases/sql-server.md)</li><li>[[!DNL Oracle]](../../sources/connectors/databases/oracle.md)</li></ul> |

Zie voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).
