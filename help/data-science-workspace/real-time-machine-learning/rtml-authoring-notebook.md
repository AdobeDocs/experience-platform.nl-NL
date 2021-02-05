---
keywords: Experience Platform;ontwikkelaarsgids;de Werkruimte van de Wetenschap van Gegevens;populaire onderwerpen;In real time machine het leren;knoopverwijzing;
solution: Experience Platform
title: Real-time Machine Learning-laptops beheren
topic: Training and scoring a ML model
description: In de volgende handleiding worden de stappen beschreven die nodig zijn om een toepassing voor het leren van machines in realtime te maken in Adobe Experience Platform JupyterLab.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '1669'
ht-degree: 0%

---


# Real-time Machine Learning-laptops beheren (Alpha)

>[!IMPORTANT]
>
>Het leren van de machine in real time is niet beschikbaar aan alle gebruikers nog. Deze functie bevindt zich in alfa en wordt nog steeds getest. Dit document kan worden gewijzigd.

In de volgende handleiding worden de stappen beschreven die nodig zijn om een toepassing voor het leren van machines in realtime te bouwen. Met behulp van de Adobe die **[!UICONTROL Real-time ML]** Python notebooksjabloon wordt aangeboden, behandelt deze handleiding het trainen van een model, het creëren van een DSL, het publiceren van DSL aan Rand, en het scoren van het verzoek. Aangezien u door het uitvoeren van uw het Leren model van de machine in real time vordert, wordt verwacht dat u het malplaatje wijzigt om de behoeften van uw dataset te passen.

## Een laptop voor real-time leren van machines maken

Selecteer **[!UICONTROL Laptops]** in de gebruikersinterface van Adobe Experience Platform vanuit **Gegevenswetenschap**. Selecteer vervolgens **[!UICONTROL JupyterLab]** en laat enige tijd over aan het laden van de omgeving.

![open JupyterLab](../images/rtml/open-jupyterlab.png)

De [!DNL JupyterLab]-startprogramma wordt weergegeven. Blader omlaag naar *Real-Time Machine Learning* en selecteer de **[!UICONTROL Real-time ML]**-laptop. Er wordt een sjabloon geopend met voorbeeldlaptopcellen met een voorbeeldgegevensset.

![blanco python](../images/rtml/authoring-notebook.png)

## Knooppunten importeren en ontdekken

Begin door alle vereiste pakketten voor uw model in te voeren. Zorg ervoor om het even welk pakket u op het gebruiken voor knoop creatie van plan bent wordt ingevoerd.

>[!NOTE]
>
>De lijst met geïmporteerde producten kan afwijken, afhankelijk van het model dat u wilt maken. Deze lijst zal veranderen aangezien de nieuwe knopen in tijd worden toegevoegd. Raadpleeg de [nodenaslaggids](./node-reference.md) voor een volledige lijst met beschikbare knooppunten.

```python
from pprint import pprint
import pandas as pd
import numpy as np
import json
import uuid
from shutil import copyfile
from pathlib import Path
from datetime import date, datetime, timedelta
from platform_sdk.dataset_reader import DatasetReader

from rtml_nodelibs.nodes.standard.preprocessing.json_to_df import JsonToDataframe
from rtml_sdk.edge.utils import EdgeUtils
from rtml_sdk.graph.utils import GraphBuilder
from rtml_nodelibs.nodes.standard.ml.onnx import ONNXNode
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
from rtml_nodelibs.nodes.standard.preprocessing.pandasnode import Pandas
from rtml_nodelibs.nodes.standard.preprocessing.one_hot_encoder import OneHotEncoder
from rtml_nodelibs.nodes.standard.ml.artifact_utils import ModelUpload
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
from rtml_nodelibs.core.datamsg import DataMsg
```

In de volgende codecel wordt een lijst met beschikbare knooppunten afgedrukt.

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

![lijst van notities](../images/rtml/node-list.png)

## Een real-time leren van machines trainen

Als u een van de volgende opties gebruikt, gaat u [!DNL Python]-code schrijven om gegevens te lezen, vooraf te verwerken en te analyseren. Daarna, moet u uw eigen model van XML trainen, het in formaat rangschikken ONNX en dan uploadt het aan het Leren modelopslag van de machine in real time.

- [Uw eigen model trainen in JupyterLab-laptops](#training-your-own-model)
- [Uw eigen vooraf getrainde ONNX-model uploaden naar JupyterLab-laptops](#pre-trained-model-upload)

### Uw eigen model opleiden {#training-your-own-model}

Begin met het laden van uw trainingsgegevens.

>[!NOTE]
>
>In de **Real-time ML** sjabloon wordt de [CSV dataset van autoverzekering](https://github.com/adobe/experience-platform-dsw-reference/tree/master/datasets/insurance) opgehaald uit [!DNL Github].

![Trainingsgegevens laden](../images/rtml/load_training.png)

Als u een gegevensset wilt gebruiken vanuit Adobe Experience Platform, verwijdert u de commentaarmarkering uit de onderstaande cel. Vervolgens moet u `DATASET_ID` vervangen door de juiste waarde.

![rtml-gegevensset](../images/rtml/rtml-dataset.png)

Als u toegang wilt krijgen tot een gegevensset in uw [!DNL JupyterLab]-laptop, selecteert u het tabblad **Gegevens** in de linkernavigatie van [!DNL JupyterLab]. De directory **[!UICONTROL Datasets]** en **[!UICONTROL Schemas]** worden weergegeven. Selecteer **[!UICONTROL Datasets]** en klik met de rechtermuisknop, dan selecteer **[!UICONTROL Gegevens in Notitieboekje]** optie van het drop-down menu op de dataset u wenst te gebruiken. Onder aan de laptop wordt een uitvoerbaar code-item weergegeven. Deze cel heeft uw `dataset_id`.

![toegang tot gegevensset](../images/rtml/access-dataset.png)

Klik met de rechtermuisknop en verwijder de cel die u onder aan de laptop hebt gegenereerd.

### Trainingseigenschappen

Wijzig met behulp van de meegeleverde sjabloon een van de trainingseigenschappen binnen `config_properties`.

```python
config_properties = {
    "train_records_limit":1000000,
    "n_estimators": "80",
    "max_depth": "5",
    "ten_id": "_experienceplatform"  
}
```

### Uw model voorbereiden

Gebruikend **[!UICONTROL Real-time ML]** malplaatje, moet u uw model van ML analyseren, vooraf verwerken, trainen, en evalueren. Dit wordt gedaan door gegevenstransformaties toe te passen en een opleidingspijpleiding te bouwen.

**Gegevenstransformaties**

De **[!UICONTROL In real time ML]** malplaatjes **De cel van de Transformaties van Gegevens** moet worden gewijzigd om met uw eigen dataset te werken. Doorgaans gaat het hier om het wijzigen van de naam van kolommen, rollup van gegevens en het voorbereiden en bewerken van gegevens.

>[!NOTE]
>
>Het volgende voorbeeld is voor leesbaarheidsdoeleinden gecondenseerd met `[ ... ]`. Gelieve te bekijken en uit te breiden *Real-time ML* de sectie van malplaatjegegevenstransformaties voor de volledige codecel.

```python
df1.rename(columns = {config_properties['ten_id']+'.identification.ecid' : 'ecid',
                     [ ... ]}, inplace=True)
df1 = df1[['ecid', 'km', 'cartype', 'age', 'gender', 'carbrand', 'leasing', 'city', 
       'country', 'nationality', 'primaryuser', 'purchase', 'pricequote', 'timestamp']]
print("df1 shape 1", df1.shape)
#########################################
# Data Rollup
######################################### 
df1['timestamp'] = pd.to_datetime(df1.timestamp)
df1['hour'] = df1['timestamp'].dt.hour.astype(int)
df1['dayofweek'] = df1['timestamp'].dt.dayofweek

df1.loc[(df1['purchase'] == 'yes'), 'purchase'] = 1
df1.purchase.fillna(0, inplace=True)
df1['purchase'] = df1['purchase'].astype(int)

[ ... ]

print("df1 shape 2", df1.shape)

#########################################
# Data Preparation/Feature Engineering
#########################################      

df1['carbrand'] = df1['carbrand'].str.lower()
df1['country'] = df1['country'].str.lower()
df1.loc[(df1['carbrand'] == 'vw'), 'carbrand'] = 'volkswagen'

[ ... ]

df1['age'].fillna(df1['age'].median(), inplace=True)
df1['gender'].fillna('notgiven', inplace=True)

[ ... ]

df1['city'] = df1.groupby('country')['city'].transform(lambda x : x.fillna(x.mode()))
df1.dropna(subset = ['pricequote'], inplace=True)
print("df1 shape 3", df1.shape)
print(df1)

#grouping
grouping_cols = ['carbrand', 'cartype', 'city', 'country']

for col in grouping_cols:
    df_idx = pd.DataFrame(df1[col].value_counts().head(6))

    def grouping(x):
        if x in df_idx.index:
            return x
        else:
            return "Others"
    df1[col] = df1[col].apply(lambda x: grouping(x))

def age(x):
    if x < 20:
        return "u20"
    elif x > 19 and x < 29:
    [ ... ]
    else: 
        return "Others"

df1['age'] = df1['age'].astype(int)
df1['age_bucket'] = df1['age'].apply(lambda x: age(x))

df_final = df1[['hour', 'dayofweek','age_bucket', 'gender', 'city',  
   'country', 'carbrand', 'cartype', 'leasing', 'pricequote', 'purchase']]
print("df final", df_final.shape)

cat_cols = ['age_bucket', 'gender', 'city', 'dayofweek', 'country', 'carbrand', 'cartype', 'leasing']
df_final = pd.get_dummies(df_final, columns = cat_cols)
```

Voer de opgegeven cel uit om een voorbeeldresultaat te zien. De outputlijst die van `carinsurancedataset.csv` dataset is teruggekeerd keert de wijzigingen terug u bepaalde.

![Voorbeeld van gegevenstransformaties](../images/rtml/table-return.png)

**Trainingsleiding**

Daarna moet u de trainingspijpleiding tot stand brengen. Dit zal gelijkaardig aan een ander dossier van de trainingspijpleiding kijken behalve u moet omzetten en een ONNX dossier produceren.

Wijzig de sjabloon met de gegevenstransformaties die in de vorige cel zijn gedefinieerd. De volgende hieronder benadrukte code wordt gebruikt voor het produceren van een ONNX- dossier in uw eigenschappijpleiding. Gelieve te bekijken *Real-time ML* malplaatje voor de volledige cel van de pijpleidingscode.

```python
#for generating onnx
def generate_onnx_resources(self):        
    install_dir = os.path.expanduser('~/my-workspace')
    print("Generating Onnx")
        
    from skl2onnx import convert_sklearn
    from skl2onnx.common.data_types import FloatTensorType
        
    # ONNX-ification
    initial_type = [('float_input', FloatTensorType([None, self.feature_len]))]

    print("Converting Model to Onnx")
    onx = convert_sklearn(self.model, initial_types=initial_type)
             
    with open("model.onnx", "wb") as f:
        f.write(onx.SerializeToString())
            
    print("Model onnx created")
```

Nadat u de trainingsleiding hebt voltooid en uw gegevens hebt gewijzigd via gegevenstransformaties, gebruikt u de volgende cel om training uit te voeren.

```python
model = train(config_properties, df_final)
```

### Een ONNX-model genereren en uploaden

Nadat u een training hebt voltooid, moet u een ONNX-model genereren en het opgeleide model uploaden naar de modelwinkel voor het leren van machines in real time. Nadat u de volgende cellen hebt uitgevoerd, verschijnt uw ONNX-model in de linkerrail naast al uw andere laptops.

```python
import os
import skl2onnx, subprocess

model.generate_onnx_resources()
```

>[!NOTE]
>
>Wijzig de tekenreekswaarde `model_path` (`model.onnx`) om de naam van het model te wijzigen.

```python
model_path = "model.onnx"
```

>[!NOTE]
>
>De volgende cel is niet bewerkbaar of kan worden verwijderd en is vereist voor het werken van uw toepassing voor het leren van machines in realtime.

```python
model = ModelUpload(params={'model_path': model_path})
msg_model = model.process(None, 1)
model_id = msg_model.model['model_id']
 
print("Model ID : ", model_id)
```

![ONNX-model](../images/rtml/onnx-model-rail.png)

### Uw eigen vooraf opgeleide ONNX-model uploaden {#pre-trained-model-upload}

Met de uploadknop in [!DNL JupyterLab]-laptops kunt u uw vooraf opgeleide ONNX-model uploaden naar de [!DNL Data Science Workspace]-laptopomgeving.

![uploadpictogram](../images/rtml/upload.png)

Wijzig vervolgens de tekenreekswaarde `model_path` in de laptop *Real-time ML*, zodat deze overeenkomt met de naam van uw ONNX-model. Zodra voltooid, stel de *modelweg* cel in en stel dan *Upload uw model aan RTML ModelStore* cel in werking. Uw modellocatie en model-id worden beide geretourneerd in de reactie als de bewerking succesvol was.

![eigen model uploaden](../images/rtml/upload-own-model.png)

## Maken van domeinspecifieke taal (DSL)

Deze sectie schetst het creëren van een DSL. U gaat de knopen schrijven die om het even welke voorverwerking van gegevens samen met knoop ONNX omvatten. Vervolgens wordt een DSL-grafiek gemaakt met knooppunten en randen. Randen verbinden knooppunten met behulp van een op twee gebaseerde indeling (node_1, node_2). De grafiek moet geen cycli hebben.

>[!IMPORTANT]
>
>Het gebruik van het ONNX-knooppunt is verplicht. Zonder het ONNX-knooppunt is de toepassing mislukt.

### Node authoring

>[!NOTE]
>
> U hebt waarschijnlijk meerdere knooppunten op basis van het type gegevens dat wordt gebruikt. Het volgende voorbeeld schetst slechts één enkele knoop in *Real-time ML* malplaatje. Bekijk de *Real-time ML* sjablonen *Node Authoring* sectie voor de volledige codecel.

Het Pandas-knooppunt hieronder gebruikt `"import": "map"` om de methodenaam als een tekenreeks in de parameters te importeren, gevolgd door de parameters in te voeren als een toewijzingsfunctie. In het onderstaande voorbeeld wordt dit gedaan met `{'arg': {'dataLayerNull': 'notgiven', 'no': 'no', 'yes': 'yes', 'notgiven': 'notgiven'}}`. Nadat u de kaart op zijn plaats hebt, hebt u de optie om `inplace` als `True` of `False` te plaatsen. Stel `inplace` in als `True` of `False` op basis van of u transformatie wilt toepassen. Standaard wordt een nieuwe kolom gemaakt. `"inplace": False` Ondersteuning voor het opgeven van een nieuwe kolomnaam is ingesteld om in een volgende release te worden toegevoegd. De laatste regel `cols` kan een enkele kolomnaam of een lijst met kolommen zijn. Geef de kolommen op waarop u de transformatie wilt toepassen. In dit voorbeeld wordt `leasing` opgegeven. Voor meer informatie over de beschikbare knopen en hoe te om hen te gebruiken, bezoek [de gids van de knoopverwijzing](./node-reference.md).

```python
# Renaming leasing column using Pandas Node
leasing_mapper_node = Pandas(params={'import': 'map',
                                'kwargs': {'arg': {
                                    'dataLayerNull': 'notgiven', 
                                    'no': 'no', 
                                    'yes': 'yes', 
                                    'notgiven': 'notgiven'}},
                                'inplace': True,
                                'cols': 'leasing'})
```

### De DSL-grafiek maken

Als uw knooppunten zijn gemaakt, bestaat de volgende stap uit het koppelen van de knooppunten om een grafiek te maken.

Begin door van alle knopen een lijst te maken die een deel van de grafiek door een serie vormen.

```python
nodes = [json_df_node, 
        to_datetime_node,
        hour_node,
        dayofweek_node,
        age_fillna_node,
        carbrand_fillna_node,
        country_fillna_node,
        cartype_primary_nationality_km_fillna_node,
        carbrand_mapper_node,
        cartype_mapper_node,
        country_mapper_node,
        gender_mapper_node,
        leasing_mapper_node,
        age_to_int_node,
        age_bins_node,
        dummies_node, 
        onnx_node]
```

Sluit vervolgens de knooppunten aan op de randen. Elke tuple is een [!DNL Edge] verbinding.

>[!TIP]
>
> Aangezien de knopen lineair van elkaar afhankelijk zijn (elke knoop hangt van de output van vorige knoop af), kunt u verbindingen tot stand brengen gebruikend een eenvoudige het lijstbegrip van Python. Voeg uw eigen verbindingen toe als een knooppunt afhankelijk is van meerdere invoeren.

```python
edges = [(nodes[i], nodes[i+1]) for i in range(len(nodes)-1)]
```

Maak de grafiek wanneer uw knooppunten zijn verbonden. De onderstaande cel is verplicht en kan niet worden bewerkt of verwijderd.

```python
dsl = GraphBuilder.generate_dsl(nodes=nodes, edges=edges)
pprint(json.loads(dsl))
```

Na voltooiing, is een `edge` voorwerp teruggekeerd die elk van de knopen en de parameters bevatten die aan hen in kaart werden gebracht.

![edge return](../images/rtml/edge-return.png)

## Publiceren naar rand (hub)

>[!NOTE]
>
>Het leren van de machine in real time wordt tijdelijk opgesteld aan en beheerd door de Hub van Adobe Experience Platform. Voor meer details, bezoek de overzichtssectie op [Real-time het Leren van de Machine architectuur](./home.md#architecture).

Nu u een grafiek van DSL hebt gecreeerd, kunt u uw grafiek aan [!DNL Edge] opstellen.

>[!IMPORTANT]
>
>Publiceer niet vaak naar [!DNL Edge], dit kan de [!DNL Edge] knopen overladen. Het wordt niet aanbevolen hetzelfde model meerdere keren te publiceren.

```python
edge_utils = EdgeUtils()
(edge_location, service_id) = edge_utils.publish_to_edge(dsl=dsl)
print(f'Edge Location: {edge_location}')
print(f'Service ID: {service_id}')
```

### De DSL bijwerken en opnieuw publiceren naar Edge (optioneel)

Als u uw DSL niet hoeft bij te werken, kunt u naar [scoring](#scoring) gaan.

>[!NOTE]
>
>De volgende cellen zijn alleen vereist als u een bestaande DSL wilt bijwerken die naar Edge is gepubliceerd.

Uw modellen zullen zich waarschijnlijk blijven ontwikkelen. In plaats van een volledige nieuwe service te maken, is het mogelijk een bestaande service bij te werken met uw nieuwe model. U kunt een knooppunt definiëren dat u wilt bijwerken, er een nieuwe id aan toewijzen en vervolgens de nieuwe DSL opnieuw uploaden naar [!DNL Edge].

In het onderstaande voorbeeld wordt knooppunt 0 bijgewerkt met een nieuwe id.

```python
# Update the id of Node 0 with a random uuid.

dsl_dict = json.loads(dsl)
print(f"ID of Node 0 in current DSL: {dsl_dict['edge']['applicationDsl']['nodes'][0]['id']}")

new_node_id = str(uuid.uuid4())
print(f'Updated Node ID: {new_node_id}')

dsl_dict['edge']['applicationDsl']['nodes'][0]['id'] = new_node_id
```

![Bijgewerkt knooppunt](../images/rtml/updated-node.png)

Na het bijwerken van knoopidentiteitskaart, kunt u een bijgewerkte DSL aan de Rand opnieuw publiceren.

```python
# Republish the updated DSL to Edge
(edge_location_ret, service_id, updated_dsl) = edge_utils.update_deployment(dsl=json.dumps(dsl_dict), service_id=service_id)
print(f'Updated dsl: {updated_dsl}')
```

U bent teruggekeerd bijgewerkte DSL.

![Bijgewerkte DSL](../images/rtml/updated-dsl.png)

## Scores {#scoring}

Na publicatie naar [!DNL Edge] wordt het scoren uitgevoerd door een POST-aanvraag van een client. Dit kan doorgaans worden gedaan vanuit een clienttoepassing waarvoor XML-scores vereist zijn. Je kunt het ook van Postman doen. Het **[!UICONTROL Real-time ML]** malplaatje gebruikt EdgeUtils om dit proces aan te tonen.

>[!NOTE]
>
>Er is een kleine verwerkingstijd vereist voordat het scoren begint.

```python
# Wait for the app to come up
import time
time.sleep(20)
```

Met hetzelfde schema dat in de training werd gebruikt, worden voorbeeldgegevens voor het bijhouden van de score gegenereerd. Deze gegevens worden gebruikt om een dataframe voor scoring te maken en vervolgens om te zetten in een scorewoordenboek. Gelieve te bekijken *Real-time ML* malplaatje voor de volledige codecel.

![Scoregegevens](../images/rtml/generate-score-data.png)

### Score tegen het eindpunt van de Rand

Gebruik de volgende cel binnen *Real-time ML* malplaatje aan score tegen uw [!DNL Edge] dienst.

![Score tegen rand](../images/rtml/scoring-edge.png)

Wanneer de scoring is voltooid, worden de [!DNL Edge] URL, Payload en de gescorde uitvoer van [!DNL Edge] geretourneerd.

## Geef uw geïmplementeerde apps weer vanuit de [!DNL Edge]

Als u een lijst wilt genereren van uw momenteel geïmplementeerde apps op de [!DNL Edge], voert u de volgende codecel uit. Deze cel kan niet worden bewerkt of verwijderd.

```python
services = edge_utils.list_deployed_services()
print(services)
```

De teruggekeerde reactie is een serie van uw opgestelde diensten.

```json
[
    {
        "created": "2020-05-25T19:18:52.731Z",
        "deprecated": false,
        "id": "40eq76c0-1c6f-427a-8f8f-54y9cdf041b7",
        "type": "edge",
        "updated": "2020-05-25T19:18:52.731Z"
    }
]
```

## Een geïmplementeerde app of service-id verwijderen uit [!DNL Edge] (optioneel)

>[!CAUTION]
>
>Deze cel wordt gebruikt om uw geïmplementeerde Edge-toepassing te verwijderen. Gebruik de volgende cel alleen als u een geïmplementeerde [!DNL Edge]-toepassing moet verwijderen.

```python
if edge_utils.delete_from_edge(service_id=service_id):
    print(f"Deleted service id {service_id} successfully")
else:
    print(f"Failed to delete service id {service_id}")
```

## Volgende stappen

Door de bovenstaande zelfstudie te volgen, hebt u een ONNX-model getraind en geüpload naar de modelwinkel voor het leren van machines in realtime. Bovendien, hebt u uw in real time het Leren model van de Machine gescoord en opgesteld. Als u meer over de knopen beschikbaar voor modelontwerp wilt leren, bezoek [de gids van de knoopverwijzing](./node-reference.md).