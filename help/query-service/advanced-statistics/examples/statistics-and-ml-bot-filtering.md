---
title: Bot filteren met behulp van statistieken en leren van machines
description: Leer hoe u Distiller-statistieken voor gegevens en computerleren gebruikt om beide activiteiten te identificeren en te filteren om nauwkeurige analyses en verbeterde gegevensintegriteit te garanderen.
exl-id: 30d98281-7d15-47a6-b365-3baa07356010
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 0%

---

# Bot filteren met behulp van statistieken en machinaal leren

De praktische toepassingen van beide filteren bestrijken verschillende industrieën. In e-commerce verbetert het de betrouwbaarheid van de cijfers van de omrekeningskoers, kunnen nieuwswebsites van het verlichten van valse betrokkenheidsmetriek profiteren, en de advertentienetwerken kunnen eerlijke facturering verzekeren. Om nauwkeurige analyses te handhaven en gegevensintegriteit in klikstroom of Webverkeersgegevens te verzekeren, moet u beide activiteit richten. U kunt kwalitatief hoogstaande analysegegevens garanderen door Data Distiller te gebruiken voor het implementeren van effectieve gegevensfilters en het verwijderen van ongewenste verkeer.

Dit document biedt een uitgebreide gids voor het identificeren en filteren van beide activiteiten met behulp van SQL- en computerleertechnieken. Het biedt een progressie van complementaire benaderingen, te beginnen met elementaire filtering en de overgang naar machinaal leren-gebaseerde detectie en evaluatie. Neem dit robuuste kader aan om uw bot detectie te verbeteren en uw gegevensintegriteit te behouden.

## Begrijp beide activiteit {#understand-bot-activity}

Beide activiteiten kunnen worden geïdentificeerd door spikes in gebruikersacties binnen specifieke tijdintervallen te detecteren. Bijvoorbeeld, kunnen de bovenmatige kliks die door één enkele gebruiker in een korte tijd worden uitgevoerd op allebei gedrag wijzen. De twee belangrijkste kenmerken die bij beide filters worden gebruikt, zijn:

- **ECID (identiteitskaart van de Bezoeker van Experience Cloud):** Een universele, blijvende identiteitskaart die bezoekers identificeert.
- **Tijdstempel:** de tijd en de datum wanneer een activiteit op de website voorkomt.

In de onderstaande voorbeelden ziet u hoe u SQL- en computerleertechnieken kunt gebruiken om beide activiteiten te identificeren, te verfijnen en te voorspellen. Gebruik deze methoden om de gegevensintegriteit te verbeteren en te zorgen dat de analysemogelijkheden actief zijn.

## Filteren op basis van SQL {#sql-based-bot-filtering}

Dit op SQL-Gebaseerde bot het filtreren voorbeeld toont aan hoe te om SQL vragen te gebruiken om drempels te bepalen en beide activiteit te ontdekken die op vooraf bepaalde regels wordt gebaseerd. Deze basisbenadering helpt anomalieën in Webverkeer te identificeren door ongebruikelijke activiteit te verwijderen. Door detectieregels aan te passen met gedefinieerde drempelwaarden en intervallen, kunt u beide filters op effectieve wijze aanpassen aan uw specifieke verkeerspatronen.

### Drempelwaarden voor beide activiteiten definiëren {#define-thresholds}

Begin door uw dataset te analyseren om gebruikersgedrag te identificeren en te categoriseren. Focus op kenmerken zoals ECID, timestamp en `webPageDetails.name` (de naam van de bezochte webpagina) om gebruikersacties te groeperen en patronen te detecteren die beide activiteiten aangeven.

De SQL-query hieronder laat zien hoe u de drempel van meer dan 60 klikken in één minuut toepast om verdachte activiteiten te identificeren:

```sql
SELECT *
FROM analytics_events_table
WHERE enduserids._experience.ecid NOT IN (
    SELECT enduserids._experience.ecid
    FROM analytics_events_table
    GROUP BY Unix_timestamp(timestamp) / 60, enduserids._experience.ecid
    HAVING Count(*) > 60
);
```

### Naar meerdere intervallen uitbreiden {#expand-to-multiple-intervals}

Vervolgens definieert u verschillende tijdsintervallen voor drempelwaarden. Deze intervallen kunnen het volgende omvatten:

- **1 minieme interval:** Tot 60 klikken.
- **5 minieme interval:** Tot 300 klikt.
- **miniem interval 30:** Tot 1800 klikt.

Met de volgende SQL-query wordt een weergave met de naam `analytics_events_clicks_count_criteria` gemaakt voor het afhandelen van drempels over meerdere intervallen. De verklaring consolideert kliktellingen voor 1 minuut, 5 minuten, en 30 minieme intervallen in een gestructureerde dataset en vlagt potentiële beide activiteit die op vooraf bepaalde drempels wordt gebaseerd.

```sql
CREATE VIEW analytics_events_clicks_count_criteria as  
SELECT struct (
        cast(count_1_min AS int) one_minute,
        cast(count_5_mins AS int) five_minute,
        cast(count_30_mins AS int) thirty_minute
       ) count_per_id,
       id,
      struct (
        struct (name) webpagedetails
      ) web,
      CASE
        WHEN count.one_minute > 50 THEN 1
        ELSE 0
      END AS isBot
FROM (
  SELECT table_count_1_min.mcid AS id,
         count_1_min,
         count_5_mins,
         count_30_mins,
         table_count_1_min.name AS name
  FROM (
      (SELECT mcid, Max(count_1_min) AS count_1_min, name
       FROM (SELECT enduserids._experience.mcid.id AS mcid,
                    Count(*) AS count_1_min,
                    web.webPageDetails.name AS name
             FROM delta_table
             WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                               AND TO_TIMESTAMP('2019-09-01 23:00:00')
             GROUP BY UNIX_TIMESTAMP(timestamp) / 60,
                      enduserids._experience.mcid.id,
                      web.webPageDetails.name)
       GROUP BY mcid, name) AS table_count_1_min
       LEFT JOIN
       (SELECT mcid, Max(count_5_mins) AS count_5_mins, name
        FROM (SELECT enduserids._experience.mcid.id AS mcid,
                     Count(*) AS count_5_mins,
                     web.webPageDetails.name AS name
              FROM delta_table
              WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                                AND TO_TIMESTAMP('2019-09-01 23:00:00')
              GROUP BY UNIX_TIMESTAMP(timestamp) / 300,
                       enduserids._experience.mcid.id,
                       web.webPageDetails.name)
        GROUP BY mcid, name) AS table_count_5_mins
       ON table_count_1_min.mcid = table_count_5_mins.mcid
       LEFT JOIN
       (SELECT mcid, Max(count_30_mins) AS count_30_mins, name
        FROM (SELECT enduserids._experience.mcid.id AS mcid,
                     Count(*) AS count_30_mins,
                     web.webPageDetails.name AS name
              FROM delta_table
              WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                                AND TO_TIMESTAMP('2019-09-01 23:00:00')
              GROUP BY UNIX_TIMESTAMP(timestamp) / 1800,
                       enduserids._experience.mcid.id,
                       web.webPageDetails.name)
        GROUP BY mcid, name) AS table_count_30_mins
       ON table_count_1_min.mcid = table_count_30_mins.mcid
  )
)
```

De instructie voegt gegevens van `table_count_1_min` , `table_count_5_mins` en `table_count_30_mins` samen met de waarde `mcid` en webpagina. Het consolideert dan kliktellingen voor elke gebruiker over veelvoudige tijdintervallen om een volledige mening van gebruikersactiviteit te verstrekken. Tot slot identificeert de het vlaggen logica dan gebruikers die 50 klikken in één minuut overschrijden en merkt hen als bots (`isBot = 1`).

### Structuur van uitvoergegevensset

De uitvoerdataset is gestructureerd met zowel vlakke als genestelde gebieden. Deze structuur staat flexibiliteit toe wanneer het ontdekken van anomolisch verkeer en steunt geavanceerde het filtreren strategieën die SQL en machine het leren gebruiken. De geneste velden bevatten `count` en `web` , waarin gedetailleerde informatie over activiteitsdrempels en webpagina&#39;s wordt ingekapseld. Door deze metriek vast te leggen, kunnen functies eenvoudig worden uitgepakt voor training en voorspellingstaken.

Het volgende schemadiagram schetst de structuur van de resulterende dataset en benadrukt hoe de genestelde en vlakke gebieden voor efficiënte verwerking en beide opsporing kunnen worden gebruikt.

```console
root
 |-- count: struct (nullable = false)
 |    |-- one_minute: integer (nullable = true)
 |    |-- five_minute: integer (nullable = true)
 |    |-- thirty_minute: integer (nullable = true)
 |-- id: string (nullable = true)
 |-- web: struct (nullable = false)
 |    |-- webpagedetails: struct (nullable = false)
 |    |    |-- name: string (nullable = true)
 |-- isBot: integer (nullable = false)
```

### De gegevensset met uitvoergegevens die moet worden gebruikt voor opleiding

Het resultaat van deze expressie kan er ongeveer zo uitzien als in de onderstaande tabel. In de tabel fungeert de kolom `isBot` als een label dat onderscheid maakt tussen beide en niet-beide activiteiten.

```console
| `id`         | `count_per_id`                                      |`isBot`| `web`                                                                                                                    |
|--------------|-----------------------------------------------------|-------|------------------------------------------------------------------------------------------------------------------------|
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":99}| 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 1E+18        | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"KR+CC8TQzPyMOE/bk7EGgN3lSvP8OsxeI2aLaVrbaeLn8XK3y3zok2ryVyZoiBu3"}}                       |
| 1.00007E+18  | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"8DN0dM4rlvJxt4oByYLKZ/wuHyq/8CvsWNyXvGYnImytXn/bjUizfRSl86vmju7MFMXxnhTBoCWLHtyVSWro9LYg0MhN8jGbswLRLXoOIyh2wduVbc9XeN8yyQElkJm3AW3zcqC7iXNVv2eBS8vwGg=="}} |
| 1.00008E+18  | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"KR+CC8TQzPyMOE/bk7EGgN3lSvP8OsxeI2aLaVrbaeLn8XK3y3zok2ryVyZoiBu3"}}                       |
```

## Geavanceerde statistische functies voor beide filters {#statistical-functions-for-bot-filtering}

Dit tweede voorbeeld bouwt op basis SQL het filtreren voort door machine het leren technieken op te nemen om drempels te verfijnen en het filtreren nauwkeurigheid te verbeteren. Door geavanceerde statistische functies te gebruiken, zoals regressieanalyse of clusteringsalgoritmen, introduceert deze benadering voorspellende mogelijkheden die u kunt gebruiken om modellen te ontwikkelen voor de behandeling van complexe datasets met grotere nauwkeurigheid.

### Een trainingsgegevensset maken {#build-a-training-dataset}

Bereid eerst een dataset met vlakke en genestelde structuren voor die het machine het leren model (zoals hierboven beschreven) kan gebruiken. De verdere begeleiding op hoe te om dit te doen kan in [&#x200B; worden gevonden Werkend met genestelde documentatie van gegevensstructuren &#x200B;](../../key-concepts/nested-data-structures.md). Groepeer de gegevens op tijdstempel, gebruikers-id en webpaginanaam om patronen in beide activiteiten te identificeren.

### De clausules van TRANSFORM en van OPTIONS van het gebruik voor modelverwezenlijking {#transform-and-preprocess}

Om uw dataset om te zetten en uw machine het leren model effectief te vormen, volg de hieronder stappen. In de stappen wordt gedetailleerd beschreven hoe u null-waarden kunt verwerken, functies kunt voorbereiden en de parameters van het model kunt definiëren voor optimale prestaties.

>[!TIP]
>
>Meer leren over het gebruiken van transformaties en het preprocessing van uw gegevens, verwijs naar de [&#x200B; documentatie van de transformatietechnieken van de Eigenschap transformatie &#x200B;](../feature-transformation.md).

1. Als u null-waarden in numerieke, tekenreeks- en booleaanse kolommen wilt vullen, gebruikt u respectievelijk de functies `numeric_imputer` , `string_imputer` en `boolean_imputer` . Met deze stap zorgt u ervoor dat het leeralgoritme van de computer de gegevens zonder fouten kan verwerken.
2. Pas eigenschaptransformaties toe om de gegevens voor modellering voor te bereiden. Pas `binarized`, `quantile_discretizer` of `string_indexer` toe om de kolommen te categoriseren of te standaardiseren. Geef vervolgens de uitvoer van de imputers ( `numeric_imputer` en `string_imputer` ) door naar volgende transformatoren zoals `string_indexer` of `quantile_discretizer` om betekenisvolle functies te maken.
3. Gebruik de functie `vector_assembler` om de getransformeerde kolommen te combineren tot één functiekolom. Schaal de functies vervolgens met `min_max_scaler` om de waarden te normaliseren voor betere modelprestaties. Opmerking: in het SQL-voorbeeld wordt de laatste transformatie die in de TRANSFORM-component wordt vermeld, de eigenschapkolom die wordt gebruikt door het model voor machinaal leren.
4. Geef het modeltype en eventuele andere hyperparameters op in de OPTIONS-component. `decision_tree_classifier` is hier bijvoorbeeld gekozen omdat dit een classificatieprobleem is. Andere parameters zoals `max_depth` zijn aangepast (`MAX_DEPTH=4`) om het model af te stemmen voor betere prestaties.
5. Combineer functies en geef een label op voor de uitvoergegevens. Gebruik de clausule SELECT om de dataset voor opleiding te specificeren. Deze clausule zou zowel de eigenschapkolommen (`count_per_id`, `web`, `id`) als de etiketkolom (`isBot`) moeten omvatten, die erop wijst of een actie waarschijnlijk een bot zal zijn.

Uw instructie ziet er mogelijk hetzelfde uit als het onderstaande voorbeeld.

```sql
CREATE MODEL bot_filtering_model
TRANSFORM (
  numeric_imputer(count_per_id.one_minute, 'mean') imputed_one_minute,
  numeric_imputer(count_per_id.five_minute, 'mode') imputed_five_minute,
  numeric_imputer(count_per_id.thirty_minute) imputed_thirty_minute,
  string_imputer(id, 'unknown') imputed_id,
  string_indexer(imputed_id) si_id,
  quantile_discretizer(imputed_five_minute) buckets_five,
  string_indexer(web.webpagedetails.NAME) si_name,
  quantile_discretizer(imputed_thirty_minute) buckets_thirty,
  vector_assembler(array(si_id, imputed_one_minute, buckets_five, si_name, buckets_thirty)) features,
  min_max_scaler(features) scaled_features
)
OPTIONS (model_type='decision_tree_classifier', max_depth=4, label='isBot')
AS
SELECT count_per_id, isBot, web, id FROM analytics_events_clicks_count_criteria;
```

**Resultaat**

In de hieronder weergegeven resultaten wordt het model `bot_filtering_model` gemaakt met een unieke id, naam en versie. Deze uitvoer dient als referentie voor het bijhouden en beheren van modellen. Gebruik deze verwijzingen om de nauwkeurige configuratie en de versie te identificeren die voor voorspellingen of evaluaties worden vereist.

```console
           Created Model ID           |       Created Model       | Version
|--------------------------------------+---------------------------+---------
 2fb4b49e-d35c-44cf-af19-cc210e7dc72c | bot_filtering_model       |       1
```

### Evalueer het getrainde model {#evaluate-trained-model}

Nadat u het model hebt gemaakt, gebruikt u de opdracht `MODEL_EVALUATE` om de prestaties ervan te evalueren. Deze stap zorgt ervoor dat het model voldoet aan de nauwkeurigheids- en prestatievereisten voor het detecteren van beide activiteiten.

Gebruik de volgende argumenten in uw SQL-opdracht om het model te evalueren:

1. Specificeer de modelnaam (`bot_filtering_model`) om op te geven welk model te evalueren. Deze naam moet overeenkomen met de naam die u eerder hebt gemaakt met de opdracht `CREATE MODEL` .
2. Verstrek de modelversie (`1`) in het tweede argument om de versie van het model te specificeren u wilt evalueren. Als er meerdere versies zijn, wordt de juiste versie gebruikt.
3. Omvat de dataset van de evaluatie om de dataset voor evaluatie te bepalen. Zorg ervoor dat de dataset dezelfde functiekolommen (`count_per_id`, `web`, `id`) en de labelkolom (`isBot`) bevat die tijdens de training worden gebruikt.

>[!NOTE]
>
>De transformaties die tijdens modeltraining worden toegepast, worden automatisch toegepast tijdens de evaluatie.

```sql
SELECT *
FROM   model_evaluate(bot_filtering_model, 1,
                      SELECT count_per_id, isBot, web, id
                      FROM   analytics_events_clicks_count_criteria);
```

**Resultaat**

De reactie omvat metriek zoals nauwkeurigheid, precisie, herinnering, en AUC-ROC. De resultaten bevestigen of het model goed presteerde.

>[!NOTE]
>
>Waarden in het bereik 0-1 geven de verhoudingen of waarschijnlijkheid aan, met 1,0 geeft de perfecte prestaties aan.

```console
auc_roc | accuracy | precision | recall
|---------+----------+-----------+--------
     1.0 |      1.0 |       1.0 |    1.0
```

| **Metrisch** | **Beschrijving** |
|--------------|-----------------------------------------------------------------------------------------------------|
| `auc_roc` | Deze metrische waarde geeft aan hoe effectief uw model bots en non-bots kan classificeren. Het wordt op grote schaal gebruikt voor de evaluatie van classificatiemodellen. |
| `accuracy` | Het percentage correcte voorspellingen dat door het model wordt gemaakt. |
| `precision` | Het aandeel van echte beide voorspellingen onder alle voorspelde bots. |
| `recall` | Het percentage echte bots dat is gedetecteerd van alle echte bots. |

>[!TIP]
>
>Voor gebruik op productiesandboxen, overweeg evaluatie van het model op testdatasets om ervoor te zorgen het effectief generaliseert.

### Voorspelende botactiviteit {#predict-bot-activity}

Gebruik het bevel `MODEL_PREDICT` met het getrainde model om te identificeren welke gebruikers (`id`) bots zijn. Volg de onderstaande stappen om voorspellingen te genereren voor het identificeren van beide activiteiten:

1. Gebruik de modelnaam (`bot_filtering_model`) in het eerste argument om te specificeren welk model voor voorspellingen te gebruiken.
2. Specificeer de modelversie (`1`) in het tweede argument om de correcte versie van het model te verzekeren wordt gebruikt.
3. Als u de juiste gegevens voor voorspellingen wilt opgeven, gebruikt u een SELECT-instructie om de functiekolommen op te geven (`count_per_id`, `web`, `id` ). Neem de labelkolom (`isBot`) niet op omdat het model voorspellingen voor dit veld zal genereren.

```sql
SELECT *
FROM model_predict(bot_filtering_model, 1,
    SELECT count_per_id, web, id FROM analytics_events_clicks_count_criteria
);
```

**Resultaat**

De reactie omvat voorspellingen voor elke gebruiker (`id`) samen met details over hun activiteit en het de classificatieresultaat van het model. Deze uitvoer maakt een gedetailleerde analyse mogelijk van het gedrag van de gebruiker en de classificatie van beide activiteiten door het model.

<!-- Q) Anil, why is there no ID in the first two rows? Can we get that info? Or should it be the same as the other IDs? -->

```console
         id          | count.one_minute | count.five_minute | count.thirty_minute |                                                                  web.webpagedetails.name                                                                  | prediction
|---------------------+------------------+-------------------+---------------------+-------+----------------------------------------------------------------------------------------------------------------------------------------------------+------------
                     |              110 |                   |                     |   4UNDilcY5VAgu2pRmX4/gtVnj+YxDDQaJd1G8p8WX46//wYcrHy+APUN0I556E80j1gIzFmilA6DV4s0Zcs4ruiP36gLgC7bj4TH0q6LU0E=                                             |        1.0  
                     |              105 |                   |                     |   lrSaZk04Yq+5P9+6l4BohwXik0s0/XeW9X28ZgWt1yj1QQztiAt9Qgt2WYrWcAeoGZChAJw/l8e4ojZDT5WHCjteSt35S01Vv1JzDGPAg+IyhIzMTsVyLpW8WWpXjJoMCt6Tv7fFdF73EIH+IrK5fA== |        1.0
 2553215812530219515 |               99 |                 1 |                   1 |   KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg==                                                                 |        1.0
 2553215812530219515 |               99 |                 1 |                   1 |   KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg==                                                                 |        1.0
```

In de onderstaande tabel wordt elke meting uitgelegd:

| Kolomnaam | Beschrijving |
|---------------------------|----------------------------------------------------------------------------------------------------------|
| `id` | De unieke id voor elke gebruiker. |
| `count.one_minute` | De geaggregeerde kliktellingen voor 1 minieme intervallen. |
| `count.five_minute` | De geaggregeerde kliktellingen voor vijf-minieme intervallen. |
| `count.thirty_minute` | De geaggregeerde kliktellingen voor intervallen van 30 minuten. |
| `web.webpagedetails.name` | De naam van de bezochte webpagina. Dit verstrekt context voor gebruikersactiviteit. |
| `prediction` | De voorspelling van het model. Een `1.0` -resultaat geeft aan dat de gebruiker is gemarkeerd als een bot op basis van zijn activiteitspatronen. |

## Uw modellen beheren {#manage-models}

Gebruik de SQL-sleutelwoorden in de onderstaande sectie om uw modellen voor het leren van machines te beheren.

### Beschikbare modellen weergeven {#list-available-models}

Beheer en reviseer de modellen op efficiënte wijze met de opdracht `SHOW MODELS;` . Deze opdracht geeft een overzicht van alle modellen voor machinaal leren die in de huidige werkruimte zijn gemaakt. De uitvoer biedt een overzicht van de beschikbare modellen en bevat de namen, versies en andere metagegevens van deze modellen.

```sql
SHOW MODELS;
```

### Modellen verwijderen {#delete-models}

Als u bronnen wilt vrijmaken en alleen de relevante modellen wilt behouden, gebruikt u de opdracht `DROP MODEL` om verouderde of onnodige modellen te verwijderen. Met deze opdracht verwijdert u elk model voor machinaal leren dat na de trefwoorden is opgegeven. In het onderstaande voorbeeld wordt `bot_filtering_model` uit het systeem verwijderd.

```sql
DROP MODEL bot_filtering_model;
```

## Volgende stappen

Door dit document te lezen, hebt u geleerd hoe u beide activiteiten kunt identificeren en filteren met behulp van SQL- en machinetechnieken die gebruikmaken van Data Distiller-methoden. Pas daarna deze concepten op uw datasets toe en automatiseer modelomscholing voor ononderbroken verbetering.
