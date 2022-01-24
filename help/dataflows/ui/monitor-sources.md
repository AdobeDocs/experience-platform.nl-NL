---
keywords: Experience Platform;thuis;populaire onderwerpen;monitorrekeningen;monitordataflows;dataflows;bronnen
description: Deze zelfstudie biedt stappen om uw gegevensstroom te controleren met behulp van zowel de geaggregeerde controleweergave als de cross-service bewaking.
solution: Experience Platform
title: De Dataflows van de monitor voor Bronnen in UI
topic-legacy: overview
type: Tutorial
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: 38e56beacd8857648abbbf20f4a5c4941ff779ee
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 0%

---

# Dataflows controleren voor bronnen in de gebruikersinterface

>[!IMPORTANT]
>
>Streaming bronnen, zoals de [HTTP API-bron](../../sources/connectors/streaming/http.md) worden momenteel niet ondersteund door het dashboard voor bewaking. Op dit moment kunt u het dashboard alleen gebruiken om batchbronnen te controleren.

In Adobe Experience Platform worden gegevens uit een groot aantal verschillende bronnen opgenomen, binnen het Experience Platform geanalyseerd en geactiveerd voor een groot aantal verschillende bestemmingen. Platform maakt het proces om deze potentieel niet-lineaire stroom van gegevens te volgen gemakkelijker door transparantie van gegevensstromen te verstrekken.

Het controledashboard voorziet u van een visuele vertegenwoordiging van de reis van een gegevensstroom. U kunt een samengevoegde controlemening gebruiken en verticaal van het bronniveau, aan een dataflow, en aan een dataflow looppas navigeren, toestaand u om de overeenkomstige metriek te bekijken die tot het succes of de mislukking van een dataflow bijdragen. U kunt ook de cross-service controlecapaciteit van het dashboard voor controle gebruiken om de reis van een gegevensstroom van een bron te controleren, aan [!DNL Identity Service]en [!DNL Profile].

Deze zelfstudie biedt stappen om uw gegevensstroom te controleren met behulp van zowel de geaggregeerde controleweergave als de cross-service bewaking.

## Aan de slag {#getting-started}

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Gegevensstromen](../home.md): Dataflows zijn een voorstelling van gegevenstaken die gegevens over het Platform verplaatsen. Dataflows worden gevormd over verschillende diensten, die gegevens van bronschakelaars aan doeldatasets helpen bewegen, aan [!DNL Identity] en [!DNL Profile]en [!DNL Destinations].
   * [Dataflow-uitvoering](../../sources/notifications.md): De looppas van Dataflow is de terugkomende geplande banen die op de frequentieconfiguratie van geselecteerde dataflows worden gebaseerd.
* [Bronnen](../../sources/home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Identiteitsservice](../../identity-service/home.md): Verbeter een beter beeld van individuele klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen.
* [Klantprofiel in realtime](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [Sandboxen](../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## Geaggregeerde monitoringweergave {#aggregated-monitoring-view}

>[!CONTEXTUALHELP]
>id="platform_monitoring_source_ingestion"
>title="Bron invoegen"
>abstract="De bronverwerking bevat informatie over de status van de gegevensactiviteit en metriek in de dienst van het gegevensmeer, met inbegrip van opgenomen verslagen en ontbroken verslagen. Bekijk de metrische definitiegids voor meer informatie over metriek en grafieken."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_ingestion"
>title="Gegevens gegevensstroom"
>abstract="De bronverwerking bevat informatie over de status van de gegevensactiviteit en metriek in de dienst van het gegevensmeer, met inbegrip van opgenomen verslagen en ontbroken verslagen. Bekijk de metrische definitiegids voor meer informatie over metriek en grafieken."
>text="Learn more in documentation"

In de [UI Platform](https://platform.adobe.com), selecteert u **[!UICONTROL Monitoring]** van de linkernavigatie om tot [!UICONTROL Monitoring] dashboard. De [!UICONTROL Monitoring] het dashboard bevat metriek en informatie over alle brongegevens, met inbegrip van inzicht in de gezondheid van gegevensverkeer van een bron aan [!DNL Identity Service]en [!DNL Profile].

In het midden van het dashboard bevindt zich de [!UICONTROL Source ingestion] paneel, dat metriek en grafieken bevat die gegevens tonen over opgenomen verslagen en ontbroken verslagen.

![bewakingsdashboard](../assets/ui/monitor-sources/monitoring-dashboard.png)

Standaard bevatten de weergegeven gegevens de innamesnelheden van de laatste 24 uur. Selecteren **[!UICONTROL Last 24 hours]** om het tijdkader van getoonde verslagen aan te passen.

![wijzigingsdatum](../assets/ui/monitor-sources/change-date.png)

Er wordt een kalenderpop-upvenster weergegeven met opties voor alternatieve ingstijd. Selecteren **[!UICONTROL Last 30 days]** en selecteer vervolgens **[!UICONTROL Apply]**

![aanpassen-tijdframe](../assets/ui/monitor-sources/adjust-timeframe.png)

De grafieken zijn standaard ingeschakeld en u kunt ze uitschakelen om de lijst met bronnen hieronder uit te vouwen. Selecteer **[!UICONTROL Metrics and graphs]** schakelen om de grafieken uit te schakelen.

![metriek en grafieken](../assets/ui/monitor-sources/metrics-graphs.png)

| Bron invoegen | Beschrijving |
| ---------------- | ----------- |
| [!UICONTROL Records ingested ] | Het totale aantal records dat wordt ingevoerd. |
| [!UICONTROL Records failed] | Het totale aantal records dat niet is opgenomen als gevolg van fouten in de gegevens. |
| [!UICONTROL Total failed dataflows] | Het totale aantal gegevensstromen met a `failed` status. |

In de lijst met brongegevens worden alle bronnen weergegeven die ten minste één bestaande account bevatten. De lijst bevat ook informatie over de opnamesnelheid van elke bron, het aantal mislukte records en het totale aantal mislukte gegevensstromen op basis van het tijdkader dat u hebt toegepast.

![bron-opname](../assets/ui/monitor-sources/source-ingestion.png)

Selecteer **[!UICONTROL My sources]** en selecteer vervolgens de gewenste categorie in het vervolgkeuzemenu. Als u zich bijvoorbeeld wilt concentreren op cloudopslagsystemen, selecteert u  **[!UICONTROL Cloud storage]**

![per categorie](../assets/ui/monitor-sources/sort-by-category.png)

Selecteer **[!UICONTROL Dataflows]**.

![view-all-dataflows](../assets/ui/monitor-sources/view-all-dataflows.png)

U kunt ook een bron invoeren in de zoekbalk om één bron te isoleren. Wanneer de bron is geïdentificeerd, selecteert u het filterpictogram ![filter](../assets/ui/monitor-sources/filter.png) naast het om een lijst van zijn actieve dataflows te zien.

![zoeken](../assets/ui/monitor-sources/search.png)

Er wordt een lijst met gegevensstromen weergegeven. Selecteer **[!UICONTROL Show failures only]**.

![show-failure-only](../assets/ui/monitor-sources/show-failures-only.png)

Zoek de gegevensstroom die u wilt controleren en selecteer vervolgens het filterpictogram ![filter](../assets/ui/monitor-sources/filter.png) naast het, om meer informatie over zijn looppasstatus te zien.

![dataflow](../assets/ui/monitor-sources/dataflow.png)

De dataflow run pagina geeft informatie weer over de begindatum, grootte van de gegevens, status en de duur van de verwerkingstijd van de dataflow. Filterpictogram selecteren ![filter](../assets/ui/monitor-sources/filter.png) naast de dataflow runtime begintijd om zijn dataflow loopingdetails te zien.

![dataflow-run-start](../assets/ui/monitor-sources/dataflow-run-start.png)

De [!UICONTROL Dataflow run details] op de pagina wordt informatie weergegeven over de metagegevens van de gegevensstroom, de status van gedeeltelijke invoer en het overzicht van de fouten. Het foutenoverzicht bevat de specifieke fout op hoofdniveau die toont bij welke stap het innameproces een fout tegenkwam.

Schuif omlaag om specifiekere informatie over de fout te zien die optrad.

![details dataflow-run](../assets/ui/monitor-sources/dataflow-run-details.png)

De [!UICONTROL Dataflow run errors] geeft de specifieke fout- en foutcode weer die tot de fout bij het opnemen van de gegevensstroom heeft geleid. In dit scenario is een maptransformatiefout opgetreden, wat resulteert in de fout van 24 records.

Selecteren **[!UICONTROL Files]** voor meer informatie .

![dataflow-run-fouten](../assets/ui/monitor-sources/dataflow-run-errors.png)

De [!UICONTROL Files] bevat informatie over de naam en het pad van het bestand.

Selecteer **[!UICONTROL Preview error diagnostics]**.

![bestanden](../assets/ui/monitor-sources/files.png)

De [!UICONTROL Error diagnostics preview] wordt weergegeven met een voorvertoning van maximaal 100 fouten in de gegevensstroom. U kunt **[!UICONTROL Download]** om een krullopdracht terug te winnen, die dan u toestaat om de foutendiagnostiek te downloaden.

Als u klaar bent, selecteert u **[!UICONTROL Close]**

![error-diagnostics](../assets/ui/monitor-sources/error-diagnostics.png)

U kunt het broodkruimelsysteem bij de hoogste kopbal gebruiken om uw weg terug naar te navigeren [!UICONTROL Monitoring] dashboard. Selecteren **[!UICONTROL Run start: 2/14/2021, 9:47 PM]** om terug te keren naar de vorige pagina en vervolgens **[!UICONTROL Dataflow: Loyalty Data Ingestion Demo - Failed]** om terug te keren naar de pagina met gegevensstromen.

![broodkruimels](../assets/ui/monitor-sources/breadcrumbs.png)

## Controle tussen verschillende services {#cross-service-monitoring}

Het bovenste deel van het dashboard bevat een voorstelling van de innamestroom van het bronniveau tot [!DNL Identity Service]en [!DNL Profile]. Elke cel bevat een puntmarkering die de aanwezigheid aangeeft van fouten die zich in dat stadium van inname hebben voorgedaan. Een groene stip betekent een foutloze opname, terwijl een rode stip betekent dat er een fout is opgetreden in dat specifieke stadium van inname.

![cross-service-monitoring](../assets/ui/monitor-sources/cross-service-monitoring.png)

Zoek op de pagina met gegevensstromen een geslaagde gegevensstroom en selecteer het filterpictogram ![filter](../assets/ui/monitor-sources/filter.png) naast het, om zijn dataflow looppas informatie te zien.

![dataflow-success](../assets/ui/monitor-sources/dataflow-success.png)

De [!UICONTROL Source ingestion] Deze pagina bevat informatie die de geslaagde inname van uw gegevensstroom bevestigt. Van hier, kunt u beginnen de reis van uw gegevensstroom van bron-niveau te controleren, aan [!DNL Identity Service]en vervolgens naar [!DNL Profile].

Selecteren **[!UICONTROL Identities]** om inname te zien in de [!UICONTROL Identities] in.

![bronnen](../assets/ui/monitor-sources/sources.png)

### [!DNL Identity] cijfers {#identity-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_identity_processing"
>title="Identiteitsverwerking"
>abstract="Identiteitsverwerking bevat gegevens over records die aan de identiteitsdienst zijn toegevoegd, zoals het aantal toegevoegde identiteiten, gemaakte grafieken en bijgewerkte grafieken. Bekijk de metrische definitiegids voor meer informatie over metriek en grafieken."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_identity"
>title="Gegevens gegevensstroom"
>abstract="Op de pagina met details over uitvoering van de Dataflow-software wordt meer informatie weergegeven over de uitvoering van uw identiteitsgegevens, waaronder de IMS-organisatie-id en de uitvoerid van de dataflow."

De [!UICONTROL Identity processing] pagina bevat informatie over records die aan worden toegevoegd [!DNL Identity Service], inclusief het aantal toegevoegde identiteiten, gemaakte grafieken en bijgewerkte grafieken.

Filterpictogram selecteren ![filter](../assets/ui/monitor-sources/filter.png) naast de dataflow run start time om meer informatie over uw [!DNL Identity] dataflow run.

![identiteiten](../assets/ui/monitor-sources/identities.png)

| Identiteitswaarden | Beschrijving |
| ---------------- | ----------- |
| [!UICONTROL Records received] | Het aantal records dat is ontvangen van [!DNL Data Lake]. |
| [!UICONTROL Records failed] | Het aantal records dat niet in het Platform is opgenomen als gevolg van fouten in de gegevens. |
| [!UICONTROL Records skipped] | Het aantal records dat is ingesloten, maar niet in [!DNL Identity Service] omdat de recordrij slechts één id bevat. |
| [!UICONTROL Records ingested] | Het aantal records waarin [!DNL Identity Service]. |
| [!UICONTROL Total records] | Het totale aantal records, inclusief mislukte records, records overgeslagen, [!DNL Identities] toegevoegde, en gedupliceerde verslagen. |
| [!UICONTROL Identities added] | Het aantal netto nieuwe id&#39;s dat wordt toegevoegd aan [!DNL Identity Service]. |
| [!UICONTROL Graphs created] | Het aantal netto nieuwe identiteitsgrafieken dat is gemaakt in [!DNL Identity Service]. |
| [!UICONTROL Graphs updated] | Het aantal bestaande identiteitsgrafieken dat met nieuwe randen is bijgewerkt. |
| [!UICONTROL Failed dataflow runs] | Het aantal dataflow wordt uitgevoerd dat is mislukt. |
| [!UICONTROL Processing time] | De tijdstempel vanaf het begin van de opname tot aan de voltooiing. |
| [!UICONTROL Status] | Bepaalt de algemene status van een gegevensstroom. De mogelijke statuswaarden zijn: <ul><li>`Success`: Geeft aan dat een gegevensstroom actief is en gegevens opneemt volgens het schema dat is opgegeven.</li><li>`Failed`: Geeft aan dat het activeringsproces van een gegevensstroom is onderbroken door fouten. </li><li>`Processing`: Geeft aan dat de gegevensstroom nog niet actief is. Deze status wordt vaak direct na het maken van een nieuwe gegevensstroom aangetroffen.</li></ul> |

De [!UICONTROL Dataflow run details] pagina geeft meer informatie over uw [!DNL Identity] dataflow run, inclusief de IMS Org ID en de dataflow run ID. Op deze pagina ziet u ook de bijbehorende foutcode en het foutbericht van [!DNL Identity Service], indien er fouten optreden in het innameproces.

Selecteren **[!UICONTROL Run start: 2/14/2021, 9:47 PM]** om terug te keren naar de vorige pagina.

![identity-dataflow-run](../assets/ui/monitor-sources/identities-dataflow-run.png)

Van de [!UICONTROL Identity processing] pagina, selecteert u **[!UICONTROL Profiles]** om de status van records te zien die in de [!UICONTROL Profiles] in.

![profielen selecteren](../assets/ui/monitor-sources/select-profiles.png)

### [!DNL Profile] cijfers {#profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_profile_processing"
>title="Profielverwerking"
>abstract="De profielverwerking bevat informatie over verslagen die aan de dienst van het Profiel worden opgenomen, met inbegrip van het aantal gemaakte profielfragmenten, profielfragmenten bijgewerkt en het totale aantal profielfragmenten."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_profile"
>title="Gegevens gegevensstroom"
>abstract="Op de pagina met details over gegevensuitvoering in de dataflow-runtime van DataFlow wordt meer informatie weergegeven over uw profiel, waaronder de IMS-organisatie-id en de uitvoerings-id van de dataflow."

De [!UICONTROL Profile processing] pagina bevat informatie over records die aan worden toegevoegd [!DNL Profile], inclusief het aantal gemaakte profielfragmenten, de bijgewerkte profielfragmenten en het totale aantal profielfragmenten.

Filterpictogram selecteren ![filter](../assets/ui/monitor-sources/filter.png) naast de dataflow run start time om meer informatie over uw [!DNL Profile] dataflow run.

![profielen](../assets/ui/monitor-sources/profiles.png)

| Profielafmetingen | Beschrijving |
| --------------- | ----------- |
| [!UICONTROL Records received] | Het aantal records dat is ontvangen van [!DNL Data Lake]. |
| [!UICONTROL Records failed ] | Het aantal records dat is ingesloten, maar niet in [!DNL Profile] vanwege fouten. |
| [!UICONTROL Profile fragments added] | Het aantal netto nieuwe [!DNL Profile] fragmenten toegevoegd. |
| [!UICONTROL Profile fragments updated] | Het aantal bestaande [!DNL Profile] fragmenten bijgewerkt |
| [!UICONTROL Total Profile fragments] | The total number of records written into [!DNL Profile], met inbegrip van alle bestaande [!DNL Profile] fragmenten bijgewerkt en nieuw [!DNL Profile] gemaakte fragmenten. |
| [!UICONTROL Failed dataflow runs] | Het aantal dataflow wordt uitgevoerd dat is mislukt. |
| [!UICONTROL Processing time] | De tijdstempel vanaf het begin van de opname tot aan de voltooiing. |
| [!UICONTROL Status] | Bepaalt de algemene status van een gegevensstroom. De mogelijke statuswaarden zijn: <ul><li>`Success`: Geeft aan dat een gegevensstroom actief is en gegevens opneemt volgens het schema dat is opgegeven.</li><li>`Failed`: Geeft aan dat het activeringsproces van een gegevensstroom is onderbroken door fouten. </li><li>`Processing`: Geeft aan dat de gegevensstroom nog niet actief is. Deze status wordt vaak direct na het maken van een nieuwe gegevensstroom aangetroffen.</li></ul> |

De [!UICONTROL Dataflow run details] pagina geeft meer informatie over uw [!DNL Profile] dataflow run, inclusief de IMS Org ID en de dataflow run ID. Op deze pagina ziet u ook de bijbehorende foutcode en het foutbericht van [!DNL Profile], indien er fouten optreden in het innameproces.

![profiles-dataflow-run](../assets/ui/monitor-sources/profiles-dataflow-run.png)

## Volgende stappen {#next-steps}

Door deze zelfstudie te volgen, hebt u met succes de gegevensstroom van de opname van bron-niveau gecontroleerd, aan [!DNL Identity Service]en [!DNL Profile], met de **[!UICONTROL Monitoring]** dashboard. U hebt ook met succes fouten geïdentificeerd die tot de mislukking van gegevensstromen tijdens het innameproces hebben bijgedragen. Raadpleeg de volgende documenten voor meer informatie:

* [Overzicht van het realtime klantprofiel](../../profile/home.md)
* [Overzicht van de Data Science Workspace](../../data-science-workspace/home.md)
