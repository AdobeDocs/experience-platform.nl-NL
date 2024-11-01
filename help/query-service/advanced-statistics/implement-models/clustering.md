---
title: Algoritmen groeperen
description: Leer hoe te om diverse het groeperen algoritmen met zeer belangrijke parameters, beschrijvingen, en voorbeeldcode te vormen en te optimaliseren om u te helpen geavanceerde statistische modellen uitvoeren.
role: Developer
source-git-commit: 4d4e9ae527deb149f02edb39716851e995c23d21
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 2%

---

# Algoritmen groeperen {#clustering-algorithms}

Algoritmen groeperen gegevenspunten in verschillende clusters op basis van hun gelijkenissen, waardoor ongecontroleerde leerprocessen patronen binnen de gegevens kunnen detecteren. Als u een clusteringalgoritme wilt maken, gebruikt u de parameter `type` in de `OPTIONS` -component om het algoritme op te geven dat u wilt gebruiken voor modeltraining. Vervolgens definieert u de relevante parameters als sleutel-waardeparen om het model te verfijnen.

>[!NOTE]
>
>Zorg ervoor dat u de parametervereisten voor het gekozen algoritme begrijpt. Sommige parameters kunnen positioneel zijn en vereisen dat alle voorafgaande parameters worden opgegeven als er aangepaste waarden zijn opgegeven. Als u ervoor kiest om bepaalde parameters niet aan te passen, past het systeem standaardinstellingen toe. Raadpleeg de relevante documentatie voor een beter begrip van de functie en standaardwaarden van elke parameter.

## [!DNL K-Means] {#kmeans}

`K-Means` is een groeperend algoritme dat gegevenspunten in een vooraf bepaald aantal clusters (k) verdeelt. Het is een van de meest gebruikte algoritmes voor clustering vanwege de eenvoud en efficiëntie ervan.

**Parameters**

Wanneer u `K-Means` gebruikt, kunnen de volgende parameters worden ingesteld in de `OPTIONS` -component:

| Parameter | Beschrijving | Standaardwaarde | Mogelijke waarden |
|---------------------|---------------------------------------------------------------------------------------------------------------|-----------------|----------------------------------|
| `MAX_ITERATIONS` | Het aantal herhalingen dat het algoritme moet uitvoeren. | `20` | (>= 0) |
| `TOL` | Het convergentietolerantieniveau. | `0.0001` | (>= 0) |
| `NUM_CLUSTERS` | Het aantal clusters dat moet worden gemaakt (`k`). | `2` | (>1) |
| `DISTANCE_TYPE` | Het algoritme dat wordt gebruikt om de afstand tussen twee punten te berekenen. | `euclidean` | `euclidean`, `cosine` |
| `KMEANS_INIT_METHOD` | Het initialisatiealgoritme voor de clustercentra. | `k-means` | `random`, `k-means` |
| `INIT_STEPS` | Het aantal stappen voor de initialisatiemodus `k-means` . | `2` | (>0) |
| `PREDICTION_COL` | De naam van de kolom waar de voorspellingen zullen worden opgeslagen. | `prediction` | Willekeurige tekenreeks |
| `SEED` | Een willekeurig zaad voor reproduceerbaarheid. | `-1689246527` | Willekeurig 64-bits getal |
| `WEIGHT_COL` | De naam van de kolom die wordt gebruikt voor bijvoorbeeld gewichten. Indien niet ingesteld, worden alle instanties even gewogen. | `not set` | N.v.t. |

{style="table-layout:auto"}

**Voorbeeld**

```sql
CREATE MODEL modelname 
OPTIONS(
  type = 'kmeans',
  MAX_ITERATIONS = 30,
  NUM_CLUSTERS = 4
) 
AS SELECT col1, col2, col3 FROM training-dataset;
```

## [!DNL Bisecting K-means] {#bisecting-kmeans}

[!DNL Bisecting K-means] is een hiërarchisch groeperend algoritme dat een verdeelde (of &quot;top-down&quot;) benadering gebruikt. Alle waarnemingen beginnen in één cluster en splitsingen worden recursief uitgevoerd terwijl de hiërarchie wordt opgebouwd. [!DNL Bisecting K-means] kan vaak sneller zijn dan normale K-middelen, maar het veroorzaakt typisch verschillende clusterresultaten.

**Parameters**

| Parameter | Beschrijving | Standaardwaarde | Mogelijke waarden |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------------|
| `MAX_ITER` | Het maximumaantal herhalingen dat het algoritme uitvoert. | 20 | (>= 0) |
| `WEIGHT_COL` | De kolomnaam voor bijvoorbeeld gewichten. Als deze niet is ingesteld of leeg is, worden alle instantiegewichten behandeld als `1.0` . | NIET INGESTELD | Willekeurige tekenreeks |
| `NUM_CLUSTERS` | Het gewenste aantal bladclusters. Het werkelijke aantal kan kleiner zijn als er geen verdeelbare clusters overblijven. | 4 | (> 1) |
| `SEED` | Het willekeurige zaadgetal dat wordt gebruikt voor de besturing van willekeurige processen in het algoritme. | NIET INGESTELD | Willekeurig 64-bits getal |
| `DISTANCE_MEASURE` | De afstandsmaat die wordt gebruikt om gelijkenis tussen punten te berekenen. | &quot;euclidean&quot; | `euclidean`, `cosine` |
| `MIN_DIVISIBLE_CLUSTER_SIZE` | Het minimumaantal punten (indien >= 1,0) of het minimumpercentage punten (indien &lt; 1,0) dat vereist is om een cluster te verdelen. | 1,0 | (>= 0) |
| `PREDICTION_COL` | De kolomnaam voor voorspellingsuitvoer. | &quot;voorspelling&quot; | Willekeurige tekenreeks |

{style="table-layout:auto"}

**Voorbeeld**

```sql
Create MODEL modelname OPTIONS(
  type = 'bisecting_kmeans',
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Gaussian Mixture Model] {#gaussian-mixture-model}

[!DNL Gaussian Mixture Model] staat voor een samengestelde distributie waarbij gegevenspunten worden getekend op basis van een van de Gaussiaanse subdistributies in k, elk met een eigen waarschijnlijkheid. Het wordt gebruikt om gegevenssets te modelleren die verondersteld worden te worden geproduceerd van een mengsel van verscheidene Gaussiaanse distributies.

**Parameters**

| Parameter | Beschrijving | Standaardwaarde | Mogelijke waarden |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | Het maximumaantal herhalingen voor het uit te voeren algoritme. | 100 | (>= 0) |
| `WEIGHT_COL` | De kolomnaam, bijvoorbeeld, gewichten. Als deze niet is ingesteld of leeg is, worden alle instantiegewichten behandeld als `1.0` . | NIET INGESTELD | Willekeurige tekenreeks |
| `NUM_CLUSTERS` | Het aantal onafhankelijke Gaussiaanse distributies in het mengselmodel. | 2 | (> 1) |
| `SEED` | Het willekeurige zaad dat wordt gebruikt om willekeurige processen in het algoritme te controleren. | NIET INGESTELD | Willekeurig 64-bits getal |
| `AGGREGATION_DEPTH` | De diepte die voor samenvoeging tijdens berekening wordt gebruikt. | 2 | (>= 1) |
| `PROBABILITY_COL` | De kolomnaam voor voorspelde klasse voorwaardelijke kansen. Deze moeten worden behandeld als betrouwbaarheidsscores in plaats van als exacte waarschijnlijkheid. | &quot;waarschijnlijkheid&quot; | Willekeurige tekenreeks |
| `TOL` | De convergentietolerantie voor herhalende algoritmen. | 0,01 | (>= 0) |
| `PREDICTION_COL` | De kolomnaam voor voorspellingsuitvoer. | &quot;voorspelling&quot; | Willekeurige tekenreeks |

{style="table-layout:auto"}

**Voorbeeld**

```sql
Create MODEL modelname OPTIONS(
  type = 'gaussian_mixture',
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Latent Dirichlet Allocation] (LDA) {#latent-dirichlet-allocation}

[!DNL Latent Dirichlet Allocation] (LDA) is een probabilistisch model dat de onderliggende onderwerpstructuur van een inzameling van documenten vangt. Het is een hiërarchisch Bayesiaans model met drie niveaus met woord, onderwerp, en documentlagen. LDA gebruikt deze lagen, samen met de waargenomen documenten, om een latente onderwerpstructuur te bouwen.

**Parameters**

| Parameter | Beschrijving | Standaardwaarde | Mogelijke waarden |                                                                                                                                                                  | Standaardwaarde | Mogelijke waarden |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | Het maximumaantal herhalingen dat het algoritme uitvoert. | 20 | (>= 0) |
| `OPTIMIZER` | De optimalisator of het afleidingsalgoritme die wordt gebruikt om het LDA-model te schatten. Ondersteunde opties zijn `"online"` (Online Variationele Bayes) en `"em"` (Verwachting-Maximalisatie). | &quot;online&quot; | `online`, `em` |
| `NUM_CLUSTERS` | Het aantal clusters dat moet worden gemaakt (k). | 10 | (> 1) |
| `CHECKPOINT_INTERVAL` | Hiermee geeft u aan hoe vaak de in de cache opgeslagen knooppunt-id&#39;s moeten worden gecontroleerd. | 10 | (>= 1) |
| `DOC_CONCENTRATION` | De parameter van de concentratie (&quot;alpha&quot;) voor de vroegere geplaatste op de distributie van documenten over onderwerpen. Hiermee regelt u de regularisatie (vloeiend maken). | Automatisch | Eén waarde of vector met lengte k |
| `KEEP_LAST_CHECKPOINT` | Geeft aan of het laatste controlepunt moet worden behouden wanneer de functie `em` optimizer wordt gebruikt. | `true` | `true`, `false` |
| `LEARNING_DECAY` | De leersnelheid voor de `online` optimizer, die als exponentiële dalingssnelheid tussen `(0.5, 1.0]` wordt geplaatst. | 0,51 | `(0.5, 1.0]` |
| `LEARNING_OFFSET` | Een leerparameter voor de `online` optimalisator die vroege herhalingen vermindert om vroege herhalingen minder te maken. | 1024 | (> 0) |
| `SEED` | Willekeurig zaad voor het controleren van willekeurige processen in het algoritme. | NIET INGESTELD | Willekeurig 64-bits getal |
| `OPTIMIZE_DOC_CONCENTRATION` | Voor `online` optimizer: of de parameter `docConcentration` (Dirichlet-parameter voor document-onderwerp-distributie) tijdens de training moet worden geoptimaliseerd. | `false` | `true`, `false` |
| `SUBSAMPLING_RATE` | Voor de `online` optimizer: de fractie van de corpus die wordt gesampled en gebruikt in elke iteratie van een mini-batch-verloop, in het bereik `(0, 1]` . | 0,05 | `(0, 1]` |
| `TOPIC_CONCENTRATION` | De parameter van de concentratie (&quot;bèta&quot; of &quot;eta&quot;) voor de vroegere geplaatste op de distributie van onderwerpen over termijnen. | Automatisch | (>= 0) |
| `TOPIC_DISTRIBUTION_COL` | Uitvoerkolom met schattingen van de distributie van de onderwerpmenmengeling voor elk document. | NIET INGESTELD | Willekeurige tekenreeks |

**Voorbeeld**

```sql
Create MODEL modelname OPTIONS(
  type = 'lda',
) AS
  select col1, col2, col3 from training-dataset
```

## Volgende stappen

Na het lezen van dit document, weet u nu hoe te om diverse het groeperen algoritmen te vormen en te gebruiken. Daarna, verwijs naar de documenten op [ classificatie ](./classification.md) en [ regressie ](./regression.md) om over andere soorten geavanceerde statistische modellen te leren.
