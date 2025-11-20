---
description: Leer hoe u de gegevensstromen tijdens segmentatie kunt controleren gebruikend de gebruikersinterface van Experience Platform.
title: Gegevensstromen van de monitor voor publiek in UI
type: Tutorial
exl-id: 32fd2ba1-0ff0-4ea7-8d55-80d53eebc02f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1710'
ht-degree: 0%

---

# Dataflows for publiek in UI controleren

Met de segmentatieservice kunt u een publiek maken via segmentdefinities of andere bronnen van uw [!DNL Real-Time Customer Profile] -gegevens. Experience Platform verstrekt gegevensstromen om deze stroom van gegevens van bronnen aan bestemmingen doorzichtig te volgen.

Gebruik het controledashboard om een visuele vertegenwoordiging van de activiteit van de gegevens binnen een publiek, met inbegrip van de status van de segmentatie van uw gegevens te zien. Lees de zelfstudie voor instructies over hoe u het monitoringdashboard kunt gebruiken om de segmentatie van uw gegevens te controleren met behulp van de Experience Platform-gebruikersinterface, zodat u de status van activering, evaluatie en exporttaken van het publiek kunt bijhouden.

## Aan de slag {#getting-started}

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [&#x200B; Dataflows &#x200B;](../home.md): Dataflows zijn een vertegenwoordiging van gegevensbanen die gegevens over Experience Platform bewegen. Dataflows worden geconfigureerd op verschillende services, waardoor gegevens van bronconnectors naar doelgegevenssets worden verplaatst, naar [!DNL Identity] en [!DNL Profile] en naar [!DNL Destinations] .
   - [&#x200B; looppas Dataflow &#x200B;](../../sources/notifications.md): De looppas van Dataflow is de terugkomende geplande banen die op de frequentieconfiguratie van geselecteerde dataflows worden gebaseerd.
- [&#x200B; Segmentatie &#x200B;](../../segmentation/home.md): De segmentatie staat u toe om publiek van uw gegevens van het Profiel van de Klant in real time tot stand te brengen.
   - [&#x200B; de banen van de Activering &#x200B;](../../destinations/ui/activation-overview.md): Een activeringsbaan wordt gebruikt om uw publiek aan een gespecificeerde bestemming te activeren.
   - [&#x200B; de banen van de Evaluatie &#x200B;](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment): Een evaluatietaak is een asynchroon proces dat het publiek evalueert.
   - [&#x200B; de banen van de Uitvoer &#x200B;](../../segmentation/api/export-jobs.md): Een uitvoerbaan is een asynchrone processen die worden gebruikt om publieksleden aan datasets voort te zetten.
- [&#x200B; Sandboxen &#x200B;](../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

## Het dashboard voor publiek controleren {#monitoring-audiences-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segments"
>title="Doelgroepen"
>abstract="De weergave Soorten publiek bevat informatie over het publiek van uw organisatie, met meer informatie over de activerings- en evaluatietaken van uw organisatie."

Als u het dashboard **[!UICONTROL Audiences]** wilt openen, selecteert u **[!UICONTROL Monitoring]** in de linkernavigatie. Selecteer eenmaal op de pagina **[!UICONTROL Monitoring]** de **[!UICONTROL Audiences]** -kaart.

![&#x200B; de kaart van het publiek. De informatie over de laatste evaluatietaak en de laatste uitvoerbaan wordt getoond.](../assets/ui/monitor-audiences/audience-card.png)

Op het hoofddashboard van **[!UICONTROL Audiences]** geeft de **[!UICONTROL Audiences]** -kaart de status en datum van de laatste evaluatietaak en de laatste exporttaak weer.

Het dashboard zelf bevat meetgegevens voor zowel publiek- als segmentatietaken. Standaard ziet u op het dashboard de meetgegevens voor het publiek voor de laatste 24 uur. Meer over de de baanmening van de segmentatie leren, gelieve te lezen [&#x200B; controlerend segmentatietaken &#x200B;](#monitoring-segmentation-jobs-dashboard) sectie.

>[!IMPORTANT]
>
>Momenteel, slechts worden het publiek dat aan [&#x200B; (op dossier-gebaseerde) bestemmingen &#x200B;](../../destinations/destination-types.md#file-based) wordt geactiveerd gesteund voor het dashboard van het controlepubliek.

![&#x200B; het publiek dashboard. De informatie over de verschillende soorten publiek in uw organisatie en zandbak wordt getoond.](../assets/ui/monitor-audiences/audience-dashboard.png)

De volgende metriek is beschikbaar voor deze dashboardmening:

| Metrisch | Beschrijving |
| ------ | ----------- |
| **[!UICONTROL Audience name]** | De naam van het publiek. |
| **[!UICONTROL Data type]** | Het gegevenstype van het publiek. Mogelijke waarden zijn **[!UICONTROL Customer]** , **[!UICONTROL Account]** en **[!UICONTROL Prospect]** . U kunt voor publiek van een gespecificeerd gegevenstype bekijken door het [!UICONTROL Data type] filter boven het lint van kaarten te gebruiken. |
| **[!UICONTROL Last evaluation timestamp]** | De datum en tijd waarop de laatste evaluatietaak van het publiek werd uitgevoerd. |
| **[!UICONTROL Last evaluation status]** | De status van de laatste evaluatietaak van het publiek. Mogelijke waarden zijn **[!UICONTROL Success]** , **[!UICONTROL No runs]** en **[!UICONTROL Failed]** . |
| **[!UICONTROL Last evaluation method]** | De evaluatiemethode van het publiek. Aangezien alleen batchsegmentatie wordt ondersteund, is de enige mogelijke waarde **[!UICONTROL Batch]** . |
| **[!UICONTROL Last evaluation profiles]** | Het aantal profielen dat is geëvalueerd in de laatste evaluatietaak van het publiek. |
| **[!UICONTROL Last activation timestamp]** | De datum en tijd waarop de laatste activeringstaak van het publiek werd uitgevoerd. |
| **[!UICONTROL Last activation status]** | De status van de laatste activeringstaak van het publiek. Mogelijke waarden zijn **[!UICONTROL Success]** , **[!UICONTROL No runs]** en **[!UICONTROL Failed]** . |
| **[!UICONTROL Last activation identities]** | Het aantal identiteiten dat is geactiveerd in de laatste activeringstaak van het publiek. |
| **[!UICONTROL Last activation destination]** | De naam van de bestemming waarop de laatste activeringstaak van het publiek is geactiveerd. |

U kunt de resultaten aan een specifiek publiek filtreren en zijn segmentatietaken bekijken door het filterpictogram (![&#x200B; te selecteren het filterpictogram.](/help/images/icons/filter-add.png)). De segmentatietaken worden gesorteerd in chronologische volgorde, waarbij de meest recente segmentatietaken bovenaan worden weergegeven.

![&#x200B; het filterpictogram wordt benadrukt. Het selecteren van dit staat u toe om de segmentatietaken voor het gespecificeerde publiek te bekijken.](../assets/ui/monitor-audiences/filter-audience.png)

Het gefilterde publieksdashboard verschijnt. Op de **[!UICONTROL Audiences]** -kaart staan de status en datum van de laatste evaluatietaak en de laatste activeringstaak.

![&#x200B; de kaart van het publiek. De informatie over de laatste evaluatietaak en de laatste activeringsbaan wordt getoond.](../assets/ui/monitor-audiences/specified-audience-card.png)

Het dashboard zelf toont de tijd en de status van de laatste evaluatie en activeringstaken, een grafiek die de profieltelling van de publieksevaluatie, en metriek voor de segmentatietaken toont die werden in werking gesteld. Standaard worden op het dashboard de gegevens van de segmentatietaak voor de laatste 24 uur weergegeven.

![&#x200B; het gefilterde publieksdashboard. De informatie over de diverse segmentatietaken die voor dit publiek in werking zijn gesteld wordt getoond.](../assets/ui/monitor-audiences/filter-audience.png)

De volgende metriek is beschikbaar voor deze dashboardmening:

| Metrisch | Beschrijving |
| ------ | ----------- |
| **[!UICONTROL Job start]** | De datum en tijd waarop de segmentatietaak is gestart. |
| **[!UICONTROL Type]** | Geeft het type segmentatietaak aan. De twee gesteunde baantypes zijn **activering** en **evaluatie** banen. |
| **[!UICONTROL Job complete]** | De datum en tijd waarop de segmentatietaak is voltooid. |
| **[!UICONTROL Processing time]** | De hoeveelheid tijd die nodig was om de segmentatietaak te voltooien. |
| **[!UICONTROL Job status]** | De status van de segmentatietaak. Tot de ondersteunde waarden behoren **[!UICONTROL Success]** , **[!UICONTROL In Progress]** en **[!UICONTROL Failed]** . |
| **[!UICONTROL Profile count]** | Het aantal profielen dat de segmentatietaak evalueert. Elke gebruiker moet een uniek profiel hebben. |
| **[!UICONTROL Identity activated]** | Het aantal identiteiten dat de segmentatietaak activeert. Elk profiel kan meerdere identiteiten hebben. Een profiel kan bijvoorbeeld een e-mail, telefoonnummer en een loyaliteitsnummer als identiteiten hebben. |
| **[!UICONTROL Destination name]** | De naam van het doel waarop de segmentatietaak wordt geactiveerd. |

U kunt aan een specifieke segmentatietaak verder filtreren en zijn details zien door het filterpictogram (![&#x200B; te selecteren het filterpictogram.](/help/images/icons/filter.png)). Er zijn twee verschillende soorten segmentatietaken die gefilterd kunnen worden: activeringsbanen en evaluatietaken.

### Gegevens activeringstaak {#activation-job-details}

De pagina met gegevens over de uitvoering van de activeringstaak bevat informatie over de metriek van de uitvoering, fouten bij uitvoering van de gegevensstroom en soorten publiek die betrekking hebben op de segmentatietaak. Een activeringstaak wordt gebruikt om uw publiek voor een gespecificeerde bestemming te activeren.

![&#x200B; het dashboard van de activeringstaak. De informatie over de diverse segmentatietaken die voor dit publiek in werking zijn gesteld wordt getoond.](../assets/ui/monitor-audiences/activation-job-dashboard.png)

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
| **[!UICONTROL IMS org ID]** | De id van de organisatie waartoe de activeringstaak behoort. |
| **[!UICONTROL Destination name]** | De naam van het doel waarop de gegevens worden geactiveerd. |

Onder de sectie Soorten publiek ziet u een lijst met soorten publiek die zijn geactiveerd als onderdeel van de activeringstaak.

![&#x200B; het dashboard van de activeringstaak. De informatie over de identiteiten die ontbrak of werd uitgesloten wordt benadrukt.](../assets/ui/monitor-audiences/activation-job-audiences.png)

Voor de sectie publiek zijn de volgende meetgegevens beschikbaar:

| Metrisch | Beschrijving |
| ------ | ----------- |
| **[!UICONTROL Name]** | De naam van het publiek dat is geactiveerd. |
| **[!UICONTROL Identities activated]** | Het totale aantal identiteiten dat met succes aan de bestemming werd geactiveerd, die op de ontvangen profielen wordt gebaseerd. |
| **[!UICONTROL Identities excluded]** | Het totale aantal identiteiten dat op basis van de ontvangen profielen is uitgesloten van activering naar de bestemming. Deze identiteiten kunnen worden uitgesloten vanwege ontbrekende kenmerken of schending van de toestemming. |
| **[!UICONTROL Last dataflow run status]** | De status van de laatste activeringstaak die voor dat publiek werd uitgevoerd. |
| **[!UICONTROL Last dataflow run date]** | De datum en het tijdstip van de laatste activeringstaak die voor dat publiek werd uitgevoerd. |

Bovendien kunt u details over de dataflow looppas fouten bekijken. In de sectie met uitvoerfouten voor gegevensstroom kunt u zowel de mislukte identiteiten als de uitgesloten identiteiten weergeven. De sectie Fouten bevat details over de foutcode en het aantal mislukte of uitgesloten identiteiten.

![&#x200B; het dashboard van de activeringstaak. De informatie over de identiteiten die ontbrak of werd uitgesloten wordt benadrukt.](../assets/ui/monitor-audiences/activation-job-errors.png)

### Gegevens van evaluatietaken {#evaluation-job-details}

De dataflow van de evaluatietaak looppas detailpagina toont informatie over de metriek en het publiek van de looppas die met de segmentatietaak verwant zijn.

![&#x200B; het dashboard van de evaluatietaak. De informatie over de de evaluatietaak van het publiek wordt getoond.](../assets/ui/monitor-audiences/evaluation-job-details.png)

De volgende metriek is beschikbaar voor deze dashboardmening:

| Metrisch | Beschrijving |
| ------ | ----------- |
| **[!UICONTROL Total profiles]** | Het totale aantal profielen dat wordt geëvalueerd. |
| **[!UICONTROL Status]** | De status van de evaluatietaak. Mogelijke statussen voor de evaluatietaak zijn **[!UICONTROL Success]** en **[!UICONTROL Failed]** . |
| **[!UICONTROL Job start]** | De datum en het tijdstip waarop de evaluatietaak is begonnen. |
| **[!UICONTROL Job end]** | De datum en het tijdstip waarop de evaluatietaak is beëindigd. |
| **[!UICONTROL Job type]** | Het type segmentatietaak. In dit geval wordt dit altijd een **[!UICONTROL Segment evaluation]** -taak. |
| **[!UICONTROL Evaluation type]** | Het soort evaluatie dat wordt uitgevoerd. Dit kan **[!UICONTROL Batch]** of **[!UICONTROL Streaming]** zijn. |
| **[!UICONTROL Job ID]** | De id van de evaluatietaak. |
| **[!UICONTROL IMS org ID]** | De id van de organisatie waartoe de evaluatietaak behoort. |
| **[!UICONTROL Audience name]** | De naam van het publiek dat wordt geëvalueerd. |
| **[!UICONTROL Audience ID]** | De id van het publiek dat wordt geëvalueerd. |

Onder de sectie [!UICONTROL Audiences] ziet u een lijst met doelgroepen die worden geëvalueerd als onderdeel van de evaluatietaak. U kunt de lijst met soorten publiek filteren op naam met de zoekbalk.

>[!IMPORTANT]
>
>Deze dashboardweergave biedt momenteel ondersteuning voor maximaal 800 publieksmetingen.

Voor de sectie [!UICONTROL Audiences] zijn de volgende meetgegevens beschikbaar:

| Metrisch | Beschrijving |
| ------ | ----------- |
| **[!UICONTROL Name]** | De naam van het publiek dat wordt geëvalueerd. |
| **[!UICONTROL Profile count]** | Het aantal profielen dat wordt geëvalueerd. |

## Dashboard voor segmentatietaken controleren {#monitoring-segmentation-jobs-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segment_jobs"
>title="Segmentatietaken"
>abstract="De weergave voor segmentatietaken bevat informatie over de evaluatie- en exporttaken voor al uw doelgroepen."

Als u het dashboard **[!UICONTROL Segmentation Jobs]** wilt openen, selecteert u **[!UICONTROL Segmentation jobs]** in het dashboard [!UICONTROL Audiences] . Het dashboard van [!UICONTROL Monitoring] bevat metriek en informatie over de evaluatie en de uitvoerbanen.

>[!NOTE]
>
>Slechts **de banen van de segmentatieevaluatie** worden gesteund voor per-publiekscontrole. De de uitvoerbanen van de segmentatie steunen slechts organisatie-vlakke controle.

![&#x200B; de segmentatietaken die dashboard controleren wordt getoond. De knevel om tussen de banen van het publiek en van de Segmentatie te schakelen wordt benadrukt.](../assets/ui/monitor-audiences/segmentation-jobs-dashboard.png)

Gebruik het dashboard van [!UICONTROL Segmentation Jobs] om te begrijpen als de profielevaluatie en de uitvoer op tijd en zonder enige uitzonderingen voorkomen, zodat kunnen de stroomafwaartse diensten voor bestemmingsactivering de recentste geëvalueerde profielgegevens hebben.

De volgende metriek is beschikbaar voor segmentatietaken:

| Metrisch | Beschrijving |
| ------ | ----------- |
| **[!UICONTROL Segmentation job]** | Geeft de naam van de segmentatietaak aan. |
| **[!UICONTROL Type]** | Geeft het type segmentatietaak aan: exporteren of evalueren. Merk op dat in beide gevallen, de segmentatietaak **alle** publiek evalueert of uitvoert die tot een organisatie behoren. Om meer over de uitvoerbanen te leren, te lezen gelieve de gids op het [&#x200B; eindpunt van de uitvoerbanen &#x200B;](../../segmentation/api/export-jobs.md). Meer over evaluatietaken leren, te lezen gelieve het leerprogramma op [&#x200B; beoordelend een segmentdefinitie &#x200B;](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment). |
| **[!UICONTROL Job start]** | De datum en tijd waarop de segmentatietaak is gestart. |
| **[!UICONTROL Job end]** | De datum en tijd waarop de segmentatietaak is voltooid. |
| **[!UICONTROL Status]** | De status van de voltooide taak. Mogelijke statussen voor de segmentatietaak zijn geslaagd of mislukt. |
