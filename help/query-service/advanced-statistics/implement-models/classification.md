---
title: Classificatiealgoritmen
description: Leer om diverse classificatiealgoritmen met zeer belangrijke parameters, beschrijvingen, en voorbeeldcode te vormen en te optimaliseren om u te helpen geavanceerde statistische modellen uitvoeren.
role: Developer
source-git-commit: b248e8f8420b617a117d36aabad615e5bbf66b58
workflow-type: tm+mt
source-wordcount: '2360'
ht-degree: 2%

---

# Classificatiealgoritmen {#classification-algorithms}

Dit document biedt een overzicht van verschillende classificatiealgoritmen, waarbij de nadruk ligt op hun configuratie, sleutelparameters en praktisch gebruik in geavanceerde statistische modellen. Classificatiealgoritmen worden gebruikt om categorieën aan gegevenspunten toe te wijzen die op inputeigenschappen worden gebaseerd. Elke sectie omvat parameterbeschrijvingen en voorbeeldcode om u te helpen deze algoritmen voor taken uitvoeren en optimaliseren zoals beslissingsbomen, willekeurig bos, en naive classificatie Bayes.

## [!DNL Decision Tree Classifier] {#decision-tree-classifier}

[!DNL Decision Tree Classifier] is een leermethode onder toezicht die wordt gebruikt in statistieken, datamining en het leren van machines. In deze aanpak wordt een beslissingsstructuur gebruikt als een voorspellend model voor classificatietaken, waarbij conclusies worden getrokken uit een reeks waarnemingen.

**Parameters**

In de onderstaande tabel staan de belangrijkste parameters voor het configureren en optimaliseren van de prestaties van een [!DNL Decision Tree Classifier] .

| Parameter | Beschrijving | Standaardwaarde | Mogelijke waarden |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------|
| `MAX_BINS` | Het maximumaantal bakken bepaalt hoe ononderbroken eigenschappen in discrete intervallen worden verdeeld. Dit beïnvloedt hoe de eigenschappen bij elke knoop van de beslissingsboom worden verdeeld. Meer bins zorgen voor een hogere granulariteit. | 32 | Moet ten minste 2 en ten minste gelijk zijn aan het aantal categorieën in een categorisch kenmerk. |
| `CACHE_NODE_IDS` | Als `false` , gaat het algoritme bomen tot uitvoerders over om instanties met knopen aan te passen. Als `true`, het algoritme knoop IDs voor elke instantie in cache plaatst, die de opleiding van diepere bomen versnelt. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Hiermee geeft u aan hoe vaak de in de cache opgeslagen knooppunt-id&#39;s moeten worden gecontroleerd. `10` betekent bijvoorbeeld dat de cache om de 10 herhalingen wordt gecontroleerd. | 10 | (>= 1) |
| `IMPURITY` | Het criterium dat wordt gebruikt voor de berekening van de informatieverbreding (hoofdlettergevoelig). | &quot;gini&quot; | `entropy`, `gini` |
| `MAX_DEPTH` | De maximale diepte van de boom (niet-negatief). De diepte `0` betekent bijvoorbeeld 1 bladknooppunt en de diepte `1` 1 interne node en 2 bladknooppunten. | 5 | [ 0, 30 ] |
| `MIN_INFO_GAIN` | De minimuminformatietoename die voor een splitsing wordt vereist om bij een boomknoop te worden overwogen. | 0,0 | (>= 0,0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | De minimale fractie van het gewogen aantal monsters die elk kind na een splitsing moet hebben. Als een splitsing ertoe leidt dat de fractie van het totale gewicht in een van beide kinderen kleiner is dan deze waarde, wordt deze weggegooid. | 0,0 | (>= 0,0, &lt;= 0,5) |
| `MIN_INSTANCES_PER_NODE` | Het minimum aantal exemplaren dat elk kind na een splitsing moet hebben. Als een splitsing minder instanties oplevert dan deze waarde, wordt de splitsing genegeerd. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Het maximale geheugen, in MB, dat is toegewezen aan histogramaggregatie. Als deze waarde te klein is, wordt slechts één knooppunt gesplitst per iteratie en kunnen de aggregaten ervan deze grootte overschrijden. | 256 |                    |
| `PREDICTION_COL` | De kolomnaam voor voorspellingsuitvoer. | &quot;voorspelling&quot; | Willekeurige tekenreeks |
| `SEED` | Het willekeurige zaadje. | NIET INGESTELD | Willekeurig 64-bits getal |
| `WEIGHT_COL` | De kolomnaam, bijvoorbeeld, gewichten. Als deze niet is ingesteld of leeg is, worden alle instantiegewichten behandeld als `1.0` . | NIET INGESTELD | Willekeurige tekenreeks |
| `ONE_VS_REST` | Hiermee schakelt u het inpakken van dit algoritme met One-vs-Rest in of uit, dat wordt gebruikt voor classificatieproblemen met meerdere klassen. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Voorbeeld**

```sql
Create MODEL modelname OPTIONS(
  type = 'decision_tree_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Factorization Machine Classifier] {#factorization-machine-classifier}

[!DNL Factorization Machine Classifier] is een classificatiealgoritme dat normale gradiënt descent en de solver AdamW steunt. Het indelingsmodel van de Factorization Machine maakt gebruik van logistiek verlies, dat kan worden geoptimaliseerd via een afdaling van het verloop en bevat vaak regularisatievoorwaarden zoals L2 om overmaat te voorkomen.

**Parameters**

In de onderstaande tabel staan de belangrijkste parameters voor het configureren en optimaliseren van de prestaties van de [!DNL Factorization Machine Classifier] .

| Parameter | Beschrijving | Standaardwaarde | Mogelijke waarden |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-------------------------------------------------------------------------------------------------------|
| `TOL` | De convergentietolerantie, die de nauwkeurigheid van de optimalisering controleert. | `1E-6` | (>= 0) |
| `FACTOR_SIZE` | De dimensionaliteit van de factoren. | 8 | (>= 0) |
| `FIT_INTERCEPT` | Geeft aan of een onderscheppingsterm moet passen. | `true` | `true`, `false` |
| `FIT_LINEAR` | Geeft aan of de lineaire term moet worden gebruikt (ook wel de term uit één richting genoemd). | `true` | `true`, `false` |
| `INIT_STD` | De standaardafwijking voor het initialiseren van coëfficiënten. | 0,01 | (>= 0) |
| `MAX_ITER` | Het maximumaantal herhalingen voor het uit te voeren algoritme. | 100 | (>= 0) |
| `MINI_BATCH_FRACTION` | Het deel van de gegevens dat tijdens de training in minibatches wordt gebruikt. Moet binnen het bereik `(0, 1]` vallen. | 1,0 | `(0, 1]` |
| `REG_PARAM` | De regularisatieparameter, die modelingewikkeldheid helpt te controleren en overfitting te verhinderen. | 0,0 | (>= 0) |
| `SEED` | Het willekeurige zaad voor het controleren van willekeurige processen in het algoritme. | NIET INGESTELD | Willekeurig 64-bits getal |
| `SOLVER` | Het solveralgoritme dat wordt gebruikt voor optimalisatie. Ondersteunde opties zijn `gd` (verlopende descent) en `adamW` . | &quot;adamW&quot; | `gd`, `adamW` |
| `STEP_SIZE` | De initiële stapgrootte voor optimalisatie, vaak geïnterpreteerd als de leersnelheid. | 1,0 | > 0 |
| `PROBABILITY_COL` | De kolomnaam voor voorspelde klasse voorwaardelijke kansen. Opmerking: niet alle modellen hebben een goede kalibratie van de waarschijnlijkheden; deze moeten worden behandeld als betrouwbaarheidsscores in plaats van als exacte waarschijnlijkheid. | &quot;waarschijnlijkheid&quot; | Willekeurige tekenreeks |
| `PREDICTION_COL` | De kolomnaam voor voorspelde klassenlabels. | &quot;voorspelling&quot; | Willekeurige tekenreeks |
| `RAW_PREDICTION_COL` | De kolomnaam voor onbewerkte voorspellingswaarden (ook wel betrouwbaarheid genoemd). | &quot;rawPrediction&quot; | Willekeurige tekenreeks |
| `ONE_VS_REST` | Geeft aan of de indeling One-vs-Rest moet worden ingeschakeld voor meerdere klassen. | FALSE | `true`, `false` |

{style="table-layout:auto"}

**Voorbeeld**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'factorization_machines_classifier'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Gradient Boosted Tree Classifier] {#gradient-boosted-tree-classifier}

[!DNL Gradient Boosted Tree Classifier] gebruikt een samenstel van beslissingsbomen om de nauwkeurigheid van classificatietaken te verbeteren, die veelvoudige bomen combineren om modelprestaties te verbeteren.

**Parameters**

In de onderstaande tabel staan de belangrijkste parameters voor het configureren en optimaliseren van de prestaties van de [!DNL Gradient Boosted Tree Classifier] .

| Parameter | Beschrijving | Standaardwaarde | Mogelijke waarden |
|-------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Het maximumaantal bakken bepaalt hoe ononderbroken eigenschappen in discrete intervallen worden verdeeld. Dit beïnvloedt hoe de eigenschappen bij elke knoop van de beslissingsboom worden verdeeld. Meer bins zorgen voor een hogere granulariteit. | 32 | Moet ten minste 2 en gelijk zijn aan of groter zijn dan het aantal categorieën in een categorisch kenmerk. |
| `CACHE_NODE_IDS` | Als `false` , gaat het algoritme bomen tot uitvoerders over om instanties met knopen aan te passen. Als `true`, het algoritme knoop IDs voor elke instantie in cache plaatst, die de opleiding van diepere bomen versnelt. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Hiermee geeft u aan hoe vaak de in de cache opgeslagen knooppunt-id&#39;s moeten worden gecontroleerd. `10` betekent bijvoorbeeld dat de cache om de 10 herhalingen wordt gecontroleerd. | 10 | (>= 1) |
| `MAX_DEPTH` | De maximale diepte van de boom (niet-negatief). De diepte `0` betekent bijvoorbeeld 1 bladknooppunt en de diepte `1` 1 interne node en 2 bladknooppunten. | 5 | (>= 0) |
| `MIN_INFO_GAIN` | De minimuminformatietoename die voor een splitsing wordt vereist om bij een boomknoop te worden overwogen. | 0,0 | (>= 0,0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | De minimale fractie van het gewogen aantal monsters die elk kind na een splitsing moet hebben. Als een splitsing ertoe leidt dat de fractie van het totale gewicht in een van beide kinderen kleiner is dan deze waarde, wordt deze weggegooid. | 0,0 | (>= 0,0, &lt;= 0,5) |
| `MIN_INSTANCES_PER_NODE` | Het minimum aantal exemplaren dat elk kind na een splitsing moet hebben. Als een splitsing minder instanties oplevert dan deze waarde, wordt de splitsing genegeerd. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Het maximale geheugen, in MB, dat is toegewezen aan histogramaggregatie. Als deze waarde te klein is, wordt slechts één knooppunt gesplitst per iteratie en kunnen de aggregaten ervan deze grootte overschrijden. | 256 |                                                                                                      |
| `PREDICTION_COL` | De kolomnaam voor voorspellingsuitvoer. | &quot;voorspelling&quot; | Willekeurige tekenreeks |
| `VALIDATION_INDICATOR_COL` | De kolomnaam geeft aan of elke rij wordt gebruikt voor training of validatie. `false` voor training en `true` voor validatie. | NIET INGESTELD | Willekeurige tekenreeks |
| `RAW_PREDICTION_COL` | De kolomnaam voor onbewerkte voorspellingswaarden (ook wel betrouwbaarheid genoemd). | &quot;rawPrediction&quot; | Willekeurige tekenreeks |
| `LEAF_COL` | De kolomnaam voor bladindexen, de voorspelde bladindex van elke instantie in elke boom, die wordt gegenereerd door het vooraf doorlopen van de volgorde. | &quot;&quot; | Willekeurige tekenreeks |
| `FEATURE_SUBSET_STRATEGY` | Het aantal eigenschappen overwogen voor het verdelen bij elke boomknoop. Ondersteunde opties: `auto` , `all` , `onethird` , `sqrt` , `log2` en `n` (voor een fractie van functies). | &quot;auto&quot; | `auto`, `all`, `onethird`, `sqrt`, `log2`, `n` (waarbij `n` een fractie tussen 0 en 1,0 is) |
| `WEIGHT_COL` | De kolomnaam, bijvoorbeeld, gewichten. Als deze niet is ingesteld of leeg is, worden alle instantiegewichten behandeld als `1.0` . | NIET INGESTELD |                                                                                                      |
| `LOSS_TYPE` | De verliesfunctie die het [!DNL Gradient Boosted Tree] -model probeert te minimaliseren. Ondersteunde opties: `logistic`. | &quot;logistiek&quot; | `logistic` |
| `STEP_SIZE` | De stapgrootte (ook wel de leersnelheid genoemd) in het bereik `(0, 1]` die wordt gebruikt om de bijdrage van elke schatter te verlagen. | 0,1 | `(0, 1]` |
| `MAX_ITER` | Het maximumaantal herhalingen voor het algoritme. | 20 | (>= 0) |
| `SUBSAMPLING_RATE` | Het deel van de trainingsgegevens dat wordt gebruikt om elke beslissingsboom te trainen, in het bereik `(0, 1]` . | 1,0 | `(0, 1]` |
| `PROBABILITY_COL` | De kolomnaam voor voorspelde klasse voorwaardelijke kansen. Opmerking: niet alle modellen hebben een goede kalibratie van de waarschijnlijkheden; deze moeten worden behandeld als betrouwbaarheidsscores in plaats van als exacte waarschijnlijkheid. | &quot;waarschijnlijkheid&quot; | Willekeurige tekenreeks |
| `ONE_VS_REST` | Schakelt het verpakken van dit algoritme met One-vs-Rest voor classificatie van meerdere klassen in of uit. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Voorbeeld**

```sql
Create MODEL modelname OPTIONS(
  type = 'gradient_boosted_tree_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Linear Support Vector Classifier] (LinearSVC) {#linear-support-vector-classifier}

Met [!DNL Linear Support Vector Classifier] (LinearSVC) wordt een hypervlak gemaakt waarin gegevens worden ingedeeld in een hoogdimensionale ruimte. U kunt deze optie gebruiken om de marge tussen klassen te maximaliseren om classificatiefouten te minimaliseren.

**Parameters**

In de onderstaande tabel staan de belangrijkste parameters voor het configureren en optimaliseren van de prestaties van de [!DNL Linear Support Vector Classifier (LinearSVC)] .

| Parameter | Beschrijving | Standaardwaarde | Mogelijke waarden |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_ITER` | Het maximumaantal herhalingen voor het uit te voeren algoritme. | 100 | (>= 0) |
| `AGGREGATION_DEPTH` | De voorgestelde diepte voor boomaggregatie. | 2 |                                                                                                      |
| `FIT_INTERCEPT` | Of een onderscheppingsterm moet passen. | `true` | `true`, `false` |
| `TOL` | De convergentietolerantie voor optimalisering. | 1E-6 | (>= 0) |
| `MAX_BLOCK_SIZE_IN_MB` | Het maximale geheugen in MB voor het stapelen van invoergegevens in blokken. De gegevens worden gestapeld binnen verdelingen, en als de resterende gegevensgrootte in een verdeling kleiner is, wordt deze waarde dienovereenkomstig aangepast. | 0,0 | (>= 0) |
| `REG_PARAM` | De regularisatieparameter, die modelingewikkeldheid helpt te controleren en overfitting te verhinderen. | 0,0 | (>= 0) |
| `STANDARDIZATION` | Of u trainingsfuncties wilt standaardiseren voordat u het model aanpast. | `true` | `true`, `false` |
| `PREDICTION_COL` | De kolomnaam voor voorspellingsuitvoer. | &quot;voorspelling&quot; | Willekeurige tekenreeks |
| `RAW_PREDICTION_COL` | De kolomnaam voor onbewerkte voorspellingswaarden (ook wel betrouwbaarheid genoemd). | &quot;rawPrediction&quot; | Willekeurige tekenreeks |
| `ONE_VS_REST` | Schakelt het verpakken van dit algoritme met One-vs-Rest voor classificatie van meerdere klassen in of uit. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Voorbeeld**

```sql
Create MODEL modelname OPTIONS(
  type = 'linear_svc_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Logistic Regression] {#logistic-regression}

[!DNL Logistic Regression] is een onder toezicht staand algoritme dat wordt gebruikt voor binaire classificatie. Het modelleert de waarschijnlijkheid dat een instantie tot een klasse gebruikend de logistieke functie behoort, die het voor taken geschikt maakt waar het doel is instanties in één van twee categorieën te classificeren.

**Parameters**

In de onderstaande tabel staan de belangrijkste parameters voor het configureren en optimaliseren van de prestaties van [!DNL Logistic Regression] .

| Parameter | Beschrijving | Standaardwaarde | Mogelijke waarden |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|----------------|
| `MAX_ITER` | Het maximumaantal herhalingen dat het algoritme uitvoert. | 100 | (>= 0) |
| `REGPARAM` | De regularisatieparameter wordt gebruikt om de ingewikkeldheid van het model te controleren. | 0,0 | (>= 0) |
| `ELASTICNETPARAM` | De `ElasticNet` -mixparameter bepaalt de balans tussen L1 (Lasso) en L2 (Ridge) boetes. Bij de waarde 0 wordt een L2-boete toegepast (Rand, waardoor de grootte van de coëfficiënten afneemt), terwijl bij de waarde 1 een L1-boete wordt toegepast (Lasso, dat de flexibiliteit aanmoedigt door bepaalde coëfficiënten in te stellen op nul). | 0,0 | (>= 0, &lt;= 1) |

{style="table-layout:auto"}

**Voorbeeld**

```sql
Create MODEL modelname OPTIONS(
  type = 'logistic_reg'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Multilayer Perceptron Classifier] {#multilayer-perceptron-classifier}

[!DNL Multilayer Perceptron Classifier] is een kunstmatige kunstmatige zenuwnetwerkclassificator die bestaat uit meerdere volledig verbonden lagen knooppunten. Elke knoop in een laag brengt input aan output in kaart gebruikend een gewogen lineaire combinatie van de inputgegevens, met knoopgewichten (`w`) en afwijking (`b`), die door een activeringsfunctie wordt gevolgd. Dit proces helpt geavanceerde statistische modellen te configureren en te optimaliseren door belangrijke parameters aan te passen, met codevoorbeelden voor verdere begeleiding. —>

**Parameters**

| Parameter | Beschrijving | Standaardwaarde | Mogelijke waarden |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | Het maximumaantal herhalingen voor het uit te voeren algoritme. | 100 | (>= 0) |
| `BLOCK_SIZE` | De blokgrootte voor het stapelen van inputgegevens in matrixen binnen verdelingen. Als de blokgrootte de resterende gegevens in een verdeling overschrijdt, wordt het dienovereenkomstig aangepast. | 128 | (>= 0) |
| `STEP_SIZE` | De stapgrootte die voor elke herhaling van optimalisatie wordt gebruikt (alleen van toepassing op de oplosser `gd` ). | 0,03 | (> 0) |
| `TOL` | De convergentietolerantie voor optimalisering. | `1E-6` | (>= 0) |
| `PREDICTION_COL` | De kolomnaam voor voorspellingsuitvoer. | &quot;voorspelling&quot; | Willekeurige tekenreeks |
| `SEED` | Het willekeurige zaad voor het controleren van willekeurige processen in het algoritme. | NIET INGESTELD | Willekeurig 64-bits getal |
| `PROBABILITY_COL` | De kolomnaam voor voorspelde klasse voorwaardelijke kansen. Deze moeten worden behandeld als betrouwbaarheidsscores in plaats van als exacte waarschijnlijkheid. | &quot;waarschijnlijkheid&quot; | Willekeurige tekenreeks |
| `RAW_PREDICTION_COL` | De kolomnaam voor onbewerkte voorspellingswaarden (ook wel betrouwbaarheid genoemd). | &quot;rawPrediction&quot; | Willekeurige tekenreeks |
| `ONE_VS_REST` | Schakelt het verpakken van dit algoritme met One-vs-Rest voor classificatie van meerdere klassen in of uit. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Voorbeeld**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'multilayer_perceptron_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Naive Bayes Classifier] {#naive-bayes-classifier}

[!DNL Naive Bayes Classifier] is een eenvoudige probabilistische, meerklassenclassificator gebaseerd op de stelling van Bayes met sterke (naïeve) onafhankelijkheidsaannames tussen eigenschappen. Het is zeer efficiënt in opleiding, die slechts één enkele pas over de opleidingsgegevens vereisen om de voorwaardelijke kansverdeling van elke eigenschap te berekenen gegeven elk etiket. Voor voorspellingen gebruikt het de stelling van Bayes om de voorwaardelijke waarschijnlijkheidsverdeling van elk label te berekenen op basis van een waarneming.

**Parameters**

| Parameter | Beschrijving | Standaardwaarde | Mogelijke waarden |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------------|
| `MODEL_TYPE` | Hiermee geeft u het modeltype op. Ondersteunde opties zijn `"multinomial"` , `"complement"` , `"bernoulli"` en `"gaussian"` . Modeltype is hoofdlettergevoelig. | &quot;multinomial&quot; | `"multinomial"`, `"complement"`, `"bernoulli"`, `"gaussian"` |
| `SMOOTHING` | De parameter smoothing, die wordt gebruikt om categoriale gegevens vloeiend te maken en onzichtbare functies te verwerken. | 1,0 | (>= 0) |
| `PROBABILITY_COL` | De kolomnaam voor voorspelde klasse voorwaardelijke kansen. Deze moeten worden behandeld als betrouwbaarheidsscores in plaats van als exacte waarschijnlijkheid. | &quot;waarschijnlijkheid&quot; | Willekeurige tekenreeks |
| `WEIGHT_COL` | De kolomnaam voor bijvoorbeeld gewichten. Als deze niet is ingesteld of leeg is, worden alle instantiegewichten behandeld als `1.0` . | NIET INGESTELD | Willekeurige tekenreeks |
| `PREDICTION_COL` | De kolomnaam voor voorspellingsuitvoer. | &quot;voorspelling&quot; | Willekeurige tekenreeks |
| `RAW_PREDICTION_COL` | De kolomnaam voor onbewerkte voorspellingswaarden (ook wel betrouwbaarheid genoemd). | &quot;rawPrediction&quot; | Willekeurige tekenreeks |
| `ONE_VS_REST` | Geeft aan of de indeling One-vs-Rest moet worden ingeschakeld voor meerdere klassen. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Voorbeeld**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'naive_bayes_classifier'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Random Forest Classifier] {#random-forest-classifier}

[!DNL Random Forest Classifier] is een ensemble Learning-algoritme die tijdens de training meerdere beslissingsstructuren maakt. Het verzacht overdreven aanpassing door voorspellingen te gemiddelde te nemen en de klasse te kiezen die door de meerderheid van de bomen voor classificatietaken wordt gekozen.

**Parameters**

| Parameter | Beschrijving | Standaardwaarde | Mogelijke waarden |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Het maximumaantal bakken bepaalt hoe ononderbroken eigenschappen in discrete intervallen worden verdeeld. Dit beïnvloedt hoe de eigenschappen bij elke knoop van de beslissingsboom worden verdeeld. Meer bins zorgen voor een hogere granulariteit. | 32 | Moet ten minste 2 en gelijk zijn aan of groter zijn dan het aantal categorieën in een categorisch kenmerk. |
| `CACHE_NODE_IDS` | Als `false` , gaat het algoritme bomen tot uitvoerders over om instanties met knopen aan te passen. Indien `true`, plaatst het algoritme knoop IDs voor elke instantie in het voorgeheugen, die opleiding versnelt. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Hiermee geeft u aan hoe vaak de in de cache opgeslagen knooppunt-id&#39;s moeten worden gecontroleerd. `10` betekent bijvoorbeeld dat de cache om de 10 herhalingen wordt gecontroleerd. | 10 | (>= 1) |
| `IMPURITY` | Het criterium dat wordt gebruikt voor de berekening van de informatieverbreding (hoofdlettergevoelig). | &quot;gini&quot; | `entropy`, `gini` |
| `MAX_DEPTH` | De maximale diepte van de boom (niet-negatief). De diepte `0` betekent bijvoorbeeld 1 bladknooppunt en de diepte `1` 1 interne node en 2 bladknooppunten. | 5 | (>= 0) |
| `MIN_INFO_GAIN` | De minimuminformatietoename die voor een splitsing wordt vereist om bij een boomknoop te worden overwogen. | 0,0 | (>= 0,0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | De minimale fractie van het gewogen aantal monsters die elk kind na een splitsing moet hebben. Als een splitsing ertoe leidt dat de fractie van het totale gewicht in een van beide kinderen kleiner is dan deze waarde, wordt deze weggegooid. | 0,0 | (>= 0,0, &lt;= 0,5) |
| `MIN_INSTANCES_PER_NODE` | Het minimum aantal exemplaren dat elk kind na een splitsing moet hebben. Als een splitsing minder instanties oplevert dan deze waarde, wordt de splitsing genegeerd. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Het maximale geheugen, in MB, dat is toegewezen aan histogramaggregatie. Als deze waarde te klein is, wordt slechts één knooppunt gesplitst per iteratie en kunnen de aggregaten ervan deze grootte overschrijden. | 256 | (>= 1) |
| `PREDICTION_COL` | De kolomnaam voor voorspellingsuitvoer. | &quot;voorspelling&quot; | Willekeurige tekenreeks |
| `WEIGHT_COL` | De kolomnaam, bijvoorbeeld, gewichten. Als deze niet is ingesteld of leeg is, worden alle instantiegewichten behandeld als `1.0` . | NIET INGESTELD | Willekeurige tekenreeks |
| `SEED` | Het willekeurige zaadgetal dat wordt gebruikt voor de besturing van willekeurige processen in het algoritme. | -1689246527 | Willekeurig 64-bits getal |
| `BOOTSTRAP` | Of laarzentestmonsters worden gebruikt bij het bouwen van bomen. | `true` | `true`, `false` |
| `NUM_TREES` | Het aantal bomen dat moet worden getraind. Als `1` , dan wordt geen bootstrapping gebruikt. Als dit groter is dan `1`, wordt de overvulling bootstrapping toegepast. | 20 | (>= 1) |
| `SUBSAMPLING_RATE` | Het deel van de opleidingsgegevens die voor het leren van elke beslissingsboom worden gebruikt. | 1,0 | (> 0, &lt;= 1) |
| `LEAF_COL` | De kolomnaam voor de bladindexen, die de voorspelde bladindex van elke instantie in elke boom op voorvolgorde bevat. | &quot;&quot; | Willekeurige tekenreeks |
| `PROBABILITY_COL` | De kolomnaam voor voorspelde klasse voorwaardelijke kansen. Deze moeten worden behandeld als betrouwbaarheidsscores in plaats van als exacte waarschijnlijkheid. | &quot;waarschijnlijkheid&quot; | Willekeurige tekenreeks |
| `RAW_PREDICTION_COL` | De kolomnaam voor onbewerkte voorspellingswaarden (ook wel betrouwbaarheid genoemd). | &quot;rawPrediction&quot; | Willekeurige tekenreeks |
| `ONE_VS_REST` | Geeft aan of de indeling One-vs-Rest moet worden ingeschakeld voor meerdere klassen. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Voorbeeld**

```sql
Create MODEL modelname OPTIONS(
  type = 'random_forest_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## Volgende stappen

Na het lezen van dit document, weet u nu hoe te om diverse classificatiealgoritmen te vormen en te gebruiken. Daarna, verwijs naar de documenten op [ regressie ](./regression.md) en [ groeperend ](./clustering.md) om over andere soorten geavanceerde statistische modellen te leren.

