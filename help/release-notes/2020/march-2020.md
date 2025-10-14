---
title: Aanvullende informatie van maart 2020 voor Adobe Experience Platform
description: Aanvullende informatie van maart 2020 voor Adobe Experience Platform.
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: opmerkingen bij de release;
exl-id: 407c2bac-4c8a-4939-b3dd-788250f15650
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 15%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum:donderdag 11 maart 2020**

Updates voor bestaande functies in Adobe Experience Platform:

* [Datagovernance](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## Datagovernance {#governance}

[!DNL Experience Platform] stelt bedrijven in staat gegevens van meerdere bedrijfssystemen samen te brengen, zodat marketers klanten beter kunnen identificeren, begrijpen en betrekken. [!DNL Experience Platform] bevat een end-to-end infrastructuur voor gegevensbeheer die ervoor zorgt dat gegevens binnen [!DNL Experience Platform] correct worden gebruikt en dat gegevens tussen systemen worden gedeeld.

Adobe Experience Platform-datagovernance is een reeks strategieën en technologieën die worden gebruikt om klantgegevens te beheren en naleving te waarborgen van regelgeving, beperkingen en beleidsregels die op gegevensgebruik van toepassing zijn. Dit speelt binnen [!DNL Experience Platform] een sleutelrol op verschillende niveaus zoals catalogisering, gegevensoorsprong, labeling van gegevensgebruik, beleid voor gegevenstoegang en beheer van toegang tot gegevens voor marketingacties.

**Nieuwe functies**

>[!NOTE]
>
>Enkele van de volgende nieuwe functies zijn momenteel in bèta beschikbaar en niet voor alle gebruikers. Beta-functies kunnen worden gewijzigd.

| Functie | Beschrijving |
| ------- | ----------- |
| Geautomatiseerde handhaving van beleid voor gegevensgebruik voor [!DNL Real-Time Customer Data Platform] | Het beleid van het gegevensgebruik wordt nu afgedwongen in het werkschema van het activeren van gegevens aan bestemmingen. Het Beleid van gegevens wordt ook ingebed en afgedwongen wanneer het aanbrengen van veranderingen die bestaande activeringen (zoals veranderingen in datasetetiketten, fusiebeleid, segmentdefinities, en anderen) beïnvloeden. |
| Gegevenslijn voor handhaving | Wanneer een beleid van het gegevensgebruik in Real-Time CDP wordt geschonden, toont UI een bericht dat de informatie van de gegevenslijn bevat om de gebruiker te helpen begrijpen waarom het beleid werd geschonden en wat zij kunnen doen om de schending op te lossen. |


**Bekende kwesties**

* Geen

Voor meer informatie over het Beleid van Gegevens, zie het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](../../data-governance/home.md).

## Gegevensopname {#ingestion}

Adobe Experience Platform biedt een uitgebreide reeks functies voor het invoeren van elk type en elke vertraging van gegevens. Adobe Experience Platform [!DNL Data Ingestion] biedt meerdere alternatieven voor het opnemen van gegevens, zoals batch-API&#39;s, streaming API&#39;s, native Adobe-connectors, partners voor gegevensintegratie of de Adobe Experience Platform-interface.

**Nieuwe functies**

| Functie | Beschrijving |
|------- | -----------|
| Gedeeltelijke batch ingestie | Gedeeltelijke batch-opname is de mogelijkheid om gegevens met fouten in te voeren, tot een bepaalde drempel. Met deze functie kunnen gebruikers al hun juiste gegevens in Adobe Experience Platform opnemen terwijl al hun onjuiste gegevens afzonderlijk worden opgeslagen. Details worden toegevoegd aan batches die niet zijn gelukt om uit te leggen waarom deze niet zijn geslaagd voor validatie. Meer informatie over gedeeltelijke partijingestie kan in de [&#x200B; gedeeltelijke partijingestitiedocumentatie &#x200B;](../../ingestion/batch-ingestion/partial.md) worden gevonden. |

**Bekende kwesties**

* Geen

Meer over het opnemen van gegevens in Experience Platform leren, bezoek de [&#x200B; documentatie van de Ingestie van Gegevens &#x200B;](../../ingestion/home.md).


## Bestemmingen {#destinations}

In [&#x200B; Real-Time Customer Data Platform &#x200B;](../../rtcdp/overview.md), zijn de bestemmingen pre-gebouwde integratie met bestemmingsplatforms die gegevens aan die partners op een naadloze manier activeren.

**Nieuwe bestemmingen**

Er zijn nieuwe doelen beschikbaar waar u uw Adobe Experience Platform-gegevens kunt activeren. Zie hieronder voor meer informatie:

| Bestemming | Beschrijving |
|--- | ---|
| Opslagdoelen voor cloud | Real-Time CDP kan uw segmenten nu als gegevensbestanden leveren aan uw [!DNL Amazon S3] - of SFTP-locatie voor cloudopslag. Hierdoor kunt u het publiek en de bijbehorende profielkenmerken naar uw interne systemen verzenden via CSV-bestanden of bestanden met tabs als scheidingsteken. |
| Advertising-bestemmingen | De [!DNL Google] -doelkaart wordt nu gesplitst in drie doelkaarten voor de drie verschillende [!DNL Google] -platforms die momenteel worden ondersteund in Real-Time CDP: [!DNL Google Ads] , [!DNL Google Ad Manager] , [!DNL Google] Display &amp; Video 360. |

Meer leren, bezoek het [&#x200B; overzicht van bestemmingen &#x200B;](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

Voor het aanbieden van relevante digitale ervaringen is een volledig begrip van uw klant vereist. Dit wordt bemoeilijkt wanneer uw klantengegevens over verschillende systemen worden gefragmenteerd, die elke individuele klant ertoe brengen om veelvoudige &quot;identiteiten&quot;te hebben te schijnen.

Met Adobe Experience Platform [!DNL Identity Service] kunt u uw klanten en hun gedrag beter laten zien door identiteiten tussen apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Verbeterde persoonlijke grafiek | De functionaliteit voor privégrafieken is verbeterd en verlaagt zo de latentie bij het genereren van grafieken van een wekelijks batchproces tot een dagelijks vernieuwde grafiek. Hierdoor hebben [!DNL Identity Service] -klanten toegang tot meer actuele identiteitsgrafieken en koppelingen. |

**Bekende kwesties**

* Geen

Voor meer informatie over [!DNL Identity Service], zie het [&#x200B; overzicht van de Dienst van de Identiteit &#x200B;](../../identity-service/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Experience Platform] -services. U kunt gegevens opnemen uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe functies**

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

Meer over bronnen leren, zie het [&#x200B; overzicht van bronnen &#x200B;](../../sources/home.md).
