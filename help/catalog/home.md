---
keywords: Experience Platform;home;populaire onderwerpen;catalogusservice;catalogus;Catalogusservice;gegevenslocatie;Gegevenslocatie;Gegevensbeheer;Lineage;Lijn;Catalogus;Gegevensset inschakelen
solution: Experience Platform
title: Overzicht van Catalog Service
description: Catalogusservice is het systeem voor het vastleggen van de locatie van gegevens en de gegevensverbinding in Adobe Experience Platform. Terwijl alle gegevens die in Experience Platform worden opgenomen in het meer van Gegevens als dossiers en folders worden opgeslagen, houdt de Catalogus de meta-gegevens en de beschrijving van die dossiers en folders voor raadpleging en controledoeleinden.
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
source-git-commit: 0ebe9eadb1bce6252b43a50af009ce1b0f6e5d6e
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---

# [!DNL Catalog Service]-overzicht

[!DNL Catalog Service] is het recordsysteem voor de gegevenslocatie en -lijn in Adobe Experience Platform. Hoewel alle gegevens die in [!DNL Experience Platform] worden opgenomen, in [!DNL Data Lake] als bestanden en mappen worden opgeslagen, bevat [!DNL Catalog] de metagegevens en een beschrijving van deze bestanden en mappen voor opzoekings- en controledoeleinden.

Eenvoudig gesteld, [!DNL Catalog] dienst als meta-gegevensopslag of &quot;catalogus&quot;waar u informatie over uw gegevens binnen [!DNL Experience Platform] kunt vinden. U kunt [!DNL Catalog] gebruiken om de volgende vragen te beantwoorden:

* Waar bevinden mijn gegevens zich?
* In welk stadium van verwerking bevinden deze gegevens zich?
* Welke systemen of processen hebben op mijn gegevens gehandeld?
* Hoeveel gegevens zijn verwerkt?
* Welke fouten zijn tijdens de verwerking opgetreden?

[!DNL Catalog] biedt een RESTful-API waarmee u [!DNL Platform] -metagegevens programmatisch kunt beheren met behulp van standaard-CRUD-bewerkingen. Zie de [ de ontwikkelaarsgids van de Catalogus ](api/getting-started.md) voor meer informatie.

## [!DNL Catalog] en [!DNL Experience Platform] services

De bronnen die [!DNL Catalog Service] tracks gebruiken, worden door meerdere [!DNL Experience Platform] -services gebruikt. Als u de mogelijkheden van [!DNL Catalog's] optimaal wilt benutten, is het raadzaam bekend te raken met deze services en te weten hoe deze werken met [!DNL Catalog] .

### [!DNL Experience Data Model] (XDM)-systeem

[!DNL Experience Data Model] (XDM) System is het gestandaardiseerde framework waarmee [!DNL Platform] gegevens over de klantervaring organiseert. [!DNL Experience Platform] gebruikt XDM-schema&#39;s om de gegevensstructuur op een consistente en herbruikbare manier te beschrijven.

Wanneer gegevens in [!DNL Platform] worden opgenomen, wordt de structuur van die gegevens toegewezen aan een XDM-schema en in [!DNL Data Lake] opgeslagen als onderdeel van een dataset. De meta-gegevens voor elke dataset worden gevolgd door [!DNL Catalog Service], die een verwijzing naar het XDM schema omvat dat de dataset met in overeenstemming is.

Voor meer algemene informatie over Systeem XDM, gelieve te zien het [ XDM overzicht van het Systeem ](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] neemt gegevens van veelvoudige bronnen op en handhaaft verslagen als datasets binnen [!DNL Data Lake]. [!DNL Catalog] volgt de meta-gegevens voor deze datasets, ongeacht hun bron of methode van opname.

Wanneer u de batchinvoermethode gebruikt, worden in [!DNL Catalog] ook aanvullende metagegevens voor batchbestanden bijgehouden. Batches zijn gegevenseenheden die bestaan uit een of meer bestanden die als één eenheid moeten worden ingevoerd. [!DNL Catalog] volgt de meta-gegevens voor deze partijdossiers, evenals de datasets zij binnen na opname worden voortgeduurd. De meta-gegevens van de partij omvatten informatie over het aantal met succes opgenomen verslagen, evenals om het even welke ontbroken verslagen en bijbehorende foutenmeldingen.

Zie het [ overzicht van de gegevensopname ](../ingestion/home.md) voor meer informatie.

## [!DNL Catalog] objecten

Zoals in de vorige sectie wordt beschreven, houdt [!DNL Catalog] metagegevens bij voor verschillende soorten bronnen en bewerkingen die door andere [!DNL Platform] -services worden gebruikt. [!DNL Catalog] behoudt een eigen opslagruimte van &#39;objecten&#39; die deze metagegevens inkapselen. [!DNL Catalog] -objecten zijn queryable-representaties van [!DNL Platform] -gegevens waarmee u gegevens kunt zoeken, controleren en labelen zonder dat u toegang hoeft te krijgen tot de gegevens zelf.

In de volgende tabel worden de verschillende objecttypen weergegeven die worden ondersteund door [!DNL Catalog] :

| Object | API-eindpunt | Definitie |
|---|---|---|
| Batch | `/batches` | Batches zijn gegevenseenheden die bestaan uit een of meer bestanden die als één eenheid moeten worden ingevoerd. Een batchobject in [!DNL Catalog] beschrijft de innamemetriek van de batch (zoals het aantal verwerkte records of de grootte op schijf) en kan ook koppelingen bevatten naar gegevenssets, weergaven en andere bronnen die door de batchbewerking zijn beïnvloed. |
| Gegevensset | `/dataSets` | Een dataset is een opslag en beheersconstructie die voor de inzameling van gegevens (typisch een lijst) wordt gebruikt die een schema (kolommen) en gebieden (rijen) bevat. Zie het [ overzicht van datasets ](./datasets/overview.md) voor meer informatie. |
| Gegevensbestand | `/datasetFiles` | Gegevensbestanden vertegenwoordigen gegevensblokken die zijn opgeslagen op [!DNL Platform] . Als verslagen van letterlijke dossiers, zijn deze waar u de grootte van het dossier, het aantal verslagen kunt vinden het bevat, en een verwijzing naar de partij die het dossier opnam. |

## Volgende stappen

Dit document biedt een inleiding tot [!DNL Catalog Service] en de manier waarop het werkt binnen het grotere bereik van [!DNL Experience Platform] . Zie de [[!DNL Catalog]  ontwikkelaarsgids ](api/getting-started.md) voor stappen bij het in wisselwerking staan met de verschillende eindpunten van dat [!DNL Catalog] API. Het wordt geadviseerd dat u ook naar de gids op [ het filtreren gegevens van de Catalogus ](api/filter-data.md) verwijst om beste praktijken te volgen voor het beperken van de gegevens die in API reacties zijn teruggekeerd.
