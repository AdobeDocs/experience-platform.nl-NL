---
keywords: Experience Platform;ontwikkelaarshandleiding;Data Science Workspace;populaire onderwerpen;Real-time Machine Learning;node reference;
solution: Experience Platform
title: Naslaggids voor het leren van machines in realtime
description: Een knooppunt is de fundamentele eenheid waarvan grafieken worden gevormd. Elke knoop voert een specifieke taak uit en zij kunnen samen gebruikend verbindingen worden geketend om een grafiek te vormen die een pijpleiding van XML vertegenwoordigt. De taak die door een knoop wordt uitgevoerd vertegenwoordigt een verrichting op inputgegevens zoals een transformatie van gegevens of schema, of een machine het leren conclusie. Het knooppunt geeft de getransformeerde of afgeleide waarde uit aan de volgende node(s).
exl-id: 67fe26b5-ce03-4a9a-ad45-783b2acf8d92
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---

# Real-time Machine Learning node reference (Alpha)

>[!IMPORTANT]
>
>Het leren van de machine in real time is niet beschikbaar aan alle gebruikers nog. Deze functie bevindt zich in alfa en wordt nog steeds getest. Dit document kan worden gewijzigd.

Een knooppunt is de fundamentele eenheid waarvan grafieken worden gevormd. Elke knoop voert een specifieke taak uit en zij kunnen samen gebruikend verbindingen worden geketend om een grafiek te vormen die een pijpleiding van XML vertegenwoordigt. De taak die door een knoop wordt uitgevoerd vertegenwoordigt een verrichting op inputgegevens zoals een transformatie van gegevens of schema, of een machine het leren conclusie. Het knooppunt geeft de getransformeerde of afgeleide waarde uit aan de volgende node(s).

De volgende gids schetst de gesteunde knoopbibliotheken voor het Leren van de machine in real time.

## Het ontdekken van knopen voor gebruik in uw pijpleiding van ML

Kopieer de volgende code naar een [!DNL Python] -laptop om alle knooppunten weer te geven die beschikbaar zijn voor gebruik.

```python
from pprint import pprint
 
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
```

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

**reactie van het Voorbeeld**

```json
{'FieldOps': 'rtml_nodelibs.nodes.standard.preprocessing.fieldops.FieldOps',
 'FieldTrans': 'rtml_nodelibs.nodes.standard.preprocessing.fieldtrans.FieldTrans',
 'ModelUpload': 'rtml_nodelibs.nodes.standard.ml.artifact_utils.ModelUpload',
 'ONNXNode': 'rtml_nodelibs.nodes.standard.ml.onnx.ONNXNode',
 'Pandas': 'rtml_nodelibs.nodes.standard.preprocessing.pandasnode.Pandas',
 'Processor': 'rtml_nodelibs.nodes.standard.preprocessing.processor.Processor',
 'Receiver': 'rtml_nodelibs.nodes.standard.preprocessing.receiver.Receiver',
 'ScikitLearn': 'rtml_nodelibs.nodes.standard.ml.scikitlearn.ScikitLearn',
 'Simulator': 'rtml_nodelibs.nodes.standard.preprocessing.simulator.Simulator',
 'Split': 'rtml_nodelibs.nodes.standard.preprocessing.splitter.Split'}
```

## Standaardknooppunten

Standaardknooppunten bouwen voort op open-source gegevenswetenschapsbibliotheken zoals Pandas en ScikitLearn.

### ModelUpload

Het knooppunt ModelUpload is een interne node voor Adobe die een model_path neemt en het model uploadt van het lokale modelpad naar de blob-opslag voor machines in real time.

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNXNode

ONNXNode is een interne knoop van de Adobe die een modelidentiteitskaart neemt om het vooraf opgeleide model ONNX te trekken en het gebruikt om op inkomende gegevens te score.

>[!TIP]
>
>Geef de kolommen op in dezelfde volgorde als de gegevens die naar het ONNX-model moeten worden verzonden.

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### Pandas {#pandas}

Met het volgende Pandas-knooppunt kunt u elke `pd.DataFrame` -methode of elke algemene pandaserfunctie op hoofdniveau importeren. Meer over de methodes van Pandas leren, bezoek de [ Pandas methodedocumentatie ](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html). Voor meer informatie over hoogste niveaufuncties, bezoek de [ Pandas API verwijzingsgids voor algemene functies ](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html).

Het onderstaande knooppunt gebruikt `"import": "map"` om de methodenaam als een tekenreeks in de parameters te importeren, gevolgd door de parameters in te voeren als een kaartfunctie. In het onderstaande voorbeeld wordt dit gedaan met `{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}` . Nadat u de kaart hebt geplaatst, kunt u `inplace` instellen als `True` of `False` . Stel `inplace` in als `True` of `False` op basis van of u transformatie wilt toepassen. Standaard maakt `"inplace": False` een nieuwe kolom. Ondersteuning voor het opgeven van een nieuwe kolomnaam is ingesteld om in een volgende release te worden toegevoegd. De laatste regel `cols` kan één kolomnaam of een lijst met kolommen zijn. Geef de kolommen op waarop u de transformatie wilt toepassen. In dit voorbeeld wordt `device` opgegeven.

```python
#  df["device"] = df["device"].map({"Desktop":1, "Mobile":0}, na_action=0)
 
node_device_apply = Pandas(params={"import": "map",
    "kwargs": {"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0},
    "inplace": True,
    "cols": "device"})
 
 
# df["browser"] = df["browser"].map({"chrome": 1, "firefox": 0}, "na_action": 0})
 
node_browser_apply = Pandas(params={"import": "map",
    "kwargs": {"arg": {"chrome": 1, "firefox": 0}, "na_action": 0},
    "inplace": True,
    "cols": "browser"})
```

### ScikitLearn

Met het ScikitLearn-knooppunt kunt u elk ScikitLearn ML-model of -scaler importeren. Gebruik de onderstaande tabel voor meer informatie over de waarden die in het voorbeeld worden gebruikt:

```python
model_train = ScikitLearn(params={
    "features":['browser', 'device', 'login_page', 'product_page', 'search_page'],
    "label": "payment_confirm",
    "mode": "train",
    "model_path": "resources/model.onnx",
    "params": {
        "model": "sklearn.linear_model.LogisticRegression",
        "model_params": {"solver": 'lbfgs'}
    }})
msg6 = model_train.process(msg5)
```

| Waarde | Beschrijving |
| --- | --- |
| functies | Invoerfuncties voor het model (lijst met tekenreeksen). <br> Bijvoorbeeld: `browser`, `device`, `login_page`, `product_page`, `search_page` |
| label | Naam van doelkolom (tekenreeks). |
| mode | Trein/test (tekenreeks). |
| model_path | Pad naar het model lokaal opslaan in onx-indeling. |
| params.model | Absoluut importpad naar het model (tekenreeks), bijvoorbeeld: `sklearn.linear_model.LogisticRegression` . |
| params.model_params | Model hyperparameters, zie de [ klearn API (kaart/dict) ](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) documentatie voor meer informatie. |
| node_instance.process(data_message_from_previous_node) | De methode `process()` neemt DataMsg van de vorige knoop en past transformatie toe. Dit hangt van de huidige knoop af die wordt gebruikt. |

### Splitsen

Gebruik het volgende knooppunt om uw gegevensframe in een trein te splitsen en te testen door `train_size` of `test_size` door te geven. Dit retourneert een dataframe met een meervoudige index. U hebt toegang tot dataframes van de trein en kunt deze testen met behulp van het volgende voorbeeld, `msg5.data.xs("train")` .

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## Volgende stappen

De volgende stap is knopen voor gebruik in het scoren van een Echte-tijd het Leren van de Machine model tot stand te brengen. Voor meer informatie, bezoek de [ Echt - tijd machine die notitieboekjectgebruikershandleiding ](./rtml-authoring-notebook.md) leren.
