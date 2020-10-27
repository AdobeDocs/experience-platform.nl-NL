---
keywords: Experience Platform;home;popular topics;data location;Data Location;Data management;data management;Lineage;lineage;data type;data types;Data types;Data type
solution: Experience Platform
title: Overzicht van gegevenssets
topic: datasets
description: Dit document verstrekt een overzicht op hoog niveau van datasets in Experience Platform.
translation-type: tm+mt
source-git-commit: 1c00456ee06c1fc09c8e4ce070c90255f51811e1
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---


# Overzicht van gegevenssets

Alle gegevens die met succes in Adobe Experience Platform worden opgenomen, blijven binnen de [!DNL Data Lake] gegevensset bestaan. Een dataset is een opslag en beheersconstructie voor een inzameling van gegevens, typisch een lijst, die een schema (kolommen) en gebieden (rijen) bevat. Datasets bevatten ook metagegevens die verschillende aspecten van de gegevens beschrijven die ze opslaan.

Dit document biedt een overzicht op hoog niveau van gegevenssets in [!DNL Experience Platform].

## Gegevenssets maken en metagegevens bijhouden

[!DNL Catalog Service] is het systeem van verslag voor gegevensplaats en lijn binnen [!DNL Experience Platform], en wordt gebruikt om datasets tot stand te brengen en te beheren. [!DNL Catalog] volgt de meta-gegevens voor elke dataset, die een verwijzing naar het [!DNL Experience Data Model] (XDM) schema omvat de dataset aan (verklaard in de volgende sectie) en het aantal verslagen voldoet die in die dataset worden opgenomen.

Zie het overzicht [van de](../home.md) Catalogusservice voor meer informatie.

## Beperkingen van gegevenssetgegevens afdwingen

[!DNL Experience Data Model] (XDM) is het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Platform] georganiseerd. Alle gegevens die in worden opgenomen [!DNL Platform] moeten met een vooraf bepaald schema XDM in overeenstemming zijn alvorens het in [!DNL Data Lake] als dataset kan worden voortgeduurd.

Alle datasets bevatten een verwijzing naar het schema XDM dat het formaat en de structuur van de gegevens beperkt die zij kunnen opslaan. Het proberen om gegevens aan een dataset te uploaden die niet met het schema XDM van de dataset in overeenstemming is zal binnendringen veroorzaken om te ontbreken.

Voor meer informatie over XDM, zie het overzicht [van het](../../xdm/home.md)Systeem XDM.

## Gegevens in gegevenssets invoegen

Adobe Experience Platform Data Ingestie vertegenwoordigt de veelvoudige methodes waardoor gegevens uit diverse bronnen [!DNL Platform] opnemen. Ongeacht de methode van opname, worden alle gegevens met succes omgezet in batchbestanden. Batches zijn gegevenseenheden die bestaan uit een of meer bestanden die als één eenheid moeten worden ingevoerd. Deze partijdossiers worden dan toegevoegd aan specifieke datasets en binnen [!DNL Data Lake]voortgeduurd.

Zie het [Overzicht](../../ingestion/home.md) van de Ingestie van Gegevens voor meer informatie.

## Gebruikslabels toepassen op gegevenssets

Met Adobe Experience Platform [!DNL Data Governance] kunt u klantgegevens beheren om ervoor te zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op het gebruik van gegevens worden nageleefd. Met het [!DNL Data Governance] framework kunt u gebruikslabels toepassen om gegevens te categoriseren volgens het gebruiksbeleid dat op die gegevens van toepassing is.

De etiketten van het gebruik van gegevens kunnen op volledige datasets of individuele datasetgebieden worden toegepast. De etiketten die op het datasetniveau worden toegevoegd worden geërft door alle gebieden binnen die dataset.

Zie het overzicht [van](../../data-governance/home.md) Gegevensbeheer voor meer informatie over de dienst. Raadpleeg de volgende hulplijnen voor stappen over het werken met gebruikslabels in [!DNL Platform]:

* [Labels beheren in de gebruikersinterface](../../data-governance/labels/user-guide.md)
* [Gegevenssetlabels beheren in de API](../../data-governance/labels/dataset-api.md)

## Gegevensbestanden in downstream- [!DNL Platform] services

Zodra de datasets zijn gebruikt om ingebedde gegevens op te slaan, worden die datasets dan gebruikt door stroomafwaartse [!DNL Platform] diensten om klantenprofielen bij te werken, inzichten door machine het leren te bereiken, en meer.

Hieronder volgt een lijst met downstreamservices die gegevenssets gebruiken voor diverse bewerkingen. Raadpleeg de documentatie bij elke service voor meer informatie.

* [[!DNL Data Access API]](../../data-access/home.md): Staat u toe om tot de inhoud van dossiers toegang te hebben en te downloaden die binnen datasets worden opgeslagen.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Bruggen identiteiten over apparaten en systemen, die datasets verbinden samen op de identiteitsgebieden worden bepaald die door de schema&#39;s XDM worden bepaald zij met in overeenstemming zijn.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Hefboomwerkingen [!DNL Identity Service] om gedetailleerde klantenprofielen van uw datasets in real time tot stand te brengen. [!DNL Real-time Customer Profile] trekt gegevens van de klant [!DNL Data Lake] en voortduurt klantenprofielen in zijn eigen afzonderlijke gegevensopslag.
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md): Staat u toe om segmenten te bouwen en publiek van uw [!DNL Real-time Customer Profile] gegevens te produceren. Deze doelgroepen kunnen vervolgens worden geëxporteerd naar hun eigen gegevensbestanden in de [!DNL Data Lake]map.
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md): Gebruikt machinaal leren en kunstmatige intelligentie om inzichten in grote datasets te ontdekken.
* [Adobe Experience Platform Query Service](../../query-service/home.md): Staat u toe om standaardSQL aan vraaggegevens binnen te gebruiken, die tot om het even welke datasets binnen de [!DNL Experience Platform]en het vangen van vraagresultaten als nieuwe dataset voor gebruik in het melden, [!DNL Data Lake] of [!DNL Data Science Workspace][!DNL Real-time Customer Profile]toetreden.

## Volgende stappen

Door dit document te lezen, bent u geïntroduceerd aan het kerngebruik van datasets in [!DNL Experience Platform], evenals de diverse [!DNL Platform] diensten die datasets gebruiken. Voor meer details over de vele manieren worden de datasets gebruikt in [!DNL Platform], te herzien gelieve de de dienstdocumentatie verbonden door dit overzicht.

Voor stappen op hoe te met datasets binnen [!DNL Experience Platform] UI in wisselwerking te staan, zie de de gebruikersgids [van de](user-guide.md)datasets.