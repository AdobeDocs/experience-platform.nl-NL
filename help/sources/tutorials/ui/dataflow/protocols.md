---
keywords: Experience Platform;thuis;populaire onderwerpen;protocolaansluiting
solution: Experience Platform
title: Creeer een Dataflow Gebruikend een Bron van Protocollen in UI
topic-legacy: overview
type: Tutorial
description: Een dataflow is een geplande taak die gegevens van een bron aan een dataset van de Platform terugwint en opneemt. Dit leerprogramma verstrekt stappen op hoe te om een dataflow voor een protocolbron tot stand te brengen gebruikend Platform UI.
exl-id: 94631a78-14ea-41d7-876c-468634dfc6c1
source-git-commit: a9a443eda060606be4394dfc2e2707fe18618160
workflow-type: tm+mt
source-wordcount: '1344'
ht-degree: 0%

---

# Creeer een dataflow gebruikend een protocolbron in UI

Een dataflow is een geplande taak die gegevens van een bron aan een dataset in Adobe Experience Platform terugwint en opneemt. Dit leerprogramma verstrekt stappen op hoe te om een dataflow voor een protocolbron tot stand te brengen gebruikend het Platform UI.

>[!NOTE]
>
>Om een gegevensstroom tot stand te brengen, moet u reeds een voor authentiek verklaarde rekening met een protocolbron hebben. Een lijst van leerprogramma&#39;s voor het creëren van verschillende protocollen bronrekeningen in UI kan in worden gevonden [overzicht van bronnen](../../../home.md#protocols).

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Platform:

* [Bronnen](../../../home.md): Met Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met [!DNL Platform] diensten.
* [[!DNL Experience Data Model (XDM)] Systeem](../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema Editor](../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [[!DNL Data Prep]](../../../../data-prep/home.md): Staat gegevensingenieurs toe om, gegevens aan en van het Model van de Gegevens van de Ervaring in kaart te brengen om te zetten en te bevestigen (XDM).

## Gegevens toevoegen

Nadat u de bronaccount voor protocollen hebt gemaakt, **[!UICONTROL Add data]** stap verschijnt, verstrekkend een interface voor u om de de lijsthiërarchie van uw protocollen te onderzoeken bronrekening.

* De linkerhelft van de interface is een browser waarin een lijst met gegevenstabellen in uw account wordt weergegeven. De interface bevat ook een zoekoptie waarmee u snel de brongegevens kunt identificeren die u wilt gebruiken.
* De rechterhelft van de interface is een voorvertoningsvenster waarin u maximaal 100 rijen gegevens kunt voorvertonen.

>[!NOTE]
>
>De zoekbrongegevensoptie is beschikbaar voor alle op tabellen gebaseerde bronnen, met uitzondering van de Adobe Analytics, [!DNL Amazon Kinesis], en [!DNL Azure Event Hubs].

Wanneer u de brongegevens hebt gevonden, selecteert u de tabel en selecteert u vervolgens **[!UICONTROL Next]**.

![select-data](../../../images/tutorials/dataflow/table-based/select-data.png)

## Gegevens over gegevensstroom opgeven

De [!UICONTROL Dataflow detail] De pagina staat u toe om te selecteren of u een bestaande dataset of een nieuwe dataset wilt gebruiken. Tijdens dit proces kunt u ook instellingen configureren voor [!UICONTROL Profile dataset], [!UICONTROL Error diagnostics], [!UICONTROL Partial ingestion], en [!UICONTROL Alerts].

![dataFlow-detail](../../../images/tutorials/dataflow/table-based/dataflow-detail.png)

### Een bestaande gegevensset gebruiken

Om gegevens in een bestaande dataset in te voeren, selecteer **[!UICONTROL Existing dataset]**. U kunt of een bestaande dataset terugwinnen gebruikend [!UICONTROL Advanced search] of door door de lijst van bestaande datasets in het dropdown menu te scrollen. Zodra u een dataset hebt geselecteerd, verstrek een naam en een beschrijving voor uw gegevensstroom.

![bestaande gegevensset](../../../images/tutorials/dataflow/table-based/existing-dataset.png)

### Een nieuwe gegevensset gebruiken

Om in een nieuwe dataset in te gaan, selecteer **[!UICONTROL New dataset]** en geef vervolgens een naam voor de uitvoergegevensset en een optionele beschrijving op. Selecteer vervolgens het schema waaraan u wilt toewijzen [!UICONTROL Advanced search] of door door de lijst van bestaande schema&#39;s in het dropdown menu te scrollen. Nadat u een schema hebt geselecteerd, geeft u een naam en een beschrijving voor de gegevensstroom op.

![new-dataset](../../../images/tutorials/dataflow/table-based/new-dataset.png)

### Inschakelen [!DNL Profile] en foutdiagnostiek

Selecteer vervolgens de **[!UICONTROL Profile dataset]** schakelen om uw gegevensset in te schakelen voor [!DNL Profile]. Hierdoor kunt u een holistische weergave maken van de kenmerken en het gedrag van een entiteit. Gegevens van alle [!DNL Profile]- de toegelaten datasets zullen in worden omvat [!DNL Profile] en wijzigingen worden toegepast wanneer u de gegevensstroom opslaat.

[!UICONTROL Error diagnostics] laat gedetailleerde foutenmelding generatie voor om het even welke onjuiste verslagen toe die in uw dataflow voorkomen, terwijl [!UICONTROL Partial ingestion] kunt u gegevens met fouten opnemen tot een bepaalde drempel die u handmatig definieert. Zie de [gedeeltelijke batch-opname, overzicht](../../../../ingestion/batch-ingestion/partial.md) voor meer informatie .

![met profiel en fouten](../../../images/tutorials/dataflow/table-based/profile-and-errors.png)

### Waarschuwingen inschakelen

U kunt waarschuwingen inschakelen om meldingen te ontvangen over de status van uw gegevensstroom. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over waarschuwingen raadpleegt u de handleiding over [abonneren op berichten voor bronnen met behulp van de gebruikersinterface](../alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw gegevensstroom, selecteert u **[!UICONTROL Next]**.

![waarschuwingen](../../../images/tutorials/dataflow/table-based/alerts.png)

## Gegevensvelden toewijzen aan een XDM-schema

De [!UICONTROL Mapping] de stap verschijnt, die u van een interface voorziet om de brongebieden van uw bronschema aan hun aangewezen doelXDM gebieden in het doelschema in kaart te brengen.

Platform biedt intelligente aanbevelingen voor automatisch toegewezen velden op basis van het doelschema of de gegevensset die u hebt geselecteerd. U kunt toewijzingsregels handmatig aanpassen aan uw gebruiksgevallen. Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of gegevens prep-functies te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Voor uitvoerige stappen bij het gebruiken van de kaartperinterface en berekende gebieden, zie [UI-hulplijn voor gegevensvoorinstelling](../../../../data-prep/ui/mapping.md).

Als de brongegevens eenmaal zijn toegewezen, selecteert u **[!UICONTROL Next]**.

![toewijzing](../../../images/tutorials/dataflow/table-based/mapping.png)

## Planninguitvoering

De [!UICONTROL Scheduling] de stap verschijnt, toestaand u om een innameprogramma te vormen om de geselecteerde brongegevens automatisch in te nemen gebruikend de gevormde afbeeldingen. Standaard is de planning ingesteld op `Once`. Selecteer **[!UICONTROL Frequency]** en selecteert u vervolgens een optie in het vervolgkeuzemenu.

>[!TIP]
>
>Interval en backfill zijn niet zichtbaar tijdens een eenmalige opname.

![plannen](../../../images/tutorials/dataflow/table-based/scheduling.png)

Als u de innamefrequentie instelt op `Minute`, `Hour`, `Day`, of `Week`dan moet u een interval instellen om een bepaald tijdkader tussen elke opname te bepalen. Bijvoorbeeld een innamefrequentie ingesteld op `Day` en een interval instellen op `15` betekent dat uw gegevensstroom gepland is om gegevens in te voeren om de 15 dagen.

Tijdens deze stap kunt u ook **backfill** en definieert u een kolom voor de incrementele opname van gegevens. Backfill wordt gebruikt om historische gegevens in te voeren, terwijl in de kolom die u voor incrementele inname definieert, nieuwe gegevens kunnen worden onderscheiden van bestaande gegevens.

Zie de lijst hieronder voor meer informatie over het plannen van configuraties.

| Veld | Beschrijving |
| --- | --- |
| Frequentie | De frequentie waarin inname plaatsvindt. Selecteerbare frequenties omvatten `Once`, `Minute`, `Hour`, `Day`, en `Week`. |
| Interval | Een geheel getal dat het interval voor de geselecteerde frequentie instelt. De waarde van het interval moet een geheel getal zijn dat niet gelijk is aan nul en moet worden ingesteld op groter dan of gelijk aan 15. |
| Begintijd | Een UTC-tijdstempel die aangeeft wanneer de eerste opname wordt uitgevoerd. De begintijd moet groter zijn dan of gelijk zijn aan de huidige UTC-tijd. |
| Achtergrond | Een booleaanse waarde die bepaalt welke gegevens eerst worden ingevoerd. Als backfill is ingeschakeld, worden alle huidige bestanden in het opgegeven pad tijdens de eerste geplande inname opgenomen. Als terugvullen is uitgeschakeld, worden alleen de bestanden opgenomen die tussen de eerste opname en de begintijd worden geladen. Bestanden die vóór de begintijd zijn geladen, worden niet opgenomen. |
| Incrementele gegevens laden met | Een optie met een gefilterde reeks gebieden van het bronschema van type, datum, of tijd. Dit veld wordt gebruikt om onderscheid te maken tussen nieuwe en bestaande gegevens. Incrementele gegevens worden opgenomen op basis van het tijdstempel van de geselecteerde kolom. |

![backfill](../../../images/tutorials/dataflow/table-based/backfill.png)

## Controleer uw gegevensstroom

De **[!UICONTROL Review]** wordt weergegeven, zodat u de nieuwe gegevensstroom kunt controleren voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: Toont het brontype, de relevante weg van het gekozen brondossier, en de hoeveelheid kolommen binnen dat brondossier.
* **[!UICONTROL Assign dataset & map fields]**: Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset zich aan houdt.
* **[!UICONTROL Scheduling]**: Toont de actieve periode, de frequentie, en het interval van het innameprogramma.

Nadat u de gegevensstroom hebt gecontroleerd, selecteert u **[!UICONTROL Finish]** en laat enige tijd voor de gegevensstroom worden gecreeerd.

![revisie](../../../images/tutorials/dataflow/table-based/review.png)

## Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over innamepercentages, succes, en fouten te zien. Voor meer informatie over hoe te om dataflow te controleren, zie de zelfstudie op [het controleren van rekeningen en gegevensstromen in UI](../monitor.md).

## Uw gegevensstroom verwijderen

U kunt gegevensstromen schrappen die niet meer noodzakelijk of verkeerd gecreeerd gebruikend zijn **[!UICONTROL Delete]** functie beschikbaar in de **[!UICONTROL Dataflows]** werkruimte. Raadpleeg de zelfstudie voor meer informatie over het verwijderen van gegevensstromen [verwijderen, gegevensstromen in de gebruikersinterface](../delete.md).

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes een dataflow gecreeerd om gegevens van uw protocolbron aan Platform te brengen. Binnenkomende gegevens kunnen nu door downstreamgebruikers worden gebruikt [!DNL Platform] diensten zoals [!DNL Real-time Customer Profile] en [!DNL Data Science Workspace]. Raadpleeg de volgende documenten voor meer informatie:

* [[!DNL Real-time Customer Profile] - overzicht](../../../../profile/home.md)
* [[!DNL Data Science Workspace] - overzicht](../../../../data-science-workspace/home.md)


>[!WARNING]
>
> De interface van het Platform die in de volgende video wordt getoond is verouderd. Raadpleeg de bovenstaande documentatie voor de meest recente schermafbeeldingen en functionaliteit van de gebruikersinterface.
>
>[!VIDEO](https://video.tv.adobe.com/v/29711?quality=12&learn=on)