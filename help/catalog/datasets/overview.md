---
keywords: Experience Platform;home;populaire onderwerpen;gegevenslocatie;Gegevenslocatie;Gegevensbeheer;gegevensbeheer;Lineaire;lengte;gegevenstype;gegevenstypen;Gegevenstypen;Gegevenstype
solution: Experience Platform
title: Overzicht van gegevenssets
description: Dit document biedt een overzicht op hoog niveau van gegevenssets in Experience Platform.
user-guide-description: Krijg een overzicht op hoog niveau van datasets in Experience Platform met deze gids. Leer hoe te om hen tot stand te brengen, beperkingen op gegevens af te dwingen en gegevens in datasets hier in te voeren.
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 1%

---

# Overzicht van gegevenssets

Alle gegevens die met succes in Adobe Experience Platform worden opgenomen, blijven binnen [!DNL Data Lake] als datasets bestaan. Een dataset is een opslag en beheersconstructie voor een inzameling van gegevens, typisch een lijst, die een schema (kolommen) en gebieden (rijen) bevat. Datasets bevatten ook metagegevens die verschillende aspecten van de gegevens beschrijven die ze opslaan.

Dit document biedt een overzicht op hoog niveau van gegevenssets in [!DNL Experience Platform] .

## Gegevenssets maken en metagegevens bijhouden

[!DNL Catalog Service] is het recordsysteem voor de gegevenslocatie en -lijn binnen [!DNL Experience Platform] en wordt gebruikt om gegevenssets te maken en te beheren. [!DNL Catalog] volgt de meta-gegevens voor elke dataset, die een verwijzing naar het [!DNL Experience Data Model] (XDM) schema omvat de dataset aan (verklaard in de volgende sectie) en het aantal verslagen voldoet die in die dataset worden opgenomen.

Zie het [ overzicht van de Dienst van de Catalogus ](../home.md) voor meer informatie.

## Beperkingen van gegevenssetgegevens afdwingen

[!DNL Experience Data Model] (XDM) is het gestandaardiseerde framework waarmee [!DNL Experience Platform] gegevens voor de klantervaring indeelt. Alle gegevens die in [!DNL Experience Platform] worden opgenomen, moeten in overeenstemming zijn met een vooraf gedefinieerd XDM-schema voordat het in [!DNL Data Lake] als dataset kan worden voortgezet.

Alle datasets bevatten een verwijzing naar het schema XDM dat het formaat en de structuur van de gegevens beperkt die zij kunnen opslaan. Het proberen om gegevens aan een dataset te uploaden die niet met het schema XDM van de dataset in overeenstemming is zal binnendringen veroorzaken om te ontbreken.

Voor meer informatie over XDM, zie het [ XDM overzicht van het Systeem ](../../xdm/home.md).

## Gegevens in gegevenssets invoegen

Adobe Experience Platform Data Ingestie vertegenwoordigt de meerdere methoden waarmee [!DNL Experience Platform] gegevens uit verschillende bronnen inneemt. Ongeacht de manier van inname worden alle gegevens die correct zijn ingesloten, geconverteerd naar batchbestanden. Batches zijn gegevenseenheden die bestaan uit een of meer bestanden die als één eenheid moeten worden ingevoerd. Deze partijdossiers worden dan toegevoegd aan specifieke datasets en binnen [!DNL Data Lake] voortgeduurd.

Zie het [ Overzicht van de Ingestie van Gegevens ](../../ingestion/home.md) voor meer informatie.

## Labels die worden toegepast op gegevenssets van schema&#39;s

Met Adobe Experience Platform Data Governance kunt u klantgegevens beheren om ervoor te zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op het gebruik van gegevens worden nageleefd. Met het gegevensbeheerframework kunt u gebruikslabels toepassen om gegevens te categoriseren volgens het gebruiksbeleid dat op die gegevens van toepassing is. De etiketten kunnen op individuele schema&#39;s, gebieden binnen die schema&#39;s, en volledige individuele datasets worden toegepast. Wanneer de etiketten rechtstreeks op een schema worden toegepast, worden die etiketten verspreid aan alle bestaande en toekomstige datasets die op dat schema gebaseerd zijn.

>[!IMPORTANT]
>
>Labels kunnen niet meer worden toegepast op velden op het niveau van de gegevensset. Deze workflow is vervangen door labels op schemaniveau. Alle labels die eerder op het niveau van gegevenssetobjecten zijn toegepast, worden tot 31 mei 2024 nog steeds ondersteund via de gebruikersinterface van Experience Platform. Om ervoor te zorgen dat uw etiketten over alle schema&#39;s verenigbaar zijn, moeten om het even welke etiketten die eerder aan gebieden op het datasetniveau worden vastgemaakt door u over het komende jaar worden gemigreerd aan het schemaniveau. Zie de sectie op [ migrerend eerder toegepaste etiketten ](../../data-governance/e2e.md#migrate-labels) voor instructies op hoe te om dit te doen.

Zie het [ overzicht van het Beleid van Gegevens ](../../data-governance/home.md) voor meer informatie over de dienst. Raadpleeg de volgende hulplijnen voor stappen over het werken met gebruikslabels in [!DNL Experience Platform] :

* [Labels beheren in de gebruikersinterface](../../data-governance/labels/user-guide.md)
* [Gegevenssetlabels beheren in de API](../../data-governance/labels/dataset-api.md)

## Datasets in downstream [!DNL Experience Platform] -services

Zodra de datasets zijn gebruikt om ingebedde gegevens op te slaan, worden die datasets dan gebruikt door stroomafwaartse [!DNL Experience Platform] diensten om klantenprofielen bij te werken, inzichten door machine het leren te bereiken, en meer.

Hieronder volgt een lijst met downstreamservices die gegevenssets gebruiken voor diverse bewerkingen. Raadpleeg de documentatie bij elke service voor meer informatie.

* [[!DNL Data Access API]](../../data-access/home.md): Hiermee kunt u de inhoud van bestanden in gegevenssets openen en downloaden.
* [ Dienst van de Identiteit van Adobe Experience Platform ](../../identity-service/home.md): Brugshanden identiteiten over apparaten en systemen, die datasets verbinden samen op de identiteitsgebieden worden gebaseerd die door de schema&#39;s XDM worden bepaald zij met in overeenstemming zijn.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): maakt gebruik van [!DNL Identity Service] om in real-time gedetailleerde klantprofielen te maken op basis van uw gegevenssets. [!DNL Real-Time Customer Profile] haalt gegevens van [!DNL Data Lake] en houdt klantenprofielen in zijn eigen afzonderlijke gegevensopslag voort.
* [ de Dienst van de Segmentatie van Adobe Experience Platform ](../../segmentation/home.md): Staat u toe om segmenten te bouwen en publiek van uw [!DNL Real-Time Customer Profile] gegevens te produceren. Deze doelgroepen kunnen vervolgens worden geëxporteerd naar hun eigen gegevenssets in de [!DNL Data Lake] .
* [ Workspace van de Wetenschap van Gegevens van Adobe Experience Platform ](../../data-science-workspace/home.md): Gebruikt machine het leren en kunstmatige intelligentie om inzichten in grote datasets te ontdekken.
* [ de Dienst van de Vraag van Adobe Experience Platform ](../../query-service/home.md): Staat u toe om standaardSQL te gebruiken om gegevens in [!DNL Experience Platform] te vragen, die tot om het even welke datasets binnen [!DNL Data Lake] toetreden en vraagresultaten als nieuwe dataset voor gebruik in het melden, [!DNL Data Science Workspace], of [!DNL Real-Time Customer Profile] vangen.
* [ de Dienst van Bestemmingen van Adobe Experience Platform ](../../destinations/home.md): Staat u toe [ uitvoerdatasets ](/help/destinations/ui/export-datasets.md) aan uw gewenste wolkenopslag of e-mail marketing bestemmingen, voor het melden van of activiteiten van de gegevenswetenschap.

## Volgende stappen

Door dit document te lezen, bent u geïntroduceerd in de belangrijkste toepassingen van datasets in [!DNL Experience Platform], evenals de diverse [!DNL Experience Platform] diensten die datasets gebruiken. Voor meer informatie over de vele manieren worden de datasets gebruikt in [!DNL Experience Platform], te herzien gelieve de de dienstdocumentatie verbonden door dit overzicht.

Voor stappen op hoe te met datasets binnen [!DNL Experience Platform] UI in wisselwerking te staan, zie de [ gids van de datasetgebruiker ](user-guide.md).
