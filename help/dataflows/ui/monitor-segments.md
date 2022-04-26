---
keywords: Experience Platform;huis;populaire onderwerpen;monitorsegmenten;monitordataflows;dataflows;segmentatie
description: De segmentatie staat u toe om segmenten en publiek van uw gegevens van het Profiel van de Klant in real time tot stand te brengen. Deze zelfstudie bevat instructies voor het controleren van gegevensstromen tijdens segmentatie met behulp van de gebruikersinterface van het Experience Platform.
title: Dataflows for Segments in UI controleren
topic-legacy: overview
type: Tutorial
source-git-commit: cec27197d47d2dd979bdf29f16fef77e8ff855e3
workflow-type: tm+mt
source-wordcount: '1783'
ht-degree: 0%

---

# Dataflows for segments in UI

Met de segmentatieservice kunt u segmenten en publiek maken op basis van uw gegevens in het realtime klantprofiel in Adobe Experience Platform. Platform verstrekt gegevensstromen om deze stroom van gegevens van bronnen aan bestemmingen doorzichtig te volgen.

Het controledashboard voorziet u van een visuele vertegenwoordiging van de activiteit van de gegevens binnen een segment, met inbegrip van de status van de segmentatie van uw gegevens. Deze zelfstudie bevat instructies over hoe u het dashboard voor bewaking kunt gebruiken om de segmentatie van uw gegevens te controleren met behulp van de gebruikersinterface van het Experience Platform, zodat u de status van segmentactivering, -evaluatie en -exporttaken kunt bijhouden.

## Aan de slag {#getting-started}

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [Gegevensstromen](../home.md): Dataflows zijn een voorstelling van gegevenstaken die gegevens over het Platform verplaatsen. Dataflows worden gevormd over verschillende diensten, die gegevens van bronschakelaars aan doeldatasets helpen bewegen, aan [!DNL Identity] en [!DNL Profile]en [!DNL Destinations].
   - [Dataflow-uitvoering](../../sources/notifications.md): De looppas van Dataflow is de terugkomende geplande banen die op de frequentieconfiguratie van geselecteerde dataflows worden gebaseerd.
- [Segmentering](../../segmentation/home.md): De segmentatie staat u toe om segmenten en publiek van uw gegevens van het Profiel van de Klant in real time tot stand te brengen.
   - [Activeringstaken](../../destinations/ui/activation-overview.md): Een activeringsbaan wordt gebruikt om uw segment aan een gespecificeerde bestemming te activeren.
   - [Evaluatiebanen](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment): Een evaluatietaak is een asynchroon proces dat tot een publiekssegment leidt dat op het gespecificeerde segment wordt gebaseerd.
   - [Exporttaken](../../segmentation/api/export-jobs.md): Een uitvoerbaan is een asynchrone processen die worden gebruikt om de leden van het publiekssegment aan datasets voort te zetten.
- [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## Dashboard voor segmenten controleren {#monitoring-segments-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segments"
>title="Segmenten"
>abstract="De segmentweergave bevat informatie over alle segmenten van uw IMS-organisatie, met meer informatie over hun activerings- en evaluatietaken."

Om toegang te krijgen tot **[!UICONTROL Segments]** dashboard, selecteren **[!UICONTROL Monitoring]** in de linkernavigatie. Eén keer op de knop **[!UICONTROL Monitoring]** pagina, selecteert u de **[!UICONTROL Segments]** kaart.

![De segmentkaart. Informatie over de laatste evaluatietaak en de laatste exporttaak wordt weergegeven.](../assets/ui/monitor-segments/segment-card-monitoring.png)

Over de hoofdlijnen **[!UICONTROL Segments]** dashboard, het **[!UICONTROL Segments]** op de kaart staan de status en de datum van de laatste evaluatietaak en de laatste exporttaak.

Het dashboard zelf bevat meetgegevens voor zowel segmenten als segmenttaken. Standaard worden in het dashboard de segmentwaarden voor de laatste 24 uur weergegeven. Lees voor meer informatie over de weergave voor segmenttaken de [segmenttaken controleren](#monitoring-segment-jobs-dashboard) sectie.

>[!IMPORTANT]
>
>Momenteel worden alleen segmenten geactiveerd waarop [batchbestemmingen (op basis van bestanden)](../../destinations/destination-types.md#file-based) worden ondersteund voor het dashboard voor monitoringssegmenten.

![Het segmentdashboard. Informatie over de verschillende segmenten in uw IMS-organisatie en -sandbox wordt weergegeven.](../assets/ui/monitor-segments/segment-monitoring-dashboard.png)

De volgende metriek is beschikbaar voor deze dashboardmening:

| Metrisch | Beschrijving |
| ------ | ----------- |
| **[!UICONTROL Segment name]** | De naam van het segment. |
| **[!UICONTROL Last evaluation timestamp]** | De datum en de tijd dat de laatste evaluatietaak van het segment liep. |
| **[!UICONTROL Last evaluation status]** | De status van de laatste evaluatietaak van het segment. Mogelijke waarden zijn **[!UICONTROL Success]**, **[!UICONTROL No runs]**, en **[!UICONTROL Failed]**. |
| **[!UICONTROL Last evaluation profiles]** | Het aantal profielen dat in de laatste evaluatietaak van het segment werd geëvalueerd. |
| **[!UICONTROL Last activation timestamp]** | De datum en tijd waarop de laatste activeringstaak van het segment werd uitgevoerd. |
| **[!UICONTROL Last activation status]** | De status van de laatste activeringstaak van het segment. Mogelijke waarden zijn **[!UICONTROL Success]**, **[!UICONTROL No runs]**, en **[!UICONTROL Failed]**. |
| **[!UICONTROL Last activation identities]** | Het aantal identiteiten die in de laatste activeringstaak van het segment werden geactiveerd. |
| **[!UICONTROL Last activation destination]** | De naam van de bestemming waarop de laatste activeringstaak van het segment heeft geactiveerd. |

U kunt de resultaten naar een specifiek segment filteren en de segmenttaken ervan bekijken door het filterpictogram (![Het filterpictogram.](../assets/ui/monitor-segments/filter-icon.png)). De segmentbanen worden gesorteerd in chronologische volgorde, waarbij de meest recente segmentbanen eerst verschijnen.

![Het filterpictogram wordt gemarkeerd. Als u dit selecteert, kunt u de segmenttaken voor het opgegeven segment weergeven.](../assets/ui/monitor-segments/filter-segment.png)

Het gefilterde segmentdashboard wordt weergegeven. De **[!UICONTROL Segments]** op de kaart staan de status en de datum van de laatste evaluatietaak en de laatste activeringstaak.

![De segmentkaart. Informatie over de laatste evaluatietaak en de laatste activeringstaak wordt weergegeven.](../assets/ui/monitor-segments/specified-segment-card.png)

Het dashboard zelf toont de tijd en de status van de laatste evaluatie en activeringstaken, een grafiek die de profieltelling van de segmentevaluatie, en metriek voor de segmentbanen toont die werden in werking gesteld. Standaard worden in het dashboard de resultaten van de segmenttaak voor de laatste 24 uur weergegeven.

![Het gefilterde segmentdashboard. De informatie over de diverse segmentbanen die voor dit segment zijn gelopen wordt getoond.](../assets/ui/monitor-segments/filter-specified-segment.png)

De volgende metriek is beschikbaar voor deze dashboardmening:

| Metrisch | Beschrijving |
| ------ | ----------- |
| **[!UICONTROL Job start]** | De datum en tijd waarop de segmenttaak is gestart. |
| **[!UICONTROL Type]** | Geeft het type segmenttaak aan. De twee ondersteunde taaktypen zijn **activering** en **evaluatie** banen. |
| **[!UICONTROL Job complete]** | De datum en de tijd toen de segmentbaan voltooide. |
| **[!UICONTROL Processing time]** | De hoeveelheid tijd die het voor de segmentbaan nam om te voltooien. |
| **[!UICONTROL Job status]** | De status van de segmenttaak. Tot de ondersteunde waarden behoren **[!UICONTROL Success]**, **[!UICONTROL In Progress]**, en **[!UICONTROL Failed]**. |
| **[!UICONTROL Profile count]** | Het aantal profielen dat de segmentbaan evalueert. Elke gebruiker moet een uniek profiel hebben. |
| **[!UICONTROL Identity count]** | Het aantal identiteiten dat de segmentbaan activeert. Elk profiel kan meerdere identiteiten hebben. Een profiel kan bijvoorbeeld een e-mail, telefoonnummer en een loyaliteitsnummer als identiteiten hebben. |
| **[!UICONTROL Destination name]** | De naam van de bestemming waarop de segmenttaak wordt geactiveerd. |

U kunt verder filteren naar een specifieke segmenttaak en de details ervan bekijken door het filterpictogram te selecteren (![Het filterpictogram.](../assets/ui/monitor-segments/filter-icon.png)). Er zijn twee verschillende soorten segmentbanen die kunnen worden gefilterd: activerende banen en evaluatietaken.

### Gegevens activeringstaak {#activation-job-details}

De pagina met gegevens over de uitvoering van de activeringstaak bevat informatie over de metriek van de uitvoering, fouten bij uitvoering van de gegevensstroom en segmenten die betrekking hebben op de segmenttaak. Een activeringsbaan wordt gebruikt om uw segment voor een gespecificeerde bestemming te activeren. Standaard worden op de detailpagina de fouten weergegeven die zijn opgetreden bij het uitvoeren van de gegevensstroom.

![Het gefilterde segmentdashboard. De informatie over de diverse segmentbanen die voor dit segment zijn gelopen wordt getoond.](../assets/ui/monitor-segments/activation-job-details.png)

De volgende metriek is beschikbaar voor deze dashboardmening:

| Metrisch | Beschrijving |
| ------ | ----------- |
| **[!UICONTROL Profiles received]** | Het totale aantal profielen dat is ontvangen in de activeringsstroom. |
| **[!UICONTROL Identities activated]** | Het totale aantal identiteiten dat met succes aan de bestemming werd geactiveerd, die op de ontvangen profielen wordt gebaseerd. |
| **[!UICONTROL Identities excluded]** | Het totale aantal identiteiten dat op basis van de ontvangen profielen is uitgesloten van activering naar de bestemming. Deze identiteiten kunnen worden uitgesloten vanwege ontbrekende kenmerken of schendingen van de toestemming. |
| **[!UICONTROL Size of data]** | De grootte van de gegevensstroom die wordt geactiveerd. |
| **[!UICONTROL Total files]** | Het totale aantal bestanden dat in de gegevensstroom wordt geactiveerd. |
| **[!UICONTROL Status]** | De huidige status van de activeringstaak. |
| **[!UICONTROL Dataflow run start]** | De datum en tijd waarop de activeringstaak is gestart. |
| **[!UICONTROL Dataflow run end]** | De datum en tijd waarop de activeringstaak is beëindigd. |
| **[!UICONTROL Dataflow run ID]** | De id van de huidige activeringstaak. |
| **[!UICONTROL IMS org ID]** | De id van de IMS-organisatie waartoe de activeringstaak behoort. |
| **[!UICONTROL Destination name]** | De naam van het doel waarop de gegevens worden geactiveerd. |

Onder de metriek, wordt een knevel om tussen de dataflow loopfouten en de segmenten te selecteren getoond.

![Het gefilterde segmentdashboard. De knevel die wordt gebruikt om tussen de dataflow loopfouten en de segmentvertoning te schakelen wordt benadrukt.](../assets/ui/monitor-segments/activation-job-details-toggle.png)

Selecteer onder de sectie met fouten bij uitvoering van de gegevensstroom de schakeloptie om de mislukte identiteiten of de velden voor het uitsluiten van identiteiten weer te geven. De sectie Fouten bevat details over de foutcode en het aantal mislukte of uitgesloten identiteiten.

![Het gefilterde segmentdashboard. Informatie over de identiteiten die zijn mislukt of uitgesloten, wordt gemarkeerd.](../assets/ui/monitor-segments/activation-job-details.png)

Onder de segmentsectie ziet u een lijst met segmenten die als onderdeel van de activeringstaak zijn geactiveerd. Gebruik de zoekbalk om de lijst met segmenten op naam te filteren.

![Het gefilterde segmentdashboard. Informatie over de identiteiten die zijn mislukt of uitgesloten, wordt gemarkeerd.](../assets/ui/monitor-segments/activation-job-details-segments.png)

Voor de segmentsectie zijn de volgende metriek beschikbaar:

| Metrisch | Beschrijving |
| ------ | ----------- |
| **[!UICONTROL Name]** | De naam van het segment dat is geactiveerd. |
| **[!UICONTROL Identities activated]** | Het totale aantal identiteiten dat met succes aan de bestemming werd geactiveerd, die op de ontvangen profielen wordt gebaseerd. |
| **[!UICONTROL Identities excluded]** | Het totale aantal identiteiten dat op basis van de ontvangen profielen is uitgesloten van activering naar de bestemming. Deze identiteiten kunnen worden uitgesloten vanwege ontbrekende kenmerken of schending van de toestemming. |
| **[!UICONTROL Last dataflow run status]** | De status van de laatste activeringstaak die voor dat segment is uitgevoerd. |
| **[!UICONTROL Last dataflow run date]** | De datum en tijd van de laatste activeringsbaan die voor dat segment liep. |

### Gegevens van evaluatietaken {#evaluation-job-details}

De dataflow van de evaluatietaak detailpagina toont informatie over de metriek en de segmenten van de looppas die met de segmentbaan verwant zijn. Een evaluatietaak is een asynchroon proces dat tot een publiekssegment leidt dat op het gespecificeerde segment wordt gebaseerd. Lees de zelfstudie voor meer informatie over evaluatietaken [evalueren van een segment](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment).

![Het dashboard voor de evaluatietaak. De informatie over de baan van de segmentevaluatie wordt getoond.](../assets/ui/monitor-segments/evaluation-job-details.png)

De volgende metriek is beschikbaar voor deze dashboardmening:

| Metrisch | Beschrijving |
| ------ | ----------- |
| **[!UICONTROL Total profiles]** | Het totale aantal profielen dat wordt geëvalueerd. |
| **[!UICONTROL Status]** | De status van de evaluatietaak. Mogelijke statussen voor de evaluatietaak omvatten **[!UICONTROL Success]** en **[!UICONTROL Failed]**. |
| **[!UICONTROL Job start]** | De datum en het tijdstip waarop de evaluatietaak is begonnen. |
| **[!UICONTROL Job end]** | De datum en het tijdstip waarop de evaluatietaak is beëindigd. |
| **[!UICONTROL Job type]** | Het type segmenttaak. In dit geval zal het altijd een segmentevaluatietaak zijn. |
| **[!UICONTROL Evaluation type]** | Het soort evaluatie dat wordt uitgevoerd. Dit kan **[!UICONTROL Batch]** of **[!UICONTROL Streaming]**. |
| **[!UICONTROL Job ID]** | De id van de evaluatietaak. |
| **[!UICONTROL IMS org ID]** | De id van de IMS-organisatie waartoe de evaluatietaak behoort. |
| **[!UICONTROL Segment name]** | De naam van het segment dat wordt geëvalueerd. |
| **[!UICONTROL Segment ID]** | De id van het segment dat wordt geëvalueerd. |

Onder de segmentsectie, kunt u een lijst van segmenten zien die als deel van de evaluatietaak worden geëvalueerd. U kunt de lijst met segmenten filteren op naam met de zoekbalk.

>[!IMPORTANT]
>
>Deze dashboardweergave biedt momenteel ondersteuning voor maximaal 800 segmentmetriek.

Voor de segmentsectie zijn de volgende metriek beschikbaar:

| Metrisch | Beschrijving |
| ------ | ----------- |
| **[!UICONTROL Name]** | De naam van het segment dat wordt geëvalueerd. |
| **[!UICONTROL Profile count]** | Het aantal profielen dat wordt geëvalueerd. |

## Het dashboard voor segmenttaken controleren {#monitoring-segment-jobs-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segment_jobs"
>title="Segmenttaken"
>abstract="De mening van segmentbanen bevat informatie over de evaluatie en de uitvoerbanen voor al uw segmenten."

Om toegang te krijgen tot **[!UICONTROL Segment Jobs]** dashboard, selecteren **[!UICONTROL Monitoring]** (![bewakingspictogram](../assets/ui/monitor-destinations/monitoring-icon.png)) in de linkernavigatie. Eén keer op de knop [!UICONTROL Monitoring] pagina, selecteert u **[!UICONTROL Segment Jobs]**. De [!UICONTROL Monitoring] het dashboard bevat metriek en informatie over de segmentevaluatie en de uitvoerbanen.

>[!NOTE]
>
>Alleen **segmentevaluatietaken** worden ondersteund voor bewaking per segment. De de uitvoerbanen van het segment steunen slechts organisatie-vlakke controle.

![Dashboard voor bewaking van segmenttaken](../assets/ui/monitor-segments/segment-jobs-dashboard.png)

Gebruik de [!UICONTROL Segment Jobs] dashboard om te begrijpen als de profielevaluatie en de uitvoer op tijd en zonder enige uitzonderingen voorkomen, zodat kunnen de stroomafwaartse diensten voor bestemmingsactivering de recentste geëvalueerde profielgegevens hebben.

De volgende metriek is beschikbaar voor segmentbanen:

| Metrisch | Beschrijving |
---------|----------|
| **[!UICONTROL Segment job]** | Geeft de naam van de segmenttaak aan. |
| **[!UICONTROL Type]** | Geeft het type segmenttaak aan: exporteren of evalueren. Merk op dat in beide gevallen de segmentbaan evalueert of uitvoert **alles** segmenten die tot een organisatie behoren. Voor meer informatie over exporttaken leest u de handleiding op de [eindpunt exporttaken](../../segmentation/api/export-jobs.md). Lees de zelfstudie voor meer informatie over evaluatietaken [evalueren van een segment](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment). |
| **[!UICONTROL Job start]** | De datum en tijd waarop de segmenttaak is gestart. |
| **[!UICONTROL Job end]** | De datum en de tijd toen de segmentbaan voltooide. |
| **[!UICONTROL Status]** | De status van de voltooide taak. Mogelijke statussen voor de segmentbaan omvatten succes of ontbroken. |