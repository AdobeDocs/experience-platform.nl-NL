---
keywords: Experience Platform;thuis;populaire onderwerpen;protocolaansluiting
solution: Experience Platform
title: Vorm een Dataflow voor een Verbinding van de Bron van het Protocol in UI
topic-legacy: overview
type: Tutorial
description: Een dataflow is een geplande taak die gegevens van een bron aan een dataset van Adobe Experience Platform terugwint en opneemt. Dit leerprogramma verstrekt stappen om een nieuwe dataflow te vormen gebruikend uw protocolrekening.
exl-id: 94631a78-14ea-41d7-876c-468634dfc6c1
source-git-commit: 38f64f2ba0b40a20528aac6efff0e2fd6bc12ed2
workflow-type: tm+mt
source-wordcount: '1398'
ht-degree: 0%

---

# Een gegevensstroom configureren voor een protocolverbinding in de gebruikersinterface

Een dataflow is een geplande taak die gegevens van een bron aan een dataset van Adobe Experience Platform terugwint en opneemt. Dit leerprogramma verstrekt stappen om een nieuwe dataflow te vormen gebruikend uw protocolrekening.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Systeem](../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   - [Basisbeginselen van de schemacompositie](../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie Schema Editor](../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-time Customer Profile]](../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Bovendien, vereist dit leerprogramma dat u reeds een protocolrekening hebt gecreeerd. Een lijst van leerprogramma&#39;s voor het creëren van verschillende protocolschakelaars in UI kan in worden gevonden [overzicht van bronconnectors](../../../home.md).

## Gegevens selecteren

Nadat u uw protocolaccount hebt gemaakt, kunt u **[!UICONTROL Select data]** wordt weergegeven met een interactieve interface waarmee u de bestandshiërarchie kunt verkennen.

- De linkerhelft van de interface is een directorybrowser waarin de bestanden en mappen van uw server worden weergegeven.
- Met de rechterhelft van de interface kunt u maximaal 100 rijen gegevens uit een compatibel bestand voorvertonen.

U kunt de **[!UICONTROL Search]** boven aan de pagina om snel de brongegevens te identificeren die u wilt gebruiken.

>[!NOTE]
>
>De optie van onderzoeksbrongegevens is beschikbaar aan alle op tabelvorm-gebaseerde bronschakelaars behalve de Analytics, Classifications, de Hubs van de Gebeurtenis, en de schakelaars van Kinesis.

Als u de brongegevens hebt gevonden, selecteert u de map en klikt u op **[!UICONTROL Next]**.

![select-data](../../../images/tutorials/dataflow/all-tabular/select-data.png)

## Gegevensvelden toewijzen aan een XDM-schema

De **[!UICONTROL Mapping]** stap wordt weergegeven en biedt een interactieve interface voor het toewijzen van de brongegevens aan een [!DNL Platform] dataset.

Kies een dataset voor binnenkomende gegevens waarin moeten worden opgenomen. U kunt of een bestaande dataset gebruiken of een nieuwe dataset tot stand brengen.

### Een bestaande gegevensset gebruiken

Om gegevens in een bestaande dataset in te voeren, selecteer **[!UICONTROL Use existing dataset]** klikt u op het pictogram van de gegevensset.

![use-existing-dataset](../../../images/tutorials/dataflow/protocols/use-existing-dataset.png)

De **[!UICONTROL Select dataset]** wordt weergegeven. Zoek de dataset u wenst te gebruiken, het te selecteren, dan klik **[!UICONTROL Continue]**.

![select-existing-dataset](../../../images/tutorials/dataflow/protocols/select-existing-dataset.png)

### Een nieuwe gegevensset gebruiken

Om gegevens in een nieuwe dataset in te voeren, selecteer **[!UICONTROL Create new dataset]** en voert een naam en een beschrijving voor de gegevensset in de opgegeven velden in.

U kunt een schemagebied vastmaken door een schemanaam in te gaan in **[!UICONTROL Select schema]** zoekbalk. U kunt ook het vervolgkeuzepictogram selecteren om een lijst met bestaande schema&#39;s weer te geven. U kunt ook **[!UICONTROL Advanced search]** toegang tot het scherm van bestaande schema&#39;s, met inbegrip van hun respectieve details.

Tijdens deze stap, kunt u uw dataset voor toelaten [!DNL Real-time Customer Profile] en een holistische weergave te maken van de kenmerken en gedragingen van een entiteit. Gegevens van alle ingeschakelde gegevenssets worden opgenomen in [!DNL Profile] en wijzigingen worden toegepast wanneer u de gegevensstroom opslaat.

Schakelen tussen **[!UICONTROL Profile dataset]** knoop om uw doeldataset voor toe te laten [!DNL Profile].

![create-new-dataset](../../../images/tutorials/dataflow/protocols/new-dataset.png)

De **[!UICONTROL Select schema]** wordt weergegeven. Selecteer het schema u op de nieuwe dataset wenst toe te passen, dan klik **[!UICONTROL Done]**.

![selectieschema](../../../images/tutorials/dataflow/protocols/select-existing-schema.png)

Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of gegevens prep-functies te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Voor uitvoerige stappen bij het gebruiken van de kaartperinterface en berekende gebieden, zie [UI-hulplijn voor gegevensvoorinstelling](../../../../data-prep/ui/mapping.md).

>[!TIP]
>
>Platform biedt intelligente aanbevelingen voor automatisch toegewezen velden op basis van het doelschema of de gegevensset die u hebt geselecteerd. U kunt toewijzingsregels handmatig aanpassen aan uw gebruiksgevallen.

![](../../../images/tutorials/dataflow/all-tabular/mapping.png)

Selecteren **[!UICONTROL Preview data]** om afbeeldingsresultaten van maximaal 100 rijen steekproefgegevens van de geselecteerde dataset te zien.

Tijdens de voorvertoning krijgt de identiteitskolom de prioriteit als het eerste veld, omdat dit de belangrijkste informatie is die nodig is voor het valideren van toewijzingsresultaten.

![](../../../images/tutorials/dataflow/all-tabular/mapping-preview.png)

Selecteer **[!UICONTROL Close]**.

## Planninguitvoering

De **[!UICONTROL Scheduling]** de stap verschijnt, toestaand u om een innameprogramma te vormen om de geselecteerde brongegevens automatisch in te nemen gebruikend de gevormde afbeeldingen. De volgende lijst schetst de verschillende configureerbare gebieden voor het plannen:

| Veld | Beschrijving |
| --- | --- |
| Frequentie | Selecteerbare frequenties omvatten `Once`, `Minute`, `Hour`, `Day`, en `Week`. |
| Interval | Een geheel getal dat het interval voor de geselecteerde frequentie instelt. |
| Begintijd | Een UTC-tijdstempel die aangeeft wanneer de eerste opname wordt uitgevoerd. |
| Achtergrond | Een booleaanse waarde die bepaalt welke gegevens eerst worden ingevoerd. Indien **[!UICONTROL Backfill]** is ingeschakeld, worden alle huidige bestanden in het opgegeven pad tijdens de eerste geplande opname opgenomen. Indien **[!UICONTROL Backfill]** is uitgeschakeld, worden alleen de bestanden opgenomen die tussen de eerste opname en de begintijd worden geladen. Bestanden die vóór de begintijd zijn geladen, worden niet opgenomen. |
| Delta-kolom | Een optie met een gefilterde reeks gebieden van het bronschema van type, datum, of tijd. Dit veld wordt gebruikt om onderscheid te maken tussen nieuwe en bestaande gegevens. Incrementele gegevens worden opgenomen op basis van het tijdstempel van de geselecteerde kolom. |

Dataflows worden ontworpen om gegevens automatisch in te voeren op een geplande basis. Begin door de innamefrequentie te selecteren. Daarna, plaats het interval om de periode tussen twee stroomlooppas aan te wijzen. De waarde van het interval moet een geheel getal zijn dat niet gelijk is aan nul en moet worden ingesteld op groter dan of gelijk aan 15.

Als u de begintijd voor inname wilt instellen, past u de datum en tijd aan die worden weergegeven in het vak Begintijd. U kunt ook het kalenderpictogram selecteren om de begintijdwaarde te bewerken. De begintijd moet groter zijn dan of gelijk zijn aan de huidige UTC-tijd.

Selecteren **[!UICONTROL Load incremental data by]** om de deltakolom toe te wijzen. In dit veld wordt een onderscheid gemaakt tussen nieuwe en bestaande gegevens.

![](../../../images/tutorials/dataflow/databases/schedule-interval-on.png)

### Eenmalige gegevensstroom voor inname instellen

Als u eenmalige invoer wilt instellen, selecteert u de pijl-omlaag voor de frequentie en selecteert u **[!UICONTROL Once]**.

>[!TIP]
>
>**[!UICONTROL Interval]** en **[!UICONTROL Backfill]** niet zichtbaar zijn tijdens eenmalig gebruik.

Als u de juiste waarden voor het schema hebt opgegeven, selecteert u **[!UICONTROL Next]**.

![](../../../images/tutorials/dataflow/databases/schedule-once.png)

## Gegevens over gegevensstroom opgeven

De **[!UICONTROL Dataflow detail]** wordt weergegeven, zodat u een naam kunt geven en een korte beschrijving kunt geven van uw nieuwe gegevensstroom.

Tijdens dit proces kunt u ook **[!UICONTROL Partial ingestion]** en **[!UICONTROL Error diagnostics]**. Inschakelen **[!UICONTROL Partial ingestion]** biedt de mogelijkheid om gegevens met fouten tot een bepaalde drempel in te voeren. Eenmaal **[!UICONTROL Partial ingestion]** is ingeschakeld, versleept u de **[!UICONTROL Error threshold %]** wijzerplaat om de foutendrempel van de partij aan te passen. U kunt de drempelwaarde ook handmatig aanpassen door het invoervak te selecteren. Zie voor meer informatie de [gedeeltelijke batch-opname, overzicht](../../../../ingestion/batch-ingestion/partial.md).

Geef waarden op voor de gegevensstroom en selecteer **[!UICONTROL Next]**.

![details gegevensstroom](../../../images/tutorials/dataflow/all-tabular/dataflow-detail.png)

## Controleer uw gegevensstroom

De **[!UICONTROL Review]** wordt weergegeven, zodat u de nieuwe gegevensstroom kunt controleren voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

- **[!UICONTROL Connection]**: Toont het brontype, de relevante weg van het gekozen brondossier, en de hoeveelheid kolommen binnen dat brondossier.
- **[!UICONTROL Assign dataset & map fields]**: Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset zich aan houdt.
- **[!UICONTROL Scheduling]**: Toont de actieve periode, de frequentie, en het interval van het innameprogramma.

Nadat u de gegevensstroom hebt gecontroleerd, klikt u op **[!UICONTROL Finish]** en laat enige tijd voor de gegevensstroom worden gecreeerd.

![revisie](../../../images/tutorials/dataflow/protocols/review.png)

## Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over innamepercentages, succes, en fouten te zien. Voor meer informatie over hoe te om dataflow te controleren, zie de zelfstudie op [het controleren van rekeningen en gegevensstromen in UI](../monitor.md).

## Uw gegevensstroom verwijderen

U kunt gegevensstromen schrappen die niet meer noodzakelijk of verkeerd gecreeerd gebruikend zijn **[!UICONTROL Delete]** functie beschikbaar in de **[!UICONTROL Dataflows]** werkruimte. Raadpleeg de zelfstudie voor meer informatie over het verwijderen van gegevensstromen [verwijderen, gegevensstromen in de gebruikersinterface](../delete.md).

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes een dataflow gecreeerd om gegevens van een systeem van de marketingautomatisering in te brengen en inzicht verworven in de controle van datasets. Binnenkomende gegevens kunnen nu door downstreamgebruikers worden gebruikt [!DNL Platform] diensten zoals [!DNL Real-time Customer Profile] en [!DNL Data Science Workspace]. Raadpleeg de volgende documenten voor meer informatie:

- [[!DNL Real-time Customer Profile] - overzicht](../../../../profile/home.md)
- [[!DNL Data Science Workspace] - overzicht](../../../../data-science-workspace/home.md)

## Aanhangsel

De volgende secties verstrekken extra informatie voor het werken met bronschakelaars.

### Een gegevensstroom uitschakelen

Wanneer een gegevensstroom wordt gecreeerd, wordt het onmiddellijk actief en neemt gegevens volgens het programma op het werd gegeven. U kunt een actieve gegevensstroom op elk ogenblik onbruikbaar maken door de instructies hieronder te volgen.

Binnen de **[!UICONTROL Dataflows]** selecteert u de naam van de gegevensstroom die u wilt uitschakelen.

![browse-dataset-flow](../../../images/tutorials/dataflow/protocols/view-dataset-flows.png)

De **[!UICONTROL Properties]** wordt aan de rechterkant van het scherm weergegeven. Dit deelvenster bevat een **[!UICONTROL Enabled]** schakelknop. Klik op de schakeloptie om de gegevensstroom uit te schakelen. Dezelfde schakeloptie kan worden gebruikt om een gegevensstroom opnieuw in te schakelen nadat deze is uitgeschakeld.

![disable](../../../images/tutorials/dataflow/protocols/disable.png)

### Inkomende gegevens activeren voor [!DNL Profile] bevolking

De binnenkomende gegevens van uw bronschakelaar kunnen aan het verrijken en het bevolken van uw [!DNL Real-time Customer Profile] gegevens. Voor meer informatie over het vullen van uw [!DNL Real-time Customer Profile] gegevens, raadpleeg de zelfstudie over [Profielpopulatie](../profile.md).
