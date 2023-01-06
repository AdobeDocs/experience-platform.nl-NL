---
keywords: Experience Platform;optimaliseren;model;Data Science Workspace;populaire onderwerpen;modelinzichten
solution: Experience Platform
title: Een model optimaliseren met behulp van het Model Insights Framework
type: Tutorial
description: Het Model Insights Framework biedt de gegevenswetenschapper hulpmiddelen in de Data Science Workspace om snelle en geïnformeerde keuzes te maken voor optimale modellen voor machinaal leren op basis van experimenten.
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---

# Een model optimaliseren met behulp van het Model Insights-framework

Het Model Insights Framework biedt de gegevenswetenschapper instrumenten in [!DNL Data Science Workspace] snelle en geïnformeerde keuzes te maken voor optimale modellen voor machinaal leren op basis van experimenten. Het kader zal de snelheid en doeltreffendheid van de werkstroom voor machinaal leren verbeteren en het gebruiksgemak voor gegevenswetenschappers verbeteren. Dit wordt gedaan door een standaardmalplaatje voor elk machine het leren algoritme type te verstrekken om met model het stemmen bij te wonen. Dankzij het eindresultaat kunnen wetenschappers op het gebied van gegevens en burgergegevens betere modeloptimalisatiebeslissingen maken voor hun eindgebruikers.

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

Voorbeeldcode voor recepten vindt u in het gedeelte [experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference) opslagplaats onder `recipes`. In deze zelfstudie wordt verwezen naar specifieke bestanden in deze opslagplaats.

### Scala {#scala}

Er zijn twee manieren om metriek in de recepten te brengen. Één moet de standaardevaluatiemetriek gebruiken die door SDK wordt verstrekt en andere moet de metriek van de douaneevaluatie schrijven.

#### Standaardevaluatiemetriek voor Scala

Standaardevaluaties worden berekend als onderdeel van de classificatiealgoritmen. Hier volgen enkele standaardwaarden voor beoordelaars die momenteel worden geïmplementeerd:

| Evaluatorklasse | `evaluation.class` |
|--- | ---|
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

De beoordelaar kan worden gedefinieerd in het recept in het [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) in het `recipe` map. Voorbeeldcode die het mogelijk maakt `DefaultBinaryClassificationEvaluator` wordt hieronder weergegeven:

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

Nadat een evaluatorklasse wordt toegelaten, zal een aantal metriek tijdens opleiding door gebrek worden berekend. De standaardmetriek kan uitdrukkelijk worden verklaard door de volgende lijn aan uw toe te voegen `application.properties`.

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>Als metrisch niet wordt bepaald, zullen de standaardmetriek actief zijn.

Een specifieke metrische waarde kan worden toegelaten door de waarde te veranderen voor `evaluation.metrics.com`. In het volgende voorbeeld, wordt metrisch F-Score toegelaten.

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

In de volgende tabel worden de standaardmetriek voor elke klasse weergegeven. Een gebruiker kan ook de waarden in het dialoogvenster `evaluation.metric` kolom om specifieke metrisch toe te laten.

| `evaluator.class` | Standaardwaarden | `evaluation.metric` |
| --- | --- | --- |
| `DefaultBinaryClassificationEvaluator` | -Precision <br>-Recall <br>-Verfusiematrix <br>-F-score <br>-Nauwkeurigheid <br>- Operationele kenmerken van de ontvanger <br>-Gebied onder de exploitatiekenmerken van de ontvanger | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | -Precision <br>-Recall <br>-Verfusiematrix <br>-F-score <br>-Nauwkeurigheid <br>- Operationele kenmerken van de ontvanger <br>-Gebied onder de exploitatiekenmerken van de ontvanger | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -Gemiddelde gemiddelde precisie (MAP) <br>- Genormaliseerde gedisconteerde cumulatieve winst <br>-Gemiddelde Wederkerige Rang <br>-Metrisch K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Eigen evaluatiemetriek voor Scala

De aangepaste beoordelaar kan worden opgegeven door de interface van `MLEvaluator.scala` in uw `Evaluator.scala` bestand. In het voorbeeld [Evaluator.range](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) bestand, definiëren we aangepaste `split()` en `evaluate()` functies. Ons `split()` functie splitst de gegevens willekeurig met een verhouding van 8:2 en onze `evaluate()` function definieert en retourneert 3 metriek: MAPE, MAE en RMSE.

>[!IMPORTANT]
>
>Voor de `MLMetric` klasse, niet gebruiken `"measures"` for `valueType` bij het maken van een nieuwe `MLMetric` anders zal metrisch niet in de lijst van metriek van de douaneevaluatie bevolken.
>  
> Doe dit: `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> Niet dit: `metrics.add(new MLMetric("MAPE", mape, "measures"))`


Wanneer het in het recept is gedefinieerd, is de volgende stap het in de recepten toelaten. Dit wordt gedaan in [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) bestand in de `resources` map. Hier `evaluation.class` is ingesteld op `Evaluator` klasse gedefinieerd in `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

In de [!DNL Data Science Workspace]De gebruiker zou de inzichten op het tabblad &quot;Evaluatiemetriek&quot; in de testpagina kunnen bekijken.

### [!DNL Python/Tensorflow] {#pythontensorflow}

Op dit moment zijn er geen standaardevaluatiemetriek voor [!DNL Python] of [!DNL Tensorflow]. Aldus, om de evaluatiemetriek voor te krijgen [!DNL Python] of [!DNL Tensorflow], zult u een metrische douaneevaluatie moeten tot stand brengen. Dit kan worden gedaan door de `Evaluator` klasse.

#### Eigen evaluatiemetriek voor [!DNL Python]

Voor de metriek van de douaneevaluatie, zijn er twee belangrijkste methodes die voor de beoordelaar moeten worden uitgevoerd: `split()` en `evaluate()`.

Voor [!DNL Python]Deze methoden worden gedefinieerd in [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) voor de `Evaluator` klasse. Volg de [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) koppeling voor een voorbeeld van de `Evaluator`.

Beoordelingsmaatstaven maken in [!DNL Python] vereist dat de gebruiker de `evaluate()` en `split()` methoden.

De `evaluate()` methode retourneert het metrische object dat een array van metrische objecten bevat met eigenschappen van `name`, `value`, en `valueType`.

Het doel van de `split()` methode is het invoeren van gegevens en het uitvoeren van een opleiding en een testdataset. In ons voorbeeld `split()` gegevens van methodeinput gebruiken `DataSetReader` SDK en schoont dan de gegevens door niet verwante kolommen te verwijderen. Hierna worden extra functies gemaakt op basis van bestaande onbewerkte functies in de gegevens.

De `split()` Deze methode retourneert een dataframe voor training en testen dat vervolgens door de `pipeline()` methoden om het ML-model op te leiden en te testen.

#### Eigen evaluatiemetriek voor Tensorflow

Voor [!DNL Tensorflow], vergelijkbaar met [!DNL Python], de methoden `evaluate()` en `split()` in de `Evaluator` klasse zal moeten worden uitgevoerd. Voor `evaluate()`, moeten de metriek worden geretourneerd terwijl `split()` retourneert de trein- en testgegevenssets.

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

Vanaf nu, zijn er geen standaardevaluatiemetriek voor R. Aldus, om de evaluatiemetriek voor R te krijgen, zult u moeten bepalen `applicationEvaluator` als onderdeel van het recept.

#### Eigen evaluatiemetriek voor R

Het hoofddoel van de `applicationEvaluator` moet een JSON-object retourneren dat sleutelwaardeparen metriek bevat.

Dit [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) kan als voorbeeld worden gebruikt. In dit voorbeeld wordt `applicationEvaluator` is opgedeeld in drie vertrouwde secties:
- Gegevens laden
- Gegevensvoorbereiding/functietechniek
- Opgeslagen model ophalen en evalueren

De gegevens worden eerst geladen aan een dataset van een bron zoals bepaald in [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json). Vanaf dat moment worden de gegevens gereinigd en zo ontworpen dat ze passen in het model voor machinaal leren. Ten slotte, wordt het model gebruikt om een voorspelling te maken gebruikend onze dataset en van de voorspelde waarden en daadwerkelijke waarden, worden de metriek berekend. In dit geval worden MAPE, MAE en RMSE gedefinieerd en geretourneerd in het dialoogvenster `metrics` object.

## Vooraf gebouwde metriek- en visualisatiekaarten gebruiken

De [!DNL Sensei Model Insights Framework] zal één standaardmalplaatje voor elk type van machine het leren algoritme steunen. In de onderstaande tabel ziet u veelvoorkomende machineleesalgoritme-klassen en de bijbehorende evaluatiemetriek en -visualisaties.

| ML Algorithm Type | Beoordelingswaarden | Visualisaties |
| --- | --- | --- |
| Regressie | - RMSE<br>- MAPE<br>- MASE<br>- MAE | Voorspelde versus werkelijke bedekkingscurve voor waarden |
| Binaire indeling | - Verfusiematrix<br>- Precision-terugroepen<br>- Nauwkeurigheid<br>- F-score (met name F1,F2)<br>- AUC<br>- ROC | ROC-curve en verwarringsmatrix |
| Classificatie van meerdere klassen | -Verfusiematrix <br>- Voor elke klasse: <br>- precisie van de terugroepacties <br>- F-score (met name F1, F2) | ROC-curve en verwarringsmatrix |
| Clustering (met waarheid op de grond) | - NMI (genormaliseerde score voor wederzijdse informatie), AMI (aangepaste score voor wederzijdse informatie)<br>- RI (Rand Index), ARI (Aangepaste Rand Index)<br>- homogeniteitsscore, volledigheidsscore en V-maat<br>- FMI (Fowlkes-Mallows-index)<br>- Zuiverheid<br>- Jaccard-index | Clusters tekenen clusters en centroïden met relatieve clustergrootten die de gegevenspunten weergeven die binnen een cluster vallen |
| Clustering (zonder waarheid op de grond) | - Inertia<br>- Silhouetcoëfficiënt<br>- CHI (index Calinski-Harabaz)<br>- DBI (index van Davies-Bouldin)<br>- Dunn-index | Clusters tekenen clusters en centroïden met relatieve clustergrootten die de gegevenspunten weergeven die binnen een cluster vallen |
| Aanbeveling | -Gemiddelde gemiddelde precisie (MAP) <br>- Genormaliseerde gedisconteerde cumulatieve winst <br>-Gemiddelde Wederkerige Rang <br>-Metrisch K | TBD |
| Gebruiksgevallen van TensorFlow | TensorFlow Model Analysis (TFMA) | Vergelijking van neurale netwerkmodellen/visualisatie ongedaan maken |
| Ander/fout-vastlegmechanisme | De metrische logica van de douane (en overeenkomstige evaluatiekaarten) die door modelauteur worden bepaald. Handige foutafhandeling in geval van niet-overeenkomende sjabloon | Lijst met zeer belangrijke paren voor evaluatiemetriek |
