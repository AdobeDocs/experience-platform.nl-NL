---
keywords: Experience Platform;home;populaire onderwerpen;Bronaansluiting voor analyse;Analytische aansluiting;Analytische bron;Analytics
solution: Experience Platform
title: Een Adobe Analytics-bronverbinding maken in de gebruikersinterface
topic: overview
type: Tutorial
description: Leer hoe u een Adobe Analytics-bronverbinding maakt in de gebruikersinterface om consumentengegevens over te brengen naar Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 0%

---


# Een Adobe Analytics-bronverbinding maken in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een Adobe Analytics-bronverbinding in de gebruikersinterface om consumentengegevens over te brengen naar Adobe Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [XDM-systeem](../../../../../xdm/home.md) (Experience Data Model): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
* [Klantprofiel](../../../../../profile/home.md) in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## Een bronverbinding maken met Adobe Analytics

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer **[!UICONTROL Bronnen]** in de linkernavigatiebalk om de werkruimte Bronnen te openen. Het **scherm Catalog** toont beschikbare bronnen om binnenkomende verbindingen met tot stand te brengen, en elke bron toont het aantal bestaande rekeningen en datasetstromen verbonden aan hen.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie **[!UICONTROL Adobe toepassingen]** **[!UICONTROL Adobe Analytics]** om een informatiebalk aan de rechterkant van het scherm weer te geven. De informatiebalk bevat een korte beschrijving van de geselecteerde bron en opties voor het maken van verbinding met de bron of het bekijken van de documentatie. Selecteer **[!UICONTROL Accounts]** om bestaande accounts weer te geven.

![](../../../../images/tutorials/create/analytics/catalog.png)

### Gegevens selecteren

De stap **[!UICONTROL Adobe Analytics]** wordt weergegeven. Eerder ingestelde gegevenssetstromen voor Analytics worden vermeld op dit scherm. U kunt een nieuwe datasetstroom tot stand brengen door **[!UICONTROL Selecteer gegevens]** te klikken.

>[!NOTE]
>
>Er kunnen meerdere interne verbindingen met een bron worden gemaakt om verschillende gegevens in te voeren.

![](../../../../images/tutorials/create/analytics/dataset-flows.png)

<!---Analytics report suites can be configured for one sandbox at a time. To import the same report suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

Van de lijst van beschikbare rapportreeksen, selecteer één u in Platform wilt brengen en **[!UICONTROL daarna]** klikken.

![](../../../../images/tutorials/create/analytics/select-data.png)

### Geef de gegevenssetstroom een naam

De **[!UICONTROL Dataset flow detail]** stap verschijnt, waar u een naam en een facultatieve beschrijving voor de datasetstroom moet verstrekken. Selecteer **[!UICONTROL Volgende]** als u klaar bent.

![](../../../../images/tutorials/create/analytics/dataset-flow-detail.png)

### De gegevenssetstroom controleren

De stap **[!UICONTROL Review]** verschijnt, toestaand u om uw nieuwe Analytics in-gebonden datasetstroom te herzien alvorens het wordt gecreeerd. De details van de verbinding worden gegroepeerd per categorieën, die omvatten:

* **[!UICONTROL Verbinding]**: Toont het type van de bronverbinding en de geselecteerde rapportreeks.
* **[!UICONTROL Gegevensset- en kaartvelden]** toewijzen: Wanneer het creëren van andere bronschakelaars, toont deze container welke dataset de brongegevens opnemen in, met inbegrip van het schema de dataset zich aan houdt. Het outputschema en de dataset worden automatisch gevormd voor de gegevenssetstromen van Analytics.

![](../../../../images/tutorials/create/analytics/review.png)

### De gegevenssetstroom controleren

Zodra uw datasetstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen. Selecteer **[!UICONTROL Gegevensstromen]** in het scherm **[!UICONTROL Catalogus]** om een lijst weer te geven met bestaande stromen die zijn gekoppeld aan uw account Analytics.

![](../../../../images/tutorials/create/analytics/catalog-dataset-flows.png)

Het scherm **Dataset flows** wordt weergegeven. Op deze pagina is een paar gegevenssetstromen, met inbegrip van informatie over hun naam, brongegevens, aanmaaktijd, en status.

De schakelaar concretiseert twee datasetstromen. De ene flow vertegenwoordigt de backfill-gegevens en de andere stroom is bedoeld voor live-gegevens. De gegevens van de backfill worden niet gevormd voor Profiel maar wordt verzonden naar het gegevensmeer voor analytische en gegeven-wetenschapsgebruik-gevallen.

Zie [Overzicht van de gegevensconnector Analytics](../../../../connectors/adobe-applications/analytics.md) voor meer informatie over backfill, live gegevens en de bijbehorende latentie.

Selecteer de datasetstroom u wenst om van de lijst te bekijken.

![](../../../../images/tutorials/create/analytics/backfill.png)

De pagina **Datasetactiviteit** wordt weergegeven. Op deze pagina wordt de snelheid van berichten weergegeven die in de vorm van een grafiek worden gebruikt. Selecteer *Gegevensbeheer* in de bovenste koptekst om de labelvelden te openen.

![](../../../../images/tutorials/create/analytics/batches.png)

U kunt de geërfte etiketten van een datasetstroom van het *Gegevens bestuur* scherm bekijken. Als u specifieke labels wilt openen, selecteert u de knop Bewerken aan de rechterbovenzijde.

![](../../../../images/tutorials/create/analytics/data-gov.png)

Het deelvenster **Regellabels bewerken** wordt weergegeven. Dit scherm staat u toe om tot het contract, de identiteit, en de gevoelige etiketten van een datasetstroom toegang te hebben en uit te geven.

Voor meer informatie over hoe te om gegevens te etiketteren die uit Analytics komen, bezoek [de gids van de etiketten van het gegevensgebruik](../../../../../data-governance/labels/user-guide.md).

![](../../../../images/tutorials/create/analytics/labels.png)

## Volgende stappen en extra bronnen

Zodra de verbinding wordt gecreeerd, wordt een doelschema en datasetstroom automatisch gecreeerd om de inkomende gegevens te bevatten. Bovendien vindt de terugvulling van gegevens plaats en neemt deze tot 13 maanden aan historische gegevens in. Wanneer de aanvankelijke opname voltooit, analyseert gegevens en door de stroomafwaartse diensten van het Platform zoals het Profiel van de Klant In real time en de Dienst van de Segmentatie wordt gebruikt. Raadpleeg de volgende documenten voor meer informatie:

* [Overzicht van het realtime klantprofiel](../../../../../profile/home.md)
* [Overzicht van segmentatieservice](../../../../../segmentation/home.md)
* [Overzicht van de Data Science Workspace](../../../../../data-science-workspace/home.md)
* [Overzicht van Query Service](../../../../../query-service/home.md)

De volgende video is bedoeld ter ondersteuning van uw inzicht in het opnemen van gegevens via de Adobe Analytics Source-connector:

>[!WARNING]
>
> De interface [!DNL Platform] die in de volgende video wordt getoond is verouderd. Raadpleeg de bovenstaande documentatie voor de meest recente schermafbeeldingen en functionaliteit van de gebruikersinterface.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)

