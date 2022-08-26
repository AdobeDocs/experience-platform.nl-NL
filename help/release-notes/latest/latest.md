---
title: Opmerkingen bij de release van Adobe Experience Platform
description: De meest recente releaseopmerkingen voor Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: f2d2499147b40a15a413773068b65139278bd4ff
workflow-type: tm+mt
source-wordcount: '2044'
ht-degree: 1%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 24 augustus 2022**

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Klantprofiel in realtime](#profile)
- [Segmenteringsservice](#segmentation)
- [Bronnen](#sources)

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

Met AI/ML-services kunnen marketinganalisten en praktijkmensen gebruikmaken van de kracht van kunstmatige intelligentie en het leren van machines in gebruiksgevallen voor de klant. Dit staat voor marketing analisten toe om modellen op te zetten specifiek voor de behoeften van een bedrijf gebruikend zaken-vlakke configuraties zonder de behoefte aan de deskundigheid van de gegevenswetenschap.

### Attribution AI

Attribution AI wordt gebruikt om credits toe te wijzen aan aanraakpunten die leiden tot conversiegebeurtenissen. Dit kan door marketers worden gebruikt om het marketing effect van elk individueel marketing aanraakpunt over klantenreizen te kwantificeren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Ondersteuning voor privacy | <ul><li>Attribution AI ondersteunt nu het definiëren van gebruikersrollen en het te beheren toegangsbeleid [machtigingen](../../../help/access-control/abac/ui/permissions.md) voor functies en objecten in een producttoepassing.</li><li>De middelen van het logboek van de controle worden geregistreerd automatisch aangezien de activiteit voorkomt.</li><li>Doorheen [attribuut-based toegangsbeheer](../../../help/access-control/abac/overview.md)kunnen beheerders de toegang tot specifieke objecten en/of mogelijkheden beheren op basis van bepaalde kenmerken. Dit kunnen metagegevens zijn die aan een object worden toegevoegd, zoals labels. Beheerders kunnen ook gebruikersrollen definiëren die alleen toegang hebben tot specifieke velden en gegevens die overeenkomen met die velden.</li><li>Attribution AI gebruikt Platform datasets. Om de naleving van GDPR te vergemakkelijken, kunt u Adobe Experience Platform Privacy Service aan opstellingsprotocollen gebruiken om klantenverzoeken tot toegang en schrapping van hun gegevens over het datumpeer, de Dienst van de Identiteit, en het Profiel van de Klant in real time te respecteren. Alle gegevens worden in doorvoer en in rust versleuteld.</li></ul> |

{style=&quot;table-layout:auto&quot;}

**Opmerking**: Attribution AI zal niet beschikbaar zijn bij bestaande klanten van het gezondheidsschild of het privacyschild tot nader order.

Zie voor meer informatie over Attribution AI de [Attribution AI](../../intelligent-services/attribution-ai/overview.md) overzicht.

### Customer AI

De in Real-time Customer Data Platform beschikbare AI van de klant wordt gebruikt om aangepaste eigenschapscores zoals kurn en conversie voor individuele profielen op schaal te produceren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Ondersteuning voor privacy | <ul><li>De AI van de Klant steunt nu het bepalen van gebruikersrollen en toegangsbeleid om te leiden [machtigingen](../../../help/access-control/abac/ui/permissions.md) voor functies en objecten in een producttoepassing.</li><li>De middelen van het logboek van de controle worden geregistreerd automatisch aangezien de activiteit voorkomt.</li><li> Doorheen [attribuut-based toegangsbeheer](../../access-control/abac/overview.md)kunnen beheerders de toegang tot specifieke objecten en/of mogelijkheden beheren op basis van bepaalde kenmerken. Deze kenmerken kunnen metagegevens zijn die aan een object worden toegevoegd, zoals labels. Beheerders kunnen ook gebruikersrollen definiëren die alleen toegang hebben tot specifieke velden en gegevens die overeenkomen met die velden.</li><li>Klant-AI maakt gebruik van gegevenssets van Platforms. Om de naleving van GDPR te vergemakkelijken, kunt u Adobe Experience Platform Privacy Service aan opstellingsprotocollen gebruiken om klantenverzoeken tot toegang en schrapping van hun gegevens over het datumpeer, de Dienst van de Identiteit, en het Profiel van de Klant in real time te respecteren. Alle gegevens worden in doorvoer en in rust versleuteld.</li></ul> |

{style=&quot;table-layout:auto&quot;}

**Opmerking**: Klanten van AI zijn tot nader order niet bij bestaande klanten van het gezondheidsschild of het privacyschild beschikbaar.

Voor meer informatie over AI van de Klant, gelieve te zien [Customer AI](../../intelligent-services/customer-ai/overview.md) overzicht.

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform biedt meerdere [!DNL dashboards] waardoor u belangrijke inzichten over de gegevens van uw organisatie kunt bekijken, zoals die tijdens dagelijkse momentopnamen worden gevangen.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Geplande activeringswidget | De [!UICONTROL Scheduled activations] widget biedt een tabellarische weergave van de laatst geactiveerde doelen. Voor elk segment bevat dit de naam, het doelplatform en de begin- en einddatum van de activering. Met deze widget kunt u in één oogopslag zien waar en wanneer het publiek wordt geactiveerd en kunt u dubbele of overbodige activeringen transparanter maken. Deze geaccumuleerde informatie benadrukt ook waar om het even welke activiteiten zijn weggelaten. |

Voor meer informatie over [!DNL Dashboards], zie de [[!DNL Dashboards] overzicht](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om, gegevens aan en van het Model van Gegevens van de Ervaring in kaart te brengen om te zetten en te bevestigen (XDM).

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor het opnemen van records met waarschuwingen | Met Data Prep worden nu waarschuwingen (niet-kritieke fouten) gelokaliseerd voor de velden en kan de rest van de rij worden ingevoegd. Alle maptransformatiefouten worden nu gerapporteerd als waarschuwingen en rijen die gedeeltelijk worden ingepakt, worden als geslaagd beschouwd, met een waarschuwing.  De bewaking wordt ook ondersteund in registers met waarschuwingen en diagnostische details. Gedeeltelijke invoer van records met waarschuwingen is momenteel alleen beschikbaar voor streaming gegevens. Raadpleeg de documentatie over [opnemen, records met waarschuwingen](../../sources/tutorials/ui/monitor-streaming.md) voor meer informatie . |

{style=&quot;table-layout:auto&quot;}

Meer informatie over [!DNL Data Prep], zie de [[!DNL Data Prep] overzicht](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ----------- | ----------- |
| (Bèta) Op attributen-gebaseerde verpersoonlijkingssteun voor verpersoonlijkingsbestemmingen | Met de bètaversie van op attribuut-gebaseerde verpersoonlijking, zult u twee nieuwe kaarten in zien [doelcatalogus](../../destinations/catalog/overview.md): <ul><li>**[!UICONTROL Adobe Target V2]**: Deze connector is momenteel in bèta beschikbaar voor een beperkt aantal klanten. Naast de functionaliteit van de Adobe Target V1-kaart voegt de Target V2-connector een [toewijzingsstap](/help/destinations/ui/activate-profile-request-destinations.md#map-attributes) aan de activeringswerkstroom, waarmee u profielkenmerken kunt toewijzen aan Adobe Target, waardoor op kenmerken gebaseerde personalisatie op dezelfde pagina en op een volgende pagina mogelijk is.</li><li>**[!UICONTROL Custom Personalization With Attributes]**: Deze connector is momenteel in bèta beschikbaar voor een beperkt aantal klanten. Naast de door de **[!UICONTROL Custom Personalization]** de **[!UICONTROL Custom Personalization With Attributes]** connector voegt een optionele [toewijzingsstap](../../destinations/ui/activate-profile-request-destinations.md#map-attributes) aan de activeringswerkstroom, die u toestaat om profielattributen aan uw douanebestemming van de douaneverpersoonlijking in kaart te brengen, toelatend op attribuut-gebaseerde zelfde-pagina en volgende-pagina verpersoonlijking.</li></ul> <br> Profielkenmerken kunnen vertrouwelijke gegevens bevatten. Om deze gegevens te beschermen, **[!UICONTROL Custom Personalization With Attributes]** doel vereist dat u de [Edge Network Server-API](../../server-api/overview.md) voor gegevensverzameling. Bovendien moeten alle API-aanroepen van de server worden uitgevoerd in een [geverifieerde context](../../server-api/authentication.md). |

{style=&quot;table-layout:auto&quot;}

**Nieuwe bestemmingen**

| Bestemming | Beschrijving |
| ----------- | ----------- |
| [[!DNL Outreach]](../..//destinations/catalog/crm/outreach.md) | [[!DNL Outreach]](https://www.outreach.io/) is een Platform van de Uitvoering van de Verkoop met de meeste B2B koper-verkoper interactiegegevens in de wereld en significante investeringen in merkgebonden AI technologieën om verkoopgegevens in intelligentie om te zetten. [!DNL Outreach] helpt organisaties hun verkoopbetrokkenheid te automatiseren en op inkomstenintelligentie te handelen om hun efficiency, voorspelbaarheid, en groei te verbeteren. |

{style=&quot;table-layout:auto&quot;}

Voor meer algemene informatie over bestemmingen raadpleegt u de [Overzicht van doelen](../../destinations/home.md).

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
| Harde limiet voor beleid samenvoegen | Platform zal nu een harde limiet opleggen aan **vijf** samenvoegbeleid per sandbox. Als uw sandbox momenteel meer dan vijf samenvoegbeleidsregels heeft, **niet** kan nieuw samenvoegbeleid maken totdat de sandbox minder dan vijf samenvoegbeleidsregels heeft. |
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

{style=&quot;table-layout:auto&quot;}

Zie voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).