---
title: Opmerkingen bij de release van Adobe Experience Platform, maart 2020
description: Aanvullende informatie van maart 2020 voor Adobe Experience Platform.
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: opmerkingen bij de release;
exl-id: 407c2bac-4c8a-4939-b3dd-788250f15650
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 3%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: donderdag 11 maart 2020**

Updates voor bestaande functies in Adobe Experience Platform:

* [Gegevensbeheer](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## Gegevensbeheer {#governance}

[!DNL Experience Platform] stelt bedrijven in staat gegevens van meerdere bedrijfssystemen samen te brengen, zodat marketers klanten beter kunnen identificeren, begrijpen en betrekken. [!DNL Experience Platform] bevat een end-to-end infrastructuur voor gegevensbeheer die ervoor zorgt dat gegevens binnen [!DNL Platform] correct worden gebruikt en dat gegevens tussen systemen worden gedeeld.

Adobe Experience Platform Data Governance is een reeks strategieën en technologieën die worden gebruikt om klantgegevens te beheren en naleving van regelgeving, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik te waarborgen. De klasse speelt binnen [!DNL Experience Platform] op diverse niveaus een sleutelrol, zoals catalogisering, gegevenskoppeling, labels voor gegevensgebruik, beleid voor gegevenstoegang en toegangsbeheer voor marketingacties.

**Nieuwe eigenschappen**

>[!NOTE]
>
>Enkele van de volgende nieuwe functies zijn momenteel in bèta beschikbaar en niet voor alle gebruikers. Beta-functies kunnen worden gewijzigd.

| Functie | Beschrijving |
| ------- | ----------- |
| Geautomatiseerde handhaving van beleid voor gegevensgebruik voor [!DNL Real-Time Customer Data Platform] | Het beleid van het gegevensgebruik wordt nu afgedwongen in het werkschema van het activeren van gegevens aan bestemmingen. Het Beleid van gegevens wordt ook ingebed en afgedwongen wanneer het aanbrengen van veranderingen die bestaande activeringen (zoals veranderingen in datasetetiketten, fusiebeleid, segmentdefinities, en anderen) beïnvloeden. |
| Gegevenslijn voor handhaving | Wanneer een beleid van het gegevensgebruik in Real-Time CDP wordt geschonden, toont UI een bericht dat de informatie van de gegevenslijn bevat om de gebruiker te helpen begrijpen waarom het beleid werd geschonden en wat zij kunnen doen om de schending op te lossen. |


**Bekende kwesties**

* Geen

Voor meer informatie over het Beleid van Gegevens, zie het [ overzicht van het Beleid van Gegevens ](../../data-governance/home.md).

## Gegevensopname {#ingestion}

Adobe Experience Platform biedt een uitgebreide reeks functies voor het invoeren van elk type en elke vertraging van gegevens. Adobe Experience Platform [!DNL Data Ingestion] biedt meerdere alternatieven voor het opnemen van gegevens, zoals batch-API&#39;s, streaming API&#39;s, native Adobe-connectors, partners voor gegevensintegratie of de Adobe Experience Platform-interface.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
|------- | -----------|
| Gedeeltelijke batch ingestie | Gedeeltelijke batch-opname is de mogelijkheid om gegevens met fouten in te voeren, tot een bepaalde drempel. Met deze functie kunnen gebruikers al hun juiste gegevens in Adobe Experience Platform opnemen terwijl al hun onjuiste gegevens afzonderlijk worden opgeslagen. Details worden toegevoegd aan batches die niet zijn gelukt om uit te leggen waarom deze niet zijn geslaagd voor validatie. Meer informatie over gedeeltelijke partijingestie kan in de [ gedeeltelijke partijingestitiedocumentatie ](../../ingestion/batch-ingestion/partial.md) worden gevonden. |

**Bekende kwesties**

* Geen

Meer leren over het opnemen van gegevens in Platform, bezoek de [ documentatie van de Ingestie van Gegevens ](../../ingestion/home.md).


## Doelen {#destinations}

In [ Real-time Customer Data Platform ](../../rtcdp/overview.md), zijn de bestemmingen pre-gebouwde integratie met bestemmingsplatforms die gegevens aan die partners op een naadloze manier activeren.

**Nieuwe bestemmingen**

Er zijn nieuwe doelen beschikbaar waar u uw Adobe Experience Platform-gegevens kunt activeren. Zie hieronder voor meer informatie:

| Doel | Beschrijving |
|--- | ---|
| Opslagdoelen voor cloud | Real-Time CDP kan uw segmenten nu als gegevensbestanden leveren aan uw [!DNL Amazon S3] - of SFTP-locatie voor cloudopslag. Hierdoor kunt u het publiek en de bijbehorende profielkenmerken naar uw interne systemen verzenden via CSV-bestanden of bestanden met tabs als scheidingsteken. |
| Advertising-bestemmingen | De [!DNL Google] -doelkaart wordt nu gesplitst in drie doelkaarten voor de drie verschillende [!DNL Google] -platforms die momenteel worden ondersteund in Real-Time CDP: [!DNL Google Ads] , [!DNL Google Ad Manager] , [!DNL Google] Display &amp; Video 360. |

Meer leren, bezoek het [ overzicht van bestemmingen ](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

Voor het aanbieden van relevante digitale ervaringen is een volledig begrip van uw klant vereist. Dit wordt bemoeilijkt wanneer uw klantengegevens over verschillende systemen worden gefragmenteerd, die elke individuele klant ertoe brengen om veelvoudige &quot;identiteiten&quot;te hebben te schijnen.

Met Adobe Experience Platform [!DNL Identity Service] kunt u uw klanten en hun gedrag beter laten zien door identiteiten tussen apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| Verbeterde persoonlijke grafiek | De functionaliteit voor privégrafieken is verbeterd en verlaagt zo de latentie bij het genereren van grafieken van een wekelijks batchproces tot een dagelijks vernieuwde grafiek. Hierdoor hebben [!DNL Identity Service] -klanten toegang tot meer actuele identiteitsgrafieken en koppelingen. |

**Bekende kwesties**

* Geen

Voor meer informatie over [!DNL Identity Service], zie het [ overzicht van de Dienst van de Identiteit ](../../identity-service/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Platform] -services. U kunt gegevens van een verscheidenheid van bronnen zoals de toepassingen van de Adobe, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| Verouderde signalen voor Adobe Audience Manager-connector | Gegevens op signaalniveau van Audience Manger worden niet meer verzonden. Merk op dat segmentlidmaatschap voor Traits en Segmenten nog zal worden omvat. Als gevolg van deze wijziging worden er geen binnenkomende gegevenssets meer gegenereerd. |
| Naam van gegevensset wijzigen | Datasets die door de schakelaar van de Manager van de Publiek worden geproduceerd zullen bijgewerkte namen en beschrijvingen hebben. |
| Schakelen tussen [!DNL Profile] en Audience Manger inschakelen | [!DNL Profile] kan worden in- of uitgeschakeld om gegevensset te promoten naar [!DNL Real-Time Customer Profile] . Schakelen wordt standaard ingeschakeld. |
| UI-ondersteuning voor cloudopslagsystemen | Nieuwe bronconnector voor [!DNL Azure Data Lake Storage Gen2] in de gebruikersinterface. |
| UI-ondersteuning voor CRM-systemen | Nieuwe bronconnector voor [!DNL HubSpot] , [!DNL Salesforce Service Cloud] en [!DNL ServiceNow] in de gebruikersinterface. |
| UI-ondersteuning voor databasesystemen | Nieuwe bronconnector voor [!DNL AWS Redshift] , [!DNL Google BigQuery] , [!DNL MariaDB] , [!DNL Microsoft SQL Server] en [!DNL MySQL] in de gebruikersinterface. |

**Bekende kwesties**

* Geen

Meer over bronnen leren, zie het [ overzicht van bronnen ](../../sources/home.md).
