---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Gegevens toevoegen aan realtime klantprofiel
topic: tutorial
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---


# Gegevens toevoegen aan [!DNL Real-time Customer Profile]

In deze zelfstudie worden de stappen beschreven die nodig zijn om gegevens aan toe te voegen [!DNL Real-time Customer Profile].

## Een schema inschakelen voor [!DNL Real-time Customer Profile]

Gegevens die worden opgenomen in [!DNL Experience Platform] voor gebruik door [!DNL Real-time Customer Profile] moeten met een [!DNL Experience Data Model] (XDM) schema in overeenstemming zijn dat voor [!DNL Profile]. Een schema kan alleen worden ingeschakeld voor Profiel als het de klasse [!DNL XDM Individual Profile] [!DNL XDM ExperienceEvent] of de klasse implementeert.

U kunt een schema inschakelen voor gebruik in [!DNL Real-time Customer Profile] de [!DNL Schema Registry] API of de [!DNL Schema Editor] gebruikersinterface. Om te beginnen, volg de leerprogramma&#39;s voor het [creëren van een schema gebruikend APIs](../../xdm/tutorials/create-schema-api.md) of [creërend een schema gebruikend de Redacteur van het Schema UI](../../xdm/tutorials/create-schema-ui.md).

## Gegevens toevoegen met batch-opname

Alle gegevens die naar het [!DNL Platform] gebruiken van batch-opname worden geüpload worden geüpload naar individuele datasets. Alvorens deze gegevens door kunnen worden gebruikt, moet de dataset in kwestie specifiek worden gevormd. [!DNL Real-time Customer Profile] Voor volledige instructies, zie de zelfstudie over het [vormen van een dataset voor de Dienst](dataset-configuration.md)van het Profiel en van de Identiteit.

Zodra de dataset is gevormd, kunt u beginnen gegevens in het op te nemen. Zie de handleiding voor [het ontwikkelen van](../../ingestion/batch-ingestion/api-overview.md) batches voor gedetailleerde stappen over het uploaden van bestanden in verschillende indelingen.

## Gegevens toevoegen met streaming opname

Om het even welk stroom-ingebed gegeven dat met een [!DNL Profile]-toegelaten XDM schema volgt zal automatisch het aangewezen verslag binnen toevoegen of overschrijven [!DNL Real-time Customer Profile]. Als er meer dan één identiteit wordt opgegeven in de record of als er tijdreeksgegevens worden gebruikt, worden deze identiteiten zonder extra configuratie toegewezen aan de identiteitsgrafiek. Raadpleeg de handleiding voor [](../../ingestion/tutorials/streaming-record-data.md) streamingingontwikkeling voor meer informatie.

## Bevestig dat het uploaden is gelukt

Wanneer het uploaden van gegevens naar een nieuwe dataset voor het eerst, of als deel van een proces dat een nieuwe ETL of een gegevensbron impliceert, wordt geadviseerd om de gegevens zorgvuldig te controleren om ervoor te zorgen het correct geupload is.

Gebruikend de [!DNL Real-time Customer Profile] Toegang API, kunt u partijgegevens terugwinnen aangezien het in een dataset wordt geladen. Als u om het even welke entiteiten niet kunt terugwinnen u verwacht, kan uw dataset niet voor worden toegelaten [!DNL Profile]. Na het bevestigen dat uw dataset is toegelaten, zorg ervoor dat uw brongegevensformaat en herkenningstekens uw verwachtingen steunen.

Voor gedetailleerde instructies over hoe te om tot entiteiten toegang te hebben die API gebruiken, gelieve te verwijzen naar de gids [!DNL Real-time Customer Profile] van het [entiteitseindpunt, die ook als &quot;API&quot;wordt bekend](../api/entities.md)[!DNL Profile Access] .