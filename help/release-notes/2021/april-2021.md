---
title: Aanvullende informatie van april 2021 voor Adobe Experience Platform
description: Aanvullende informatie van april 2021 voor Adobe Experience Platform.
doc-type: release notes
last-update: April 21, 2021
author: ens72741
exl-id: cc78e48a-3578-4c55-ae86-1946d62bddb9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 27%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum: donderdag 21 april 2021**

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Experience Data Model (XDM)]](#xdm)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om gegevens in kaart te brengen, om te zetten en te bevestigen aan en van het Model van de Gegevens van de Ervaring (XDM).

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Ondersteuning voor het bewerken van toewijzingen voor bestaande gegevensstromen | U kunt nu de sets met toewijzingen van een bestaande gegevensstroom bijwerken. U kunt geen toewijzingssets bijwerken voor gegevensstromen die voor eenmalig gebruik waren gepland. Deze functie wordt niet ondersteund voor HTTP API, Adobe Analytics, Adobe Audience Manager en [!DNL Marketo Engage] . Voor meer informatie, zie het leerprogramma bij [ het bijwerken van bronnen dataflows in UI ](../../sources/tutorials/ui/update-dataflows.md). |
| Ondersteuning voor streaming-opname | U kunt nu functies van het gegevensvoorvoegsel gebruiken wanneer u een streamingbronverbinding maakt. Voor meer informatie, zie het leerprogramma bij [ het creëren van een het stromen bronverbinding in UI ](../../sources/tutorials/ui/create/streaming/http.md). |

Voor meer informatie, gelieve te zien het [[!DNL Data Prep]  overzicht ](../../data-prep/home.md).

## [!DNL Experience Data Model (XDM)] {#xdm}

Het Model van Gegevens van de ervaring (XDM) is een open-bronspecificatie die wordt ontworpen om de kracht van digitale ervaringen te verbeteren. Het verstrekt gemeenschappelijke structuren en definities voor om het even welke toepassing om met de diensten op Adobe Experience Platform te communiceren. Door de XDM-standaarden te hanteren, kunnen alle gegevens over de klantervaring worden opgenomen in een gemeenschappelijke weergave. Zo worden inzichten sneller en beter geïntegreerd verkregen. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

| Functie | Beschrijving |
| --- | --- |
| Aanbevelingen van het bedrijfsleven inzake schema | Wanneer het selecteren van klassen en groepen van het schemagebied in de Redacteur UI van het Schema, kunt u een nieuw filter gebruiken om geadviseerde standaardcomponenten te bekijken die op uw specifieke industrie worden gebaseerd. Zie de documentatie over [ de modellen van de industriegegevens ](https://www.adobe.com/go/xdm-industry-erds-en) voor meer informatie over hoe deze componenten met elkaar voor verschillende de gebruiksgevallen van de industrie betrekking hebben. |

## [!DNL Intelligent Services] {#intelligent-services}

Intelligente services stellen marketinganalisten en praktijkmensen in staat om gebruik te maken van de kracht van kunstmatige intelligentie en het leren van machines in gebruiksgevallen van de klantervaring. Dit staat voor marketing analisten toe om voorspellingen op te zetten specifiek voor de behoeften van een bedrijf gebruikend zaken-vlakke configuraties zonder de behoefte aan de deskundigheid van de gegevenswetenschap.

### Customer AI

De in Real-Time Customer Data Platform beschikbare AI van de klant wordt gebruikt om aangepaste eigenschapscores zoals kurn en conversie voor individuele profielen op schaal te produceren. Dit wordt bereikt zonder de bedrijfsbehoeften te hoeven omzetten in een machine learning-probleem, een algoritme te kiezen, te trainen of te implementeren.

| Functie | Beschrijving |
| ------- | ----------- |
| Ondersteuning voor Adobe Analytics-gegevens | Bijgewerkte functionaliteit om Adobe Analytics datasets via de bron van Analytics schakelaar zonder de behoefte te steunen om uw gegevens te ETL om aan het schema van de Gebeurtenis van de Consumentenervaring (CEE) in overeenstemming te zijn. |
| Ondersteuning voor Adobe Audience Manager-gegevens | Bijgewerkte functionaliteit om Adobe Audience Manager datasets via de Audience Manager bronschakelaar te steunen zonder de behoefte om uw gegevens te ETL om aan het schema van de Gebeurtenis van de Consumentenervaring (CEE) in overeenstemming te zijn. |
| Overzicht van modelprestaties | De Klant AI heeft nu het overzicht tabel van de a [ modelprestaties ](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics) binnen de pagina van de Inzichten van de de dienstinstantie. Op het tabblad Modelprestaties worden alle werkelijke conversie- en koelingssnelheden weergegeven. Hierdoor kun je ontcijferen en begrijpen wat er gebeurt in elk van je nevenemmers. |

Voor meer informatie over gesteunde datasets, zie gelieve de [[!DNL Intelligent Services]  documentatie van de gegevensvoorbereiding ](../../intelligent-services/data-preparation.md).

### Attributie-AI

Attribution AI wordt gebruikt om credits toe te wijzen aan touchpoints die leiden tot conversiegebeurtenissen. Dit kan door marketeers worden gebruikt om de marketingimpact van elk individueel marketing-touchpoint in journeys van de klant te kwantificeren.

| Functie | Beschrijving |
| ------- | ----------- |
| Ondersteuning voor Adobe Analytics-gegevens | Bijgewerkte functionaliteit om Adobe Analytics datasets via de bron van Analytics schakelaar zonder de behoefte te steunen om uw gegevens te ETL om aan het schema van de Gebeurtenis van de Consumentenervaring (CEE) in overeenstemming te zijn. |

Voor meer informatie over gesteunde datasets, zie gelieve de [[!DNL Intelligent Services]  documentatie van de gegevensvoorbereiding ](../../intelligent-services/data-preparation.md).

## Segmentatieservice {#segmentation}

Adobe Experience Platform Segmentation Service biedt een gebruikersinterface en RESTful-API waarmee u segmenten kunt samenstellen en doelgroepen kunt genereren op basis van uw [!DNL Real-Time Customer Profile] -gegevens. Deze segmenten worden centraal geconfigureerd en onderhouden op Experience Platform, waardoor ze gemakkelijk toegankelijk zijn voor alle Adobe-toepassingen.

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Aanvullende aggregatiefuncties | De functies van de telling zijn toegevoegd in de Bouwer van het Segment. Met telfuncties kunt u tellen hoe vaak de opgegeven gebeurtenis is uitgevoerd. Meer informatie over de tellingsfuncties kan in de sectie van tellingsfuncties van de [ gids van de Bouwer van het Segment ](../../segmentation/ui/segment-builder.md#count-functions) worden gevonden |

Voor meer informatie over [!DNL Segmentation Service], raadpleegt u het [overzicht van segmentatie](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens opnemen uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

| Functie | Beschrijving |
| ------- | ----------- |
| [!DNL Marketo Engage] (Beta) | U kunt nu een [!DNL Marketo Engage] -bronverbinding maken met behulp van de gebruikersinterface om B2B-gegevens naar Experience Platform te verzenden en deze gegevens up-to-date te houden met Experience Platform-toepassingen. Voor meer informatie, zie de [[!DNL Marketo Engage]  documentatie van de bronschakelaar ](../../sources/connectors/adobe-applications/marketo/marketo.md). |
| Beta-bronnen die naar GA gaan | De volgende bronnen zijn gepromoveerd van bèta naar GA: <ul><li>[[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure EventHubs]](../../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../../sources/connectors/streaming/http.md)</li><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL Microsoft SQL Server]](../../sources/connectors/databases/sql-server.md)</li><li>[[!DNL Oracle]](../../sources/connectors/databases/oracle.md)</li></ul> |

Meer over bronnen leren, zie het [ overzicht van bronnen ](../../sources/home.md).
