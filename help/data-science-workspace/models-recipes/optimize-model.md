---
keywords: Experience Platform;optimaliseren;model;Data Science Workspace;populaire onderwerpen;modelinzichten
solution: Experience Platform
title: Een model optimaliseren met behulp van het Model Insights Framework
topic: tutorial
type: Tutorial
description: Het Model Insights Framework biedt de gegevenswetenschapper hulpmiddelen in de Data Science Workspace om snelle en geïnformeerde keuzes te maken voor optimale modellen voor machinaal leren op basis van experimenten.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---


# Een model optimaliseren met behulp van het Model Insights-framework

Het Model Insights Framework biedt de gegevenswetenschapper de tools in [!DNL Data Science Workspace] om snelle en geïnformeerde keuzes te maken voor optimale modellen voor machinaal leren op basis van experimenten. Het kader zal de snelheid en doeltreffendheid van de werkstroom voor machinaal leren verbeteren en het gebruiksgemak voor gegevenswetenschappers verbeteren. Dit wordt gedaan door een standaardmalplaatje voor elk machine het leren algoritme type te verstrekken om met model het stemmen bij te wonen. Dankzij het eindresultaat kunnen wetenschappers op het gebied van gegevens en burgergegevens betere modeloptimalisatiebeslissingen maken voor hun eindgebruikers.

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

Voorbeeldcode voor recepten vindt u in de gegevensopslagruimte [experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference) onder `recipes`. In deze zelfstudie wordt verwezen naar specifieke bestanden in deze opslagplaats.

### Schalen {#scala}

Er zijn twee manieren om metriek in de recepten te brengen. Één moet de standaardevaluatiemetriek gebruiken die door SDK wordt verstrekt en andere moet de metriek van de douaneevaluatie schrijven.

#### Standaardevaluatiemetriek voor Scala

Standaardevaluaties worden berekend als onderdeel van de classificatiealgoritmen. Hier volgen enkele standaardwaarden voor beoordelaars die momenteel worden geïmplementeerd:

| Evaluatorklasse | `evaluation.class` |
--- | ---
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

De evaluator kan in het recept in het [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) dossier in `recipe` omslag worden bepaald. De voorbeeldcode voor het inschakelen van `DefaultBinaryClassificationEvaluator` wordt hieronder weergegeven:

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

Nadat een evaluatorklasse wordt toegelaten, zal een aantal metriek tijdens opleiding door gebrek worden berekend. De standaardmetriek kan uitdrukkelijk worden verklaard door de volgende lijn aan uw `application.properties` toe te voegen.

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>Als metrisch niet wordt bepaald, zullen de standaardmetriek actief zijn.

Een specifieke metrische waarde kan worden toegelaten door de waarde voor `evaluation.metrics.com` te veranderen. In het volgende voorbeeld, wordt metrisch F-Score toegelaten.

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

In de volgende tabel worden de standaardmetriek voor elke klasse weergegeven. Een gebruiker kan de waarden in `evaluation.metric` kolom ook gebruiken om specifieke metrisch toe te laten.

| `evaluator.class` | Standaardwaarden | `evaluation.metric` |
--- | --- | ---
| `DefaultBinaryClassificationEvaluator` | -Precision <br>-Recall <br>-Confusiematrix <br>-F-score <br>-Accuracy <br>-Receiver Operating Characteristics <br>-Area under the Receiver Operating Characters | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | -Precision <br>-Recall <br>-Confusiematrix <br>-F-score <br>-Accuracy <br>-Receiver Operating Characteristics <br>-Area under the Receiver Operating Characters | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -Gemiddelde gemiddelde precisie (MAP) <br>-genormaliseerde gekwantificeerde gecumuleerde gecumuleerde winst <br>-Gemiddelde kringloop <br>-Metrisch K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Eigen evaluatiemetriek voor Scala

De douanebeoordelaar kan worden verstrekt door de interface van `MLEvaluator.scala` in uw `Evaluator.scala` dossier uit te breiden. In het voorbeeld [Evaluator.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala), bepalen wij douane `split()` en `evaluate()` functies. Onze functie `split()` splitst onze gegevens willekeurig met een verhouding van 8:2 en onze functie `evaluate()` bepaalt en keert 3 metriek terug: MAPE, MAE en RMSE.

>[!IMPORTANT]
>
>Voor de `MLMetric` klasse, gebruik `"measures"` niet voor `valueType` wanneer het creëren van nieuw `MLMetric` anders metrisch zal niet in de lijst van metriek van de douaneevaluatie bevolken.
>  
> Doe dit: `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> Niet dit: `metrics.add(new MLMetric("MAPE", mape, "measures"))`


Wanneer het in het recept is gedefinieerd, is de volgende stap het in de recepten toelaten. Dit wordt gedaan in het [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) dossier in de `resources` omslag van het project. Hier wordt de `evaluation.class` ingesteld op de klasse `Evaluator` die is gedefinieerd in `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

In [!DNL Data Science Workspace], zou de gebruiker de inzichten in het lusje van &quot;Metriek van de Evaluatie&quot;in de experimenteerpagina kunnen zien.

### [!DNL Python/Tensorflow] {#pythontensorflow}

Vanaf nu zijn er geen standaardevaluatiemetriek voor [!DNL Python] of [!DNL Tensorflow]. Aldus, om de evaluatiemetriek voor [!DNL Python] of [!DNL Tensorflow] te krijgen, zult u een metrisch van de douaneevaluatie moeten tot stand brengen. Dit kan worden gedaan door de `Evaluator` klasse uit te voeren.

#### Eigen evaluatiemetriek voor [!DNL Python]

Voor de metriek van de douaneevaluatie, zijn er twee belangrijkste methodes die voor de beoordelaar moeten worden uitgevoerd: `split()` en `evaluate()`.

Voor [!DNL Python], zouden deze methodes in [beoordelator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) voor de `Evaluator` klasse worden bepaald. Volg de [beoordelator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) verbinding voor een voorbeeld van `Evaluator`.

Voor het maken van evaluatiemetriek in [!DNL Python] moet de gebruiker de methoden `evaluate()` en `split()` implementeren.

De methode `evaluate()` retourneert het metrische object dat een array van metrische objecten met eigenschappen `name`, `value` en `valueType` bevat.

Het doel van de `split()` methode is gegevens in te voeren en een opleiding en een testdataset uit te voeren. In ons voorbeeld voert de methode `split()` gegevens in met behulp van de SDK `DataSetReader` en wist vervolgens de gegevens door niet-verwante kolommen te verwijderen. Hierna worden extra functies gemaakt op basis van bestaande onbewerkte functies in de gegevens.

De `split()` methode zou een opleiding en testdataframe moeten terugkeren dat dan door de `pipeline()` methodes wordt gebruikt om het model van ML op te leiden en te testen.

#### Eigen evaluatiemetriek voor Tensorflow

Voor [!DNL Tensorflow], gelijkend op [!DNL Python], zullen de methodes `evaluate()` en `split()` in de `Evaluator` klasse moeten worden uitgevoerd. Voor `evaluate()`, zouden de metriek moeten zijn teruggekeerd terwijl `split()` de trein en de reeksen van testgegevens terugkeert.

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

Vanaf nu, zijn er geen standaardevaluatiemetriek voor R. Aldus, om de evaluatiemetriek voor R te krijgen, zult u de `applicationEvaluator` klasse als deel van het recept moeten bepalen.

#### Eigen evaluatiemetriek voor R

Het belangrijkste doel van `applicationEvaluator` is een voorwerp terug te keren JSON dat zeer belangrijk-waardeparen van metriek bevat.

Dit [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) kan als voorbeeld worden gebruikt. In dit voorbeeld wordt `applicationEvaluator` opgedeeld in drie vertrouwde secties:
- Gegevens laden
- Gegevensvoorbereiding/functietechniek
- Opgeslagen model ophalen en evalueren

De gegevens worden eerst geladen aan een dataset van een bron zoals die in [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json) wordt bepaald. Vanaf dat moment worden de gegevens gereinigd en zo ontworpen dat ze passen in het model voor machinaal leren. Tot slot wordt het model gebruikt om een voorspelling te maken die onze dataset gebruikt en van de voorspelde waarden en daadwerkelijke waarden, worden de metriek berekend. In dit geval worden MAPE, MAE en RMSE gedefinieerd en geretourneerd in het object `metrics`.

## Vooraf gebouwde metriek- en visualisatiekaarten gebruiken

[!DNL Sensei Model Insights Framework] zal één standaardmalplaatje voor elk type van machine het leren algoritme steunen. In de onderstaande tabel ziet u veelvoorkomende machineleesalgoritme-klassen en de bijbehorende evaluatiemetriek en -visualisaties.

| ML Algorithm Type | Beoordelingswaarden | Visualisaties |
--- | --- | ---
| Regressie | - RMSE<br>- MAPE<br>- MASE<br>- MAE | Voorspelde versus werkelijke bedekkingscurve voor waarden |
| Binaire indeling | - Verfusiematrix<br>- Precision-terugroeping<br>- Nauwkeurigheid<br>- F-score (specifiek F1,F2)<br>- AUC<br>- ROC | ROC-curve en verwarringsmatrix |
| Classificatie van meerdere klassen | -Confusiematrix <br>- Voor elke klasse: <br>- precisie-terugroepnauwkeurigheid <br>- F-score (met name F1, F2) | ROC-curve en verwarringsmatrix |
| Clustering (met waarheid op de grond) | - NMI (genormaliseerde score voor wederzijdse informatie), AMI (aangepaste score voor wederzijdse informatie)<br>- RI (Rand Index), ARI (aangepaste Rand Index)<br>- homogeniteitsscore, volledigheidsscore en V-maat<br>- FMI (Fowlkes-Mallows index)<br>- Zuiverheid<br>- Jaccard index | Clusters tekenen clusters en centroïden met relatieve clustergrootten die de gegevenspunten weergeven die binnen een cluster vallen |
| Clustering (zonder waarheid op de grond) | - Inertia<br>- Silhouetcoëfficiënt<br>- CHI (Calinski-Harabaz index)<br>- DBI (Davies-Bouldin index)<br>- Dunn index | Clusters tekenen clusters en centroïden met relatieve clustergrootten die de gegevenspunten weergeven die binnen een cluster vallen |
| Aanbeveling | -Gemiddelde gemiddelde precisie (MAP) <br>-genormaliseerde gekwantificeerde gecumuleerde gecumuleerde winst <br>-Gemiddelde kringloop <br>-Metrisch K | TBD |
| Gebruiksgevallen van TensorFlow | TensorFlow Model Analysis (TFMA) | Vergelijking van neurale netwerkmodellen/visualisatie ongedaan maken |
| Ander/fout-vastlegmechanisme | De metrische logica van de douane (en overeenkomstige evaluatiekaarten) die door modelauteur worden bepaald. Handige foutafhandeling in geval van niet-overeenkomende sjabloon | Lijst met zeer belangrijke paren voor evaluatiemetriek |
