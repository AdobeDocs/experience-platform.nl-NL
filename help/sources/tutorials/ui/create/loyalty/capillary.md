---
title: Verbinding maken met Capillary met Experience Platform via de gebruikersinterface
description: Leer hoe u Capillary kunt verbinden met Experience Platform via de gebruikersinterface
badge: Beta
exl-id: c90e6500-b92c-44ba-8de6-84e772bd9db1
source-git-commit: 428aed259343f56a2bf493b40ff2388340fffb7b
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 0%

---

# Verbinding maken [!DNL Capillary Streaming Events] met Experience Platform via de gebruikersinterface

>[!AVAILABILITY]
>
>De bron [!DNL Capillary Streaming Events] is in bèta. Lees de [ termijnen en voorwaarden ](../../../../home.md#terms-and-conditions) in het bronoverzicht voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

Lees deze handleiding voor informatie over hoe u uw [!DNL Capillary] -database kunt verbinden met Adobe Experience Platform via de werkruimte voor bronnen in de Experience Platform-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

>[!NOTE]
>
>Lees het [[!DNL Capillary Streaming Events]  overzicht ](../../../../connectors/loyalty/capillary.md) voor informatie over opstelling die voor de [!DNL Capillary] bron wordt vereist.

## Navigeren door de catalogus met bronnen

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van *[!UICONTROL Sources]* . Selecteer de juiste categorie in het deelvenster *[!UICONTROL Categories]*. U kunt ook op de zoekbalk navigeren naar de specifieke bron die u wilt gebruiken.

Als u [!DNL Capillary] wilt gebruiken, selecteert u de **[!UICONTROL Capillary Streaming Events]** bronkaart onder *[!UICONTROL Loyalty]* en selecteert u vervolgens **[!UICONTROL Add data]** .

>[!TIP]
>
>Bronnen in de catalogus met bronnen geven de optie **[!UICONTROL Set up]** weer wanneer een bepaalde bron nog geen geverifieerde account heeft. Zodra een geverifieerd account is gemaakt, verandert deze optie in **[!UICONTROL Add data]** .

![ de broncatalogus in UI met Capillary die de kaart van Gebeurtenissen stroomt die.](../../../../images/tutorials/create/capillary/catalog.png)

## Gegevens selecteren

Gebruik vervolgens de interface van *[!UICONTROL Select data]* om een voorbeeld-JSON-bestand te uploaden om uw bronschema te definiëren. Tijdens deze stap kunt u de voorvertoningsinterface gebruiken om de bestandsstructuur van de laadbewerking weer te geven. Selecteer **[!UICONTROL Next]** als u klaar bent.

>[!TIP]
>
>U kunt de [ Gebeurtenissen en schema&#39;s van het Profiel ](../../../../images/tutorials/create/capillary/schemas.zip) voor [!DNL Capillary] downloaden om in de interface van de gegevensselectie te gebruiken.

![ de uitgezochte gegevensstap van het bronwerkschema ](../../../../images/tutorials/create/capillary/select-data.png)

## Gegevens gegevensstroom

Daarna, moet u informatie betreffende uw dataset en uw gegevensstroom verstrekken.

### Gegevens over gegevensset

Een dataset is een opslag en beheersconstructie voor een inzameling van gegevens, typisch een lijst, die een schema (kolommen) en gebieden (rijen) bevat. De gegevens die met succes in Experience Platform worden opgenomen worden voortgeduurd binnen het gegevensmeer als datasets.

Tijdens deze stap, kunt u of een bestaande dataset gebruiken of een nieuwe dataset creëren.

>[!NOTE]
>
>Ongeacht of u een bestaande dataset gebruikt of een nieuwe dataset creeert, moet u ervoor zorgen dat uw dataset **voor de opname van het Profiel** wordt toegelaten.

+++Selecteer deze optie als u de stappen voor het inschakelen van profielopname, foutdiagnose en gedeeltelijke inname wilt uitvoeren.

Als uw dataset voor het Profiel van de Klant in real time wordt toegelaten, dan tijdens deze stap, kunt u **[!UICONTROL Profile dataset]** van een knevel voorzien om uw gegevens voor Profiel-opname toe te laten. U kunt deze stap ook gebruiken om **[!UICONTROL Error diagnostics]** en **[!UICONTROL Partial ingestion]** in te schakelen.

* **[!UICONTROL Error diagnostics]**: Selecteer **[!UICONTROL Error diagnostics]** om de bron de instructie te geven foutdiagnostiek te produceren waarnaar u later kunt verwijzen bij het controleren van de gegevenssetactiviteit en de status van de gegevensstroom.
* **[!UICONTROL Partial ingestion]**: Gedeeltelijke batch-opname is de mogelijkheid om gegevens met fouten in te voeren tot een bepaalde configureerbare drempel. Met deze functie kunt u al uw nauwkeurige gegevens in Experience Platform opnemen, terwijl al uw onjuiste gegevens afzonderlijk worden opgeslagen met informatie over waarom deze niet geldig zijn.

+++

### Gegevens gegevensstroom

Zodra uw dataset wordt gevormd, moet u details op uw gegevensstroom, met inbegrip van een naam, een facultatieve beschrijving, en waakzame configuraties dan verstrekken.

![ de dataflow detailinterface ](../../../../images/tutorials/create/capillary/dataflow-detail.png)

| Dataflow-configuraties | Beschrijving |
| --- | --- |
| Naam gegevensstroom | De naam van de gegevensstroom.  Standaard wordt hiervoor de naam gebruikt van het bestand dat wordt geïmporteerd. |
| Beschrijving | (Optioneel) Een korte beschrijving van uw gegevensstroom. |
| Waarschuwingen | Experience Platform kan waarschuwingen op basis van gebeurtenissen produceren waarop gebruikers zich kunnen abonneren. Met deze opties kan een actieve gegevensstroom deze waarschuwingen activeren.  Voor meer informatie, lees het [ alarm overzicht ](../../alerts.md) <ul><li>**het Begin van de Looppas van Bronnen Dataflow**: Selecteer dit alarm om een bericht te ontvangen wanneer uw dataflow looppas begint.</li><li>**Bronnen Dataflow de Succes van de Looppas**: Selecteer dit alarm om een bericht te ontvangen als uw dataflow zonder enige fouten beëindigt.</li><li>**de Uitval van de Looppas van Gegevensstroom van Bronnen**: Selecteer dit alarm om een bericht te ontvangen als uw dataflow looppas met om het even welke fouten beëindigt.</li></ul> |

{style="table-layout:auto"}

## Toewijzing

Gebruik de toewijzingsinterface om uw brongegevens toe te wijzen aan de aangewezen schemagebieden alvorens gegevens aan Experience Platform in te voeren. Voor meer informatie, lees de [ kaartgids in UI ](../../../../../data-prep/ui/mapping.md).

>[!TIP]
>
>U kunt de [ Gebeurtenissen en afbeeldingen van het Profiel ](../../../../images/tutorials/create/capillary/mappings.zip) voor [!DNL Capillary] downloaden en [ de dossiers invoeren aan Prep van Gegevens ](../../../../../data-prep/ui/mapping.md#import-mapping) wanneer u bereid bent om uw gegevens in kaart te brengen.

![ de kaartinterface voor Capillary.](../../../../images/tutorials/create/capillary/mappings.png)

## Controleren

De stap *[!UICONTROL Review]* wordt weergegeven, zodat u de details van de gegevensstroom kunt bekijken voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: geeft de accountnaam, het bronplatform en de bronnaam weer.
* **[!UICONTROL Assign dataset and map fields]**: toont de doeldataset en het schema dat de dataset volgt.

Selecteer **[!UICONTROL Finish]** nadat u hebt bevestigd dat de details juist zijn.

![ de revisiestap in het bronwerkschema.](../../../../images/tutorials/create/capillary/review.png)

## De URL van het streamingeindpunt ophalen

Als de verbinding is gemaakt, wordt de pagina met brondetails weergegeven. Deze pagina bevat details van de zojuist gemaakte verbinding, waaronder eerder uitgevoerde dataflows, ID en URL van het streamingeindpunt.

![ het stromen eindpunt URL.](../../../../images/tutorials/create/capillary/endpoint-url.png)
