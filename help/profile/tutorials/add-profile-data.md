---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Gegevens toevoegen aan realtime klantprofiel
topic: tutorial
translation-type: tm+mt
source-git-commit: 93aae0e394e1ea9b6089d01c585a94871863818e
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---


# Gegevens toevoegen aan realtime klantprofiel

In deze zelfstudie worden de stappen beschreven die nodig zijn om gegevens toe te voegen aan het realtime profiel van de klant.

## Een schema voor realtime klantprofiel inschakelen

Gegevens die in Experience Platform voor gebruik door het Profiel van de Klant in real time worden opgenomen moeten aan een schema van de Gegevens van de Ervaring (XDM) in overeenstemming zijn dat voor Profiel wordt toegelaten. Een schema kan alleen worden ingeschakeld voor Profiel als het de klasse XDM Individual Profile of XDM ExperienceEvent implementeert.

U kunt een schema voor gebruik in het Profiel van de Klant in real time toelaten gebruikend de Registratie API van het Schema of het gebruikersinterface van de Redacteur van het Schema. Om te beginnen, volg de leerprogramma&#39;s voor het [creëren van een schema gebruikend APIs](../../xdm/tutorials/create-schema-api.md) of [creërend een schema gebruikend de Redacteur van het Schema UI](../../xdm/tutorials/create-schema-ui.md).

## Gegevens toevoegen met batch-opname

Alle gegevens die met batch-opname naar het Platform zijn geüpload, worden geüpload naar afzonderlijke gegevenssets. Alvorens deze gegevens door het Profiel van de Klant in real time kunnen worden gebruikt, moet de dataset in kwestie specifiek worden gevormd. Voor volledige instructies, zie de zelfstudie over het [vormen van een dataset voor de Dienst](dataset-configuration.md)van het Profiel en van de Identiteit.

Zodra de dataset is gevormd, kunt u beginnen gegevens in het op te nemen. Zie de handleiding voor [het ontwikkelen van](../../ingestion/batch-ingestion/api-overview.md) batches voor gedetailleerde stappen over het uploaden van bestanden in verschillende indelingen.

## Gegevens toevoegen met streaming opname

Om het even welke stroom-ingebedde gegevens die met een profiel-toegelaten XDM schema volgden zullen automatisch het aangewezen verslag in het Profiel van de Klant in real time toevoegen of overschrijven. Als er meer dan één identiteit wordt opgegeven in de record of als er tijdreeksgegevens worden gebruikt, worden deze identiteiten zonder extra configuratie toegewezen aan de identiteitsgrafiek. Raadpleeg de handleiding voor [](../../ingestion/tutorials/streaming-record-data.md) streamingingontwikkeling voor meer informatie.

## Bevestig dat het uploaden is gelukt

Wanneer het uploaden van gegevens naar een nieuwe dataset voor het eerst, of als deel van een proces dat een nieuwe ETL of een gegevensbron impliceert, wordt geadviseerd om de gegevens zorgvuldig te controleren om ervoor te zorgen het correct geupload is.

Gebruikend de Toegang API van het Profiel van de Klant in real time, kunt u partijgegevens terugwinnen aangezien het in een dataset wordt geladen. Als u geen van de entiteiten kunt terugwinnen u verwacht, kan uw dataset niet voor Profiel worden toegelaten. Na het bevestigen dat uw dataset is toegelaten, zorg ervoor dat uw brongegevensformaat en herkenningstekens uw verwachtingen steunen.

Voor gedetailleerde instructies over hoe te om tot entiteiten toegang te hebben die in real time API van het Profiel van de Klant gebruiken, gelieve te verwijzen naar de gids [van het](../api/entities.md)entiteitseindpunt, die ook als &quot;API van de Toegang van het Profiel&quot;wordt bekend.