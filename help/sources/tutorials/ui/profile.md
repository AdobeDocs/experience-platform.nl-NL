---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Activeer binnenkomende brongegevens om klantenprofielen te bevolken
topic: overview
translation-type: tm+mt
source-git-commit: d6d2faf3d5eabcd8e948d3717fd8f8df4b9cb85a

---


# Activeer binnenkomende brongegevens om klantenprofielen te bevolken

De binnenkomende gegevens van uw bronschakelaar kunnen worden gebruikt om uw gegevens van het Profiel van de Klant in real time te verrijken en te bevolken.

## Aan de slag

Voor deze zelfstudie is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

- [XDM-systeem](../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
   - [Basisbeginselen van de schemacompositie](../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie](../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [Klantprofiel](../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Bovendien, vereist dit leerprogramma dat u reeds een bronschakelaar hebt gecreeerd en gevormd.  Een lijst van leerprogramma&#39;s voor het creëren van verschillende schakelaars in UI kan in het overzicht [van](../../home.md)bronschakelaars worden gevonden.

## Uw gegevens van het Profiel van de Klant in real time bevolken

Om klantprofielen te verrijken, moet het bronschema van de doeldataset voor gebruik in het Profiel van de Klant in real time compatibel zijn. Een compatibel schema voldoet aan de volgende vereisten:

- Het schema heeft minstens één die attribuut als identiteitseigenschap wordt gespecificeerd.
- Het schema heeft een identiteitseigenschap die als primaire identiteit wordt bepaald.
- Er bestaat een toewijzing binnen de gegevensstroom waarin de primaire identiteit een doelkenmerk is.

Klik in de werkruimte Bronnen op het tabblad **Bladeren** om uw basisverbindingen weer te geven. Zoek in de weergegeven lijst de verbinding met de gegevensstroom waarmee u de profielen wilt vullen. Klik op de naam van de verbinding om de details te openen.

![](../../images/tutorials/dataflow/cloud-storage/browse.png)

Het scherm van de *Bron van de verbinding activiteit* verschijnt, tonend de datasets die de verbinding brongegevens in opneemt. Klik op de naam van de gegevensset die u wilt inschakelen voor Profiel.

![](../../images/tutorials/dataflow/cloud-storage/dataset-dataflow.png)

Het scherm *Dataset-activiteit* wordt weergegeven. De *kolom van Eigenschappen* op de rechterkant van het scherm toont de details van de dataset, en omvat een schakelaar van het **Profiel** en een verbinding aan het schema de dataset volgt. Klik de naam van het schema om zijn samenstelling te bekijken.

![](../../images/tutorials/dataflow/cloud-storage/select-dataset-schema.png)

De *Schema-editor* wordt weergegeven en toont de structuur van het schema in het middelste canvas. Selecteer in het canvas het veld dat u als primaire identiteit wilt instellen. Selecteer onder het tabblad *Veldeigenschappen* dat wordt weergegeven het selectievakje **Identiteit** en vervolgens **Primaire identiteit**. Selecteer ten slotte een geschikte naamruimte **** Identiteit en klik op **Toepassen**.

![](../../images/tutorials/dataflow/cloud-storage/set-schema-identity.png)

Klik op het bovenste object van de structuur van het schema en de kolom met *Schema-eigenschappen* wordt weergegeven. Schakel de **profielschakelaar** in om het schema voor Profiel in te schakelen. Klik op **Opslaan** om de wijzigingen te voltooien.

![](../../images/tutorials/dataflow/cloud-storage/enable-profile.png)

Nu het schema voor Profiel wordt toegelaten, terugkeer aan het de activiteitenscherm van de *Dataset* en laat de dataset voor Profiel toe door de knevel van het **Profiel** binnen de kolom van *Eigenschappen* te klikken.

![](../../images/tutorials/dataflow/cloud-storage/enable-dataset-profile.png)

Met zowel het schema als de dataset die voor Profiel wordt toegelaten, zullen de gegevens in die dataset worden opgenomen ook klantenprofielen bevolken.

>[!NOTE] Bestaande gegevens binnen een recent ingeschakelde gegevensset worden niet gebruikt door profiel

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de binnenkomende gegevens voor de profielpopulatie geactiveerd. Zie het overzicht [van het profiel van de](../../../profile/home.md)real-time klant voor meer informatie.