---
keywords: Experience Platform;home;populaire onderwerpen;cloudopslagaansluiting;cloudopslag
solution: Experience Platform
title: Een DataFlow configureren voor een Cloud Storage Streaming Connector in de gebruikersinterface
topic: overview
type: Tutorial
description: Een dataflow is een geplande taak die gegevens van een bron aan een dataset van de Platform terugwint en opneemt. Deze zelfstudie bevat stappen voor het configureren van een nieuwe gegevensstroom met behulp van de basisaansluiting voor cloudopslag.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 0%

---


# Een gegevensstroom configureren voor een streamingverbinding voor cloudopslag in de gebruikersinterface

Een dataflow is een geplande taak die gegevens van een bron aan een [!DNL Platform] dataset terugwint en opneemt. Deze zelfstudie bevat stappen voor het configureren van een nieuwe gegevensstroom met behulp van de basisaansluiting voor cloudopslag.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Experience Platform] klantenervaring worden georganiseerd.
   - [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md) Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Bovendien is voor deze zelfstudie vereist dat u al een cloudopslagaansluiting hebt gemaakt. Een lijst met zelfstudies voor het maken van verschillende cloudopslagconnectors in de gebruikersinterface vindt u in het [overzicht van de bronconnectors](../../../../home.md).

## Gegevens selecteren

Nadat u de aansluiting voor cloudopslag hebt gemaakt, wordt de stap *Gegevens selecteren* weergegeven. Deze stap biedt een interface waarmee u kunt selecteren van welke stream u gegevens wilt streamen.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-data.png)

## Gegevensvelden toewijzen aan een XDM-schema

De stap **[!UICONTROL Toewijzing]** verschijnt, die een interactieve interface verstrekt om de brongegevens aan een [!DNL Platform] dataset in kaart te brengen.

Kies een dataset voor binnenkomende gegevens waarin moeten worden opgenomen. U kunt of een bestaande dataset gebruiken of nieuwe creëren.

**Een bestaande gegevensset gebruiken**

Om gegevens in een bestaande dataset in te voeren, selecteer **[!UICONTROL bestaande dataset]** gebruiken, dan klik het datasetpictogram.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-existing-data.png)

Het dialoogvenster **[!UICONTROL Gegevensset selecteren]** wordt weergegeven. Zoek de dataset u wenst te gebruiken, het te selecteren, dan **[!UICONTROL ga]** te klikken.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-existing-data.png)

**Een nieuwe gegevensset gebruiken**

Om gegevens in een nieuwe dataset in te voeren, selecteer **[!UICONTROL nieuwe dataset]** creëren en ga een naam en een beschrijving voor de dataset op de verstrekte gebieden in. Selecteer vervolgens het schema dat u wilt gebruiken onder het vervolgkeuzemenu.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-new-dataset.png)

## Geef uw gegevensstroom een naam

De stap **[!UICONTROL Dataflow detail]** verschijnt, toestaand u om een naam en een korte beschrijving over uw nieuwe dataflow te geven.

Geef waarden op voor de gegevensstroom en klik op **[!UICONTROL Volgende]**.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/name-your-dataflow.png)

### Controleer uw gegevensstroom

De stap **[!UICONTROL Review]** verschijnt, die u toestaat om uw nieuwe gegevensstroom te herzien alvorens het wordt gecreeerd. De details worden gegroepeerd in de volgende categorieën:

- **[!UICONTROL Brongegevens]**: Toont het brontype en andere relevante details over de bron.
- **[!UICONTROL Doelgegevens]**: Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset zich aan houdt.

Zodra u uw gegevensstroom hebt herzien, klik **[!UICONTROL Afwerking]** en laat wat tijd voor dataflow toe om worden gecreeerd.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## Uw gegevensstroom controleren en verwijderen

Nadat u de gegevens voor de cloudopslag hebt gemaakt, kunt u de gegevens controleren die er doorheen worden ingevoerd. Zie de zelfstudie over [dataflows controleren](../../../../../ingestion/quality/monitor-data-ingestion.md) voor meer informatie over het controleren en verwijderen van gegevensstromen.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes een dataflow gemaakt om gegevens van een externe wolkenopslag in te brengen, en hebt u inzicht gekregen in de controle van datasets. Binnenkomende gegevens kunnen nu worden gebruikt door downstreamservices [!DNL Platform] zoals [!DNL Real-time Customer Profile] en [!DNL Data Science Workspace]. Raadpleeg de volgende documenten voor meer informatie:

- [[!DNL Real-time Customer Profile]  - overzicht](../../../../../profile/home.md)
- [[!DNL Data Science Workspace]  - overzicht](../../../../../data-science-workspace/home.md)

## Aanhangsel

De volgende secties verstrekken extra informatie voor het werken met bronschakelaars.

### Een gegevensstroom uitschakelen

Wanneer een gegevensstroom wordt gecreeerd, wordt het onmiddellijk actief en neemt gegevens volgens het programma op het werd gegeven. U kunt een actieve gegevensstroom op elk ogenblik onbruikbaar maken door de instructies hieronder te volgen.

Klik in de werkruimte **[!UICONTROL Bronnen]** op het tabblad **[!UICONTROL Bladeren]**. Klik vervolgens op de naam van de verbinding die is gekoppeld aan de actieve gegevensstroom die u wilt uitschakelen.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/browse.png)

De pagina **[!UICONTROL Bronactiviteit]** wordt weergegeven. Selecteer de actieve dataflow in de lijst om zijn **[!UICONTROL Eigenschappen]** kolom op de rechterkant van het scherm te openen, die **[!UICONTROL Enabled]** knevelknoop bevat. Klik op de schakeloptie om de gegevensstroom uit te schakelen. Dezelfde schakeloptie kan worden gebruikt om een gegevensstroom opnieuw in te schakelen nadat deze is uitgeschakeld.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/disable-source.png)

### Binnenkomende gegevens voor [!DNL Profile] populatie activeren

De binnenkomende gegevens van uw bronschakelaar kunnen worden gebruikt om uw [!DNL Real-time Customer Profile] gegevens te verrijken en te vullen. Zie de zelfstudie over [Profielpopulatie](../../profile.md) voor meer informatie over het vullen van uw [!DNL Real-time Customer Profile]-gegevens.
