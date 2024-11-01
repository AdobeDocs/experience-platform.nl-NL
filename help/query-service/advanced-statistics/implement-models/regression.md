---
title: Regressiealgoritmen
description: Leer om diverse regressiealgoritmen met zeer belangrijke parameters, beschrijvingen, en voorbeeldcode te vormen en te optimaliseren om u te helpen geavanceerde statistische modellen uitvoeren.
role: Developer
source-git-commit: b248e8f8420b617a117d36aabad615e5bbf66b58
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 2%

---

# Regressiealgoritmen {#regression-algorithms}

Dit document biedt een overzicht van verschillende regressiealgoritmen, waarbij de nadruk ligt op hun configuratie, sleutelparameters en praktisch gebruik in geavanceerde statistische modellen. Regressiealgoritmen worden gebruikt om de relatie tussen afhankelijke en onafhankelijke variabelen te modelleren, waarbij continue resultaten worden voorspeld op basis van waargenomen gegevens. Elke sectie omvat parameterbeschrijvingen en voorbeeldcode om u te helpen deze algoritmen voor taken uitvoeren en optimaliseren zoals lineair, willekeurig bos, en overlevingsregressie.

## [!DNL Decision Tree] regressie {#decision-tree-regression}

[!DNL Decision Tree] leren is een onder toezicht staande leermethode die wordt gebruikt in statistieken, datamining en het leren van machines. In deze aanpak wordt een structuur voor de classificatie of de regressiebeslissing gebruikt als een voorspellend model om conclusies te trekken over een reeks waarnemingen.

**Parameters**

In de onderstaande tabel worden de belangrijkste parameters voor het configureren en optimaliseren van de prestaties van modellen met beslissingsstructuren beschreven.

| Parameter | Beschrijving | Standaardwaarde | Mogelijke waarden |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|--------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Het maximumaantal bakken bepaalt hoe ononderbroken eigenschappen in discrete intervallen worden verdeeld. Dit beïnvloedt hoe de eigenschappen bij elke knoop van de beslissingsboom worden verdeeld. Meer bins zorgen voor een hogere granulariteit. | 32 | Moet ten minste 2 en ten minste het aantal categorieën in een categorisch kenmerk zijn. |
| `CACHE_NODE_IDS` | Als `false` , gaat het algoritme bomen tot uitvoerders over om instanties met knopen aan te passen. Indien `true`, plaatst het algoritme knoop IDs voor elke instantie in het voorgeheugen. Caching kan de opleiding van diepere bomen versnellen. | false | `true` of `false` |
| `CHECKPOINT_INTERVAL` | Hiermee geeft u aan hoe vaak de in de cache opgeslagen knooppunt-id&#39;s moeten worden gecontroleerd. `10` betekent bijvoorbeeld dat de cache elke 10 herhalingen wordt gecontroleerd. | 10 | (>=1) |
| `IMPURITY` | Het criterium dat wordt gebruikt voor de berekening van de informatieverbreding (hoofdlettergevoelig). | `gini` | `entropy`, `gini` |
| `MAX_DEPTH` | De maximale diepte van de boom (niet-negatief). De diepte `0` betekent bijvoorbeeld 1 bladknooppunt en de diepte `1` 1 interne node en 2 bladknooppunten. | 5 | [ 0, 30 ] |
| `MIN_INFO_GAIN` | De minimuminformatietoename die voor een splitsing wordt vereist om bij een boomknoop te worden overwogen. | 0,0 | (>=0,0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | De minimale fractie van het gewogen aantal monsters die elk kind na een splitsing moet hebben. Als een splitsing ertoe leidt dat de fractie van het totale gewicht in een van beide kinderen kleiner is dan deze waarde, wordt deze weggegooid. | 0,0 | (>=0,0, 0,5) |
| `MIN_INSTANCES_PER_NODE` | Het minimum aantal exemplaren dat elk kind na een splitsing moet hebben. Als een splitsing minder instanties oplevert dan deze waarde, wordt de splitsing genegeerd. | 1 | (>=1) |
| `MAX_MEMORY_IN_MB` | Het maximale geheugen, in MB, dat is toegewezen aan histogramaggregatie. Als het geheugen te klein is, wordt slechts één knooppunt gesplitst per herhaling, wat ertoe kan leiden dat de aggregaten de grootte overschrijden. | 256 |                                                                                                        |
| `PREDICTION_COL` | De parameter voor de naam van de voorspellingskolom. | &quot;voorspelling&quot; | Willekeurige tekenreeks |
| `SEED` | De parameter voor het willekeurige zaad. | N.v.t. | Willekeurig 64-bits getal |
| `WEIGHT_COL` | De parameter voor de naam van de gewichtskolom. Als deze niet is ingesteld of leeg is, worden alle instantiegewichten behandeld als `1.0` . | niet ingesteld |                                                                                                        |

{style="table-layout:auto"}

**Voorbeeld**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'decision_tree_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Factorization Machines] regressie {#factorization-machines-regression}

[!DNL Factorization Machines] is een regressieleeralgoritme dat normale gradiënt descent en de AdamW solver steunt. Het algoritme is gebaseerd op het document door S. Rendle (2010), &quot;[!DNL Factorization Machines]&quot;.

**Parameters**

In de onderstaande tabel staan de belangrijkste parameters voor het configureren en optimaliseren van de prestaties van [!DNL Factorization Machines] Regression.

| Parameter | Beschrijving | Standaardwaarde | Mogelijke waarden |
|------------------------|--------------------------------------------------------------------------------------|---------------|----------------|
| `TOL` | De convergentie-tolerantie. | `1E-6` | (>= 0) |
| `FACTOR_SIZE` | De dimensionaliteit van de factoren. | 8 | (>= 0) |
| `FIT_INTERCEPT` | Of een onderscheppingsterm moet passen. | `true` | `true`, `false` |
| `FIT_LINEAR` | Of de lineaire term moet worden gebruikt (ook wel de eenrichtingsterm genoemd). | `true` | `true`, `false` |
| `INIT_STD` | De standaardafwijking van de oorspronkelijke coëfficiënten. | 0,01 | (>= 0) |
| `MAX_ITER` | Het aantal herhalingen dat het algoritme moet uitvoeren. | 100 | (>= 0) |
| `MINI_BATCH_FRACTION` | De mini-batchfractie, die binnen het bereik `(0, 1]` moet liggen. | 1,0 | `(0, 1]` |
| `REG_PARAM` | De regularisatieparameter. | 0,0 | (>= 0) |
| `SEED` | Het willekeurige zaadje. | NIET INGESTELD | Willekeurig 64-bits getal |
| `SOLVER` | Het solveralgoritme dat wordt gebruikt voor optimalisatie. | &quot;adamW&quot; | `gd`, `adamW` |
| `STEP_SIZE` | De initiële stapgrootte voor de eerste stap (vergelijkbaar met de leersnelheid). | 1,0 |                   |
| `PREDICTION_COL` | De naam van de voorspellingskolom. | &quot;voorspelling&quot; | Willekeurige tekenreeks |

{style="table-layout:auto"}

**Voorbeeld**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'factorization_machines_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Generalized Linear] regressie {#generalized-linear-regression}

In tegenstelling tot lineaire regressie, waarbij ervan wordt uitgegaan dat het resultaat een normale (Gaussiaanse) distributie volgt, staan [!DNL Generalized Linear] Models (GLMs) het resultaat toe om verschillende typen distributies te volgen, zoals [!DNL Poisson] of binomiaal, afhankelijk van de aard van de gegevens.

**Parameters**

In de onderstaande tabel staan de belangrijkste parameters voor het configureren en optimaliseren van de prestaties van [!DNL Generalized Linear] regression.

| Parameter | Beschrijving | Standaardwaarde | Mogelijke waarden |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-------------------------------------------------------------------------|
| `MAX_ITER` | Hiermee stelt u het maximum aantal herhalingen in (van toepassing bij gebruik van de solver `irls` ). | 25 | (>= 0) |
| `REG_PARAM` | De regularisatieparameter. | NIET INGESTELD | (>= 0) |
| `TOL` | De convergentie-tolerantie. | `1E-6` | (>= 0) |
| `AGGREGATION_DEPTH` | De voorgestelde diepte voor `treeAggregate`. | 2 | (>= 2) |
| `FAMILY` | De familieparameter, die de foutendistributie beschrijft die in het model wordt gebruikt. Ondersteunde opties zijn `gaussian` , `binomial` , `poisson` , `gamma` en `tweedie` . | &quot;gaussiaans&quot; | `gaussian`, `binomial`, `poisson`, `gamma`, `tweedie` |
| `FIT_INTERCEPT` | Of een onderscheppingsterm moet passen. | `true` | `true`, `false` |
| `LINK` | De koppelingsfunctie, die de relatie tussen de lineaire voorspeller en het gemiddelde van de distributiefunctie bepaalt. Ondersteunde opties zijn `identity` , `log` , `inverse` , `logit` , `probit` , `cloglog` en `sqrt` . | NIET INGESTELD | `identity`, `log`, `inverse`, `logit`, `probit`, `cloglog`, `sqrt` |
| `LINK_POWER` | De index in de power link functie, van toepassing op de [!DNL Tweedie] familie. Als deze optie niet is ingesteld, wordt deze standaard ingesteld op `1 - variancePower` , na het R `statmod` -pakket. De bevoegdheden van de verbinding van 0, 1, -1, en 0.5 beantwoorden aan Logboek, Identiteit, Omgekeerde, en Sqrt verbinding, respectievelijk. | 1 |
| `SOLVER` | Het solveralgoritme dat wordt gebruikt voor optimalisatie. Ondersteunde optie: `irls` (minst vierkanten herhaaldelijk opnieuw gewogen). | &quot;irls&quot; | `irls` |
| `VARIANCE_POWER` | De macht in de variantfunctie van de [!DNL Tweedie] distributie, die de verhouding tussen variantie en gemiddelde bepaalt. Ondersteunde waarden zijn 0 en `[1, inf)` . | 0,0 | 0, `[1, inf)` |
| `LINK_PREDICTION_COL` | De kolomnaam voor de koppelingsvoorspelling (lineaire voorspelling). | NIET INGESTELD | Willekeurige tekenreeks |
| `OFFSET_COL` | De naam van de verschuivingskolom. Indien niet ingesteld, worden alle instantieverschuivingen behandeld als 0,0. De verschuivingsfunctie heeft een constante coëfficiënt van 1,0. | NIET INGESTELD |                                                                        |
| `WEIGHT_COL` | De naam van de gewichtskolom. Als deze niet is ingesteld of leeg is, worden alle instantiegewichten behandeld als `1.0` . In de Binomial-familie komen de gewichten overeen met het aantal onderzoeken en worden niet-gehele gewichten afgerond in de AIC-berekening. | NIET INGESTELD |                                                                        |

{style="table-layout:auto"}

**Voorbeeld**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'generalized_linear_reg'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Gradient Boosted Tree] regressie {#gradient-boosted-tree-regression}

Bomen met verloopversterkingen (GBT&#39;s) zijn een effectieve methode voor indeling en regressie die de voorspellingen van meerdere beslissingsbomen combineert om de voorspellende nauwkeurigheid en de prestaties van het model te verbeteren.

**Parameters**

In de onderstaande tabel staan de belangrijkste parameters voor het configureren en optimaliseren van de prestaties van [!DNL Gradient Boosted Tree] regression.

| Parameter | Beschrijving | Standaardwaarde | Mogelijke waarden |
|-------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Het maximumaantal banden dat wordt gebruikt om ononderbroken eigenschappen in discrete intervallen te verdelen, die helpt bepalen hoe de eigenschappen bij elke knoop van de beslissingsboom worden gesplitst. Meer bins zorgen voor een hogere granulariteit. | 32 | Moet ten minste 2 en gelijk zijn aan of groter zijn dan het aantal categorieën in een categorisch kenmerk. |
| `CACHE_NODE_IDS` | Als `false` , gaat het algoritme bomen tot uitvoerders over om instanties met knopen aan te passen. Indien `true`, plaatst het algoritme knoop IDs voor elke instantie in het voorgeheugen. Caching kan de opleiding van diepere bomen versnellen. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Hiermee geeft u aan hoe vaak de in de cache opgeslagen knooppunt-id&#39;s moeten worden gecontroleerd. `10` betekent bijvoorbeeld dat de cache om de 10 herhalingen wordt gecontroleerd. | 10 | (>= 1) |
| `MAX_DEPTH` | De maximale diepte van de boom (niet-negatief). De diepte `0` betekent bijvoorbeeld 1 bladknooppunt en de diepte `1` 1 interne node met 2 bladknooppunten. | 5 | (>= 0) |
| `MIN_INFO_GAIN` | De minimuminformatietoename die voor een splitsing wordt vereist om bij een boomknoop te worden overwogen. | 0,0 | (>= 0,0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | De minimale fractie van het gewogen aantal monsters die elk kind na een splitsing moet hebben. Als een splitsing ertoe leidt dat de fractie van het totale gewicht in een van beide kinderen kleiner is dan deze waarde, wordt deze weggegooid. | 0,0 | (>= 0,0, &lt;= 0,5) |
| `MIN_INSTANCES_PER_NODE` | Het minimum aantal exemplaren dat elk kind na een splitsing moet hebben. Als een splitsing minder instanties oplevert dan deze waarde, wordt de splitsing genegeerd. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Het maximale geheugen, in MB, dat is toegewezen aan histogramaggregatie. Als deze waarde te klein is, wordt slechts één knooppunt gesplitst per iteratie en kunnen de aggregaten ervan deze grootte overschrijden. | 256 |                                                                                                      |
| `PREDICTION_COL` | De kolomnaam voor voorspellingsuitvoer. | &quot;voorspelling&quot; | Willekeurige tekenreeks |
| `VALIDATION_INDICATOR_COL` | De kolomnaam die aangeeft of elke rij wordt gebruikt voor training of validatie. `false` voor training en `true` voor validatie. | NIET INGESTELD | Willekeurige tekenreeks |
| `LEAF_COL` | De kolomnaam voor bladindexen. De voorspelde bladindex van elke instantie in elke boomstructuur, die wordt gegenereerd door het traversal van de voorvolgorde. | &quot;&quot; | Willekeurige tekenreeks |
| `FEATURE_SUBSET_STRATEGY` | Het aantal eigenschappen overwogen voor het verdelen bij elke boomknoop. | &quot;auto&quot; | `auto`, `all`, `onethird`, `sqrt`, `log2`, `n` (waarbij `n` een fractie tussen 0 en 1,0 is) |
| `SEED` | Het willekeurige zaadje. | NIET INGESTELD | Willekeurig 64-bits getal |
| `WEIGHT_COL` | De kolomnaam, bijvoorbeeld, gewichten. Als deze niet is ingesteld of leeg is, worden alle instantiegewichten behandeld als `1.0` . | NIET INGESTELD |                                                                                                      |
| `LOSS_TYPE` | De verliesfunctie die het [!DNL Gradient Boosted Tree] -model probeert te minimaliseren. | &quot;kwadraat&quot; | `squared` (L2) en `absolute` (L1). Opmerking: waarden zijn niet hoofdlettergevoelig. |
| `STEP_SIZE` | De stapgrootte (ook wel de leersnelheid genoemd) in het bereik `(0, 1]` die wordt gebruikt om de bijdrage van elke schatter te verlagen. | 0,1 | `(0, 1]` |
| `MAX_ITER` | Het maximumaantal herhalingen voor het algoritme. | 20 | (>= 0) |
| `SUBSAMPLING_RATE` | Het deel van de trainingsgegevens dat wordt gebruikt om elke beslissingsstructuur te leren, in het bereik `(0, 1]` . | 1,0 | `(0, 1]` |

{style="table-layout:auto"}

**Voorbeeld**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'gradient_boosted_tree_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Isotonic] regressie {#isotonic-regression}

[!DNL Isotonic Regression] is een algoritme dat wordt gebruikt om afstanden herhaaldelijk aan te passen terwijl de relatieve orde van ongelijkenissen in de gegevens bewaard blijft.

**Parameters**

In de onderstaande tabel staan de belangrijkste parameters voor het configureren en optimaliseren van de prestaties van [!DNL Isotonic Regression] .

| Parameter | Beschrijving | Standaardwaarde | Mogelijke waarden |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `ISOTONIC` | Geeft aan of de uitvoerreeks isotonisch (toenemend) moet zijn wanneer deze `true` of antitonisch (afnemend) is wanneer `false` . | `true` | `true`, `false` |
| `WEIGHT_COL` | De kolomnaam, bijvoorbeeld, gewichten. Als deze niet is ingesteld of leeg is, worden alle instantiegewichten behandeld als `1.0` . | NIET INGESTELD | Willekeurige tekenreeks |
| `PREDICTION_COL` | De kolomnaam voor voorspellingsuitvoer. | &quot;voorspelling&quot; | Willekeurige tekenreeks |
| `FEATURE_INDEX` | De index van de functie, van toepassing wanneer `featuresCol` een vectorkolom is. Als deze niet is ingesteld, is de standaardwaarde `0` . Anders heeft het geen effect. | 0 |                 |

{style="table-layout:auto"}

**Voorbeeld**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'isotonic_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Linear] regressie {#linear-regression}

[!DNL Linear Regression] is een onder toezicht staand computerleeralgoritme dat een lineaire vergelijking met gegevens past om de relatie tussen een afhankelijke variabele en onafhankelijke eigenschappen te modelleren.

**Parameters**

In de onderstaande tabel staan de belangrijkste parameters voor het configureren en optimaliseren van de prestaties van [!DNL Linear Regression] .

| Parameter | Beschrijving | Standaardwaarde | Mogelijke waarden |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `MAX_ITER` | Het maximale aantal herhalingen. | 100 | (>= 0) |
| `REGPARAM` | De regularisatieparameter die wordt gebruikt om de complexiteit van het model te bepalen. | 0,0 | (>= 0) |
| `ELASTICNETPARAM` | De ElasticNet-mixparameter, die de balans tussen L1 (Lasso) en L2 (Ridge) boetes bepaalt. Bij de waarde 0 wordt een L2-boete toegepast, bij de waarde 1 wordt een L1-boete toegepast. | 0,0 | (>= 0, &lt;= 1) |

{style="table-layout:auto"}

**Voorbeeld**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'linear_reg'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Random Forest Regression] {#random-forest-regression}

[!DNL Random Forest Regression] is een ensemble-algoritme dat meerdere beslissingsbomen bouwt tijdens de training en de gemiddelde voorspelling van die bomen voor regressietaken retourneert, waardoor overplaatsing wordt voorkomen.

**Parameters**

In de onderstaande tabel staan de belangrijkste parameters voor het configureren en optimaliseren van de prestaties van [!DNL Random Forest Regression] .

| Parameter | Beschrijving | Standaardwaarde | Mogelijke waarden |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Het maximumaantal banden dat wordt gebruikt om ononderbroken eigenschappen in discretie te brengen en te bepalen hoe de eigenschappen bij elke knoop worden verdeeld. Meer bins zorgen voor een hogere granulariteit. | 32 | Moet ten minste 2 en ten minste gelijk zijn aan het aantal categorieën in een categorisch kenmerk. |
| `CACHE_NODE_IDS` | Als `false` , gaat het algoritme bomen tot uitvoerders over om instanties met knopen aan te passen. Als `true`, het algoritme knoop IDs voor elke instantie in cache plaatst, die de opleiding van diepere bomen versnelt. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Hiermee geeft u aan hoe vaak de in de cache opgeslagen knooppunt-id&#39;s moeten worden gecontroleerd. `10` betekent bijvoorbeeld dat de cache om de 10 herhalingen wordt gecontroleerd. | 10 | (>= 1) |
| `IMPURITY` | Het criterium dat wordt gebruikt voor de berekening van de informatieverbreding (hoofdlettergevoelig). | &quot;entropie&quot; | `entropy`, `gini` |
| `MAX_DEPTH` | De maximale diepte van de boom (niet-negatief). De diepte `0` betekent bijvoorbeeld 1 bladknooppunt en de diepte `1` 1 interne node en 2 bladknooppunten. | 5 | [ 0, 30 ] |
| `MIN_INFO_GAIN` | De minimuminformatietoename die voor een splitsing wordt vereist om bij een boomknoop te worden overwogen. | 0,0 | (>= 0,0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | De minimale fractie van het gewogen aantal monsters die elk kind na een splitsing moet hebben. Als een splitsing ertoe leidt dat de fractie van het totale gewicht in een van beide kinderen kleiner is dan deze waarde, wordt deze weggegooid. | 0,0 | (>= 0,0, &lt;= 0,5) |
| `MIN_INSTANCES_PER_NODE` | Het minimum aantal exemplaren dat elk kind na een splitsing moet hebben. Als een splitsing minder instanties oplevert dan deze waarde, wordt de splitsing genegeerd. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Het maximale geheugen, in MB, dat is toegewezen aan histogramaggregatie. Als deze waarde te klein is, wordt slechts één knooppunt gesplitst per iteratie en kunnen de aggregaten ervan deze grootte overschrijden. | 256 |                                                                                                      |
| `BOOTSTRAP` | Of laarzentestmonsters moeten worden gebruikt bij het bouwen van bomen. | TRUE | `true`, `false` |
| `NUM_TREES` | Het aantal bomen dat moet worden opgeleid (ten minste 1). Als `1` , wordt geen bootstrapping gebruikt. Als dit groter is dan `1`, wordt de overvulling bootstrapping toegepast. | 20 | (>= 1) |
| `SUBSAMPLING_RATE` | Het deel van trainingsgegevens dat wordt gebruikt om elke beslissingsboom te trainen, in het bereik `(0, 1]`. | 1,0 | `(0, 1]` |
| `LEAF_COL` | De kolomnaam voor bladindexen, de voorspelde bladindex van elke instantie in elke boom, die wordt gegenereerd door het vooraf doorlopen van de volgorde. | &quot;&quot; | Willekeurige tekenreeks |
| `PREDICTION_COL` | De kolomnaam voor voorspellingsuitvoer. | &quot;voorspelling&quot; | Willekeurige tekenreeks |
| `SEED` | Het willekeurige zaadje. | NIET INGESTELD | Willekeurig 64-bits getal |
| `WEIGHT_COL` | De kolomnaam, bijvoorbeeld, gewichten. Als deze niet is ingesteld of leeg is, worden alle instantiegewichten behandeld als `1.0` . | NIET INGESTELD | Een geldige kolomnaam of leeg laten. |

{style="table-layout:auto"}

**Voorbeeld**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'random_forest_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Survival Regression] {#survival-regression}

[!DNL Survival Regression] wordt gebruikt voor het passen van een parametrisch regressiemodel, het [!DNL Accelerated Failure Time] (AFT)-model genoemd, gebaseerd op het [!DNL Weibull distribution] . Het kan instanties in blokken voor betere prestaties stapelen.

**Parameters**

In de onderstaande tabel staan de belangrijkste parameters voor het configureren en optimaliseren van de prestaties van [!DNL Survival Regression] .

| Parameter | Beschrijving | Standaardwaarde | Mogelijke waarden |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `MAX_ITER` | Het maximumaantal herhalingen dat het algoritme zou moeten in werking stellen. | 100 | (>= 0) |
| `TOL` | De convergentie-tolerantie. | `1E-6` | (>= 0) |
| `AGGREGATION_DEPTH` | De voorgestelde diepte voor `treeAggregate`. Als de eigenschapafmetingen of het aantal verdelingen groot zijn, kan deze parameter aan een grotere waarde worden geplaatst. | 2 | (>= 2) |
| `FIT_INTERCEPT` | Of een onderscheppingsterm moet passen. | TRUE | `true`, `false` |
| `PREDICTION_COL` | De kolomnaam voor voorspellingsuitvoer. | &quot;voorspelling&quot; | Willekeurige tekenreeks |
| `CENSOR_COL` | De kolomnaam voor censuur. De waarde `1` geeft aan dat de gebeurtenis heeft plaatsgevonden (ongecensureerd), terwijl `0` betekent dat de gebeurtenis is gecensureerd. | &quot;censor&quot; | 0,1 |
| `MAX_BLOCK_SIZE_IN_MB` | Het maximale geheugen in MB voor het stapelen van invoergegevens in blokken. Als de resterende gegevensgrootte in een partitie kleiner is, wordt deze waarde dienovereenkomstig aangepast. Bij de waarde `0` is automatische aanpassing mogelijk. | 0,0 | (>= 0) |

{style="table-layout:auto"}

**Voorbeeld**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'survival_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## Volgende stappen

Nadat u dit document hebt gelezen, weet u nu hoe u verschillende regressiealgoritmen kunt configureren en gebruiken. Daarna, verwijs naar de documenten op [ classificatie ](./classification.md) en [ groeperend ](./clustering.md) om over andere soorten geavanceerde statistische modellen te leren.
