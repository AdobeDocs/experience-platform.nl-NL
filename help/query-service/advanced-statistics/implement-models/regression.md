---
title: Regressiealgoritmen
description: Leer om diverse regressiealgoritmen met zeer belangrijke parameters, beschrijvingen, en voorbeeldcode te vormen en te optimaliseren om u te helpen geavanceerde statistische modellen uitvoeren.
role: Developer
exl-id: d38733bb-0420-40bf-a70b-19e0e0e58730
source-git-commit: 8b9cfb48a11701f0e4b358416c6b627bedf1db8b
workflow-type: tm+mt
source-wordcount: '2384'
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
| `MAX_BINS` | Deze parameter specificeert het maximumaantal banden die worden gebruikt om ononderbroken eigenschappen in diskrediet te brengen en splits bij elke knoop te bepalen. Meer bindingen resulteren in een fijnere korreligheid en gedetailleerdheid. | 32 | Moet ten minste 2 en ten minste het aantal categorieën in een categorisch kenmerk zijn. |
| `CACHE_NODE_IDS` | Deze parameter bepaalt of om knoop IDs voor elke instantie in het voorgeheugen onder te brengen. Als `false` , gaat het algoritme bomen tot uitvoerders over om instanties met knopen aan te passen. Als `true`, het algoritme knoop IDs voor elke instantie in cache plaatst, die de opleiding van diepere bomen kan versnellen. Gebruikers kunnen bepalen hoe vaak de cache moet worden gecontroleerd of uitschakelen door `CHECKPOINT_INTERVAL` in te stellen. | false | `true` of `false` |
| `CHECKPOINT_INTERVAL` | Deze parameter specificeert hoe vaak de caching knoop IDs zou moeten worden gecontroleerd. Als u deze bijvoorbeeld instelt op `10` , wordt de cache elke 10 herhalingen gecontroleerd. Dit is alleen van toepassing als `CACHE_NODE_IDS` is ingesteld op `true` en de map checkpoint is geconfigureerd in `org.apache.spark.SparkContext` . | 10 | (>=1) |
| `IMPURITY` | Deze parameter specificeert het criterium dat wordt gebruikt voor het berekenen van de informatietoename. Ondersteunde waarden zijn `entropy` en `gini` . | `gini` | `entropy`, `gini` |
| `MAX_DEPTH` | Deze parameter geeft de maximale diepte van de structuur aan. Een diepte van `0` betekent bijvoorbeeld 1 bladknooppunt, terwijl een diepte van `1` 1 intern knooppunt en 2 bladknooppunten betekent. De diepte moet binnen het bereik `[0, 30]` liggen. | 5 | [ 0, 30 ] |
| `MIN_INFO_GAIN` | Deze parameter plaatst de minimuminformatietoename die voor een spleet wordt vereist om als geldig op een boomknoop te worden beschouwd. | 0,0 | (>=0,0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Deze parameter specificeert de minimumfractie van de gewogen steekproeftelling die elke kindknoop na een spleet moet hebben. Als een van beide onderliggende knooppunten een fractie heeft die kleiner is dan deze waarde, wordt de splitsing genegeerd. | 0,0 | [ 0.0, 0.5 ] |
| `MIN_INSTANCES_PER_NODE` | Deze parameter plaatst het minimumaantal instanties dat elke kindknoop na een spleet moet hebben. Als een splitsing minder instanties oplevert dan deze waarde, wordt de splitsing genegeerd als ongeldig. | 1 | (>=1) |
| `MAX_MEMORY_IN_MB` | Deze parameter specificeert het maximumgeheugen, in megabytes (MB), dat voor histogramaggregatie wordt toegewezen. Als het geheugen te klein is, wordt slechts één knooppunt gesplitst per herhaling en kunnen de aggregaten ervan deze grootte overschrijden. | 256 | Een positief geheel getal |
| `PREDICTION_COL` | Deze parameter specificeert de naam van de kolom die voor het opslaan van voorspellingen wordt gebruikt. | &quot;voorspelling&quot; | Willekeurige tekenreeks |
| `SEED` | Met deze parameter wordt het willekeurige zaad ingesteld dat in het model wordt gebruikt. | Geen | Willekeurig 64-bits getal |
| `WEIGHT_COL` | Deze parameter geeft de naam van de gewichtskolom aan. Wanneer deze parameter niet is ingesteld of leeg is, worden alle instantiegewichten behandeld als `1.0` . | Niet ingesteld | Willekeurige tekenreeks |

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

In de onderstaande tabel staan de belangrijkste parameters voor het configureren en optimaliseren van de prestaties van [!DNL Factorization Machines] regression.

| Parameter | Beschrijving | Standaardwaarde | Mogelijke waarden |
|------------------------|-------------------------------------------------------------------------------------------------|---------------|-----------------------|
| `TOL` | Deze parameter specificeert de convergentie tolerantie voor het algoritme. Hogere waarden kunnen resulteren in snellere convergentie, maar minder nauwkeurigheid. | `1E-6` | (>= 0) |
| `FACTOR_SIZE` | Deze parameter definieert de dimensionaliteit van de factoren. Hogere waarden verhogen de complexiteit van het model. | 8 | (>= 0) |
| `FIT_INTERCEPT` | Deze parameter geeft aan of het model een onderscheppingsterm moet bevatten. | `true` | `true`, `false` |
| `FIT_LINEAR` | Deze parameter specificeert of om een lineaire termijn (ook genoemd de 1 wegtermijn) in het model te omvatten. | `true` | `true`, `false` |
| `INIT_STD` | Deze parameter definieert de standaardafwijking van de oorspronkelijke coëfficiënten die in het model worden gebruikt. | 0,01 | (>= 0) |
| `MAX_ITER` | Deze parameter specificeert het maximumaantal herhalingen voor het algoritme om in werking te stellen. | 100 | (>= 0) |
| `MINI_BATCH_FRACTION` | Deze parameter stelt de mini-batchfractie in, die het gedeelte van gegevens bepaalt dat in elke batch wordt gebruikt. Het moet binnen het bereik `(0, 1]` vallen. | 1,0 | `(0, 1]` |
| `REG_PARAM` | Deze parameter plaatst de regularisatieparameter om overfitting te verhinderen. | 0,0 | (>= 0) |
| `SEED` | Deze parameter specificeert het willekeurige zaad dat voor modelinitialisatie wordt gebruikt. | Geen | Willekeurig 64-bits getal |
| `SOLVER` | Deze parameter specificeert het solveralgoritme dat voor optimalisering wordt gebruikt. | &quot;adamW&quot; | `gd` (verlopende descent), `adamW` |
| `STEP_SIZE` | Deze parameter geeft de initiële stapgrootte (of leersnelheid) voor de eerste optimaliseringsstap aan. | 1,0 | Elke positieve waarde |
| `PREDICTION_COL` | Deze parameter geeft de naam op van de kolom waarin de voorspellingen worden opgeslagen. | &quot;voorspelling&quot; | Willekeurige tekenreeks |

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
| `LINK_POWER` | Deze parameter specificeert de index in de macht verbindingsfunctie. De parameter is alleen van toepassing op de [!DNL Tweedie] -familie. Als deze niet is ingesteld, wordt de standaardwaarde ingesteld op `1 - variancePower` , die wordt uitgelijnd met het R `statmod` -pakket. Specifieke verbindingsbevoegdheden 0, 1, -1 en 0,5 komen overeen met respectievelijk de koppelingen Logboek, Identiteit, Omgekeerd en Sqrt. | 1 | Willekeurige numerieke waarde |
| `SOLVER` | Het solveralgoritme dat wordt gebruikt voor optimalisatie. Ondersteunde optie: `irls` (minst vierkanten herhaaldelijk opnieuw gewogen). | &quot;irls&quot; | `irls` |
| `VARIANCE_POWER` | Deze parameter specificeert de macht in de variancefunctie van de [!DNL Tweedie] distributie, die de verhouding tussen variantie en gemiddelde bepaalt. Ondersteunde waarden zijn 0 en `[1, inf)` . Variantiebevoegdheden van 0, 1 en 2 komen overeen met respectievelijk de families Gaussiaans, Poisson en Gamma. | 0,0 | 0, `[1, inf)` |
| `LINK_PREDICTION_COL` | De kolomnaam voor de koppelingsvoorspelling (lineaire voorspelling). | NIET INGESTELD | Willekeurige tekenreeks |
| `OFFSET_COL` | De naam van de verschuivingskolom. Indien niet ingesteld, worden alle instantieverschuivingen behandeld als 0,0. De verschuivingsfunctie heeft een constante coëfficiënt van 1,0. | NIET INGESTELD | Willekeurige tekenreeks |
| `WEIGHT_COL` | De naam van de gewichtskolom. Als deze niet is ingesteld of leeg is, worden alle instantiegewichten behandeld als `1.0` . In de Binomial-familie komen de gewichten overeen met het aantal onderzoeken en worden niet-gehele gewichten afgerond in de AIC-berekening. | NIET INGESTELD | Willekeurige tekenreeks |

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
| `MAX_MEMORY_IN_MB` | Het maximale geheugen, in MB, dat is toegewezen aan histogramaggregatie. Als deze waarde te klein is, wordt slechts één knooppunt gesplitst per iteratie en kunnen de aggregaten ervan deze grootte overschrijden. | 256 | Een positief geheel getal |
| `PREDICTION_COL` | De kolomnaam voor voorspellingsuitvoer. | &quot;voorspelling&quot; | Willekeurige tekenreeks |
| `VALIDATION_INDICATOR_COL` | De kolomnaam die aangeeft of elke rij wordt gebruikt voor training of validatie. `false` voor training en `true` voor validatie. | NIET INGESTELD | Willekeurige tekenreeks |
| `LEAF_COL` | De kolomnaam voor bladindexen. De voorspelde bladindex van elke instantie in elke boomstructuur, die wordt gegenereerd door het traversal van de voorvolgorde. | &quot;&quot; | Willekeurige tekenreeks |
| `FEATURE_SUBSET_STRATEGY` | Deze parameter specificeert het aantal eigenschappen om voor spleten bij elke boomknoop in overweging te nemen. | &quot;auto&quot; | `auto` , `all` , `onethird` , `sqrt` , `log2` of een fractie tussen 0 en 1,0 |
| `SEED` | Het willekeurige zaadje. | NIET INGESTELD | Willekeurig 64-bits getal |
| `WEIGHT_COL` | De kolomnaam, bijvoorbeeld, gewichten. Als deze niet is ingesteld of leeg is, worden alle instantiegewichten behandeld als `1.0` . | NIET INGESTELD | Willekeurige tekenreeks |
| `LOSS_TYPE` | Deze parameter geeft de verliesfunctie aan die het [!DNL Gradient Boosted Tree] model minimaliseert. | &quot;kwadraat&quot; | `squared` (L2) en `absolute` (L1). Opmerking: waarden zijn niet hoofdlettergevoelig. |
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
| `FEATURE_INDEX` | De index van de functie, van toepassing wanneer `featuresCol` een vectorkolom is. Als deze niet is ingesteld, is de standaardwaarde `0` . Anders heeft het geen effect. | 0 | Een niet-negatief geheel getal |

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
| `MAX_DEPTH` | De maximale diepte van de boom (niet-negatief). De diepte `0` betekent bijvoorbeeld 1 bladknooppunt en de diepte `1` 1 interne node en 2 bladknooppunten. | 5 | Een niet-negatief geheel getal |
| `MIN_INFO_GAIN` | De minimuminformatietoename die voor een splitsing wordt vereist om bij een boomknoop te worden overwogen. | 0,0 | (>= 0,0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | De minimale fractie van het gewogen aantal monsters die elk kind na een splitsing moet hebben. Als een splitsing ertoe leidt dat de fractie van het totale gewicht in een van beide kinderen kleiner is dan deze waarde, wordt deze weggegooid. | 0,0 | (>= 0,0, &lt;= 0,5) |
| `MIN_INSTANCES_PER_NODE` | Het minimum aantal exemplaren dat elk kind na een splitsing moet hebben. Als een splitsing minder instanties oplevert dan deze waarde, wordt de splitsing genegeerd. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Het maximale geheugen, in MB, dat is toegewezen aan histogramaggregatie. Als deze waarde te klein is, wordt slechts één knooppunt gesplitst per iteratie en kunnen de aggregaten ervan deze grootte overschrijden. | 256 | (>= 1) |
| `BOOTSTRAP` | Of laarzentestmonsters moeten worden gebruikt bij het bouwen van bomen. | TRUE | `true`, `false` |
| `NUM_TREES` | Het aantal bomen dat moet worden opgeleid (ten minste 1). Als `1` , wordt geen bootstrapping gebruikt. Als dit groter is dan `1`, wordt de overvulling bootstrapping toegepast. | 20 | (>= 1) |
| `SUBSAMPLING_RATE` | Het deel van trainingsgegevens dat wordt gebruikt om elke beslissingsboom te trainen, in het bereik `(0, 1]`. | 1,0 | (>= 0,0, &lt;= 1) |
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

Nadat u dit document hebt gelezen, weet u nu hoe u verschillende regressiealgoritmen kunt configureren en gebruiken. Daarna, verwijs naar de documenten op [&#x200B; classificatie &#x200B;](./classification.md) en [&#x200B; groeperend &#x200B;](./clustering.md) om over andere soorten geavanceerde statistische modellen te leren.
