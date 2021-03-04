---
title: Opmerkingen bij de release van Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform van 11 maart 2020
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: opmerkingen bij de release;
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 2%

---


# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 11 maart 2020**

Updates voor bestaande functies in Adobe Experience Platform:

* [[!DNL Data Governance]](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## [!DNL Data Governance] {#governance}

[!DNL Experience Platform] staat bedrijven toe om gegevens van veelvoudige ondernemingssystemen samen te brengen om marketers beter toe te staan om, klanten te identificeren te begrijpen en in dienst te nemen. [!DNL Experience Platform] omvat een end-to-end infrastructuur voor gegevensbeheer om te zorgen voor het juiste gebruik van gegevens binnen  [!DNL Platform] en wanneer deze worden gedeeld tussen systemen.

Adobe Experience Platform [!DNL Data Governance] is een reeks strategieën en technologieën die worden gebruikt om klantgegevens te beheren en naleving van verordeningen, beperkingen, en beleid te verzekeren die op gegevensgebruik van toepassing zijn. Het speelt een belangrijke rol binnen [!DNL Experience Platform] op diverse niveaus, met inbegrip van catalogiseren, gegevenslijn, het etiketteren van het gegevensgebruik, het beleid van de gegevenstoegang, en toegangsbeheer over gegevens voor marketing acties.

**Nieuwe functies**

>[!NOTE]
>
>Enkele van de volgende nieuwe functies zijn momenteel in bèta beschikbaar en niet voor alle gebruikers. Beta-functies kunnen worden gewijzigd.

| Functie | Beschrijving |
| ------- | ----------- |
| Geautomatiseerde handhaving van beleidsregels voor gegevensgebruik voor [!DNL Real-time Customer Data Platform] | Het beleid van het gegevensgebruik wordt nu afgedwongen in het werkschema van het activeren van gegevens aan bestemmingen. [!DNL Data Governance] wordt ook ingebed en afgedwongen wanneer het aanbrengen van veranderingen die bestaande activeringen (zoals veranderingen in datasetetiketten, fusiepolitiek, segmentdefinities, en anderen) beïnvloeden. |
| Gegevenslijn voor handhaving | Wanneer een beleid van het gegevensgebruik in real time CDP wordt geschonden, toont UI een bericht dat de informatie van de gegevenslijn bevat om de gebruiker te helpen begrijpen waarom het beleid werd geschonden en wat zij kunnen doen om de schending op te lossen. |


**Bekende problemen**

* Geen

Zie [Overzicht van gegevensbeheer](../../data-governance/home.md) voor meer informatie over [!DNL Data Governance].

## Gegevensinname {#ingestion}

Adobe Experience Platform biedt een uitgebreide reeks functies voor het invoeren van elk type en elke vertraging van gegevens. Adobe Experience Platform [!DNL Data Ingestion] biedt meerdere alternatieven voor het opnemen van gegevens, zoals batch-API&#39;s, streaming API&#39;s, native Adobe-connectors, partners voor gegevensintegratie of de Adobe Experience Platform-interface.

**Nieuwe functies**

| Functie | Beschrijving |
|------- | -----------|
| Gedeeltelijke batch ingestie | Gedeeltelijke batch-opname is de mogelijkheid om gegevens met fouten in te voeren, tot een bepaalde drempel. Met deze functie kunnen gebruikers al hun juiste gegevens in Adobe Experience Platform opnemen terwijl al hun onjuiste gegevens afzonderlijk worden opgeslagen. Er worden details toegevoegd aan batches die niet zijn gelukt om uit te leggen waarom deze niet zijn geslaagd voor de validatie. Meer informatie over gedeeltelijke batch-opname vindt u in de [documentatie over gedeeltelijke batch-opname](../../ingestion/batch-ingestion/partial.md). |

**Bekende problemen**

* Geen

Meer over het opnemen van gegevens in Platform, bezoek [de documentatie van de Ingestie van Gegevens](../../ingestion/home.md).


## Doelen {#destinations}

In [Real-time Platform van de Gegevens van de Klant](../../rtcdp/overview.md), zijn de bestemmingen prebuilt integraties met bestemmingsplatforms die gegevens aan die partners op een naadloze manier activeren.

**Nieuwe bestemmingen**

Er zijn nieuwe doelen beschikbaar waar u uw Adobe Experience Platform-gegevens kunt activeren. Zie hieronder voor meer informatie:

| Bestemming | Beschrijving |
|--- | ---|
| Opslagdoelen voor cloud | CDP in realtime kan uw segmenten nu als gegevensbestanden leveren aan uw [!DNL Amazon S3]- of SFTP-locatie voor cloudopslag. Hierdoor kunt u het publiek en de bijbehorende profielkenmerken naar uw interne systemen verzenden via CSV- of tabgescheiden bestanden. |
| Reclamebestemmingen | De [!DNL Google] bestemmingskaart wordt nu gesplitst in drie bestemmingskaarten, voor de drie verschillende [!DNL Google] platforms momenteel gesteund in Echt - tijd CDP: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] Display &amp; Video 360. |

Voor meer informatie gaat u naar het [overzicht van doelen](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

Voor het aanbieden van relevante digitale ervaringen is een volledig begrip van uw klant vereist. Dit wordt bemoeilijkt wanneer uw klantengegevens over verschillende systemen worden gefragmenteerd, die elke individuele klant ertoe brengen om veelvoudige &quot;identiteiten&quot;te hebben te schijnen.

Met Adobe Experience Platform [!DNL Identity Service] kunt u een beter beeld krijgen van uw klant en zijn gedrag door identiteiten tussen apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Verbeterde persoonlijke grafiek | De functionaliteit voor privégrafieken is verbeterd en verkleint de latentie bij het genereren van grafieken van een wekelijks batchproces tot een dagelijks vernieuwde grafiek. Hierdoor hebben klanten van [!DNL Identity Service] toegang tot meer actuele identiteitsgrafieken en koppelingen. |

**Bekende problemen**

* Geen

Voor meer informatie over [!DNL Identity Service], zie [Overzicht van de Dienst van de Identiteit](../../identity-service/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met services van [!DNL Platform]. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Verouderde signalen voor Adobe Audience Manager-connector | Gegevens op signaalniveau van Audience Manger worden niet meer verzonden. Merk op dat segmentlidmaatschap voor Traits en Segmenten nog zal worden omvat. Als gevolg van deze wijziging worden er geen binnenkomende gegevenssets meer gegenereerd. |
| Naam van gegevensset wijzigen | Datasets die door de schakelaar van de Manager van de Publiek worden geproduceerd zullen bijgewerkte namen en beschrijvingen hebben. |
| [!DNL Profile]-schakeloptie inschakelen in Audience Manger | [!DNL Profile] schakelopties kunnen worden in- of uitgeschakeld om gegevenssets te promoten naar  [!DNL Real-time Customer Profile]. Schakelen wordt standaard ingeschakeld. |
| UI-ondersteuning voor cloudopslagsystemen | Nieuwe bronschakelaar voor [!DNL Azure Data Lake Storage Gen2] in UI. |
| UI-ondersteuning voor CRM-systemen | Nieuwe bronconnector voor [!DNL HubSpot], [!DNL Salesforce Service Cloud] en [!DNL ServiceNow] in de interface. |
| UI-ondersteuning voor databasesystemen | Nieuwe bronconnector voor [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server] en [!DNL MySQL] in de gebruikersinterface. |

**Bekende problemen**

* Geen

Meer over bronnen leren, zie [bronnen overzicht](../../sources/home.md).