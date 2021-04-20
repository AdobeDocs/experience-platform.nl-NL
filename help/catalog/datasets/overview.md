---
keywords: Experience Platform;home;populaire onderwerpen;gegevenslocatie;Gegevenslocatie;Gegevensbeheer;gegevensbeheer;Lineaire;lengte;gegevenstype;gegevenstypen;Gegevenstypen;Gegevenstype
solution: Experience Platform
title: Overzicht van gegevenssets
topic: datasets
description: Dit document verstrekt een overzicht op hoog niveau van datasets in Experience Platform.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 0%

---


# Overzicht van gegevenssets

Alle gegevens die met succes in Adobe Experience Platform worden opgenomen, blijven binnen [!DNL Data Lake] als datasets voortbestaan. Een dataset is een opslag en beheersconstructie voor een inzameling van gegevens, typisch een lijst, die een schema (kolommen) en gebieden (rijen) bevat. Datasets bevatten ook metagegevens die verschillende aspecten van de gegevens beschrijven die ze opslaan.

Dit document biedt een overzicht op hoog niveau van gegevenssets in [!DNL Experience Platform].

## Gegevenssets maken en metagegevens bijhouden

[!DNL Catalog Service] is het systeem van verslag voor gegevensplaats en lijn binnen  [!DNL Experience Platform], en wordt gebruikt om datasets tot stand te brengen en te beheren. [!DNL Catalog] volgt de meta-gegevens voor elke dataset, die een verwijzing naar het  [!DNL Experience Data Model] (XDM) schema omvat de dataset aan (verklaard in de volgende sectie) en het aantal verslagen voldoet die in die dataset worden opgenomen.

Zie [Overzicht van de Catalogusservice](../home.md) voor meer informatie.

## Beperkingen van gegevenssetgegevens afdwingen

[!DNL Experience Data Model] (XDM) is het gestandaardiseerde kader waardoor de gegevens van de klantenervaring  [!DNL Platform] organiseren. Alle gegevens die in [!DNL Platform] worden opgenomen moeten met een vooraf bepaald schema XDM in overeenstemming zijn alvorens het in [!DNL Data Lake] als dataset kan worden voortgeduurd.

Alle datasets bevatten een verwijzing naar het schema XDM dat het formaat en de structuur van de gegevens beperkt die zij kunnen opslaan. Het proberen om gegevens aan een dataset te uploaden die niet met het schema XDM van de dataset in overeenstemming is zal binnendringen veroorzaken om te ontbreken.

Voor meer informatie over XDM, zie [XDM System overview](../../xdm/home.md).

## Gegevens in gegevenssets invoegen

Adobe Experience Platform Data Ingestie vertegenwoordigt de veelvoudige methodes waardoor [!DNL Platform] gegevens uit diverse bronnen opneemt. Ongeacht de methode van opname, worden alle gegevens met succes omgezet in batchbestanden. Batches zijn gegevenseenheden die bestaan uit een of meer bestanden die als één eenheid moeten worden ingevoerd. Deze partijdossiers worden dan toegevoegd aan specifieke datasets en binnen [!DNL Data Lake] voortgeduurd.

Zie [Overzicht van de Ingestie van Gegevens](../../ingestion/home.md) voor meer informatie.

## Gebruikslabels toepassen op gegevenssets

Met Adobe Experience Platform [!DNL Data Governance] kunt u klantgegevens beheren om ervoor te zorgen dat wordt voldaan aan de voorschriften, beperkingen en beleidsregels die van toepassing zijn op het gebruik van gegevens. Met het [!DNL Data Governance]-framework kunt u gebruikslabels toepassen om gegevens te categoriseren volgens het gebruiksbeleid dat op die gegevens van toepassing is.

De etiketten van het gebruik van gegevens kunnen op volledige datasets of individuele datasetgebieden worden toegepast. De etiketten die op het datasetniveau worden toegevoegd worden geërft door alle gebieden binnen die dataset.

Zie [Overzicht van gegevensbeheer](../../data-governance/home.md) voor meer informatie over de service. Raadpleeg de volgende hulplijnen voor informatie over het werken met gebruikslabels in [!DNL Platform]:

* [Labels beheren in de gebruikersinterface](../../data-governance/labels/user-guide.md)
* [Gegevenssetlabels beheren in de API](../../data-governance/labels/dataset-api.md)

## Datasets in downstreamservices [!DNL Platform]

Zodra datasets zijn gebruikt om ingebedde gegevens op te slaan, worden die datasets dan gebruikt door stroomafwaartse [!DNL Platform] diensten om klantenprofielen bij te werken, inzichten door machine het leren te bereiken, en meer.

Hieronder volgt een lijst met downstreamservices die gegevenssets gebruiken voor diverse bewerkingen. Raadpleeg de documentatie bij elke service voor meer informatie.

* [[!DNL Data Access API]](../../data-access/home.md): Staat u toe om tot de inhoud van dossiers toegang te hebben en te downloaden die binnen datasets worden opgeslagen.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Bruggen identiteiten over apparaten en systemen, die datasets verbinden samen op de identiteitsgebieden worden bepaald die door de schema&#39;s XDM worden bepaald zij met in overeenstemming zijn.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Hefboomwerkingen  [!DNL Identity Service] om gedetailleerde klantenprofielen van uw datasets in real time tot stand te brengen. [!DNL Real-time Customer Profile] trekt gegevens van de klant  [!DNL Data Lake] en persisteert klantenprofielen in zijn eigen afzonderlijke gegevensopslag.
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md): Staat u toe om segmenten te bouwen en publiek van uw  [!DNL Real-time Customer Profile] gegevens te produceren. Deze doelgroepen kunnen vervolgens naar hun eigen gegevensbestanden worden geëxporteerd binnen de [!DNL Data Lake].
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md): Gebruikt machinaal leren en kunstmatige intelligentie om inzichten in grote datasets te ontdekken.
* [Adobe Experience Platform Query Service](../../query-service/home.md): Staat u toe om standaardSQL aan vraaggegevens binnen te gebruiken, die tot om het even welke datasets binnen de  [!DNL Experience Platform]en het vangen vraagresultaten als nieuwe dataset voor gebruik in het melden,  [!DNL Data Lake] of  [!DNL Data Science Workspace]  [!DNL Real-time Customer Profile]. toetreden.

## Volgende stappen

Door dit document te lezen, bent u geïntroduceerd aan de belangrijkste toepassingen van datasets in [!DNL Experience Platform], evenals de diverse [!DNL Platform] diensten die datasets gebruiken. Voor meer informatie over de vele manieren worden de datasets gebruikt in [!DNL Platform], te herzien gelieve de de dienstdocumentatie verbonden door dit overzicht.

Voor stappen op hoe te met datasets binnen [!DNL Experience Platform] UI in wisselwerking te staan, zie [datasets gebruikersgids](user-guide.md).