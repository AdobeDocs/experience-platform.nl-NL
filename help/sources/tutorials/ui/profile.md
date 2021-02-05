---
keywords: Experience Platform;thuis;populaire onderwerpen;activeer binnenkomende gegevens;bevolk profiel;bevolkt rtcp;bevolkt verenigd profiel
solution: Experience Platform
title: Activeer Binnenkomende Brongegevens om Klantprofielen in UI te bevolken
topic: overview
type: Tutorial
description: De binnenkomende gegevens van uw bronschakelaar kunnen worden gebruikt om uw gegevens van het Profiel van de Klant in real time te verrijken en te bevolken.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---


# Activeer binnenkomende brongegevens om klantenprofielen te bevolken

De binnenkomende gegevens van uw bronschakelaar kunnen worden gebruikt om uw [!DNL Real-time Customer Profile] gegevens te verrijken en te vullen.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Systeem](../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Experience Platform] klantenervaring worden georganiseerd.
   - [Basisbeginselen van de schemacompositie](../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie](../../../xdm/tutorials/create-schema-ui.md) Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Bovendien, vereist dit leerprogramma dat u reeds een bronschakelaar hebt gecreeerd en gevormd.  Een lijst van leerprogramma&#39;s voor het creëren van verschillende schakelaars in UI kan in [overzicht van bronschakelaars](../../home.md) worden gevonden.

## Uw [!DNL Real-time Customer Profile]-gegevens vullen

Om klantprofielen te verrijken, moet het bronschema van de doeldataset voor gebruik in [!DNL Real-time Customer Profile] compatibel zijn. Een compatibel schema voldoet aan de volgende vereisten:

- Het schema heeft minstens één die attribuut als identiteitseigenschap wordt gespecificeerd.
- Het schema heeft een identiteitseigenschap die als primaire identiteit wordt bepaald.
- Er bestaat een toewijzing binnen de gegevensstroom waarin de primaire identiteit een doelkenmerk is.

Klik in de werkruimte Bronnen op het tabblad **[!UICONTROL Bladeren]** om uw basisverbindingen weer te geven. Zoek in de weergegeven lijst de verbinding met de gegevensstroom waarmee u de profielen wilt vullen. Klik op de naam van de verbinding om de details te openen.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

Het scherm **[!UICONTROL Bronactiviteit]** van de verbinding verschijnt, tonend de datasets die de verbinding brongegevens in opneemt. Klik op de naam van de gegevensset die u wilt inschakelen voor [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

Het scherm **[!UICONTROL Datasetactiviteit]** wordt weergegeven. De **[!UICONTROL Eigenschappen]** kolom op de rechterkant van het scherm toont de details van de dataset, en omvat een **[!UICONTROL Profiel]** schakelaar en een verbinding aan het schema de dataset volgt aan. Klik de naam van het schema om zijn samenstelling te bekijken.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

De **[!UICONTROL Schemaeditor]** wordt weergegeven en toont de structuur van het schema in het middelste canvas. Selecteer in het canvas het veld dat u als primaire identiteit wilt instellen. Selecteer onder het tabblad **[!UICONTROL Veldeigenschappen]** dat wordt weergegeven het selectievakje **[!UICONTROL Identiteit]** en vervolgens **[!UICONTROL Primaire identiteit]**. Tot slot selecteer aangewezen **[!UICONTROL Identiteitsnamespace]**, dan klik **[!UICONTROL Apply]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Klik op het bovenste object van de structuur van het schema en de kolom **[!UICONTROL Schemaeigenschappen]** wordt weergegeven. Schakel het schema voor [!DNL Profile] in door de schakelaar **[!UICONTROL Profile]** in en uit te schakelen. Klik **[!UICONTROL Opslaan]** om uw wijzigingen te voltooien.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Nu het schema voor [!DNL Profile] wordt toegelaten, terugkeer aan **[!UICONTROL Dataset activiteit]** scherm en laat de dataset voor [!DNL Profile] door **[!UICONTROL Profiel]** knevel binnen **[!UICONTROL Eigenschappen]** kolom toe te klikken.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Als zowel het schema als de dataset voor [!DNL Profile] wordt toegelaten, zullen de gegevens die in die dataset worden opgenomen ook klantenprofielen nu bevolken.

>[!NOTE]
>
>Bestaande gegevens binnen een recent ingeschakelde gegevensset worden niet door [!DNL Profile] gebruikt.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes binnenkomende gegevens voor [!DNL Profile] populatie geactiveerd. Voor meer informatie, zie [[!DNL Real-time Customer Profile] overzicht](../../../profile/home.md).