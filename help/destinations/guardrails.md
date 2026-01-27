---
keywords: Experience Platform;activering;problemen oplossen;instructies;richtlijnen;beperken
title: Standaardinstructies voor gegevensactivering
solution: Experience Platform
product: experience platform
type: Documentation
description: Meer informatie over het standaardgebruik en de tarieflimieten van gegevensactivering.
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: 11ef8fe8b64a7c2bb698c62093aafe3fb11d3789
workflow-type: tm+mt
source-wordcount: '1731'
ht-degree: 1%

---

# Grails voor gegevensactivering

>[!IMPORTANT]
>
>Controleer uw vergunningsrechten in uw Orde van de Verkoop en de overeenkomstige [ Beschrijving van het Product ](https://helpx.adobe.com/legal/product-descriptions.html) op daadwerkelijke gebruiksgrenzen naast deze guardrails pagina.

Deze pagina bevat standaardgebruiks- en tarieflimieten voor activeringsgedrag. Wanneer het herzien van de volgende gidsen, wordt het verondersteld dat u correct [ met bestemmingen ](/help/destinations/ui/connect-destination.md) hebt verbonden.

>[!NOTE]
>
>* De meeste klanten overschrijden deze standaardgrenzen niet. Neem contact op met uw medewerker van de klantenservice als u meer wilt weten over aangepaste limieten.
>* De limieten die in dit document worden uiteengezet, worden voortdurend verbeterd. Controleer regelmatig of er updates zijn.
>* Afhankelijk van individuele downstreambeperkingen, kunnen sommige doelen strengere instructies hebben dan de doelen die op deze pagina worden beschreven. Zorg ervoor om de [ catalogus ](/help/destinations/catalog/overview.md) pagina van de bestemming ook te controleren u verbindt en gegevens activeert aan.

## Typen guardrail {#limit-types}

Dit document bevat twee typen standaardlimieten:

| Het type Guardrail | Beschrijving |
|----------|---------|
| **Gegarandeerde van Prestaties (Zachte grens)** | Prestatiegaranties zijn gebruikslimieten die betrekking hebben op het bereik van uw gebruiksgevallen. Als u de prestatiegaranties overschrijdt, kan de prestaties achteruitgaan en de latentie vertragen. Adobe is niet verantwoordelijk voor deze verslechtering van de prestaties. Klanten die een prestatiegarantie consequent overschrijden, kunnen ervoor kiezen om extra capaciteit te licentiëren om prestatievermindering te voorkomen. |
| **systeem-afgedwongen grails (Harde grens)** | De door het systeem afgedwongen instructies worden afgedwongen door de gebruikersinterface of API van Real-Time CDP. Dit zijn grenzen die u niet kunt overschrijden aangezien UI en API u zal tegenhouden dit te doen of een fout zal terugkeren. |

{style="table-layout:auto"}


## Activeringslimieten {#activation-limits}

De volgende gidsen verstrekken geadviseerde grenzen wanneer het activeren van gegevens van het Profiel van de Klant in real time aan bestemmingen.

### Algemene activeringsinstructies {#general-activation-guardrails}

De hieronder gidsen zijn over het algemeen van toepassing op activering door [ alle bestemmingstypes ](/help/destinations/destination-types.md#destination-types).

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Maximumaantal doelgroepen | 250 | Prestatiegerichting | De aanbeveling moet een maximum van 250 publiek aan één enkele bestemming in een dataflow in kaart brengen. <br><br> Als u meer dan 250 soorten publiek naar een doel moet activeren, kunt u: <ul><li> Ontkaart publiek dat u niet meer wilt activeren, of</li><li>Creeer een nieuwe dataflow aan de gewenste bestemming en kaartpubliek aan deze nieuwe dataflow.</li></ul> <br> Houd er rekening mee dat in het geval van bepaalde doelen, het aantal doelgroepen kan worden beperkt tot minder dan 250. Deze bestemmingen worden hieronder op de pagina in hun respectieve secties vermeld. |
| Maximumaantal kenmerken dat aan een doel is toegewezen | 50 | Prestatiegerichting | In het geval van verschillende bestemmingen en bestemmingstypen kunt u profielkenmerken en identiteiten selecteren die u wilt toewijzen voor export. Voor optimale prestaties, zou een maximum van 50 attributen in een dataflow aan een bestemming moeten worden in kaart gebracht. |
| Maximum aantal bestemmingen | 100 | Door het systeem afgedwongen geleiding | U kunt een maximum van 100 bestemmingen tot stand brengen dat u gegevens kunt verbinden en activeren aan, *per zandbak*. [ de verpersoonlijkingsbestemmingen van Edge (de verpersoonlijking van de Douane) ](#edge-destinations-activation) kan omhoog een maximum van 10 van de 100 geadviseerde bestemmingen maken. |
| Type gegevens die op bestemmingen worden geactiveerd | Profielgegevens, inclusief identiteiten en identiteitskaarten | Door het systeem afgedwongen geleiding | Momenteel, is het slechts mogelijk om *attributen van het profielverslag* naar bestemmingen uit te voeren. XDM-kenmerken die gebeurtenisgegevens beschrijven, worden momenteel niet ondersteund voor exporteren. |
| Type gegevens geactiveerd voor doelen - ondersteuning voor array- en kaartkenmerken | Gedeeltelijk beschikbaar | Door het systeem afgedwongen geleiding | U kunt serieattributen naar [ op dossier-gebaseerde bestemmingen ](/help/destinations/destination-types.md#file-based) uitvoeren. [Lees meer](/help/destinations/ui/export-arrays-maps-objects.md) over de nieuwe functionaliteit. |

{style="table-layout:auto"}

### Streaming activering {#streaming-activation}

De hieronder gidsen zijn op activering door [ het stromen bestemmingen ](/help/destinations/ui/activate-segment-streaming-destinations.md) van toepassing.

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Aantal activeringen (HTTP-berichten met profielexport) per seconde | N.v.t. | - | Er is momenteel geen limiet voor het aantal berichten per seconde dat van Experience Platform naar API eindpunten van partnerbestemmingen wordt verzonden. <br> Om het even welke grenzen of latentie worden gedicteerd door het eindpunt waar Experience Platform gegevens verzendt. Zorg ervoor om de [ catalogus ](/help/destinations/catalog/overview.md) pagina van de bestemming ook te controleren u verbindt en gegevens activeert aan. |

{style="table-layout:auto"}

### Batch (op bestand gebaseerd) activeren {#batch-file-based-activation}

De hieronder gidsen zijn op activering door [ partij (op dossier-gebaseerde) bestemmingen ](/help/destinations/ui/activate-batch-profile-destinations.md) van toepassing.

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Activeringsfrequentie | Eén dagelijkse volledige export of frequentere incrementele export om de 3, 6, 8 of 12 uur. | Door het systeem afgedwongen geleiding | Lees de [ uitvoer volledige dossiers ](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) en [ uitvoer stijgende dossiers ](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) documentatiesecties voor meer informatie over de frequentieverhogingen voor partijuitvoer. |
| Maximumaantal soorten publiek dat in een bepaald uur kan worden geëxporteerd | 100 | Prestatiegerichting | De aanbeveling moet een maximum van 100 publiek aan partijbestemmingsdataflows toevoegen. |
| Maximumaantal rijen (records) per bestand dat moet worden geactiveerd | 5 miljoen | Door het systeem afgedwongen geleiding | Adobe Experience Platform splitst de geëxporteerde bestanden automatisch op 5 miljoen records (rijen) per bestand. Elke rij vertegenwoordigt één profiel. Namen van gesplitste bestanden worden toegevoegd met een getal dat aangeeft dat het bestand deel uitmaakt van een grotere exportbewerking: `filename.csv` , `filename_2.csv` , `filename_3.csv` . Voor meer informatie, leest de [ plannende sectie ](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) van het activerende partijbestemmingsleerprogramma. |
| Maximumaantal aangepaste uploadsoorten dat in een gegevensstroom kan worden geactiveerd | 10 | Door het systeem afgedwongen geleiding | Wanneer het activeren van [ douane uploadt publiek ](/help/segmentation/ui/audience-portal.md#import-audience) aan op dossier-gebaseerde bestemmingen, is er een grens van 10 zulk publiek dat u in een dataflow kunt activeren. Lees meer over het werkschema om [ douane te activeren upload publiek aan op dossier-gebaseerde bestemmingen ](/help/destinations/ui/activate-batch-profile-destinations.md#select-audiences). |

{style="table-layout:auto"}

### Ad-hocactivering {#ad-hoc-activation}

De hieronder gidsen zijn op de [ ad-hoc activering ](/help/destinations/api/ad-hoc-activation-api.md) methode van toepassing.

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Publiek geactiveerd per ad-hocactiveringstaak | 80 | Door het systeem afgedwongen geleiding | Op dit moment kan elke ad-hocactiveringstaak maximaal 80 soorten publiek activeren. Als u probeert meer dan 80 soorten publiek per taak te activeren, mislukt de taak. Dit gedrag kan in toekomstige versies worden gewijzigd. |
| Gelijktijdige ad-hocactiveringstaken per publiek | 1 | Door het systeem afgedwongen geleiding | Voer niet meer dan één gelijktijdige ad-hocactiveringstaak per publiek uit. |

{style="table-layout:auto"}

### Activering van Edge-personalisatiedoelen {#edge-destinations-activation}

De hieronder begeleiding is van toepassing op activering door [ de bestemmingen van de randverpersoonlijking ](/help/destinations/destination-types.md#advanced-enterprise-destinations).

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Maximum aantal [ Aangepaste verpersoonlijking ](/help/destinations/catalog/personalization/custom-personalization.md) bestemmingen | 10 | Prestatiegerichting | U kunt gegevensstromen aan 10 Aangepaste verpersoonlijkingsbestemmingen per zandbak plaatsen. |
| Maximumaantal kenmerken dat per sandbox aan een verpersoonlijkingsdoel is toegewezen | 30 | Prestatiegerichting | Een maximum van 30 attributen kan in een dataflow aan een verpersoonlijkingsbestemming, per zandbak worden in kaart gebracht. |

{style="table-layout:auto"}

### Dataset exporteren {#dataset-exports}

De uitvoer van de gegevensset wordt momenteel gesteund in a **[!UICONTROL First Full and then Incremental]** [ patroon ](/help/destinations/ui/export-datasets.md#scheduling). De gidsen die in deze sectie *worden beschreven zijn op de eerste volledige uitvoer* van toepassing die voorkomen nadat een werkschema van de datasetuitvoer opstelling is.

<!--

| Guardrail | Limit | Limit Type | Description |
| --- | --- | --- | --- |
| Size of exported datasets | 5 billion records | Soft | The limit described here for dataset exports is a *soft guardrail*. For example, while the user interface will not block you from exporting datasets larger than 5 billion records, the behavior is unpredictable and exports might either fail or have very long export latency. |

{style="table-layout:auto"}

-->

#### Dataset-typen {#dataset-types}

De instructies voor de uitvoer van gegevenssets zijn van toepassing op twee soorten gegevenssets die uit Experience Platform worden geëxporteerd, zoals hieronder beschreven:

**Datasets die op het schema en de datasets worden gebaseerd van de Gebeurtenissen van de Ervaring XDM die op een ander schema** worden gebaseerd

In het geval van datasets die op het schema van de Gebeurtenissen van de Ervaring XDM worden gebaseerd, omvat het datasetschema een top level timestamp kolom. Gegevens worden alleen toegevoegd. In het geval van datasets die op een ander schema worden gebaseerd, kan het datasetschema een timestamp kolom omvatten en de gegevens worden opgenomen op een upsert manier.

De onderstaande zachte handleiding is van toepassing op alle gegevenssets die uit Experience Platform worden geëxporteerd. Bekijk ook de harde instructies hieronder, specifiek voor verschillende dataset en compressietypen.

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Grootte van geëxporteerde gegevenssets | 5 miljard records | Prestatiegerichting | De grens die hier voor datasetuitvoer wordt beschreven is a *zachte guardrail*. Bijvoorbeeld, terwijl de gebruikersinterface u niet zal blokkeren van het uitvoeren van datasets groter dan 5 miljard verslagen, is het gedrag onvoorspelbaar en de uitvoer zou of kunnen ontbreken of zeer lange uitvoerlatentie hebben. |

{style="table-layout:auto"}

#### Guardrails voor de uitvoer van geplande gegevenssets

Voor geplande, of terugkomende datasetuitvoer, zijn de hieronder grails voor de twee formaten van het uitgevoerde dossier (JSON of parquet) identiek, en gegroepeerd door datasettype.

>[!WARNING]
>
>Exporteren naar JSON-bestanden worden alleen in de gecomprimeerde modus ondersteund.

| Het type DataSet | Guardrail | Het type Guardrail | Beschrijving |
|---------|----------|---------|-------|
| Datasets die op het **worden gebaseerd XDM schema van de Gebeurtenissen van de Ervaring** | Laatste 365 dagen met gegevens | Door het systeem afgedwongen geleiding | De gegevens van het laatste kalenderjaar worden uitgevoerd. |
| Datasets die op **worden gebaseerd om het even welk schema buiten het schema van de Gebeurtenissen van de Ervaring XDM** | Tien miljard records in alle geëxporteerde bestanden in een gegevensstroom | Door het systeem afgedwongen geleiding | Het recordaantal van de dataset moet minder dan tien miljard voor samengeperste JSON of parquet dossiers en één miljoen voor ongecomprimeerde parketdossiers zijn, anders ontbreekt de uitvoer. Verminder de grootte van de dataset die u probeert uit te voeren als het groter is dan de toegestane drempel. |

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

Lees meer over [het exporteren van datasets](/help/destinations/ui/export-datasets.md).


### Destination SDK guardrails {#destination-sdk-guardrails}

[ Destination SDK ](/help/destinations/destination-sdk/overview.md) is een reeks van configuratie APIs die u toestaan om de patronen van de bestemmingsintegratie voor Experience Platform te vormen om publiek en profielgegevens aan uw eindpunt te leveren, die op gegevens en authentificatieformaten van uw keus wordt gebaseerd. De onderstaande instructies zijn van toepassing op de doelen die u met Destination SDK configureert.

| Guardrail | Limiet | Limiettype | Beschrijving |
| --- | --- | --- | --- |
| Maximum aantal [ privé douanebestemmingen ](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | Prestatiegerichting | Met Destination SDK kunt u maximaal vijf eigen streaming- of batchbestemmingen maken. Neem contact op met een aangepaste zorgvertegenwoordiger als u meer dan vijf van dergelijke doelen moet maken. |
| Profielexportbeleid voor Destination SDK | <ul><li>`maxBatchAgeInSecs` (minimaal 301 en maximaal 3600)</li><li>`maxNumEventsInBatch` (minimaal 1.000 en maximaal 10.000)</li></ul> | Door het systeem afgedwongen geleiding | Wanneer het gebruiken van de [ configureerbare samenvoeging ](destination-sdk/functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) optie voor uw bestemming, houd rekening met de minimum en maximumwaarden die bepalen hoe vaak de berichten van HTTP naar uw op API-Gebaseerde bestemming worden verzonden en hoeveel profielen de berichten zouden moeten omvatten. |
| OAuth 2 tokenleven voor Destination SDK | Minimaal 24 uur aanbevolen | Prestatiegerichting | Voor bestemmingen die [ OAuth 2 vergunning ](/help/destinations/destination-sdk/functionality/destination-configuration/oauth2-authorization.md) gebruiken, adviseert Adobe plaatsend de waarden van het toegangstoken leven aan een minimum van 24 uren. Verbindingen met tokens met een levensduur van minder dan 1 uur leiden tot het wegvallen van profielen tijdens activering. |

{style="table-layout:auto"}

### Beleidswijziging en opnieuw proberen van bestemming {#destination-throttling-and-retry-policy}

Gegevens over drempelwaarden of beperkingen voor bepaalde bestemmingen. Deze sectie verstrekt ook informatie betreffende het hertestbeleid voor bestemmingen.

| Type bestemming | Beschrijving |
| --- | --- |
| Enterprise-bestemmingen (HTTP-API, Amazon Kinesis, Azure EventHubs) | In 95 percent van de tijd, probeert Experience Platform om een productietolerantie van minder dan 10 minuten voor met succes verzonden berichten met een tarief van minder dan 10.000 verzoeken per seconde voor elke dataflow aan een ondernemingsbestemming aan te bieden. <br> In het geval van mislukte verzoeken aan uw ondernemingsbestemming, slaat Experience Platform de ontbroken verzoeken op en probeert tweemaal om de verzoeken naar uw eindpunt te verzenden. |

{style="table-layout:auto"}

## Volgende stappen

Raadpleeg de volgende documentatie voor meer informatie over andere Experience Platform Services-instructies, informatie over end-to-end latentie en licentiegegevens uit Real-Time CDP Product Description-documenten:

* [Real-Time CDP guardrails](/help/rtcdp/guardrails/overview.md)
* [ de diagrammen van de de latentie van begin tot eind ](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) voor diverse diensten van Experience Platform.
* [ Real-Time Customer Data Platform (B2C Edition - Prime en de Pakketten van Ultimate) ](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [ Real-Time Customer Data Platform (B2P - de Pakketten van Prime en van Ultimate) ](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [ Real-Time Customer Data Platform (B2B - de Pakketten van Prime en van Ultimate) ](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
