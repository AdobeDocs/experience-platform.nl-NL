---
keywords: Experience Platform;optimaliseren;model;Data Science Workspace;populaire onderwerpen;modelinzichten
solution: Experience Platform
title: Een model optimaliseren met behulp van het Model Insights Framework
type: Tutorial
description: Het Model Insights Framework biedt de gegevenswetenschapper hulpmiddelen in Data Science Workspace om snelle en geïnformeerde keuzes te maken voor optimale modellen voor machinaal leren op basis van experimenten.
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1210'
ht-degree: 0%

---

# Een model optimaliseren met behulp van het Model Insights-framework

>[!NOTE]
>
>Data Science Workspace kan niet meer worden aangeschaft.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

Het Model Insights Framework biedt de gegevenswetenschapper in [!DNL Data Science Workspace] gereedschappen om snelle en geïnformeerde keuzes te maken voor optimale modellen voor machinaal leren op basis van experimenten. Het kader zal de snelheid en doeltreffendheid van de werkstroom voor machinaal leren verbeteren en het gebruiksgemak voor gegevenswetenschappers verbeteren. Dit wordt gedaan door een standaardmalplaatje voor elk machine het leren algoritme type te verstrekken om met model het stemmen bij te wonen. Dankzij het eindresultaat kunnen wetenschappers op het gebied van gegevens en burgergegevens betere modeloptimalisatiebeslissingen maken voor hun eindgebruikers.

## Wat zijn metriek?

Na het implementeren en trainen van een model, zou een wetenschapper de volgende stap zetten om te zien hoe goed het model zal presteren. Diverse metriek worden gebruikt om te vinden hoe efficiënt een model in vergelijking met anderen zal zijn. Voorbeelden van gebruikte metriek zijn:
- Classificatienauwkeurigheid
- Oppervlak onder curve
- Verfusiematrix
- Classificatierapport

## Recept-code configureren

Momenteel ondersteunt het Model Insights Framework de volgende runtimes:
- [Scala](#scala)
- [Python/Tensorflow](#pythontensorflow)
- [R](#r)

De code van de steekproef voor recepten kan in de [&#x200B; ervaring-platform-dsw-verwijzing &#x200B;](https://github.com/adobe/experience-platform-dsw-reference) bewaarplaats onder `recipes` worden gevonden. In deze zelfstudie wordt naar specifieke bestanden in deze opslagplaats verwezen.

### Scala {#scala}

Er zijn twee manieren om metrics aan de recepten toe te voegen. De ene is de standaardevaluatiemetriek te gebruiken die door de SDK wordt verstrekt en de andere is aangepaste evaluatiemetrieken te schrijven.

#### Standaardevaluatiemetrieken voor Scala

Standaardevaluaties worden berekend als onderdeel van de classificatiealgoritmen. Hier volgen enkele standaardwaarden voor beoordelaars die momenteel zijn geïmplementeerd:

| Evaluatorklasse | `evaluation.class` |
|--- | ---|
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

De evaluator kan worden gedefinieerd in het recept in het [bestand application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) in de `recipe` map. Voorbeeldcode die het inschakelen van de functie voor het inschakelen van de `DefaultBinaryClassificationEvaluator` functie wordt hieronder weergegeven:

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

Nadat een evaluatieklasse is ingeschakeld, worden standaard tijdens de training een aantal metrische gegevens berekend. Standaardgegevens kunnen expliciet worden gedeclareerd door de volgende regel toe te voegen aan uw `application.properties`.

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>Als de metriek niet is gedefinieerd, zijn de standaard metrische gegevens actief.

U kunt een specifieke metrische waarde inschakelen door de waarde voor `evaluation.metrics.com` te wijzigen. In het volgende voorbeeld, wordt metrisch F-Score toegelaten.

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

In de volgende tabel worden de standaardmetriek voor elke klasse weergegeven. Een gebruiker kan ook de waarden in de kolom `evaluation.metric` gebruiken om een specifieke metrische waarde in te schakelen.

| `evaluator.class` | Standaardwaarden | `evaluation.metric` |
| --- | --- | --- |
| `DefaultBinaryClassificationEvaluator` | -Precision <br> -Recall <br> -Confusion Matrix <br> -F-Score <br> -Accuracy <br> -Receiver Operating Characters <br> -Area under the Receiver Operating Characters | -`PRECISION` <br> -`RECALL` <br> - `CONFUSION_MATRIX` <br> - `FSCORE` <br> - `ACCURACY` <br> - `ROC` <br> - `AUROC` |
| `DefaultMultiClassificationEvaluator` | -Precision <br> -Recall <br> -Confusion Matrix <br> -F-Score <br> -Accuracy <br> -Receiver-besturingskenmerken <br> -area under the Receiver-besturingskenmerken | -`PRECISION` <br> -`RECALL` <br> -`CONFUSION_MATRIX` <br> -`FSCORE` <br> -`ACCURACY` <br> -`ROC` <br> -`AUROC` |
| `RecommendationsEvaluator` | -Gemiddelde gemiddelde precisie (MAP) <br> - Gegormaliseerde gekwantificeerde cumulatieve winst <br> - Gemiddelde kringloop <br> - Metrisch K | -`MEAN_AVERAGE_PRECISION` <br> -`NDCG` <br> - `MRR` <br> -`METRIC_K` |


#### Eigen evaluatiemetrics voor Scala

U kunt de aangepaste evaluatiefunctie gebruiken door de interface van `MLEvaluator.scala` in uw `Evaluator.scala` bestand uit te breiden. In het voorbeeldbestand [Evaluator.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) definiëren we aangepaste `split()` en `evaluate()` functies. Onze `split()` functie splitst onze gegevens willekeurig met een verhouding van 8:2 en onze `evaluate()` functie definieert en retourneert 3 metrische gegevens: MAPE, MINIATURE, en RMSE.

>[!IMPORTANT]
>
>Gebruik voor de `MLMetric` klasse niet `"measures"` `valueType` als u een nieuwe `MLMetric` , andere metrische waarde maakt, wordt de metrische waarde niet weergegeven in de tabel met aangepaste evaluatiegegevens.
>  
> Ga als volgt te werk: `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> Niet dit: `metrics.add(new MLMetric("MAPE", mape, "measures"))`


Eenmaal gedefinieerd in het recept, bestaat de volgende stap uit het inschakelen in de recepten. Dit wordt gedaan in het {[&#128279;](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) dossier 0} application.properties in de omslag van het project `resources`.  Hier wordt de `evaluation.class` ingesteld op de `Evaluator` -klasse die is gedefinieerd in `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

In [!DNL Data Science Workspace] zou de gebruiker de inzichten op het tabblad &quot;Evaluatiemetriek&quot; in de testpagina kunnen zien.

### [!DNL Python/Tensorflow] {#pythontensorflow}

Op dit moment zijn er geen standaardevaluatiemetriek voor [!DNL Python] of [!DNL Tensorflow] . Als u dus de evaluatiemetriek voor [!DNL Python] of [!DNL Tensorflow] wilt ophalen, moet u een maateenheid voor aangepaste evaluatie maken. Dit kan worden gedaan door de `Evaluator` -klasse te implementeren.

#### Eigen evaluatiemetriek voor [!DNL Python]

Voor aangepaste evaluatiemetrieken zijn er twee hoofdmethoden die voor de evaluator moeten worden geïmplementeerd: `split()` en `evaluate()` .

Voor [!DNL Python], zouden deze methodes in [&#x200B; evaluator.py &#x200B;](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) voor de `Evaluator` klasse worden bepaald. Volg de {[&#128279;](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) verbinding 0} beoordelator.py voor een voorbeeld van `Evaluator`.

Voor het maken van evaluatiemetriek in [!DNL Python] moet de gebruiker de methoden `evaluate()` en `split()` implementeren.

De methode `evaluate()` retourneert het metrische object dat een array van metrische objecten met de eigenschappen `name` , `value` en `valueType` bevat.

Het doel van de methode `split()` is gegevens in te voeren en een training en een testdataset uit te voeren. In ons voorbeeld voert de methode `split()` gegevens in met behulp van de `DataSetReader` SDK en wist vervolgens de gegevens door de niet-verwante kolommen te verwijderen. Hierna worden extra functies gemaakt op basis van bestaande onbewerkte functies in de gegevens.

De `split()` -methode moet een training- en testgegevensframe retourneren dat vervolgens door de `pipeline()` -methoden wordt gebruikt om het XML-model op te leiden en te testen.

#### Eigen evaluatiemetriek voor Tensorflow

Voor [!DNL Tensorflow], vergelijkbaar met [!DNL Python] , moeten de methoden `evaluate()` en `split()` in de klasse `Evaluator` worden geïmplementeerd. Voor `evaluate()` moeten de metriek worden geretourneerd terwijl `split()` de trein en de testgegevenssets retourneert.

```PYTHON
from ml.runtime.python.Interfaces.AbstractEvaluator import AbstractEvaluator

class Evaluator(AbstractEvaluator):
    def __init__(self):
       print ("initiate")

    def evaluate(self, data=[], model={}, config={}):

        return metrics

    def split(self, config={}):

       return 'train', 'test'
```

### R {#r}

Vanaf nu, zijn er geen standaardevaluatiemetriek voor R. Als u dus de evaluatiemetriek voor R wilt ophalen, moet u de klasse `applicationEvaluator` definiëren als onderdeel van het recept.

#### Eigen evaluatiemetriek voor R

Het belangrijkste doel van `applicationEvaluator` is een JSON-object te retourneren dat sleutelwaardeparen metriek bevat.

Dit [&#x200B; applicationEvaluator.R &#x200B;](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) kan als voorbeeld worden gebruikt. In dit voorbeeld wordt `applicationEvaluator` gesplitst in drie vertrouwde secties:
- Gegevens laden
- Gegevensvoorbereiding/functietechniek
- Opgeslagen model ophalen en evalueren

De gegevens worden eerst in een gegevensset geladen vanuit een bron zoals gedefinieerd in [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json). Van daaruit worden de gegevens opgeschoond en ontwikkeld om te voldoen aan het machine learning-model. Ten slotte wordt het model gebruikt om een voorspelling te doen aan de hand van onze dataset. In dit geval worden MAPE, PNG en RMSE gedefinieerd en in het `metrics` object geretourneerd.

## Vooraf gebouwde metrische en visualisatiegrafieken gebruiken

De [!DNL Sensei Model Insights Framework] ondersteunt één standaardsjabloon voor elk type machine learning-algoritme. In de onderstaande tabel vindt u veelvoorkomende algoritmeklassen op hoog niveau voor machine learning en bijbehorende evaluatiemetrieken en -visualisaties.

| ML Algorithm Type | Beoordelingscijfers | Visualisaties |
| --- | --- | --- |
| Regressie | - RMSE<br> - MAPE <br> - MASE <br> - MAE | Voorspelde versus werkelijke bedekkingscurve voor waarden |
| Binaire indeling | - de matrijs van de verwarring <br> - precisie-herinner <br> - Nauwkeurigheid <br> - F-score (specifiek F1, F2) <br> - AUC <br> - ROC | ROC-curve en verwarringsmatrix |
| Classificatie met meerdere klassen | -Verwarring matrix <br>- voor elke klasse: <br>- precisie-recall nauwkeurigheid <br>- F-score (met name F1, F2) | ROC-curve en verwarringsmatrix |
| Clustering (w/grondwaarheid) | - NMI (score genormaliseerde wederzijdse informatie), AMI (aangepaste score voor wederzijdse informatie)<br>- RI (Rand-index), ARI (aangepaste Rand-index)<br>- homogeniteitsscore, volledigheidsscore en V-maat<br>- FMI (Fowlkes-Mallows index)<br>- Purity<br>- Jaccard index | Clustersplot dat clusters en clusters met clusters en clusters met relatieve clustergrootten die gegevenspunten weerspiegelen die binnen het cluster vallen, weergeven |
| Clustering (met grond waarheid) | - Inertia <br> - Silhouette coëfficiënt <br> - CHI (Calinski-Harabaz index) <br> - DBI (Davies-Bouldin index) <br> - Dunn index | Clusters worden in een grafiek geplaatst met clusters en centroïden met relatieve clustergrootten die de gegevenspunten weergeven die binnen een cluster vallen |
| Aanbeveling | -Gemiddelde gemiddelde precisie (MAP) <br> - Gegormaliseerde gekwantificeerde cumulatieve winst <br> - Gemiddelde kringloop <br> - Metrisch K | TBD |
| Gebruiksgevallen van TensorFlow | TensorFlow Model Analysis (TFMA) | Vergelijken van neurale netwerkmodellen/visualisatie |
| Ander/fout-vastlegmechanisme | Aangepaste metrische logica (en bijbehorende evaluatieteksten) gedefinieerd door de auteur van het model. Handige foutafhandeling bij niet-overeenkomende sjablonen | Tabel met sleutel-waardeparen voor evaluatiestatistieken |
