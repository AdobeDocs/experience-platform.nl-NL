---
title: Opmerkingen bij de release van Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform van 11 maart 2020
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: opmerkingen bij de release;
exl-id: 407c2bac-4c8a-4939-b3dd-788250f15650
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 3%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 11 maart 2020**

Updates voor bestaande functies in Adobe Experience Platform:

* [Data Governance](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## Gegevensbeheer {#governance}

[!DNL Experience Platform] staat bedrijven toe om gegevens van veelvoudige ondernemingssystemen samen te brengen om marketers beter toe te staan om, klanten te identificeren te begrijpen en in dienst te nemen. [!DNL Experience Platform] omvat een end-to-end infrastructuur voor gegevensbeheer om het juiste gebruik van gegevens binnen [!DNL Platform] en wanneer deze worden gedeeld tussen systemen.

Adobe Experience Platform Data Governance is een reeks strategieën en technologieën die worden gebruikt om klantgegevens te beheren en naleving van regelgeving, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik te waarborgen. Het speelt een sleutelrol binnen [!DNL Experience Platform] op verschillende niveaus, waaronder catalogisering, gegevenskoppeling, etikettering van het gegevensgebruik, beleid inzake gegevenstoegang en toegangscontrole voor marketingacties.

**Nieuwe functies**

>[!NOTE]
>
>Enkele van de volgende nieuwe functies zijn momenteel in bèta beschikbaar en niet voor alle gebruikers. Beta-functies kunnen worden gewijzigd.

| Functie | Beschrijving |
| ------- | ----------- |
| Geautomatiseerde handhaving van beleid voor gegevensgebruik voor [!DNL Real-time Customer Data Platform] | Het beleid van het gegevensgebruik wordt nu afgedwongen in het werkschema van het activeren van gegevens aan bestemmingen. Het Beleid van gegevens wordt ook ingebed en afgedwongen wanneer het aanbrengen van veranderingen die bestaande activeringen (zoals veranderingen in datasetetiketten, fusiebeleid, segmentdefinities, en anderen) beïnvloeden. |
| Gegevenslijn voor handhaving | Wanneer een beleid van het gegevensgebruik in real time CDP wordt geschonden, toont UI een bericht dat de informatie van de gegevenslijn bevat om de gebruiker te helpen begrijpen waarom het beleid werd geschonden en wat zij kunnen doen om de schending op te lossen. |


**Bekende problemen**

* Geen

Voor meer informatie over het Beheer van Gegevens, zie [Overzicht van gegevensbeheer](../../data-governance/home.md).

## Gegevensinname {#ingestion}

Adobe Experience Platform biedt een uitgebreide reeks functies voor het invoeren van elk type en elke vertraging van gegevens. Adobe Experience Platform [!DNL Data Ingestion] biedt meerdere alternatieven voor het opnemen van gegevens, waaronder batch-API&#39;s, streaming API&#39;s, native Adobe-connectors, partners voor gegevensintegratie of de Adobe Experience Platform-interface.

**Nieuwe functies**

| Functie | Beschrijving |
|------- | -----------|
| Gedeeltelijke batch ingestie | Gedeeltelijke batch-opname is de mogelijkheid om gegevens met fouten in te voeren, tot een bepaalde drempel. Met deze functie kunnen gebruikers al hun juiste gegevens in Adobe Experience Platform opnemen terwijl al hun onjuiste gegevens afzonderlijk worden opgeslagen. Er worden details toegevoegd aan batches die niet zijn gelukt om uit te leggen waarom deze niet zijn geslaagd voor de validatie. Meer informatie over gedeeltelijke batch-opname vindt u in de [gedeeltelijke batch-opname documentatie](../../ingestion/batch-ingestion/partial.md). |

**Bekende problemen**

* Geen

Ga voor meer informatie over het opnemen van gegevens in het Platform naar de [Documentatie over gegevensinname](../../ingestion/home.md).


## Doelen {#destinations}

In [Real-time Customer Data Platform](../../rtcdp/overview.md), zijn de bestemmingen prebuilt integratie met bestemmingsplatforms die gegevens aan die partners op een naadloze manier activeren.

**Nieuwe bestemmingen**

Er zijn nieuwe doelen beschikbaar waar u uw Adobe Experience Platform-gegevens kunt activeren. Zie hieronder voor meer informatie:

| Bestemming | Beschrijving |
|--- | ---|
| Opslagdoelen voor cloud | CDP in real time kan nu uw segmenten als gegevensdossiers aan uw leveren [!DNL Amazon S3] of SFTP-cloudopslaglocaties. Hierdoor kunt u het publiek en de bijbehorende profielkenmerken naar uw interne systemen verzenden via CSV- of tabgescheiden bestanden. |
| Reclamebestemmingen | De [!DNL Google] de bestemmingskaart is nu verdeeld in drie bestemmingskaarten, voor de drie verschillende [!DNL Google] platformen die momenteel worden ondersteund in CDP in realtime: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] Weergave en video 360. |

Ga voor meer informatie naar de [Overzicht van doelen](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

Voor het aanbieden van relevante digitale ervaringen is een volledig begrip van uw klant vereist. Dit wordt bemoeilijkt wanneer uw klantengegevens over verschillende systemen worden gefragmenteerd, die elke individuele klant ertoe brengen om veelvoudige &quot;identiteiten&quot;te hebben te schijnen.

Adobe Experience Platform [!DNL Identity Service] helpt u om een beter beeld van uw klant en hun gedrag te krijgen door identiteiten over apparaten en systemen te overbruggen, die u toestaan om daadwerkelijke, persoonlijke digitale ervaringen in echt te leveren - tijd.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Verbeterde persoonlijke grafiek | De functionaliteit voor privégrafieken is verbeterd en verlaagt zo de latentie bij het genereren van grafieken van een wekelijks batchproces tot een dagelijks vernieuwde grafiek, zodat [!DNL Identity Service] klanten toegang krijgen tot meer actuele identiteitsgrafieken en koppelingen. |

**Bekende problemen**

* Geen

Meer informatie over [!DNL Identity Service], zie de [Overzicht van identiteitsservice](../../identity-service/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Platform] diensten. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Verouderde signalen voor Adobe Audience Manager-connector | Gegevens op signaalniveau van Audience Manger worden niet meer verzonden. Merk op dat segmentlidmaatschap voor Traits en Segmenten nog zal worden omvat. Als gevolg van deze wijziging worden er geen binnenkomende gegevenssets meer gegenereerd. |
| Naam van gegevensset wijzigen | Datasets die door de schakelaar van de Manager van de Publiek worden geproduceerd zullen bijgewerkte namen en beschrijvingen hebben. |
| Inschakelen [!DNL Profile] schakelen in Audience Manger | [!DNL Profile] schakelt u in of uit om gegevensset te promoten naar [!DNL Real-time Customer Profile]. Schakelen wordt standaard ingeschakeld. |
| UI-ondersteuning voor cloudopslagsystemen | Nieuwe bronconnector voor [!DNL Azure Data Lake Storage Gen2] in de gebruikersinterface. |
| UI-ondersteuning voor CRM-systemen | Nieuwe bronconnector voor [!DNL HubSpot], [!DNL Salesforce Service Cloud], en [!DNL ServiceNow] in de gebruikersinterface. |
| UI-ondersteuning voor databasesystemen | Nieuwe bronconnector voor [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server], en [!DNL MySQL] in de gebruikersinterface. |

**Bekende problemen**

* Geen

Zie voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).
