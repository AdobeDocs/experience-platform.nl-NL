---
keywords: Experience Platform;home;popular topics;catalog service;catalog;Catalog service;data location;Data Location;Data management;data management;Lineage;lineage;Catalog;enable dataset
solution: Experience Platform
title: Overzicht van Catalog Service
topic: overview
description: Catalogusservice is het systeem voor het vastleggen van de gegevenslocatie en -lijn in Adobe Experience Platform. Terwijl alle gegevens die in Experience Platform worden opgenomen in het meer van Gegevens als dossiers en folders worden opgeslagen, houdt de Catalogus de meta-gegevens en de beschrijving van die dossiers en folders voor raadpleging en controledoeleinden.
translation-type: tm+mt
source-git-commit: 34cfcaac276bf2645a0365a0dfa71c4ead6e2ecb
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 0%

---


# [!DNL Catalog Service] - overzicht

[!DNL Catalog Service] is het registratiesysteem voor gegevenslocatie en -lijn in Adobe Experience Platform. Terwijl alle gegevens die in worden opgenomen in [!DNL Experience Platform] in [!DNL Data Lake] als dossiers en folders worden opgeslagen, [!DNL Catalog] houdt de meta-gegevens en de beschrijving van die dossiers en folders voor raadpleging en controledoeleinden.

Eenvoudig gezet, handelt [!DNL Catalog] als meta-gegevensopslag of &quot;catalogus&quot;waar u informatie over uw gegevens binnen kunt vinden [!DNL Experience Platform]. U kunt de volgende vragen [!DNL Catalog] beantwoorden:

* Waar bevinden mijn gegevens zich?
* In welk stadium van verwerking bevinden deze gegevens zich?
* Welke systemen of processen hebben op mijn gegevens gehandeld?
* Hoeveel gegevens zijn verwerkt?
* Welke fouten zijn tijdens de verwerking opgetreden?

[!DNL Catalog] biedt een RESTful-API waarmee u [!DNL Platform] metagegevens programmatisch kunt beheren met behulp van standaard-CRUD-bewerkingen. Zie de [ontwikkelaarsgids](api/getting-started.md) van de Catalogus voor meer informatie.

## [!DNL Catalog] en [!DNL Experience Platform] diensten

De middelen die [!DNL Catalog Service] sporen worden gebruikt door de veelvoudige [!DNL Experience Platform] diensten. Om de [!DNL Catalog's] mogelijkheden optimaal te benutten, wordt u aangeraden vertrouwd te raken met deze services en te weten te komen hoe deze werken met [!DNL Catalog].

### [!DNL Experience Data Model] (XDM) System

[!DNL Experience Data Model] (XDM) Het systeem is het gestandaardiseerde kader waardoor de gegevens van de klantenervaring [!DNL Platform] organiseren. [!DNL Experience Platform] hefboomwerkingen XDM schema&#39;s om de structuur van gegevens op een verenigbare en herbruikbare manier te beschrijven.

Wanneer het gegeven in wordt opgenomen [!DNL Platform], wordt de structuur van dat gegeven in kaart gebracht aan een schema XDM en binnen [!DNL Data Lake] als deel van een dataset opgeslagen. De meta-gegevens voor elke dataset wordt gevolgd door [!DNL Catalog Service], die een verwijzing naar het schema XDM omvat dat de dataset met inachtneming is.

Voor meer algemene informatie over XDM System, gelieve te zien het [XDM systeemoverzicht](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] Neemt gegevens van veelvoudige bronnen op en handhaaft verslagen als datasets binnen [!DNL Data Lake]. [!DNL Catalog] volgt de meta-gegevens voor deze datasets, ongeacht hun bron of methode van opname.

Wanneer u de methode voor het toevoegen van batches gebruikt, worden [!DNL Catalog] ook aanvullende metagegevens voor batchbestanden bijgehouden. Batches zijn gegevenseenheden die bestaan uit een of meer bestanden die als één eenheid moeten worden ingevoerd. [!DNL Catalog] volgt de meta-gegevens voor deze partijdossiers, evenals de datasets zij binnen na opname worden voortgeduurd. De meta-gegevens van de partij omvatten informatie over het aantal met succes opgenomen verslagen, evenals om het even welke ontbroken verslagen en bijbehorende foutenmeldingen.

Zie het overzicht [van](../ingestion/home.md) gegevensinvoer voor meer informatie.

## [!DNL Catalog] objecten

Zoals geschetst in de vorige sectie, [!DNL Catalog] volgt meta-gegevens voor verscheidene soorten middelen en verrichtingen die door andere [!DNL Platform] diensten worden gebruikt. [!DNL Catalog] onderhoudt een eigen opslagruimte van &#39;objecten&#39; die deze metagegevens omvat. [!DNL Catalog] de voorwerpen zijn queryable vertegenwoordiging van [!DNL Platform] gegevens die u toestaan om, uw gegevens te zoeken te controleren en te etiketteren zonder het moeten tot de gegevens zelf toegang hebben.

In de volgende tabel worden de verschillende objecttypen weergegeven die worden ondersteund door [!DNL Catalog]:

| Object | API-eindpunt | Definitie |
|---|---|---|
| Account | `/accounts` | Bij het maken van bronverbindingen moeten verificatiereferenties worden opgegeven. Een rekening vertegenwoordigt een inzameling van authentificatiegeloofsbrieven die werden gebruikt om een verbinding van een specifiek type tot stand te brengen. Elke verbinding heeft een reeks unieke parameters die door [!DNL Catalog] en beveiligd in een [!DNL Azure Key Vault]. worden voortgeduurd. |
| Batch | `/batches` | Batches zijn gegevenseenheden die bestaan uit een of meer bestanden die als één eenheid moeten worden ingevoerd. Een batchobject in [!DNL Catalog] contouren de innamemetriek van de batch (zoals het aantal verwerkte records of de grootte op schijf) en kan ook koppelingen naar gegevenssets, weergaven en andere bronnen bevatten die door de batchbewerking zijn beïnvloed. |
| Verbinding | `/connections` | Een verbinding is één enkel geval van een bronschakelaar, uniek aan uw organisatie en gevormd gebruikend de aangewezen authentificatiereferenties voor het schakelaartype. |
| Connector | `/connectors` | De schakelaars bepalen hoe de bronverbindingen gegevens van andere toepassingen van Adobe (zoals Adobe Analytics en Adobe Audience Manager), derdewolkenopslagbronnen (zoals [!DNL Azure Blob], [!DNL Amazon S3], de servers van FTP, en servers SFTP), en de systemen van derdeCRM (zoals [!DNL Microsoft Dynamics] en [!DNL Salesforce]) moeten verzamelen. |
| Gegevensset | `/dataSets` | Een dataset is een opslag en beheersconstructie die voor de inzameling van gegevens (typisch een lijst) wordt gebruikt die een schema (kolommen) en gebieden (rijen) bevat. Zie het overzicht [van](./datasets/overview.md) gegevenssets voor meer informatie. |
| Gegevensbestand | `/datasetFiles` | Gegevensbestanden vertegenwoordigen gegevensblokken waarop is opgeslagen [!DNL Platform]. Als verslagen van letterlijke dossiers, zijn deze waar u de grootte van het dossier, het aantal verslagen kunt vinden het bevat, en een verwijzing naar de partij die het dossier opnam. |

## Volgende stappen

Dit document gaf een inleiding op [!DNL Catalog Service] en hoe het functioneert binnen de grotere reikwijdte van [!DNL Experience Platform]. Zie de [[!DNL Catalog] ontwikkelaarsgids](api/getting-started.md) voor stappen bij het in wisselwerking staan met de verschillende eindpunten van die [!DNL Catalog] API. U wordt aangeraden ook naar de handleiding voor het [filteren van catalogusgegevens](api/filter-data.md) te verwijzen om de best practices voor het beperken van de gegevens die worden geretourneerd in API-reacties te volgen.