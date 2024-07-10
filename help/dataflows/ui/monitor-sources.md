---
description: Leer hoe te om het controledashboard te gebruiken om gegevens te controleren die van bronnen worden ingebed.
title: De Dataflows van de monitor voor Bronnen in UI
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: 51f8a8c77518a0b2e9e4b914c891f97433db1ef2
workflow-type: tm+mt
source-wordcount: '1229'
ht-degree: 0%

---

# Dataflows controleren voor bronnen in de gebruikersinterface

>[!IMPORTANT]
>
>Streaming bronnen, zoals de [HTTP API-bron](../../sources/connectors/streaming/http.md) worden momenteel niet ondersteund door het dashboard voor bewaking. Op dit moment kunt u het dashboard alleen gebruiken om batchbronnen te controleren.

Lees dit document om te leren hoe te om het controledashboard te gebruiken om uw brongegevens in de UI van het Experience Platform te controleren.

## Aan de slag {#get-started}

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Gegevensstromen](../home.md): Gegevensstromen zijn een weergave van gegevenstaken die gegevens verplaatsen over het hele platform. Dataflows worden gevormd over verschillende diensten, die gegevens van bronschakelaars aan doeldatasets helpen bewegen, aan [!DNL Identity] en [!DNL Profile], en [!DNL Destinations].
   * [Dataflow-uitvoering](../../sources/notifications.md): De looppas van Dataflow is de terugkomende geplande banen die op de frequentieconfiguratie van geselecteerde dataflows worden gebaseerd.
* [Bronnen](../../sources/home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de platformservices.
* [Identiteitsservice](../../identity-service/home.md): Verbeter een beter beeld van individuele klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen.
* [Klantprofiel in realtime](../../profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
* [Sandboxen](../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één platforminstantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## Brongegevens controleren met het dashboard voor bewaking

>[!CONTEXTUALHELP]
>id="platform_monitoring_source_ingestion"
>title="Source ingestion"
>abstract="De weergave Source-opname bevat informatie over de status van de gegevensactiviteit en metriek in de datameerservice, inclusief opgenomen records en mislukte records. Bekijk de metrische definitiegids voor meer informatie over metriek en grafieken."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_ingestion"
>title="Gegevens gegevensstroom uitvoeren"
>abstract="De bronverwerking bevat informatie over de status van de gegevensactiviteit en metriek in de dienst van het gegevensmeer, met inbegrip van opgenomen verslagen en ontbroken verslagen. Bekijk de metrische definitiegids voor meer informatie over metriek en grafieken."
>text="Learn more in documentation"

<!-- In the [Platform UI](https://platform.adobe.com), select **[!UICONTROL Monitoring]** from the left navigation to access the [!UICONTROL Monitoring] dashboard. The [!UICONTROL Monitoring] dashboard contains metrics and information on all sources dataflows, including insights into the health of data traffic from a source to [!DNL Identity Service], and to [!DNL Profile].

At the center of the dashboard is the [!UICONTROL Source ingestion] panel, which contains metrics and graphs that display data on records ingested and records failed. -->

Selecteer in het dashboard voor bewaking de optie [!UICONTROL Sources] in de hoofdkop om het dashboard bij te werken met een weergave van de gegevensstroomopnamesnelheid van uw bronnen.

![Het controledashboard met de geselecteerde bronkaart.](../assets/ui/monitor-sources/sources.png)

De [!UICONTROL Ingestion rate] de grafiek toont uw tarief van de gegevensopname die op uw gevormd tijdkader wordt gebaseerd. Standaard geeft het dashboard voor de bewaking de innamesnelheid van de laatste 24 uur weer. Voor stappen op hoe te om uw tijdkader te vormen, lees de gids op [bewakingstijd configureren](monitor.md#configure-monitoring-time-frame).

De grafiek wordt standaard weergegeven. Als u de grafiek wilt verbergen, selecteert u **[!UICONTROL Metrics and graphs]** om de knevel onbruikbaar te maken en de grafiek te verbergen.

![De grafiek van de metrische gegevens voor de inlaatsnelheid.](../assets/ui/monitor-sources/metrics-graph.png)

Het onderste gedeelte van het dashboard toont een lijst die het huidige metriekrapport voor alle bestaande brongegevens schetst.

![De metrietabel voor het monitoringdashboard.](../assets/ui/monitor-sources/metrics-table.png)

| Metrics | Beschrijving |
| --- | --- |
| Ontvangen records | Het totale aantal records dat van de bron is ontvangen. |
| Opgenomen records | Het totale aantal records dat aan data Lake wordt ingesloten. |
| Records overgeslagen | Het totale aantal overgeslagen records. |
| Records mislukt | Het totale aantal records dat niet kan worden opgenomen vanwege fouten. |
| Verhoogde snelheid | Het percentage records dat is opgenomen, is gebaseerd op het totale aantal records dat is ontvangen. |
| Totaal aantal mislukte gegevensstromen | Het totale aantal mislukte gegevensstromen. |

{style="table-layout:auto"}

U kunt uw gegevens verder filteren met de opties boven de metrieke tabel:

| Filteropties | Beschrijving |
| --- | --- |
| Zoeken | Met de zoekbalk kunt u de weergave filteren op één brontype. |
| Bronnen | Selecteren **[!UICONTROL Sources]** om uw mening te filtreren en metrische gegevens per brontype te tonen. Dit is de standaardweergave die het dashboard voor bewaking gebruikt. |
| Gegevensstromen | Selecteren **[!UICONTROL Dataflows]** om uw mening te filtreren en metrische gegevens per dataflow te tonen. |
| Alleen fouten tonen | Selecteren **[!UICONTROL Show failures only]** om uw mening te filtreren en slechts gegevens te tonen die gemelde innamemislukkingen. |
| Mijn bronnen | U kunt de weergave verder filteren met de opdracht [!UICONTROL My sources] vervolgkeuzelijst. Met het vervolgkeuzemenu filtert u de weergave op categorie. U kunt ook **[!UICONTROL All sources]** om metriek op alle of bronnen te tonen, of te selecteren **[!UICONTROL My sources]** om alleen de bronnen weer te geven waarmee u een corresponderende account hebt. |

{style="table-layout:auto"}

Selecteer het filterpictogram om de gegevens te controleren die in een specifieke gegevensstroom worden opgenomen ![filter](../assets/ui/monitor-sources/filter.png) naast een bron.

![Controleer een specifieke gegevensstroom door het filterpictogram naast een bepaalde bron te selecteren.](../assets/ui/monitor-sources/monitor-dataflow.png)

De metrietabel werkt aan een lijst van actieve gegevens bij die aan de bron beantwoorden die u selecteerde. Tijdens deze stap, kunt u extra informatie over uw gegevensstromen, met inbegrip van hun overeenkomstige dataset en gegevenstype, evenals een tijdstempel bekijken om erop te wijzen wanneer zij het laatst actief waren.

Selecteer het filterpictogram om een gegevensstroom verder te inspecteren ![filter](../assets/ui/monitor-sources/filter.png) naast een gegevensstroom.

![De dataflows lijst in het controledashboard.](../assets/ui/monitor-sources/select-dataflow.png)

Daarna, wordt u genomen aan een interface die van alle dataflow looplooploopherhalingen van dataflow een lijst maakt die u selecteerde.

Dataflow-uitvoering is een instantie van de uitvoering van de gegevensstroom. Bijvoorbeeld, als een dataflow om 09:00 AM, 10:00 AM, en 11:00 AM gepland is te lopen, dan zou u drie instanties van een stroomlooppas hebben. De looppas van de stroom is specifiek voor uw bepaalde organisatie.

Als u metriek van een specifieke gegevensstroomrun-iteratie wilt inspecteren, selecteert u het filterpictogram ![filter](../assets/ui/monitor-sources/filter.png) naast uw gegevensstroom.

![De metrische pagina van de dataflow looppas.](../assets/ui/monitor-sources/dataflow-page.png)

Gebruik de gegevenspagina van de dataflow looppas om metriek en informatie van uw geselecteerde looppas herhaling te bekijken.

![De gegevenspagina van de dataflow-run.](../assets/ui/monitor-sources/dataflow-run-details.png)

| Gegevens gegevensstroom uitvoeren | Beschrijving |
| --- | --- |
| Opgenomen records | Het totale aantal verslagen die van dataflow looppas werden opgenomen. |
| Records mislukt | Het totale aantal verslagen die niet werden opgenomen toe te schrijven aan fouten in dataflow looppas. |
| Totaal aantal bestanden | Het totale aantal bestanden in de gegevensstroom dat wordt uitgevoerd. |
| Grootte van gegevens | De totale grootte van gegevens bevat in dataflow looppas. |
| ID gegevensstroom uitvoeren | De id van de gegevensstroomrun-iteratie. |
| Org-id | De id van de organisatie waarin de dataflow-run is gemaakt. |
| Status | De status van de gegevensstroom wordt uitgevoerd. |
| Start gegevensstroom | Een tijdstempel die aangeeft wanneer de gegevensstroom is gestart. |
| Einde gegevensstroom | Een tijdstempel die aangeeft wanneer de gegevensstroom is beëindigd. |
| Gegevensset | De dataset die wordt gebruikt om dataflow tot stand te brengen. |
| Gegevenstype | Het type van de gegevens dat in dataflow was. |
| Gedeeltelijke inname | Gedeeltelijke batch-opname is de mogelijkheid om gegevens met fouten in te voeren, tot een bepaalde configureerbare drempel. Met deze functie kunt u al uw nauwkeurige gegevens in het Experience Platform opnemen, terwijl al uw onjuiste gegevens afzonderlijk worden opgeslagen met informatie over waarom deze niet geldig zijn. U kunt gedeeltelijke opname tijdens het dataflow-aanmaakproces toelaten. |
| Foutdiagnostiek | De diagnostiek van de fout instrueert de bron om foutendiagnostiek te veroorzaken die u kunt later van verwijzingen voorzien wanneer het controleren van uw datasetactiviteit en dataflow status. U kunt foutdiagnostiek inschakelen tijdens het maken van de gegevensstroom. |
| Overzicht van Error | Op basis van een mislukte gegevensstroomuitvoering geeft het foutenoverzicht een foutcode en een beschrijving weer om samen te vatten waarom de uitvoering is mislukt. |

{style="table-layout:auto"}

Als er fouten optreden in de dataflow-uitvoering, kunt u omlaag schuiven naar de onderkant van de pagina met de opdracht [!UICONTROL Dataflow run errors] interface.

Gebruik de [!UICONTROL Records failed] sectie om metriek weer te geven op records die niet zijn opgenomen vanwege fouten. Als u een uitgebreid foutrapport wilt weergeven, selecteert u **[!UICONTROL Preview error diagnostics]**. Als u een kopie van de foutdiagnose en het bestandsmanifest wilt downloaden, selecteert u **[!UICONTROL Download]** en kopieer vervolgens de voorbeeld-API-aanroep die u met de [!DNL Data Access] API.

>[!NOTE]
>
>U kunt foutdiagnostiek alleen gebruiken als deze functie is ingeschakeld tijdens het maken van de bronverbinding.

![Het deelvenster met uitvoerfouten voor de gegevensstroom.](../assets/ui/monitor-sources/errors.png)

## Volgende stappen {#next-steps}

Door deze zelfstudie te volgen, hebt u met succes de gegevensstroom van de opname van bron-niveau gecontroleerd gebruikend **[!UICONTROL Monitoring]** dashboard. U hebt ook met succes fouten geïdentificeerd die tot de mislukking van gegevensstromen tijdens het innameproces hebben bijgedragen. Raadpleeg de volgende documenten voor meer informatie:

* [Identiteitsgegevens controleren](./monitor-identities.md).
* [Bewaking van profielgegevens](./monitor-profiles.md).
