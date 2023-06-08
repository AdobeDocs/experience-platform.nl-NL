---
keywords: Experience Platform;home;populaire onderwerpen;catalogusservice;catalogus;Catalogusservice;gegevenslocatie;Gegevenslocatie;Gegevensbeheer;Lineage;Lijn;Catalogus;Gegevensset inschakelen
solution: Experience Platform
title: Overzicht van Catalog Service
description: Catalogusservice is het systeem voor het vastleggen van de locatie van gegevens en de verbinding in Adobe Experience Platform. Terwijl alle gegevens die in Experience Platform worden opgenomen in het meer van Gegevens als dossiers en folders worden opgeslagen, houdt de Catalogus de meta-gegevens en de beschrijving van die dossiers en folders voor raadpleging en controledoeleinden.
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
source-git-commit: 0ebe9eadb1bce6252b43a50af009ce1b0f6e5d6e
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---

# [!DNL Catalog Service]-overzicht

[!DNL Catalog Service] is het registratiesysteem voor gegevenslocatie en -lijn in Adobe Experience Platform. Terwijl alle gegevens waarin [!DNL Experience Platform] wordt opgeslagen in het dialoogvenster [!DNL Data Lake] als bestanden en mappen, [!DNL Catalog] bevat de metagegevens en een beschrijving van deze bestanden en mappen voor opzoekings- en controledoeleinden.

Eenvoudig gezegd, [!DNL Catalog] fungeert als een opslagplaats voor metagegevens of als een &quot;catalogus&quot; waarin u informatie over uw gegevens kunt vinden binnen [!DNL Experience Platform]. U kunt [!DNL Catalog] om de volgende vragen te beantwoorden :

* Waar bevinden mijn gegevens zich?
* In welk stadium van verwerking bevinden deze gegevens zich?
* Welke systemen of processen hebben op mijn gegevens gehandeld?
* Hoeveel gegevens zijn verwerkt?
* Welke fouten zijn tijdens de verwerking opgetreden?

[!DNL Catalog] verstrekt een RESTful API die u toestaat programmatically te beheren [!DNL Platform] metagegevens met behulp van standaard-CRUD-bewerkingen. Zie de [Handleiding voor ontwikkelaars van catalogi](api/getting-started.md) voor meer informatie .

## [!DNL Catalog] en [!DNL Experience Platform] diensten

De middelen die [!DNL Catalog Service] tracks worden door meerdere [!DNL Experience Platform] diensten. Om de [!DNL Catalog's] mogelijkheden, adviseert men dat u vertrouwd met deze diensten wordt en hoe zij met [!DNL Catalog].

### [!DNL Experience Data Model] (XDM) System

[!DNL Experience Data Model] (XDM) Systeem is het gestandaardiseerde kader waardoor [!DNL Platform] organiseert de gegevens van de klantenervaring. [!DNL Experience Platform] hefboomwerkingen XDM schema&#39;s om de structuur van gegevens op een verenigbare en herbruikbare manier te beschrijven.

Wanneer gegevens worden ingevoerd in [!DNL Platform], wordt de structuur van die gegevens toegewezen aan een XDM-schema en opgeslagen binnen het [!DNL Data Lake] als onderdeel van een gegevensset. De metagegevens voor elke gegevensset worden bijgehouden door [!DNL Catalog Service], die een verwijzing naar het XDM-schema omvat waaraan de dataset voldoet.

Voor meer algemene informatie over XDM System, gelieve te zien [XDM System, overzicht](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] neemt gegevens van veelvoudige bronnen op en handhaaft verslagen als datasets binnen [!DNL Data Lake]. [!DNL Catalog] volgt de meta-gegevens voor deze datasets, ongeacht hun bron of methode van opname.

Bij gebruik van de methode voor het toevoegen van batches, [!DNL Catalog] controleert ook extra meta-gegevens voor partijdossiers. Batches zijn gegevenseenheden die bestaan uit een of meer bestanden die als één eenheid moeten worden ingevoerd. [!DNL Catalog] volgt de meta-gegevens voor deze partijdossiers, evenals de datasets zij binnen na opname worden voortgeduurd. De meta-gegevens van de partij omvatten informatie over het aantal met succes opgenomen verslagen, evenals om het even welke ontbroken verslagen en bijbehorende foutenmeldingen.

Zie de [gegevensinvoer - overzicht](../ingestion/home.md) voor meer informatie .

## [!DNL Catalog] objecten

Zoals in het vorige deel is uiteengezet, [!DNL Catalog] controleert meta-gegevens voor verscheidene soorten middelen en verrichtingen die door andere worden gebruikt [!DNL Platform] diensten. [!DNL Catalog] onderhoudt een eigen opslagruimte van &#39;objecten&#39; die deze metagegevens omvat. [!DNL Catalog] objecten zijn leesbare representaties van [!DNL Platform] gegevens waarmee u uw gegevens kunt zoeken, controleren en labelen zonder dat u toegang hoeft te krijgen tot de gegevens zelf.

In de volgende tabel worden de verschillende objecttypen beschreven die worden ondersteund door [!DNL Catalog]:

| Object | API-eindpunt | Definitie |
|---|---|---|
| Batch | `/batches` | Batches zijn gegevenseenheden die bestaan uit een of meer bestanden die als één eenheid moeten worden ingevoerd. Een batchobject in [!DNL Catalog] schetst de de innamemetriek van de partij (zoals het aantal verwerkte verslagen of grootte op schijf) en kan verbindingen aan datasets, meningen, en andere middelen omvatten die door de partijverrichting werden beïnvloed. |
| Gegevensset | `/dataSets` | Een dataset is een opslag en beheersconstructie die voor de inzameling van gegevens (typisch een lijst) wordt gebruikt die een schema (kolommen) en gebieden (rijen) bevat. Zie de [Overzicht van gegevenssets](./datasets/overview.md) voor meer informatie . |
| Gegevensbestand | `/datasetFiles` | Gegevensbestanden vertegenwoordigen gegevensblokken waarop is opgeslagen [!DNL Platform]. Als verslagen van letterlijke dossiers, zijn deze waar u de grootte van het dossier, het aantal verslagen kunt vinden het bevat, en een verwijzing naar de partij die het dossier opnam. |

## Volgende stappen

In dit document werd een inleiding gegeven op [!DNL Catalog Service] en hoe het functioneert binnen de grotere reikwijdte van [!DNL Experience Platform]. Zie de [[!DNL Catalog] ontwikkelaarsgids](api/getting-started.md) voor stappen voor interactie met de verschillende eindpunten van dat [!DNL Catalog] API. U wordt aangeraden ook de handleiding op [catalogusgegevens filteren](api/filter-data.md) om de best practices voor het beperken van de gegevens die worden geretourneerd in API-reacties te volgen.
