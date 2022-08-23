---
title: Opmerkingen bij de release van Adobe Experience Platform, augustus 2022
description: De release van augustus 2022 bevat opmerkingen voor Adobe Experience Platform.
source-git-commit: b8513fa214ea74eec6809796cc194466e05cbb21
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 2%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 24 augustus 2022**

Updates voor bestaande functies in Adobe Experience Platform:

- [Gegevensprep](#data-prep)
- [Bronnen](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om, gegevens aan en van het Model van Gegevens van de Ervaring in kaart te brengen om te zetten en te bevestigen (XDM).

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor het opnemen van records met waarschuwingen | Met Data Prep worden nu waarschuwingen (niet-kritieke fouten) gelokaliseerd voor de velden en kan de rest van de rij worden ingevoegd. Alle maptransformatiefouten worden nu gerapporteerd als waarschuwingen en rijen die gedeeltelijk worden ingepakt, worden als geslaagd beschouwd, met een waarschuwing.  De bewaking wordt ook ondersteund in registers met waarschuwingen en diagnostische details. Gedeeltelijke invoer van records met waarschuwingen is momenteel alleen beschikbaar voor streaming gegevens. Raadpleeg de documentatie over [opnemen, records met waarschuwingen](../../sources/tutorials/ui/monitor-streaming.md) voor meer informatie . |

{style=&quot;table-layout:auto&quot;}

Meer informatie over [!DNL Data Prep], zie de [[!DNL Data Prep] overzicht](../../data-prep/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Algemene beschikbaarheid van Self-Serve Bronnen (Batch SDK) | Ontwikkel, test, en integreer uw REST API-based gegevensbron om partijgegevens in Experience Platform in te voeren gebruikend gemakkelijk om bronspecificaties te vormen. Met Bronnen SDK kunt u: <ul><li>Vorm een nieuwe bron aan de catalogus van het Experience Platform.</li><li>Bepaal specificaties voor uw bron, met inbegrip van informatie betreffende gesteunde authentificatietypen, het plannen, en hoe de middelgegevens worden gehaald.</li><li>Maak gebruikersgerichte documentatie voor uw nieuwe bron.</li></ul> Lees de documentatie over [Self-Serve Sources (Batch SDK)](../../sources/sources-sdk/overview.md). |
| Algemene beschikbaarheid van [!DNL Google BigQuery] bron | Gebruik de [!DNL Google BigQuery] bron om gegevens van uw [!DNL Google BigQuery] datawarepot aan Experience Platform. Voor meer informatie leest u de documentatie op het tabblad [[!DNL Google BigQuery] bron](../../sources/connectors/databases/bigquery.md). |
| [!DNL Teradata Vantage] bron (bèta) | Gebruik de [!DNL Teradata Vantage] bron voor het opnemen van gegevens van hybride multi-wolkomgevingen naar Experience Platform. Voor meer informatie leest u de documentatie op het tabblad [[!DNL Teradata Vantage] bron](../../sources/connectors/databases/teradata-vantage.md). |
| Ondersteuning voor verschillende regio&#39;s van Adobe Analytics-bronnen | U kunt nu rapportsuites uit om het even welke regio (Verenigde Staten, Verenigd Koninkrijk, of Singapore) opnemen. Rapportsuites moeten worden toegewezen aan dezelfde organisatie als de Sandbox-instantie van het Experience Platform waarin de bronverbinding wordt gemaakt. Lees voor meer informatie de handleiding op [een Adobe Analytics-bronverbinding maken in de gebruikersinterface](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |
| API-ondersteuning voor inname op aanvraag | Gebruik inname op aanvraag om een ad-hocflowrun voor een bepaalde gegevensstroom te maken met de [!DNL Flow Service] API. De gecreeerde looppas van de stroom moet aan éénmalige opname worden geplaatst. Lees voor meer informatie de handleiding op [een flow-run maken voor opname op aanvraag met behulp van de API](../../sources/tutorials/api/on-demand-ingestion.md) voor meer informatie . |

{style=&quot;table-layout:auto&quot;}

Zie voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).
