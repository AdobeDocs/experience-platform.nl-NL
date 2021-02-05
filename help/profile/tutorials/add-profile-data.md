---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API;profiel inschakelen;profiel inschakelen
title: Gegevens toevoegen aan realtime klantprofiel
topic: tutorial
type: Tutorial
description: In deze zelfstudie worden de stappen beschreven die nodig zijn om gegevens toe te voegen aan het realtime profiel van de klant.
translation-type: tm+mt
source-git-commit: cad9c690be986961aea2969ef0ade975f33a8ee5
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---


# Gegevens toevoegen aan [!DNL Real-time Customer Profile]

In deze zelfstudie worden de stappen beschreven die nodig zijn om gegevens toe te voegen aan [!DNL Real-time Customer Profile].

## Een schema inschakelen voor [!DNL Real-time Customer Profile]

Gegevens die in [!DNL Experience Platform] voor gebruik door [!DNL Real-time Customer Profile] worden opgenomen moeten met een [!DNL Experience Data Model] (XDM) schema in overeenstemming zijn dat voor [!DNL Profile] wordt toegelaten. Een schema kan alleen worden ingeschakeld voor Profiel als het de klasse [!DNL XDM Individual Profile] of [!DNL XDM ExperienceEvent] implementeert.

U kunt een schema voor gebruik in [!DNL Real-time Customer Profile] toelaten gebruikend [!DNL Schema Registry] API of [!DNL Schema Editor] gebruikersinterface. Om te beginnen, volg de leerprogramma&#39;s voor [creërend een schema gebruikend APIs](../../xdm/tutorials/create-schema-api.md) of [creërend een schema gebruikend de Redacteur UI van het Schema](../../xdm/tutorials/create-schema-ui.md).

## Gegevens toevoegen met batch-opname

Alle gegevens die naar [!DNL Platform] worden geüpload met behulp van batch-opname, worden geüpload naar afzonderlijke gegevenssets. Alvorens deze gegevens door [!DNL Real-time Customer Profile] kunnen worden gebruikt, moet de dataset in kwestie specifiek worden gevormd. Voor volledige instructies, zie de zelfstudie over [het vormen van een dataset voor de Dienst van het Profiel en van de Identiteit](dataset-configuration.md).

Zodra de dataset is gevormd, kunt u beginnen gegevens in het op te nemen. Zie de [handleiding voor ontwikkelaars van batchinvoer](../../ingestion/batch-ingestion/api-overview.md) voor gedetailleerde stappen over het uploaden van bestanden in verschillende indelingen.

## Gegevens toevoegen met streaming opname

Om het even welke stroom-ingebed gegevens die met een [!DNL Profile]-Toegelaten schema compatibel zijn zullen automatisch het aangewezen verslag in [!DNL Real-time Customer Profile] toevoegen of beschrijven. Als er meer dan één identiteit wordt opgegeven in de record of als er tijdreeksgegevens worden gebruikt, worden deze identiteiten zonder extra configuratie toegewezen aan de identiteitsgrafiek. Raadpleeg de [handleiding voor het streamen van ingeslikte toepassingen](../../ingestion/tutorials/streaming-record-data.md) voor meer informatie.

## Bevestig dat het uploaden is gelukt

Wanneer het uploaden van gegevens naar een nieuwe dataset voor het eerst, of als deel van een proces dat een nieuwe ETL of een gegevensbron impliceert, wordt geadviseerd om de gegevens zorgvuldig te controleren om ervoor te zorgen het correct geupload is.

Met de API [!DNL Real-time Customer Profile] Access kunt u batchgegevens ophalen terwijl deze in een gegevensset worden geladen. Als u geen van de entiteiten kunt terugwinnen u verwacht, kan uw dataset niet voor [!DNL Profile] worden toegelaten. Na het bevestigen dat uw dataset is toegelaten, zorg ervoor dat uw brongegevensformaat en herkenningstekens uw verwachtingen steunen.

Voor gedetailleerde instructies over hoe te om tot entiteiten toegang te hebben die [!DNL Real-time Customer Profile] API gebruiken, gelieve te verwijzen naar [de gids van het eindpunt van entiteiten](../api/entities.md), ook gekend als &quot;[!DNL Profile Access] API&quot;.