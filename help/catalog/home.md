---
keywords: Experience Platform;home;populaire onderwerpen;catalogusservice;catalogus;Catalogusservice;gegevenslocatie;Gegevenslocatie;Gegevensbeheer;Lineage;Lijn;Catalogus;Gegevensset inschakelen
solution: Experience Platform
title: Overzicht van Catalog Service
topic: overview
description: Catalogusservice is het systeem voor het vastleggen van de gegevenslocatie en -lijn in Adobe Experience Platform. Terwijl alle gegevens die in Experience Platform worden opgenomen in het meer van Gegevens als dossiers en folders worden opgeslagen, houdt de Catalogus de meta-gegevens en de beschrijving van die dossiers en folders voor raadpleging en controledoeleinden.
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---


# [!DNL Catalog Service] - overzicht

[!DNL Catalog Service] is het registratiesysteem voor gegevenslocatie en -lijn in Adobe Experience Platform. Terwijl alle gegevens die in [!DNL Experience Platform] worden opgenomen in [!DNL Data Lake] als dossiers en folders worden opgeslagen, [!DNL Catalog] houdt de meta-gegevens en beschrijving van die dossiers en folders voor raadpleging en controledoeleinden.

Eenvoudig gezet, [!DNL Catalog] dienst als meta-gegevensopslag of &quot;catalogus&quot;waar u informatie over uw gegevens binnen [!DNL Experience Platform] kunt vinden. U kunt [!DNL Catalog] gebruiken om de volgende vragen te beantwoorden:

* Waar bevinden mijn gegevens zich?
* In welk stadium van verwerking bevinden deze gegevens zich?
* Welke systemen of processen hebben op mijn gegevens gehandeld?
* Hoeveel gegevens zijn verwerkt?
* Welke fouten zijn tijdens de verwerking opgetreden?

[!DNL Catalog] verstrekt een RESTful API die u toestaat om  [!DNL Platform] meta-gegevens programmatically te beheren gebruikend basisCRUD verrichtingen. Zie [Handleiding voor ontwikkelaars van catalogi](api/getting-started.md) voor meer informatie.

## [!DNL Catalog] en  [!DNL Experience Platform] diensten

De middelen die [!DNL Catalog Service] sporen worden gebruikt door veelvoudige [!DNL Experience Platform] diensten. Als u de [!DNL Catalog's] mogelijkheden optimaal wilt benutten, is het raadzaam bekend te raken met deze services en te weten hoe deze met [!DNL Catalog] werken.

### [!DNL Experience Data Model] (XDM) System

[!DNL Experience Data Model] (XDM) Het systeem is het gestandaardiseerde kader waardoor de gegevens van de klantenervaring  [!DNL Platform] organiseren. [!DNL Experience Platform] hefboomwerkingen XDM schema&#39;s om de structuur van gegevens op een verenigbare en herbruikbare manier te beschrijven.

Wanneer gegevens in [!DNL Platform] worden opgenomen, wordt de structuur van die gegevens in kaart gebracht aan een XDM-schema en binnen [!DNL Data Lake] als deel van een dataset opgeslagen. De meta-gegevens voor elke dataset worden gevolgd door [!DNL Catalog Service], die een verwijzing naar het XDM schema omvat dat de dataset met in overeenstemming is.

Voor meer algemene informatie over het Systeem XDM, te zien gelieve [XDM systeemoverzicht](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] Neemt gegevens van veelvoudige bronnen op en handhaaft verslagen als datasets binnen  [!DNL Data Lake]. [!DNL Catalog] volgt de meta-gegevens voor deze datasets, ongeacht hun bron of methode van opname.

Als u de methode voor het invoeren van batch gebruikt, worden ook extra metagegevens voor batchbestanden bijgehouden. [!DNL Catalog] Batches zijn gegevenseenheden die bestaan uit een of meer bestanden die als één eenheid moeten worden ingevoerd. [!DNL Catalog] volgt de meta-gegevens voor deze partijdossiers, evenals de datasets zij binnen na opname worden voortgeduurd. De meta-gegevens van de partij omvatten informatie over het aantal met succes opgenomen verslagen, evenals om het even welke ontbroken verslagen en bijbehorende foutenmeldingen.

Zie het [overzicht van gegevensinvoer](../ingestion/home.md) voor meer informatie.

## [!DNL Catalog] objecten

Zoals in de vorige sectie wordt geschetst, [!DNL Catalog] houdt meta-gegevens voor verscheidene soorten middelen en verrichtingen bij die door andere [!DNL Platform] diensten worden gebruikt. [!DNL Catalog] onderhoudt een eigen opslagruimte van &#39;objecten&#39; die deze metagegevens omvat. [!DNL Catalog] de voorwerpen zijn queryable vertegenwoordiging van  [!DNL Platform] gegevens die u toestaan om, uw gegevens te zoeken te controleren en te etiketteren zonder het moeten tot de gegevens zelf toegang hebben.

In de volgende tabel worden de verschillende objecttypen weergegeven die worden ondersteund door [!DNL Catalog]:

| Object | API-eindpunt | Definitie |
|---|---|---|
| Account | `/accounts` | Bij het maken van bronverbindingen moeten verificatiereferenties worden opgegeven. Een rekening vertegenwoordigt een inzameling van authentificatiegeloofsbrieven die werden gebruikt om een verbinding van een specifiek type tot stand te brengen. Elke verbinding heeft een reeks unieke parameters die door [!DNL Catalog] worden voortgeduurd en in [!DNL Azure Key Vault] worden beveiligd. |
| Batch | `/batches` | Batches zijn gegevenseenheden die bestaan uit een of meer bestanden die als één eenheid moeten worden ingevoerd. Een partijvoorwerp in [!DNL Catalog] schetst de innamemetriek van de partij (zoals het aantal verwerkte verslagen of grootte op schijf) en kan verbindingen aan datasets, meningen, en andere middelen omvatten die door de partijverrichting werden beïnvloed. |
| Verbinding | `/connections` | Een verbinding is één enkel geval van een bronschakelaar, uniek aan uw organisatie en gevormd gebruikend de aangewezen authentificatiereferenties voor het schakelaartype. |
| Connector | `/connectors` | Connectors definiëren hoe bronverbindingen gegevens moeten verzamelen van andere Adobe-toepassingen (zoals Adobe Analytics en Adobe Audience Manager), bronnen voor cloudopslag van derden (zoals [!DNL Azure Blob], [!DNL Amazon S3], FTP-servers en SFTP-servers) en CRM-systemen van derden (zoals [!DNL Microsoft Dynamics] en [!DNL Salesforce]). |
| Gegevensset | `/dataSets` | Een dataset is een opslag en beheersconstructie die voor de inzameling van gegevens (typisch een lijst) wordt gebruikt die een schema (kolommen) en gebieden (rijen) bevat. Zie [datasets overview](./datasets/overview.md) voor meer informatie. |
| Gegevensbestand | `/datasetFiles` | Gegevensbestanden vertegenwoordigen gegevensblokken die zijn opgeslagen op [!DNL Platform]. Als verslagen van letterlijke dossiers, zijn deze waar u de grootte van het dossier, het aantal verslagen kunt vinden het bevat, en een verwijzing naar de partij die het dossier opnam. |

## Volgende stappen

Dit document gaf een inleiding aan [!DNL Catalog Service] en hoe het binnen het grotere werkingsgebied van [!DNL Experience Platform] functioneert. Zie de [[!DNL Catalog] ontwikkelaarshandleiding](api/getting-started.md) voor stappen bij het werken met de verschillende eindpunten van die [!DNL Catalog] API. Het wordt aanbevolen ook te verwijzen naar de handleiding voor het filteren van catalogusgegevens](api/filter-data.md) om de best practices voor het beperken van de gegevens die worden geretourneerd in API-reacties te volgen.[