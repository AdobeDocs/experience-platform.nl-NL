---
title: Opmerkingen bij de release van Adobe Experience Platform
description: De meest recente releaseopmerkingen voor Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 37d073266bf9293ad3a9e85c193acd1e2e47fa2a
workflow-type: tm+mt
source-wordcount: '1536'
ht-degree: 1%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 25 mei 2022**

<!-- New features in Adobe Experience Platform: -->

<!-- - [Attribute-based access control](#abac) -->
<!-- - [Data hygiene](#hygiene) -->

Updates voor bestaande functies in Adobe Experience Platform:

- [Controlelogboeken](#audit-logs)
- [Dashboards](#dashbaords)
- [Gegevensverzameling](#data-collection)

<!-- - [Data Governance](#data-governance) -->
- [Gegevensprep](#data-prep)
- [Doelen](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Query-service](#query-service)
- [Bronnen](#sources)

<!-- ## Attribute-based access control {#abac}

>[!IMPORTANT]
>
>Attribute-based access control is currently available in a limited release for US-based healthcare customers. This capability will be available to all Real-time Customer Data Platform customers once it is fully released.

Attribute-based access control is a capability of Adobe Experience Platform that enables administrators to control access to specific objects and/or capabilities based on attributes. Attributes can be metadata added to an object, such as a label added to a schema field or segment. An administrator defines access policies that include attributes to manage user access permissions.

Through attribute-based access control, administrators of your organization can control users’ access to both sensitive personal data (SPD) and personally identifiable information (PII) across all Platform workflows and resources. Administrators can define user roles that have access only to specific fields and data that correspond to those fields.

| Feature | Description |
| --- | --- |
| Attribute-based access control | Attribute-based access control allows you to label Experience Data Model (XDM) schema fields with labels that define organizational or data usage scopes. In parallel, administrators can use the user and role administration interface to define access policies covering XDM schema fields and better manage the access given to users or groups of users (internal, external, or third-party users). Additionally, attribute-based access control allows administrators to manage access to specific segments. |
| Permissions | Permissions is the area of Experience Cloud where administrators can define user roles and access policies to manage access permissions for features and objects within a product application. Through Permissions, you can create and manage roles, as well as assign the desired resource permissions for these roles. Permissions also allow you to manage the labels, sandboxes, and users associated with a specific role. For more information, see the [Permissions UI guide](../../access-control/abac/ui/browse.md). |

For more information on attribute-based access control, see the [attribute-based access control overview](../../access-control/abac/overview.md). -->

<!-- ## Data hygiene {#hygiene}

Experience Platform provides a suite of data hygiene capabilities that allow you manage your stored data through programmatic deletions of consumer records and datasets. Using either the [!UICONTROL Data Hygiene] workspace in the UI or through calls to the Data Hygiene API, you can manage your data stores to ensure that information is used as expected, is updated when incorrect data needs fixing, and is deleted when organizational policies deem it necessary.

>[!IMPORTANT]
>
>Data hygiene capabilities are currently only available for organizations that have purchased the Adobe Shield for Healthcare add-on offering.

**New features**

| Feature | Description |
| --- | --- |
| Consumer deletion | [Delete consumer records](../../hygiene/ui/delete-consumer.md) from the data lake and Profile store based on primary identity data. |
| Time to live (TTL) for datasets | [Schedule TTLs](../../hygiene/ui/ttl.md) for Platform datasets.  |

For more information on audit logs in Platform, refer to the [data hygiene overview](../../hygiene/home.md). -->

## Controlelogboeken {#audit-logs}

Experience Platform staat u toe om gebruikersactiviteit voor diverse diensten en mogelijkheden te controleren. De auditlogboeken bevatten informatie over wie wat heeft gedaan en wanneer.

**Bijgewerkte functies**

| Functie | Naam | Beschrijving | | — | — | — | | Toegevoegde middelen | <ul><li> Toegangsbeheerbeleid </li><li> Rol </li><li> Controlelogboeken </li><li> Werkorder </li><li> Naamruimte identiteit </li><li> Identiteitsgrafiek </li><li> Query </li><li> Gegevensset </li><li> Gegevensstroom bron </li></ul> | Bronnen van controlelogbestanden worden automatisch opgenomen wanneer de activiteit plaatsvindt. Als de eigenschap wordt toegelaten moet u niet manueel logboekinzameling toelaten. |



Raadpleeg voor meer informatie over auditlogs in Platform de [overzicht van auditlogboeken](../../landing/governance-privacy-security/audit-logs/overview.md).

## Dashboards {#dashboards}

Adobe Experience Platform biedt meerdere dashboards waarmee u belangrijke informatie over de gegevens van uw organisatie kunt bekijken, zoals vastgelegd tijdens dagelijkse momentopnamen.

### Profieldashboards

Op het dashboard Profielen wordt een momentopname weergegeven van de kenmerkgegevens (record) die uw organisatie heeft in de profielopslag in Experience Platform.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Poortoverlapping door de widget voor samenvoegbeleid | Deze widget toont de visuele oversteekplaats van segmentdefinities en staat u toe om segmenteringsstrategie te optimaliseren door gelijkenissen tussen uw segmentdefinities te bestuderen. |
| Tendens van aantal profielen door identiteitswidget | Met deze widgets kunt u de behoeften voor doelactivering beheren door het groeipatroon van profielen aan te tonen die door de vereiste identiteit zijn gefilterd. |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over profielen raadpleegt u de [documentatie van dashboard voor profielen](../../dashboards/guides/profiles.md).

### Doeldashboards

Het bestemmingendashboard toont een momentopname van de bestemmingen die uw organisatie binnen Experience Platform heeft toegelaten.

| Functie | Beschrijving |
| --- | --- |
| Geactiveerd publiek op doelwidget | Deze widget helpt u in een oogopslag de waarde van uw bestemmingen te begrijpen op basis van het aantal geactiveerde doelgroepen. Het verleent ook gemakkelijke toegang tot meer gedetailleerde informatie over uw segmenten die aan de bestemming in kaart zijn gebracht. |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over bestemmingen raadpleegt u de [documentatie van het doeldashboard](../../dashboards/guides/destinations.md).

### Segmentdashboards

Het segmentdashboard verstrekt een gebruikersinterface waardoor u belangrijke informatie over uw segmenten kunt bekijken, zoals die tijdens een dagelijkse momentopname wordt gevangen.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Audioverlap-widget | Met deze widget kunt u uw segmentatiestrategie optimaliseren door de gelijkenissen in de resultaten van uw segmentdefinities te visualiseren. |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over segmenten raadpleegt u de [segmentdashboarddocumentatie](../../dashboards/guides/segments.md).

## Gegevensverzameling {#data-collection}

Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar het Adobe Experience Platform Edge Network kunt verzenden waar het kan worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Gegevensstromen kopiëren | [Een kopie van een bestaande gegevensstroom maken](../../edge/datastreams/overview.md#copy) en pas zo nodig de configuratie ervan aan, waarbij de noodzaak om helemaal opnieuw te beginnen wordt vermeden. |
| Gegevensstroomtoewijzingsregels importeren | Als u Gegevensvoorinstelling instelt voor gegevensverzameling, kunt u [de toewijzingsregels van een bestaande gegevensstroom importeren](../../edge/datastreams/data-prep.md#import-mapping) in plaats van elke veldtoewijzing handmatig te configureren. |
| Ondersteuning voor gegevenstoewijzing voor Mobile SDK | U kunt de Prep van Gegevens voor de Inzameling van Gegevens op gegevensstromen nu vormen voorgenomen voor gebruik met het Experience Platform Mobiele SDK. |
| Ondersteuning voor gegevenstoewijzing voor XDM-objecten | XDM-objecten naast gegevenslaagobjecten toewijzen wanneer [configureren van Data Prep voor gegevensverzameling](../../edge/datastreams/data-prep.md#select-data). |

Voor meer informatie over gegevensverzameling in Platform raadpleegt u de [overzicht van gegevensverzameling](../../collection/home.md).

<!-- ## Data Governance {#governance}

Adobe Experience Platform Data Governance is a series of strategies and technologies used to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data usage. It plays a key role within [!DNL Experience Platform] at various levels, including cataloging, data lineage, data usage labeling, data access policies, and access control on data for marketing actions.

**New features**

| Feature | Description | 
| ------- | ----------- |
| Consent policy enforcement (limited availability) | If your organization has purchased the Adobe Shield for Healthcare add-on offering, you can now [create consent policies](../../data-governance/policies/user-guide.md#consent-policy) to automatically [enforce customer consents and preferences in segment participation](../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation). |

{style="table-layout:auto"}

See the [Data Governance overview](../../data-governance/home.md) for more information on the service. -->

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om, gegevens aan en van het Model van Gegevens van de Ervaring in kaart te brengen om te zetten en te bevestigen (XDM).

**Bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Gelokaliseerde gegevensfouten | [!DNL Data Prep] lokaliseert nu alle transformatiefouten naar het kenmerkniveau (eerder op rijniveau). Dataflows krijgen nu gedeeltelijke rijen die zijn gevuld met kolommen die geen transformatiefouten hebben, in plaats van de volledige rijen te negeren. |
| Upservers streamen naar [!DNL Profile Service] | Upseringen streamen met [!DNL Data Prep] om gedeeltelijke rijupdates naar de Dienst van het Profiel te verzenden gebruikend [[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md), [[!DNL Azure Event Hubs]](../../sources/connectors/cloud-storage/eventhub.md), of [[!DNL HTTP API]](../../sources/connectors/streaming/http.md) bron. Zie de handleiding op [streaming upserts](../../data-prep/upserts.md) voor meer informatie . |

{style=&quot;table-layout:auto&quot;}

<!-- | Attribute-based access control in [!DNL Data Prep] | You will now only be able to map attributes that you have access to. Attributes that you do not have access to can not be used in pass-through mappings and calculated fields. For more information, see [attribute-based access control in [!DNL Data Prep]](../../data-prep/home.md). **Note**: Attribute-based access control is currently available in a limited release for US-based healthcare customers. This capability will be available to all Real-time Customer Data Platform customers once it is fully released. | -->

Voor meer informatie over [!DNL Data Prep], zie de [[!DNL Data Prep] overzicht](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ----------- | ----------- |
| Nieuwste profielkwalificaties exporteren [na dagelijkse segmentbeoordeling](../../destinations/ui/activate-batch-profile-destinations.md#export-full-files) | U kunt nu een volledige dossieruitvoer, één of dagelijks, met de recentste profielkwalificaties plannen, nadat de dagelijkse segmentevaluatie volledig is. |
| Optionele gegevensstroom-id voor [Adobe Target-bestemmingen](../../destinations/catalog/personalization/adobe-target-connection.md) | Om de verpersoonlijking van Adobe Target voor gebruikers toe te laten die niet het Web SDK van het Experience Platform kunnen uitvoeren, is de selectie van gegevensstroom identiteitskaart nu facultatief wanneer het vormen van de bestemmingen van Adobe Target. Als u geen gegevensstroom gebruikt, ondersteunen segmenten die van Experience Platform naar doel zijn geëxporteerd alleen de volgende-sessiepersonalisatie, terwijl randsegmentatie is uitgeschakeld, samen met alle [use cases](../../destinations/ui/configure-personalization-destinations.md) die afhankelijk zijn van randsegmentatie. |

{style=&quot;table-layout:auto&quot;}

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe XDM-componenten**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Veldgroep | [[!UICONTROL Change set]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/changeset.schema.json) | Hiermee legt u wijzigingen op rijniveau vast in en van gegevenssets. Deze veldgroep kan door elke klasse worden gebruikt. |
| Veldgroep | [[!UICONTROL Reference keys]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-reference-keys.schema.json) | Vangt verwijzingssleutels voor schema&#39;s ExperienceEvent, toestaand u om verhoudingen met schema&#39;s te bouwen die op andere klassen worden gebaseerd. |

{style=&quot;table-layout:auto&quot;}

**Bijgewerkte XDM-componenten**

| Componenttype | Naam | Beschrijving bijwerken |
| --- | --- | --- |
| Gedraging | [[!UICONTROL Time-series Schema]](https://github.com/surbhi114/xdm/blob/master/components/behaviors/time-series.schema.json) | Bijgewerkt `eventType` om verschillende nieuwe gebeurtenistypen op te nemen die betrekking hebben op media en een binnenkomend gebruik van een webkanaal voor Adobe Journey Optimizer. |
| Algemeen schema | [[!UICONTROL Destination]](https://github.com/tumulurik/xdm/blob/master/schemas/destinations/destination.schema.json) | Enumwaarden zijn verwijderd uit `xdm:destinationCategory`. |
| Veldgroep | [[!UICONTROL Record Status]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/record-status.schema.json) | Status van veldgroep bijgewerkt vanuit `experimental` tot `stable`. |
| Veldgroep | (Meerdere) | Verschillende B2B-veldgroepen zijn bijgewerkt zodat bepaalde id-velden zijn vervangen door sleuteltekstvelden die de [[!UICONTROL B2B Source]](../../xdm/data-types/b2b-source.md) gegevenstype. De vorige id-velden worden in een toekomstige update vervangen. Raadpleeg het volgende: [pull-verzoek](https://github.com/adobe/xdm/pull/1533/files#diff-720c0bb1d1cbaf622f5656c2a4b62d35830c75f6563794da72a280a6a520fbc1) voor een volledige lijst met wijzigingen in de betrokken veldgroepen. |
| Gegevenstype | [[!UICONTROL Browser details]](https://github.com/liljenback/xdm/blob/master/components/datatypes/browserdetails.schema.json) | Een nieuw veld toegevoegd `xdm:userAgentClientHints` waarmee contextafhankelijke informatie wordt vastgelegd over de interactie van de gebruikersagent met de browser. |
| Gegevenstype | [[!UICONTROL Media information]](https://github.com/lidiaist/xdm/blob/master/components/datatypes/media.schema.json) | Toegevoegde `xdm:playhead` veld om de afspeelkoptijd voor een stuk media-inhoud vast te leggen. Vaste patroonvalidatie voor `xdm:videoSegment`. |
| Gegevenstype | [[!UICONTROL Rating]](https://github.com/lidiaist/xdm/blob/master/components/datatypes/external/iptc/rating.schema.json) | `iptc4xmpExt:RatingSourceLink` is niet langer een vereist veld. |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over XDM in Platform, zie [XDM System, overzicht](../../xdm/home.md).

## Query-service {#query-service}

De Dienst van de vraag staat u toe om standaardSQL aan vraaggegevens in Adobe Experience Platform te gebruiken [!DNL data lake]. U kunt zich bij om het even welke datasets van aansluiten [!DNL data lake] en leg de vraagresultaten als nieuwe dataset voor gebruik in rapportering, de Werkruimte van de Wetenschap van Gegevens, of voor opname in het Profiel van de Klant in real time vast.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Integratie van controlelogbestand voor Query Service | De de controlelogboekintegratie van de Dienst van de Vraag verstrekt verslagen van vraag-verwante gebruikersacties voor het oplossen van problemen of naleving van het beleid van het collectieve gegevensbeheer en regelgevende vereisten. Zie de [documentatie over de integratie van auditlogbestanden](../../query-service/data-governance/audit-log-guide.md) voor uitgebreide informatie |
| ALTER TABLE SQL-constructie | Gebruik SQL om primaire identiteiten in een ad hoc dataset te plaatsen. De Dienst van de vraag staat u toe om datasetkolommen als of primaire of secundaire identiteiten direct door SQL te merken gebruikend `ALTER TABLE` gebruiken. |

{style=&quot;table-layout:auto&quot;}

<!-- For more information on data governance in Query Service, see the [data governance overview](../../query-service/data-governance/overview.md). -->

Voor meer informatie over de mogelijkheden van de Dienst van de Vraag, zie [Overzicht van Query Service](../../query-service/home.md)

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

| Functie | Beschrijving |
| --- | --- |
| Bètaversie van [!DNL Zendesk] bron | Gebruik de [!DNL Zendesk] bron om gebruiker, agent, en organisatiegegevens van uw in te voeren [!DNL Zendesk] instantie voor [!DNL Profile] verrijking. Zie de [[!DNL Zendesk] bronoverzicht](../../sources/connectors/customer-success/zendesk.md) voor meer informatie . |
| Ondersteuning voor gegevensverzameling Adobe | Gebruik de broncatalogus om tot uw gegevens van de Rand van de Ervaring van de Inzameling van Gegevens, met inbegrip van Prep van Gegevens voor de Inzameling van Gegevens en betere steun voor gegevenswaarschuwingen van Prep van Gegevens toegang te hebben. Zie de [Overzicht van de bron van Adobe-gegevensverzameling](../../sources/connectors/adobe-applications/data-collection.md) voor meer informatie . |
| Ondersteuning voor het opnemen van bestanden met `ISO-8859-1` coderen | Gebruik de `encoding` parameter voor opnemen `ISO-8859-1` Gecodeerde bestanden met een bron voor cloudopslag die met de [!DNL Flow Service] API. Zie de handleiding op [maken van een bronverbinding voor cloudopslag](../../sources/tutorials/api/collect/cloud-storage.md) voor meer informatie . |

{style=&quot;table-layout:auto&quot;}

<!-- | Attribute-based access control in sources | You can now manage and control access to individual source fields and attributes during ingestion. **Note**: Attribute-based access control is currently available in a limited release for US-based healthcare customers. This capability will be available to all Real-time Customer Data Platform customers once it is fully released.  | -->

Zie voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).
