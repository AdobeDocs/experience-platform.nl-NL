---
description: Leer hoe u antipatronen voor algemene taakplanningconfiguratie in Adobe Experience Platform kunt identificeren en oplossen.
solution: Experience Platform
title: Anti-patronen voor taakplanning identificeren
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: 3696ebffc4bd1e588a04e5789ff0c7971e636b56
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 0%

---


# Anti-patronen voor taakplanning identificeren

>[!AVAILABILITY]
>
>[!UICONTROL Job schedules] zijn momenteel alleen beschikbaar als een beperkte release en voor de volgende Real-Time CDP-taken:
>
> * Batchgegevens
> * Inname van batchprofiel
> * Batchsegmentatie
> * Batchdoelactivering.

De [&#x200B; planningen van de Baan &#x200B;](job-schedules.md) chronologiemening helpt u gemeenschappelijke configuratiekwesties identificeren die uw prestaties en betrouwbaarheid van de gegevenspijpleiding negatief kunnen beïnvloeden. Deze anti-patronen leiden vaak tot banenmislukkingen, gegevensinconsistenties, of verminderde systeemprestaties. Door deze patronen vroegtijdig te ontdekken, kunt u uw banen aanpassen om problemen te vermijden alvorens zij uw bedrijfsverrichtingen beïnvloeden.

## Vereisten {#prerequisites}

Voordat u anti-patronen kunt identificeren, moet u:

* Heb toegang tot [!UICONTROL Job Schedules] met **[!UICONTROL View Job Schedules]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions).
* Ben vertrouwd met de [&#x200B; interface van Programma&#39;s van de Baan &#x200B;](job-schedules.md#understanding-interface) en hoe te om de chronologiemening te lezen.
* Begrijp fundamentele [&#x200B; partij ingestie &#x200B;](../ingestion/batch-ingestion/overview.md), [&#x200B; segmentatie &#x200B;](../segmentation/home.md), en [&#x200B; de concepten van de profielverwerking &#x200B;](../profile/home.md).

## Snelle verwijzing {#anti-pattern-quick-reference}

| Anti-patroon | Wat u op de tijdlijn ziet | Primair effect | Ernst |
|--------------|----------------------------------|----------------|----------|
| [&#x200B; overlap van het Programma &#x200B;](#schedule-overlap-pattern) | Meerdere taken tegelijk uitvoeren | Bronconflict en mislukte taken | Hoog |
| [&#x200B; Geplande baandichtheid &#x200B;](#scheduled-density) | Vele datasets met partijen die in zelfde uur gegroepeerd zijn | Pijpknelpunten en onvolledige segmentering | Hoog |
| [&#x200B; Excessieve partijen per dataset &#x200B;](#excessive-batches-per-dataset) | Eén dataset met tientallen dagelijkse batches | Inefficiënte verwerking en operationele complexiteit | Medium |

## Planningsoverlapping {#schedule-overlap-pattern}

**strengheid van het Effect**: Hoog | **Primaire kwestie**: De geschil van het Middel

**wat te zoeken**: De veelvoudige banen die worden gepland om tezelfdertijd of in dichte opeenvolging te lopen, in het bijzonder wanneer middel-intensieve banen overlappen.

In dit voorbeeld kunt u batch-opname-taken zien die tegelijkertijd met een geplande segmentatietaak worden uitgevoerd. Dit leidt tot middelgeschil omdat beide verrichtingen significante verwerkingscapaciteit en geheugen vereisen.

**waarom dit problematisch is**:

* **geschil van het Middel**: Wanneer de veelvoudige middel-intensieve banen gelijktijdig lopen, concurreren zij voor systeemmiddelen (CPU, geheugen, I/O), veroorzakend alle banen om langzamer te lopen.
* **Onvoorspelbare prestaties**: De duur van de baan wordt inconsistent, makend het om betrouwbare programma&#39;s te plannen.
* **Cascading vertragingen**: Als de banen langer dan verwacht duren, kunnen zij stroomafwaarts afhankelijke banen vertragen, die tot een rimpeleffect door uw pijpleiding leiden.
* **Verhoogd mislukkingsrisico**: De uitputting van het middel kan banen aan onderbreking veroorzaken of volledig ontbreken.

**hoe te om het** te bevestigen:

* **de baanprogramma&#39;s van de Stagger**: Verzeker middel-intensieve verrichtingen opeenvolgend eerder dan gelijktijdig lopen.
* **voeg buffertijd** toe: Verlaat adequate het uit elkaar plaatsen tussen banen om voor verwerkingsvariaties rekening te houden.
* **gebiedsdelen van het Overzicht**: Identificeer welke banen moeten voltooien alvorens anderen veilig kunnen beginnen.

## Geplande taakdichtheid {#scheduled-density}

**strengheid van het Effect**: Hoog | **Primaire kwestie**: De knelpunten van de pijpleiding

**wat om** te zoeken: Te veel datasets met veelvoudige partijen die binnen het zelfde uur worden gepland, met name wanneer deze partijen dicht bij elkaar worden gestapeld en dichtbij kritieke verwerkingsvensters zoals segmentatiebegintijden worden gepland.

In dit patroon ziet u:

* Meerdere gegevenssets die elk meerdere batches per dag uitvoeren
* ETL-taken (opname van data Lake en opname van profielen) geclusterd binnen hetzelfde uur
* Batchopname gepland vlak voor of tijdens geplande segmentatievensters

**waarom dit problematisch is**:

* **knelpunt van de Pijpleiding**: Wanneer talrijke partijen van verschillende datasets binnen een kort tijdvenster worden gestapeld, leiden zij tot een verwerkingsknelpunt dat de innamepijpleiding kan overweldigen.
* **Vertraagde profielbeschikbaarheid**: De banen van de opname van het profiel die te dicht bij de tijden van het segmentatiebegin lopen kunnen niet in tijd voltooien, resulterend in onvolledige of stapelpublieksevaluaties.
* **Onvoorspelbare segmentatie**: Als de stroomopwaartse innametaken nog lopen wanneer de segmentatie begint, riskeert u evaluerend publiek tegen onvolledige gegevens, die tot onjuist publiekslidmaatschap leiden.
* **Cascading mislukkingen**: Één enkele vertraagde partij in een dicht gestapeld programma kan een domino-effect veroorzaken, vertragend alle verdere partijen en stroomafwaartse processen.
* **het stromen van het Middel**: Het systeem kan worstelen om voldoende middelen toe te wijzen wanneer het verwerken van teveel gezamenlijke inslidingbanen, die tot langzamere verwerkingstijden of mislukkingen leiden.

**hoe te om het** te bevestigen:

* **consolideert partijen**: Verminder partijfrequentie door veelvoudige kleine partijen in minder, grotere partijen per dataset te combineren.
* **verdeel gelijkmatig**: De banen van de spreadopname door de dag eerder dan het groeperen van hen in specifieke uren.
* **voeg buffertijd** toe: verzeker een minimum 1-2 uurbuffer tussen de voltooiing van de profielopname en segmentatiebegin.
* **vereisten van het Overzicht**: Bepaal of alle datasets echt veelvoudige dagelijkse partijen-vele gebruiksgevallen met minder frequente updates nodig hebben.

## Te veel batches per gegevensset {#excessive-batches-per-dataset}

**strengheid van het Effect**: Medium | **Primaire kwestie**: Inefficiënte verwerking

**wat te zoeken**: Één enkele dataset met een bovenmatig aantal individuele partijbanen die door de dag worden gepland, die tot een lange verticale stapel banen op de chronologie leiden.

In dit patroon, zult u één datasetrij met vele individuele batch ingestion banen zien die met regelmatige intervallen-soms tientallen partijen per dag voor één enkele dataset worden gepland.

**waarom dit problematisch is**:

* **Inefficiënte verwerking**: Elke partijbaan heeft overheadkosten (initialisering, bevestiging, meta-gegevensupdates). Veel kleine batches verwerken is aanzienlijk minder efficiënt dan grotere batches verwerken.
* **Verhoogde mislukkingsoppervlakte**: Meer banen betekenen meer kansen voor mislukking. Voor elke batch waarvoor dit niet het geval is, zijn onderzoek en mogelijke opwerking vereist.
* **Onnoodzakelijke systeemlading**: De frequente kleine partijen houden het systeem constant bezig met overheadtaken eerder dan daadwerkelijke gegevensverwerking, die algemene productie verminderen.
* **Vertraagde gegevensbeschikbaarheid**: Paradoxaal, die vele kleine partijen in werking stellen kan vertragen wanneer de gegevens voor stroomafwaartse processen in vergelijking met geconsolideerde partijen beschikbaar worden.
* **Moeilijke inspectie**: Het volgen van het succes en de prestaties van tientallen individuele partijbanen per dataset worden operationeel complex en tijdrovend.
* **de verwerkingsvertraging van het Profiel**: Elke partij van de profielopname brengt profielverwerking teweeg. Veelvoorkomende kleine batches kunnen ertoe leiden dat de profielverwerking bijna ononderbroken wordt uitgevoerd, waardoor een efficiënte batchoptimalisatie wordt voorkomen.

**hoe te om het** te bevestigen:

* **Verminder partijfrequentie**: Consolideer aan minder partijen per dag per dataset voor de meeste gebruiksgevallen.
* **de partijgrootte van de Verhoging**: Haal meer gegevens vóór het teweegbrengen van opname eerder dan onmiddellijk het opnemen op.
* **richt zich op bedrijfsbehoeften**: Verifieer of de uurupdates echt worden vereist, of als dagelijks/tweemaal daags updates voldoende zijn.
* **het stromen van het Gebruik voor real time**: Schakelaar aan het stromen ingestie voor echte vereisten in real time in plaats van het te simuleren met frequente partijen.

## Volgende stappen {#next-steps}

Na het identificeren van anti-patronen in uw taakprogramma&#39;s:

* Bekijk [&#x200B; baandetails &#x200B;](job-schedules-details.md) om specifieke datasets en baanlooppas te onderzoeken die kwesties kunnen veroorzaken.
* Herzie het [&#x200B; overzicht van de Programma&#39;s van de Baan &#x200B;](job-schedules.md) om de interface en inspectiemogelijkheden te begrijpen.
* Leer over [&#x200B; partij ingestie &#x200B;](../ingestion/batch-ingestion/overview.md) om uw gegevens te optimaliseren ladende programma&#39;s.
* Begrijp [&#x200B; segmenteringsprogramma&#39;s &#x200B;](../segmentation/home.md) om juiste timing van publieksevaluaties te verzekeren.
* Onderzoek [&#x200B; controlerende bestemmingsdataflows &#x200B;](../dataflows/ui/monitor-destinations.md) voor pijpleidingszicht van begin tot eind.
