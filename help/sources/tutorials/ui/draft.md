---
title: Conceptgegevens in de gebruikersinterface
description: Leer hoe u uw gegevens als concept opslaat en deze later publiceert wanneer u de werkruimte Bronnen gebruikt.
exl-id: ee00798e-152a-4618-acb3-db40f2f55fae
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---

# Conceptgegevens in de gebruikersinterface

Sla de voortgang van de onvoltooide gegevensinvoer op door de gegevensstroom in te stellen op een conceptstatus. U kunt uw geschreven gegevensstromen op een later tijdstip hervatten en voltooien.

Dit document bevat stappen voor het opslaan van uw gegevensstromen wanneer u de werkruimte Bronnen in de gebruikersinterface van Adobe Experience Platform gebruikt.

## Aan de slag

Voor dit document is een goed begrip van de volgende Adobe Experience Platform-componenten vereist:

* [Bronnen](../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de platformservices.

## Een gegevensstroom opslaan als concept

U kunt de voortgang van het maken van de gegevensstroom op elk gewenst moment pauzeren nadat u de gegevens hebt geselecteerd die u wilt overbrengen naar het platform.

Als u bijvoorbeeld de voortgang wilt opslaan tijdens de stap met de details voor de gegevensstroom, selecteert u **[!UICONTROL Save as draft]**.

![De stap met details over gegevensstroom van de bronworkflow met Opslaan als geselecteerd concept.](../../images/tutorials/draft/save-as-draft.png)

Nadat u uw concept hebt opgeslagen, gaat u naar de pagina van uw account, waar u een lijst kunt zien met uw bestaande gegevensstromen, inclusief uw concepten.

![Een lijst met gegevensstromen voor een bepaalde account.](../../images/tutorials/draft/draft-dataflow.png)

>[!TIP]
>
>De status van de getekende gegevensstromen wordt niet ingeschakeld en ingesteld op `draft`.

Als u wilt doorgaan met uw concept, selecteert u de ellipsen (`...`) naast de naam van de gegevensstroom en selecteer **[!UICONTROL Update dataflow]**.

>[!NOTE]
>
>Als uw concept planningsinformatie bevat, kunt u in het vervolgkeuzevenster ook het volgende kiezen: **[!UICONTROL Edit schedule]**.

![Een vervolgkeuzevenster met de updatedatum geselecteerd.](../../images/tutorials/draft/update-dataflow.png)

### Toegang tot uw concepten uit de broncatalogus

Via de dataflows-catalogus hebt u ook toegang tot uw conceptgegevens. Selecteren **[!UICONTROL Dataflows]** in de bovenste koptekst om toegang te krijgen tot de dataflow-catalogus. Van hier, vind uw ontwerp van de lijst van bestaande dataflows in uw organisatie, selecteer de ellipsen (`...`) naast de naam en selecteer vervolgens **[!UICONTROL Update dataflow]**.

![Een lijst met gegevensstromen voor een bepaalde organisatie.](../../images/tutorials/draft/catalog-access.png)

## Uw conceptgegevensstroom publiceren

U bent teruggekeerd aan [!UICONTROL Add data] stap van de workflow voor bronnen, waarin u de indeling van uw gegevens opnieuw kunt bevestigen en verder kunt gaan met het verwerken van uw gegevensstroom.

Nadat u de opmaak, het scheidingsteken en het compressietype van de gegevens hebt bevestigd, selecteert u **[!UICONTROL Next]** om verder te gaan.

![De gegevensstap toevoegen van de workflow voor bronnen.](../../images/tutorials/draft/select-data.png)

Bevestig vervolgens uw gegevens over de gegevensstroom. Met de dataflow-detailinterface kunt u configuraties bijwerken rondom de naam, beschrijving, gedeeltelijke opname, instellingen voor foutdiagnose en voorkeuren voor waarschuwingen.

Nadat u de configuraties hebt voltooid, selecteert u **[!UICONTROL Next]** om verder te gaan.

![De stap met details van de gegevensstroom van de bronworkflow.](../../images/tutorials/draft/dataflow-detail.png)

De [!UICONTROL Mapping] wordt weergegeven. Tijdens deze stap, kunt u de kaartconfiguraties van uw dataflow aanpassen. Voor een uitgebreide gids over de gegevens prep functies die voor afbeelding worden gebruikt, bezoek [UI-hulplijn voor gegevenprep](../../../data-prep/ui/mapping.md).

Als u de configuratie van de toewijzing hebt voltooid, selecteert u **[!UICONTROL Next]** om verder te gaan.

![De toewijzingsstap van de workflow voor bronnen.](../../images/tutorials/draft/mapping.png)

Gebruik de [!UICONTROL Scheduling] stap om een innameprogramma voor uw gegevensstroom te vestigen. U kunt de innamefrequentie instellen op `once`, `minute`, `hour`, `day`, of `week`. Selecteer **[!UICONTROL Next]** om verder te gaan.

![De planningsstap van de bronworkflow.](../../images/tutorials/draft/scheduling.png)

Controleer ten slotte de details van uw gegevensstroom en selecteer **[!UICONTROL Finish]** uw concept publiceren.

![De revisiestap van de workflow voor bronnen.](../../images/tutorials/draft/review.png)

Nadat u een concept hebt opgeslagen en gepubliceerd, wordt de gegevensstroom ingeschakeld en kunt u deze niet meer opnieuw instellen als een concept.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u geleerd hoe u uw voortgang kunt opslaan en een gegevensstroom als concept kunt instellen. Ga voor meer informatie over bronnen naar de [overzicht van bronnen](../../home.md).
