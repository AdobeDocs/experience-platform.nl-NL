---
description: Leer hoe te om gedetailleerde informatie over datasets en individuele baanlooppas in de Programma's van de Baan te bekijken.
solution: Experience Platform
title: Taakplanningsgegevens weergeven
type: Tutorial
hide: true
source-git-commit: 436ce6843e96b76dac0595ff5ab8a6067fb521ea
workflow-type: tm+mt
source-wordcount: '1783'
ht-degree: 0%

---


# Details taakplanning weergeven

>[!AVAILABILITY]
>
>[!UICONTROL Job schedules] zijn momenteel alleen beschikbaar als een beperkte release en voor de volgende Real-Time CDP-taken:
>
> * Batchgegevens
> * Inname van batchprofiel
> * Batchsegmentatie
> * Batchdoelactivering.

Wanneer het oplossen van problemenbaanmislukkingen of het onderzoeken van prestatieskwesties, hebt u gedetailleerde informatie over specifieke datasets en hun baanlooppas nodig. De [ interface van de Programma&#39;s van de Baan ](job-schedules.md) staat u toe om neer van de chronologiemening in individuele datasets en banen te boren om uitvoeringsgeschiedenis, timing, en status te begrijpen.

Met deze gedetailleerde weergave kunt u:

* Onderzoek waarom een specifieke baan ontbrak of langer duurde dan verwacht
* Herzie de uitvoeringsgeschiedenis voor een dataset in tijd
* Begrijp de timing en duurpatronen van partijbanen
* Identificeer welke specifieke partijen pijpleidingskwesties veroorzaken
* Informatie verzamelen die nodig is voor probleemoplossing met Adobe Support

## Vereisten {#prerequisites}

Voordat u de taakdetails weergeeft, moet u:

* Heb toegang tot [!UICONTROL Job Schedules] met **[!UICONTROL View Job Schedules]** en **[!UICONTROL View Profile Management]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions).
* Ben vertrouwd met de [ interface van Programma&#39;s van de Baan ](job-schedules.md#understanding-interface) en chronologiemening.
* Begrijp de verschillende [ baantypes ](job-schedules.md#job-schedules-details) (meeropname, profielopname, segmentatie, activering).

## Werken met de detailhiërarchie {#details-hierarchy}

De dienstprogramma&#39;s verstrekken drie niveaus van detail, die u toestaan om van brede patronen aan specifieke kwesties over te gaan:

| Weergaveniveau | Wat het laat zien | Wanneer gebruikt u het |
|------------|---------------|----------------|
| **mening van de Chronologie** | Alle datasets en hun geplande banen over de geselecteerde tijdspanne | Het identificeren van patronen, het spotting [ anti-patronen ](job-schedules-anti-patterns.md), en het krijgen van een overzicht van uw volledige pijpleiding |
| **de details van de Dataset** | Samengevoegde metriek en uitvoeringsgeschiedenis voor één enkele dataset | Het volgen van algemene prestaties van één dataset, het begrip van gegevensvolumes, en het herzien baanfrequentie |
| **de looppas van de Baan details** | Specifieke uitvoeringsinformatie voor een individuele uitgevoerde taak | Controleren waarom een bepaalde taak is mislukt, exacte timing controleren en verwerkte records controleren |

**de stroom van de Navigatie**: Begin met de chronologiemening om kwesties te identificeren → Selecteer een dataset om zijn details te zien → Selecteer een specifieke baanlooppas om details te onderzoeken.

### De tijdlijnweergave {#timeline-visualization}

In de tijdlijnweergave wordt een horizontale en verticale indeling gebruikt om u inzicht te geven in taakschema&#39;s en kritieke verwerkingstijden:

* **Horizontale as (tijdvooruitgang)**: Datasets en hun baanlooppas worden getoond over de chronologie van links aan recht, die toont wanneer de banen over de geselecteerde tijdspanne (vandaag, gisteren, of afgelopen 7 dagen) uitvoeren. Elke gekleurde balk vertegenwoordigt een taak die horizontaal wordt geplaatst op basis van de begin- en eindtijd.

* **Verticale as (geplande begintijden)**: De kritieke geplande begintijden worden getoond als verticale lijnen die zich over alle datasets uitstrekken, die het gemakkelijk maken om de timingsverhouding tussen stroomopwaartse banen en stroomafwaartse verwerking te zien:
   * **Blauwe verticale lijn**: Vertegenwoordigt wanneer de segmentatie gepland is te beginnen
   * **Zwarte verticale lijn**: Vertegenwoordigt wanneer de bestemmingsactivering wordt gepland om te beginnen

Deze lay-out staat u toe om timingsverhoudingen tussen uw banen van de gegevenspijpleiding en stroomafwaartse verwerking snel te identificeren. In het ideale geval moeten upstream-taken (zoals het opnemen van gegevens in het meer en het profiel) links van deze verticale markeertekens worden voltooid, zodat de gegevens gereed zijn voordat de segmentatie en activering beginnen. Banen die voorbij deze markeertekens reiken, wijzen op mogelijke tijdsproblemen waarbij downstreamprocessen kunnen beginnen voordat gegevens volledig worden voorbereid.

### Welk standpunt moet ik innemen? {#which-view}

Gebruik de onderstaande tabel om de juiste weergave voor uw taak te kiezen. Pas aan wat u met de geadviseerde mening moet doen om efficiënt te navigeren.

| Ik moet... | Deze weergave gebruiken |
|--------------|---------------|
| Bekijk al mijn profiel-toegelaten datasets en hun programma&#39;s in één keer | [ mening van de Chronologie ](job-schedules.md) |
| Conflicten of antipatronen tijdens het plannen vaststellen | [ mening van de Chronologie ](job-schedules.md) |
| De algemene prestaties van het spoor van één dataset | [ de details van de Dataset ](#view-dataset-details) |
| Zie hoeveel totale verslagen een dataset heeft verwerkt | [ de details van de Dataset ](#view-dataset-details) |
| De baanprestaties voor één dataset in tijd vergelijken | [ de details van de Dataset ](#view-dataset-details) |
| Onderzoek waarom een specifieke baan ontbrak | [ de looppas van de Baan details ](#view-job-details) |
| De exacte timing van een bepaalde taak controleren | [ de looppas van de Baan details ](#view-job-details) |
| Gegevens verifiëren die in één enkele run zijn verwerkt | [ de looppas van de Baan details ](#view-job-details) |
| Gedetailleerde foutberichten openen | [ de looppas van de Baan details ](#view-job-details) → Selecteer dataflow looppas identiteitskaart |

## Gegevens gegevensset weergeven {#view-dataset-details}

Om details voor een specifieke dataset te bekijken:

1. Zoek in de tijdlijnweergave van **[!UICONTROL Job Schedules]** de gegevensset die u wilt onderzoeken.
2. Selecteer de naam van de gegevensset in de linkerkolom.

De mening van de datasetdetails opent in een juist paneel, dat informatie over alle banen toont verbonden aan deze dataset.

![ het paneel van de gegevenssetdetails die de bijeengevoegde meer en profielingestitie metriek voor een geselecteerde dataset tonen.](assets/job-schedules/view-dataset-details.png)

In het deelvenster Gegevens van de gegevensset worden de naam, de id en taakspecifieke metriek van de gegevensset weergegeven, ingedeeld op taaktype. Bovenaan in het deelvenster wordt de id van de gegevensset weergegeven als een klikbare koppeling. Selecteer deze id om naar de volledige pagina met gegevens over de gegevensset te navigeren.

Elk deelvenster met gegevens over gegevenssets bevat de volgende gegevens:

### Meting van de ingestie van het meer {#lake-ingestion-metrics}

Voor datasets met gegevens bevat het paneel de volgende metriek:

| Metrisch | Beschrijving | Gebruiken voor |
|--------|-------------|---------|
| **[!UICONTROL Total runs]** | Het totale aantal banen van de gegevensmeeropname die voor deze dataset zijn voltooid | Activiteit bijhouden |
| **[!UICONTROL Runs in progress]** | Hoeveel banen zijn er op dit moment in de binnenvaart? | Botsingdetectie |
| **[!UICONTROL Total records added]** | Het cumulatieve aantal nieuwe records dat aan het gegevensmeer is toegevoegd over alle taakuitvoering | Volumeregeling |
| **[!UICONTROL Total ingestion time]** | De gecombineerde duur van alle taken voor het opnemen van gegevens in het meer | Bezig met verwerken van tijdbeoordeling |
| **[!UICONTROL Total records updated]** | Het cumulatieve aantal bestaande records dat tijdens inname is bijgewerkt | Patroonanalyse vernieuwen |
| **[!UICONTROL Avg. ingestion speed (records/second)]** | De gemiddelde doorvoersnelheid voor datumpagenbanen | Prestatievergelijking |

### Metrische gegevens voor het opnemen van profielen {#profile-ingestion-metrics}

Voor datasets met de banen van de profielopname, toont het paneel de volgende metriek:

| Metrisch | Beschrijving | Gebruiken voor |
|--------|-------------|---------|
| **[!UICONTROL Total runs]** | Het totale aantal taken voor het opnemen van profielen dat is voltooid voor deze gegevensset | Activiteit bijhouden |
| **[!UICONTROL Runs in progress]** | Hoeveel taken voor het opnemen van profielen worden momenteel uitgevoerd | Vertragingsdetectie |
| **[!UICONTROL Total profiles created]** | Het cumulatieve aantal nieuwe profielen die van deze dataset over alle baanlooppas worden gecreeerd | Controle van de profielgroei |
| **[!UICONTROL Total profile ingestion time]** | De gecombineerde duur van alle taken voor het opnemen van profielen | Identificatie van tijdkwestie |
| **[!UICONTROL Total profiles updated]** | Het cumulatieve aantal bestaande profielen dat met gegevens van deze dataset werd bijgewerkt | Frequentie bijhouden bijwerken |
| **[!UICONTROL Avg. profile ingestion speed (profiles/second)]** | De gemiddelde doorvoersnelheid voor profieltaken | Prestatiebewaking |

>[!NOTE]
>
> Deze metriek tonen cumulatieve totalen over alle baanlooppas voor deze dataset. Als u details voor een specifieke uitvoering wilt zien, selecteert u een taak rechtstreeks in de tijdlijn.

## Gegevenssets in de tijdlijn filteren {#filter-datasets}

Wanneer u vele datasets met geplande banen hebt, kunt u zich op specifieke datasets eerder willen concentreren dan het bekijken van allen tegelijkertijd. Met het gegevenssetfilter kunt u selecteren welke gegevenssets in de tijdlijnweergave worden weergegeven.

![ het paneel van de datasetfilter dat u toestaat om te selecteren welke datasets in de chronologiemening verschijnen.](assets/job-schedules/view-datasets.gif)

De datasets filteren die in de tijdlijn worden weergegeven:

1. Zoek naar de datasetteller in de hogere linkerzijde van de chronologiemening (bijvoorbeeld, &quot;2 Datasets&quot;).
2. Selecteer het filterpictogram naast de datasetteller.
3. Er wordt een deelvenster voor de selectie van gegevenssets geopend waarin alle beschikbare, voor profielen geschikte gegevenssets met geplande taken worden weergegeven.
4. Selecteer of schrap datasets om hen in de chronologiemening te tonen of te verbergen.
5. De tijdlijn wordt direct bijgewerkt om alleen de geselecteerde datasets weer te geven.

Filteren gebruiken voor:

* **nadruk op specifieke gegevensbronnen**: Wanneer het oplossen van problemen een bepaalde gegevenspijpleiding, filter om slechts de relevante datasets te tonen.
* **Verminder visuele rommel**: Als u vele datasets hebt, helpt het filtreren u patronen duidelijker voor een ondergroep van gegevens zien.
* **vergelijk verwante datasets**: Selecteer slechts datasets die verwant zijn om hun het plannen verhouding te begrijpen.
* **onderzoekt anti-patronen**: Wanneer u een potentiële [ configuratiekwestie ](job-schedules-anti-patterns.md) identificeert, filter aan de beïnvloede datasets om hen nauwkeuriger te onderzoeken.

Het filter blijft tijdens uw zitting voortbestaan, zodat kunt u tussen tijdperiodes (vandaag, gisteren, afgelopen 7 dagen) navigeren terwijl het handhaven van uw datasetselectie.

## Gegevens van afzonderlijke taakuitvoering weergeven {#view-job-details}

Wanneer u een specifieke taaklooppas moet onderzoeken, selecteer het van de chronologie om gedetailleerde uitvoeringsinformatie voor die bepaalde looppas te zien.

### Gegevens voor taakuitvoering openen {#access-job-details}

Details weergeven voor een specifieke uitgevoerde taak:

1. Zoek in de tijdlijnweergave van [!UICONTROL Job Schedules] de specifieke taakuitvoering die u wilt onderzoeken.
2. Selecteer de taakindicator op de tijdlijn (de gekleurde balk die de taak vertegenwoordigt).

Het deelvenster **[!UICONTROL Dataflow run details]** wordt geopend en bevat informatie over de uitvoering van die specifieke taak.

![ het dataflow looppas detailpaneel die uitvoeringsinformatie voor een specifieke baan tonen in werking wordt gesteld.](assets/job-schedules/job-details.png)

### Gegevens gegevensstroom uitvoeren {#dataflow-run-details}

In het detailvenster met gegevens over uitvoering van de gegevensstroom wordt informatie weergegeven over de specifieke uitgevoerde taak, ingedeeld op taaktype. Voor inname-taken zie je details voor zowel meerinname als profielopname.

#### Gegevens over meer ingeslikte banen {#lake-ingestion-job-details}

| Veld | Beschrijving |
|-------|-------------|
| **[!UICONTROL Dataflow run ID]** | De unieke id voor deze specifieke meeropname-taak wordt uitgevoerd. Selecteer de id om de volledige gegevens van de gegevensstroom te bekijken. |
| **[!UICONTROL Run status]** | Het resultaat van de taak (Voltooid, Mislukt, Bezig, In wachtrij). Een groene indicator geeft aan dat de bewerking is voltooid. |
| **[!UICONTROL Started at]** | De datum en tijd waarop de opname van het meer werd uitgevoerd. |
| **[!UICONTROL Completed at]** | De datum en het tijdstip waarop de innametaak van het meer is voltooid. |
| **[!UICONTROL Records added]** | Het aantal nieuwe verslagen die aan het gegevensmeer tijdens deze baanlooppas worden toegevoegd. |
| **[!UICONTROL Records updated]** | Het aantal bestaande verslagen die in het gegevensmeer tijdens deze baanlooppas werden bijgewerkt. |

#### Gegevens van ingevulde profieltaak {#profile-ingestion-job-details}

| Veld | Beschrijving |
|-------|-------------|
| **[!UICONTROL Dataflow run ID]** | De unieke id voor deze specifieke profielingstaak die wordt uitgevoerd. Selecteer de id om de volledige gegevens van de gegevensstroom te bekijken. |
| **[!UICONTROL Run status]** | Het resultaat van de taak (Voltooid, Mislukt, Bezig, In wachtrij). Een groene indicator geeft aan dat de bewerking is voltooid. |
| **[!UICONTROL Started at]** | De datum en tijd waarop de innametaak van het profiel werd uitgevoerd. |
| **[!UICONTROL Completed at]** | De datum en tijd waarop de uitvoeringstaak van de profielopname is voltooid. |
| **[!UICONTROL Records added]** | Het aantal nieuwe profielen dat is gemaakt tijdens de uitvoering van deze taak. |
| **[!UICONTROL Records updated]** | Het aantal bestaande profielen dat tijdens deze taak is bijgewerkt. |

### Werken met de uitvoering van taken {#job-execution-flow}

Wanneer u een specifieke job run bekijkt, kunt u de relatie zien tussen meeropname en profielopname:

* **de looppas van de inname van het meer eerst**: Het gegeven wordt geladen in het gegevenshoop en bevestigd.
* **het opnemen van het Profiel volgt**: Nadat het meer wordt opgenomen voltooit, worden de in aanmerking komende verslagen verwerkt in de profielopslag.
* **Timing doet zich voor**: Noteer het tijdverschil tussen wanneer de meeropname voltooit en wanneer de profielopname begint. De tussenruimten hier kunnen stroomafwaartse processen zoals segmentatie beïnvloeden.

**de baanloopdetails van het Gebruik aan**:

* Controleren of een specifieke taak is voltooid
* De werkelijke duur van een uitgevoerde taak berekenen (voltooide tijd minus begintijd)
* Begrijp hoeveel verslagen in een specifieke looppas werden verwerkt
* Vergelijk prestaties over verschillende baanlooppas
* Toegang tot gedetailleerde dataflow-controle voor probleemoplossing
* Problemen met de timing vaststellen tussen de fasen van het opnemen van meer en profielen

## Problemen met taakdetails oplossen {#troubleshooting}

Gebruik taakdetails om problemen te onderzoeken en de volgende stappen te bepalen:

**Ontbroken banen**: Selecteer dataflow looppas identiteitskaart aan meningsfoutendetails in het controledashboard. Controle [ datasetdetails ](#view-dataset-details) voor terugkomende patronen, herzie de [ chronologie ](job-schedules.md) voor middelgeschil, en identificeer [ anti-patronen ](job-schedules-anti-patterns.md) in uw configuratie.

**Trage banen**: Vergelijk duur met historische gemiddelden in [ datasetmetriek ](#view-dataset-details). De gemeenschappelijke oorzaken omvatten [ overlapping van het programma ](job-schedules-anti-patterns.md#schedule-overlap-pattern), [ dichte partij het stapelen ](job-schedules-anti-patterns.md#scheduled-density), of verhoogd gegevensvolume.

**de wanverhoudingen van het Verslag**: Vergelijk de verslagen van de meeropname tegen de verslagen van de profielopname in de details van de baanlooppas. Het opnemen van het profiel toont typisch minder verslagen toe te schrijven aan identiteitsvereisten en de regels van de gegevenskwaliteit.

Voor gedetailleerde dataflow statusinformatie, zie [ de gegevens van de Monitor meer ingang ](../dataflows/ui/monitor-sources.md), [ dataflows van de Monitor voor profielen ](../dataflows/ui/monitor-profiles.md), [ dataflows voor publiek ](../dataflows/ui/monitor-audiences.md), en [ dataflows voor bestemmingen ](../dataflows/ui/monitor-destinations.md).

## Volgende stappen {#next-steps}

Na het leren hoe u taakdetails kunt weergeven:

* Herzie het [ overzicht van de Planningen van de Baan ](job-schedules.md) om de chronologiemening en de interface te begrijpen.
* Leer over [ anti-patronen ](job-schedules-anti-patterns.md) om gemeenschappelijke configuratiekwesties te verhinderen.
* Begrijp [ partijingestie ](../ingestion/batch-ingestion/overview.md) om uw gegevens te optimaliseren ladende programma&#39;s.
* Onderzoek [ controlerende bestemmingsdataflows ](../dataflows/ui/monitor-destinations.md) voor pijpleidingszicht van begin tot eind.
