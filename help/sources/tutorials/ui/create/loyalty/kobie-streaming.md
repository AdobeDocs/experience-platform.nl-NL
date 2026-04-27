---
title: Gegevens via de gebruikersinterface streamen van Kobie naar Experience Platform
description: Leer hoe u gegevens van Kobie naar Adobe Experience Platform kunt streamen met behulp van de gebruikersinterface.
hide: true
hidefromtoc: true
exl-id: 4e2e3287-3673-4426-8666-5f2ee284ca3d
source-git-commit: 1939a3914b796985a837aee00b6ad14299b976ec
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 0%

---

# Gegevens van [!DNL Kobie Streaming Events] naar Experience Platform streamen met de gebruikersinterface

[!DNL Kobie Alchemy Loyalty Cloud (KALC)] is een hoogst configureerbaar, veilig, en scalable platform MACH dat zich aan uw loyaliteitsstrategie aanpast - het versnellen van tijd aan waarde, het verbeteren van efficiency, en het beschermen van uw merk met onderneming-rang bestuur. Dankzij naadloze integratie tussen CDP&#39;s, CRM&#39;s, CMS en meer biedt [!DNL KALC] marketers de mogelijkheid om realtime personalisatie te leveren voor elk kanaal en tegelijk de flexibiliteit en traceerbaarheid te bieden die nodig zijn om te evolueren naarmate uw merkloyaliteit groeit.

Lees deze handleiding voor het maken van verbinding en het streamen van gegevens van [!DNL Kobie Streaming Events] naar Adobe Experience Platform met de werkruimte voor bronnen in de gebruikersinterface.

>[!IMPORTANT]
>
>Neem rechtstreeks contact op met uw [!DNL Kobie Client Services] -vertegenwoordiger voor informatie over het instellen en toewijzen van voorwaarden.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

## Navigeren door de catalogus met bronnen

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van *[!UICONTROL Sources]* . Selecteer de gewenste categorie in het deelvenster *[!UICONTROL Categories]* . U kunt ook met de zoekbalk navigeren naar de specifieke bron die u wilt gebruiken.

Als u gegevens wilt streamen vanuit [!DNL Kobie] , selecteert u de **[!UICONTROL Kobie Streaming Events]** bronkaart onder *[!UICONTROL Loyalty]* en selecteert u vervolgens **[!UICONTROL Add data]** .

>[!TIP]
>
>Bronnen in de catalogus met bronnen geven de optie **[!UICONTROL Set up]** weer wanneer een bepaalde bron nog geen geverifieerde account heeft. Zodra een geverifieerd account is gemaakt, verandert deze optie in **[!UICONTROL Add data]** .

![ de broncatalogus in UI met de Kobie die kaart van Gebeurtenissen stroomt die.](../../../../images/tutorials/create/kobie/catalog.png)

## Gegevens selecteren

Gebruik vervolgens de interface van *[!UICONTROL Select data]* om een voorbeeld-JSON-bestand te uploaden om uw bronschema te definiëren. Tijdens deze stap kunt u de voorvertoningsinterface gebruiken om de bestandsstructuur van de laadbewerking weer te geven. Selecteer **[!UICONTROL Next]** als u klaar bent.

![ de uitgezochte gegevensstap van het bronwerkschema ](../../../../images/tutorials/create/kobie/select-data.png)

## Gegevens gegevensstroom

Daarna, moet u informatie betreffende uw dataset en uw gegevensstroom verstrekken.

### Gegevens over gegevensset

Een dataset is een opslag en beheersconstructie voor een inzameling van gegevens, typisch een lijst, die een schema (kolommen/gebieden) en verslagen (rijen) bevat. De gegevens die met succes in Experience Platform worden opgenomen worden voortgeduurd binnen het gegevensmeer als datasets.

Tijdens deze stap, kunt u of een bestaande dataset gebruiken of een nieuwe dataset creëren.

>[!NOTE]
>
>Ongeacht of u een bestaande dataset gebruikt of een nieuwe dataset creeert, moet u ervoor zorgen dat uw dataset **voor de opname van het Profiel** wordt toegelaten.

+++Selecteer deze optie als u de stappen voor het inschakelen van profielopname, foutdiagnose en gedeeltelijke inname wilt uitvoeren.

Als uw dataset voor het Profiel van de Klant in real time wordt toegelaten, dan tijdens deze stap, kunt u **[!UICONTROL Profile dataset]** van een knevel voorzien om uw gegevens voor de opname van het Profiel toe te laten. U kunt deze stap ook gebruiken om **[!UICONTROL Error diagnostics]** en **[!UICONTROL Partial ingestion]** in te schakelen.

* **[!UICONTROL Error diagnostics]**: Selecteer **[!UICONTROL Error diagnostics]** om de bron de instructie te geven foutdiagnostiek te produceren waarnaar u later kunt verwijzen bij het controleren van de gegevenssetactiviteit en de status van de gegevensstroom.
* **[!UICONTROL Partial ingestion]**: Gedeeltelijke batch-opname is de mogelijkheid om gegevens met fouten in te voeren tot een bepaalde configureerbare drempel. Met deze functie kunt u al uw nauwkeurige gegevens in Experience Platform opnemen, terwijl al uw onjuiste gegevens afzonderlijk worden opgeslagen met informatie over waarom deze niet geldig zijn.

+++

### Gegevens gegevensstroom

Zodra uw dataset wordt gevormd, moet u details op uw gegevensstroom, met inbegrip van een naam, een facultatieve beschrijving, en waakzame configuraties dan verstrekken.

![ de dataflow detailinterface ](../../../../images/tutorials/create/kobie/dataflow-details.png)

| Dataflow-configuraties | Beschrijving |
| --- | --- |
| Naam gegevensstroom | De naam van de gegevensstroom. Standaard wordt hiervoor de naam gebruikt van het bestand dat wordt geïmporteerd. |
| Beschrijving | (Optioneel) Een korte beschrijving van uw gegevensstroom. |
| Waarschuwingen | Experience Platform kan waarschuwingen op basis van gebeurtenissen produceren waarop gebruikers zich kunnen abonneren. Met deze opties kan een actieve gegevensstroom deze waarschuwingen activeren.  Voor meer informatie, lees het [ alarm overzicht ](../../alerts.md) <ul><li>**het Begin van de Looppas van Bronnen Dataflow**: Selecteer dit alarm om een bericht te ontvangen wanneer uw dataflow looppas begint.</li><li>**Bronnen Dataflow de Succes van de Looppas**: Selecteer dit alarm om een bericht te ontvangen als uw dataflow zonder enige fouten beëindigt.</li><li>**de Uitval van de Looppas van Gegevensstroom van Bronnen**: Selecteer dit alarm om een bericht te ontvangen als uw dataflow looppas met om het even welke fouten beëindigt.</li></ul> |

{style="table-layout:auto"}

## Toewijzing

Gebruik de toewijzingsinterface om uw brongegevens toe te wijzen aan de aangewezen schemagebieden alvorens gegevens aan Experience Platform in te voeren. Voor meer informatie, lees de [ kaartgids in UI ](../../../../../data-prep/ui/mapping.md).

![ de afbeeldingsstap van het werkschema ](../../../../images/tutorials/create/kobie/mapping.png)

## Controleren

De stap *[!UICONTROL Review]* wordt weergegeven, zodat u de details van de gegevensstroom kunt bekijken voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: geeft de accountnaam, het bronplatform en de bronnaam weer.
* **[!UICONTROL Assign dataset and map fields]**: toont de doeldataset en het schema dat de dataset volgt.

Selecteer **[!UICONTROL Finish]** nadat u hebt bevestigd dat de details juist zijn.

![ de revisiestap in het bronwerkschema.](../../../../images/tutorials/create/kobie/review.png)

## De URL van het streamingeindpunt ophalen

Als de verbinding is gemaakt, wordt de pagina met brondetails weergegeven. Deze pagina bevat details van de zojuist gemaakte verbinding, waaronder eerder uitgevoerde dataflows, ID en URL van het streamingeindpunt.

![ het stromen eindpunt URL.](../../../../images/tutorials/create/kobie/streaming-endpoint.png)

## Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over innamepercentages, succes, en fouten te zien. Voor meer informatie over hoe te om dataflow te controleren, zie het leerprogramma op [ controlerekeningen en dataflows in UI ](../../monitor-streaming.md).
