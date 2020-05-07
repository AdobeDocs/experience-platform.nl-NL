---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;node reference;
solution: Experience Platform
title: Score een Echte Model van de Machine het Leren
topic: Scoring a ML model
translation-type: tm+mt
source-git-commit: dd2c9714c410d00ef2ba06e9f9728747fc6f989a
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---


# Score een Echte Model van de Machine het Leren

>[!IMPORTANT]
>Het leren van de machine in real time is niet beschikbaar aan alle gebruikers nog. Deze functie bevindt zich in alfa en wordt nog steeds getest. Dit document kan worden gewijzigd.

Deze zelfstudie laat zien hoe u in real time Machine Learning-knooppunten kunt gebruiken om inkomende gegevens vooraf te verwerken en deze op uw ONNX-model te scoren.

>[!IMPORTANT]
> - De functies die in knopen worden gebruikt kunnen niet in series worden vervaardigd. Bijvoorbeeld, een lambdafunctie die in een pandasknoop wordt gebruikt.
> - Er is 60 seconden slaap nadat de randplaatsing manueel wordt gedaan. Dit kan naar de score_edge methode van EdgeUtils worden overgebracht.


>[!NOTE]
>Om een model voor gebruik in het Leren van de Machine in real time te scoren moet u het vorige leerprogramma over het [trainen van een model voor het Leren van de Machine in real time hebben voltooid](./training-ml-model.md)

## Een nieuw notebook maken

Selecteer in de gebruikersinterface van het Adobe Experience Platform **[!UICONTROL laptops]** uit *Data Science*. Selecteer vervolgens **[!UICONTROL JupyterLab]** en laat de omgeving enige tijd laden.

![open JupyterLab](../images/rtml/open-jupyterlab.png)

Begin met het selecteren van de **lege Python 3-laptop** in de JupyterLab-startprogramma.

![blanco python](../images/rtml/python-blank.png)

## Knooppunten importeren en ontdekken

Begin door alle vereiste pakketten voor uw model in te voeren. Zorg ervoor om het even welke pakketten u op het gebruiken voor knoop creatie van plan bent worden ingevoerd.

>[!NOTE]
>De lijst met geïmporteerde producten kan afwijken, afhankelijk van het model dat u hebt gemaakt.

```python
from pprint import pprint
import json
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
from rtml_sdk.graph.utils import GraphBuilder
from rtml_sdk.edge.utils import EdgeUtils

from rtml_nodelibs.nodes.standard.preprocessing.pandasnode import Pandas
from rtml_nodelibs.nodes.standard.ml.onnx import ONNXNode
from rtml_nodelibs.nodes.standard.preprocessing.json_to_df import JsonToDataframe
from rtml_nodelibs.core.datamsg import DataMsg
import uuid
```

Kopieer en plak het volgende voorbeeld in uw notitieboek om de lijst met beschikbare knooppunten weer te geven.

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

De ontvangen reactie is een lijst met knooppunten.

![lijst van notities](../images/rtml/node-list.png)

## Knooppuntontwerp voor randschildering

Vervolgens moet u een knooppunt voor randscoring definiëren en ontwerpen. Vervang het `model_id` in het voorbeeld door uw model-id die u hebt ontvangen van het voltooien van de training in de [vorige zelfstudie](./training-ml-model.md). In dit voorbeeld wordt het knooppunt Pandas gebruikt om een methode pd.DataDrame of een algemene functie op hoofdniveau voor panda&#39;s te importeren. De kaartfunctie wordt geïmporteerd en gebruikt om twee knooppunten te maken. Voor meer informatie over de beschikbare knopen en hoe te om hen te gebruiken, bezoek de gids [van de](./node-reference.md)knoopverwijzing.

```python
model_id = '{your_model_id}' # Get Model ID from Training Notebook.

data = {'sepal_length': {0: 5.8},
        'sepal_width': {0: 2.8},
        'petal_length': {0: 5.1},
        'petal_width': {0: 2.4}}

json2DF_node = JsonToDataframe(params={"json_payload":json.dumps(data)})
fill_na_node = Pandas(params={"import": "fillna", "kwargs":{"value":0}})
model_score_node = ONNXNode(params={"features": ['sepal_length', 'sepal_width', 'petal_length', 'petal_width'],
                                    "model_id": model_id})
```

## Build Graph DSL

Als uw knooppunten zijn gemaakt, bestaat de volgende stap uit het koppelen van de knooppunten om een grafiek te maken.

Begin door alle knooppunten weer te geven die deel uitmaken van de grafiek.

```python
nodes = [node_device_apply, node_browser_apply, node_model_score]
```

Sluit vervolgens de knooppunten aan op de randen. Elke tuple is een randverbinding.

```python
edges = [ (node_device_apply, node_browser_apply), (node_browser_apply, node_model_score)]
```

Maak de grafiek wanneer uw knooppunten zijn verbonden.

```python
dsl = GraphBuilder.generate_dsl(nodes=nodes, edges=edges)
```

## Publiceren naar rand

Nu u een grafiek hebt gemaakt, kunt u de grafiek op de rand toepassen.

>[!IMPORTANT]
>Publiceer niet vaak naar edge, waardoor de randknooppunten kunnen worden overbelast. Het wordt niet aanbevolen hetzelfde model meerdere keren te publiceren.

```python
edge_utils = EdgeUtils()
(edge_location, service_id) = edge_utils.publish_to_edge(dsl=dsl)
```

## Edge-client

Na het publiceren aan rand, wordt het scoren gedaan door een POST- verzoek van een cliënt. Dit kan doorgaans worden gedaan vanuit een clienttoepassing waarvoor XML-scores vereist zijn. Je kunt het ook van Postman doen. Hier, wordt EdgeUtils gebruikt om het proces aan te tonen.

```python
import time
time.sleep(600)
```

```python
data = {"sepal_length": {0: 5.8}, "sepal_width": {0: 2.8}, "petal_length": {0: 5.1}, "petal_width": {0: 2.4}}
```

```python
scored_output = edge_utils.score_edge(edge_location=edge_location,
                              service_id=service_id,
                              scoring_data=data)
print(f'Scored Output from Edge: {scored_output}')
```

Zodra het scoren is voltooid, worden de rand-URL, Payload en de gescorde uitvoer van edge geretourneerd.

![scoring voltooid](../images/rtml/scoring-complete.png)

## Een geïmplementeerde toepassing van rand verwijderen (optioneel)

>!![CAUTION]
Deze cel wordt gebruikt om uw opgestelde randtoepassing te schrappen. Gebruik de volgende cel alleen als u een geïmplementeerde randtoepassing moet verwijderen.

```python
if edge_utils.delete_from_edge(service_id=service_id):
    print(f"Deleted service id {service_id} successfully")
else:
    print(f"Failed to delete service id {service_id}")
```

## Volgende stappen

Door het leerprogramma hierboven te volgen, hebt u met succes uw het Leren model van de machine in real time gesteund en opgesteld. Als u meer over de knopen beschikbaar voor modelontwerp wilt leren, bezoek de gids [van de](./node-reference.md)knoopverwijzing.



