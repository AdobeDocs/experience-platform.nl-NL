---
title: Gegevens vanuit uw Snowflake-database naar Experience Platform streamen met behulp van de gebruikersinterface
description: Leer hoe u gegevens kunt streamen van uw SnwofLake-database naar Experience Platform
exl-id: 49d488f1-90d8-452a-9f3e-02afdcc79b09
source-git-commit: 0d646136da2c508fe7ce99a15787ee15c5921a6c
workflow-type: tm+mt
source-wordcount: '1397'
ht-degree: 0%

---

# Gegevens vanuit uw [!DNL Snowflake] -database naar Experience Platform streamen met de gebruikersinterface

Lees deze handleiding voor informatie over het streamen van gegevens van uw [!DNL Snowflake] -database naar Experience Platform met de werkruimte voor bronnen in de gebruikersinterface.

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

Onder de *categorie van Gegevensbestanden*, selecteer **[!DNL Snowflake Streaming]**, en selecteer dan **[!UICONTROL Set up]**.

>[!TIP]
>
>Bronnen zonder geverifieerde account in de broncatalogus geven de optie **[!UICONTROL Set up]** weer. Zodra een geverifieerd account bestaat, verandert deze optie in **[!UICONTROL Add data]** .

![ de broncatalogus in Experience Platform UI, met de Snowflake die bronkaart stroomt geselecteerd.](../../../../images/tutorials/create/snowflake-streaming/catalog.png)

De pagina **[!UICONTROL Connect Snowflake Streaming account]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Een nieuwe account maken

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geeft u een naam en een optionele beschrijving voor uw account.

![ de nieuwe interface van de rekeningsverwezenlijking van het bronwerkschema.](../../../../images/tutorials/create/snowflake-streaming/new.png)

>[!BEGINTABS]

>[!TAB  Basisauthentificatie ]

Als u [!UICONTROL Basic authentication] wilt gebruiken, selecteert u **[!UICONTROL Basic Authentication for Snowflake]** en geeft u referenties voor uw [!DNL Snowflake] -account op. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat de verbinding enkele ogenblikken tot stand komen.

Lees het [!DNL Snowflake Streaming] overzicht voor meer informatie over [ verzamelen vereiste geloofsbrieven ](../../../../connectors/databases/snowflake-streaming.md#gather-required-credentials).

![ de nieuwe rekeningsinterface in het bronwerkschema, met geselecteerde basisauthentificatie.](../../../../images/tutorials/create/snowflake-streaming/basic-auth.png)

>[!TAB  authentificatie KeyPair ]

Als u [!UICONTROL KeyPair authentication] wilt gebruiken, selecteert u **[!UICONTROL KeyPair Authentication for Snowflake]** en geeft u referenties voor uw [!DNL Snowflake] -account op. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat de verbinding enkele ogenblikken tot stand komen.

Lees het [!DNL Snowflake Streaming] overzicht voor meer informatie over [ verzamelen vereiste geloofsbrieven ](../../../../connectors/databases/snowflake-streaming.md#gather-required-credentials).

![ de nieuwe rekeningsinterface in het bronwerkschema, sleutel-paar geselecteerde authentificatie ](../../../../images/tutorials/create/snowflake-streaming/key-pair.png)

>[!ENDTABS]

Als u een bestaande account wilt gebruiken, kiest u **[!UICONTROL Existing account]** , selecteert u uw account in de lijst en selecteert u **[!UICONTROL Next]** .

## Gegevens selecteren {#select-data}

>[!IMPORTANT]
>
>* Er moet een tijdstempelkolom in de brontabel staan om een streaminggegevensstroom te kunnen maken. Experience Platform moet de tijdstempel hebben om te weten wanneer gegevens worden ingevoerd en wanneer incrementele gegevens worden gestreamd. U kunt met terugwerkende kracht een tijdstempelkolom toevoegen voor een bestaande verbinding en een nieuwe gegevensstroom creëren.
>
>* Zorg ervoor dat het hoofdlettergebruik van de gegevensvelden in het bestand met voorbeeldbrongegevens in overeenstemming is met de [!DNL Snowflake] -richtlijnen voor de oplossing van hoofdletters en kleine letters voor id&#39;s. Lees het [[!DNL Snowflake]  document op herkenningsteken casing ](https://docs.snowflake.com/en/sql-reference/identifiers-syntax#label-identifier-casing) voor meer informatie.

De stap [!UICONTROL Select data] wordt weergegeven. In deze stap moet u de gegevens selecteren die u in Experience Platform wilt importeren, tijdstempels en tijdzones configureren en een bestand met voorbeeldbrongegevens opgeven voor de invoer van onbewerkte gegevens.

Gebruik de databasemap links op het scherm en selecteer de tabel die u naar Experience Platform wilt importeren.

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

Als u een bestaande dataset hebt, selecteert u **[!UICONTROL Existing dataset]** en gebruikt u vervolgens de optie **[!UICONTROL Advanced search]** om een venster weer te geven met alle datasets in uw organisatie, inclusief de respectievelijke details, zoals of deze zijn ingeschakeld voor opname in Real-Time Klantprofiel.

![ de bestaande interface van de datasetselectie.](../../../../images/tutorials/create/snowflake-streaming/dataset.png)

Als u een nieuwe gegevensset wilt gebruiken, selecteert u **[!UICONTROL New dataset]** en geeft u vervolgens een naam en een optionele beschrijving voor de gegevensset op. U moet ook een schema van het Model van de Gegevens van de Ervaring (XDM) selecteren dat uw dataset volgt aan.

| Nieuwe gegevens gegevensset | Beschrijving |
| --- | --- |
| Naam uitvoergegevensset | De naam van uw nieuwe dataset. |
| Beschrijving | (Optioneel) Een kort overzicht van de nieuwe gegevensset. |
| Schema | Een vervolgkeuzelijst met schema&#39;s die in uw organisatie bestaan. U kunt ook uw eigen schema vóór het proces van de bronconfiguratie maken. Voor meer informatie, lees de gids op [ creërend een schema XDM in UI ](../../../../../xdm/tutorials/create-schema-ui.md). |

### Gegevens gegevensstroom {#dataflow-details}

Zodra uw dataset wordt gevormd, moet u details op uw gegevensstroom, met inbegrip van een naam, een facultatieve beschrijving, en waakzame configuraties dan verstrekken.

![ de stap van de de detailconfiguratie van de gegevensstroom.](../../../../images/tutorials/create/snowflake-streaming/dataflow-detail.png)

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
