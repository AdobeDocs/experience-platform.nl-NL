---
title: Opmerkingen bij de release van Adobe Experience Platform, augustus 2022
description: De release van augustus 2022 bevat opmerkingen voor Adobe Experience Platform.
source-git-commit: 5967dee9c8b1c05ebd103998021e02a47ac3982c
workflow-type: tm+mt
source-wordcount: '1215'
ht-degree: 1%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 24 augustus 2022**

Updates voor bestaande functies in Adobe Experience Platform:

- [Gegevensprep](#data-prep)
- [Experience Data Model (XDM)](#xdm)
- [Klantprofiel in realtime](#profile)
- [Segmenteringsservice](#segmentation)
- [Bronnen](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om, gegevens aan en van het Model van Gegevens van de Ervaring in kaart te brengen om te zetten en te bevestigen (XDM).

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor het opnemen van records met waarschuwingen | Met Data Prep worden nu waarschuwingen (niet-kritieke fouten) gelokaliseerd voor de velden en kan de rest van de rij worden ingevoegd. Alle maptransformatiefouten worden nu gerapporteerd als waarschuwingen en rijen die gedeeltelijk worden ingepakt, worden als geslaagd beschouwd, met een waarschuwing.  De bewaking wordt ook ondersteund in registers met waarschuwingen en diagnostische details. Gedeeltelijke invoer van records met waarschuwingen is momenteel alleen beschikbaar voor streaming gegevens. Raadpleeg de documentatie over [opnemen, records met waarschuwingen](../../sources/tutorials/ui/monitor-streaming.md) voor meer informatie . |

{style=&quot;table-layout:auto&quot;}

Meer informatie over [!DNL Data Prep], zie de [[!DNL Data Prep] overzicht](../../data-prep/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe XDM-componenten**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Algemeen schema | [[!UICONTROL AJO Entity Schema]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity.schema.json) | Beschrijft gedenormaliseerde entiteiten voor Adobe Journey Optimizer. |
| Klasse | [[!UICONTROL AJO Execution Entities]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-execution-entity.schema.json) | Beschrijft de uitvoeringsentiteiten van Adobe Journey Optimizer voor gebruik in segmentatie. |
| Veldgroep | [[!UICONTROL Workfront Work Objects]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobjects-all.schema.json) | Een omvattende veldgroep die verwijst naar alle objectspecifieke veldgroepen op een lager niveau voor Adobe Workfront. |

{style=&quot;table-layout:auto&quot;}

**Bijgewerkte XDM-componenten**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Veldgroep | [[!UICONTROL Journey Orchestration Step Event Common Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Er zijn twee nieuwe eigenschappen toegevoegd: `origTimeStamp` en `experienceID`. |
| Veldgroep | [[!UICONTROL Segment Membership Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/segmentation.schema.json) | Naast [!UICONTROL XDM Individual Profile], kan deze veldgroep nu ook worden gebruikt in schema&#39;s die op de klasse van de Rekening van Bedrijfs XDM worden gebaseerd. |
| Veldgroep | (Meerdere) | Verschillende veldgroepen met betrekking tot de B2B-activiteiten van Marketo zijn bijgewerkt naar een stabiele status. Zie het volgende [pull-verzoek](https://github.com/adobe/xdm/pull/1593/files) voor meer informatie. |
| Veldgroep | (Meerdere) | Verschillende aan het weer gerelateerde veldgroepen zijn bijgewerkt om fouten op te lossen die voorkwamen voor `uvIndex` en `sunsetTime`. Zie het volgende [pull-verzoek](https://github.com/adobe/xdm/pull/1602/files) voor meer informatie. |
| Gegevenstype | [[!UICONTROL Product list item]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Een nieuwe eigenschap `productImageUrl` is toegevoegd. |
| Gegevenstype | [[!UICONTROL Qoe Data details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Een nieuwe eigenschap `framesPerSecond` is toegevoegd. |
| Gegevenstype | [[!UICONTROL Session details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | `sdkVersion` is hernoemd naar `appVersion`. `meta:enum` en `description` de velden zijn ook bijgewerkt. |
| Gegevenstypen en veldgroepen | (Meerdere) | Verschillende mediatypen en veldgroepen hebben nieuwe velden en bijgewerkte beschrijvingen. Zie het volgende [pull-verzoek](https://github.com/adobe/xdm/pull/1582/files) voor meer informatie. |
| (Alle) | (Meerdere) | Alle schemaobjecten die een `enum` veld bevat nu ook een overeenkomend veld `meta:enum` veld voor het aangeven van de weergavewaarden voor elke restrictie. Zie het volgende [pull-verzoek](https://github.com/adobe/xdm/pull/1601/files) voor meer informatie. |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over XDM in Platform, zie [XDM System, overzicht](../../xdm/home.md).

## Klantprofiel in realtime {#profile}

Met Adobe Experience Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met het Profiel van de Klant in real time, kunt u een holistische mening van elke individuele klant zien die gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens combineert. Het profiel staat u toe om klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

| Functie | Beschrijving |
| ------- | ----------- |
| Opschonen van kenmerken van rand met zwevend profiel | Voor alle organisaties, verwijdert de Dienst van het Profiel nu randattributen van gebruikersactiviteitengebied op een dagelijkse basis om een nauwkeurigere vertegenwoordiging van uw profielen in uw systeem te geven. Deze opschoonbewerking vindt plaats nadat alle profielfragmenten voor een bepaald profiel zijn verwijderd. Dit heeft gevolgen voor profielen die worden samengevoegd in gegevenssets waarin `com_adobe_aep_profile_region_dataset` is gemarkeerd als `true`. Dit kan een daling in &quot;Adressable publiek&quot;metrisch in het dashboard van het vergunningsgebruik tonen en kan een daling in &quot;Aantal van het Profiel&quot;metrisch in het dashboard van het Profiel tonen, aangezien deze metriek de fragmenten van het de randattribuut van het leftover voorafgaand aan deze versie omvatte. |

{style=&quot;table-layout:auto&quot;}

Als u meer wilt weten over het realtime profiel van de klant, inclusief zelfstudies en aanbevolen procedures voor het werken met profielgegevens, leest u eerst de [Overzicht van het realtime klantprofiel](../../profile/home.md).

## Segmenteringsservice {#segmentation}

[!DNL Segmentation Service] definieert een bepaalde subset van profielen door de criteria te beschrijven die een verhandelbare groep personen binnen uw klantenbasis onderscheiden. De segmenten kunnen op verslaggegevens (zoals demografische informatie) of tijdreeksgebeurtenissen worden gebaseerd die klanteninteractie met uw merk vertegenwoordigen.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Ondersteuning voor 4000 segmenten | Alle organisaties met Platform kunnen nu tot 4000 segmentdefinities steunen. Voor meer informatie over hoe deze wijziging de segmenttaak-API&#39;s beïnvloedt, leest u de [segmenttaakeindgebruikershandleiding](../../segmentation/api/segment-jobs.md) |

Voor meer informatie over [!DNL Segmentation Service], zie de [Overzicht van segmentatie](../../segmentation/home.md).

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
