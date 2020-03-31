---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Overzicht van gegevenssets
topic: datasets
translation-type: tm+mt
source-git-commit: 06733eb374d1b9409102a7cf13d61ed266cedaad

---


# Overzicht van gegevenssets

Alle gegevens die met succes in het Platform van de Ervaring van Adobe worden opgenomen blijven binnen het meer van Gegevens als datasets. Een dataset is een opslag en beheersconstructie voor een inzameling van gegevens, typisch een lijst, die een schema (kolommen) en gebieden (rijen) bevat. Datasets bevatten ook metagegevens die verschillende aspecten van de gegevens beschrijven die ze opslaan.

Dit document verstrekt een overzicht op hoog niveau van datasets in het Platform van de Ervaring.

## Gegevenssets maken en metagegevens bijhouden

De Dienst van de Catalogus is het systeem van verslag voor gegevensplaats en lijn binnen het Platform van de Ervaring, en wordt gebruikt om datasets tot stand te brengen en te beheren. De catalogus volgt de meta-gegevens voor elke dataset, die een verwijzing naar het schema van de Gegevens van de Ervaring (XDM) omvat de dataset aan (verklaard in de volgende sectie) en het aantal verslagen voldoet die in die dataset worden opgenomen.

Zie het overzicht [van de](../home.md) Catalogusservice voor meer informatie.

## Beperkingen van gegevenssetgegevens afdwingen

Het Model van Gegevens van de ervaring (XDM) is het gestandaardiseerde kader waardoor het Platform gegevens van de klantenervaring organiseert. Alle gegevens die in Platform worden opgenomen moeten met een vooraf bepaald schema XDM in overeenstemming zijn alvorens het in het meer van Gegevens als dataset kan worden voortgeduurd.

Alle datasets bevatten een verwijzing naar het schema XDM dat het formaat en de structuur van de gegevens beperkt die zij kunnen opslaan. Het proberen om gegevens aan een dataset te uploaden die niet met het schema XDM van de dataset in overeenstemming is zal binnendringen veroorzaken om te ontbreken.

Voor meer informatie over XDM, zie het overzicht [van het](../../xdm/home.md)Systeem XDM.

## Gegevens in gegevenssets invoegen

De Opname van de Gegevens van het Platform van de Ervaring van Adobe vertegenwoordigt de veelvoudige methodes waardoor Platform gegevens uit diverse bronnen opneemt. Ongeacht de methode van opname, worden alle gegevens met succes omgezet in batchbestanden. Batches zijn gegevenseenheden die bestaan uit een of meer bestanden die als één eenheid moeten worden ingevoerd. Deze partijdossiers worden dan toegevoegd aan specifieke datasets en voortgeduurd binnen het meer van Gegevens.

Zie het [Overzicht](../../ingestion/home.md) van de Ingestie van Gegevens voor meer informatie.

## Gebruikslabels toepassen op gegevenssets

Met de gegevensbeheer van het Adobe Experience Platform kunt u klantgegevens beheren om ervoor te zorgen dat de voorschriften, beperkingen en beleidsregels die van toepassing zijn op het gebruik van gegevens worden nageleefd. Gebruikend de Etikettering en de Handhaving van het Gebruik van Gegevens (DULE) als zijn kernkader, staat het Beleid van Gegevens u toe om gebruiksetiketten toe te passen om gegevens volgens het gebruiksbeleid te categoriseren dat op die gegevens van toepassing is.

De etiketten van het gebruik van gegevens kunnen op volledige datasets of individuele datasetgebieden worden toegepast. De etiketten die op het datasetniveau worden toegevoegd worden geërft door alle gebieden binnen die dataset.

Zie het overzicht [van](../../data-governance/home.md) Gegevensbeheer voor meer informatie over de dienst. Voor stappen op hoe te met gebruiksetiketten in de UI van het Platform van de Ervaring te werken, zie de de etiketgebruikersgids [van het](../../data-governance/labels/user-guide.md)gegevensgebruik.

## Gegevensbestanden in downstream Platform-services

Zodra de datasets zijn gebruikt om ingebedde gegevens op te slaan, worden die datasets dan gebruikt door de stroomafwaartse diensten van het Platform om klantenprofielen bij te werken, inzichten door machine het leren te bereiken, en meer.

Hieronder volgt een lijst met downstreamservices die gegevenssets gebruiken voor diverse bewerkingen. Raadpleeg de documentatie bij elke service voor meer informatie.

* [API](../../data-access/home.md)voor gegevenstoegang: Staat u toe om tot de inhoud van dossiers toegang te hebben en te downloaden die binnen datasets worden opgeslagen.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Bruggen identiteiten over apparaten en systemen, die datasets verbinden samen op de identiteitsgebieden worden bepaald die door de schema&#39;s XDM worden bepaald zij met in overeenstemming zijn.
* [Klantprofiel](../../profile/home.md)in realtime: Gebruikt de Dienst van de Identiteit om gedetailleerde klantenprofielen van uw datasets in real time tot stand te brengen. De Klant in real time trekt gegevens van het meer van Gegevens en handhaaft klantenprofielen in zijn eigen afzonderlijke gegevensopslag.
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md): Staat u toe om segmenten te bouwen en publiek van uw gegevens van het Profiel van de Klant in real time te produceren. Deze doelgroepen kunnen vervolgens naar hun eigen gegevensbestanden worden geëxporteerd binnen het Data Lake.
* [Werkruimte](../../data-science-workspace/home.md)voor gegevenswetenschap van Adobe Experience Platform: Gebruikt machinaal leren en kunstmatige intelligentie om inzichten in grote datasets te ontdekken.
* [Adobe Experience Platform Query Service](../../query-service/home.md): Staat u toe om standaardSQL aan vraaggegevens in het Platform van de Ervaring te gebruiken, die tot om het even welke datasets binnen het meer van Gegevens toetreden en vraagresultaten als nieuwe dataset voor gebruik in rapportering, de Werkruimte van de Wetenschap van Gegevens, of het Profiel van de Klant in real time vangen.
* [Adobe Experience Platform Decisioning Service](../../decisioning-service/home.md): Gebruikt het Profiel van de Klant in real time om de meest waarschijnlijke keus te bepalen een klant van een reeks opties zal maken, die op de gedragsgegevens wordt gebaseerd die het Profiel van toegelaten datasets trekt.

## Volgende stappen

Door dit document te lezen, bent u geïntroduceerd aan het kerngebruik van datasets in het Platform van de Ervaring, evenals de diverse diensten van het Platform die datasets gebruiken. Voor meer details over de vele manieren worden de datasets gebruikt in Platform, te herzien gelieve de de dienstdocumentatie verbonden door dit overzicht.

Voor stappen op hoe te met datasets binnen het Platform van de Ervaring in wisselwerking te staan UI, zie de [datasets gebruikersgids](user-guide.md).