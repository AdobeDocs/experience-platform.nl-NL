---
keywords: Experience Platform;home;popular topics;activate inbound data;populate profile;populate rtcp;populated unified profile
solution: Experience Platform
title: Activeer binnenkomende brongegevens om klantenprofielen te bevolken
topic: overview
type: Tutorial
description: De binnenkomende gegevens van uw bronschakelaar kunnen worden gebruikt om uw gegevens van het Profiel van de Klant in real time te verrijken en te bevolken.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---


# Activeer binnenkomende brongegevens om klantenprofielen te bevolken

De binnenkomende gegevens van uw bronschakelaar kunnen worden gebruikt om uw [!DNL Real-time Customer Profile] gegevens te verrijken en te bevolken.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Systeem](../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
   - [Basisbeginselen van de schemacompositie](../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie](../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Bovendien, vereist dit leerprogramma dat u reeds een bronschakelaar hebt gecreeerd en gevormd.  Een lijst van leerprogramma&#39;s voor het creëren van verschillende schakelaars in UI kan in het overzicht [van](../../home.md)bronschakelaars worden gevonden.

## Uw [!DNL Real-time Customer Profile] gegevens vullen

Om klantenprofielen te verrijken, moet het bronschema van de doeldataset voor gebruik binnen compatibel zijn [!DNL Real-time Customer Profile]. Een compatibel schema voldoet aan de volgende vereisten:

- Het schema heeft minstens één die attribuut als identiteitseigenschap wordt gespecificeerd.
- Het schema heeft een identiteitseigenschap die als primaire identiteit wordt bepaald.
- Er bestaat een toewijzing binnen de gegevensstroom waarin de primaire identiteit een doelkenmerk is.

Klik in de werkruimte Bronnen op het tabblad **[!UICONTROL Bladeren]** om uw basisverbindingen weer te geven. Zoek in de weergegeven lijst de verbinding met de gegevensstroom waarmee u de profielen wilt vullen. Klik op de naam van de verbinding om de details te openen.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

Het scherm van de **[!UICONTROL Bron van de verbinding activiteit]** verschijnt, tonend de datasets die de verbinding brongegevens in opneemt. Klik de naam van de dataset u wenst om voor toe te laten [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

Het scherm **[!UICONTROL Dataset-activiteit]** wordt weergegeven. De **[!UICONTROL kolom van Eigenschappen]** op de rechterkant van het scherm toont de details van de dataset, en omvat een schakelaar van het **[!UICONTROL Profiel]** en een verbinding aan het schema de dataset volgt. Klik de naam van het schema om zijn samenstelling te bekijken.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

De **[!UICONTROL Schema-editor]** wordt weergegeven en toont de structuur van het schema in het middelste canvas. Selecteer in het canvas het veld dat u als primaire identiteit wilt instellen. Selecteer onder het tabblad **[!UICONTROL Veldeigenschappen]** dat wordt weergegeven het selectievakje **[!UICONTROL Identiteit]** en vervolgens **[!UICONTROL Primaire identiteit]**. Selecteer ten slotte een geschikte naamruimte **** Identiteit en klik op **[!UICONTROL Toepassen]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Klik op het bovenste object van de structuur van het schema en de kolom met **[!UICONTROL Schema-eigenschappen]** wordt weergegeven. Schakel het schema in [!DNL Profile] door de schakelaar **[!UICONTROL Profiel]** in en uit te schakelen. Klik op **[!UICONTROL Opslaan]** om de wijzigingen te voltooien.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Nu het schema wordt toegelaten voor [!DNL Profile], ga aan het de activiteitenscherm van de **[!UICONTROL Dataset]** terug en laat de dataset voor toe [!DNL Profile] door de **[!UICONTROL knevel van het Profiel]** binnen de kolom van **[!UICONTROL Eigenschappen]** te klikken.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Met zowel het schema als de dataset die voor wordt toegelaten, zullen de gegevens in die dataset worden opgenomen ook klantenprofielen bevolken. [!DNL Profile]

>[!NOTE]
>
>Bestaande gegevens binnen een recent ingeschakelde gegevensset worden niet door [!DNL Profile]gebruikt.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de binnenkomende gegevens voor de [!DNL Profile] populatie geactiveerd. Zie het [[!DNL Real-time Customer Profile] overzicht](../../../profile/home.md)voor meer informatie.