---
keywords: Experience Platform;thuis;populaire onderwerpen;betaalaansluiting
solution: Experience Platform
title: Een gegevensstroom configureren voor een verbinding met een betalingsbron in de gebruikersinterface
topic-legacy: overview
type: Tutorial
description: Een dataflow is een geplande taak die gegevens van een bron aan een dataset van Adobe Experience Platform terugwint en opneemt. Deze zelfstudie bevat stappen voor het configureren van een nieuwe gegevensstroom met uw betaalaccount.
exl-id: 7355435b-c038-4310-b04a-8ac6b6723b9b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1400'
ht-degree: 0%

---

# Een gegevensstroom configureren voor een betalingsverbinding in de gebruikersinterface

Een dataflow is een geplande taak die gegevens van een bron aan een dataset van Adobe Experience Platform terugwint en opneemt. Deze zelfstudie bevat stappen voor het configureren van een nieuwe gegevensstroom met uw betaalaccount.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Systeem](../../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Experience Platform] klantenervaring worden georganiseerd.
   - [Basisbeginselen van de schemacompositie](../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie](../../../../xdm/tutorials/create-schema-ui.md) Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-time Customer Profile]](../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Bovendien moet u voor deze zelfstudie al een betaalaccount hebben gemaakt. Een lijst met zelfstudies voor het maken van verschillende betalingsconnectors in de gebruikersinterface vindt u in het [overzicht van bronconnectors](../../../home.md).

## Gegevens selecteren

Nadat u uw betaalaccount hebt gemaakt, wordt de stap **[!UICONTROL Select data]** weergegeven en krijgt u een interactieve interface om de bestandshiërarchie te verkennen.

- De linkerhelft van de interface is een directorybrowser waarin de bestanden en mappen van uw server worden weergegeven.
- Met de rechterhelft van de interface kunt u maximaal 100 rijen gegevens uit een compatibel bestand voorvertonen.

Met de optie **[!UICONTROL Search]** boven aan de pagina kunt u snel de brongegevens identificeren die u wilt gebruiken.

>[!NOTE]
>
>De optie van onderzoeksbrongegevens is beschikbaar aan alle op tabelvorm-gebaseerde bronschakelaars behalve de Analytics, Classifications, de Hubs van de Gebeurtenis, en de schakelaars van Kinesis.

Wanneer u de brongegevens hebt gevonden, selecteert u de map en klikt u op **[!UICONTROL Next]**.

![select-data](../../../images/tutorials/dataflow/all-tabular/select-data.png)

## Gegevensvelden toewijzen aan een XDM-schema

De stap **[!UICONTROL Mapping]** verschijnt, die een interactieve interface verstrekken om de brongegevens aan een [!DNL Platform] dataset in kaart te brengen.

Kies een dataset voor binnenkomende gegevens waarin moeten worden opgenomen. U kunt of een bestaande dataset gebruiken of een nieuwe dataset tot stand brengen.

### Een bestaande gegevensset gebruiken

Om gegevens in een bestaande dataset in te voeren, selecteer **[!UICONTROL Use existing dataset]**, dan klik het datasetpictogram.

![use-existing-dataset](../../../images/tutorials/dataflow/payments/existing-dataset.png)

Het dialoogvenster **[!UICONTROL Select dataset]** wordt weergegeven. Zoek de dataset u wenst te gebruiken, het te selecteren, dan **[!UICONTROL Continue]** te klikken.

![select-existing-dataset](../../../images/tutorials/dataflow/payments/select-dataset.png)

### Een nieuwe gegevensset gebruiken

Om gegevens in een nieuwe dataset in te voeren, selecteer **[!UICONTROL Create new dataset]** en ga een naam en een beschrijving voor de dataset op de verstrekte gebieden in.

U kunt een schemagebied vastmaken door een schemanaam in **[!UICONTROL Select schema]** onderzoeksbar in te gaan. U kunt ook het vervolgkeuzepictogram selecteren om een lijst met bestaande schema&#39;s weer te geven. U kunt ook **[!UICONTROL Advanced search]** selecteren om toegang te krijgen tot het scherm van bestaande schema&#39;s met hun respectievelijke details.

Tijdens deze stap, kunt u uw dataset voor [!DNL Real-time Customer Profile] toelaten en een holistische mening van de attributen en het gedrag van een entiteit creëren. De gegevens van alle toegelaten datasets zullen in [!DNL Profile] worden omvat en de veranderingen worden toegepast wanneer u uw gegevensstroom bewaart.

Schakel de knop **[!UICONTROL Profile dataset]** in of uit om uw doelgegevensset in te schakelen voor [!DNL Profile].

![create-new-dataset](../../../images/tutorials/dataflow/payments/new-dataset.png)

Het dialoogvenster **[!UICONTROL Select schema]** wordt weergegeven. Selecteer het schema u wenst om op de nieuwe dataset toe te passen, dan klik **[!UICONTROL Done]**.

![selectieschema](../../../images/tutorials/dataflow/payments/select-schema.png)

Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of mapperfuncties te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Raadpleeg de zelfstudie over het toewijzen van CSV-gegevens aan XDM-schemavelden](../../../../ingestion/tutorials/map-a-csv-file.md) voor meer informatie over gegevenstoewijzing en mapperfuncties.[

>[!TIP]
>
>[!DNL Platform] verstrekt intelligente aanbevelingen voor auto-in kaart gebrachte gebieden die op het doelschema of de dataset worden gebaseerd dat u selecteerde. U kunt toewijzingsregels handmatig aanpassen aan uw gebruiksgevallen.

![](../../../images/tutorials/dataflow/all-tabular/mapping.png)

Selecteer **[!UICONTROL Preview data]** om toewijzingsresultaten van maximaal 100 rijen steekproefgegevens van de geselecteerde dataset te zien.

Tijdens de voorvertoning krijgt de identiteitskolom de prioriteit als het eerste veld, omdat dit de belangrijkste informatie is die nodig is voor het valideren van toewijzingsresultaten.

![](../../../images/tutorials/dataflow/all-tabular/mapping-preview.png)

Selecteer **[!UICONTROL Close]** als de brongegevens zijn toegewezen.

## Planninguitvoering

De stap **[!UICONTROL Scheduling]** verschijnt, toestaand u om een insluitingsprogramma te vormen om de geselecteerde brongegevens automatisch in te nemen gebruikend de gevormde afbeeldingen. De volgende lijst schetst de verschillende configureerbare gebieden voor het plannen:

| Veld | Beschrijving |
| --- | --- |
| Frequentie | Selecteerbare frequenties zijn onder andere `Once`, `Minute`, `Hour`, `Day` en `Week`. |
| Interval | Een geheel getal dat het interval voor de geselecteerde frequentie instelt. |
| Begintijd | Een UTC-tijdstempel die aangeeft wanneer de eerste opname wordt uitgevoerd. |
| Achtergrond | Een booleaanse waarde die bepaalt welke gegevens eerst worden ingevoerd. Als **[!UICONTROL Backfill]** wordt toegelaten, zullen alle huidige dossiers in de gespecificeerde weg tijdens de eerste geplande opname worden opgenomen. Als **[!UICONTROL Backfill]** is uitgeschakeld, worden alleen de bestanden opgenomen die tussen de eerste opname en de begintijd worden geladen. Bestanden die vóór de begintijd zijn geladen, worden niet opgenomen. |
| Delta-kolom | Een optie met een gefilterde reeks gebieden van het bronschema van type, datum, of tijd. Dit veld wordt gebruikt om onderscheid te maken tussen nieuwe en bestaande gegevens. Incrementele gegevens worden opgenomen op basis van het tijdstempel van de geselecteerde kolom. |

Dataflows worden ontworpen om gegevens automatisch in te voeren op een geplande basis. Begin door de innamefrequentie te selecteren. Daarna, plaats het interval om de periode tussen twee stroomlooppas aan te wijzen. De waarde van het interval moet een geheel getal zijn dat niet gelijk is aan nul en moet worden ingesteld op groter dan of gelijk aan 15.

Als u de begintijd voor inname wilt instellen, past u de datum en tijd aan die worden weergegeven in het vak Begintijd. U kunt ook het kalenderpictogram selecteren om de begintijdwaarde te bewerken. De begintijd moet groter zijn dan of gelijk zijn aan de huidige UTC-tijd.

Selecteer **[!UICONTROL Load incremental data by]** om de deltakolom toe te wijzen. In dit veld wordt een onderscheid gemaakt tussen nieuwe en bestaande gegevens.

![](../../../images/tutorials/dataflow/databases/schedule-interval-on.png)

### Eenmalige gegevensstroom voor inname instellen

Als u eenmalige invoer wilt instellen, selecteert u de pijl voor de frequentieverlaging en selecteert u **[!UICONTROL Once]**.

>[!TIP]
>
>**[!UICONTROL Interval]** en niet zichtbaar  **[!UICONTROL Backfill]** zijn tijdens eenmalig gebruik.

Als u de juiste waarden voor het schema hebt opgegeven, selecteert u **[!UICONTROL Next]**.

![](../../../images/tutorials/dataflow/databases/schedule-once.png)

## Gegevens over gegevensstroom opgeven

De stap **[!UICONTROL Dataflow detail]** wordt weergegeven, zodat u een naam kunt geven en een korte beschrijving kunt geven van uw nieuwe gegevensstroom.

Tijdens dit proces kunt u **[!UICONTROL Partial ingestion]** en **[!UICONTROL Error diagnostics]** ook inschakelen. Als u **[!UICONTROL Partial ingestion]** inschakelt, kunt u gegevens met fouten tot een bepaalde drempel invoeren. Wanneer **[!UICONTROL Partial ingestion]** is ingeschakeld, sleept u de **[!UICONTROL Error threshold %]**-schijf om de foutdrempel van de batch aan te passen. U kunt de drempelwaarde ook handmatig aanpassen door het invoervak te selecteren. Voor meer informatie, zie [gedeeltelijk partijingesinzicht overzicht](../../../../ingestion/batch-ingestion/partial.md).

Geef waarden op voor de gegevensstroom en selecteer **[!UICONTROL Next]**.

![details gegevensstroom](../../../images/tutorials/dataflow/all-tabular/dataflow-detail.png)

## Controleer uw gegevensstroom

De stap **[!UICONTROL Review]** wordt weergegeven, zodat u de nieuwe gegevensstroom kunt controleren voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

- **[!UICONTROL Connection]**: Toont het brontype, de relevante weg van het gekozen brondossier, en de hoeveelheid kolommen binnen dat brondossier.
- **[!UICONTROL Assign dataset & map fields]**: Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset zich aan houdt.
- **[!UICONTROL Scheduling]**: Toont de actieve periode, de frequentie, en het interval van het innameprogramma.

Zodra u uw gegevensstroom hebt herzien, klik **[!UICONTROL Finish]** en laat wat tijd voor dataflow om worden gecreeerd.

![revisie](../../../images/tutorials/dataflow/payments/review.png)

## Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over innamepercentages, succes, en fouten te zien. Voor meer informatie over hoe te om dataflow te controleren, zie de zelfstudie over [het controleren van rekeningen en dataflows in UI](../monitor.md).

## Uw gegevensstroom verwijderen

U kunt gegevensstromen schrappen die niet meer noodzakelijk of verkeerd gecreeerd gebruikend de functie **[!UICONTROL Delete]** beschikbaar in de **[!UICONTROL Dataflows]** werkruimte zijn. Voor meer informatie over hoe te om dataflows te schrappen, zie de zelfstudie over [het schrappen van gegevensstromen in UI](../delete.md).

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes een dataflow gecreeerd om gegevens van een systeem van de marketingautomatisering in te brengen en inzicht verworven in de controle van datasets. Binnenkomende gegevens kunnen nu worden gebruikt door downstreamservices [!DNL Platform] zoals [!DNL Real-time Customer Profile] en [!DNL Data Science Workspace]. Raadpleeg de volgende documenten voor meer informatie:

- [[!DNL Real-time Customer Profile] overzicht](../../../../profile/home.md)
- [[!DNL Data Science Workspace] overzicht](../../../../data-science-workspace/home.md)

## Aanhangsel

De volgende secties verstrekken extra informatie voor het werken met bronschakelaars.

### Een gegevensstroom uitschakelen

Wanneer een gegevensstroom wordt gecreeerd, wordt het onmiddellijk actief en neemt gegevens volgens het programma op het werd gegeven. U kunt een actieve gegevensstroom op elk ogenblik onbruikbaar maken door de instructies hieronder te volgen.

Selecteer in het scherm **[!UICONTROL Dataflows]** de naam van de gegevensstroom die u wilt uitschakelen.

![browse-dataset-flow](../../../images/tutorials/dataflow/payments/view-dataset-flows.png)

De kolom **[!UICONTROL Properties]** wordt aan de rechterkant van het scherm weergegeven. Dit deelvenster bevat een schakelknop **[!UICONTROL Enabled]**. Klik op de schakeloptie om de gegevensstroom uit te schakelen. Dezelfde schakeloptie kan worden gebruikt om een gegevensstroom opnieuw in te schakelen nadat deze is uitgeschakeld.

![disable](../../../images/tutorials/dataflow/payments/disable.png)

### Binnenkomende gegevens voor [!DNL Profile] populatie activeren

De binnenkomende gegevens van uw bronschakelaar kunnen worden gebruikt om uw [!DNL Real-time Customer Profile] gegevens te verrijken en te vullen. Zie de zelfstudie over [Profielpopulatie](../profile.md) voor meer informatie over het vullen van uw [!DNL Real-time Customer Profile]-gegevens.
