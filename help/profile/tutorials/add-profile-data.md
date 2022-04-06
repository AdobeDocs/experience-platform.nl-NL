---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API;profiel inschakelen;profiel inschakelen
title: Gegevens toevoegen aan realtime klantprofiel
topic-legacy: tutorial
type: Tutorial
description: In deze zelfstudie worden de stappen beschreven die nodig zijn om gegevens toe te voegen aan het realtime profiel van de klant.
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: 9f00bff31f9e7d2da1294d3d1f24cba7870a4614
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# Gegevens toevoegen aan [!DNL Real-time Customer Profile]

In deze zelfstudie worden de stappen beschreven die nodig zijn om gegevens toe te voegen aan [!DNL Real-time Customer Profile].

## Een schema inschakelen voor [!DNL Real-time Customer Profile]

Gegevens die worden ingevoerd in [!DNL Experience Platform] voor gebruik door [!DNL Real-time Customer Profile] voldoen aan een [!DNL Experience Data Model] (XDM) schema dat wordt toegelaten voor [!DNL Profile]. Als u een schema wilt inschakelen voor Profiel, moet u ofwel de opdracht [!DNL XDM Individual Profile] of [!DNL XDM ExperienceEvent] klasse.

U kunt een schema inschakelen voor gebruik in [!DNL Real-time Customer Profile] met de [!DNL Schema Registry] API of de [!DNL Schema Editor] gebruikersinterface. Volg de zelfstudies voor [een schema maken met behulp van API&#39;s](../../xdm/tutorials/create-schema-api.md) of [het creëren van een schema gebruikend de Redacteur UI van het Schema](../../xdm/tutorials/create-schema-ui.md).

## Gegevens toevoegen met batch-opname

Alle gegevens geüpload naar [!DNL Platform] het gebruiken van partijingestie wordt geupload aan individuele datasets. Voordat deze gegevens kunnen worden gebruikt door [!DNL Real-time Customer Profile], moet de betrokken gegevensset specifiek worden geconfigureerd. Voor volledige instructies raadpleegt u de zelfstudie op [configureren van een gegevensset voor profiel- en identiteitsservice](dataset-configuration.md).

Zodra de dataset is gevormd, kunt u beginnen gegevens in het op te nemen. Zie de [handleiding voor het ontwikkelen van batch-inhoud](../../ingestion/batch-ingestion/api-overview.md) voor gedetailleerde stappen voor het uploaden van bestanden in verschillende indelingen.

## Gegevens toevoegen met streaming opname

Alle via een stream opgenomen gegevens die voldoen aan een [!DNL Profile]-enabled XDM schema zal automatisch het aangewezen verslag binnen toevoegen of overschrijven [!DNL Real-time Customer Profile]. Als er meer dan één identiteit wordt opgegeven in de record of als er tijdreeksgegevens worden gebruikt, worden deze identiteiten zonder extra configuratie toegewezen aan de identiteitsgrafiek. Zie de [handleiding voor streamingopname](../../ingestion/tutorials/streaming-record-data.md) voor meer informatie.

## Bevestig dat het uploaden is gelukt

Wanneer het uploaden van gegevens naar een nieuwe dataset voor het eerst, of als deel van een proces dat een nieuwe ETL of een gegevensbron impliceert, wordt geadviseerd om de gegevens zorgvuldig te controleren om ervoor te zorgen het correct geupload is.

Met de [!DNL Real-time Customer Profile] Toegang API, kunt u partijgegevens terugwinnen aangezien het in een dataset wordt geladen. Als u geen van de entiteiten kunt terugwinnen u verwacht, kan uw dataset niet worden toegelaten voor [!DNL Profile]. Na het bevestigen dat uw dataset is toegelaten, zorg ervoor dat uw brongegevensformaat en herkenningstekens uw verwachtingen steunen.

Voor gedetailleerde instructies over hoe te om tot entiteiten toegang te hebben gebruikend [!DNL Real-time Customer Profile] API, gelieve te verwijzen naar [eindgebruikershandleiding voor entiteiten](../api/entities.md), ook wel bekend als &quot;[!DNL Profile Access] API&quot;.

## Profielopslaggegevens bijwerken

Soms kan het nodig zijn gegevens bij te werken in de profielopslag van uw organisatie. U moet bijvoorbeeld records corrigeren of een kenmerkwaarde wijzigen. Dit kan door partijopname worden gedaan en vereist een profiel-Toegelaten dataset die met een upsert markering wordt gevormd. Voor meer informatie over hoe te om een dataset voor attributenupdates te vormen, gelieve te verwijzen naar het leerprogramma voor [het toelaten van een dataset voor Profiel en upsert](../../catalog/datasets/enable-upsert.md).
