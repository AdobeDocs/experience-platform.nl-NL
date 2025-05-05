---
keywords: Experience Platform;ontwikkelaarshandleiding;Data Science Workspace;populaire onderwerpen;Real-time machine learning;node reference;
solution: Experience Platform
title: Real-time machine learning-laptops beheren
description: In de volgende handleiding worden de stappen beschreven die nodig zijn om een Real-Time Machine Learning-toepassing te maken in Adobe Experience Platform JupyterLab.
exl-id: 604c4739-5a07-4b5a-b3b4-a46fd69e3aeb
source-git-commit: 923c6f2deb4d1199cfc5dc9dc4ca7b4da154aaaa
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 0%

---

# Real-time Machine Learning-laptops beheren (Alpha)

>[!NOTE]
>
>Data Science Workspace kan niet meer worden aangeschaft.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

>[!IMPORTANT]
>
>Het leren van de machine in real time is niet beschikbaar aan alle gebruikers nog. Deze functie bevindt zich in alfa en wordt nog steeds getest. Dit document kan worden gewijzigd.

In de volgende handleiding worden de stappen beschreven die nodig zijn om een toepassing voor het leren van machines in realtime te bouwen. Deze handleiding, die gebruikmaakt van de Adobe **[!UICONTROL Real-time ML]** Python-laptopsjabloon, omvat de training van een model, het maken van een DSL, het publiceren van DSL naar Edge en het scoren van de aanvraag. Aangezien u door het uitvoeren van uw het Leren model van de machine in real time vordert, wordt verwacht dat u het malplaatje wijzigt om de behoeften van uw dataset te passen.

## Een laptop voor real-time leren van machines maken

In Adobe Experience Platform UI, selecteer **[!UICONTROL Notebooks]** van binnen **Wetenschap van Gegevens**. Selecteer vervolgens **[!UICONTROL JupyterLab]** en laat de omgeving wat tijd om te laden.

![ open JupyterLab ](../images/rtml/open-jupyterlab.png)

De [!DNL JupyterLab] -startprogramma wordt weergegeven. De rol neer aan *het Leren van de machine in real time* en selecteert de **[!UICONTROL Real-time ML]** notitieboekje. Er wordt een sjabloon geopend met voorbeelden van notebookcellen met een voorbeeldgegevensset.

![ lege python ](../images/rtml/authoring-notebook.png)

## Knooppunten importeren en ontdekken

Begin door alle vereiste pakketten voor uw model in te voeren. Zorg ervoor om het even welk pakket u op het gebruiken voor knoop creatie van plan bent wordt ingevoerd.

>[!NOTE]
>
>De lijst met geïmporteerde producten kan afwijken, afhankelijk van het model dat u wilt maken. Deze lijst zal veranderen aangezien de nieuwe knopen in tijd worden toegevoegd. Gelieve te verwijzen naar de [ gids van de knoopverwijzing ](./node-reference.md) voor een volledige lijst van beschikbare knopen.

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

![ lijst van nota&#39;s ](../images/rtml/node-list.png)

## Een real-time leren van machines trainen

Als u een van de volgende opties gebruikt, schrijft u [!DNL Python] -code voor het lezen, verwerken en analyseren van gegevens. Daarna, moet u uw eigen model van XML trainen, het in formaat rangschikken ONNX en dan uploadt het aan het Leren modelopslag van de machine in real time.

- [Uw eigen model trainen in JupyterLab-laptops](#training-your-own-model)
- [Uw eigen vooraf getrainde ONNX-model uploaden naar JupyterLab-laptops](#pre-trained-model-upload)

### Uw eigen model trainen {#training-your-own-model}

Begin met het laden van uw trainingsgegevens.

>[!NOTE]
>
>In het **Real-time ML** malplaatje, wordt de [ dataset van de autoverzekering CSV ](https://github.com/adobe/experience-platform-dsw-reference/tree/master/datasets/insurance) gegrabbed van [!DNL Github].

![ Laad opleidingsgegevens ](../images/rtml/load_training.png)

Als u een gegevensset wilt gebruiken vanuit Adobe Experience Platform, verwijdert u de commentaarmarkering uit de onderstaande cel. Vervolgens moet u `DATASET_ID` vervangen door de juiste waarde.

![ rtml dataset ](../images/rtml/rtml-dataset.png)

Om tot een dataset in uw [!DNL JupyterLab] notitieboekje toegang te hebben, selecteer het **lusje van Gegevens** in de linkernavigatie van [!DNL JupyterLab]. De mappen **[!UICONTROL Datasets]** en **[!UICONTROL Schemas]** worden weergegeven. Selecteer **[!UICONTROL Datasets]** en klik met de rechtermuisknop en selecteer vervolgens de optie **[!UICONTROL Explore Data in Notebook]** in het vervolgkeuzemenu in de gegevensset die u wilt gebruiken. Onder aan de laptop wordt een uitvoerbaar code-item weergegeven. Deze cel heeft uw `dataset_id` .

{de toegang van 0} dataset ![&#128279;](../images/rtml/access-dataset.png)

Klik met de rechtermuisknop en verwijder de cel die u onder aan de laptop hebt gegenereerd.

### Trainingseigenschappen

Wijzig met behulp van de meegeleverde sjabloon een van de trainingseigenschappen in `config_properties` .

```python
config_properties = {
    "train_records_limit":1000000,
    "n_estimators": "80",
    "max_depth": "5",
    "ten_id": "_experienceplatform"  
}
```

### Uw model voorbereiden

Met de sjabloon van **[!UICONTROL Real-time ML]** moet u uw XML-model analyseren, vooraf verwerken, trainen en evalueren. Dit gebeurt door datatransformaties toe te passen en een trainingspijplijn te bouwen.

**transformaties van Gegevens**

De **[!UICONTROL Real-time ML]** malplaatjes **cel van de Transformaties van Gegevens** moet worden gewijzigd om met uw eigen dataset te werken. Meestal gaat het om het wijzigen van de naam van kolommen, gegevensrollup en gegevensvoorbereiding/functietechniek.

>[!NOTE]
>
>Het volgende voorbeeld is versmald ten behoeve van leesbaarheid met `[ ... ]` . Gelieve te bekijken en uit te breiden *in real time de sectie van XML* malplaatjegegevens transformaties voor de volledige codecel.

```python
df1.rename(columns = {config_properties['ten_id']+'.identification.ecid': 'ecid',
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

df1['city'] = df1.groupby('country')['city'].transform(lambda x: x.fillna(x.mode()))
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

Voer de opgegeven cel uit om een voorbeeldresultaat te zien. De outputlijst die van de `carinsurancedataset.csv` dataset is teruggekeerd keert de wijzigingen terug u bepaalde.

![ Voorbeeld van gegevenstransformaties ](../images/rtml/table-return.png)

**de pijpleiding van 0&rbrace; Opleiding**

Daarna moet u de trainingspijpleiding tot stand brengen. Dit zal gelijkaardig aan een ander dossier van de trainingspijpleiding kijken behalve u moet omzetten en een ONNX dossier produceren.

Wijzig de sjabloon met de gegevenstransformaties die in de vorige cel zijn gedefinieerd. De volgende hieronder benadrukte code wordt gebruikt voor het produceren van een ONNX- dossier in uw eigenschappijpleiding. Gelieve te bekijken het *in real time ML* malplaatje voor de volledige cel van de pijpleidingscode.

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
>Wijzig de `model_path` tekenreekswaarde ( `model.onnx` ) om de naam van het model te wijzigen.

```python
model_path = "model.onnx"
```

>[!NOTE]
>
>De volgende cel kan niet worden bewerkt of kan worden verwijderd en is vereist voor het werken van uw Real-time Machine Learning-toepassing.

```python
model = ModelUpload(params={'model_path': model_path})
msg_model = model.process(None, 1)
model_id = msg_model.model['model_id']
 
print("Model ID: ", model_id)
```

![ ONNX model ](../images/rtml/onnx-model-rail.png)

### Uw eigen vooraf getrainde ONNX-model uploaden {#pre-trained-model-upload}

Met de uploadknop in [!DNL JupyterLab] -laptops kunt u uw vooraf getrainde ONNX-model uploaden naar de omgeving van de [!DNL Data Science Workspace] -laptops.

![ uploadpictogram ](../images/rtml/upload.png)

Daarna, verander de `model_path` koordwaarde in *in real time ML* notitieboekje om uw ONNX modelnaam aan te passen. Zodra volledig, stel de *reeks modelweg* in werking en stel dan *in werking uploadt uw model aan RTML ModelCel van de Opslag*. Uw modellocatie en model-id worden beide geretourneerd in de reactie als de bewerking succesvol was.

![ uploadend eigen model ](../images/rtml/upload-own-model.png)

## Maken van domeinspecifieke taal (DSL)

Deze sectie schetst het creëren van een DSL. U gaat de knooppunten ontwerpen die een voorbehandeling van gegevens samen met het ONNX-knooppunt bevatten. Vervolgens wordt een DSL-grafiek gemaakt met knooppunten en randen. Randen verbinden knooppunten met behulp van een op twee gebaseerde indeling (node_1, node_2). De grafiek moet geen cycli hebben.

>[!IMPORTANT]
>
>Het gebruik van het ONNX-knooppunt is verplicht. Zonder het ONNX-knooppunt is de toepassing mislukt.

### Node authoring

>[!NOTE]
>
> U hebt waarschijnlijk meerdere knooppunten op basis van het type gegevens dat wordt gebruikt. Het volgende voorbeeld schetst slechts één enkele knoop in het *in real time ML* malplaatje. Gelieve te bekijken de *malplaatjes* Authoring van de Knoop *sectie in real time van XML &lbrace;voor de volledige codecel.*

Het onderstaande Pandas-knooppunt gebruikt `"import": "map"` om de methodenaam als een tekenreeks in de parameters te importeren, gevolgd door het invoeren van de parameters als een kaartfunctie. In het onderstaande voorbeeld wordt dit gedaan met `{'arg': {'dataLayerNull': 'notgiven', 'no': 'no', 'yes': 'yes', 'notgiven': 'notgiven'}}` . Nadat u de kaart hebt geplaatst, kunt u `inplace` instellen als `True` of `False` . Stel `inplace` in als `True` of `False` op basis van of u transformatie wilt toepassen. Standaard maakt `"inplace": False` een nieuwe kolom. Ondersteuning voor het opgeven van een nieuwe kolomnaam is ingesteld om in een volgende release te worden toegevoegd. De laatste regel `cols` kan één kolomnaam of een lijst met kolommen zijn. Geef de kolommen op waarop u de transformatie wilt toepassen. In dit voorbeeld wordt `leasing` opgegeven. Voor meer informatie over de beschikbare knopen en hoe te om hen te gebruiken, bezoek de [ gids van de knoopverwijzing ](./node-reference.md).

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

Sluit vervolgens de knooppunten aan op de randen. Elke tuple is een [!DNL Edge] -verbinding.

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

Wanneer de bewerking is voltooid, wordt een `edge` -object geretourneerd dat elk van de knooppunten en de parameters bevat die eraan zijn toegewezen.

![ randterugkeer ](../images/rtml/edge-return.png)

## Publish naar Edge (Hub)

>[!NOTE]
>
>Het leren van de machine in real time wordt tijdelijk opgesteld aan en beheerd door de Hub van Adobe Experience Platform. Voor extra details, bezoek de overzichtssectie op [ in real time het Leren van de Machine architectuur ](./home.md#architecture).

Nu u een DSL-grafiek hebt gemaakt, kunt u de grafiek implementeren in de [!DNL Edge] .

>[!IMPORTANT]
>
>Publiceer niet vaak naar [!DNL Edge] , waardoor de knooppunten van [!DNL Edge] worden overbelast. Het wordt niet aanbevolen hetzelfde model meerdere keren te publiceren.

```python
edge_utils = EdgeUtils()
(edge_location, service_id) = edge_utils.publish_to_edge(dsl=dsl)
print(f'Edge Location: {edge_location}')
print(f'Service ID: {service_id}')
```

### DSL bijwerken en opnieuw publiceren naar Edge (optioneel)

Als u uw DSL niet moet bijwerken, kunt u aan [ het scoren ](#scoring) overslaan.

>[!NOTE]
>
>De volgende cellen zijn alleen vereist als u een bestaande DSL wilt bijwerken die naar Edge is gepubliceerd.

Uw modellen zullen zich waarschijnlijk blijven ontwikkelen. In plaats van een volledige nieuwe service te maken, is het mogelijk een bestaande service bij te werken met uw nieuwe model. U kunt een knooppunt definiëren dat u wilt bijwerken, er een nieuwe id aan toewijzen en vervolgens de nieuwe DSL opnieuw uploaden naar de [!DNL Edge] .

In het onderstaande voorbeeld wordt knooppunt 0 bijgewerkt met een nieuwe id.

```python
# Update the id of Node 0 with a random uuid.

dsl_dict = json.loads(dsl)
print(f"ID of Node 0 in current DSL: {dsl_dict['edge']['applicationDsl']['nodes'][0]['id']}")

new_node_id = str(uuid.uuid4())
print(f'Updated Node ID: {new_node_id}')

dsl_dict['edge']['applicationDsl']['nodes'][0]['id'] = new_node_id
```

![ Bijgewerkte knoop ](../images/rtml/updated-node.png)

Na het bijwerken van knoopidentiteitskaart, kunt u een bijgewerkte DSL aan Edge opnieuw publiceren.

```python
# Republish the updated DSL to Edge
(edge_location_ret, service_id, updated_dsl) = edge_utils.update_deployment(dsl=json.dumps(dsl_dict), service_id=service_id)
print(f'Updated dsl: {updated_dsl}')
```

U bent teruggekeerd bijgewerkte DSL.

![ Bijgewerkte DSL ](../images/rtml/updated-dsl.png)

## Scores {#scoring}

Na publicatie naar [!DNL Edge] wordt de scoring uitgevoerd door een POST-aanvraag van een client. Dit kan doorgaans worden gedaan vanuit een clienttoepassing waarvoor XML-scores vereist zijn. Je kunt het ook vanuit Postman doen. De sjabloon **[!UICONTROL Real-time ML]** gebruikt EdgeUtils om dit proces te demonstreren.

>[!NOTE]
>
>Er is een kleine verwerkingstijd vereist voordat het scoren begint.

```python
# Wait for the app to come up
import time
time.sleep(20)
```

Met hetzelfde schema dat in de training werd gebruikt, worden voorbeeldgegevens voor het bijhouden van de score gegenereerd. Deze gegevens worden gebruikt om een dataframe voor scoring te maken en vervolgens om te zetten in een scorewoordenboek. Gelieve te bekijken het *in real time ML* malplaatje voor de volledige codecel.

![ het Scoren gegevens ](../images/rtml/generate-score-data.png)

### Score tegen het Edge-eindpunt

Gebruik de volgende cel binnen het *malplaatje in real time van XML* aan score tegen uw [!DNL Edge] dienst.

![ Score tegen rand ](../images/rtml/scoring-edge.png)

Wanneer de scoring is voltooid, worden de uitvoer van [!DNL Edge] URL, Payload en scored uit de [!DNL Edge] geretourneerd.

## Maak een lijst met uw geïmplementeerde apps vanuit de [!DNL Edge]

Als u een lijst wilt genereren met de apps die u op dat moment in de [!DNL Edge] gebruikt, voert u de volgende codecel uit. Deze cel kan niet worden bewerkt of verwijderd.

```python
services = edge_utils.list_deployed_services()
print(services)
```

De geretourneerde reactie is een array van uw geïmplementeerde services.

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

## Een geïmplementeerde app of service-id verwijderen uit de [!DNL Edge] (optioneel)

>[!CAUTION]
>
>Deze cel wordt gebruikt om uw geïmplementeerde Edge-toepassing te verwijderen. Gebruik de volgende cel niet tenzij u een geïmplementeerde [!DNL Edge] -toepassing moet verwijderen.

```python
if edge_utils.delete_from_edge(service_id=service_id):
    print(f"Deleted service id {service_id} successfully")
else:
    print(f"Failed to delete service id {service_id}")
```

## Volgende stappen

Door de bovenstaande zelfstudie te volgen, hebt u een ONNX-model getraind en geüpload naar de real-time Machine Learning Modelstore. Bovendien, hebt u uw in real time het Leren model van de Machine gescoord en opgesteld. Als u wenst om meer over de knopen beschikbaar voor model creatie te leren, bezoek de [ gids van de knoopverwijzing ](./node-reference.md).
