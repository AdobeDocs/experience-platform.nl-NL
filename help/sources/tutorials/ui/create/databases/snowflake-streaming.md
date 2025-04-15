---
title: Gegevens vanuit uw Snowflake-database naar Experience Platform streamen met behulp van de gebruikersinterface
description: Leer hoe u gegevens kunt streamen van uw SnwofLake-database naar Experience Platform
exl-id: 49d488f1-90d8-452a-9f3e-02afdcc79b09
source-git-commit: 04a1cecbacdaf0b701d3ef18d03497973a8f3263
workflow-type: tm+mt
source-wordcount: '1597'
ht-degree: 0%

---

# Gegevens vanuit uw [!DNL Snowflake] -database naar Experience Platform streamen met de gebruikersinterface

Volg deze handleiding om te leren hoe u de gebruikersinterface kunt gebruiken om gegevens vanuit uw [!DNL Snowflake] -database te streamen naar Adobe Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

### Verificatie

Lees de gids op [ eerste vereiste opstelling voor  [!DNL Snowflake]  het stromen gegevens ](../../../../connectors/databases/snowflake-streaming.md) voor informatie over de stappen die u moet voltooien alvorens u het stromen gegevens van [!DNL Snowflake] aan Experience Platform kunt opnemen.

## Gebruik de [!DNL Snowflake Streaming] -bron om [!DNL Snowflake] -gegevens te streamen naar Experience Platform

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] . U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de *categorie van Gegevensbestanden*, selecteer **[!DNL Snowflake Streaming]**, en selecteer dan **[!UICONTROL Add data]**.

>[!TIP]
>
>Bronnen zonder geverifieerde account in de broncatalogus geven de optie **[!UICONTROL Set up]** weer. Zodra een geverifieerd account bestaat, verandert deze optie in **[!UICONTROL Add data]** .

![ de broncatalogus in Experience Platform UI, met de Snowflake die bronkaart stroomt geselecteerd.](../../../../images/tutorials/create/snowflake-streaming/catalog.png)

De pagina **[!UICONTROL Connect Snowflake Streaming account]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

>[!BEGINTABS]

>[!TAB  creeer een nieuwe rekening ]

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geeft u een naam, een optionele beschrijving en uw referenties op.

Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![ de nieuwe interface van de rekeningsverwezenlijking van het bronwerkschema.](../../../../images/tutorials/create/snowflake-streaming/new.png)

| Credentials | Beschrijving |
| --- | --- |
| Account | De naam van uw [!DNL Snowflake] account. Voor overeenkomsten op rekeningsnamen, lees de [[!DNL Snowflake Streaming]  authentificatiegids ](../../../../connectors/databases/snowflake-streaming.md#gather-required-credentials). |
| Warehouse | De naam van uw [!DNL Snowflake] magazijn. De opslagplaatsen beheren de uitvoering van vragen in [!DNL Snowflake]. Elk [!DNL Snowflake] -pakhuis is onafhankelijk van elkaar en moet afzonderlijk worden benaderd om gegevens naar Experience Platform te kunnen verzenden. |
| Database | De naam van de [!DNL Snowflake] -database. De database bevat de gegevens die u naar Experience Platform wilt verzenden. |
| Schema | (Optioneel) Het databaseschema dat aan uw [!DNL Snowflake] -account is gekoppeld. |
| Gebruikersnaam | De gebruikersnaam van uw [!DNL Snowflake] -account. |
| Wachtwoord | Het wachtwoord voor uw [!DNL Snowflake] -account. |
| Rol | (Optioneel) Een op maat gedefinieerde rol die voor een bepaalde verbinding aan een gebruiker kan worden gegeven. Als deze waarde niet is opgegeven, wordt deze standaard ingesteld op `public` . |

Voor meer informatie over rekeningsverwezenlijking, lees de sectie over [ het vormen rolmontages ](../../../../connectors/databases/snowflake-streaming.md#configure-role-settings) in het [!DNL Snowflake Streaming] overzicht.

>[!TAB  Gebruik een bestaande rekening ]

Als u een bestaand account wilt gebruiken, selecteert u **[!UICONTROL Existing account]** en selecteert u het gewenste account in de bestaande accountcatalogus.

Selecteer **[!UICONTROL Next]** om door te gaan.

![ de bestaande pagina van de rekeningsselectie van de broncatalogus.](../../../../images/tutorials/create/snowflake-streaming/existing.png)

>[!ENDTABS]

## Gegevens selecteren {#select-data}

>[!IMPORTANT]
>
>* Er moet een tijdstempelkolom in de brontabel staan om een streaminggegevensstroom te kunnen maken. Experience Platform moet de tijdstempel hebben om te weten wanneer gegevens worden ingevoerd en wanneer incrementele gegevens worden gestreamd. U kunt met terugwerkende kracht een tijdstempelkolom toevoegen voor een bestaande verbinding en een nieuwe gegevensstroom creëren.
>
>* Zorg ervoor dat het hoofdlettergebruik van de gegevensvelden in het bestand met voorbeeldbrongegevens in overeenstemming is met de [!DNL Snowflake] -richtlijnen voor de oplossing van hoofdletters en kleine letters voor id&#39;s. Lees het [[!DNL Snowflake]  document op herkenningsteken casing ](https://docs.snowflake.com/en/sql-reference/identifiers-syntax#label-identifier-casing) voor meer informatie.

De stap [!UICONTROL Select data] wordt weergegeven. In deze stap moet u de gegevens selecteren die u in Experience Platform wilt importeren, tijdstempels en tijdzones configureren en een bestand met voorbeeldbrongegevens opgeven voor de invoer van onbewerkte gegevens.

Gebruik de databasemap links op het scherm en selecteer de tabel die u naar Experience Platform wilt importeren.

![ de uitgezochte gegevensinterface met een geselecteerde gegevensbestandlijst.](../../../../images/tutorials/create/snowflake-streaming/select-table.png)

Selecteer vervolgens het kolomtype voor de tijdstempel van de tabel. U kunt kiezen uit twee typen tijdstempelkolommen: `TIMESTAMP_NTZ` of `TIMESTAMP_LTZ` . Als u een kolomtype `TIMESTAMP_NTZ` selecteert, moet u ook een tijdzone opgeven. De kolommen moeten een beperking hebben die niet null is. Voor meer informatie, lees de sectie over [ beperkingen en vaak gestelde vragen ](../../../../connectors/databases/snowflake-streaming.md#limitations-and-frequently-asked-questions).

Tijdens deze stap kunt u ook instellingen voor backfill configureren. Met Backfill wordt bepaald welke gegevens in eerste instantie worden ingevoerd. Als backfill is ingeschakeld, worden alle huidige bestanden in het opgegeven pad tijdens de eerste geplande inname opgenomen. Als dat niet het geval is, worden alleen de bestanden opgenomen die tussen de eerste opname en de begintijd worden geladen. Bestanden die vóór de begintijd zijn geladen, worden niet opgenomen.

Selecteer de schakeloptie **[!UICONTROL Backfill]** om terugvullen in te schakelen.

![ timestamp, timezone, en backfill configuratiestappen.](../../../../images/tutorials/create/snowflake-streaming/timezone.png)

Tot slot selecteert u **[!UICONTROL Choose file]** om een voorbeeldbrongegevens te uploaden om de set toewijzingen te maken. Deze set wordt in een latere stap gebruikt om uw oorspronkelijke gegevens toe te wijzen aan het XDM-model (Experience Data Model).

Als u klaar bent, selecteert u **[!UICONTROL Next]** om door te gaan.

![ de voorproef van de bronsteekproefgegevens.](../../../../images/tutorials/create/snowflake-streaming/preview.png)

## Gegevensset en gegevens over gegevensstroom opgeven {#provide-dataset-and-dataflow-details}

Daarna, moet u informatie over uw dataset en uw gegevensstroom verstrekken.

### Gegevens over gegevensset {#dataset-details}

Een dataset is een opslag en beheersconstructie voor een inzameling van gegevens, typisch een lijst, die een schema (kolommen) en gebieden (rijen) bevat. De gegevens die met succes in Experience Platform worden opgenomen worden voortgeduurd binnen het gegevensmeer als datasets. Tijdens deze stap, kunt u een nieuwe dataset tot stand brengen of een bestaande dataset gebruiken.

>[!BEGINTABS]

>[!TAB  Gebruik een nieuwe dataset ]

Als u een nieuwe gegevensset wilt gebruiken, selecteert u **[!UICONTROL New dataset]** en geeft u vervolgens een naam en een optionele beschrijving voor de gegevensset op. U moet ook een schema van het Model van de Gegevens van de Ervaring (XDM) selecteren dat uw dataset volgt aan.

![ de nieuwe interface van de datasetselectie.](../../../../images/tutorials/create/snowflake-streaming/new-dataset.png)

| Nieuwe gegevens gegevensset | Beschrijving |
| --- | --- |
| Naam uitvoergegevensset | De naam van uw nieuwe dataset. |
| Beschrijving | (Optioneel) Een kort overzicht van de nieuwe gegevensset. |
| Schema | Een vervolgkeuzelijst met schema&#39;s die in uw organisatie bestaan. U kunt ook uw eigen schema vóór het proces van de bronconfiguratie maken. Voor meer informatie, lees de gids op [ creërend een schema XDM in UI ](../../../../../xdm/tutorials/create-schema-ui.md). |

>[!TAB  Gebruik een bestaande dataset ]

Als u al een bestaande dataset hebt, selecteert u **[!UICONTROL Existing dataset]** en gebruikt u vervolgens de optie **[!UICONTROL Advanced search]** om een venster weer te geven met alle datasets in uw organisatie, inclusief de respectievelijke details, zoals of deze zijn ingeschakeld voor opname in Real-Time klantprofiel.

![ de bestaande interface van de datasetselectie.](../../../../images/tutorials/create/snowflake-streaming/existing-dataset.png)

>[!ENDTABS]

+++Selecteer voor stappen om de opname van het Profiel, de diagnostiek van de fout, en gedeeltelijke opname toe te laten.

Als uw dataset voor het Profiel van de Klant in real time wordt toegelaten, dan tijdens deze stap, kunt u **[!UICONTROL Profile dataset]** van een knevel voorzien om uw gegevens voor Profiel-opname toe te laten. U kunt deze stap ook gebruiken om **[!UICONTROL Error diagnostics]** en **[!UICONTROL Partial ingestion]** in te schakelen.

* **[!UICONTROL Error diagnostics]**: Selecteer **[!UICONTROL Error diagnostics]** om de bron de instructie te geven foutdiagnostiek te produceren waarnaar u later kunt verwijzen bij het controleren van de gegevenssetactiviteit en de status van de gegevensstroom.
* **[!UICONTROL Partial ingestion]**: Gedeeltelijke batch-opname is de mogelijkheid om gegevens met fouten in te voeren tot een bepaalde configureerbare drempel. Met deze functie kunt u al uw nauwkeurige gegevens in Experience Platform opnemen, terwijl al uw onjuiste gegevens afzonderlijk worden opgeslagen met informatie over waarom deze niet geldig zijn.

+++

### Gegevens gegevensstroom {#dataflow-details}

Zodra uw dataset wordt gevormd, moet u details op uw gegevensstroom, met inbegrip van een naam, een facultatieve beschrijving, en waakzame configuraties dan verstrekken.

![ de stap van de de detailconfiguratie van de gegevensstroom.](../../../../images/tutorials/create/snowflake-streaming/dataflow-details.png)

| Dataflow-configuraties | Beschrijving |
| --- | --- |
| Naam gegevensstroom | De naam van de gegevensstroom.  Standaard wordt hiervoor de naam gebruikt van het bestand dat wordt geïmporteerd. |
| Beschrijving | (Optioneel) Een korte beschrijving van uw gegevensstroom. |
| Waarschuwingen | Experience Platform kan op gebeurtenissen gebaseerde waarschuwingen produceren waarop gebruikers zich kunnen abonneren. Deze opties vereisen een lopende gegevensstroom om hen teweeg te brengen. Voor meer informatie, lees het [ alarm overzicht ](../../alerts.md) <ul><li>**het Begin van de Looppas van Bronnen Dataflow**: Selecteer dit alarm om een bericht te ontvangen wanneer uw dataflow looppas begint.</li><li>**Bronnen Dataflow de Succes van de Looppas**: Selecteer dit alarm om een bericht te ontvangen als uw dataflow zonder enige fouten beëindigt.</li><li>**de Uitval van de Looppas van Gegevensstroom van Bronnen**: Selecteer dit alarm om een bericht te ontvangen als uw dataflow looppas met om het even welke fouten beëindigt.</li></ul> |

Als u klaar bent, selecteert u **[!UICONTROL Next]** om door te gaan.

## Velden toewijzen aan een XDM-schema {#mapping}

De stap [!UICONTROL Mapping] wordt weergegeven. Gebruik de toewijzingsinterface om uw brongegevens toe te wijzen aan de aangewezen schemagebieden alvorens die gegevens in Experience Platform op te nemen, dan uitgezocht **[!UICONTROL Next]**. Voor een uitgebreide gids op hoe te om de kaartinterface te gebruiken, lees de [ gids UI van de Prep van Gegevens ](../../../../../data-prep/ui/mapping.md) voor meer informatie.

![ de afbeeldingsinterface van het bronwerkschema.](../../../../images/tutorials/create/snowflake-streaming/mapping.png)

## Controleer uw gegevensstroom {#review}

De laatste stap in het proces voor het maken van een gegevensstroom is het controleren van de gegevensstroom voordat deze wordt uitgevoerd. Gebruik de stap **[!UICONTROL Review]** om de details van de nieuwe gegevensstroom te bekijken voordat deze wordt uitgevoerd. De details worden gegroepeerd in de volgende categorieën:

* **Verbinding**: Toont het brontype, de relevante weg van het gekozen brondossier, en het aantal kolommen binnen dat brondossier.
* **wijst dataset &amp; kaartgebieden** toe: Toont welke dataset de brongegevens in, met inbegrip van het schema worden opgenomen dat de dataset aan vasthoudt.

Nadat u de gegevensstroom hebt gereviseerd, selecteert u **[!UICONTROL Finish]** en laat u enige tijd over om de gegevensstroom te maken.

![ de stap van het Overzicht van het bronwerkschema.](../../../../images/tutorials/create/snowflake-streaming/review.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een streaminggegevensstroom voor [!DNL Snowflake] -gegevens gemaakt. Lees de onderstaande documentatie voor aanvullende bronnen.

### Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over innamesnelheden, succes, en fouten te bekijken. Voor meer informatie over hoe te om het stromen dataflows te controleren, bezoek het leerprogramma op [ het stromen dataflows in UI ](../../monitor-streaming.md).

### Uw gegevensstroom bijwerken

Om configuraties voor uw dataflows bij te werken die, afbeelding, en algemene informatie plannen, bezoek het leerprogramma op [ bijwerken brondataflows in UI ](../../update-dataflows.md).

### Uw gegevensstroom verwijderen

U kunt gegevensstromen verwijderen die niet meer nodig zijn of die onjuist zijn gemaakt met de functie **[!UICONTROL Delete]** die beschikbaar is in de **[!UICONTROL Dataflows]** -werkruimte. Voor meer informatie over hoe te om dataflows te schrappen, bezoek het leerprogramma bij [ het schrappen van dataflows in UI ](../../delete.md).
