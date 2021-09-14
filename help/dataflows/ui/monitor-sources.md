---
keywords: Experience Platform;thuis;populaire onderwerpen;monitorrekeningen;monitordataflows;dataflows;bronnen
description: Deze zelfstudie biedt stappen om uw gegevensstroom te controleren met behulp van zowel de geaggregeerde controleweergave als de cross-service bewaking.
solution: Experience Platform
title: De Dataflows van de monitor voor Bronnen in UI
topic-legacy: overview
type: Tutorial
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: a5b52d7cc2a39ce15b5a9568df14c86624ae069a
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 0%

---

# Dataflows controleren voor bronnen in de gebruikersinterface

>[!IMPORTANT]
>
>Streaming bronnen, zoals de [HTTP API-bron](../../sources/connectors/streaming/http.md), worden momenteel niet ondersteund door het dashboard voor bewaking. Op dit moment kunt u het dashboard alleen gebruiken om batchbronnen te controleren.

In Adobe Experience Platform worden gegevens uit een groot aantal verschillende bronnen opgenomen, binnen het Experience Platform geanalyseerd en geactiveerd voor een groot aantal verschillende bestemmingen. Platform maakt het proces om deze potentieel niet-lineaire stroom van gegevens te volgen gemakkelijker door transparantie van gegevensstromen te verstrekken.

Het controledashboard voorziet u van een visuele vertegenwoordiging van de reis van een gegevensstroom. U kunt een samengevoegde controlemening gebruiken en verticaal van het bronniveau, aan een dataflow, en aan een dataflow looppas navigeren, toestaand u om de overeenkomstige metriek te bekijken die tot het succes of de mislukking van een dataflow bijdragen. U kunt ook de cross-service controlecapaciteit van het monitoringdashboard gebruiken om de reis van een gegevensstroom van een bron, naar [!DNL Identity Service] en naar [!DNL Profile] te controleren.

Deze zelfstudie biedt stappen om uw gegevensstroom te controleren met behulp van zowel de geaggregeerde controleweergave als de cross-service bewaking.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Gegevensstroom](../home.md): Dataflows zijn een voorstelling van gegevenstaken die gegevens over het Platform verplaatsen. Dataflows worden geconfigureerd op verschillende services, waardoor gegevens van bronconnectors naar doelgegevenssets, naar [!DNL Identity] en [!DNL Profile] en naar [!DNL Destinations] worden verplaatst.
   * [Dataflow wordt uitgevoerd](../../sources/notifications.md): De looppas van Dataflow is de terugkomende geplande banen die op de frequentieconfiguratie van geselecteerde dataflows worden gebaseerd.
* [Bronnen](../../sources/home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Identiteitsservice](../../identity-service/home.md): Verbeter een beter beeld van individuele klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen.
* [Klantprofiel](../../profile/home.md) in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [Sandboxen](../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## Geaggregeerde monitoringweergave

In [Platform UI](https://platform.adobe.com), selecteer **[!UICONTROL Monitoring]** van de linkernavigatie om tot [!UICONTROL Monitoring] dashboard toegang te hebben. Het [!UICONTROL Monitoring] dashboard bevat metriek en informatie over alle brongegevens, met inbegrip van inzichten in de gezondheid van gegevensverkeer van een bron aan [!DNL Identity Service], en aan [!DNL Profile].

In het midden van het dashboard bevindt zich het [!UICONTROL Source ingestion]-deelvenster, dat metriek en grafieken bevat die gegevens weergeven over opgenomen records en records is mislukt.

![bewakingsdashboard](../assets/ui/monitor-sources/monitoring-dashboard.png)

Standaard bevatten de weergegeven gegevens de innamesnelheden van de laatste 24 uur. Selecteer **[!UICONTROL Last 24 hours]** om het tijdkader van getoonde verslagen aan te passen.

![wijzigingsdatum](../assets/ui/monitor-sources/change-date.png)

Er wordt een kalenderpop-upvenster weergegeven met opties voor alternatieve ingstijd. Selecteer **[!UICONTROL Last 30 days]** en selecteer **[!UICONTROL Apply]**

![aanpassen-tijdframe](../assets/ui/monitor-sources/adjust-timeframe.png)

De grafieken zijn standaard ingeschakeld en u kunt ze uitschakelen om de lijst met bronnen hieronder uit te vouwen. Selecteer **[!UICONTROL Metrics and graphs]** knevel om de grafieken onbruikbaar te maken.

![metriek en grafieken](../assets/ui/monitor-sources/metrics-graphs.png)

| Bron invoegen | Beschrijving |
| ---------------- | ----------- |
| [!UICONTROL Records ingested ] | Het totale aantal records dat wordt ingevoerd. |
| [!UICONTROL Records failed] | Het totale aantal records dat niet is opgenomen als gevolg van fouten in de gegevens. |
| [!UICONTROL Total failed dataflows] | Het totale aantal gegevens met een status `failed`. |

In de lijst met brongegevens worden alle bronnen weergegeven die ten minste één bestaande account bevatten. De lijst bevat ook informatie over de opnamesnelheid van elke bron, het aantal mislukte records en het totale aantal mislukte gegevensstromen op basis van het tijdkader dat u hebt toegepast.

![bron-opname](../assets/ui/monitor-sources/source-ingestion.png)

Als u de lijst met bronnen wilt doorlopen, selecteert u **[!UICONTROL My sources]** en selecteert u vervolgens de gewenste categorie in het vervolgkeuzemenu. Selecteer **[!UICONTROL Cloud storage]** om bijvoorbeeld de focus op cloudopslagsystemen te plaatsen

![per categorie](../assets/ui/monitor-sources/sort-by-category.png)

Selecteer **[!UICONTROL Dataflows]** om alle bestaande gegevensstromen uit alle bronnen weer te geven.

![view-all-dataflows](../assets/ui/monitor-sources/view-all-dataflows.png)

U kunt ook een bron invoeren in de zoekbalk om één bron te isoleren. Wanneer de bron is geïdentificeerd, selecteert u het filterpictogram ![filter](../assets/ui/monitor-sources/filter.png) naast het om een lijst met de actieve dataflows te zien.

![zoeken](../assets/ui/monitor-sources/search.png)

Er wordt een lijst met gegevensstromen weergegeven. Selecteer **[!UICONTROL Show failures only]** om de lijst te beperken en de focus op gegevensstromen met fouten te beperken.

![show-failure-only](../assets/ui/monitor-sources/show-failures-only.png)

Zoek de gegevensstroom die u wilt controleren en selecteer dan het filterpictogram ![filter](../assets/ui/monitor-sources/filter.png) naast het, om meer informatie over zijn looppasstatus te zien.

![dataflow](../assets/ui/monitor-sources/dataflow.png)

De dataflow run pagina geeft informatie weer over de begindatum, grootte van de gegevens, status en de duur van de verwerkingstijd van de dataflow. Selecteer het filterpictogram ![filter](../assets/ui/monitor-sources/filter.png) naast de dataflow runtime begintijd om zijn gegevens van de dataflow looppas te zien.

![dataflow-run-start](../assets/ui/monitor-sources/dataflow-run-start.png)

Op de pagina [!UICONTROL Dataflow run details] wordt informatie weergegeven over de metagegevens van de gegevensstroom, de status van gedeeltelijke invoer en het overzicht van de fouten. Het foutenoverzicht bevat de specifieke fout op hoofdniveau die toont bij welke stap het innameproces een fout tegenkwam.

Schuif omlaag om specifiekere informatie over de fout te zien die optrad.

![details dataflow-run](../assets/ui/monitor-sources/dataflow-run-details.png)

In het deelvenster [!UICONTROL Dataflow run errors] worden de specifieke fout- en foutcode weergegeven die tot de fout bij het opnemen van de gegevensstroom heeft geleid. In dit scenario is een maptransformatiefout opgetreden, wat resulteert in de fout van 24 records.

Selecteer **[!UICONTROL Files]** voor meer informatie.

![dataflow-run-fouten](../assets/ui/monitor-sources/dataflow-run-errors.png)

Het deelvenster [!UICONTROL Files] bevat informatie over de naam en het pad van het bestand.

Selecteer **[!UICONTROL Preview error diagnostics]** voor een gedetailleerdere weergave van de fout.

![bestanden](../assets/ui/monitor-sources/files.png)

Het venster [!UICONTROL Error diagnostics preview] wordt weergegeven met een voorvertoning van maximaal 100 fouten in de gegevensstroom. U kunt **[!UICONTROL Download]** selecteren om een krullbevel terug te winnen, dat dan u toestaat om de foutendiagnostiek te downloaden.

Als u klaar bent, selecteert u **[!UICONTROL Close]**

![error-diagnostics](../assets/ui/monitor-sources/error-diagnostics.png)

U kunt het broodkruimelsysteem bij de hoogste kopbal gebruiken om uw weg terug naar het [!UICONTROL Monitoring] dashboard te navigeren. Selecteer **[!UICONTROL Run start: 2/14/2021, 9:47 PM]** om naar de vorige pagina terug te keren en selecteer **[!UICONTROL Dataflow: Loyalty Data Ingestion Demo - Failed]** om naar de dataflows pagina terug te keren.

![broodkruimels](../assets/ui/monitor-sources/breadcrumbs.png)

## Controle tussen verschillende services

Het bovenste deel van het dashboard bevat een voorstelling van de innamestroom van het bron-niveau naar [!DNL Identity Service] en naar [!DNL Profile]. Elke cel bevat een puntmarkering die de aanwezigheid aangeeft van fouten die zich in dat stadium van inname hebben voorgedaan. Een groene stip betekent een foutloze opname, terwijl een rode stip betekent dat er een fout is opgetreden in dat specifieke stadium van inname.

![cross-service-monitoring](../assets/ui/monitor-sources/cross-service-monitoring.png)

Van de dataflows pagina, bepaal de plaats van een succesvolle dataflow en selecteer het filterpictogram ![filter](../assets/ui/monitor-sources/filter.png) naast het, om zijn dataflow looplooppasinformatie te zien.

![dataflow-success](../assets/ui/monitor-sources/dataflow-success.png)

De [!UICONTROL Source ingestion] pagina bevat informatie die de succesvolle opname van uw gegevensstroom bevestigt. Van hier, kunt u beginnen de reis van uw gegevensstroom van bron-niveau, aan [!DNL Identity Service], en dan aan [!DNL Profile] te controleren.

Selecteer **[!UICONTROL Identities]** om inname in het [!UICONTROL Identities] werkgebied te zien.

![bronnen](../assets/ui/monitor-sources/sources.png)

### [!DNL Identity] cijfers

De pagina [!UICONTROL Identity processing] bevat informatie over records die aan [!DNL Identity Service] worden toegevoegd, zoals het aantal toegevoegde identiteiten, gemaakte grafieken en bijgewerkte grafieken.

Selecteer het filterpictogram ![filter](../assets/ui/monitor-sources/filter.png) naast de dataflow runtime begintijd om meer informatie over uw [!DNL Identity] dataflow run te zien.

![identiteiten](../assets/ui/monitor-sources/identities.png)

| Identiteitswaarden | Beschrijving |
| ---------------- | ----------- |
| [!UICONTROL Records received] | Het aantal records dat is ontvangen van [!DNL Data Lake]. |
| [!UICONTROL Records failed] | Het aantal records dat niet in het Platform is opgenomen als gevolg van fouten in de gegevens. |
| [!UICONTROL Records skipped] | Het aantal records dat is ingevoerd, maar niet in [!DNL Identity Service] omdat de recordrij slechts één id bevat. |
| [!UICONTROL Records ingested] | Het aantal records dat wordt ingevoerd in [!DNL Identity Service]. |
| [!UICONTROL Total records] | Het totale aantal records, inclusief records is mislukt, records zijn overgeslagen, [!DNL Identities] heeft records toegevoegd en gedupliceerde records bevat. |
| [!UICONTROL Identities added] | Het aantal netto nieuwe id&#39;s dat aan [!DNL Identity Service] wordt toegevoegd. |
| [!UICONTROL Graphs created] | Het aantal netto nieuwe identiteitsgrafieken die in [!DNL Identity Service] worden gecreeerd. |
| [!UICONTROL Graphs updated] | Het aantal bestaande identiteitsgrafieken dat met nieuwe randen is bijgewerkt. |
| [!UICONTROL Failed dataflow runs] | Het aantal dataflow wordt uitgevoerd dat is mislukt. |
| [!UICONTROL Processing time] | De tijdstempel vanaf het begin van de opname tot aan de voltooiing. |
| [!UICONTROL Status] | Bepaalt de algemene status van een gegevensstroom. De mogelijke statuswaarden zijn: <ul><li>`Success`: Geeft aan dat een gegevensstroom actief is en gegevens opneemt volgens het schema dat is opgegeven.</li><li>`Failed`: Geeft aan dat het activeringsproces van een gegevensstroom is onderbroken door fouten. </li><li>`Processing`: Geeft aan dat de gegevensstroom nog niet actief is. Deze status wordt vaak direct na het maken van een nieuwe gegevensstroom aangetroffen.</li></ul> |

De [!UICONTROL Dataflow run details] pagina toont meer informatie over uw [!DNL Identity] dataflow looppas, met inbegrip van zijn IMS Org ID en dataflow looppas identiteitskaart Deze pagina toont ook de overeenkomstige foutencode en foutenmelding die door [!DNL Identity Service] wordt verstrekt, als om het even welke fouten in het innameproces voorkomen.

Selecteer **[!UICONTROL Run start: 2/14/2021, 9:47 PM]** om naar de vorige pagina terug te keren.

![identity-dataflow-run](../assets/ui/monitor-sources/identities-dataflow-run.png)

Selecteer [!UICONTROL Identity processing] op de pagina **[!UICONTROL Profiles]** om de status van recordinvoer in het werkgebied [!UICONTROL Profiles] weer te geven.

![profielen selecteren](../assets/ui/monitor-sources/select-profiles.png)

### [!DNL Profile] cijfers

De pagina [!UICONTROL Profile processing] bevat informatie over records die aan [!DNL Profile] worden toegevoegd, zoals het aantal gemaakte profielfragmenten, de bijgewerkte profielfragmenten en het totale aantal profielfragmenten.

Selecteer het filterpictogram ![filter](../assets/ui/monitor-sources/filter.png) naast de dataflow runtime begintijd om meer informatie over uw [!DNL Profile] dataflow run te zien.

![profielen](../assets/ui/monitor-sources/profiles.png)

| Profielafmetingen | Beschrijving |
| --------------- | ----------- |
| [!UICONTROL Records received] | Het aantal records dat is ontvangen van [!DNL Data Lake]. |
| [!UICONTROL Records failed ] | Het aantal records dat is ingevoerd, maar niet in [!DNL Profile] vanwege fouten. |
| [!UICONTROL Profile fragments added] | Het aantal netto nieuwe [!DNL Profile] fragmenten toegevoegd. |
| [!UICONTROL Profile fragments updated] | Het aantal bestaande [!DNL Profile] bijgewerkte fragmenten |
| [!UICONTROL Total Profile fragments] | Het totale aantal records dat in [!DNL Profile] is geschreven, inclusief alle bestaande [!DNL Profile] fragmenten die zijn bijgewerkt en nieuwe [!DNL Profile] fragmenten die zijn gemaakt. |
| [!UICONTROL Failed dataflow runs] | Het aantal dataflow wordt uitgevoerd dat is mislukt. |
| [!UICONTROL Processing time] | De tijdstempel vanaf het begin van de opname tot aan de voltooiing. |
| [!UICONTROL Status] | Bepaalt de algemene status van een gegevensstroom. De mogelijke statuswaarden zijn: <ul><li>`Success`: Geeft aan dat een gegevensstroom actief is en gegevens opneemt volgens het schema dat is opgegeven.</li><li>`Failed`: Geeft aan dat het activeringsproces van een gegevensstroom is onderbroken door fouten. </li><li>`Processing`: Geeft aan dat de gegevensstroom nog niet actief is. Deze status wordt vaak direct na het maken van een nieuwe gegevensstroom aangetroffen.</li></ul> |

De [!UICONTROL Dataflow run details] pagina toont meer informatie over uw [!DNL Profile] dataflow looppas, met inbegrip van zijn IMS Org ID en dataflow looppas identiteitskaart Deze pagina toont ook de overeenkomstige foutencode en foutenmelding die door [!DNL Profile] wordt verstrekt, als om het even welke fouten in het innameproces voorkomen.

![profiles-dataflow-run](../assets/ui/monitor-sources/profiles-dataflow-run.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes de gegevensstroom van de opname van bron-niveau, aan [!DNL Identity Service], en aan [!DNL Profile] gecontroleerd, gebruikend het **[!UICONTROL Monitoring]** dashboard. U hebt ook met succes fouten geïdentificeerd die tot de mislukking van gegevensstromen tijdens het innameproces hebben bijgedragen. Raadpleeg de volgende documenten voor meer informatie:

* [Overzicht van het realtime klantprofiel](../../profile/home.md)
* [Overzicht van de Data Science Workspace](../../data-science-workspace/home.md)
