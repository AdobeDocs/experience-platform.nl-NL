---
description: Leer hoe u dataflows voor uw bestemmingen kunt controleren gebruikend het gebruikersinterface van het Experience Platform.
solution: Experience Platform
title: Dataflows voor Doelen in UI controleren
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
source-git-commit: 93430a9ba5911bf8dc901ec3f82f06a6b25b8dc4
workflow-type: tm+mt
source-wordcount: '3183'
ht-degree: 0%

---

# Dataflows voor doelen in de UI controleren

Gebruik de diverse bestemmingen in de catalogus van het Experience Platform om uw gegevens van Platform aan ontelbare externe partners te activeren. Platform maakt het proces om de stroom van gegevens aan uw bestemmingen gemakkelijker te volgen door transparantie van gegevensstromen te verstrekken.

Het controledashboard voorziet u van een visuele vertegenwoordiging van de reis van een dataflow, met inbegrip van de bestemming die de gegevens worden geactiveerd aan, het type gegevens dat u bekijkt, uitgevoerde gegevens per dataflow looppas, en veel meer.

Dit leerprogramma verstrekt instructies op hoe u of dataflows direct in de bestemmingswerkruimte kunt controleren of het controledashboard gebruiken om dataflows voor uw bestemmingen te controleren gebruikend het gebruikersinterface van het Experience Platform.

## Aan de slag {#getting-started}

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [Gegevensstromen](../home.md): Gegevensstromen zijn een weergave van gegevenstaken die gegevens verplaatsen over het hele platform. Dataflows worden gevormd over verschillende diensten, die gegevens van bronschakelaars aan doeldatasets helpen bewegen, aan [!DNL Identity] en [!DNL Profile], en [!DNL Destinations].
   - [Dataflow-uitvoering](../../sources/notifications.md): De looppas van Dataflow is de terugkomende geplande banen die op de frequentieconfiguratie van geselecteerde dataflows worden gebaseerd.
- [Doelen](../../destinations/home.md): De bestemmingen zijn pre-gebouwde integratie met algemeen gebruikte toepassingen die voor de naadloze activering van gegevens van Platform voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen toestaan.
- [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## Gegevens controleren in de werkruimte Doelen {#monitor-dataflows-in-the-destinations-workspace}

In de **[!UICONTROL Destinations]** binnen de gebruikersinterface van het platform navigeert u naar de **[!UICONTROL Browse]** en selecteert u de naam van een doel dat u wilt weergeven.

![Doelweergave selecteren met gemarkeerde doelverbinding](../assets/ui/monitor-destinations/select-destination.png)

Er wordt een lijst met bestaande gegevensstromen weergegeven. Op deze pagina vindt u een lijst met zichtbare gegevensstromen, waaronder informatie over het doel, de gebruikersnaam, het aantal gegevensstromen en de status.

Zie de volgende tabel voor meer informatie over statussen:

| Status | Beschrijving |
| ------ | ----------- |
| Ingeschakeld | De `Enabled` status geeft aan dat een gegevensstroom actief is en gegevens exporteert volgens het schema dat is opgegeven. |
| Uitgeschakeld | De `Disabled` status geeft aan dat een gegevensstroom inactief is en geen gegevens exporteert. |
| Verwerking | De `Processing` status geeft aan dat een gegevensstroom nog niet actief is. Deze status wordt vaak direct na het maken van een nieuwe gegevensstroom aangetroffen. |
| Fout | De `Error` status geeft aan dat het activeringsproces van een gegevensstroom is onderbroken. |

### Dataflow wordt uitgevoerd voor streamingdoelen {#dataflow-runs-for-streaming-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation_streaming"
>title="Gegevens gegevensstroom uitvoeren"
>abstract="De gegevens van de bestemmingdataflow looppas bevatten informatie over de activeringsstatus van een publiek en metriek die van het Profiel van de Klant in real time wordt genomen om unieke identiteiten te produceren. Raadpleeg de handleiding voor metrische definities voor meer informatie."

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_streaming"
>title="Ontvangen profielen"
>abstract="Het totale aantal profielen dat is ontvangen in de gegevensstroom. Deze waarde wordt elke 60 minuten bijgewerkt."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_streaming"
>title="Geactiveerde identiteiten"
>abstract="Het aantal afzonderlijke profiel-id&#39;s dat is geactiveerd voor het geselecteerde doel. Deze metrische waarde bevat identiteiten die zijn gemaakt, bijgewerkt en verwijderd uit geëxporteerde doelgroepen."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_streaming"
>title="Uitgesloten identiteiten"
>abstract="Het aantal afzonderlijke profielrecords dat is uitgesloten van activering voor de geselecteerde bestemming op basis van ontbrekende kenmerken en schending van de toestemming."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesfailed_streaming"
>title="Identiteiten mislukt"
>abstract="Het aantal individuele profielidentiteiten die voor de geselecteerde bestemming ontbraken. Controleer de foutdiagnostiek voor meer informatie."

Voor streamingdoelen geldt het [!UICONTROL Dataflow runs] bevat een update per uur voor metrische gegevens in uw dataflow-runtime. De meest prominente statistieken met het label zijn voor identiteiten.

De identiteiten vertegenwoordigen de verschillende facetten van een profiel. Als een profiel bijvoorbeeld zowel een telefoonnummer als een e-mailadres bevat, heeft dat profiel twee identiteiten.

Er wordt een lijst met afzonderlijke reeksen en de bijbehorende maatstaven weergegeven, samen met de volgende totalen voor identiteiten:

- **[!UICONTROL Identities activated]**: Het totale aantal profielidentiteiten dat is geactiveerd voor de geselecteerde bestemming. Deze metrische waarde bevat identiteiten die zijn gemaakt, bijgewerkt en verwijderd uit geëxporteerde doelgroepen.
- **[!UICONTROL Identities excluded]**: Het totale aantal profiel-id&#39;s dat voor activering wordt overgeslagen op basis van ontbrekende kenmerken en schending van de toestemming.
- **[!UICONTROL Identities failed]**: Het totale aantal profielidentiteiten dat niet aan de bestemming wegens fouten wordt geactiveerd.

![Dataflow voert details voor het stromen bestemmingen uit.](../assets/ui/monitor-destinations/dataflow-runs-stream.png)

Elke individuele dataflow run toont de volgende details:

- **[!UICONTROL Dataflow run start]**: De tijd waarop de dataflow is gestart. Voor het stromen dataflow looppas, vangt het Experience Platform metriek op het begin van dataflow looppas, in de vorm van uurmetriek wordt gebaseerd. Voor het stromen dataflow looppas, als een dataflow looppas, bijvoorbeeld, bij 10:30PM begon, metrisch toont de begintijd zoals 10:00 PM in UI.
- **[!UICONTROL Processing time]**: De hoeveelheid tijd die het voor dataflow nam in werking te stellen proces.
   - Voor **[!UICONTROL completed]** De metrische verwerkingstijd toont altijd één uur.
   - Voor dataflow-run die zich nog steeds in een **[!UICONTROL processing]** staat, het venster om alle metriek te vangen open meer dan een uur, om alle metriek te verwerken die aan de dataflow looppas beantwoorden. Bijvoorbeeld, zou een dataflow looppas die bij 9:30 AM begon in een verwerkingsstaat één uur en dertig minuten kunnen blijven om alle metriek te vangen en te verwerken. Vervolgens wordt het verwerkingsvenster gesloten en wordt de status van de dataflow-run bijgewerkt naar **voltooid**, wordt de weergegeven verwerkingstijd gewijzigd in één uur.
- **[!UICONTROL Profiles received]**: Het totale aantal profielen dat is ontvangen in de gegevensstroom.
- **[!UICONTROL Identities activated]**: Het totale aantal profielidentiteiten dat met succes aan de geselecteerde bestemming als deel van dataflow looppas werd geactiveerd. Deze metrische waarde bevat identiteiten die zijn gemaakt, bijgewerkt en verwijderd uit geëxporteerde doelgroepen.
- **[!UICONTROL Identities excluded]**: Het totale aantal profiel-id&#39;s dat van activering is uitgesloten op basis van ontbrekende kenmerken en schending van de toestemming.
- **[!UICONTROL Identities failed]** Het totale aantal profielidentiteiten dat niet aan de bestemming wegens fouten wordt geactiveerd.
- **[!UICONTROL Activation rate]**: Het percentage ontvangen identiteiten dat is geactiveerd of overgeslagen. De volgende formule laat zien hoe deze waarde wordt berekend:
  ![Activeringssnelheidsformule.](../assets/ui/monitor-destinations/activation-rate-formula.png)
- **[!UICONTROL Status]**: Geeft de status aan waarin de dataflow zich bevindt: een van de volgende [!UICONTROL Completed] of [!UICONTROL Processing]. [!UICONTROL Completed] betekent dat alle identiteiten voor de overeenkomstige dataflow run binnen de periode van één uur werden uitgevoerd. [!UICONTROL Processing] betekent dat de dataflow run nog niet is voltooid.

Om de details van een bepaalde dataflow looppas te bekijken, selecteer de begintijd van de looppas van de lijst.

De detailpagina voor een dataflow-run bevat aanvullende informatie zoals het aantal ontvangen profielen, het aantal geactiveerde identiteiten, het aantal mislukte identiteiten en het aantal uitgesloten identiteiten.

![Gegevens over gegevensstroom voor streamingdoelen.](../assets/ui/monitor-destinations/dataflow-details-stream.png)

Op de detailpagina wordt ook een lijst met mislukte identiteiten en identiteiten weergegeven die zijn uitgesloten. De informatie voor zowel de mislukte als uitgesloten identiteiten wordt getoond, met inbegrip van de foutencode, het aantal van de identiteit, en beschrijving. Standaard worden in de lijst de mislukte identiteiten weergegeven. Als u overgeslagen identiteiten wilt weergeven, selecteert u de optie **[!UICONTROL Identities excluded]** schakelen.

![Dataflow-records voor streamingdoelen met een foutbericht gemarkeerd.](../assets/ui/monitor-destinations/dataflow-records-stream.png)

### Dataflow wordt uitgevoerd voor batchdoelen {#dataflow-runs-for-batch-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation"
>title="Gegevens gegevensstroom uitvoeren"
>abstract="De gegevens van de bestemmingdataflow looppas bevatten informatie over de activeringsstatus van een publiek en metriek die van het Profiel van de Klant in real time wordt genomen om unieke identiteiten te produceren. Raadpleeg de handleiding voor metrische definities voor meer informatie."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dataflows/ui/monitor-destinations.html#dataflow-runs-for-streaming-destinations" text="Dataflow wordt uitgevoerd voor streamingdoelen"

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_batch"
>title="Ontvangen profielen"
>abstract="Het totale aantal profielen dat is ontvangen in de gegevensstroom. Deze waarde wordt elke 60 minuten bijgewerkt."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_batch"
>title="Geactiveerde identiteiten"
>abstract="Het aantal afzonderlijke profiel-id&#39;s dat is geactiveerd voor het geselecteerde doel. Deze metrische waarde bevat identiteiten die zijn gemaakt, bijgewerkt en verwijderd uit geëxporteerde doelgroepen."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_batch"
>title="Uitgesloten identiteiten"
>abstract="Het aantal afzonderlijke profielrecords dat is uitgesloten van activering voor de geselecteerde bestemming op basis van ontbrekende kenmerken en schending van de toestemming."

Voor batchbestemmingen wordt de [!UICONTROL Dataflow runs] bevat metrische gegevens over de gegevensstroomuitvoering. Er wordt een lijst met afzonderlijke reeksen en de bijbehorende maatstaven weergegeven, samen met de volgende totalen voor identiteiten:

- **[!UICONTROL Identities activated]**: Het totale aantal profielidentiteiten dat is geactiveerd voor de geselecteerde bestemming. Deze metrische waarde bevat identiteiten die zijn gemaakt, bijgewerkt en verwijderd uit geëxporteerde doelgroepen.
- **[!UICONTROL Identities excluded]**: Het aantal individuele profielidentiteiten die zijn uitgesloten van activering voor de geselecteerde bestemming, op basis van ontbrekende kenmerken en schending van toestemming.

![Dataflow voert mening voor partijbestemmingen uit.](../assets/ui/monitor-destinations/dataflow-runs-batch.png)

Elke individuele dataflow run toont de volgende details:

- **[!UICONTROL Dataflow run start]**: De tijd waarop de dataflow is gestart.
- **[!UICONTROL Audience]**: De naam van het publiek dat aan elke dataflow-run is gekoppeld.
- **[!UICONTROL Processing time]**: De hoeveelheid tijd die het voor de dataflow in beslag nam om te worden verwerkt.
- **[!UICONTROL Profiles received]**: Het totale aantal profielen dat is ontvangen in de gegevensstroom. Deze waarde wordt elke 60 minuten bijgewerkt.
- **[!UICONTROL Identities activated]**: Het totale aantal profielidentiteiten dat met succes aan de geselecteerde bestemming als deel van dataflow looppas werd geactiveerd. Deze metrische waarde bevat identiteiten die zijn gemaakt, bijgewerkt en verwijderd uit geëxporteerde doelgroepen.
- **[!UICONTROL Identities excluded]**: Het totale aantal profiel-id&#39;s dat van activering is uitgesloten op basis van ontbrekende kenmerken en schending van de toestemming.
- **[!UICONTROL Status]**: Geeft de status aan waarin de gegevensstroom zich bevindt. Dit kan een van drie staten zijn: [!UICONTROL Success], [!UICONTROL Failed], en [!UICONTROL Processing]. [!UICONTROL Success] betekent dat de gegevensstroom actief is en gegevens volgens zijn verstrekt programma uitvoert. [!UICONTROL Failed] betekent dat de activering van gegevens is opgeschort als gevolg van fouten. [!UICONTROL Processing] betekent dat de gegevensstroom nog niet actief is en over het algemeen wordt ontmoet wanneer een nieuwe gegevensstroom wordt gecreeerd.

Om details van een specifieke dataflow looppas te bekijken, selecteer de begintijd van de looppas van de lijst.

>[!NOTE]
>
>De looppas van Dataflow wordt geproduceerd gebaseerd op de planningsfrequentie van bestemmingsdataflow. Er wordt een aparte dataflow-run uitgevoerd voor elk [samenvoegingsbeleid](../../profile/merge-policies/overview.md) toegepast op een publiek.

De detailspagina voor een dataflow, naast de details die op de dataflows lijst worden getoond, toont specifiekere informatie over dataflow:

- **[!UICONTROL Size of data]**: De grootte van de gegevensstroom die wordt geëxporteerd.
- **[!UICONTROL Total files]**: Het totale aantal bestanden dat in de gegevensstroom is geëxporteerd.
- **[!UICONTROL Last updated]**: De tijd de dataflow looppas werd laatst bijgewerkt.

![Dataflow-run-details voor batchdoelen.](../assets/ui/monitor-destinations/dataflow-batch.png)

Op de detailpagina wordt ook een lijst met mislukte identiteiten en identiteiten weergegeven die zijn uitgesloten. Er wordt informatie voor zowel de mislukte als de uitgesloten identiteiten weergegeven, inclusief de foutcode en beschrijving. Standaard worden in de lijst de mislukte identiteiten weergegeven. Als u uitgesloten identiteiten wilt weergeven, selecteert u de **[!UICONTROL Identities excluded]** schakelen.

![Dataflow-records voor batchbestemmingen met een foutbericht gemarkeerd.](../assets/ui/monitor-destinations/dataflow-records-batch.png)

## Het dashboard Bestemmingen controleren {#monitoring-destinations-dashboard}

>[!NOTE]
>
>- Functionaliteit voor het controleren van doelen wordt momenteel ondersteund voor alle doelen in Experience Platform *behalve* de [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) en [Aangepaste personalisatie](/help/destinations/catalog/personalization/custom-personalization.md) bestemmingen.
>- Voor de [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md), en [HTTP-API](/help/destinations/catalog/streaming/http-destination.md) doelen, de metriek met betrekking tot uitgesloten, mislukte en geactiveerde identiteiten worden geschat. Hogere volumes activeringsgegevens leiden tot een hogere nauwkeurigheid van de meetwaarden.

>[!CONTEXTUALHELP]
>id="platform_monitoring_activation"
>title="Activering"
>abstract="De weergave voor doelactivering bevat informatie over de activeringsstatus van een publiek en maatstaven die vanuit het realtime-klantprofiel zijn genomen om unieke identiteiten te genereren."

Als u toegang wilt krijgen tot [!UICONTROL Monitoring] dashboard, selecteren **[!UICONTROL Monitoring]** (![bewakingspictogram](../assets/ui/monitor-destinations/monitoring-icon.png)) in de linkernavigatie. Eén keer op de knop [!UICONTROL Monitoring] pagina, selecteert u [!UICONTROL Destinations]. De [!UICONTROL Monitoring] het dashboard bevat metriek en informatie over de banen van de bestemmingslooppas.

Gebruik de [!UICONTROL Destinations] dashboard voor een algemeen idee van de gezondheid van uw activeringsstromen. Begin door inzichten op een bijeengevoegd niveau voor alle partij en het stromen bestemmingen te krijgen en dan neer in gedetailleerde meningen voor dataflows, dataflow looppas, en geactiveerd publiek voor een diepgaande blik op uw activeringsgegevens te boren. De schermen in de [!UICONTROL Monitoring] het dashboard verstrekt actionable inzichten door metriek en foutenbeschrijvingen om u te helpen om het even welke problemen oplossen die zich in uw activeringsscenario&#39;s zouden kunnen voordoen.

U kunt de weergegeven informatie filteren op gegevenstype - klanten, accounts (alleen voor de Adobe Real-Time CDP B2B-editie), vooruitzichten en verrijking van accounts. Meer informatie over deze opties vindt u in het dialoogvenster [Dashboardgids controleren](/help/dataflows/ui/monitor.md#monitoring-dashboard-overview).

![Het filter van het gegevenstype dat in de controle dashboardmening wordt benadrukt.](/help/dataflows/assets/ui/monitor-destinations/add-data-filter.png)

In het midden van het dashboard bevindt zich de [!UICONTROL Activation] , die metriek en grafieken bevat die gegevens over het activeringstarief van de gegevens tonen die naar het stromen bestemmingen worden uitgevoerd, evenals op de ontbroken partij dataflow looppas aan partijbestemmingen.

![Grafieken voor streaming en batchactivering worden gemarkeerd in de monitoringweergave.](../assets/ui/monitor-destinations/dashboard-graph.png)


Standaard bevatten de weergegeven gegevens de activeringsgegevens van de laatste 24 uur. Selecteren **[!UICONTROL Last 24 hours]** om het tijdkader van getoonde verslagen aan te passen. Beschikbare opties zijn **[!UICONTROL Last 24 hours]**, **[!UICONTROL Last 7 days]**, en **[!UICONTROL Last 30 days]**. U kunt ook de datums in het pop-upvenster Kalender selecteren dat wordt weergegeven. Als u datums hebt geselecteerd, selecteert u **[!UICONTROL Apply]** om het tijdkader van de getoonde informatie aan te passen.

>[!NOTE]
>
>De volgende schermafbeelding toont de activeringsfrequentie en batch-gegevensstroom gedurende de laatste 30 dagen in plaats van de laatste 24 uur. U kunt het tijdkader aanpassen door **[!UICONTROL Last 30 days]**.

![De controle van de terugkijkdatumwaaier van de verandering benadrukte voor geactiveerde bestemmingen](../assets/ui/monitor-destinations/dashboard-graph-change-date-range.png)

Het pijlpictogram gebruiken (![pijlpictogram](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png)) om de kaarten boven aan het scherm uit te vouwen of te negeren, waarop in één oogopslag informatie over de activeringsdetails wordt weergegeven op basis van het doeltype, streaming of batch:

- **[!UICONTROL Streaming activation rate]**: Vertegenwoordigt het percentage ontvangen identiteiten dat met succes is geactiveerd of overgeslagen. De formule die voor de berekening van dit percentage wordt gebruikt, wordt hierboven op deze pagina nader beschreven in de [Dataflow wordt uitgevoerd voor streamingdoelen](#dataflow-runs-for-streaming-destinations) sectie.
- **[!UICONTROL Batch failed dataflow runs]**: Vertegenwoordigt het aantal mislukte dataflow looppas in het geselecteerde tijdinterval.

![Kaarten boven aan pagina weergeven of negeren.](../assets/ui/monitor-destinations/monitoring-destinations-toggle-arrow.gif)

De **[!UICONTROL Activation]** de grafiek wordt standaard weergegeven en u kunt deze uitschakelen om de onderstaande lijst met doelen uit te vouwen. Selecteer de **[!UICONTROL Metrics and graphs]** schakelen om de grafieken uit te schakelen.

De **[!UICONTROL Activation]** toont een lijst van bestemmingen die minstens één bestaand rekening bevatten. Deze lijst bevat ook informatie over de ontvangen profielen, de geactiveerde identiteiten, de mislukte identiteiten, uitgesloten identiteiten, het activeringspercentage, de totale mislukte gegevensstromen, en de laatste bijgewerkte datum voor deze bestemmingen. Niet zijn alle metriek beschikbaar voor alle bestemmingstypes. In de onderstaande tabel worden de beschikbare gegevens per doeltype, streaming of batch weergegeven.

| Metrisch | Doeltype |
---------|----------|
| **[!UICONTROL Profiles received]** | Streaming en batch |
| **[!UICONTROL Identities activated]** | Streaming en batch |
| **[!UICONTROL Identities failed]** | Streaming |
| **[!UICONTROL Identities excluded]** | Streaming en batch |
| **[!UICONTROL Activation rate]** | Streaming |
| **[!UICONTROL Total failed dataflows]** | Batch |
| **[!UICONTROL Last updated]** | Streaming en batch |

![Monitoren van dashboard met alle geactiveerde doelen gemarkeerd.](../assets/ui/monitor-destinations/dashboard-destinations.png)

U kunt uw lijst van bestemmingen ook filtreren om slechts de geselecteerde categorie van bestemmingen te tonen. Selecteer de **[!UICONTROL My destinations]** en selecteert u de [doelcategorie](/help/destinations/destination-types.md#categories) waarop u wilt filteren.

![Doelen filteren met vervolgkeuzekiezer](../assets/ui/monitor-destinations/dashboard-destinations-filter-dropdown.png)

Bovendien kunt u een bestemming in de onderzoeksbar ingaan om aan één enkele bestemming te isoleren. Als u de gegevens van de bestemming wilt zien, kunt u het filter selecteren ![filter](../assets/ui/monitor-destinations/filter-add.png) naast het om een lijst van zijn actieve dataflows te zien.

![De bestemmingen van de filter gebruikend de onderzoeksbar die in de controlemening wordt benadrukt.](../assets/ui/monitor-destinations/filtered-destinations.png)

Als u alle bestaande gegevensstromen over alle bestemmingen wilt bekijken, uitgezocht **[!UICONTROL Dataflows]**.

Er wordt een lijst met gegevensstromen weergegeven, gesorteerd op de laatste dataflow-run. U kunt extra details voor een specifieke gegevensstroom zien door de plaats van de bestemming te bepalen u wilt controleren, die de filter selecteren ![filter](../assets/ui/monitor-destinations/filter-add.png) naast het, en dan het selecteren van de filter ![filter](../assets/ui/monitor-destinations/filter-add.png) naast de gegevensstroom wilt u meer informatie over.

![Alle gegevensstromen die in het controledashboard worden benadrukt.](../assets/ui/monitor-destinations/dashboard-dataflows.png)

Zodra u een gegevensstroom voor verdere inspectie selecteert, bevat de dataflow detailspagina een knevel die u toestaat om de geactiveerde gegevens in dataflow te zien, die door dataflow looppas of publiek wordt verdeeld.

### Dataflow-run-weergave {#dataflow-runs-view}

Wanneer **[!UICONTROL Dataflow runs]** is geselecteerd, kunt u een lijst van dataflow looppas voor geselecteerde dataflow en verdere informatie over elke looppas zien.

>[!INFO]
>
>Voor gegevensstromen aan het stromen bestemmingen, wordt een dataflow looppas verdeeld in uurvensters. Elk uurvenster produceert een overeenkomstige dataflow looppas identiteitskaart
>
>Voor dataflows aan partijbestemmingen, heeft elk publiek een overeenkomstige dataflow die looppas wordt geproduceerd, op de publiekactivering geplande frequentie wordt gebaseerd. Bijvoorbeeld, als u opstelling een dagelijkse geplande activering voor vijf publiek in de zelfde bestemmingsdataflow, er vijf afzonderlijke dataflow looppas zal zijn die elke dag wordt geproduceerd.

![Het deelvenster Dataflow wordt uitgevoerd en er zijn verschillende runtimes gemarkeerd.](../assets/ui/monitor-destinations/dashboard-flow-runs-view.png)

Gebruik de **[!UICONTROL Show failures only]** schakelen om alleen de mislukte uitvoering voor een gegevensstroom weer te geven.

![Dataflow voert mening met slechts benadrukt tonen mislukte knevel uit](../assets/ui/monitor-destinations/dataflow-runs-show-failures-only.gif)

### Weergave op publiek niveau {#segment-level-view}

Wanneer **[!UICONTROL Audiences]** is geselecteerd, wordt er een lijst weergegeven met de soorten publiek die binnen het geselecteerde tijdbereik zijn geactiveerd voor de geselecteerde gegevensstroom. Dit scherm bevat publieksinformatie over de geactiveerde identiteiten, uitgesloten identiteiten, evenals de status en de tijd van de laatste dataflow-run. Door de metriek voor uitgesloten en geactiveerde identiteiten te bekijken, kunt u verifiëren of een publiek met succes is geactiveerd of niet.

U activeert bijvoorbeeld een publiek met de naam &#39;Loyalty Member States in California&#39; naar een Amazon S3-bestemming &#39;Loyalty Member California December&#39;. Laten we aannemen dat er 100 profielen in het geselecteerde publiek zijn, maar dat slechts 80 van de 100 profielen Loyalty-id-kenmerken bevatten en u de regels voor exporttoewijzingen hebt gedefinieerd als `loyalty.id` is vereist. In dit geval wordt voor het publiek 80 identiteiten geactiveerd en 20 identiteiten uitgesloten.

>[!IMPORTANT]
>
>Neem nota van de huidige beperkingen met betrekking tot publiek-vlakke metriek:
>- De publiek-vlakke mening is momenteel slechts beschikbaar voor partijbestemmingen.
>- De publiek-vlakke metriek wordt momenteel geregistreerd voor succesvolle dataflow looppas slechts. Zij worden niet geregistreerd voor ontbroken dataflow looppas en uitgesloten verslagen.

![Soorten publiek gemarkeerd in het deelvenster Gegevensstroom.](../assets/ui/monitor-destinations/dashboard-segments-view.png)

In de publiek-vlakke mening, worden de metriek bijeengevoegd over veelvoudige dataflow looppas binnen de geselecteerde tijdwaaier. Als er veelvoudige dataflow looppas zijn, kunt u neer van het publieksniveau boren om de uitsplitsing voor elke dataflow looppas te zien, die door het geselecteerde publiek wordt gefiltreerd.
De filterknop gebruiken ![filter](../assets/ui/monitor-destinations/filter-add.png) om naar beneden in de dataflow looppas mening voor elk publiek in dataflow te boren.

### DataFlow-uitvoerpagina {#dataflow-runs-page}

De pagina met gegevensstroomuitvoering bevat informatie over de gegevensstroomuitvoering, zoals de begintijd van de gegevensstroom, de verwerkingstijd, ontvangen profielen, geactiveerde identiteiten, uitgesloten identiteiten, mislukte identiteiten, activeringsfrequentie en status.

Wanneer u naar beneden boort in dataflow stelt pagina van [weergave op publieksniveau](#segment-level-view), hebt u de optie om de dataflow looppas door de volgende opties te filtreren:

- **[!UICONTROL Dataflow runs with failed identities]**: Voor het geselecteerde publiek worden met deze optie alle gegevensstroombewerkingen weergegeven die zijn mislukt voor activering. Om te inspecteren waarom identiteiten in een bepaalde dataflow run ontbraken, zie [detailpagina voor gegevensstroom](#dataflow-run-details-page) voor die dataflow run.
- **[!UICONTROL Dataflow runs with skipped identities]**: Voor het geselecteerde publiek worden met deze optie alle dataflow-run weergegeven waarvoor sommige identiteiten niet volledig zijn geactiveerd en bepaalde profielen zijn overgeslagen. Om te inspecteren waarom identiteiten in een bepaalde dataflow looppas werden overgeslagen, zie [detailpagina voor gegevensstroom](#dataflow-run-details-page) voor die dataflow run.
- **[!UICONTROL Dataflow runs with activated identities]**: Voor het geselecteerde publiek worden met deze optie alle dataflow-uitvoering weergegeven die identiteiten hebben die zijn geactiveerd.

![Keuzerondjes die tonen hoe te om dataflow looppas voor publiek te filtreren.](/help/dataflows/assets/ui/monitor-destinations/dataflow-runs-segment-filter.png)

Als u meer details wilt zien over een specifieke gegevensstroomuitvoering, selecteert u het filter ![filter](../assets/ui/monitor-destinations/filter-add.png) naast de dataflow run start time om de dataflow run details page te zien.

![Dataflow voert filter in controle dashboard uit om in meer informatie voor een bepaalde dataflow looppas te boor.](../assets/ui/monitor-destinations/dataflow-runs-filter.png)

### Detailpagina voor gegevensstroom {#dataflow-run-details-page}

De dataflow looppas detailpagina, naast de details die op de dataflow looppas lijst worden getoond, toont specifiekere informatie over dataflow:

- **[!UICONTROL Dataflow run ID]**: De id van de gegevensstroom.
- **[!UICONTROL IMS org ID]**: De organisatie waartoe de gegevensstroom behoort.
- **[!UICONTROL Last updated]**: De tijd de dataflow looppas werd laatst bijgewerkt.

De detailspagina heeft ook een knevel om tussen dataflow loopfouten en publiek te schakelen. Deze optie is slechts beschikbaar voor dataflow looppas in partijbestemmingen.

In de weergave met uitvoerfouten in de gegevensstroom wordt een lijst weergegeven met mislukte identiteiten en identiteiten die zijn uitgesloten. De informatie voor zowel de mislukte als uitgesloten identiteiten wordt getoond, met inbegrip van de foutencode, het aantal van de identiteit, en beschrijving. Standaard worden in de lijst de mislukte identiteiten weergegeven. Als u overgeslagen identiteiten wilt weergeven, selecteert u de optie **[!UICONTROL Identities excluded]** schakelen.

![In de monitoringweergave gemarkeerde identiteiten uitgesloten van schakeloptie](../assets/ui/monitor-destinations/identities-excluded.png)

Wanneer **[!UICONTROL Audiences]** wordt geselecteerd, ziet u een lijst van de soorten publiek die in de geselecteerde dataflow looppas werden geactiveerd. Dit scherm bevat publieksinformatie over de geactiveerde identiteiten, uitgesloten identiteiten, evenals de status en de tijd van de laatste dataflow-run.

![De mening van het publiek in het dataflow looppas detailscherm.](../assets/ui/monitor-destinations/dataflow-run-segments-view.png)

## Volgende stappen {#next-steps}

Door deze gids te volgen, weet u nu hoe te om dataflows voor zowel partij als het stromen bestemmingen, met inbegrip van alle relevante informatie zoals verwerkingstijd, activeringstarief, en status te controleren. Als u meer wilt weten over gegevensstromen in Platform, leest u de [gegevensstroomoverzicht](../home.md). Voor meer informatie over bestemmingen leest u de [Overzicht van doelen](../../destinations/home.md).