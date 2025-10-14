---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API;profiel inschakelen;profiel inschakelen
title: Gegevens toevoegen aan realtime klantprofiel
type: Tutorial
description: In deze zelfstudie worden de stappen beschreven die nodig zijn om gegevens toe te voegen aan het realtime profiel van de klant.
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# Gegevens toevoegen aan [!DNL Real-Time Customer Profile]

In deze zelfstudie worden de stappen beschreven die nodig zijn om gegevens aan [!DNL Real-Time Customer Profile] toe te voegen.

## Een schema inschakelen voor [!DNL Real-Time Customer Profile]

Gegevens die in [!DNL Experience Platform] worden ingevoerd voor gebruik door [!DNL Real-Time Customer Profile] , moeten overeenkomen met een [!DNL Experience Data Model] (XDM)-schema dat is ingeschakeld voor [!DNL Profile] . Een schema kan alleen worden ingeschakeld voor Profiel als het de klasse [!DNL XDM Individual Profile] of [!DNL XDM ExperienceEvent] implementeert.

U kunt een schema inschakelen voor gebruik in [!DNL Real-Time Customer Profile] met de [!DNL Schema Registry] API of de [!DNL Schema Editor] -gebruikersinterface. Om begonnen te worden, volg de leerprogramma&#39;s voor [&#x200B; creërend een schema gebruikend APIs &#x200B;](../../xdm/tutorials/create-schema-api.md) of [&#x200B; creërend een schema gebruikend de Redacteur UI van het Schema &#x200B;](../../xdm/tutorials/create-schema-ui.md).

## Gegevens toevoegen met behulp van batch-opname

Alle gegevens die naar [!DNL Experience Platform] zijn geüpload met behulp van batch-invoer, worden geüpload naar afzonderlijke gegevenssets. Voordat deze gegevens door [!DNL Real-Time Customer Profile] kunnen worden gebruikt, moet de desbetreffende gegevensset specifiek zijn geconfigureerd. Voor volledige instructies, zie het leerprogramma op [&#x200B; vormend een dataset voor de Dienst van het Profiel en van de Identiteit &#x200B;](dataset-configuration.md).

Zodra de dataset is gevormd, kunt u beginnen gegevens in het op te nemen. Zie de [&#x200B; handleiding van de partijontwikkelaar &#x200B;](../../ingestion/batch-ingestion/api-overview.md) voor gedetailleerde stappen op hoe te om dossiers in verschillende formaten te uploaden.

## Gegevens toevoegen met streaming opname

Alle via een stream opgenomen gegevens die voldoen aan een XDM-schema voor [!DNL Profile] , voegen automatisch de juiste record toe in [!DNL Real-Time Customer Profile] of overschrijven deze. Als er meer dan één identiteit wordt opgegeven in de record of als er tijdreeksgegevens worden gebruikt, worden deze identiteiten zonder extra configuratie toegewezen aan de identiteitsgrafiek. Zie [&#x200B; het stromen de ontwikkelaarsgids van de insinrichting &#x200B;](../../ingestion/tutorials/streaming-record-data.md) om meer te leren.

## Bevestig dat het uploaden is gelukt

Wanneer het uploaden van gegevens naar een nieuwe dataset voor het eerst, of als deel van een proces dat een nieuwe ETL of een gegevensbron impliceert, wordt geadviseerd om de gegevens zorgvuldig te controleren om ervoor te zorgen het correct geupload is.

Met de API voor toegang van [!DNL Real-Time Customer Profile] kunt u batchgegevens ophalen terwijl deze in een gegevensset worden geladen. Als u geen van de entiteiten kunt ophalen die u verwacht, is het mogelijk dat de gegevensset niet is ingeschakeld voor [!DNL Profile] . Na het bevestigen dat uw dataset is toegelaten, zorg ervoor dat uw brongegevensformaat en herkenningstekens uw verwachtingen steunen.

Voor gedetailleerde instructies op hoe te om tot entiteiten toegang te hebben die [!DNL Real-Time Customer Profile] API gebruiken, gelieve te verwijzen naar de [&#x200B; gids van het entiteitseindpunt &#x200B;](../api/entities.md), die ook als &quot;[!DNL Profile Access] API&quot;wordt bekend.

## Gegevens in profielarchief bijwerken

Soms kan het nodig zijn gegevens bij te werken in het profielarchief van uw organisatie. U moet bijvoorbeeld records corrigeren of een kenmerkwaarde wijzigen. Dit kan door partijopname worden gedaan en vereist een profiel-Toegelaten dataset die met een upsert markering wordt gevormd. Voor meer informatie over hoe te om een dataset voor attributenupdates te vormen, gelieve te verwijzen naar het leerprogramma voor [&#x200B; toelatend een dataset voor Profiel en op te nemen &#x200B;](../../catalog/datasets/enable-upsert.md).
