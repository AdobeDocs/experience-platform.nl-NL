---
keywords: Experience Platform;home;popular topics;cloud storage connector;cloud storage
solution: Experience Platform
title: Een dataflow configureren voor een streamingconnector voor cloudopslag in de gebruikersinterface
topic: overview
type: Tutorial
description: Een dataflow is een geplande taak die gegevens van een bron aan een dataset van de Platform terugwint en opneemt. Deze zelfstudie bevat stappen voor het configureren van een nieuwe gegevensstroom met behulp van de basisaansluiting voor cloudopslag.
translation-type: tm+mt
source-git-commit: cfdaf72b7f4bf190877006ccd4cc6a7fd014adc2
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 0%

---


# Een dataflow configureren voor een streamingconnector voor cloudopslag in de gebruikersinterface

Een dataflow is een geplande taak die gegevens van een bron aan een [!DNL Platform] dataset terugwint en opneemt. Deze zelfstudie bevat stappen voor het configureren van een nieuwe gegevensstroom met behulp van de basisaansluiting voor cloudopslag.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
   - [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Bovendien is voor deze zelfstudie vereist dat u al een cloudopslagaansluiting hebt gemaakt. Een lijst met zelfstudies voor het maken van verschillende cloudopslagconnectors in de gebruikersinterface vindt u in het overzicht [van de](../../../../home.md)bronconnectors.

## Gegevens selecteren

Nadat u de aansluiting voor de cloudopslag hebt gemaakt, wordt de stap Gegevens ** selecteren weergegeven. Deze stap bevat een interface waarmee u kunt selecteren uit welke stream u gegevens wilt streamen.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-data.png)

## Gegevensvelden toewijzen aan een XDM-schema

De stap **[!UICONTROL Toewijzing]** verschijnt, die een interactieve interface verstrekt om de brongegevens aan een [!DNL Platform] dataset in kaart te brengen.

Kies een dataset voor binnenkomende gegevens waarin moeten worden opgenomen. U kunt of een bestaande dataset gebruiken of nieuwe creëren.

**Een bestaande gegevensset gebruiken**

Om gegevens in een bestaande dataset in te voeren, selecteer **[!UICONTROL Gebruik bestaande dataset]**, dan klik het datasetpictogram.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-existing-data.png)

Het dialoogvenster **[!UICONTROL Gegevensset]** selecteren wordt geopend. Zoek de gegevensset die u wilt gebruiken, selecteer deze en klik op **[!UICONTROL Doorgaan]**.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-existing-data.png)

**Een nieuwe gegevensset gebruiken**

Om gegevens in een nieuwe dataset in te voeren, **[!UICONTROL creeer nieuwe dataset]** en ga een naam en een beschrijving voor de dataset op de verstrekte gebieden in. Selecteer vervolgens het schema dat u wilt gebruiken onder het vervolgkeuzemenu.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-new-dataset.png)

## Geef uw gegevensstroom een naam

De stap met **[!UICONTROL details]** over gegevensstroom wordt weergegeven, zodat u een naam kunt geven en een korte beschrijving kunt geven van uw nieuwe gegevensstroom.

Geef waarden op voor de gegevensstroom en klik op **[!UICONTROL Volgende]**.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/name-your-dataflow.png)

### Controleer uw gegevensstroom

De stap **[!UICONTROL Revisie]** wordt weergegeven, zodat u de nieuwe gegevensstroom kunt controleren voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

- **[!UICONTROL Brongegevens]**: Toont het brontype en andere relevante details over de bron.
- **[!UICONTROL Doelgegevens]**: Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset zich aan houdt.

Nadat u de gegevensstroom hebt gereviseerd, klikt u op **[!UICONTROL Voltooien]** en laat u enige tijd over tot de gegevensstroom.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## Uw gegevensstroom controleren en verwijderen

Nadat u de gegevens voor de cloudopslag hebt gemaakt, kunt u de gegevens controleren die er doorheen worden ingevoerd. Voor meer informatie bij het controleren van en het schrappen van gegevensstromen, zie de zelfstudie over het [controleren van gegevensstromen](../../../../../ingestion/quality/monitor-data-ingestion.md).

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes een dataflow gemaakt om gegevens van een externe wolkenopslag in te brengen, en hebt u inzicht gekregen in de controle van datasets. Inkomende gegevens kunnen nu worden gebruikt door downstreamdiensten [!DNL Platform] zoals [!DNL Real-time Customer Profile] en [!DNL Data Science Workspace]. Raadpleeg de volgende documenten voor meer informatie:

- [[!DNL Real-time Customer Profile]  - overzicht](../../../../../profile/home.md)
- [[!DNL Data Science Workspace]  - overzicht](../../../../../data-science-workspace/home.md)

## Aanhangsel

De volgende secties verstrekken extra informatie voor het werken met bronschakelaars.

### Een gegevensstroom uitschakelen

Wanneer een gegevensstroom wordt gecreeerd, wordt het onmiddellijk actief en neemt gegevens volgens het programma op het werd gegeven. U kunt een actieve gegevensstroom op elk ogenblik onbruikbaar maken door de instructies hieronder te volgen.

Klik in de **[!UICONTROL werkruimte Bronnen]** op het tabblad **[!UICONTROL Bladeren]** . Klik vervolgens op de naam van de verbinding die is gekoppeld aan de actieve gegevensstroom die u wilt uitschakelen.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/browse.png)

De pagina **[!UICONTROL Bronactiviteit]** wordt weergegeven. Selecteer de actieve gegevensstroom van de lijst om zijn kolom van **[!UICONTROL Eigenschappen]** op de rechterkant van het scherm te openen, die een **[!UICONTROL Toegelaten]** knevelknoop bevat. Klik op de schakeloptie om de gegevensstroom uit te schakelen. Dezelfde schakeloptie kan worden gebruikt om een gegevensstroom opnieuw in te schakelen nadat deze is uitgeschakeld.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/disable-source.png)

### Binnenkomende gegevens voor [!DNL Profile] populatie activeren

De binnenkomende gegevens van uw bronschakelaar kunnen worden gebruikt om uw [!DNL Real-time Customer Profile] gegevens te verrijken en te bevolken. Zie de zelfstudie over de [!DNL Real-time Customer Profile] profielpopulatie [](../../profile.md)voor meer informatie over het vullen van gegevens.
