---
keywords: Experience Platform;activering;problemen oplossen;instructies;richtlijnen;beperken
title: Standaardinstructies voor activeringsgegevens
solution: Experience Platform
product: experience platform
type: Documentation
description: Meer informatie over het standaardgebruik en de tarieflimieten van gegevensactivering.
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: d8e7b5daf72afab8e0a980e35b18a9986a19387d
workflow-type: tm+mt
source-wordcount: '1527'
ht-degree: 1%

---

# Grails voor activeringsgegevens

Deze pagina bevat standaardgebruiks- en tarieflimieten voor activeringsgedrag. Bij het bekijken van de volgende instructies wordt aangenomen dat u de juiste instructies hebt [verbonden met bestemmingen](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* De meeste klanten overschrijden deze standaardgrenzen niet. Neem contact op met uw medewerker van de klantenservice als u meer wilt weten over aangepaste limieten.
>* De limieten die in dit document worden uiteengezet, worden voortdurend verbeterd. Kom regelmatig terug voor updates.
>* Afhankelijk van individuele downstreambeperkingen, kunnen sommige doelen strengere instructies hebben dan de doelen die op deze pagina worden beschreven. Controleer ook of [catalogus](/help/destinations/catalog/overview.md) pagina van het doel waarmee u verbinding maakt en gegevens activeert.

## Limiettypen {#limit-types}

Dit document bevat twee typen standaardlimieten:

* **Zachte limiet:** Het is mogelijk om verder te gaan dan een zachte limiet, maar zachte limieten bieden een aanbevolen richtlijn voor systeemprestaties.
* **Harde limiet:** Een harde grens verstrekt een absoluut maximum. De interface van het Experience Platform of API staat u niet toe om voorbij deze grens te gaan, of een fout is teruggekeerd als u voorbij deze grens gaat.


## Activeringslimieten {#activation-limits}

De volgende gidsen verstrekken geadviseerde grenzen wanneer het activeren van gegevens van het Profiel van de Klant in real time aan bestemmingen.

### Algemene activeringsinstructies {#general-activation-guardrails}

De onderstaande instructies zijn over het algemeen van toepassing op activering via [alle doeltypen](/help/destinations/destination-types.md#destination-types).

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Maximumaantal doelgroepen | 250 | Zacht | De aanbeveling moet een maximum van 250 publiek aan één enkele bestemming in een dataflow in kaart brengen. <br><br> Als u meer dan 250 publiek aan een bestemming moet activeren, kunt u of: <ul><li> Ontkaart publiek dat u niet meer wilt activeren, of</li><li>Creeer een nieuwe dataflow aan de gewenste bestemming en kaartpubliek aan deze nieuwe dataflow.</li></ul> <br> Houd er rekening mee dat in het geval van sommige bestemmingen u beperkt kunt zijn tot minder dan 250 soorten publiek die aan de bestemming zijn toegewezen. Deze bestemmingen worden hieronder op de pagina in hun respectieve secties vermeld. |
| Maximumaantal kenmerken dat aan een doel is toegewezen | 50 | Zacht | In het geval van verschillende bestemmingen en bestemmingstypen kunt u profielkenmerken en identiteiten selecteren die u wilt toewijzen voor export. Voor optimale prestaties, zou een maximum van 50 attributen in een dataflow aan een bestemming moeten worden in kaart gebracht. |
| Maximum aantal bestemmingen | 100 | Hard | U kunt maximaal 100 bestemmingen tot stand brengen die u gegevens kunt verbinden en activeren aan, *per sandbox*. [Aanpasbare Edge-doelen (Aangepaste verpersoonlijking)](#edge-destinations-activation) maximaal 10 van de 100 aanbevolen bestemmingen. |
| Type gegevens die op bestemmingen worden geactiveerd | Profielgegevens, inclusief identiteiten en identiteitskaarten | Hard | Momenteel is het alleen mogelijk om te exporteren *profielrecordkenmerken* naar bestemmingen. XDM-kenmerken die gebeurtenisgegevens beschrijven, worden momenteel niet ondersteund voor exporteren. |
| Type gegevens geactiveerd voor doelen - ondersteuning voor array- en kaartkenmerken | Niet beschikbaar | Hard | Op dit moment is het **niet** kunnen worden geëxporteerd *array- of toewijzingskenmerken* naar bestemmingen. De uitzondering op deze regel is de [identiteitsbewijs](/help/xdm/field-groups/profile/identitymap.md), die wordt geëxporteerd in zowel streaming als bestandgebaseerde activering. |

{style="table-layout:auto"}

### Streaming activering {#streaming-activation}

De onderstaande instructies zijn van toepassing op activering via [streaming doelen](/help/destinations/ui/activate-segment-streaming-destinations.md).

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Aantal activeringen (HTTP-berichten met profielexport) per seconde | N.v.t. | - | Er is momenteel geen grens aan het aantal berichten per seconde die van Experience Platform naar API eindpunten van partnerbestemmingen worden verzonden. <br> Om het even welke grenzen of latentie worden gedicteerd door het eindpunt waar het Experience Platform gegevens verzendt. Controleer ook of [catalogus](/help/destinations/catalog/overview.md) pagina van het doel waarmee u verbinding maakt en gegevens activeert. |

{style="table-layout:auto"}

### Batch (op bestand gebaseerd) activeren {#batch-file-based-activation}

De onderstaande instructies zijn van toepassing op activering via [batchbestemmingen (op basis van bestanden)](/help/destinations/ui/activate-batch-profile-destinations.md).

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Activeringsfrequentie | Eén dagelijkse volledige export of frequentere incrementele export om de 3, 6, 8 of 12 uur. | Hard | Lees de [volledige bestanden exporteren](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) en [incrementele bestanden exporteren](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) Documentatiegedeelten voor meer informatie over de frequentieverhogingen voor batchexport. |
| Maximumaantal soorten publiek dat in een bepaald uur kan worden geëxporteerd | 100 | Zacht | De aanbeveling moet een maximum van 100 publiek aan partijbestemmingsdataflows toevoegen. |
| Maximumaantal rijen (records) per bestand dat moet worden geactiveerd | 5 miljoen | Hard | Adobe Experience Platform splitst de geëxporteerde bestanden automatisch op 5 miljoen records (rijen) per bestand. Elke rij vertegenwoordigt één profiel. Namen van gesplitste bestanden worden toegevoegd met een getal dat aangeeft dat het bestand deel uitmaakt van een grotere exportbewerking, als zodanig: `filename.csv`, `filename_2.csv`, `filename_3.csv`. Lees voor meer informatie de [sectie plannen](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) van de activerende zelfstudie voor batchbestemmingen. |

{style="table-layout:auto"}

### Ad-hocactivering {#ad-hoc-activation}

De onderstaande instructies gelden voor de [ad-hocactivering](/help/destinations/api/ad-hoc-activation-api.md) methode.

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Publiek geactiveerd per ad-hocactiveringstaak | 80 | Hard | Op dit moment kan elke ad-hocactiveringstaak maximaal 80 soorten publiek activeren. Als u probeert meer dan 80 soorten publiek per taak te activeren, mislukt de taak. Dit gedrag kan in toekomstige versies worden gewijzigd. |
| Gelijktijdige ad-hocactiveringstaken per publiek | 1 | Hard | Voer niet meer dan één gelijktijdige ad-hocactiveringstaak per publiek uit. |

{style="table-layout:auto"}

### Activering van Edge-verpersoonlijkingsdoelen {#edge-destinations-activation}

De onderstaande instructies zijn van toepassing op activering via [Edge-verpersoonlijkingsdoelen](/help/destinations/destination-types.md#streaming-profile-export).

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Maximum aantal [Aangepaste personalisatie](/help/destinations/catalog/personalization/custom-personalization.md) bestemmingen | 10 | Zacht | U kunt gegevensstromen aan 10 Aangepaste verpersoonlijkingsbestemmingen per zandbak plaatsen. |
| Maximumaantal kenmerken dat per sandbox aan een verpersoonlijkingsdoel is toegewezen | 30 | Hard | Een maximum van 30 attributen kan in een dataflow aan een verpersoonlijkingsbestemming, per zandbak worden in kaart gebracht. |
| Maximum aantal soorten publiek toegewezen aan één [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) doel | 50 | Zacht | U kunt maximaal 50 soorten publiek activeren in een activeringsstroom naar één Adobe Target-bestemming. |

{style="table-layout:auto"}

### Dataset exporteren {#dataset-exports}

De uitvoer van gegevenssets wordt momenteel ondersteund in een **[!UICONTROL First Full and then Incremental]** [patroon](/help/destinations/ui/export-datasets.md#scheduling). De in dit punt beschreven instructies *van toepassing zijn op de eerste volledige uitvoer* die zich voordoet nadat een gegevensset-exportworkflow is ingesteld.

<!--

| Guardrail | Limit | Limit Type | Description |
| --- | --- | --- | --- |
| Size of exported datasets | 5 billion records | Soft | The limit described here for dataset exports is a *soft guardrail*. For example, while the user interface will not block you from exporting datasets larger than 5 billion records, the behavior is unpredictable and exports might either fail or have very long export latency. |

{style="table-layout:auto"}

-->

#### Dataset-typen {#dataset-types}

De instructies voor de uitvoer van gegevenssets zijn van toepassing op twee soorten gegevenssets die uit Experience Platform worden geëxporteerd, zoals hieronder beschreven:

**Datasets die op het schema van de Gebeurtenissen van de Ervaring XDM worden gebaseerd**
In het geval van datasets die op het schema van de Gebeurtenissen van de Ervaring XDM worden gebaseerd, omvat het datasetschema een hoogste niveau *tijdstempel* kolom. Gegevens worden alleen toegevoegd.

**Gegevenssets die zijn gebaseerd op het XDM Individuele Profielschema**
In het geval van datasets die op het XDM Individuele schema van het Profiel worden gebaseerd, omvat het datasetschema geen hoogste niveau *tijdstempel* kolom. Gegevens worden opgenomen in een pop-upmenu.

De onderstaande zachte handleiding is van toepassing op alle gegevenssets die uit Experience Platform worden geëxporteerd. Bekijk ook de harde instructies hieronder, specifiek voor verschillende dataset en compressietypen.

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Grootte van geëxporteerde gegevenssets | 5 miljard records | Zacht | De hier beschreven limiet voor de uitvoer van gegevenssets is een *zachte guardrail*. Bijvoorbeeld, terwijl de gebruikersinterface u niet zal blokkeren van het uitvoeren van datasets groter dan 5 miljard verslagen, is het gedrag onvoorspelbaar en de uitvoer zou of kunnen ontbreken of zeer lange uitvoerlatentie hebben. |

{style="table-layout:auto"}

#### Guardrails voor de uitvoer van geplande gegevenssets

Voor geplande, of terugkomende datasetuitvoer, zijn de hieronder grails voor de twee formaten van het uitgevoerde dossier (JSON of parquet) identiek, en gegroepeerd door datasettype.

>[!WARNING]
>
>Exporteren naar JSON-bestanden worden alleen in de gecomprimeerde modus ondersteund.

| Het type DataSet | Guardrail | Het type Guardrail | Beschrijving |
---------|----------|---------|-------|
| Gegevensbestanden op basis van de **XDM Experience Events-schema** | Laatste 365 dagen met gegevens | Hard | De gegevens van het laatste kalenderjaar worden uitgevoerd. |
| Gegevensbestanden op basis van de **Schema voor individueel XDM-profiel** | Tien miljard records in alle geëxporteerde bestanden in een gegevensstroom | Hard | Het recordaantal van de dataset moet minder dan tien miljard voor samengeperste JSON of parquet dossiers en één miljoen voor ongecomprimeerde parketdossiers zijn, anders ontbreekt de uitvoer. Verminder de grootte van de dataset die u probeert uit te voeren als het groter is dan de toegestane drempel. |

{style="table-layout:auto"}

<!--

#### Ad-hoc dataset exports

Exporting datasets in an-hoc manner is currently supported via API only. For ad-hoc dataset exports, you must use the backfill parameter in the API to limit the timeframe of exported data. 

The guardrails below are the same whether you are exporting parquet of JSON files ad-hoc. 

**Parquet and JSON output**

|Dataset type | Backfill parameter provided | Guardrail | Guardrail type | Description |
|---------|---------|-----------|-----------|------------|
| Datasets based on the **XDM Experience Events schema** |  <p><ul><li>Both start and end date provided in `backfill` parameter in API call</li><li>Incomplete `backfill` parameter provided in API call</li></ul></p> | <p><ul><li>Last 30 days</li><li>Last 365 days</li></ul></p> | Hard | <p><ul><li>The export fails if the `startDate - endDate` interval is over 30 days</li><li>Either the `startDate` or `endDate` are missing or  incorrectly formatted in the API call. Expected format: `yyyy-MM-dd'T'HH:mm:ss.SSS'Z'`</li></ul></p> |
| Datasets based on the **XDM Individual Profile schema** |  - | Ten billion records across all files exported in a dataflow | Hard | The record count of the dataset must be less than ten billion for compressed JSON or parquet files and one million for uncompressed parquet files, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold. |

{style="table-layout:auto"}

-->

Meer informatie over [gegevensbestanden exporteren](/help/destinations/ui/export-datasets.md).


### Destination SDK guardrails {#destination-sdk-guardrails}

[Destination SDK](/help/destinations/destination-sdk/overview.md) is een reeks van configuratie APIs die u toestaan om bestemmingsintegratiepatronen voor Experience Platform te vormen om publiek en profielgegevens aan uw eindpunt te leveren, die op gegevens en authentificatieformaten van uw keus wordt gebaseerd. De onderstaande instructies zijn van toepassing op de doelen die u configureert met behulp van Destination SDK.

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Maximum aantal [persoonlijke aangepaste bestemmingen](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | Zacht | U kunt maximaal vijf aangepaste streaming privédoelen of batchdoelen maken met behulp van Destination SDK. Neem contact op met een aangepaste zorgvertegenwoordiger als u meer dan vijf van dergelijke doelen moet maken. |
| Profielexportbeleid voor Destination SDK | <ul><li>`maxBatchAgeInSecs` (minimaal 1 800 en maximaal 3 600)</li><li>`maxNumEventsInBatch` (minimaal 1 000, maximaal 10 000)</li></ul> | Hard | Wanneer u de opdracht [configureerbare samenvoeging](destination-sdk/functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) Houd rekening met de minimum- en maximumwaarden die bepalen hoe vaak HTTP-berichten naar de op API gebaseerde bestemming worden verzonden en hoeveel profielen de berichten moeten bevatten. |

{style="table-layout:auto"}

### Beleidswijziging en opnieuw proberen van bestemming {#destination-throttling-and-retry-policy}

Gegevens over drempelwaarden of beperkingen voor bepaalde bestemmingen. Deze sectie verstrekt ook informatie betreffende het hertestbeleid voor bestemmingen.

| Type bestemming | Beschrijving |
| --- | --- |
| Enterprise-bestemmingen (HTTP-API, Amazon Kinesis, Azure EventHubs) | In 95 percent van de tijd, probeert het Experience Platform om een productietolerantie van minder dan 10 minuten voor met succes verzonden berichten met een tarief van minder dan 10.000 verzoeken per seconde voor elke dataflow aan een ondernemingsbestemming aan te bieden. <br> In het geval van ontbroken verzoeken aan uw ondernemingsbestemming, slaat het Experience Platform de ontbroken verzoeken op en probeert tweemaal om de verzoeken naar uw eindpunt te verzenden. |

{style="table-layout:auto"}

## Guardrails voor ander Experience Platform {#guardrails-other-services}

Informatie over hulplijnen weergeven voor andere services van Experience Platforms:

* Guardrails voor [gegevensinvoer](/help/ingestion/guardrails.md)
* Guardrails voor [[!DNL Identity Service] data](/help/identity-service/guardrails.md)
* Guardrails voor [[!DNL Real-Time Customer Profile] data](/help/profile/guardrails.md)
* Guardrails voor [[!DNL Query Service] data](/help/query-service/guardrails.md)
