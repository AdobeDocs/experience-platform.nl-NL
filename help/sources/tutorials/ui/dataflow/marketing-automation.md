---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Vorm een dataflow voor een schakelaar van de marketing automatisering in UI
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 0%

---


# Vorm een dataflow voor een schakelaar van de marketing automatisering in UI

Een dataflow is een geplande taak die gegevens van een bron aan een [!DNL Platform] dataset terugwint en opneemt. Deze zelfstudie biedt stappen om een nieuwe gegevensstroom te configureren met behulp van uw account voor marketingautomatisering.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Adobe Experience Platform:

- [XDM-systeem](../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
   - [Basisbeginselen van de schemacompositie](../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie](../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [Klantprofiel](../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Bovendien moet u voor deze zelfstudie al een account voor marketingautomatisering hebben gemaakt. Een lijst van leerprogramma&#39;s voor het creëren van verschillende marketing automatiseringsschakelaars in UI kan in het overzicht [van](../../../home.md)bronschakelaars worden gevonden.

## Gegevens selecteren

Nadat u uw marketingautomatiseringsaccount hebt gemaakt, wordt de stap Gegevens ** selecteren weergegeven en krijgt u een interactieve interface waarmee u de bestandshiërarchie kunt verkennen.

- De linkerhelft van de interface is een directorybrowser waarin de bestanden en mappen van uw server worden weergegeven.
- Met de rechterhelft van de interface kunt u maximaal 100 rijen gegevens uit een compatibel bestand voorvertonen.

Selecteer de directory die u wilt gebruiken en klik op **[!UICONTROL Volgende]**.

![select-data](../../../images/tutorials/dataflow/marketing-automation/select-data.png)

## Gegevensvelden toewijzen aan een XDM-schema

De stap *[!UICONTROL Toewijzing]* verschijnt, die een interactieve interface verstrekt om de brongegevens aan een [!DNL Platform] dataset in kaart te brengen.

Kies een dataset voor binnenkomende gegevens waarin moeten worden opgenomen. U kunt of een bestaande dataset gebruiken of een nieuwe dataset tot stand brengen.

### Een bestaande gegevensset gebruiken

Om gegevens in een bestaande dataset in te voeren, selecteer **[!UICONTROL Gebruik bestaande dataset]**, dan klik het datasetpictogram.

![use-existing-dataset](../../../images/tutorials/dataflow/marketing-automation/use-existing-dataset.png)

Het dialoogvenster _Gegevensset_ selecteren wordt geopend. Zoek de gegevensset die u wilt gebruiken, selecteer deze en klik op **[!UICONTROL Doorgaan]**.

![select-existing-dataset](../../../images/tutorials/dataflow/marketing-automation/select-existing-dataset.png)

### Een nieuwe gegevensset gebruiken

Om gegevens in een nieuwe dataset in te voeren, **[!UICONTROL creeer nieuwe dataset]** en ga een naam en een beschrijving voor de dataset op de verstrekte gebieden in.

Tijdens dit proces kunt u ook *[!UICONTROL gedeeltelijke inname]* en *[!UICONTROL foutdiagnose]* inschakelen. Als u *[!UICONTROL Gedeeltelijke opname]* inschakelt, kunt u gegevens met fouten, tot een bepaalde drempel die u kunt instellen, insluiten. Als u de diagnostische functie Fout inschakelt, worden details weergegeven over onjuiste gegevens die afzonderlijk in een batch worden opgeslagen. Voor meer informatie, zie het [gedeeltelijke partijingestie overzicht](../../../../ingestion/batch-ingestion/partial.md).

Klik op het schemapictogram als u klaar bent.

![use-new-dataset](../../../images/tutorials/dataflow/marketing-automation/use-new-dataset.png)

Het dialoogvenster Schema ** selecteren wordt geopend. Selecteer het schema u wenst om op de nieuwe dataset toe te passen, dan klik **[!UICONTROL Gedaan]**.

![selectieschema](../../../images/tutorials/dataflow/marketing-automation/select-schema.png)

Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of mapperfuncties te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Raadpleeg de zelfstudie over het [toewijzen van CSV-gegevens aan XDM-schemavelden](../../../../ingestion/tutorials/map-a-csv-file.md)voor meer informatie over gegevenstoewijzing en mapperfuncties.

Klik op **[!UICONTROL Volgende]** als de brongegevens zijn toegewezen.

![](../../../images/tutorials/dataflow/marketing-automation/mapping.png)

## Planninguitvoering

De *[!UICONTROL Plannende]* stap verschijnt, toestaand u om een innameprogramma te vormen om de geselecteerde brongegevens automatisch in te nemen gebruikend de gevormde afbeeldingen. De volgende lijst schetst de verschillende configureerbare gebieden voor het plannen:

| Veld | Beschrijving |
| --- | --- |
| Frequentie | Selecteerbare frequenties zijn Minuut, Uur, Dag en Week. |
| Interval | Een geheel getal dat het interval voor de geselecteerde frequentie instelt. |
| Begintijd | Een UTC-tijdstempel waarvoor de eerste invoer wordt uitgevoerd. |
| Achtergrond | Een booleaanse waarde die bepaalt welke gegevens eerst worden ingevoerd. Als *[!UICONTROL Backfill]* is ingeschakeld, worden alle huidige bestanden in het opgegeven pad tijdens de eerste geplande opname opgenomen. Als *[!UICONTROL Backfill]* is uitgeschakeld, worden alleen de bestanden opgenomen die tussen de eerste opname en de *[!UICONTROL begintijd]* worden geladen. Bestanden die vóór het begin van het *[!UICONTROL starten]* zijn geladen, worden niet opgenomen. |

Dataflows worden ontworpen om gegevens automatisch in te voeren op een geplande basis. Als u slechts één keer wilt opnemen via deze workflow, kunt u dit doen door de **[!UICONTROL Frequentie]** in te stellen op &quot;Dag&quot; en een zeer groot aantal toe te passen voor het **[!UICONTROL Interval]**, zoals 10000 of een vergelijkbaar aantal.

Geef waarden op voor het schema en klik op **[!UICONTROL Volgende]**.

![plannen](../../../images/tutorials/dataflow/marketing-automation/scheduling.png)

## Controleer uw gegevensstroom

De stap *[!UICONTROL Revisie]* wordt weergegeven, zodat u de nieuwe gegevensstroom kunt controleren voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

- *[!UICONTROL Verbinding]*: Toont het brontype, de relevante weg van het gekozen brondossier, en de hoeveelheid kolommen binnen dat brondossier.
- *[!UICONTROL Gegevensset- en kaartvelden]* toewijzen: Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset zich aan houdt.
- *[!UICONTROL Planning]*: Toont de actieve periode, de frequentie, en het interval van het innameprogramma.

Nadat u de gegevensstroom hebt gereviseerd, klikt u op **[!UICONTROL Voltooien]** en laat u enige tijd over tot de gegevensstroom.

![revisie](../../../images/tutorials/dataflow/marketing-automation/review.png)

## Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen. Voer de onderstaande stappen uit om toegang te krijgen tot de gegevenssetcontrole van een gegevensstroom.

Selecteer in de werkruimte *[!UICONTROL Bronnen]* de marketingautomatiseringsbron die u wilt weergeven in de categorie *[!UICONTROL Marketing Automation]* . Selecteer *[!UICONTROL Connect-bron]* om de verificatieinterface te starten. Als u een bestaande gegevensstroom wilt weergeven, selecteert u *[!UICONTROL Bestaande account]* en selecteert u de account die u wilt openen.

![monitor](../../../images/tutorials/dataflow/marketing-automation/monitor.png)

Het scherm *[!UICONTROL Bronactiviteit]* wordt weergegeven. Van hier, klik de naam van een dataset waarvan activiteit u wilt controleren.

![select-dataflow-dataset](../../../images/tutorials/dataflow/marketing-automation/select-dataflow-dataset.png)

Het scherm *[!UICONTROL Dataset-activiteit]* wordt weergegeven. Op deze pagina wordt de snelheid van berichten weergegeven die in de vorm van een grafiek worden gebruikt.

![datasetactiviteit](../../../images/tutorials/dataflow/marketing-automation/dataset-activity.png)

Voor meer informatie over het controleren van datasets en ingestie, verwijs naar het leerprogramma bij het [controleren van het stromen gegevens](../../../../ingestion/quality/monitor-data-flows.md).

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes een dataflow gecreeerd om gegevens van een systeem van de marketingautomatisering in te brengen en inzicht verworven in de controle van datasets. Inkomende gegevens kunnen nu worden gebruikt door downstreamdiensten [!DNL Platform] zoals [!DNL Real-time Customer Profile] en [!DNL Data Science Workspace]. Raadpleeg de volgende documenten voor meer informatie:

- [Overzicht van het realtime klantprofiel](../../../../profile/home.md)
- [Overzicht van de Data Science Workspace](../../../../data-science-workspace/home.md)

## Aanhangsel

De volgende secties verstrekken extra informatie voor het werken met bronschakelaars.

### Een gegevensstroom uitschakelen

Wanneer een gegevensstroom wordt gecreeerd, wordt het onmiddellijk actief en neemt gegevens volgens het programma op het werd gegeven. U kunt een actieve gegevensstroom op elk ogenblik onbruikbaar maken door de instructies hieronder te volgen.

Selecteer in het *[!UICONTROL verificatiescherm]* de naam van de basisverbinding die is gekoppeld aan de gegevensstroom die u wilt uitschakelen.

![](../../../images/tutorials/dataflow/marketing-automation/monitor.png)

De pagina _Bronactiviteit_ wordt weergegeven. Selecteer de actieve gegevensstroom van de lijst om zijn kolom van *[!UICONTROL Eigenschappen]* op de rechterkant van het scherm te openen, die een **[!UICONTROL Toegelaten]** knevelknoop bevat. Klik op de schakeloptie om de gegevensstroom uit te schakelen. Dezelfde schakeloptie kan worden gebruikt om een gegevensstroom opnieuw in te schakelen nadat deze is uitgeschakeld.

![disable](../../../images/tutorials/dataflow/marketing-automation/disable.png)

### Binnenkomende gegevens voor [!DNL Profile] populatie activeren

De binnenkomende gegevens van uw bronschakelaar kunnen worden gebruikt om uw [!DNL Real-time Customer Profile] gegevens te verrijken en te bevolken. Zie de zelfstudie over de [!DNL Real-time Customer Profile] profielpopulatie [](../profile.md)voor meer informatie over het vullen van gegevens.
