---
title: Aanvullende informatie van maart 2022 voor Adobe Experience Platform
description: Aanvullende informatie van maart 2022 voor Adobe Experience Platform.
exl-id: 0d499aa6-e25d-4d34-ad32-5e4ab361cba1
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '1182'
ht-degree: 14%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum:donderdag 30 maart 2022**

Nieuwe functies in Adobe Experience Platform:

- [Controlelogboeken](#audit-logs)
- [Verwante accounts in Real-Time CDP B2B edition](#related-accounts)

Updates voor bestaande functies in Adobe Experience Platform:

- [Waarschuwingen](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [Dataverzameling](#data-collection)
- [[!DNL Query Service]](#query-service)
- [Bronnen](#sources)

## Auditlogboeken {#audit-logs}

Met Experience Platform kunt u gebruikersactiviteiten controleren op verschillende services en mogelijkheden. De auditlogboeken bevatten informatie over wie wat heeft gedaan en wanneer.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Auditlogboeken voor Dataset, Schema, Klasse, Veldgroep, Gegevenstype, Sandbox, Doel, Segment, Samenvoegen, Beleid, Berekende kenmerken, Productprofiel en Account (Adobe) | Dit zijn de middelen die door auditlogboeken worden geregistreerd. Als de eigenschap wordt toegelaten, zullen de controlelogboeken automatisch worden verzameld aangezien de activiteit voorkomt. U te hoeven niet om logboekinzameling manueel toe te laten. |
| Controleverslagen exporteren | De controlelogboeken kunnen als `CSV` of `JSON` dossier worden gedownload. De gegenereerde bestanden worden rechtstreeks op uw computer opgeslagen. |

{style="table-layout:auto"}

Voor meer informatie over controlelogboeken in Experience Platform, verwijs naar het [ overzicht van controlelogboeken ](../../landing/governance-privacy-security/audit-logs/overview.md).

## Verwante accounts in Real-Time CDP B2B edition {#related-accounts}

>[!NOTE]
>
>De functie Verwante accounts is alleen beschikbaar voor klanten van de Real-Time CDP B2B edition.

B2B-ondernemingen hebben vaak hun klantgegevens opgeslagen in meerdere systemen, elk met inbegrip van slechts gedeeltelijke of zelfs conflicterende gegevens voor dezelfde reële bedrijfsentiteit. Dit zorgt voor een enorme uitdaging om tot een accuraat beeld van hun klanten te komen, waardoor de efficiëntie en effectiviteit van hun B2B-marketing- en -verkoopinspanningen afnemen. Met de release van verwante accounts geeft [!DNL Real-Time CDP B2B] nu een lijst weer met accounts die lijken op de account waarin u bladert. U kunt de verwante rekeningen in uw segmentdefinities omvatten om uw bereik uit te breiden of bredere criteria in uw segmenten toe te passen.

Meer informatie over de functie vindt u op de volgende documentatiepagina&#39;s:

- [Overzicht van verwante accounts in Real-Time CDP B2B edition](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [Het tabblad Verwante accounts in de gebruikersinterface voor het accountprofiel](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [Hoe verwant rekeningen in segmentdefinities gebruiken](../../rtcdp/segmentation/b2b.md#related-accounts)

Meer over Real-Time CDP B2B edition leren, zie het [ overzicht ](../../rtcdp/overview.md).

## Waarschuwingen {#alerts}

Met Experience Platform kunt u zich aanmelden voor gebeurtenisgebaseerde waarschuwingen voor verschillende Experience Platform-activiteiten. U kunt zich aanmelden voor verschillende waarschuwingsregels via het tabblad [!UICONTROL Alerts] in de gebruikersinterface van Experience Platform, en u kunt ervoor kiezen waarschuwingsmeldingen te ontvangen in de gebruikersinterface zelf of via e-mailberichten.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe waarschuwingsregels | Er zijn nu twee nieuwe waarschuwingsregels beschikbaar voor bronnen die te maken hebben met gegevensinvoer. Zie het overzicht op [ waakzame regels ](../../observability/alerts/rules.md) voor de bijgewerkte lijst van waakzame types. |

{style="table-layout:auto"}

Voor meer informatie over alarm in Experience Platform, verwijs naar het [ alarm overzicht ](../../observability/alerts/overview.md).

## Dashboards {#dashboards}

Adobe Experience Platform biedt meerdere [!DNL dashboards] waarmee u belangrijke informatie over de gegevens van uw organisatie kunt bekijken, zoals die tijdens dagelijkse momentopnamen zijn vastgelegd.

### Profieldashboards

Op het dashboard Profielen wordt een momentopname weergegeven van de kenmerkgegevens (record) die uw organisatie heeft in de profielopslag in Experience Platform.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Widget niet-gesegmenteerde profielen | De widget geeft het totale aantal profielen weer dat niet aan een segment is gekoppeld. Het gegenereerde nummer is nauwkeurig vanaf de laatste momentopname en biedt de mogelijkheid om het profiel in uw organisatie te activeren. Zie de [ documentatie van profielen standaard widgets ](../../dashboards/guides/profiles.md#standard-widgets) voor meer informatie. |
| Trend-widget voor niet-gesegmenteerde profielen | Deze widget verschaft een lijngrafiekillustratie voor het aantal profielen dat gedurende een bepaalde tijdsperiode niet aan een segment is gekoppeld. De trend kan worden weergegeven over perioden van 30 dagen, 90 dagen en 12 maanden. Zie de [ documentatie van profielen standaard widgets ](../../dashboards/guides/profiles.md#standard-widgets) voor meer informatie. |
| Gesegmenteerde profielen opheffen op identiteitswidget | Deze widget categoriseert het totale aantal niet-gesegmenteerde profielen op basis van hun unieke id. De gegevens worden weergegeven in een staafdiagram. Zie de [ documentatie van profielen standaard widgets ](../../dashboards/guides/profiles.md#standard-widgets) voor meer informatie. |
| Widget enkele identiteitsprofielen | Deze widget bevat een telling van de profielen van uw organisatie die slechts één type id hebben dat tot hun identiteit leidt, of een e-mail of ECID. Zie de [ documentatie van profielen standaard widgets ](../../dashboards/guides/profiles.md#standard-widgets) voor meer informatie. |

{style="table-layout:auto"}

Voor meer informatie over de dashboards van Profielen, verwijs naar het [ overzicht van de dashboards van Profielen ](../../dashboards/guides/profiles.md).

### Doeldashboards

Op het dashboard Doelen wordt een momentopname weergegeven van de doelen die uw organisatie binnen Experience Platform heeft ingeschakeld.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Widget aantal doelen | De widget geeft het totale aantal beschikbare eindpunten weer waarop een publiek kan worden geactiveerd en geleverd binnen het systeem. Dit aantal omvat zowel actieve als inactieve bestemmingen. Zie de [ documentatie van de bestemmingsstandaard widget ](../../dashboards/guides/destinations.md#standard-widgets) voor meer informatie. |

{style="table-layout:auto"}

Voor meer informatie over dashboards van Doelen in Experience Platform, verwijs naar het [ overzicht van dashboards van Doelen ](../../dashboards/guides/destinations.md).

## Dataverzameling {#data-collection}

Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen op de client kunt verzamelen en naar de Adobe Experience Platform Edge Network kunt sturen waar deze kunnen worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Algemene gegevensstroominstellingen | U kunt nu verschillende nieuwe algemene instellingen configureren tijdens het configureren van een gegevensstroom: geo-locatie, cookie van eerste-partijid en synchronisatie van externe id&#39;s. Zie de sectie op [ vormend een datastream ](../../datastreams/overview.md#create) in de gids UI van Gegevensstromen voor meer informatie. |
| [ Edge Network API ](https://developer.adobe.com/data-collection-apis/docs/getting-started/) | Met de Edge Network API kunnen klanten met de Experience Platform Edge Network communiceren via een nieuw, geverifieerd eindpunt, zodat ze een groot aantal verschillende gebruiksgevallen voor gegevensverzameling, personalisatie, reclame en marketing kunnen aansturen. |

Voor meer informatie over gegevensinzameling in Experience Platform, te zien gelieve het [ overzicht van de gegevensinzameling ](../../collection/home.md).

## Query-service {#query-service}

Met [!DNL Query Service] kunt u standaard-SQL gebruiken om query&#39;s uit te voeren op gegevens in Adobe Experience Platform [!DNL Data Lake] . U kunt willekeurige datasets van [!DNL Data Lake] combineren en de queryresultaten vastleggen als nieuwe dataset voor gebruik in rapportage, de werkruimte voor datawetenschappen, of voor opname in het Real-Time Customer Profile.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| `table_exists` | De nieuwe eigenschapbevel wordt gebruikt om te bevestigen of een lijst momenteel in het systeem bestaat of niet. Het bevel keert een booleaanse waarde terug: `true` als de lijst **&#x200B;**&#x200B;bestaat, en `false` als de lijst **niet** bestaat. Zie de [ SQL syntaxisdocumentatie ](../../query-service/sql/syntax.md) voor meer informatie. |

{style="table-layout:auto"}

Voor meer informatie over beschikbare eigenschappen, verwijs naar het [ overzicht van de Dienst van de Vraag ](../../query-service/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens opnemen uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor inname looppas te plaatsen, en gegevensopname door te beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe bronnen nu beschikbaar voor B2B-gebruik | U kunt nu alle beschikbare bronnen op Experience Platform voor B2B-gebruiksgevallen gebruiken. Zie de [ broncatalogus ](../../sources/home.md) voor een volledige lijst van beschikbare bronnen. |
| Algemene beschikbaarheid van nieuwe [!DNL Oracle Eloqua] bron | U kunt nu de [!DNL Oracle Eloqua] -bron gebruiken om naadloos gegevens in te voeren van uw [!DNL Oracle Eloqua] -instantie (account, campagne, contactpersonen) naar Experience Platform. Zie de documentatie bij [ het creëren van een  [!DNL Oracle Eloqua]  bronverbinding ](../../sources/connectors/marketing-automation/oracle-eloqua.md) voor meer informatie. |
| API-verbeteringen voor [!DNL Data Landing Zone] | De bron [!DNL Data Landing Zone] ondersteunt nu automatische detectie van bestandseigenschappen bij gebruik van de API van [!DNL Flow Service] . Zie de documentatie bij [ het creëren van a  [!DNL Data Landing Zone]  bronverbinding ](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) voor meer informatie. |

{style="table-layout:auto"}

Meer over bronnen leren, zie het [ overzicht van bronnen ](../../sources/home.md).
