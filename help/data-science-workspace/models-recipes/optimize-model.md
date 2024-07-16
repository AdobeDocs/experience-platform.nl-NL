---
keywords: Experience Platform;optimaliseren;model;Data Science Workspace;populaire onderwerpen;modelinzichten
solution: Experience Platform
title: Een model optimaliseren met behulp van het Model Insights Framework
type: Tutorial
description: Het Model Insights Framework biedt de gegevenswetenschapper hulpmiddelen in Data Science Workspace om snelle en geïnformeerde keuzes te maken voor optimale modellen voor machinaal leren op basis van experimenten.
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 0%

---

# Een model optimaliseren met behulp van het Model Insights-framework

Het Model Insights Framework biedt de gegevenswetenschapper in [!DNL Data Science Workspace] gereedschappen om snelle en geïnformeerde keuzes te maken voor optimale modellen voor machinaal leren op basis van experimenten. Het kader zal de snelheid en doeltreffendheid van de werkstroom voor machinaal leren verbeteren en het gebruiksgemak voor gegevenswetenschappers verbeteren. Dit wordt gedaan door een standaardmalplaatje voor elk machine het leren algoritme type te verstrekken om met model het stemmen bij te wonen. Dankzij het eindresultaat kunnen wetenschappers op het gebied van gegevens en burgergegevens betere modeloptimalisatiebeslissingen maken voor hun eindgebruikers.

## Wat zijn metriek?

Na het implementeren en trainen van een model, zou een wetenschapper de volgende stap zetten om te zien hoe goed het model zal presteren. Diverse metriek worden gebruikt om te vinden hoe efficiënt een model in vergelijking met anderen zal zijn. Voorbeelden van gebruikte metriek zijn:
- Classificatienauwkeurigheid
- Oppervlak onder curve
- Verfusiematrix
- Classificatieverslag

## Code voor recept configureren

Momenteel ondersteunt het Model Insights Framework de volgende runtimes:
- [Scala](#scala)
- [Python/Tensorflow](#pythontensorflow)
- [R](#r)

De code van de steekproef voor recepten kan in [ ervaring-platform-dsw-verwijzing ](https://github.com/adobe/experience-platform-dsw-reference) bewaarplaats onder `recipes` worden gevonden. In deze zelfstudie wordt verwezen naar specifieke bestanden in deze opslagplaats.

### Scala {#scala}

Er zijn twee manieren om metriek in de recepten te brengen. Één moet de standaardevaluatiemetriek gebruiken die door SDK wordt verstrekt en andere moet de metriek van de douaneevaluatie schrijven.

#### Standaardevaluatiemetriek voor Scala

Standaardevaluaties worden berekend als onderdeel van de classificatiealgoritmen. Hier volgen enkele standaardwaarden voor beoordelaars die momenteel worden geïmplementeerd:

| Evaluatorklasse | `evaluation.class` |
|--- | ---|
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

De beoordelaar kan in het recept in het {](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) dossier 0} application.properties in de `recipe` omslag worden bepaald. [ De voorbeeldcode voor het inschakelen van `DefaultBinaryClassificationEvaluator` wordt hieronder weergegeven:

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

Nadat een evaluatorklasse wordt toegelaten, zal een aantal metriek tijdens opleiding door gebrek worden berekend. Standaardmetriek kan expliciet worden gedeclareerd door de volgende regel aan de `application.properties` toe te voegen.

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>Als metrisch niet wordt bepaald, zullen de standaardmetriek actief zijn.

U kunt een specifieke metrische waarde inschakelen door de waarde voor `evaluation.metrics.com` te wijzigen. In het volgende voorbeeld, wordt metrisch F-Score toegelaten.

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

In de volgende tabel worden de standaardmetriek voor elke klasse weergegeven. Een gebruiker kan ook de waarden in de kolom `evaluation.metric` gebruiken om een specifieke metrische waarde in te schakelen.

| `evaluator.class` | Standaardwaarden | `evaluation.metric` |
| --- | --- | --- |
| `DefaultBinaryClassificationEvaluator` | -Precision <br> -Recall <br> -Confusion Matrix <br> -F-Score <br> -Accuracy <br> -Receiver Operating Characters <br> -Area under the Receiver Operating Characters | -`PRECISION` <br> -`RECALL` <br> - `CONFUSION_MATRIX` <br> - `FSCORE` <br> - `ACCURACY` <br> - `ROC` <br> - `AUROC` |
| `DefaultMultiClassificationEvaluator` | -Precision <br> -Recall <br> -Confusion Matrix <br> -F-Score <br> -Accuracy <br> -Receiver Operating Characters <br> -Area under the Receiver Operating Characters | -`PRECISION` <br> -`RECALL` <br> - `CONFUSION_MATRIX` <br> - `FSCORE` <br> - `ACCURACY` <br> - `ROC` <br> - `AUROC` |
| `RecommendationsEvaluator` | -Gemiddelde gemiddelde precisie (MAP) <br> - Genormaliseerde gekwantificeerde cumulatieve winst <br> - Gemiddelde wederkerige schijf <br> - Metrische K | -`MEAN_AVERAGE_PRECISION` <br> - `NDCG` <br> - `MRR` <br> - `METRIC_K` |


#### Eigen evaluatiemetriek voor Scala

De aangepaste beoordelaar kan worden opgegeven door de interface van `MLEvaluator.scala` in het `Evaluator.scala` -bestand uit te breiden. In het 1} dossier van voorbeeld [ Evaluator.scala, bepalen wij douane `split()` en `evaluate()` functies. ](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) Onze functie `split()` splitst onze gegevens op willekeurige wijze met een verhouding van 8:2 en onze functie `evaluate()` definieert en retourneert 3 metriek: MAPE, MAE en RMSE.

>[!IMPORTANT]
>
>Gebruik voor de klasse `MLMetric` niet `"measures"` for `valueType` wanneer u een nieuwe `MLMetric` -klasse maakt. Anders wordt de metrische waarde niet in de tabel met maateenheden voor aangepaste evaluaties ingevuld.
>  
> Doe dit: `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> Niet dit: `metrics.add(new MLMetric("MAPE", mape, "measures"))`


Wanneer het in het recept is gedefinieerd, is de volgende stap het in de recepten toelaten. Dit wordt gedaan in het {](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) dossier 0} application.properties in de omslag van het project `resources`. [ Hier wordt de `evaluation.class` ingesteld op de `Evaluator` -klasse die is gedefinieerd in `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

In [!DNL Data Science Workspace] zou de gebruiker de inzichten op het tabblad &quot;Evaluatiemetriek&quot; in de testpagina kunnen zien.

### [!DNL Python/Tensorflow] {#pythontensorflow}

Op dit moment zijn er geen standaardevaluatiemetriek voor [!DNL Python] of [!DNL Tensorflow] . Als u dus de evaluatiemetriek voor [!DNL Python] of [!DNL Tensorflow] wilt ophalen, moet u een maateenheid voor aangepaste evaluatie maken. Dit kan worden gedaan door de `Evaluator` -klasse te implementeren.

#### Eigen evaluatiemetriek voor [!DNL Python]

Voor maatstaven voor aangepaste evaluatie zijn er twee hoofdmethoden die moeten worden geïmplementeerd voor de evaluator: `split()` en `evaluate()` .

Voor [!DNL Python], zouden deze methodes in [ evaluator.py ](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) voor de `Evaluator` klasse worden bepaald. Volg de {](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) verbinding 0} evaluator.py voor een voorbeeld van `Evaluator`.[

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

Dit [ applicationEvaluator.R ](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) kan als voorbeeld worden gebruikt. In dit voorbeeld wordt `applicationEvaluator` gesplitst in drie vertrouwde secties:
- Gegevens laden
- Gegevensvoorbereiding/functietechniek
- Opgeslagen model ophalen en evalueren

Het gegeven wordt eerst geladen aan een dataset van een bron zoals die in [ wordt bepaald retail.config.json ](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json). Vanaf dat moment worden de gegevens gereinigd en zo ontworpen dat ze passen in het model voor machinaal leren. Tot slot wordt het model gebruikt om een voorspelling te maken die onze dataset gebruikt en van de voorspelde waarden en daadwerkelijke waarden, worden de metriek berekend. In dit geval worden MAPE, MAE en RMSE gedefinieerd en geretourneerd in het `metrics` -object.

## Vooraf gebouwde metriek- en visualisatiekaarten gebruiken

[!DNL Sensei Model Insights Framework] zal één standaardmalplaatje voor elk type van machine het leren algoritme steunen. In de onderstaande tabel ziet u veelvoorkomende machineleesalgoritme-klassen en de bijbehorende evaluatiemetriek en -visualisaties.

| ML Algorithm Type | Beoordelingswaarden | Visualisaties |
| --- | --- | --- |
| Regressie | - RMSE <br> - MAPE <br> - MASE <br> - MAE | Voorspelde versus werkelijke bedekkingscurve voor waarden |
| Binaire indeling | - De matrijs van de verwarring <br> - precisie-herinner <br> - Nauwkeurigheid <br> - F-score (specifiek F1, F2) <br> - AUC <br> - ROC | ROC-curve en verwarringsmatrix |
| Classificatie van meerdere klassen | -Confusiematrix <br>- Voor elke klasse: <br> - precision-terugroepnauwkeurigheid <br> - F-score (met name F1, F2) | ROC-curve en verwarringsmatrix |
| Clustering (met waarheid op de grond) | - NMI (genormaliseerde wederzijdse informatiescore), AMI (aangepaste wederzijdse informatiescore) <br> - RI (de index van de Rand), ARI (aangepaste Rand index) <br> - homogeniteitsscore, volledigheidsscore, en V-maat <br> - FMI (Fowlkes-Mallows index) <br> - Zuiverheid <br> - Jaccard index | Clusters tekenen clusters en centroïden met relatieve clustergrootten die de gegevenspunten binnen een cluster weergeven |
| Clustering (zonder waarheid op de grond) | - Inertia <br> - Silhouette coëfficiënt <br> - CHI (Calinski-Harabaz index) <br> - DBI (Davies-Bouldin index) <br> - Dunn index | Clusters tekenen clusters en centroïden met relatieve clustergrootten die de gegevenspunten binnen een cluster weergeven |
| Aanbeveling | -Gemiddelde gemiddelde precisie (MAP) <br> - Genormaliseerde gekwantificeerde cumulatieve winst <br> - Gemiddelde wederkerige schijf <br> - Metrische K | TBD |
| Gebruiksgevallen van TensorFlow | TensorFlow Model Analysis (TFMA) | Vergelijking van neurale netwerkmodellen/visualisatie ongedaan maken |
| Ander/fout-vastlegmechanisme | De metrische logica van de douane (en overeenkomstige evaluatiekaarten) die door modelauteur worden bepaald. Handige foutafhandeling in geval van niet-overeenkomende sjabloon | Lijst met zeer belangrijke paren voor evaluatiemetriek |
