---
keywords: Experience Platform;thuis;populaire onderwerpen;activeer binnenkomende gegevens;bevolk profiel;bevolkt rtcp;bevolkt verenigd profiel
solution: Experience Platform
title: Activeer Binnenkomende Brongegevens om Klantprofielen in UI te bevolken
type: Tutorial
description: De binnenkomende gegevens van uw bronschakelaar kunnen worden gebruikt om uw gegevens van het Profiel van de Klant in real time te verrijken en te bevolken.
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# Activeer binnenkomende brongegevens om klantenprofielen te bevolken

De binnenkomende gegevens van uw bronschakelaar kunnen aan het verrijken en het bevolken van uw [!DNL Real-Time Customer Profile] gegevens.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Systeem](../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   - [Basisbeginselen van de schemacompositie](../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie Schema Editor](../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Bovendien, vereist dit leerprogramma dat u reeds een bronschakelaar hebt gecreeerd en gevormd.  Een lijst van leerprogramma&#39;s voor het creëren van verschillende schakelaars in UI kan in worden gevonden [overzicht van bronconnectors](../../home.md).

## Vul uw [!DNL Real-Time Customer Profile] data

Om klantenprofielen te verrijken, moet het bronschema van de doeldataset voor gebruik binnen compatibel zijn [!DNL Real-Time Customer Profile]. Een compatibel schema voldoet aan de volgende vereisten:

- Het schema heeft minstens één die attribuut als identiteitseigenschap wordt gespecificeerd.
- Het schema heeft een identiteitseigenschap die als primaire identiteit wordt bepaald.
- Er bestaat een toewijzing binnen de gegevensstroom waarin de primaire identiteit een doelkenmerk is.

Klik in de werkruimte Bronnen op de knop **[!UICONTROL Browse]** gebruiken om uw basisverbindingen weer te geven. Zoek in de weergegeven lijst de verbinding met de gegevensstroom waarmee u de profielen wilt vullen. Klik op de naam van de verbinding om de details te openen.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

De verbinding **[!UICONTROL Source activity]** het scherm verschijnt, tonend de datasets die de verbinding brongegevens in opneemt. Klik de naam van de dataset u wilt toelaten voor [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

De **[!UICONTROL Dataset activity]** wordt weergegeven. De **[!UICONTROL Properties]** de kolom aan de rechterkant van het scherm toont de details van de dataset, en omvat een **[!UICONTROL Profile]** schakelaar en een verbinding aan het schema de dataset volgt. Klik de naam van het schema om zijn samenstelling te bekijken.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

De **[!UICONTROL Schema Editor]** wordt weergegeven en toont u de structuur van het schema in het middelste canvas. Selecteer in het canvas het veld dat u als primaire identiteit wilt instellen. Onder de **[!UICONTROL Field properties]** selecteert u de **[!UICONTROL Identity]** selectievakje, dan **[!UICONTROL Primary identity]**. Selecteer ten slotte de gewenste **[!UICONTROL Identity namespace]** en klik vervolgens op **[!UICONTROL Apply]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Klik op het bovenste object van de structuur van het schema en op de knop **[!UICONTROL Schema properties]** wordt weergegeven. Het schema inschakelen voor [!DNL Profile] door de **[!UICONTROL Profile]** switch. Klikken **[!UICONTROL Save]** om uw wijzigingen te voltooien.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Nu het schema is ingeschakeld voor [!DNL Profile], terug naar de **[!UICONTROL Dataset activity]** het scherm en laat de dataset voor toe [!DNL Profile] door op de knop **[!UICONTROL Profile]** schakelen binnen de **[!UICONTROL Properties]** kolom.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Met zowel die schema als dataset voor wordt toegelaten [!DNL Profile]Gegevens die in die dataset worden opgenomen zullen nu ook klantenprofielen bevolken.

>[!NOTE]
>
>Bestaande gegevens binnen een recent ingeschakelde gegevensset worden niet gebruikt door [!DNL Profile].

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de inkomende gegevens geactiveerd voor [!DNL Profile] bevolking. Zie voor meer informatie de [[!DNL Real-Time Customer Profile] overzicht](../../../profile/home.md).
