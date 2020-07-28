---
title: Opmerkingen bij de release Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform van 11 maart 2020
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: f881c1365684b1ca9e6bf9a8ce866d234dc54128
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 2%

---


# Opmerkingen bij de release Adobe Experience Platform

**Releasedatum: 11 maart 2020**

Updates voor bestaande functies in Adobe Experience Platform:

* [!DNL Data Governance](#governance)
* [!DNL Data Ingestion](#ingestion)
* [!DNL Destinations](#destinations)
* [!DNL Identity Service](#identity)
* [!DNL Sources](#sources)

## [!DNL Data Governance] {#governance}

[!DNL Experience Platform] staat bedrijven toe om gegevens van veelvoudige ondernemingssystemen samen te brengen om marketers beter toe te staan om, klanten te identificeren te begrijpen en in dienst te nemen. [!DNL Experience Platform] omvat een end-to-end infrastructuur voor gegevensbeheer, met inbegrip van de Etikettering en de Handhaving van het Gebruik van Gegevens (DULE), om het juiste gebruik van gegevens binnen [!DNL Platform] en wanneer het wordt gedeeld tussen systemen te verzekeren.

Adobe Experience Platform [!DNL Data Governance] is een reeks strategieën en technologieën die worden gebruikt om klantgegevens te beheren en naleving van verordeningen, beperkingen, en beleid te verzekeren die op gegevensgebruik van toepassing zijn. Het speelt een sleutelrol binnen [!DNL Experience Platform] op diverse niveaus, met inbegrip van catalogiseren, gegevenslijn, het etiketteren van het gegevensgebruik, het beleid van de gegevenstoegang, en toegangscontrole over gegevens voor marketing acties.

**Nieuwe functies**

>[!NOTE]
>
>Enkele van de volgende nieuwe functies zijn momenteel in bèta beschikbaar en niet voor alle gebruikers. Beta-functies kunnen worden gewijzigd.

| Functie | Beschrijving |
| ------- | ----------- |
| Geautomatiseerde handhaving van beleid voor gegevensgebruik voor [!DNL Real-time Customer Data Platform] | Het beleid van het gegevensgebruik wordt nu afgedwongen in het werkschema van het activeren van gegevens aan bestemmingen. [!DNL Data Governance] wordt ook ingebed en afgedwongen wanneer het aanbrengen van veranderingen die bestaande activeringen (zoals veranderingen in datasetetiketten, fusiepolitiek, segmentdefinities, en anderen) beïnvloeden. |
| Gegevenslijn voor handhaving | Wanneer een beleid van het gegevensgebruik in real time CDP wordt geschonden, toont UI een bericht dat de informatie van de gegevenslijn bevat om de gebruiker te helpen begrijpen waarom het beleid werd geschonden en wat zij kunnen doen om de schending op te lossen. |


**Bekende problemen**

* Geen

Voor meer informatie over [!DNL Data Governance], zie het [Overzicht](../../data-governance/home.md)van het Beleid van Gegevens.

## Gegevensinname {#ingestion}

Adobe Experience Platform biedt een uitgebreide reeks functies voor het invoeren van elk type en elke vertraging van gegevens. Adobe Experience Platform [!DNL Data Ingestion] biedt meerdere alternatieven voor het opnemen van gegevens, waaronder batch-API&#39;s, streaming API&#39;s, native Adobe-connectors, partners voor gegevensintegratie of de interface van het Adobe Experience Platform.

**Nieuwe functies**

| Functie | Beschrijving |
|------- | -----------|
| Gedeeltelijke batch ingestie | Gedeeltelijke batch-opname is de mogelijkheid om gegevens met fouten in te voeren, tot een bepaalde drempel. Met deze mogelijkheid kunnen gebruikers al hun juiste gegevens in het Adobe Experience Platform opnemen terwijl al hun onjuiste gegevens afzonderlijk worden opgeslagen. Er worden details toegevoegd aan batches die niet zijn gelukt om uit te leggen waarom deze niet zijn geslaagd voor de validatie. Meer informatie over gedeeltelijke batch-inname vindt u in de [documentatie](../../ingestion/batch-ingestion/partial.md)over gedeeltelijke batch-inname. |

**Bekende problemen**

* Geen

Meer over het opnemen van gegevens in Platform, bezoek de documentatie [van de Ingestie van](../../ingestion/home.md)Gegevens.


## Doelen {#destinations}

In [Adobe Real-time het Platform](../../rtcdp/overview.md)van de Gegevens van de Klant, zijn de bestemmingen prebuilt integraties met bestemmingsplatforms die gegevens aan die partners op een naadloze manier activeren.

**Nieuwe bestemmingen**

Er zijn nieuwe doelen beschikbaar waar u de gegevens van uw Adobe Experience Platform kunt activeren. Zie hieronder voor meer informatie:

| Bestemming | Beschrijving |
|--- | ---|
| Opslagdoelen voor cloud | Adobe CDP in realtime kan uw segmenten nu als gegevensbestanden leveren aan uw [!DNL Amazon S3] of SFTP-locatie voor cloudopslag. Hierdoor kunt u het publiek en de bijbehorende profielkenmerken naar uw interne systemen verzenden via CSV- of tabgescheiden bestanden. |
| Reclamebestemmingen | De [!DNL Google] bestemmingskaart wordt nu gesplitst in drie bestemmingskaarten, voor de drie verschillende [!DNL Google] platforms die momenteel in Adobe in real time CDP worden gesteund: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] Display &amp; Video 360. |

Ga voor meer informatie naar het overzicht met [bestemmingen](../../rtcdp/destinations/destinations-overview.md)

## [!DNL Identity Service] {#identity}

Voor het aanbieden van relevante digitale ervaringen is een volledig begrip van uw klant vereist. Dit wordt bemoeilijkt wanneer uw klantengegevens over verschillende systemen worden gefragmenteerd, die elke individuele klant ertoe brengen om veelvoudige &quot;identiteiten&quot;te hebben te schijnen.

Adobe Experience Platform [!DNL Identity Service] helpt u om een beter beeld van uw klant en hun gedrag te krijgen door identiteiten over apparaten en systemen te overbruggen, die u toestaan om daadwerkelijke, persoonlijke digitale ervaringen in real time te leveren.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Verbeterde persoonlijke grafiek | De functionaliteit voor privégrafieken is verbeterd en verkleint de latentie bij het genereren van grafieken van een wekelijks batchproces tot een dagelijks vernieuwde grafiek. Hierdoor hebben [!DNL Identity Service] klanten toegang tot meer actuele identiteitsgrafieken en koppelingen. |

**Bekende problemen**

* Geen

Voor meer informatie over [!DNL Identity Service], zie het overzicht [van de Dienst van de](../../identity-service/home.md)Identiteit.

## Bronnen {#sources}

Het Adobe Experience Platform kan gegevens uit externe bronnen opnemen terwijl het toestaan van u om die gegevens te structureren, te etiketteren en te verbeteren gebruikend de [!DNL Platform] diensten. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Verouderde signalen voor aansluiting van Adobe Audience Manager | Gegevens op signaalniveau van Audience Manger worden niet meer verzonden. Merk op dat segmentlidmaatschap voor Traits en Segmenten nog zal worden omvat. Als gevolg van deze wijziging worden er geen binnenkomende gegevenssets meer gegenereerd. |
| Naam van gegevensset wijzigen | Datasets die door de schakelaar van de Manager van de Publiek worden geproduceerd zullen bijgewerkte namen en beschrijvingen hebben. |
| Schakelen [!DNL Profile] in Audience Manger inschakelen | [!DNL Profile] schakelopties kunnen worden in- of uitgeschakeld om gegevenssets te promoten naar [!DNL Real-time Customer Profile]. Schakelen wordt standaard ingeschakeld. |
| UI-ondersteuning voor cloudopslagsystemen | Nieuwe bronschakelaar voor [!DNL Azure Data Lake Storage Gen2] in UI. |
| UI-ondersteuning voor CRM-systemen | Nieuwe bronschakelaar voor [!DNL HubSpot], [!DNL Salesforce Service Cloud], en [!DNL ServiceNow] in UI. |
| UI-ondersteuning voor databasesystemen | Nieuwe bronschakelaar voor [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server], en [!DNL MySQL] in UI. |

**Bekende problemen**

* Geen

Zie het [bronoverzicht](../../sources/home.md)voor meer informatie over bronnen.