---
keywords: Experience Platform;thuis;populaire onderwerpen;monitorrekeningen;monitordataflows;dataflows;bestemmingen
description: Met doelen kunt u uw gegevens activeren van Adobe Experience Platform naar talloze externe partners. Dit leerprogramma verstrekt instructies op hoe u dataflows voor uw bestemmingen kunt controleren gebruikend het gebruikersinterface van het Experience Platform.
solution: Experience Platform
title: Dataflows voor Doelen in UI controleren
topic-legacy: overview
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
source-git-commit: 042a739593b291cdd7193437906a16dc889a3b4b
workflow-type: tm+mt
source-wordcount: '3193'
ht-degree: 0%

---

# Dataflows voor doelen in de UI controleren

Met doelen kunt u uw gegevens activeren van Adobe Experience Platform naar talloze externe partners. Platform maakt het proces om de stroom van gegevens aan uw bestemmingen gemakkelijker te volgen door transparantie van gegevensstromen te verstrekken.

Het controledashboard voorziet u van een visuele vertegenwoordiging van de reis van een gegevensstroom, met inbegrip van de bestemming de gegevens worden geactiveerd aan. Dit leerprogramma verstrekt instructies op hoe u of dataflows direct in de bestemmingswerkruimte kunt controleren of het controledashboard gebruiken om dataflows voor uw bestemmingen te controleren gebruikend het gebruikersinterface van het Experience Platform.

## Aan de slag {#getting-started}

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [Gegevensstromen](../home.md): Dataflows zijn een voorstelling van gegevenstaken die gegevens over het Platform verplaatsen. Dataflows worden gevormd over verschillende diensten, die gegevens van bronschakelaars aan doeldatasets helpen bewegen, aan [!DNL Identity] en [!DNL Profile]en [!DNL Destinations].
   - [Dataflow-uitvoering](../../sources/notifications.md): De looppas van Dataflow is de terugkomende geplande banen die op de frequentieconfiguratie van geselecteerde dataflows worden gebaseerd.
- [Doelen](../../destinations/home.md): Doelen zijn voorgebouwde integraties met veelgebruikte toepassingen die het mogelijk maken om gegevens van Platform naadloos te activeren voor kanaalmarketingcampagnes, e-mailcampagnes, gerichte reclame en vele andere gebruiksgevallen.
- [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## Gegevens controleren in de werkruimte Doelen {#monitor-dataflows-in-the-destinations-workspace}

In de **[!UICONTROL Destinations]** binnen de gebruikersinterface van het Platform navigeert u naar de **[!UICONTROL Browse]** en selecteert u de naam van een doel dat u wilt weergeven.

![Doelweergave selecteren](../assets/ui/monitor-destinations/select-destination.png)

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
>title="Gegevens gegevensstroom"
>abstract="De gegevens van de bestemmingdataflow looppas bevatten informatie over de activeringsstatus van het segment en metriek die van het Profiel van de Klant in real time wordt genomen om unieke identiteiten te produceren. Voor meer informatie raadpleegt u de handleiding voor metrische definities."

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_streaming"
>title="Ontvangen profielen"
>abstract="Het totale aantal profielen dat is ontvangen in de gegevensstroom. Deze waarde wordt elke 60 minuten bijgewerkt."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_streaming"
>title="Geactiveerde identiteiten"
>abstract="Het aantal afzonderlijke profiel-id&#39;s dat is geactiveerd voor het geselecteerde doel. Deze metrische waarde bevat identiteiten die zijn gemaakt, bijgewerkt en verwijderd uit geëxporteerde segmenten."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_streaming"
>title="Uitgesloten identiteiten"
>abstract="Het aantal afzonderlijke profielrecords dat is uitgesloten van activering voor de geselecteerde bestemming op basis van ontbrekende kenmerken en schending van de toestemming."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesfailed_streaming"
>title="Identiteiten mislukt"
>abstract="Het aantal afzonderlijke profiel-id&#39;s dat is mislukt voor het geselecteerde doel. Controleer de foutdiagnostiek voor meer informatie."
>text="Learn more in documentation"

Voor streamingdoelen geldt het [!UICONTROL Dataflow runs] bevat een update per uur voor metrische gegevens in uw gegevensstroomuitvoering. De meest prominente statistieken met het label zijn voor identiteiten.

De identiteiten vertegenwoordigen de verschillende facetten van een profiel. Als een profiel bijvoorbeeld zowel een telefoonnummer als een e-mailadres bevat, heeft dat profiel twee identiteiten.

Er wordt een lijst met afzonderlijke reeksen en de bijbehorende maatstaven weergegeven, samen met de volgende totalen voor identiteiten:

- **[!UICONTROL Identities activated]**: Het totale aantal profielidentiteiten dat met succes aan de geselecteerde bestemming wordt geactiveerd. Deze metrische waarde bevat identiteiten die zijn gemaakt, bijgewerkt en verwijderd uit geëxporteerde segmenten.
- **[!UICONTROL Identities excluded]**: Het totale aantal profielidentiteiten dat voor activering wordt overgeslagen op basis van ontbrekende kenmerken en schending van de toestemming.
- **[!UICONTROL Identities failed]**: Het totale aantal profielidentiteiten dat niet aan de bestemming wegens fouten wordt geactiveerd.

![Dataflow voert details voor het stromen bestemmingen uit](../assets/ui/monitor-destinations/dataflow-runs-stream.png)

Elke individuele dataflow run toont de volgende details:

- **[!UICONTROL Dataflow run start]**: De tijd dat dataflow begon bij. Voor het stromen dataflow looppas, vangt het Experience Platform metriek op het begin van dataflow looppas, in de vorm van uurmetriek wordt gebaseerd. Voor het stromen dataflow looppas, als een dataflow looppas bijvoorbeeld bij 10:30PM begon, toont metrisch de begintijd zoals 10:00 PM in UI.
- **[!UICONTROL Processing time]**: De hoeveelheid tijd die het voor dataflow nam in werking te stellen proces.
   - Voor **[!UICONTROL completed]** De metrische verwerkingstijd toont altijd één uur.
   - Voor dataflow-run die zich nog steeds in een **[!UICONTROL processing]** staat, het venster om alle metriek te vangen open meer dan een uur, om alle metriek te verwerken die aan de dataflow looppas beantwoorden. Bijvoorbeeld, zou een dataflow looppas die bij 9:30 AM begon in een verwerkingsstaat één uur en dertig minuten kunnen blijven om alle metriek te vangen en te verwerken. Vervolgens wordt het verwerkingsvenster gesloten en wordt de status van de dataflow-run bijgewerkt naar **voltooid**, wordt de weergegeven verwerkingstijd gewijzigd in één uur.
- **[!UICONTROL Profiles received]**: Het totale aantal profielen dat is ontvangen in de gegevensstroom.
- **[!UICONTROL Identities activated]**: Het totale aantal profielidentiteiten die met succes aan de geselecteerde bestemming als deel van dataflow looppas werden geactiveerd. Deze metrische waarde bevat identiteiten die zijn gemaakt, bijgewerkt en verwijderd uit geëxporteerde segmenten.
- **[!UICONTROL Identities excluded]**: Het totale aantal profiel-id&#39;s dat van activering is uitgesloten op basis van ontbrekende kenmerken en schending van de toestemming.
- **[!UICONTROL Identities failed]** Het totale aantal profielidentiteiten dat niet aan de bestemming wegens fouten wordt geactiveerd.
- **[!UICONTROL Activation rate]**: Het percentage ontvangen identiteiten dat is geactiveerd of overgeslagen. De volgende formule laat zien hoe deze waarde wordt berekend:
   ![Activeringssnelheidsformule](../assets/ui/monitor-destinations/activation-rate-formula.png)
- **[!UICONTROL Status]**: Vertegenwoordigt de staat de dataflow is in: ofwel [!UICONTROL Completed] of [!UICONTROL Processing]. [!UICONTROL Completed] betekent dat alle identiteiten voor de overeenkomstige dataflow run binnen de periode van één uur werden uitgevoerd. [!UICONTROL Processing] betekent dat de dataflow run nog niet is voltooid.

Om de details van een bepaalde dataflow looppas te bekijken, selecteer de begintijd van de looppas van de lijst.

De detailpagina voor een dataflow-run bevat aanvullende informatie zoals het aantal ontvangen profielen, het aantal geactiveerde identiteiten, het aantal mislukte identiteiten en het aantal uitgesloten identiteiten.

![Gegevens over gegevensstroom voor streamingdoelen](../assets/ui/monitor-destinations/dataflow-details-stream.png)

Op de detailpagina wordt ook een lijst met mislukte identiteiten en identiteiten weergegeven die zijn uitgesloten. De informatie voor zowel de mislukte als uitgesloten identiteiten wordt getoond, met inbegrip van de foutencode, het aantal van de identiteit, en beschrijving. Standaard worden in de lijst de mislukte identiteiten weergegeven. Als u overgeslagen identiteiten wilt weergeven, selecteert u de optie **[!UICONTROL Identities excluded]** schakelen.

![Dataflow-records voor streamingdoelen](../assets/ui/monitor-destinations/dataflow-records-stream.png)

### Dataflow wordt uitgevoerd voor batchdoelen {#dataflow-runs-for-batch-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation"
>title="Gegevens gegevensstroom"
>abstract="De gegevens van de bestemmingdataflow looppas bevatten informatie over de activeringsstatus van het segment en metriek die van het Profiel van de Klant in real time wordt genomen om unieke identiteiten te produceren. Voor meer informatie raadpleegt u de handleiding voor metrische definities."

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation_batch"
>title="Gegevens gegevensstroom"
>abstract="De gegevens van de bestemmingdataflow looppas bevatten informatie over de activeringsstatus van het segment en metriek die van het Profiel van de Klant in real time wordt genomen om unieke identiteiten te produceren. Voor meer informatie raadpleegt u de handleiding voor metrische definities."

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_batch"
>title="Ontvangen profielen"
>abstract="Het totale aantal profielen dat is ontvangen in de gegevensstroom. Deze waarde wordt elke 60 minuten bijgewerkt."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_batch"
>title="Geactiveerde identiteiten"
>abstract="Het aantal afzonderlijke profiel-id&#39;s dat is geactiveerd voor het geselecteerde doel. Deze metrische waarde bevat identiteiten die zijn gemaakt, bijgewerkt en verwijderd uit geëxporteerde segmenten."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_batch"
>title="Uitgesloten identiteiten"
>abstract="Het aantal afzonderlijke profielrecords dat is uitgesloten van activering voor de geselecteerde bestemming op basis van ontbrekende kenmerken en schending van de toestemming."
>text="Learn more in documentation"

Voor batchbestemmingen wordt de [!UICONTROL Dataflow runs] bevat metrische gegevens over de gegevensstroomuitvoering. Er wordt een lijst met afzonderlijke reeksen en de bijbehorende maatstaven weergegeven, samen met de volgende totalen voor identiteiten:

- **[!UICONTROL Identities activated]**: Het totale aantal profielidentiteiten dat met succes aan de geselecteerde bestemming wordt geactiveerd. Deze metrische waarde bevat identiteiten die zijn gemaakt, bijgewerkt en verwijderd uit geëxporteerde segmenten.
- **[!UICONTROL Identities excluded]**: Het aantal individuele profielidentiteiten die van activering voor de geselecteerde bestemming worden uitgesloten, op basis van ontbrekende attributen en schending van de toestemming.

![Dataflow wordt weergegeven als batchdoelen](../assets/ui/monitor-destinations/dataflow-runs-batch.png)

Elke individuele dataflow run toont de volgende details:

- **[!UICONTROL Dataflow run start]**: De tijd dat dataflow begon bij.
- **[!UICONTROL Processing time]**: De hoeveelheid tijd het voor dataflow nam om te worden verwerkt.
- **[!UICONTROL Profiles received]**: Het totale aantal profielen dat is ontvangen in de gegevensstroom. Deze waarde wordt elke 60 minuten bijgewerkt.
- **[!UICONTROL Identities activated]**: Het totale aantal profielidentiteiten die met succes aan de geselecteerde bestemming als deel van dataflow looppas werden geactiveerd. Deze metrische waarde bevat identiteiten die zijn gemaakt, bijgewerkt en verwijderd uit geëxporteerde segmenten.
- **[!UICONTROL Identities excluded]**: Het totale aantal profiel-id&#39;s dat van activering is uitgesloten op basis van ontbrekende kenmerken en schending van de toestemming.
- **[!UICONTROL Status]**: Geeft de status aan waarin de gegevensstroom zich bevindt. Dit kan een van drie staten zijn: [!UICONTROL Success], [!UICONTROL Failed], en [!UICONTROL Processing]. [!UICONTROL Success] betekent dat de gegevensstroom actief is en gegevens volgens zijn verstrekt programma uitvoert. [!UICONTROL Failed] betekent dat de activering van gegevens is opgeschort als gevolg van fouten. [!UICONTROL Processing] betekent dat de gegevensstroom nog niet actief is en over het algemeen wordt ontmoet wanneer een nieuwe gegevensstroom wordt gecreeerd.

Om details van een specifieke dataflow looppas te bekijken, selecteer de begintijd van de looppas van de lijst.

>[!NOTE]
>
>De looppas van Dataflow wordt geproduceerd gebaseerd op de planningsfrequentie van bestemmingsdataflow. Er wordt een aparte dataflow-run uitgevoerd voor elk [samenvoegingsbeleid](../../profile/merge-policies/overview.md) toegepast op een segment.

De detailspagina voor een dataflow, naast de details die op de dataflows lijst worden getoond, toont specifiekere informatie over dataflow:

- **[!UICONTROL Size of data]**: De grootte van de gegevensstroom die wordt geëxporteerd.
- **[!UICONTROL Total files]**: Het totale aantal bestanden dat in de gegevensstroom is geëxporteerd.
- **[!UICONTROL Last updated]**: De tijd de dataflow looppas werd laatst bijgewerkt.

![Gegevens voor gegevensstroom uitvoeren voor batchdoelen](../assets/ui/monitor-destinations/dataflow-batch.png)

Op de detailpagina wordt ook een lijst met mislukte identiteiten en identiteiten weergegeven die zijn uitgesloten. Er wordt informatie voor zowel de mislukte als de uitgesloten identiteiten weergegeven, inclusief de foutcode en beschrijving. Standaard worden in de lijst de mislukte identiteiten weergegeven. Als u uitgesloten identiteiten wilt weergeven, selecteert u de optie **[!UICONTROL Identities excluded]** schakelen.

![Dataflow-records voor batchdoelen](../assets/ui/monitor-destinations/dataflow-records-batch.png)

## Het dashboard voor segmenttaken controleren {#monitoring-segment-jobs-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segment_jobs"
>title="Segmenttaken"
>abstract="De mening van segmentbanen bevat informatie over de evaluatie en de uitvoerbanen voor al uw segmenten."

Om toegang te krijgen tot [!UICONTROL Segment Jobs] dashboard, selecteren **[!UICONTROL Monitoring]** (![bewakingspictogram](../assets/ui/monitor-destinations/monitoring-icon.png)) in de linkernavigatie. Eén keer op de knop [!UICONTROL Monitoring] pagina, selecteert u [!UICONTROL Segment Jobs]. De [!UICONTROL Monitoring] het dashboard bevat metriek en informatie over de segmentevaluatie en de uitvoerbanen.

![Dashboard voor bewaking van segmenttaken](../assets/ui/monitor-destinations/dashboard-segment-jobs.png)

Gebruik de [!UICONTROL Segment Jobs] dashboard om te begrijpen als de profielevaluatie en de uitvoer op tijd en zonder enige uitzonderingen gebeurt, zodat kunnen de stroomafwaartse diensten voor bestemmingsactivering de recentste geëvalueerde profielgegevens hebben.

De volgende metriek is beschikbaar voor segmentbanen:

| Metrisch | Beschrijving |
---------|----------|
| **[!UICONTROL Segment job]** | Geeft de naam van de segmenttaak aan. |
| **[!UICONTROL Type]** | Geeft het type segmenttaak aan: exporteren of evalueren. Merk op dat in beide gevallen de segmentbaan evalueert of uitvoert *alles* segmenten die tot een organisatie behoren. |
| **[!UICONTROL Job start]** | De datum en tijd waarop de segmenttaak is gestart. |
| **[!UICONTROL Job end]** | De datum en de tijd toen de segmentbaan voltooide. |
| **[!UICONTROL Status]** | De status van de voltooide taak - geslaagd of mislukt. |

## Het dashboard Bestemmingen controleren {#monitoring-destinations-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_activation"
>title="Activering"
>abstract="De weergave voor doelactivering bevat informatie over de activeringsstatus van het segment en de maatstaven die vanuit het realtime profiel van de klant zijn genomen om unieke identiteiten te genereren."

Om toegang te krijgen tot [!UICONTROL Monitoring] dashboard, selecteren **[!UICONTROL Monitoring]** (![bewakingspictogram](../assets/ui/monitor-destinations/monitoring-icon.png)) in de linkernavigatie. Eén keer op de knop [!UICONTROL Monitoring] pagina, selecteert u [!UICONTROL Destinations]. De [!UICONTROL Monitoring] het dashboard bevat metriek en informatie over de banen van de bestemmingslooppas.

Gebruik de [!UICONTROL Destinations] dashboard voor een algemeen idee van de gezondheid van uw activeringsstromen. Begin door inzichten op een bijeengevoegd niveau voor alle partij en het stromen bestemmingen te krijgen en dan neer te boor in gedetailleerde meningen voor dataflows, dataflow looppas, en geactiveerde segmenten voor een diepgaande blik op uw activeringsgegevens. De schermen in de [!UICONTROL Monitoring] het dashboard verstrekt actionable inzichten door metriek en foutenbeschrijvingen om u te helpen om het even welke problemen oplossen die zich in uw activeringsscenario&#39;s zouden kunnen voordoen.

In het midden van het dashboard bevindt zich de [!UICONTROL Activation] , die metriek en grafieken bevat die gegevens over het activeringstarief van de gegevens tonen die naar het stromen bestemmingen worden uitgevoerd, evenals op de ontbroken partij dataflow looppas aan partijbestemmingen.

![Grafieken voor streaming en batchactivering](../assets/ui/monitor-destinations/dashboard-graph.png)


Standaard bevatten de weergegeven gegevens de activeringsgegevens van de laatste 24 uur. Selecteren **[!UICONTROL Last 24 hours]** om het tijdkader van getoonde verslagen aan te passen. Beschikbare opties zijn **[!UICONTROL Last 24 hours]**, **[!UICONTROL Last 7 days]**, en **[!UICONTROL Last 30 days]**. U kunt ook de datums in het pop-upvenster Kalender selecteren dat wordt weergegeven. Als u datums hebt geselecteerd, selecteert u **[!UICONTROL Apply]** om het tijdkader van de getoonde informatie aan te passen.

>[!NOTE]
>
>De volgende schermafbeelding toont de activeringsfrequentie en batch-gegevensstroom gedurende de laatste 30 dagen in plaats van de laatste 24 uur. U kunt het tijdkader aanpassen door **[!UICONTROL Last 30 days]**.

![De waaier van de raadplegingsdatum van de verandering voor geactiveerde bestemmingen](../assets/ui/monitor-destinations/dashboard-graph-change-date-range.png)

Het pijlpictogram gebruiken (![pijlpictogram](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png)) om de kaarten boven aan het scherm uit te vouwen of te negeren, die in één oogopslag informatie over de activeringsdetails weergeven, gebaseerd op het doeltype, streaming of batch:

- **[!UICONTROL Streaming activation rate]**: Vertegenwoordigt het percentage ontvangen identiteiten die met succes of overgeslagen zijn geactiveerd. De formule die voor de berekening van dit percentage wordt gebruikt, wordt hierboven nader beschreven in de [Dataflow wordt uitgevoerd voor streamingdoelen](#dataflow-runs-for-streaming-destinations) sectie.
- **[!UICONTROL Batch failed dataflow runs]**: Geeft het aantal mislukte dataflow looppas in het geselecteerde tijdinterval aan.

![Kaarten boven aan pagina weergeven of negeren](../assets/ui/monitor-destinations/monitoring-destinations-toggle-arrow.gif)

De **[!UICONTROL Activation]** de grafiek wordt standaard weergegeven en u kunt deze uitschakelen om de onderstaande lijst met doelen uit te vouwen. Selecteer **[!UICONTROL Metrics and graphs]** schakelen om de grafieken uit te schakelen.

De **[!UICONTROL Activation]** toont een lijst van bestemmingen die minstens één bestaand rekening bevatten. Deze lijst bevat ook informatie over de ontvangen profielen, de geactiveerde identiteiten, de mislukte identiteiten, uitgesloten identiteiten, het activeringspercentage, de totale mislukte gegevensstromen, en de laatste bijgewerkte datum voor deze bestemmingen. Niet zijn alle metriek beschikbaar voor alle bestemmingstypes. In de onderstaande tabel wordt aangegeven welke meetgegevens beschikbaar zijn per doeltype, streaming of batch.

| Metrisch | Doeltype |
---------|----------|
| **[!UICONTROL Profiles received]** | Streaming en batch |
| **[!UICONTROL Identities activated]** | Streaming en batch |
| **[!UICONTROL Identities failed]** | Streaming |
| **[!UICONTROL Identities excluded]** | Streaming en batch |
| **[!UICONTROL Activation rate]** | Streaming |
| **[!UICONTROL Total failed dataflows]** | Batch |
| **[!UICONTROL Last updated]** | Streaming en batch |

![Dashboard alle geactiveerde doelen](../assets/ui/monitor-destinations/dashboard-destinations.png)

U kunt uw lijst van bestemmingen ook filtreren om slechts de geselecteerde categorie van bestemmingen te tonen. Selecteer **[!UICONTROL My destinations]** en selecteert u de [doelcategorie](/help/destinations/destination-types.md#categories) waarop u wilt filteren.

![Doelen filteren met vervolgkeuzekiezer](../assets/ui/monitor-destinations/dashboard-destinations-filter-dropdown.png)

Bovendien kunt u een bestemming in de onderzoeksbar ingaan om aan één enkele bestemming te isoleren. Als u de gegevens van de bestemming wilt zien, kunt u het filter selecteren ![filter](../assets/ui/monitor-destinations/filter-add.png) naast het om een lijst van zijn actieve dataflows te zien.

![Doelen filteren met zoekbalk](../assets/ui/monitor-destinations/filtered-destinations.png)

Als u alle bestaande gegevensstromen over alle bestemmingen wilt bekijken, uitgezocht **[!UICONTROL Dataflows]**.

Er wordt een lijst met gegevensstromen weergegeven, gesorteerd op de laatste gegevensstroomuitvoering. U kunt extra details voor een specifieke gegevensstroom zien door de plaats van de bestemming te bepalen u wilt controleren, die de filter selecteren ![filter](../assets/ui/monitor-destinations/filter-add.png) naast het, en dan het selecteren van de filter ![filter](../assets/ui/monitor-destinations/filter-add.png) naast de gegevensstroom wilt u meer informatie over.

![Alle gegevensstromen die in het controledashboard worden benadrukt](../assets/ui/monitor-destinations/dashboard-dataflows.png)

Zodra u een gegevensstroom voor verdere inspectie selecteert, bevat de dataflow detailspagina een knevel die u toestaat om de geactiveerde gegevens in dataflow te zien, die door dataflow looppas of segmenten wordt verdeeld.

### Dataflow-runweergave {#dataflow-runs-view}

Wanneer **[!UICONTROL Dataflow runs]** is geselecteerd, kunt u een lijst van dataflow looppas voor geselecteerde dataflow en verdere informatie over elke looppas zien.

>[!INFO]
>
>Voor gegevensstromen aan het stromen bestemmingen, wordt een dataflow looppas verdeeld in uurvensters. Elk uurvenster produceert een overeenkomstige dataflow-run-id.
>
>Voor dataflows aan partijbestemmingen, heeft elk segment een overeenkomstige dataflow geproduceerde looppas, die op de segmentactivering wordt gebaseerd geplande frequentie. Bijvoorbeeld, als u opstelling een dagelijkse geplande activering voor vijf segmenten in de zelfde bestemmingsdataflow, er vijf afzonderlijke dataflow looppas zal zijn die elke dag wordt geproduceerd.

![Deelvenster Stroomuitvoering](../assets/ui/monitor-destinations/dashboard-flow-runs-view.png)

Gebruik de **[!UICONTROL Show failures only]** schakelt u om alleen de mislukte uitvoering voor een gegevensstroom weer te geven.

![Dataflow wordt uitgevoerd - alleen tonen van mislukkingen schakelen](../assets/ui/monitor-destinations/dataflow-runs-show-failures-only.gif)

### Weergave op segmentniveau {#segment-level-view}

Wanneer **[!UICONTROL Segments]** wordt geselecteerd, ziet u een lijst van de segmenten die aan de geselecteerde gegevensstroom, binnen de geselecteerde tijdwaaier werden geactiveerd. Dit scherm bevat op segmentniveau informatie over de geactiveerde identiteiten, de uitgesloten identiteiten, evenals de status en de tijd van de laatste dataflow-run. Door de metriek voor uitgesloten en geactiveerde identiteiten te herzien, kunt u verifiëren of een segment met succes is geactiveerd of niet.

Bijvoorbeeld, activeert u een segment genoemd &quot;Loyalty Leden in Californië&quot;aan een bestemming van Amazon S3 &quot;Loyalty Leden California December&quot;. Laten we ervan uitgaan dat het geselecteerde segment 100 profielen bevat, maar dat slechts 80 van de 100 profielen Loyalty-id-kenmerken bevatten en u de regels voor exporttoewijzingen hebt gedefinieerd als `loyalty.id` is vereist. In dit geval wordt op segmentniveau 80 identiteiten geactiveerd en worden 20 identiteiten uitgesloten.

>[!IMPORTANT]
>
>Neem nota van de huidige beperkingen met betrekking tot segment-vlakke metriek:
>- De segment-vlakke mening is momenteel slechts beschikbaar voor partijbestemmingen.
>- De het niveaumetriek van het segment wordt momenteel geregistreerd voor succesvolle dataflow looppas slechts. Zij worden niet geregistreerd voor ontbroken dataflow looppas en uitgesloten verslagen.


![Segmenten in deelvenster met gegevensstroom](../assets/ui/monitor-destinations/dashboard-segments-view.png)

In de segment-vlakke mening, worden de metriek bijeengevoegd over veelvoudige dataflow looppas binnen de geselecteerde tijdwaaier. Als er veelvoudige dataflow looppas zijn, kunt u neer van het segmentniveau boren om de mislukking voor elke dataflow looppas te zien, die door het geselecteerde segment wordt gefiltreerd.
De filterknop gebruiken ![filter](../assets/ui/monitor-destinations/filter-add.png) om neer in de dataflow looppas mening voor elk segment in dataflow te boren.

### DataFlow-uitvoerpagina {#dataflow-runs-page}

De pagina met gegevensstroomuitvoering bevat informatie over de gegevensstroomuitvoering, zoals de begintijd van de gegevensstroom, de verwerkingstijd, ontvangen profielen, geactiveerde identiteiten, uitgesloten identiteiten, mislukte identiteiten, activeringsfrequentie en status.

Wanneer u naar beneden boort in dataflow stelt pagina van [segmentweergave](#segment-level-view), hebt u de optie om de dataflow looppas door de volgende opties te filtreren:

- **[!UICONTROL Dataflow runs with failed identities]**: Voor het geselecteerde segment, maakt deze optie een lijst van alle dataflow looppas die voor activering ontbrak. Om te inspecteren waarom identiteiten in een bepaalde dataflow run ontbraken, zie [detailpagina voor gegevensstroom](#dataflow-run-details-page) voor die dataflow run.
- **[!UICONTROL Dataflow runs with skipped identities]**: Voor het geselecteerde segment, maakt deze optie een lijst van alle dataflow looppas waar sommige identiteiten niet volledig werden geactiveerd en sommige profielen werden overgeslagen. Om te inspecteren waarom identiteiten in een bepaalde dataflow looppas werden overgeslagen, zie [detailpagina voor gegevensstroom](#dataflow-run-details-page) voor die dataflow run.
- **[!UICONTROL Dataflow runs with activated identities]**: Voor het geselecteerde segment, maakt deze optie een lijst van alle dataflow looppas die identiteiten hebben die met succes werden geactiveerd.

![Dataflow-runnen filteren voor segmenten](/help/dataflows/assets/ui/monitor-destinations/dataflow-runs-segment-filter.png)

Als u meer details wilt zien over een specifieke gegevensstroomuitvoering, selecteert u het filter ![filter](../assets/ui/monitor-destinations/filter-add.png) naast de dataflow run start time om de dataflow run details page te zien.

![Dataflow voert filter uit in het dashboard voor controle](../assets/ui/monitor-destinations/dataflow-runs-filter.png)

### Detailpagina voor gegevensstroom {#dataflow-run-details-page}

De dataflow looppas detailpagina, naast de details die op de dataflow looppas lijst worden getoond, toont specifiekere informatie over dataflow:

- **[!UICONTROL Dataflow run ID]**: De id van de gegevensstroom.
- **[!UICONTROL IMS org ID]**: De IMS-organisatie waartoe de gegevensstroom behoort.
- **[!UICONTROL Last updated]**: De tijd de dataflow looppas werd laatst bijgewerkt.

De detailspagina heeft ook een knevel om tussen dataflow loopfouten en segmenten te schakelen. Deze optie is slechts beschikbaar voor dataflow looppas in partijbestemmingen.

In de weergave met uitvoerfouten in de gegevensstroom wordt een lijst weergegeven met mislukte identiteiten en identiteiten die zijn uitgesloten. De informatie voor zowel de mislukte als uitgesloten identiteiten wordt getoond, met inbegrip van de foutencode, het aantal van de identiteit, en beschrijving. Standaard worden in de lijst de mislukte identiteiten weergegeven. Als u overgeslagen identiteiten wilt weergeven, selecteert u de optie **[!UICONTROL Identities excluded]** schakelen.

![Uitgesloten entiteiten](../assets/ui/monitor-destinations/identities-excluded.png)

Wanneer **[!UICONTROL Segments]** wordt geselecteerd, ziet u een lijst van de segmenten die in de geselecteerde dataflow looppas werden geactiveerd. Dit scherm bevat op segmentniveau informatie over de geactiveerde identiteiten, de uitgesloten identiteiten, evenals de status en de tijd van de laatste dataflow-run.

![Dataflow-run - segmentweergave](../assets/ui/monitor-destinations/dataflow-run-segments-view.png)

## Volgende stappen {#next-steps}

Door deze gids te volgen, weet u nu hoe te om dataflows voor zowel partij als het stromen bestemmingen, met inbegrip van alle relevante informatie zoals verwerkingstijd, activeringstarief, en status te controleren. Lees voor meer informatie over gegevensstromen in Platform de [gegevensstroomoverzicht](../home.md). Voor meer informatie over bestemmingen leest u de [Overzicht van doelen](../../destinations/home.md).