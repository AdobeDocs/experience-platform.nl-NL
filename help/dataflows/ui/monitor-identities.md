---
keywords: Experience Platform;thuis;populaire onderwerpen;monitoridentiteiten;monitordataflows;dataflows;identiteiten;
description: De Adobe Experience Platform Identity Service biedt u een uitgebreid overzicht van uw klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden. Deze zelfstudie bevat instructies voor het controleren van gegevensstromen met identiteiten via de gebruikersinterface van het Experience Platform.
title: Gegevensstromen van de monitor voor Identiteiten in UI
type: Tutorial
exl-id: 735b0e52-74f6-47fe-98c6-e12a633b6f57
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 0%

---

# Dataflows for identity&#39;s in de UI controleren

De Adobe Experience Platform Identity Service biedt u een uitgebreid overzicht van uw klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

Op het dashboard voor bewaking ziet u een visuele weergave van de activiteit van de gegevens binnen identiteiten, inclusief de status van de identiteiten van uw gegevens. Deze zelfstudie bevat instructies over hoe u het dashboard voor bewaking kunt gebruiken om de identiteiten van uw gegevens te controleren via de gebruikersinterface van het Experience Platform, zodat u de status van identiteitsverwerking kunt volgen.

## Aan de slag {#getting-started}

- [ Dataflows ](../home.md): Dataflows zijn een vertegenwoordiging van gegevensbanen die gegevens over Platform bewegen. Dataflows worden geconfigureerd op verschillende services, waardoor gegevens van bronconnectors naar doelgegevenssets worden verplaatst, naar [!DNL Identity] en [!DNL Profile] en naar [!DNL Destinations] .
   - [ looppas Dataflow ](../../sources/notifications.md): De looppas van Dataflow is de terugkomende geplande banen die op de frequentieconfiguratie van geselecteerde dataflows worden gebaseerd.
- [ Dienst van de Identiteit ](../../identity-service/home.md): Verkrijg een betere mening van individuele klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen.
- [ Sandboxen ](../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

## Het dashboard voor het controleren van identiteiten {#identity-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_identity_processing"
>title="Identiteitsverwerking"
>abstract="De weergave Identiteitsverwerking bevat informatie over records die aan de identiteitsservice zijn toegevoegd, zoals het aantal toegevoegde identiteiten, gemaakte grafieken en bijgewerkte grafieken. Bekijk de metrische definitiegids voor meer informatie over metriek en grafieken."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_identity"
>title="Gegevens gegevensstroom uitvoeren"
>abstract="De Dataflow looppas detailpagina toont meer informatie over uw Dataslow van de Identiteit, met inbegrip van zijn organisatie ID en dataflow looppas identiteitskaart"

Als u het dashboard **[!UICONTROL Identities]** wilt openen, selecteert u **[!UICONTROL Monitoring]** in de linkernavigatie. Selecteer eenmaal op de pagina **[!UICONTROL Monitoring]** de **[!UICONTROL Identities]** -kaart.

![ de kaart van Identiteiten. De informatie over het aantal ontvangen verslagen, het aantal opgenomen verslagen, en het succestarief wordt getoond.](../assets/ui/monitor-identities/focus-card.png)

Op het hoofddashboard van **[!UICONTROL Identities]** geeft de **[!UICONTROL Identities]** -kaart informatie over het totale aantal ontvangen records, het aantal opgenomen records en de mate waarin records correct zijn ingevoerd.

Het dashboard zelf bevat gegevens over identiteitsverwerking. Standaard bevat het dashboard de identiteitsverwerkingsgegevens voor de bronnen van uw organisatie gedurende de laatste 24 uur.

![ het dashboard van Identiteiten. De informatie over het aantal verslagen die per bron worden ontvangen wordt getoond.](../assets/ui/monitor-identities/sources.png)

De pagina [!UICONTROL Identity processing] bevat informatie over records die aan [!DNL Identity Service] worden toegevoegd, zoals het aantal toegevoegde identiteiten, gemaakte grafieken en bijgewerkte grafieken.

De volgende metriek is beschikbaar voor deze dashboardmening:

| Identiteitswaarden | Beschrijving |
| ---------------- | ----------- |
| **[!UICONTROL Records received]** | Het aantal records dat wordt ontvangen van data Lake. |
| **[!UICONTROL Records failed]** | Het aantal verslagen die niet in Platform wegens fouten in de gegevens werden opgenomen. |
| **[!UICONTROL Records skipped]** | Het aantal records dat is ingevoegd, maar niet in [!DNL Identity Service] omdat de recordrij slechts één id bevat. |
| **[!UICONTROL Records ingested]** | Het aantal records dat in [!DNL Identity Service] wordt ingevoerd. |
| **[!UICONTROL Identities added]** | Het aantal nieuwe id&#39;s dat netto wordt toegevoegd aan [!DNL Identity Service]. |
| **[!UICONTROL Graphs created]** | Het aantal netto nieuwe identiteitsgrafieken die in [!DNL Identity Service] worden gecreeerd. |
| **[!UICONTROL Graphs updated]** | Het aantal bestaande identiteitsgrafieken dat met nieuwe randen is bijgewerkt. |
| **[!UICONTROL Total failed dataflows]** | Het aantal dataflow wordt uitgevoerd dat is mislukt. |

U kunt het pictogram van de filter ![ Filter ](../assets/ui/monitor-identities/filter.png) naast de bronnaam selecteren om de verwerkingsinformatie van de Identiteit voor de dataflows van die geselecteerde bron te zien.

![ het filterpictogram wordt benadrukt. Als u dit pictogram selecteert, kunt u de gegevensstromen van de geselecteerde bron weergeven.](../assets/ui/monitor-identities/sources-filter.png)

U kunt ook **[!UICONTROL Dataflows]** in de schakeloptie selecteren om de details van de identiteitsverwerking voor de gegevensstromen van uw organisatie gedurende de laatste 24 uur te zien.

![ het dashboard van Identiteiten. De informatie over het aantal identiteiten die per dataflow worden ontvangen wordt getoond.](../assets/ui/monitor-identities/dataflows.png)

De volgende metriek is beschikbaar voor deze dashboardmening:

| Metrisch | Beschrijving |
| -------| ----------- |
| **[!UICONTROL Dataflow]** | De naam van de gegevensstroom. |
| **[!UICONTROL Dataset]** | De naam van de dataset die dataflow opneemt aan. |
| **[!UICONTROL Source name]** | De naam van de bron waartoe de gegevensstroom behoort. |
| **[!UICONTROL Records received]** | Het aantal records dat wordt ontvangen van data Lake. |
| **[!UICONTROL Records failed]** | Het aantal verslagen die niet in Platform wegens fouten in de gegevens werden opgenomen. |
| **[!UICONTROL Records skipped]** | Het aantal records dat is ingevoegd, maar niet in [!DNL Identity Service] omdat de recordrij slechts één id bevat. |
| **[!UICONTROL Records ingested]** | Het aantal records dat in [!DNL Identity Service] wordt ingevoerd. |
| **[!UICONTROL Total records]** | Het totale aantal records, inclusief mislukte records, overgeslagen records, toegevoegde identiteiten en gedupliceerde records. |
| **[!UICONTROL Identities added]** | Het aantal nieuwe id&#39;s dat netto wordt toegevoegd aan [!DNL Identity Service]. |
| **[!UICONTROL Graphs created]** | Het aantal netto nieuwe identiteitsgrafieken die in [!DNL Identity Service] worden gecreeerd. |
| **[!UICONTROL Graphs updated]** | Het aantal bestaande identiteitsgrafieken dat met nieuwe randen is bijgewerkt. |
| **[!UICONTROL Total failed dataflows]** | Het aantal dataflow wordt uitgevoerd dat is mislukt. |

Selecteer het filterpictogram ![ filter ](../assets/ui/monitor-identities/filter.png) naast de dataflow runtime begintijd om meer informatie over uw [!DNL Identity] dataflow looppas te zien.

![ het filterpictogram wordt benadrukt. Als u dit pictogram selecteert, kunt u details over de geselecteerde gegevensstroom weergeven.](../assets/ui/monitor-identities/dataflows-filter.png)

Op de pagina [!UICONTROL Dataflow run details] wordt meer informatie weergegeven over de [!DNL Identity] dataflow-uitvoering, inclusief de organisatie-id en de id voor de uitvoering van de gegevensstroom. Op deze pagina worden ook de bijbehorende foutcode en het foutbericht weergegeven die door [!DNL Identity Service] worden geboden, als er fouten optreden in het innameproces.

![ het dashboard dat van A gedetailleerde informatie over geselecteerde dataflow toont wordt getoond.](../assets/ui/monitor-identities/dataflow-run-details.png)

De volgende metriek is beschikbaar voor deze dashboardmening:

| Metrisch | Beschrijving |
| -------| ----------- |
| **[!UICONTROL Records received]** | Het aantal records dat wordt ontvangen van data Lake. |
| **[!UICONTROL Records failed]** | Het aantal verslagen die niet in Platform wegens fouten in de gegevens werden opgenomen. |
| **[!UICONTROL Records skipped]** | Het aantal records dat is ingevoegd, maar niet in [!DNL Identity Service] omdat de recordrij slechts één id bevat. |
| **[!UICONTROL Records ingested]** | Het aantal records dat in [!DNL Identity Service] wordt ingevoerd. |
| **[!UICONTROL Identities added]** | Het aantal nieuwe id&#39;s dat netto wordt toegevoegd aan [!DNL Identity Service]. |
| **[!UICONTROL Graphs created]** | Het aantal netto nieuwe identiteitsgrafieken die in [!DNL Identity Service] worden gecreeerd. |
| **[!UICONTROL Graphs updated]** | Het aantal bestaande identiteitsgrafieken dat met nieuwe randen is bijgewerkt. |
| **[!UICONTROL Status]** | Bepaalt de algemene status van een gegevensstroom. De mogelijke statuswaarden zijn: <ul><li>`Success`: Geeft aan dat een gegevensstroom actief is en gegevens opneemt volgens het schema dat is opgegeven.</li><li>`Failed`: geeft aan dat het activeringsproces van een gegevensstroom is onderbroken als gevolg van fouten. </li><li>`Processing`: geeft aan dat de gegevensstroom nog niet actief is. Deze status wordt vaak direct na het maken van een nieuwe gegevensstroom aangetroffen.</li></ul> |
| **[!UICONTROL Dataflow run start]** | De datum en de tijd dataflow begon te lopen. |
| **[!UICONTROL Last updated]** | De datum en tijd de dataflow laatst bijgewerkt. |
| **[!UICONTROL Error summary]** | Als de dataflow-run is mislukt, wordt een foutcode en een overzicht weergegeven van waarom de dataflow-run is mislukt. |
| **[!UICONTROL Dataflow run ID]** | De id van de gegevensstroom wordt uitgevoerd. |
| **[!UICONTROL IMS org ID]** | De organisatie-id waartoe de dataflow-run behoort. |

Bovendien kunt u de schakeloptie selecteren om de records te bekijken die zijn mislukt of de records die zijn overgeslagen. De sectie Fouten bevat details over de foutcode en het aantal mislukte of uitgesloten records.
