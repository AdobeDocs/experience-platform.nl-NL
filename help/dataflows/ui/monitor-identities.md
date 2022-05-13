---
keywords: Experience Platform;thuis;populaire onderwerpen;monitoridentiteiten;monitordataflows;dataflows;identiteiten;
description: De Adobe Experience Platform Identity Service biedt u een uitgebreid overzicht van uw klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden. Deze zelfstudie bevat instructies voor het controleren van gegevensstromen met identiteiten via de gebruikersinterface van het Experience Platform.
title: Gegevensstromen van de monitor voor Identiteiten in UI
topic-legacy: overview
type: Tutorial
source-git-commit: 3018ee005c96e3905ae8dab24cca901cf48847ea
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 0%

---


# Dataflows for identity&#39;s in de UI controleren

De Adobe Experience Platform Identity Service biedt u een uitgebreid overzicht van uw klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

Op het dashboard voor bewaking ziet u een visuele weergave van de activiteit van de gegevens binnen identiteiten, inclusief de status van de identiteiten van uw gegevens. Deze zelfstudie bevat instructies over hoe u het dashboard voor bewaking kunt gebruiken om de identiteiten van uw gegevens te controleren via de gebruikersinterface van het Experience Platform, zodat u de status van identiteitsverwerking kunt volgen.

## Aan de slag {#getting-started}

- [Gegevensstromen](../home.md): Dataflows zijn een voorstelling van gegevenstaken die gegevens over het Platform verplaatsen. Dataflows worden gevormd over verschillende diensten, die gegevens van bronschakelaars aan doeldatasets helpen bewegen, aan [!DNL Identity] en [!DNL Profile]en [!DNL Destinations].
   - [Dataflow-uitvoering](../../sources/notifications.md): De looppas van Dataflow is de terugkomende geplande banen die op de frequentieconfiguratie van geselecteerde dataflows worden gebaseerd.
- [Identiteitsservice](../../identity-service/home.md): Verbeter een beter beeld van individuele klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen.
- [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## Het dashboard voor het controleren van identiteiten {#identity-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_identity_processing"
>title="Identiteitsverwerking"
>abstract="De weergave Identiteitsverwerking bevat informatie over records die aan de identiteitsservice zijn toegevoegd, zoals het aantal toegevoegde identiteiten, gemaakte grafieken en bijgewerkte grafieken. Bekijk de metrische definitiegids voor meer informatie over metriek en grafieken."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_identity"
>title="Gegevens gegevensstroom"
>abstract="De Dataflow looppas detailpagina toont meer informatie over uw Dataslow van de Identiteit, met inbegrip van zijn organisatie ID en dataflow looppas identiteitskaart"

Om toegang te krijgen tot **[!UICONTROL Identities]** dashboard, selecteren **[!UICONTROL Monitoring]** in de linkernavigatie. Eén keer op de knop **[!UICONTROL Monitoring]** pagina, selecteert u de **[!UICONTROL Identities]** kaart.

![De identiteitskaart van Identiteiten. Informatie over het aantal ontvangen verslagen, het aantal opgenomen verslagen, en het succestarief wordt getoond.](../assets/ui/monitor-identities/focus-card.png)

Over de hoofdlijnen **[!UICONTROL Identities]** dashboard, het **[!UICONTROL Identities]** kaart bevat informatie over het totale aantal ontvangen records, het aantal opgenomen records en het succespercentage van de opname van records.

Het dashboard zelf bevat gegevens over identiteitsverwerking. Standaard bevat het dashboard de identiteitsverwerkingsgegevens voor de bronnen van uw organisatie gedurende de laatste 24 uur.

![Het dashboard Identiteiten. De informatie over het aantal verslagen die per bron worden ontvangen wordt getoond.](../assets/ui/monitor-identities/sources.png)

De [!UICONTROL Identity processing] pagina bevat informatie over records die aan worden toegevoegd [!DNL Identity Service], inclusief het aantal toegevoegde identiteiten, gemaakte grafieken en bijgewerkte grafieken.

De volgende metriek is beschikbaar voor deze dashboardmening:

| Identiteitswaarden | Beschrijving |
| ---------------- | ----------- |
| **[!UICONTROL Records received]** | Het aantal records dat wordt ontvangen van data Lake. |
| **[!UICONTROL Records failed]** | Het aantal records dat niet in het Platform is opgenomen als gevolg van fouten in de gegevens. |
| **[!UICONTROL Records skipped]** | Het aantal records dat is ingesloten, maar niet in [!DNL Identity Service] omdat de recordrij slechts één id bevat. |
| **[!UICONTROL Records ingested]** | Het aantal records waarin [!DNL Identity Service]. |
| **[!UICONTROL Identities added]** | Het aantal netto nieuwe id&#39;s dat wordt toegevoegd aan [!DNL Identity Service]. |
| **[!UICONTROL Graphs created]** | Het aantal netto nieuwe identiteitsgrafieken dat is gemaakt in [!DNL Identity Service]. |
| **[!UICONTROL Graphs updated]** | Het aantal bestaande identiteitsgrafieken dat met nieuwe randen is bijgewerkt. |
| **[!UICONTROL Total failed dataflows]** | Het aantal dataflow wordt uitgevoerd dat is mislukt. |

U kunt het filterpictogram selecteren ![Filterpictogram](../assets/ui/monitor-identities/filter.png) naast de bronnaam om de verwerkingsinformatie van de Identiteit voor de gegevens van die geselecteerde bron te zien.

![Het filterpictogram wordt gemarkeerd. Als u dit pictogram selecteert, kunt u de gegevensstromen van de geselecteerde bron weergeven.](../assets/ui/monitor-identities/sources-filter.png)

U kunt ook **[!UICONTROL Dataflows]** in de schakeloptie voor de gegevens over identiteitsverwerking van uw organisatie gedurende de laatste 24 uur.

![Het dashboard Identiteiten. Er wordt informatie weergegeven over het aantal identiteiten dat per gegevensstroom wordt ontvangen.](../assets/ui/monitor-identities/dataflows.png)

De volgende metriek is beschikbaar voor deze dashboardmening:

| Metrisch | Beschrijving |
| -------| ----------- |
| **[!UICONTROL Dataflow]** | De naam van de gegevensstroom. |
| **[!UICONTROL Dataset]** | De naam van de dataset die dataflow opneemt aan. |
| **[!UICONTROL Source name]** | De naam van de bron waartoe de gegevensstroom behoort. |
| **[!UICONTROL Records received]** | Het aantal records dat wordt ontvangen van data Lake. |
| **[!UICONTROL Records failed]** | Het aantal records dat niet in het Platform is opgenomen als gevolg van fouten in de gegevens. |
| **[!UICONTROL Records skipped]** | Het aantal records dat is ingesloten, maar niet in [!DNL Identity Service] omdat de recordrij slechts één id bevat. |
| **[!UICONTROL Records ingested]** | Het aantal records waarin [!DNL Identity Service]. |
| **[!UICONTROL Total records]** | Het totale aantal records, inclusief mislukte records, overgeslagen records, toegevoegde identiteiten en gedupliceerde records. |
| **[!UICONTROL Identities added]** | Het aantal netto nieuwe id&#39;s dat wordt toegevoegd aan [!DNL Identity Service]. |
| **[!UICONTROL Graphs created]** | Het aantal netto nieuwe identiteitsgrafieken dat is gemaakt in [!DNL Identity Service]. |
| **[!UICONTROL Graphs updated]** | Het aantal bestaande identiteitsgrafieken dat met nieuwe randen is bijgewerkt. |
| **[!UICONTROL Total failed dataflows]** | Het aantal dataflow wordt uitgevoerd dat is mislukt. |

Filterpictogram selecteren ![filter](../assets/ui/monitor-identities/filter.png) naast de dataflow run start time om meer informatie over uw [!DNL Identity] dataflow run.

![Het filterpictogram wordt gemarkeerd. Als u dit pictogram selecteert, kunt u details weergeven over de geselecteerde gegevensstroom.](../assets/ui/monitor-identities/dataflows-filter.png)

De [!UICONTROL Dataflow run details] pagina geeft meer informatie over uw [!DNL Identity] dataflow-run, inclusief de organisatie-id en de uitvoerings-id voor dataflow. Op deze pagina ziet u ook de bijbehorende foutcode en het foutbericht van [!DNL Identity Service], indien er fouten optreden in het innameproces.

![Er wordt een dashboard weergegeven met gedetailleerde informatie over de geselecteerde gegevensstroom.](../assets/ui/monitor-identities/dataflow-run-details.png)

De volgende metriek is beschikbaar voor deze dashboardmening:

| Metrisch | Beschrijving |
| -------| ----------- |
| **[!UICONTROL Records received]** | Het aantal records dat wordt ontvangen van data Lake. |
| **[!UICONTROL Records failed]** | Het aantal records dat niet in het Platform is opgenomen als gevolg van fouten in de gegevens. |
| **[!UICONTROL Records skipped]** | Het aantal records dat is ingesloten, maar niet in [!DNL Identity Service] omdat de recordrij slechts één id bevat. |
| **[!UICONTROL Records ingested]** | Het aantal records waarin [!DNL Identity Service]. |
| **[!UICONTROL Identities added]** | Het aantal netto nieuwe id&#39;s dat wordt toegevoegd aan [!DNL Identity Service]. |
| **[!UICONTROL Graphs created]** | Het aantal netto nieuwe identiteitsgrafieken dat is gemaakt in [!DNL Identity Service]. |
| **[!UICONTROL Graphs updated]** | Het aantal bestaande identiteitsgrafieken dat met nieuwe randen is bijgewerkt. |
| **[!UICONTROL Status]** | Bepaalt de algemene status van een gegevensstroom. De mogelijke statuswaarden zijn: <ul><li>`Success`: Geeft aan dat een gegevensstroom actief is en gegevens opneemt volgens het schema dat is opgegeven.</li><li>`Failed`: Geeft aan dat het activeringsproces van een gegevensstroom is onderbroken door fouten. </li><li>`Processing`: Geeft aan dat de gegevensstroom nog niet actief is. Deze status wordt vaak direct na het maken van een nieuwe gegevensstroom aangetroffen.</li></ul> |
| **[!UICONTROL Dataflow run start]** | De datum en de tijd dataflow begon te lopen. |
| **[!UICONTROL Last updated]** | De datum en tijd de dataflow laatst bijgewerkt. |
| **[!UICONTROL Error summary]** | Als de dataflow-run is mislukt, wordt een foutcode en een overzicht weergegeven van waarom de dataflow-run is mislukt. |
| **[!UICONTROL Dataflow run ID]** | De id van de gegevensstroom wordt uitgevoerd. |
| **[!UICONTROL IMS org ID]** | De organisatie-id waartoe de dataflow-run behoort. |

Bovendien kunt u de schakeloptie selecteren om de records te bekijken die zijn mislukt of de records die zijn overgeslagen. De sectie Fouten bevat details over de foutcode en het aantal mislukte of uitgesloten records.