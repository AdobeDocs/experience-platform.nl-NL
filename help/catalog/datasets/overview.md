---
keywords: Experience Platform;home;populaire onderwerpen;gegevenslocatie;Gegevenslocatie;Gegevensbeheer;gegevensbeheer;Lineaire;lengte;gegevenstype;gegevenstypen;Gegevenstypen;Gegevenstype
solution: Experience Platform
title: Overzicht van gegevenssets
topic-legacy: datasets
description: Dit document verstrekt een overzicht op hoog niveau van datasets in Experience Platform.
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
source-git-commit: 7e4c2ef8089276829604c9d8a8dd20a122b18c7a
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 0%

---

# Overzicht van gegevenssets

Alle gegevens die met succes in Adobe Experience Platform zijn ingevoerd, blijven behouden in het dialoogvenster [!DNL Data Lake] als datasets. Een dataset is een opslag en beheersconstructie voor een inzameling van gegevens, typisch een lijst, die een schema (kolommen) en gebieden (rijen) bevat. Datasets bevatten ook metagegevens die verschillende aspecten van de gegevens beschrijven die ze opslaan.

Dit document biedt een overzicht op hoog niveau van gegevenssets in [!DNL Experience Platform].

## Gegevenssets maken en metagegevens bijhouden

[!DNL Catalog Service] is het registratiesysteem voor gegevenslocatie en -lijn binnen [!DNL Experience Platform]en wordt gebruikt om gegevenssets te maken en te beheren. [!DNL Catalog] traceert de meta-gegevens voor elke dataset, die een verwijzing naar omvat [!DNL Experience Data Model] (XDM) schema de dataset aan (verklaard in de volgende sectie) en het aantal verslagen voldoet die in die dataset worden opgenomen.

Zie de [Overzicht van Catalog Service](../home.md) voor meer informatie .

## Beperkingen van gegevenssetgegevens afdwingen

[!DNL Experience Data Model] (XDM) is het gestandaardiseerde kader waardoor [!DNL Platform] organiseert de gegevens van de klantenervaring. Alle gegevens waarin [!DNL Platform] moet in overeenstemming zijn met een vooraf gedefinieerd XDM-schema voordat het in het [!DNL Data Lake] als gegevensset.

Alle datasets bevatten een verwijzing naar het schema XDM dat het formaat en de structuur van de gegevens beperkt die zij kunnen opslaan. Het proberen om gegevens aan een dataset te uploaden die niet met het schema XDM van de dataset in overeenstemming is zal binnendringen veroorzaken om te ontbreken.

Voor meer informatie over XDM, zie [XDM System, overzicht](../../xdm/home.md).

## Gegevens in gegevenssets invoegen

Adobe Experience Platform Data Ingestie vertegenwoordigt de veelvoudige methodes waardoor [!DNL Platform] neemt gegevens uit diverse bronnen op. Ongeacht de methode van opname, worden alle gegevens met succes omgezet in batchbestanden. Batches zijn gegevenseenheden die bestaan uit een of meer bestanden die als één eenheid moeten worden ingevoerd. Deze partijdossiers worden dan toegevoegd aan specifieke datasets en voortgeduurd binnen [!DNL Data Lake].

Zie de [Overzicht van gegevensinname](../../ingestion/home.md) voor meer informatie .

## Gebruikslabels toepassen op gegevenssets

Met Adobe Experience Platform Data Governance kunt u klantgegevens beheren om ervoor te zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik worden nageleefd. Met het gegevensbeheerframework kunt u gebruikslabels toepassen om gegevens te categoriseren volgens het gebruiksbeleid dat op die gegevens van toepassing is.

>[!IMPORTANT]
>
>Het toepassen van labels op gegevenssetniveau wordt alleen ondersteund voor gevallen waarin gegevens worden beheerd. Als u probeert toegangsbeleid voor de gegevens tot stand te brengen, moet u [labels toepassen op het schema](../../xdm/tutorials/labels.md) dat de gegevensset op die gegevens is gebaseerd. Zie het overzicht op [attribuut-based toegangsbeheer](../../access-control/abac/overview.md) voor meer informatie .

De etiketten van het gebruik van gegevens kunnen op volledige datasets of individuele datasetgebieden worden toegepast. De etiketten die op het datasetniveau worden toegevoegd worden geërft door alle gebieden binnen die dataset.

Zie de [Overzicht van gegevensbeheer](../../data-governance/home.md) voor meer informatie over de dienst. Voor stappen voor het werken met gebruikslabels in [!DNL Platform]Raadpleeg de volgende hulplijnen:

* [Labels beheren in de gebruikersinterface](../../data-governance/labels/user-guide.md)
* [Gegevenssetlabels beheren in de API](../../data-governance/labels/dataset-api.md)

## Gegevensbestanden in de stroomafwaartse richting [!DNL Platform] diensten

Zodra de datasets zijn gebruikt om opgenomen gegevens op te slaan, worden die datasets dan gebruikt door stroomafwaarts [!DNL Platform] services voor het bijwerken van klantprofielen, het verkrijgen van inzicht door het leren van machines en meer.

Hieronder volgt een lijst met downstreamservices die gegevenssets gebruiken voor diverse bewerkingen. Raadpleeg de documentatie bij elke service voor meer informatie.

* [[!DNL Data Access API]](../../data-access/home.md): Staat u toe om tot de inhoud van dossiers toegang te hebben en te downloaden die binnen datasets worden opgeslagen.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Bruggen identiteiten over apparaten en systemen, die datasets verbinden samen op de identiteitsgebieden worden bepaald die door de schema&#39;s XDM worden bepaald zij met in overeenstemming zijn.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Hefboomwerking [!DNL Identity Service] om gedetailleerde klantenprofielen van uw datasets in real time tot stand te brengen. [!DNL Real-time Customer Profile] Hiermee worden gegevens opgehaald van de [!DNL Data Lake] en blijven klantenprofielen in zijn eigen afzonderlijke gegevensopslag.
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md): Hiermee kunt u segmenten samenstellen en soorten publiek genereren op basis van uw [!DNL Real-time Customer Profile] gegevens. Deze doelgroepen kunnen vervolgens naar hun eigen gegevensbestanden worden geëxporteerd binnen de [!DNL Data Lake].
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md): Gebruikt machinaal leren en kunstmatige intelligentie om inzichten in grote datasets te ontdekken.
* [Adobe Experience Platform Query Service](../../query-service/home.md): Hiermee kunt u standaard-SQL gebruiken om gegevens op te vragen in [!DNL Experience Platform], worden alle gegevenssets binnen de [!DNL Data Lake] en het vangen van vraagresultaten als nieuwe dataset voor gebruik in het melden, [!DNL Data Science Workspace], of [!DNL Real-time Customer Profile].
* [Adobe Experience Platform-bestemmingsservice](../../destinations/home.md): Hiermee kunt u [exportgegevenssets](/help/destinations/ui/export-datasets.md) naar uw gewenste locatie voor cloudopslag of e-mailmarketing, voor rapportage of gegevenswetenschappelijke activiteiten.

## Volgende stappen

Door dit document te lezen, bent u geïntroduceerd in de belangrijkste toepassingen van datasets in [!DNL Experience Platform], alsmede de diverse [!DNL Platform] services die gegevenssets gebruiken. Voor meer details over de vele manieren worden de datasets gebruikt binnen [!DNL Platform], raadpleeg de servicedocumentatie die in dit overzicht is gekoppeld.

Voor stappen op hoe te met datasets binnen interactie te gaan [!DNL Experience Platform] UI, zie [gebruikershandleiding voor gegevenssets](user-guide.md).
