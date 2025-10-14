---
keywords: Experience Platform;home;populaire onderwerpen;monitorprofielen;monitorgegevensstromen;dataflows;profiel;real-time klantprofiel;
description: In real time het Profiel van de Klant laat u een holistische mening van elke individuele klant zien door gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derde te combineren. Deze zelfstudie bevat instructies voor het controleren van gegevensstromen met profielen via de Experience Platform-gebruikersinterface.
title: Dataflows for Profiles in de UI controleren
type: Tutorial
exl-id: 00b624b2-f6d1-4ef2-abf2-52cede89b684
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 0%

---

# Dataflows for Profiles in de UI controleren

In real time het Profiel van de Klant laat u een holistische mening van elke individuele klant zien door gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derde te combineren. Het profiel staat u toe om uw klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

Op het dashboard voor bewaking ziet u een visuele weergave van de activiteit van de gegevens in Profiel, inclusief de status van de profielen van uw gegevens. Deze zelfstudie bevat instructies voor het gebruik van het dashboard voor bewaking van de gegevensprofielen via de Experience Platform-gebruikersinterface, waarmee u de status van de profielverwerking kunt bijhouden.

## Aan de slag {#getting-started}

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [&#x200B; Dataflows &#x200B;](../home.md): Dataflows zijn een vertegenwoordiging van gegevensbanen die gegevens over Experience Platform bewegen. Dataflows worden geconfigureerd op verschillende services, waardoor gegevens van bronconnectors naar doelgegevenssets worden verplaatst, naar [!DNL Identity] en [!DNL Profile] en naar [!DNL Destinations] .
   - [&#x200B; looppas Dataflow &#x200B;](../../sources/notifications.md): De looppas van Dataflow is de terugkomende geplande banen die op de frequentieconfiguratie van geselecteerde dataflows worden gebaseerd.
- [&#x200B; Real-Time Profiel van de Klant &#x200B;](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [&#x200B; Sandboxen &#x200B;](../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

## Dashboard voor controleprofielen {#profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_profile_processing"
>title="Profielverwerking"
>abstract="De profielverwerkingsweergave bevat informatie over records die worden opgenomen in de profielservice, zoals het aantal gemaakte profielfragmenten, de bijgewerkte profielfragmenten en het totale aantal profielfragmenten."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_profile"
>title="Gegevens gegevensstroom uitvoeren"
>abstract="Op de pagina met uitvoergegevens voor Dataflow-gegevens wordt meer informatie weergegeven over de uitvoering van de profielgegevens, waaronder de organisatie-id en de uitvoerings-id van de dataflow."

Als u het dashboard **[!UICONTROL Profiles]** wilt openen, selecteert u **[!UICONTROL Monitoring]** in de linkernavigatie. Selecteer eenmaal op de pagina **[!UICONTROL Monitoring]** de **[!UICONTROL Profiles]** -kaart.

![&#x200B; De kaart van Profielen. Informatie over het aantal verslagen die worden ontvangen, het aantal gemaakte en bijgewerkte profielfragmenten, en het succestarief wordt getoond.](../assets/ui/monitor-profiles/focus-card.png)

Op het hoofddashboard van **[!UICONTROL Profiles]** geeft de **[!UICONTROL Profiles]** -kaart informatie over het totale aantal ontvangen records, het aantal gemaakte en bijgewerkte profielfragmenten en de successnelheid van gemaakte en bijgewerkte profielfragmenten.

Het dashboard zelf bevat gegevens over profielverwerking. Standaard bevat het dashboard de verwerkingsgegevens van het profiel voor de bronnen van uw organisatie gedurende de laatste 24 uur.

![&#x200B; het dashboard van Profielen. De informatie over het aantal verslagen van het Profiel die per bron worden ontvangen wordt getoond.](../assets/ui/monitor-profiles/sources.png)

De pagina [!UICONTROL Profile processing] bevat informatie over records die aan [!DNL Profile] worden toegevoegd, zoals het aantal gemaakte profielfragmenten, bijgewerkte profielfragmenten en het totale aantal profielfragmenten.

De volgende metriek is beschikbaar voor deze dashboardmening:

| Metrisch | Beschrijving |
| -------| ----------- |
| **[!UICONTROL Source name]** | De naam van de bron. |
| **[!UICONTROL Records received]** | Het aantal records dat wordt ontvangen van data Lake. |
| **[!UICONTROL Records failed]** | Het aantal records dat als gevolg van fouten is opgenomen, maar niet in [!DNL Profile] . |
| **[!UICONTROL Profile fragments created]** | Het aantal netto nieuwe [!DNL Profile] fragmenten dat wordt toegevoegd. |
| **[!UICONTROL Profile fragments updated]** | Het aantal bestaande [!DNL Profile] fragmenten dat is bijgewerkt. |
| **[!UICONTROL Total Profile fragments]** | Het totale aantal records dat in [!DNL Profile] is geschreven, inclusief alle bestaande [!DNL Profile] fragmenten die zijn bijgewerkt en nieuwe [!DNL Profile] fragmenten die zijn gemaakt. |
| **[!UICONTROL Total failed dataflows]** | Het aantal dataflow wordt uitgevoerd dat is mislukt. |

U kunt het pictogram van de filter ![&#x200B; Filter &#x200B;](/help/images/icons/filter.png) naast de bronnaam selecteren om de verwerkingsinformatie van het Profiel voor de dataflows van die geselecteerde bron te zien.

![&#x200B; het filterpictogram wordt benadrukt. Als u dit pictogram selecteert, kunt u de gegevensstromen van de geselecteerde bron weergeven.](../assets/ui/monitor-profiles/sources-filter.png)

U kunt ook **[!UICONTROL Dataflows]** in de schakeloptie selecteren om de profielverwerkingsdetails voor de gegevensstromen van uw organisatie gedurende de laatste 24 uur te bekijken.

![&#x200B; het dashboard van Profielen. De informatie over het aantal verslagen van het Profiel die per dataflow worden ontvangen wordt getoond.](../assets/ui/monitor-profiles/dataflows.png)

De volgende metriek is beschikbaar voor deze dashboardmening:

| Metrisch | Beschrijving |
| -------| ----------- |
| **[!UICONTROL Dataflow]** | De naam van de gegevensstroom. |
| **[!UICONTROL Dataset]** | De naam van de dataset die dataflow opneemt aan. |
| **[!UICONTROL Source name]** | De naam van de bron waartoe de gegevensstroom behoort. |
| **[!UICONTROL Records received**] | Het aantal records dat wordt ontvangen van data Lake. |
| **[!UICONTROL Records failed]** | Het aantal records dat als gevolg van fouten is opgenomen, maar niet in [!DNL Profile] . |
| **[!UICONTROL Profile fragments created]** | Het aantal netto nieuwe [!DNL Profile] fragmenten dat wordt toegevoegd. |
| **[!UICONTROL Profile fragments updated]** | Het aantal bestaande [!DNL Profile] fragmenten dat is bijgewerkt |
| **[!UICONTROL Total Profile fragments]** | Het totale aantal records dat in [!DNL Profile] is geschreven, inclusief alle bestaande [!DNL Profile] fragmenten die zijn bijgewerkt en nieuwe [!DNL Profile] fragmenten die zijn gemaakt. |
| **[!UICONTROL Total failed flow runs]** | Het aantal dataflow wordt uitgevoerd dat is mislukt. |
| **[!UICONTROL Last active]** | De tijdstempel die de gegevensstroom het laatst heeft uitgevoerd. |

Selecteer het filterpictogram ![&#x200B; filter &#x200B;](/help/images/icons/filter.png) naast de dataflow runtime begintijd om meer informatie over uw [!DNL Profile] dataflow looppas te zien.

![&#x200B; het filterpictogram wordt benadrukt. Als u dit pictogram selecteert, kunt u details over de geselecteerde gegevensstroom weergeven.](../assets/ui/monitor-profiles/dataflows-filter.png)

Op de pagina [!UICONTROL Dataflow run details] wordt meer informatie weergegeven over de [!DNL Profile] dataflow-uitvoering, inclusief de organisatie-id en de id voor de uitvoering van de gegevensstroom. Op deze pagina worden ook de bijbehorende foutcode en het foutbericht weergegeven die door [!DNL Profile] worden geboden, als er fouten optreden in het innameproces.

![&#x200B; het dashboard dat van A gedetailleerde informatie over geselecteerde dataflow toont wordt getoond.](../assets/ui/monitor-profiles/dataflow-run-details.png)

De volgende metriek is beschikbaar voor deze dashboardmening:

| Metrisch | Beschrijving |
| -------| ----------- |
| **[!UICONTROL Records received]** | Het aantal records dat wordt ontvangen van data Lake. |
| **[!UICONTROL Records failed]** | Het aantal records dat als gevolg van fouten is opgenomen, maar niet in [!DNL Profile] . |
| **[!UICONTROL Profile fragments created]** | Het aantal netto nieuwe [!DNL Profile] fragmenten dat wordt toegevoegd. |
| **[!UICONTROL Profile fragments updated]** | Het aantal bestaande [!DNL Profile] fragmenten dat is bijgewerkt. |
| **[!UICONTROL Status]** | Bepaalt de algemene status van een gegevensstroom. De mogelijke statuswaarden zijn: <ul><li>`Success`: Geeft aan dat een gegevensstroom actief is en gegevens opneemt volgens het schema dat is opgegeven.</li><li>`Failed`: geeft aan dat het activeringsproces van een gegevensstroom is onderbroken als gevolg van fouten. </li><li>`Processing`: geeft aan dat de gegevensstroom nog niet actief is. Deze status wordt vaak direct na het maken van een nieuwe gegevensstroom aangetroffen.</li></ul> |
| **[!UICONTROL Dataflow run start]** | De datum en de tijd dataflow begon te lopen. |
| **[!UICONTROL Last updated]** | De datum en tijd de dataflow laatst bijgewerkt. |
| **[!UICONTROL Error summary]** | Als de dataflow-run is mislukt, wordt een foutcode en een overzicht weergegeven van waarom de dataflow-run is mislukt. |
| **[!UICONTROL Dataflow run ID]** | De id van de gegevensstroom wordt uitgevoerd. |
| **[!UICONTROL IMS org ID]** | De organisatie-id waartoe de dataflow-run behoort. |

Bovendien kunt u de schakeloptie selecteren om de records te bekijken die zijn mislukt of de records die zijn overgeslagen. De sectie Fouten bevat details over de foutcode en het aantal mislukte of uitgesloten records.
