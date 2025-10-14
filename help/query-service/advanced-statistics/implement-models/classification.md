---
title: Classificatiealgoritmen
description: Leer om diverse classificatiealgoritmen met zeer belangrijke parameters, beschrijvingen, en voorbeeldcode te vormen en te optimaliseren om u te helpen geavanceerde statistische modellen uitvoeren.
role: Developer
exl-id: 9105ab04-b480-48a0-b8f7-cf0ed5e5399d
source-git-commit: 489063fcd003e20f233a9c9d85d8cb6c22708d88
workflow-type: tm+mt
source-wordcount: '2449'
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
| `MAX_DEPTH` | De maximale diepte van de boom (niet-negatief). De diepte `0` betekent bijvoorbeeld 1 bladknooppunt en de diepte `1` 1 interne node en 2 bladknooppunten. | 5 | (>= 0) (waaier: [ 0,30 ]) |
| `MIN_INFO_GAIN` | De minimuminformatietoename die voor een splitsing wordt vereist om bij een boomknoop te worden overwogen. | 0,0 | (>= 0,0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | De minimale fractie van het gewogen aantal monsters die elk kind na een splitsing moet hebben. Als een splitsing ertoe leidt dat de fractie van het totale gewicht in een van beide kinderen kleiner is dan deze waarde, wordt deze weggegooid. | 0,0 | (>= 0,0, &lt;= 0,5) |
| `MIN_INSTANCES_PER_NODE` | Het minimum aantal exemplaren dat elk kind na een splitsing moet hebben. Als een splitsing minder instanties oplevert dan deze waarde, wordt de splitsing genegeerd. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Het maximale geheugen, in MB, dat is toegewezen aan histogramaggregatie. Als deze waarde te klein is, wordt slechts één knooppunt gesplitst per iteratie en kunnen de aggregaten ervan deze grootte overschrijden. | 256 | (>= 0) |
| `PREDICTION_COL` | De kolomnaam voor voorspellingsuitvoer. | &quot;voorspelling&quot; | Willekeurige tekenreeks |
| `SEED` | Het willekeurige zaadje. | N.v.t. | Willekeurig 64-bits getal |
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
| `MINI_BATCH_FRACTION` | Het deel van de gegevens dat tijdens de training in minibatches wordt gebruikt. Moet binnen het bereik `(0, 1]` vallen. | 1,0 | 0 &lt; waarde &lt;= 1 |
| `REG_PARAM` | De regularisatieparameter, die modelingewikkeldheid helpt te controleren en overfitting te verhinderen. | 0,0 | (>= 0) |
| `SEED` | Het willekeurige zaad voor het controleren van willekeurige processen in het algoritme. | N.v.t. | Willekeurig 64-bits getal |
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
| `MAX_MEMORY_IN_MB` | Het maximale geheugen, in MB, dat is toegewezen aan histogramaggregatie. Als deze waarde te klein is, wordt slechts één knooppunt gesplitst per iteratie en kunnen de aggregaten ervan deze grootte overschrijden. | 256 | (>= 0) |
| `PREDICTION_COL` | De kolomnaam voor voorspellingsuitvoer. | &quot;voorspelling&quot; | Willekeurige tekenreeks |
| `VALIDATION_INDICATOR_COL` | De kolomnaam geeft aan of elke rij wordt gebruikt voor training of validatie. De waarde `false` geeft training aan en `true` geeft validatie aan. Wanneer geen waarde is ingesteld, is de standaardwaarde `None` . | &quot;Geen&quot; | Willekeurige tekenreeks |
| `RAW_PREDICTION_COL` | De kolomnaam voor onbewerkte voorspellingswaarden (ook wel betrouwbaarheid genoemd). | &quot;rawPrediction&quot; | Willekeurige tekenreeks |
| `LEAF_COL` | De kolomnaam voor bladindexen, de voorspelde bladindex van elke instantie in elke boom, die wordt gegenereerd door het vooraf doorlopen van de volgorde. | &quot;&quot; | Willekeurige tekenreeks |
| `FEATURE_SUBSET_STRATEGY` | Het aantal eigenschappen overwogen voor het verdelen bij elke boomknoop. Ondersteunde opties: `auto` (automatisch bepaald op basis van de taak), `all` (alle functies gebruiken), `onethird` (gebruik een derde van de functies), `sqrt` (gebruik de vierkantswortel van het aantal functies), `log2` (gebruik de natuurlijke logaritme met grondtal 2 van het aantal functies) en `n` (waarbij n een fractie van de functies is als deze binnen het bereik `(0, 1]` vallen, of een specifiek aantal functies als deze binnen het bereik `[1, total number of features]` vallen). | &quot;auto&quot; | `auto`, `all`, `onethird`, `sqrt`, `log2`, `n` |
| `WEIGHT_COL` | De kolomnaam, bijvoorbeeld, gewichten. Als deze niet is ingesteld of leeg is, worden alle instantiegewichten behandeld als `1.0` . | NIET INGESTELD | Willekeurige tekenreeks |
| `LOSS_TYPE` | De verliesfunctie die het [!DNL Gradient Boosted Tree] -model probeert te minimaliseren. | &quot;logistiek&quot; | `logistic` (hoofdlettergevoelig) |
| `STEP_SIZE` | De stapgrootte (ook wel de leersnelheid genoemd) in het bereik `(0, 1]` die wordt gebruikt om de bijdrage van elke schatter te verlagen. | 0,1 | (>= 0,0, &lt;= 1) |
| `MAX_ITER` | Het maximumaantal herhalingen voor het algoritme. | 20 | (>= 0) |
| `SUBSAMPLING_RATE` | Het deel van de trainingsgegevens dat wordt gebruikt om elke beslissingsboom op te leiden. De waarde moet binnen het bereik 0 &lt; waarde &lt;= 1 liggen. | 1,0 | `(0, 1]` |
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
| `AGGREGATION_DEPTH` | De diepte voor boomsamenvoeging. Deze parameter wordt gebruikt om netwerkcommunicatie overheadkosten te verminderen. | 2 | Een positief geheel getal |
| `FIT_INTERCEPT` | Of een onderscheppingsterm moet passen. | `true` | `true`, `false` |
| `TOL` | Deze parameter bepaalt de drempel voor het stoppen van herhalingen. | 1E-6 | (>= 0) |
| `MAX_BLOCK_SIZE_IN_MB` | Het maximale geheugen in MB voor het stapelen van invoergegevens in blokken. Wanneer de parameter op `0` is ingesteld, wordt automatisch de optimale waarde gekozen (gewoonlijk rond 1 MB). | 0,0 | (>= 0) |
| `REG_PARAM` | De regularisatieparameter, die modelingewikkeldheid helpt te controleren en overfitting te verhinderen. | 0,0 | (>= 0) |
| `STANDARDIZATION` | Deze parameter geeft aan of de trainingsfuncties moeten worden gestandaardiseerd voordat het model wordt aangepast. | `true` | `true`, `false` |
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

[!DNL Logistic Regression] is een onder toezicht staand algoritme dat wordt gebruikt voor binaire classificatietaken. De methode modelleert de waarschijnlijkheid dat een instantie tot een klasse behoort die de logistieke functie gebruikt en wijst de instantie met de hogere waarschijnlijkheid toe aan de klasse. Dit maakt het geschikt voor problemen waarbij het doel is gegevens in één van twee categorieën te scheiden.

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

De [!DNL Multilayer Perceptron Classifier] (MLPC) is een kunstmatige classificatie voor neurale netwerken. Het bestaat uit meerdere volledig verbonden lagen knooppunten, waarbij elk knooppunt een gewogen lineaire combinatie van ingangen toepast, gevolgd door een activeringsfunctie. MLPC wordt gebruikt voor complexe classificatietaken die niet-lineaire beslissingsgrenzen vereisen.

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

[!DNL Naive Bayes Classifier] is een eenvoudige probabilistische, meerklassenclassificator gebaseerd op de stelling van Bayes met sterke (naïeve) onafhankelijkheidsaannames tussen eigenschappen. Het treinpersoneel traint efficiënt door voorwaardelijke waarschijnlijkheden in één keer te berekenen over de trainingsgegevens om de voorwaardelijke kansverdeling van elk onderdeel op elk label te berekenen. Voor voorspellingen gebruikt het de stelling van Bayes om de voorwaardelijke waarschijnlijkheidsverdeling van elk label te berekenen op basis van een waarneming.

**Parameters**

| Parameter | Beschrijving | Standaardwaarde | Mogelijke waarden |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------------|
| `MODEL_TYPE` | Hiermee geeft u het modeltype op. Ondersteunde opties zijn `"multinomial"` , `"complement"` , `"bernoulli"` en `"gaussian"` . Modeltype is hoofdlettergevoelig. | &quot;multinomial&quot; | `"multinomial"`, `"complement"`, `"bernoulli"`, `"gaussian"` |
| `SMOOTHING` | De parameter smoothing wordt gebruikt om nul-frequentieproblemen in categoriale gegevens te behandelen. | 1,0 | (>= 0) |
| `PROBABILITY_COL` | Deze parameter specificeert de kolomnaam voor voorspelde klasse voorwaardelijke waarschijnlijkheden. Opmerking: niet alle modellen bieden goed gekalibreerde waarschijnlijkheidsschattingen; behandelen deze waarden als betrouwbaarheidswaarden in plaats van als exacte waarschijnlijkheden. | &quot;waarschijnlijkheid&quot; | Willekeurige tekenreeks |
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
| `WEIGHT_COL` | De kolomnaam, bijvoorbeeld, gewichten. Als deze niet is ingesteld of leeg is, worden alle instantiegewichten behandeld als `1.0` . | NIET INGESTELD | Elke geldige kolomnaam of leeg |
| `SEED` | Het willekeurige zaadgetal dat wordt gebruikt voor de besturing van willekeurige processen in het algoritme. | -1689246527 | Willekeurig 64-bits getal |
| `BOOTSTRAP` | Of laarzentestmonsters worden gebruikt bij het bouwen van bomen. | `true` | `true`, `false` |
| `NUM_TREES` | Het aantal bomen dat moet worden getraind. Als `1` , dan wordt geen bootstrapping gebruikt. Als dit groter is dan `1`, wordt de overvulling bootstrapping toegepast. | 20 | (>= 1) |
| `SUBSAMPLING_RATE` | Het deel van de opleidingsgegevens die voor het leren van elke beslissingsboom worden gebruikt. | 1,0 | (> 0, &lt;= 1) |
| `LEAF_COL` | De kolomnaam voor de bladindexen, die de voorspelde bladindex van elke instantie in elke boom op voorvolgorde bevat. | &quot;&quot; | Willekeurige tekenreeks |
| `PROBABILITY_COL` | De kolomnaam voor voorspelde klasse voorwaardelijke kansen. Deze moeten worden behandeld als betrouwbaarheidsscores in plaats van als exacte waarschijnlijkheid. | NIET INGESTELD | Willekeurige tekenreeks |
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

Na het lezen van dit document, weet u nu hoe te om diverse classificatiealgoritmen te vormen en te gebruiken. Daarna, verwijs naar de documenten op [&#x200B; regressie &#x200B;](./regression.md) en [&#x200B; groeperend &#x200B;](./clustering.md) om over andere soorten geavanceerde statistische modellen te leren.
