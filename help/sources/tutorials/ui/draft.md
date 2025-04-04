---
title: Conceptgegevens in de gebruikersinterface
description: Leer hoe u uw gegevens als concept opslaat en deze later publiceert wanneer u de werkruimte Bronnen gebruikt.
exl-id: ee00798e-152a-4618-acb3-db40f2f55fae
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---

# Conceptgegevens in de gebruikersinterface

Sla de voortgang van de onvoltooide gegevensinvoer op door de gegevensstroom in te stellen op een conceptstatus. U kunt uw geschreven gegevensstromen op een later tijdstip hervatten en voltooien.

Dit document bevat stappen voor het opslaan van uw gegevensstromen wanneer u de werkruimte Bronnen in de gebruikersinterface van Adobe Experience Platform gebruikt.

## Aan de slag

Voor dit document is een goed begrip van de volgende Adobe Experience Platform-componenten vereist:

* [ Bronnen ](../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.

## Een gegevensstroom opslaan als concept

U kunt de voortgang van het maken van de gegevensstroom op elk gewenst moment pauzeren nadat u de gegevens hebt geselecteerd die u naar Experience Platform wilt verzenden.

Selecteer bijvoorbeeld **[!UICONTROL Save as draft]** als u de voortgang wilt opslaan tijdens de detailstap voor de gegevensstroom.

![ de dataflow detailstap van het bronwerkschema met sparen als geselecteerd ontwerp.](../../images/tutorials/draft/save-as-draft.png)

Nadat u uw concept hebt opgeslagen, gaat u naar de pagina van uw account, waar u een lijst kunt zien met uw bestaande gegevensstromen, inclusief uw concepten.

![ een lijst van gegevens voor een bepaalde rekening.](../../images/tutorials/draft/draft-dataflow.png)

>[!TIP]
>
>Getekende gegevens worden niet ingeschakeld en de status wordt ingesteld op `draft` .

Als u wilt doorgaan op uw concept, selecteert u de ovalen (`...`) naast de naam van de gegevensstroom en selecteert u vervolgens **[!UICONTROL Update dataflow]** .

>[!NOTE]
>
>Als uw concept planningsinformatie bevat, geeft het vervolgkeuzevenster u ook de optie **[!UICONTROL Edit schedule]** .

![ dropdown venster van A met geselecteerde updategegevens.](../../images/tutorials/draft/update-dataflow.png)

### Toegang tot uw concepten uit de broncatalogus

Via de dataflows-catalogus hebt u ook toegang tot uw conceptgegevens. Selecteer **[!UICONTROL Dataflows]** in de bovenste koptekst om de dataflows-catalogus te openen. Van hier, vind uw ontwerp van de lijst van bestaande dataflows in uw organisatie, selecteer de ellipsen (`...`) naast zijn naam, en selecteer dan **[!UICONTROL Update dataflow]**.

![ een lijst van gegevens voor een bepaalde organisatie.](../../images/tutorials/draft/catalog-access.png)

## Uw conceptgegevensstroom publiceren

U keert terug naar de [!UICONTROL Add data] stap van de bronwerkstroom, waar u het formaat van uw gegevens kunt opnieuw bevestigen en op uw gegevensstroom verder kunt gaan.

Selecteer **[!UICONTROL Next]** als u de opmaak, het scheidingsteken en het compressietype van de gegevens hebt bevestigd.

![ voegt gegevensstap van bronwerkschema toe.](../../images/tutorials/draft/select-data.png)

Bevestig vervolgens uw gegevens over de gegevensstroom. Met de dataflow-detailinterface kunt u configuraties bijwerken rondom de naam, beschrijving, gedeeltelijke opname, instellingen voor foutdiagnose en voorkeuren voor waarschuwingen.

Nadat u de configuraties hebt voltooid, selecteert u **[!UICONTROL Next]** om door te gaan.

![ de dataflow detailstap van het bronwerkschema.](../../images/tutorials/draft/dataflow-detail.png)

De stap [!UICONTROL Mapping] wordt weergegeven. Tijdens deze stap, kunt u de kaartconfiguraties van uw dataflow aanpassen. Voor een uitvoerige gids over de gegevens prep functies die voor afbeelding worden gebruikt, bezoek de [ gegevens prep UI gids ](../../../data-prep/ui/mapping.md).

Als u de configuratie van de toewijzing hebt voltooid, selecteert u **[!UICONTROL Next]** om door te gaan.

![ de afbeeldingsstap van het bronwerkschema.](../../images/tutorials/draft/mapping.png)

Gebruik de stap [!UICONTROL Scheduling] om een innameprogramma voor uw gegevensstroom te bepalen. U kunt de innamefrequentie instellen op `once` , `minute` , `hour` , `day` of `week` . Als u klaar bent, selecteert u **[!UICONTROL Next]** om door te gaan.

![ de het plannen stap van het bronwerkschema.](../../images/tutorials/draft/scheduling.png)

Controleer ten slotte de details van uw gegevensstroom en selecteer **[!UICONTROL Finish]** om uw concept te publiceren.

![ de overzichtsstap van het bronwerkschema.](../../images/tutorials/draft/review.png)

Nadat u een concept hebt opgeslagen en gepubliceerd, wordt de gegevensstroom ingeschakeld en kunt u deze niet meer opnieuw instellen als een concept.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u geleerd hoe u uw voortgang kunt opslaan en een gegevensstroom als concept kunt instellen. Voor meer informatie over bronnen, bezoek het [ overzicht van bronnen ](../../home.md).
