---
keywords: Experience Platform;home;popular topics;database connector
solution: Experience Platform
title: Vorm een dataflow voor een gegevensbestandschakelaar in UI
topic: overview
description: Een dataflow is een geplande taak die gegevens van een bron aan een dataset van de Platform terugwint en opneemt. Deze zelfstudie bevat stappen om een nieuwe gegevensstroom te configureren met behulp van uw databaseaccount.
translation-type: tm+mt
source-git-commit: 63eb8407617cda64f3f3b0cefd6bf427314e0216
workflow-type: tm+mt
source-wordcount: '1445'
ht-degree: 0%

---


# Vorm een dataflow voor een gegevensbestandschakelaar in UI

Een dataflow is een geplande taak die gegevens van een bron aan een dataset van de Platform terugwint en opneemt. Deze zelfstudie bevat stappen om een nieuwe gegevensstroom te configureren met behulp van uw databaseaccount.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model] (XDM) Systeem](../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   - [Basisbeginselen van de schemacompositie](../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie](../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-time klantprofiel]](../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Bovendien is het voor deze zelfstudie nodig dat u al een databaseaccount hebt gemaakt. Een lijst van leerprogramma&#39;s voor het creëren van verschillende gegevensbestandschakelaars in UI kan in het overzicht [van](../../../home.md)bronschakelaars worden gevonden.

## Gegevens selecteren

Nadat u uw databaseaccount hebt gemaakt, wordt de stap Gegevens **** selecteren weergegeven en krijgt u een interactieve interface om de databasehiërarchie te verkennen.

- De linkerhelft van de interface is een browser die de lijst met databases van uw account weergeeft.
- Met de rechterhelft van de interface kunt u maximaal 100 rijen met gegevens voorvertonen.

Met de optie **[!UICONTROL Zoeken]** boven aan de pagina kunt u snel de brongegevens identificeren die u wilt gebruiken.

>[!NOTE]
>
>De optie van onderzoeksbrongegevens is beschikbaar aan alle op tabelvorm-gebaseerde bronschakelaars behalve de Analytics, Classifications, de Hubs van de Gebeurtenis, en de schakelaars van Kinesis.

Nadat u de brongegevens hebt gevonden, selecteert u de map en klikt u op **[!UICONTROL Volgende]**.

![select-data](../../../images/tutorials/dataflow/databases/select-data.png)


## Gegevensvelden toewijzen aan een XDM-schema

De stap *Toewijzing* verschijnt, die een interactieve interface verstrekt om de brongegevens aan een dataset van het Platform in kaart te brengen.

Kies een dataset voor binnenkomende gegevens waarin moeten worden opgenomen. U kunt of een bestaande dataset gebruiken of een nieuwe dataset tot stand brengen.

### Een bestaande gegevensset gebruiken

Om gegevens in een bestaande dataset in te voeren, selecteer **[!UICONTROL Bestaande dataset]**, dan klik het datasetpictogram.

![](../../../images/tutorials/dataflow/databases/existing-dataset.png)

Het dialoogvenster **[!UICONTROL Gegevensset]** selecteren wordt geopend. Zoek de gegevensset die u wilt gebruiken, selecteer deze en klik op **[!UICONTROL Doorgaan]**.

![](../../../images/tutorials/dataflow/databases/select-existing-dataset.png)

### Een nieuwe gegevensset gebruiken

Om gegevens in een nieuwe dataset in te voeren, selecteer **[!UICONTROL Nieuwe dataset]** en ga een naam en een beschrijving voor de dataset op de verstrekte gebieden in.

U kunt een schemagebied vastmaken door een schemanaam in te gaan in de **[!UICONTROL Uitgezochte bar van het schemaonderzoek]** . U kunt ook het vervolgkeuzepictogram selecteren om een lijst met bestaande schema&#39;s weer te geven. U kunt ook **[!UICONTROL Geavanceerd zoeken]** selecteren om toegang te krijgen tot het scherm met bestaande schema&#39;s en de bijbehorende details.

Tijdens deze stap, kunt u uw dataset voor toelaten [!DNL Real-time Customer Profile] en tot een holistische mening van de attributen en het gedrag van een entiteit leiden. De gegevens van alle toegelaten datasets zullen in worden omvat [!DNL Profile] en de veranderingen worden toegepast wanneer u uw gegevensstroom bewaart.

Schakel de knop Gegevensset **[!UICONTROL Profiel]** in of uit om uw doelgegevensset in te schakelen [!DNL Profile].

![create-new-dataset](../../../images/tutorials/dataflow/databases/new-dataset.png)

Het dialoogvenster Schema **** selecteren wordt geopend. Selecteer het schema u wenst om op de nieuwe dataset toe te passen, dan klik **[!UICONTROL Gedaan]**.

![](../../../images/tutorials/dataflow/databases/select-existing-schema.png)

Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of mapperfuncties te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Raadpleeg de zelfstudie over het [toewijzen van CSV-gegevens aan XDM-schemavelden](../../../../ingestion/tutorials/map-a-csv-file.md)voor meer informatie over gegevenstoewijzing en mapperfuncties.

>[!TIP]
>
>[!DNL Platform] verstrekt intelligente aanbevelingen voor auto-in kaart gebrachte gebieden die op het doelschema of de dataset worden gebaseerd dat u selecteerde. U kunt toewijzingsregels handmatig aanpassen aan uw gebruiksgevallen.

![](../../../images/tutorials/dataflow/all-tabular/mapping.png)

Selecteer Gegevens **[!UICONTROL van de]** Voorproef om afbeeldingsresultaten van maximaal 100 rijen steekproefgegevens van de geselecteerde dataset te zien.

Tijdens de voorvertoning krijgt de identiteitskolom de prioriteit als het eerste veld, omdat dit de belangrijkste informatie is die nodig is voor het valideren van toewijzingsresultaten.

![](../../../images/tutorials/dataflow/all-tabular/mapping-preview.png)

Als de brongegevens eenmaal zijn toegewezen, selecteert u **[!UICONTROL Sluiten]**.

## Planninguitvoering

De **[!UICONTROL Plannende]** stap verschijnt, toestaand u om een innameprogramma te vormen om de geselecteerde brongegevens automatisch in te nemen gebruikend de gevormde afbeeldingen. De volgende lijst schetst de verschillende configureerbare gebieden voor het plannen:

| Veld | Beschrijving |
| --- | --- |
| Frequentie | De selecteerbare frequenties omvatten `Once`, `Minute`, `Hour`, `Day`, en `Week`. |
| Interval | Een geheel getal dat het interval voor de geselecteerde frequentie instelt. |
| Begintijd | Een UTC-tijdstempel die aangeeft wanneer de eerste opname wordt uitgevoerd. |
| Achtergrond | Een booleaanse waarde die bepaalt welke gegevens eerst worden ingevoerd. Als **[!UICONTROL Backfill]** is ingeschakeld, worden alle huidige bestanden in het opgegeven pad tijdens de eerste geplande opname opgenomen. Als **[!UICONTROL Backfill]** is uitgeschakeld, worden alleen de bestanden opgenomen die tussen de eerste opname en de **[!UICONTROL begintijd]** worden geladen. Bestanden die vóór het begin van het **[!UICONTROL starten]** zijn geladen, worden niet opgenomen. |
| Delta-kolom | Een optie met een gefilterde reeks gebieden van het bronschema van type, datum, of tijd. Dit veld wordt gebruikt om onderscheid te maken tussen nieuwe en bestaande gegevens. Incrementele gegevens worden opgenomen op basis van het tijdstempel van de geselecteerde kolom. |

Dataflows worden ontworpen om gegevens automatisch in te voeren op een geplande basis. Begin door de innamefrequentie te selecteren. Daarna, plaats het interval om de periode tussen twee stroomlooppas aan te wijzen. De waarde van het interval moet een geheel getal zijn dat niet gelijk is aan nul en moet worden ingesteld op groter dan of gelijk aan 15.

Als u de begintijd voor inname wilt instellen, past u de datum en tijd aan die worden weergegeven in het vak Begintijd. U kunt ook het kalenderpictogram selecteren om de begintijdwaarde te bewerken. De begintijd moet groter zijn dan of gelijk zijn aan de huidige UTC-tijd.

Selecteer Incrementele gegevens **[!UICONTROL laden door]** de deltabkolom toe te wijzen. In dit veld wordt een onderscheid gemaakt tussen nieuwe en bestaande gegevens.

![](../../../images/tutorials/dataflow/databases/schedule-interval-on.png)

### Eenmalige gegevensstroom voor inname instellen

Als u eenmalige invoer wilt instellen, selecteert u de vervolgkeuzepijl voor de frequentie en selecteert u **[!UICONTROL Eenmaal]**.

>[!TIP]
>
>**[!UICONTROL Interval]** en **[!UICONTROL backfill]** zijn niet zichtbaar tijdens eenmalig gebruik.

Als u de juiste waarden voor het schema hebt opgegeven, selecteert u **[!UICONTROL Volgende]**.

![](../../../images/tutorials/dataflow/databases/schedule-once.png)

## Gegevens over gegevensstroom opgeven

De stap met **[!UICONTROL details]** over gegevensstroom wordt weergegeven, zodat u een naam kunt geven en een korte beschrijving kunt geven van uw nieuwe gegevensstroom.

Tijdens dit proces kunt u ook **[!UICONTROL gedeeltelijke inname]** en **[!UICONTROL foutdiagnose]** inschakelen. Als u **[!UICONTROL Gedeeltelijke inname]** inschakelt, kunt u gegevens met fouten tot een bepaalde drempel innemen. Wanneer **[!UICONTROL Partiële inname]** is ingeschakeld, sleept u de **[!UICONTROL foutdrempel %]** voor een wijziging van de foutdrempel van de batch. U kunt de drempelwaarde ook handmatig aanpassen door het invoervak te selecteren. Voor meer informatie, zie het [gedeeltelijke partijingestie overzicht](../../../../ingestion/batch-ingestion/partial.md).
Geef waarden op voor de gegevensstroom en selecteer **[!UICONTROL Volgende]**.

![](../../../images/tutorials/dataflow/databases/dataflow-detail.png)

## Controleer uw gegevensstroom

De stap **[!UICONTROL Revisie]** wordt weergegeven, zodat u de nieuwe gegevensstroom kunt controleren voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

- **[!UICONTROL Verbinding]**: Toont het brontype, de relevante weg van het gekozen brondossier, en de hoeveelheid kolommen binnen dat brondossier.
- **[!UICONTROL Gegevensset- en kaartvelden]** toewijzen: Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset zich aan houdt.
- **[!UICONTROL Planning]**: Toont de actieve periode, de frequentie, en het interval van het innameprogramma.

Nadat u de gegevensstroom hebt gereviseerd, klikt u op **[!UICONTROL Voltooien]** en laat u enige tijd over tot de gegevensstroom.

![](../../../images/tutorials/dataflow/databases/review.png)

## Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over innamepercentages, succes, en fouten te zien. Voor meer informatie over hoe te om dataflow te controleren, zie de zelfstudie over het [controleren van rekeningen en dataflows in UI](../monitor.md).

## Uw gegevensstroom verwijderen

U kunt gegevensstromen schrappen die niet meer noodzakelijk of verkeerd gecreeerd gebruikend de functie van de **[!UICONTROL Schrapping]** beschikbaar in de **[!UICONTROL werkruimte Dataflows]** zijn. Voor meer informatie over hoe te om dataflows te schrappen, zie de zelfstudie over het [schrappen van gegevensstromen in UI](../delete.md).

## Volgende stappen

Door dit leerprogramma te volgen, hebt u met succes een dataflow gecreeerd om gegevens van een extern gegevensbestand in te brengen en inzicht verworven op controledatasets. Inkomende gegevens kunnen nu worden gebruikt door downstreamdiensten [!DNL Platform] zoals [!DNL Real-time Customer Profile] en [!DNL Data Science Workspace]. Raadpleeg de volgende documenten voor meer informatie:

- [[!DNL Real-time Customer Profile] overzicht](../../../../profile/home.md)
- [[!DNL Data Science Workspace] overzicht](../../../../data-science-workspace/home.md)

## Aanhangsel

De volgende secties verstrekken extra informatie voor het werken met bronschakelaars.

### Een gegevensstroom uitschakelen

Wanneer een gegevensstroom wordt gecreeerd, wordt het onmiddellijk actief en neemt gegevens volgens het programma op het werd gegeven. U kunt een actieve gegevensstroom op elk ogenblik onbruikbaar maken door de instructies hieronder te volgen.

Binnen de **[!UICONTROL Bronwerkruimte]** , selecteer de **[!UICONTROL Dataflows]** tabel. Selecteer vervolgens de gegevensstroom die u wilt uitschakelen.

![](../../../images/tutorials/dataflow/databases/list-of-dataflows.png)

De kolom **[!UICONTROL Eigenschappen]** wordt aan de rechterkant van het scherm weergegeven, inclusief een knop **[!UICONTROL Ingeschakeld]** . Selecteer de schakeloptie om de gegevensstroom uit te schakelen. Dezelfde schakeloptie kan worden gebruikt om een gegevensstroom opnieuw in te schakelen nadat deze is uitgeschakeld.

![](../../../images/tutorials/dataflow/databases/disable.png)

### Binnenkomende gegevens voor [!DNL Profile] populatie activeren

De binnenkomende gegevens van uw bronschakelaar kunnen worden gebruikt om uw [!DNL Real-time Customer Profile] gegevens te verrijken en te bevolken. Zie de zelfstudie over de [!DNL Real-time Customer Profile] profielpopulatie [](../profile.md)voor meer informatie over het vullen van gegevens.