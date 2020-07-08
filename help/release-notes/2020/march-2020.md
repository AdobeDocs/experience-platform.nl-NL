---
title: Opmerkingen bij de release Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform van 11 maart 2020
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 3%

---


# Opmerkingen bij de release Adobe Experience Platform

**Releasedatum: 11 maart 2020**

Updates voor bestaande functies in Adobe Experience Platform:

* [Data Governance](#governance)
* [Gegevensinname](#ingestion)
* [Doelen](#destinations)
* [Identiteitsservice](#identity)
* [Bronnen](#sources)

## Data Governance {#governance}

Experience Platform staat bedrijven toe om gegevens van veelvoudige ondernemingssystemen samen te brengen om marketers beter toe te staan om, klanten te identificeren te begrijpen en in dienst te nemen. Experience Platform omvat een end-to-end infrastructuur voor gegevensbeheer, met inbegrip van de Etikettering en de Handhaving van het Gebruik van Gegevens (DULE), om het juiste gebruik van gegevens binnen Platform en wanneer het wordt gedeeld tussen systemen te verzekeren.

Het Beheer van de Gegevens van het Adobe Experience Platform is een reeks strategieën en technologieën die worden gebruikt om klantengegevens te beheren en naleving van verordeningen, beperkingen, en beleid te verzekeren van toepassing op gegevensgebruik. Het speelt een sleutelrol binnen Experience Platform op diverse niveaus, met inbegrip van catalogiseren, gegevenslijn, het etiketteren van het gegevensgebruik, het beleid van de gegevenstoegang, en toegangscontrole over gegevens voor marketing acties.

**Nieuwe functies**

>[!NOTE]
>
>Enkele van de volgende nieuwe functies zijn momenteel in bèta beschikbaar en niet voor alle gebruikers. Beta-functies kunnen worden gewijzigd.

| Functie | Beschrijving |
| ------- | ----------- |
| Geautomatiseerde handhaving van het gegevensgebruiksbeleid voor het Platform van de Gegevens van de Klant in real time | Het beleid van het gegevensgebruik wordt nu afgedwongen in het werkschema van het activeren van gegevens aan bestemmingen. Het Beleid van gegevens wordt ook ingebed en afgedwongen wanneer het aanbrengen van veranderingen die bestaande activeringen (zoals veranderingen in datasetetiketten, fusiebeleid, segmentdefinities, en anderen) beïnvloeden. |
| Gegevenslijn voor handhaving | Wanneer een beleid van het gegevensgebruik in real time CDP wordt geschonden, toont UI een bericht dat de informatie van de gegevenslijn bevat om de gebruiker te helpen begrijpen waarom het beleid werd geschonden en wat zij kunnen doen om de schending op te lossen. |


**Bekende problemen**

* Geen

Zie het overzicht [van](../../data-governance/home.md)gegevensbeheer voor meer informatie over gegevensbeheer.

## Gegevensinname {#ingestion}

Adobe Experience Platform biedt een uitgebreide reeks functies voor het invoeren van elk type en elke vertraging van gegevens. De Ingestie van Gegevens van het Adobe Experience Platform verstrekt veelvoudige alternatieven voor het opnemen van gegevens met inbegrip van Band APIs, het stromen APIs, inheemse schakelaars van Adobe, de partners van de gegevensintegratie, of Adobe Experience Platform UI.

**Nieuwe functies**

| Functie | Beschrijving |
|------- | -----------|
| Gedeeltelijke batch ingestie | Gedeeltelijke batch-opname is de mogelijkheid om gegevens met fouten in te voeren, tot een bepaalde drempel. Met deze mogelijkheid kunnen gebruikers al hun juiste gegevens in het Adobe Experience Platform opnemen terwijl al hun onjuiste gegevens afzonderlijk worden opgeslagen. Er worden details toegevoegd aan batches die niet zijn gelukt om uit te leggen waarom deze niet zijn geslaagd voor de validatie. Meer informatie over gedeeltelijke batch-inname vindt u in de [documentatie](../../ingestion/batch-ingestion/partial.md)over gedeeltelijke batch-inname. |

**Bekende problemen**

* Geen

Meer over het opnemen van gegevens in Platform, bezoek de documentatie [van de Ingestie van](../../ingestion/home.md)Gegevens.


## Doelen {#destinations}

In [Adobe Real-time Customer Data Platform](../../rtcdp/overview.md)zijn doelen vooraf gebouwde integratie met doelplatforms die gegevens naadloos aan die partners activeren.

**Nieuwe bestemmingen**

Er zijn nieuwe doelen beschikbaar waar u de gegevens van uw Adobe Experience Platform kunt activeren. Zie hieronder voor meer informatie:

| Bestemming | Beschrijving |
|--- | ---|
| Opslagdoelen voor cloud | Adobe Real-time CDP kan uw segmenten nu als gegevensbestanden leveren aan uw Amazon S3- of SFTP-cloudopslaglocaties. Hierdoor kunt u het publiek en de bijbehorende profielkenmerken naar uw interne systemen verzenden via CSV- of tabgescheiden bestanden. |
| Reclamebestemmingen | De Google-doelkaart wordt nu gesplitst in drie doelkaarten voor de drie verschillende Google-platforms die momenteel worden ondersteund in Adobe Real-time CDP: Google Ads, Google Ad Manager, Google Display en Video 360. |

Ga voor meer informatie naar het overzicht met [bestemmingen](../../rtcdp/destinations/destinations-overview.md)

## Identiteitsservice {#identity}

Voor het aanbieden van relevante digitale ervaringen is een volledig begrip van uw klant vereist. Dit wordt bemoeilijkt wanneer uw klantengegevens over verschillende systemen worden gefragmenteerd, die elke individuele klant ertoe brengen om veelvoudige &quot;identiteiten&quot;te hebben te schijnen.

De Dienst van de Identiteit van het Adobe Experience Platform helpt u om een beter beeld van uw klant en hun gedrag te krijgen door identiteiten over apparaten en systemen te overbruggen, die u toestaan om impactful, persoonlijke digitale ervaringen in real time te leveren.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Verbeterde persoonlijke grafiek | De functionaliteit van de persoonlijke grafiek is verbeterd om de latentie van de grafiekgeneratie van een wekelijks partijproces aan een dagelijks vernieuwde grafiek te verminderen, die de klanten van de Dienst van de Identiteit toestaat om tot recentere identiteitsgrafieken en verbindingen toegang te hebben. |

**Bekende problemen**

* Geen

Voor meer informatie over de Dienst van de Identiteit, zie het overzicht [van de Dienst van de](../../identity-service/home.md)Identiteit.

## Bronnen {#sources}

Het Adobe Experience Platform kan gegevens uit externe bronnen opnemen terwijl het toestaan van u om die gegevens te structureren, te etiketteren en te verbeteren gebruikend de diensten van het Platform. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Verouderde signalen voor aansluiting van Adobe Audience Manager | Gegevens op signaalniveau van Audience Manger worden niet meer verzonden. Merk op dat segmentlidmaatschap voor Traits en Segmenten nog zal worden omvat. Als gevolg van deze wijziging worden er geen binnenkomende gegevenssets meer gegenereerd. |
| Naam van gegevensset wijzigen | Datasets die door de schakelaar van de Manager van de Publiek worden geproduceerd zullen bijgewerkte namen en beschrijvingen hebben. |
| Schakelen tussen profielen in Audience Manger inschakelen | De knevel van het profiel kan worden toegelaten of worden onbruikbaar gemaakt om dataset aan het Profiel van de Klant in real time te bevorderen. Schakelen wordt standaard ingeschakeld. |
| UI-ondersteuning voor cloudopslagsystemen | Nieuwe bronaansluiting voor Azure Data Lake Storage Gen2 in de gebruikersinterface. |
| UI-ondersteuning voor CRM-systemen | Nieuwe bronschakelaar voor HubSpot, de Wolk van de Dienst van Salesforce, en ServiceNow in UI. |
| UI-ondersteuning voor databasesystemen | Nieuwe bronconnector voor AWS Redshift, Google BigQuery, MariaDB, Microsoft SQL Server en MySQL in de gebruikersinterface. |

**Bekende problemen**

* Geen

Zie het [bronoverzicht](../../sources/home.md)voor meer informatie over bronnen.