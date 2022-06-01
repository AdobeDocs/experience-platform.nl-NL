---
title: Opmerkingen bij de release van Adobe Experience Platform
description: De meest recente releaseopmerkingen voor Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 1dc97fa33fa8cb46184e11d311ef8246199b4f03
workflow-type: tm+mt
source-wordcount: '2389'
ht-degree: 2%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 25 mei 2022**

Nieuwe functies in Adobe Experience Platform:

- [Op kenmerken gebaseerd toegangsbeheer](#abac)
- [Gegevenshygiëne](#hygiene)

Updates voor bestaande functies in Adobe Experience Platform:

- [Waarschuwingen](#alerts)
- [Controlelogboeken](#audit-logs)
- [Dashboards](#dashbaords)
- [Gegevensverzameling](#data-collection)
- [Data Governance](#data-governance)
- [Gegevensprep](#data-prep)
- [Doelen](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Query-service](#query-service)
- [Bronnen](#sources)

## Op kenmerken gebaseerd toegangsbeheer {#abac}

>[!IMPORTANT]
>
>Op attributen-gebaseerde toegangscontrole is momenteel beschikbaar in een beperkte versie voor op VS-Gebaseerde gezondheidszorgklanten. Deze mogelijkheid is beschikbaar voor alle Real-time Customer Data Platform-klanten zodra deze volledig is vrijgegeven.

Toegangsbeheer op basis van kenmerken is een mogelijkheid van Adobe Experience Platform waarmee beheerders de toegang tot specifieke objecten en/of mogelijkheden kunnen beheren op basis van kenmerken. Kenmerken kunnen metagegevens zijn die aan een object worden toegevoegd, zoals een label dat aan een schemaveld of -segment wordt toegevoegd. Een beheerder bepaalt toegangsbeleid dat attributen omvat om de toestemmingen van de gebruikerstoegang te beheren.

Via attribuut-gebaseerde toegangscontrole, kunnen de beheerders van uw organisatie gebruikers&#39; toegang tot zowel gevoelige persoonlijke gegevens (SPD) als persoonlijk identificeerbare informatie (PII) over alle werkschema&#39;s en middelen van het Platform controleren. Beheerders kunnen gebruikersrollen definiëren die alleen toegang hebben tot specifieke velden en gegevens die overeenkomen met die velden.

| Functie | Beschrijving |
| --- | --- |
| Op kenmerken gebaseerd toegangsbeheer | Op attribuut-gebaseerde toegangscontrole staat u toe om het schemagebieden van de Gegevens van de Ervaring te etiketteren Model (XDM) met etiketten die organisatie of gegevensgebruikswerkingsgebied bepalen. Tegelijkertijd kunnen beheerders de gebruikers- en rolbeheerinterface gebruiken om toegangsbeleid te definiëren dat XDM-schemavelden bestrijkt en om de toegang die aan gebruikers of groepen gebruikers wordt gegeven (interne, externe of externe gebruikers) beter te beheren. Bovendien, op attribuut-gebaseerde toegangsbeheer staat beheerders toe om toegang tot specifieke segmenten te beheren. Zie voor meer informatie de [op attributen-gebaseerd toegangsbeheeroverzicht](../../access-control/abac/overview.md). |
| Toestemmingen | De toestemmingen zijn het gebied van Experience Cloud waar de beheerders gebruikersrollen en toegangsbeleid kunnen bepalen om toegangstoestemmingen voor eigenschappen en voorwerpen binnen een producttoepassing te beheren. Door Toestemmingen, kunt u rollen tot stand brengen en beheren, evenals de gewenste middeltoestemmingen voor deze rollen toewijzen. Met machtigingen kunt u ook de labels, sandboxen en gebruikers beheren die aan een specifieke rol zijn gekoppeld. Zie voor meer informatie de [Handleiding voor machtigingen-UI](../../access-control/abac/ui/browse.md). |

Voor meer informatie over op attribuut-gebaseerde toegangsbeheer, zie [op attributen-gebaseerd toegangsbeheeroverzicht](../../access-control/abac/overview.md).

## Gegevenshygiëne {#hygiene}

Experience Platform biedt een reeks mogelijkheden voor gegevenshygiëne waarmee u uw opgeslagen gegevens kunt beheren via programmatische verwijderingen van consumentengegevens en gegevenssets. Het gebruiken van of [!UICONTROL Data Hygiene] De werkruimte in UI of door vraag aan de Hygiene API van Gegevens, kunt u uw gegevensopslag beheren om ervoor te zorgen dat de informatie zoals verwacht wordt gebruikt, wordt bijgewerkt wanneer de onjuiste gegevensbehoeften het bevestigen, en wordt geschrapt wanneer het organisatorische beleid het noodzakelijk acht.

>[!IMPORTANT]
>
>De mogelijkheden voor gegevenshygiëne zijn momenteel alleen beschikbaar voor organisaties die de Adobe Shield for Healthcare-add-on hebben aangeschaft.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Tijd om te leven (TTL) voor datasets | [TTL&#39;s plannen](../../hygiene/ui/ttl.md) voor gegevensbestanden voor Platforms. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg voor meer informatie over auditlogs in Platform de [overzicht van de gegevenshygiëne](../../hygiene/home.md).

## Waarschuwingen {#alerts}

Met Experience Platform kunt u zich abonneren op waarschuwingen op basis van gebeurtenissen voor verschillende activiteiten van Platforms. U kunt zich abonneren op verschillende waarschuwingsregels via de [!UICONTROL Alerts] in de gebruikersinterface van het Platform en kan ervoor kiezen waarschuwingsberichten te ontvangen binnen de gebruikersinterface zelf of via e-mailberichten.

**Bijgewerkte functies**

| Functie | Alarmregel | Beschrijving |
| --- | --- | --- |
| Nieuwe waarschuwingsregel | Het percentage kippingen overschrijdt de drempel | U kunt de waarschuwing nu gebruiken om meldingen te ontvangen wanneer de gegevensstroom van uw bronnen de drempelwaarden voor identiteiten overschrijdt. Zie het overzicht op [waarschuwingsregels](../../observability/alerts/rules.md) voor de bijgewerkte lijst met waarschuwingstypen. |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over waarschuwingen raadpleegt u de [[!DNL Observability Insights] overzicht](../../observability/home.md).

## Controlelogboeken {#audit-logs}

Experience Platform staat u toe om gebruikersactiviteit voor diverse diensten en mogelijkheden te controleren. De auditlogboeken bevatten informatie over wie wat heeft gedaan en wanneer.

**Bijgewerkte functies**

| Functie | Naam | Beschrijving |
| --- | --- | --- |
| Toegevoegde bronnen | <ul><li> Toegangsbeheerbeleid </li><li> Rol </li><li> Controlelogboeken </li><li> Werkorder </li><li> Naamruimte identiteit </li><li> Identiteitsgrafiek </li><li> Query </li><li> Gegevensset </li><li> Gegevensstroom bron </li></ul> | De middelen van het logboek van de controle worden geregistreerd automatisch aangezien de activiteit voorkomt. Als de eigenschap wordt toegelaten moet u niet manueel logboekinzameling toelaten. |

{style=&quot;table-layout:auto&quot;}

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
| Integratie met gegevensstromen | Gebruik de broncatalogus in Platform om tot uw gegevens op het Netwerk van de Rand van het Platform, met inbegrip van Prep van Gegevens voor de Inzameling van Gegevens en betere steun voor de waarschuwingen van de Prep van Gegevens toegang te hebben. Zie de [Overzicht van de bron van Adobe-gegevensverzameling](../../sources/connectors/adobe-applications/data-collection.md) voor meer informatie . |

Voor meer informatie over gegevensverzameling in Platform raadpleegt u de [overzicht van gegevensverzameling](../../collection/home.md).

## Gegevensbeheer {#governance}

Adobe Experience Platform Data Governance is een reeks strategieën en technologieën die worden gebruikt om klantgegevens te beheren en naleving van regelgeving, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik te waarborgen. Het speelt een sleutelrol binnen [!DNL Experience Platform] op verschillende niveaus, waaronder catalogisering, gegevenskoppeling, etikettering van het gegevensgebruik, beleid inzake gegevenstoegang en toegangscontrole voor marketingacties.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Toestemming voor beleidshandhaving (beperkte beschikbaarheid) | Als uw organisatie de add-on Adobe Shield for Healthcare-service heeft aangeschaft, kunt u nu [beleid voor instemming maken](../../data-governance/policies/user-guide.md#consent-policy) automatisch [klanttoestemmingen en voorkeuren in segmentdeelname afdwingen](../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation). |

{style=&quot;table-layout:auto&quot;}

Zie de [Overzicht van gegevensbeheer](../../data-governance/home.md) voor meer informatie over de dienst.

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om, gegevens aan en van het Model van Gegevens van de Ervaring in kaart te brengen om te zetten en te bevestigen (XDM).

**Bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Op kenmerken gebaseerd toegangsbeheer in [!DNL Data Prep] | U kunt nu alleen kenmerken toewijzen waartoe u toegang hebt. Kenmerken waartoe u geen toegang hebt, kunnen niet worden gebruikt in doorvoertoewijzingen en berekende velden. Zie voor meer informatie [attribuut-based toegangsbeheer in [!DNL Data Prep]](../../data-prep/home.md). **Opmerking**: Op attributen-gebaseerde toegangscontrole is momenteel beschikbaar in een beperkte versie voor op VS-Gebaseerde gezondheidszorgklanten. Deze mogelijkheid is beschikbaar voor alle Real-time Customer Data Platform-klanten zodra deze volledig is vrijgegeven. |
| Gelokaliseerde gegevensfouten | [!DNL Data Prep] lokaliseert nu alle transformatiefouten naar het kenmerkniveau (eerder op rijniveau). Dataflows krijgen nu gedeeltelijke rijen die zijn gevuld met kolommen die geen transformatiefouten hebben, in plaats van de volledige rijen te negeren. |
| Upservers streamen naar [!DNL Profile Service] | Upseringen streamen met [!DNL Data Prep] om gedeeltelijke rijupdates naar de Dienst van het Profiel te verzenden gebruikend [[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md), [[!DNL Azure Event Hubs]](../../sources/connectors/cloud-storage/eventhub.md), of [[!DNL HTTP API]](../../sources/connectors/streaming/http.md) bron. Zie de handleiding op [streaming upserts](../../data-prep/upserts.md) voor meer informatie . |

{style=&quot;table-layout:auto&quot;}

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

Voor meer informatie over de mogelijkheden van de Dienst van de Vraag, zie [Overzicht van Query Service](../../query-service/home.md)

<!--For more information on data governance in Query Service, see the [data governance overview](../../query-service/data-governance/overview.md).-->

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

| Functie | Beschrijving |
| --- | --- |
| Op kenmerken gebaseerd toegangsbeheer in bronnen | U kunt de toegang tot afzonderlijke bronvelden en -kenmerken nu beheren en beheren tijdens het opnemen. **Opmerking**: Op attributen-gebaseerde toegangscontrole is momenteel beschikbaar in een beperkte versie voor op VS-Gebaseerde gezondheidszorgklanten. Deze mogelijkheid is beschikbaar voor alle Real-time Customer Data Platform-klanten zodra deze volledig is vrijgegeven. |
| Bètaversie van [!DNL Zendesk] bron | Gebruik de [!DNL Zendesk] bron om gebruiker, agent, en organisatiegegevens van uw in te voeren [!DNL Zendesk] instantie voor [!DNL Profile] verrijking. Zie de [[!DNL Zendesk] bronoverzicht](../../sources/connectors/customer-success/zendesk.md) voor meer informatie . |
| Algemene beschikbaarheid van B2B [!DNL Microsoft Dynamics] bron | U kunt nu de opdracht [!DNL Microsoft Dynamics] bron om B2B-objecten zoals accounts, mogelijkheden, campagnes, marketinglijsten en leden van marketinglijsten in te voeren. Zie de [[!DNL Microsoft Dynamics] bronoverzicht](../../sources/connectors/crm/ms-dynamics.md) voor meer informatie . |
| Ondersteuning voor gegevensverzameling Adobe | Gebruik de broncatalogus in Platform om tot uw gegevens op het Netwerk van de Rand van het Platform, met inbegrip van Prep van Gegevens voor de Inzameling van Gegevens en betere steun voor de waarschuwingen van de Prep van Gegevens toegang te hebben. Zie de [Overzicht van de bron van Adobe-gegevensverzameling](../../sources/connectors/adobe-applications/data-collection.md) voor meer informatie . |
| Ondersteuning voor het opnemen van bestanden met `ISO-8859-1` coderen | Gebruik de `encoding` parameter voor opnemen `ISO-8859-1` Gecodeerde bestanden met een bron voor cloudopslag die met de [!DNL Flow Service] API. Zie de handleiding op [maken van een bronverbinding voor cloudopslag](../../sources/tutorials/api/collect/cloud-storage.md) voor meer informatie . |

{style=&quot;table-layout:auto&quot;}

Zie voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).
