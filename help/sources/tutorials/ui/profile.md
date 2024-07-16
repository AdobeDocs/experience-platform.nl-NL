---
keywords: Experience Platform;thuis;populaire onderwerpen;activeer binnenkomende gegevens;bevolk profiel;bevolkt rtcp;bevolkt verenigd profiel
solution: Experience Platform
title: Inkomende Source-gegevens activeren om klantprofielen te vullen in de gebruikersinterface
type: Tutorial
description: De binnenkomende gegevens van uw bronschakelaar kunnen worden gebruikt om uw gegevens van het Profiel van de Klant in real time te verrijken en te bevolken.
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# Inkomende brongegevens activeren om klantprofielen te vullen

De binnenkomende gegevens van uw bronschakelaar kunnen aan het verrijken van en het bevolken van uw [!DNL Real-Time Customer Profile] gegevens worden gebruikt.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)]  Systeem ](../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   - [ Grondbeginselen van schemacompositie ](../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [ het leerprogramma van de Redacteur van het Schema ](../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Bovendien, vereist dit leerprogramma dat u reeds een bronschakelaar hebt gecreeerd en gevormd.  Een lijst van leerprogramma&#39;s voor het creëren van verschillende schakelaars in UI kan in het [ overzicht van bronschakelaars ](../../home.md) worden gevonden.

## Uw [!DNL Real-Time Customer Profile] gegevens vullen

Om klantprofielen te verrijken, moet het bronschema van de doeldataset voor gebruik in [!DNL Real-Time Customer Profile] compatibel zijn. Een compatibel schema voldoet aan de volgende vereisten:

- Het schema heeft minstens één die attribuut als identiteitseigenschap wordt gespecificeerd.
- Het schema heeft een identiteitseigenschap die als primaire identiteit wordt bepaald.
- Er bestaat een toewijzing binnen de gegevensstroom waarin de primaire identiteit een doelkenmerk is.

Klik in de werkruimte Bronnen op het tabblad **[!UICONTROL Browse]** om de basisverbindingen weer te geven. Zoek in de weergegeven lijst de verbinding met de gegevensstroom waarmee u de profielen wilt vullen. Klik op de naam van de verbinding om de details te openen.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

Het scherm van de verbinding **[!UICONTROL Source activity]** verschijnt, tonend de datasets die de verbinding brongegevens in neemt. Klik op de naam van de gegevensset die u wilt inschakelen voor [!DNL Profile] .

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

Het scherm **[!UICONTROL Dataset activity]** wordt weergegeven. In de kolom **[!UICONTROL Properties]** aan de rechterkant van het scherm worden de details van de gegevensset weergegeven. Deze kolom bevat een **[!UICONTROL Profile]** -switch en een koppeling naar het schema waarop de gegevensset zich bevindt. Klik de naam van het schema om zijn samenstelling te bekijken.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

De **[!UICONTROL Schema Editor]** wordt weergegeven en toont de structuur van het schema in het middelste canvas. Selecteer in het canvas het veld dat u als primaire identiteit wilt instellen. Selecteer onder het tabblad **[!UICONTROL Field properties]** dat wordt weergegeven het selectievakje **[!UICONTROL Identity]** en vervolgens **[!UICONTROL Primary identity]** . Selecteer ten slotte een geschikte **[!UICONTROL Identity namespace]** en klik op **[!UICONTROL Apply]** .

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Klik op het bovenste object van de structuur van het schema en de kolom **[!UICONTROL Schema properties]** verschijnt. Schakel de **[!UICONTROL Profile]** -switch in en uit om het schema voor [!DNL Profile] in te schakelen. Klik op **[!UICONTROL Save]** om de wijzigingen te voltooien.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Nu het schema is ingeschakeld voor [!DNL Profile] , gaat u terug naar het **[!UICONTROL Dataset activity]** -scherm en schakelt u de gegevensset voor [!DNL Profile] in door op de **[!UICONTROL Profile]** -schakeloptie in de **[!UICONTROL Properties]** -kolom te klikken.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Als zowel het schema als de dataset voor [!DNL Profile] wordt toegelaten, zullen de gegevens die in die dataset worden opgenomen ook klantenprofielen bevolken.

>[!NOTE]
>
>Bestaande gegevens binnen een recent ingeschakelde gegevensset worden niet door [!DNL Profile] gebruikt.

## Volgende stappen

Aan de hand van deze zelfstudie hebt u de inkomende gegevens voor [!DNL Profile] bevolkingsgroep geactiveerd. Voor meer informatie, zie het [[!DNL Real-Time Customer Profile]  overzicht ](../../../profile/home.md).
