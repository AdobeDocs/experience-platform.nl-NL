---
keywords: Experience Platform;home;populaire onderwerpen;crm-schema;crm;CRM;dataflow;DataFlow
solution: Experience Platform
title: Vorm een Dataflow voor een BronCRM Verbinding in UI
topic-legacy: overview
type: Tutorial
description: Een dataflow is een geplande taak die gegevens van een bron aan een dataset van de Platform terugwint en opneemt. Deze zelfstudie biedt stappen om een nieuwe gegevensstroom te configureren met behulp van uw CRM-account.
exl-id: e14eafa7-6594-48e6-ab7a-f6c928d1e5fb
source-git-commit: cd9b28c66f6cc841e46e797b39db838a83e727e3
workflow-type: tm+mt
source-wordcount: '1323'
ht-degree: 0%

---

# Een gegevensstroom configureren voor een CRM-verbinding in de gebruikersinterface

Een dataflow is een geplande taak die gegevens van een bron aan een dataset van de Platform terugwint en opneemt. Deze zelfstudie biedt stappen om een nieuwe gegevensstroom te configureren met behulp van uw CRM-account.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Experience Platform] klantenervaring worden georganiseerd.
   * [Basisbeginselen van de schemacompositie](../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../xdm/tutorials/create-schema-ui.md) Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Bovendien, vereist dit leerprogramma dat u reeds een rekening van CRM hebt gecreeerd. Een lijst van leerprogramma&#39;s voor het creëren van verschillende schakelaars van CRM in UI kan in [overzicht van bronschakelaars](../../../home.md) worden gevonden.

## Gegevens selecteren

Nadat u uw CRM-account hebt gemaakt, wordt de stap [!UICONTROL Select data] weergegeven en krijgt u een interface om de bestandshiërarchie te verkennen.

* De linkerhelft van de interface is een folderbrowser, die de dossiers en de folders van uw CRM toont.
* Met de rechterhelft van de interface kunt u maximaal 100 rijen gegevens uit een compatibel bestand voorvertonen.

Met de optie **[!UICONTROL Search]** boven aan de pagina kunt u snel de brongegevens identificeren die u wilt gebruiken.

>[!NOTE]
>
>De optie van onderzoeksbrongegevens is beschikbaar aan alle op tabelvorm-gebaseerde bronschakelaars behalve de Analytics, Classifications, de Hubs van de Gebeurtenis, en de schakelaars van Kinesis.

Wanneer u de brongegevens hebt gevonden, selecteert u de map en selecteert u **[!UICONTROL Next]**.

![select-data](../../../images/tutorials/dataflow/all-tabular/select-data.png)

## Gegevensvelden toewijzen aan een XDM-schema

De stap **[!UICONTROL Mapping]** verschijnt, die een interface verstrekken om de brongegevens aan een dataset van het Platform in kaart te brengen.

Kies een dataset voor binnenkomende gegevens waarin moeten worden opgenomen. U kunt of een bestaande dataset gebruiken of een nieuwe dataset tot stand brengen.

### Een bestaande gegevensset gebruiken

Als u gegevens in een bestaande gegevensset wilt invoegen, selecteert u **[!UICONTROL Existing dataset]** en selecteert u vervolgens het gegevenspictogram ![data](../../../images/tutorials/dataflow/crm/data.png) naast de invoerbalk.

![bestaande gegevensset](../../../images/tutorials/dataflow/crm/existing-dataset.png)

Het dialoogvenster **[!UICONTROL Select dataset]** wordt weergegeven. Zoek de dataset u wenst te gebruiken, het te selecteren, dan **[!UICONTROL Continue]** te klikken.

![select-dataset](../../../images/tutorials/dataflow/crm/select-dataset.png)

### Een nieuwe gegevensset gebruiken

Om gegevens in een nieuwe dataset in te voeren, selecteer **[!UICONTROL New dataset]** en ga een naam en een beschrijving voor de dataset op de verstrekte gebieden in.

U kunt een schemagebied vastmaken door een schemanaam in **[!UICONTROL Select schema]** onderzoeksbar in te gaan. U kunt ook het vervolgkeuzepictogram selecteren om een lijst met bestaande schema&#39;s weer te geven. U kunt ook **[!UICONTROL Advanced search]** selecteren om toegang te krijgen tot het scherm van bestaande schema&#39;s met hun respectievelijke details.

Tijdens deze stap, kunt u uw dataset voor [!DNL Real-time Customer Profile] toelaten en een holistische mening van de attributen en het gedrag van een entiteit creëren. De gegevens van alle toegelaten datasets zullen in [!DNL Profile] worden omvat en de veranderingen worden toegepast wanneer u uw gegevensstroom bewaart.

Schakel de knop **[!UICONTROL Profile dataset]** in of uit om uw doelgegevensset in te schakelen voor [!DNL Profile].

![create-new-dataset](../../../images/tutorials/dataflow/crm/new-dataset.png)

Het dialoogvenster **[!UICONTROL Select schema]** wordt weergegeven. Selecteer het schema u wenst om op de nieuwe dataset toe te passen, dan klik **[!UICONTROL Done]**.

![selectieschema](../../../images/tutorials/dataflow/crm/select-schema.png)

Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of gegevens prep-functies te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Voor meer informatie over mapperfuncties en berekende velden raadpleegt u de [handleiding voor gegevenprepfuncties](../../../../data-prep/functions.md) of de [handleiding voor berekende velden](../../../../data-prep/calculated-fields.md).

<!--
>[!TIP]
>
>If you are using the [!DNL Salesforce] source as part of B2B CDP, refer to the [[!DNL Salesforce] field mapping tables](../../../connectors/adobe-applications/mapping/salesforce.md) for a guide on the appropriate mapping sets between [!DNL Salesforce] source fields and XDM target fields.
-->

Platform biedt intelligente aanbevelingen voor automatisch toegewezen velden op basis van het doelschema of de gegevensset die u hebt geselecteerd. U kunt toewijzingsregels handmatig aanpassen aan uw gebruiksgevallen.

Selecteer **[!UICONTROL Preview data]** om toewijzingsresultaten van maximaal 100 rijen steekproefgegevens van de geselecteerde dataset te zien.

![](../../../images/tutorials/dataflow/crm/preview-data.png)

Tijdens de voorvertoning krijgt de identiteitskolom de prioriteit als het eerste veld, omdat dit de belangrijkste informatie is die nodig is voor het valideren van toewijzingsresultaten.

Selecteer **[!UICONTROL Close]** als de brongegevens zijn toegewezen.

![](../../../images/tutorials/dataflow/crm/preview.png)

Selecteer vervolgens **[!UICONTROL Next]** in het scherm [!UICONTROL Mapping] om door te gaan.

![](../../../images/tutorials/dataflow/crm/mapping.png)

## Planninguitvoering

De stap **[!UICONTROL Scheduling]** verschijnt, toestaand u om een insluitingsprogramma te vormen om de geselecteerde brongegevens automatisch in te nemen gebruikend de gevormde afbeeldingen. De volgende lijst schetst de verschillende configureerbare gebieden voor het plannen:

| Veld | Beschrijving |
| --- | --- |
| Frequentie | Selecteerbare frequenties zijn onder andere `Once`, `Minute`, `Hour`, `Day` en `Week`. |
| Interval | Een geheel getal dat het interval voor de geselecteerde frequentie instelt. |
| Begintijd | Een UTC-tijdstempel die aangeeft wanneer de eerste opname wordt uitgevoerd. |
| Achtergrond | Een booleaanse waarde die bepaalt welke gegevens eerst worden ingevoerd. Als **[!UICONTROL Backfill]** wordt toegelaten, zullen alle huidige dossiers in de gespecificeerde weg tijdens de eerste geplande opname worden opgenomen. Als **[!UICONTROL Backfill]** is uitgeschakeld, worden alleen de bestanden opgenomen die tussen de eerste opname en **[!UICONTROL Start time]** worden geladen. Bestanden die vóór **[!UICONTROL Start time]** zijn geladen, worden niet opgenomen. |
| Delta-kolom | Een optie met een gefilterde reeks gebieden van het bronschema van type, datum, of tijd. Dit veld wordt gebruikt om onderscheid te maken tussen nieuwe en bestaande gegevens. Incrementele gegevens worden opgenomen op basis van het tijdstempel van de geselecteerde kolom. |

Dataflows worden ontworpen om gegevens automatisch in te voeren op een geplande basis. Begin door de innamefrequentie te selecteren. Daarna, plaats het interval om de periode tussen twee stroomlooppas aan te wijzen. De waarde van het interval moet een geheel getal zijn dat niet gelijk is aan nul en moet worden ingesteld op groter dan of gelijk aan 15.

Als u de begintijd voor inname wilt instellen, past u de datum en tijd aan die worden weergegeven in het vak Begintijd. U kunt ook het kalenderpictogram selecteren om de begintijdwaarde te bewerken. De begintijd moet groter zijn dan of gelijk zijn aan de huidige UTC-tijd.

Selecteer **[!UICONTROL Load incremental data by]** om de deltakolom toe te wijzen. In dit veld wordt een onderscheid gemaakt tussen nieuwe en bestaande gegevens.

![](../../../images/tutorials/dataflow/crm/scheduling.png)

### Eenmalige gegevensstroom voor inname instellen

Als u eenmalige invoer wilt instellen, selecteert u de pijl voor de frequentieverlaging en selecteert u **[!UICONTROL Once]**.

>[!TIP]
>
>**[!UICONTROL Interval]** en niet zichtbaar  **[!UICONTROL Backfill]** zijn tijdens eenmalig gebruik.

Als u de juiste waarden voor het schema hebt opgegeven, selecteert u **[!UICONTROL Next]**.

![schema-eens](../../../images/tutorials/dataflow/crm/one-time-ingestion.png)

## Gegevens over gegevensstroom opgeven

De stap **[!UICONTROL Dataflow detail]** wordt weergegeven, zodat u een naam kunt geven en een korte beschrijving kunt geven van uw nieuwe gegevensstroom.

Tijdens dit proces kunt u **[!UICONTROL Partial ingestion]** en **[!UICONTROL Error diagnostics]** ook inschakelen. Als u **[!UICONTROL Partial ingestion]** inschakelt, kunt u gegevens met fouten tot een bepaalde drempel invoeren. Wanneer **[!UICONTROL Partial ingestion]** is ingeschakeld, sleept u de **[!UICONTROL Error threshold %]**-schijf om de foutdrempel van de batch aan te passen. U kunt de drempelwaarde ook handmatig aanpassen door het invoervak te selecteren. Voor meer informatie, zie [gedeeltelijk partijingesinzicht overzicht](../../../../ingestion/batch-ingestion/partial.md).

Geef waarden op voor de gegevensstroom en selecteer **[!UICONTROL Next]**.

![details gegevensstroom](../../../images/tutorials/dataflow/crm/dataflow-detail.png)

## Controleer uw gegevensstroom

De stap *Review* verschijnt, die u toestaat om uw nieuwe gegevensstroom te herzien alvorens het wordt gecreeerd. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: Hiermee geeft u de naam van de bronaccount, het bronplatform, het relevante pad van het gekozen bronbestand en de hoeveelheid kolommen in dat bronbestand weer.
* **[!UICONTROL Assign dataset and map fields]**: Toont de doeldataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset volgt aan.
* **[!UICONTROL Scheduling]**: Geeft de begintijd en frequentie van de gegevensstroom weer.

Zodra u uw gegevensstroom hebt herzien, klik **[!UICONTROL Finish]** en laat wat tijd voor dataflow om worden gecreeerd.

![revisie](../../../images/tutorials/dataflow/crm/review.png)

## Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over innamepercentages, succes, en fouten te zien. Voor meer informatie over hoe te om dataflow te controleren, zie de zelfstudie over [het controleren van rekeningen en dataflows in UI](../monitor.md).

## Uw gegevensstroom verwijderen

U kunt gegevensstromen schrappen die niet meer noodzakelijk of verkeerd gecreeerd gebruikend de functie **[!UICONTROL Delete]** beschikbaar in de **[!UICONTROL Dataflows]** werkruimte zijn. Voor meer informatie over hoe te om dataflows te schrappen, zie de zelfstudie over [het schrappen van gegevensstromen in UI](../delete.md).

## Volgende stappen

Door dit leerprogramma te volgen, hebt u met succes een dataflow gecreeerd om gegevens van CRM in te brengen en inzicht verworven in de controles van datasets. Als u meer wilt weten over het maken van gegevensstromen, kunt u uw studie aanvullen door de onderstaande video te bekijken. Bovendien kunnen inkomende gegevens nu worden gebruikt door downstreamservices voor Platforms zoals [!DNL Real-time Customer Profile] en [!DNL Data Science Workspace]. Raadpleeg de volgende documenten voor meer informatie:

* [Overzicht van het realtime klantprofiel](../../../../profile/home.md)
* [Overzicht van de Data Science Workspace](../../../../data-science-workspace/home.md)

>[!WARNING]
>
> De interface van het Platform die in de volgende video wordt getoond is verouderd. Raadpleeg de bovenstaande documentatie voor de meest recente schermafbeeldingen en functionaliteit van de gebruikersinterface.
>
>[!VIDEO](https://video.tv.adobe.com/v/29711?quality=12&learn=on)
