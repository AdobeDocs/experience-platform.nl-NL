---
title: Een volheidsscore bepalen met behulp van een door een machine gegenereerd voorspellend model voor leren
description: Leer hoe u Query Service gebruikt om uw voorspellend model toe te passen op Experience Platform-gegevens. In dit document wordt uitgelegd hoe u Experience Platform-gegevens kunt gebruiken om te voorspellen of een klant bij elk bezoek geneigd is om producten te kopen.
exl-id: 29587541-50dd-405c-bc18-17947b8a5942
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 0%

---

# Bepaal een aandrijvingsscore gebruikend een machine-leren-Gegenereerd vooruitgangsmodel

Met de Query Service kunt u voorspellende modellen, zoals proxyscores, gebruiken die op uw computerleerplatform zijn gebaseerd om Experience Platform-gegevens te analyseren.

In deze handleiding wordt uitgelegd hoe u de Query-service kunt gebruiken om gegevens naar uw computerplatform te verzenden om een model op te leiden in een computerlaptop. Het opgeleide model kan op gegevens worden toegepast gebruikend SQL om de neiging van een klant te voorspellen om voor elk bezoek te kopen.

## Aan de slag

Als onderdeel van dit proces moet u een model voor machinaal leren trainen, wordt in dit document uitgegaan van een praktische kennis van een of meer computerleeromgevingen.

In dit voorbeeld wordt [!DNL Jupyter Notebook] gebruikt als een ontwikkelomgeving. Hoewel er veel opties beschikbaar zijn, wordt [!DNL Jupyter Notebook] aanbevolen omdat het een opensource webtoepassing is die lage computervereisten heeft. Het kan [ van de officiële plaats ](https://jupyter.org/) worden gedownload.

Als u dit nog niet hebt gedaan, volg de stappen [  [!DNL Jupyter Notebook]  met de Dienst van de Vraag van Adobe Experience Platform ](../clients/jupyter-notebook.md) verbinden alvorens met deze gids verder te gaan.

De bibliotheken die in dit voorbeeld worden gebruikt, zijn:

```console
python=3.6.7
psycopg2
sklearn
pandas
matplotlib
numpy
tqdm
```

## Analytische tabellen importeren van Experience Platform naar [!DNL Jupyter Notebook] {#import-analytics-tables}

Als u een model met de dichtheid wilt genereren, moet u een projectie van de analysegegevens die in Experience Platform zijn opgeslagen, importeren in [!DNL Jupyter Notebook] . Van een [!DNL Python] 3 [!DNL Jupyter Notebook] verbonden met de Dienst van de Vraag, voert de volgende bevelen een dataset van het klantengedrag van Luma, een fictieve kledingopslag in. Aangezien Experience Platform-gegevens worden opgeslagen met de XDM-indeling (Experience Data Model), moet een JSON-voorbeeldobject worden gegenereerd dat voldoet aan de structuur van het schema. Zie de documentatie voor instructies op hoe te [ het voorwerp van steekproefJSON ](../../xdm/ui/sample.md) produceren.

![ het [!DNL Jupyter Notebook] dashboard met verscheidene benadrukte bevelen.](../images/use-cases/jupyter-commands.png)

De uitvoer geeft een tabellarische weergave weer van alle kolommen in de gedragsgegevensset van Luma binnen het dashboard van [!DNL Jupyter Notebook] .

![ de in tabelvorm gebrachte output van de ingevoerde dataset van het klantengedrag van Luma binnen [!DNL Jupyter Notebook].](../images/use-cases/behavioural-dataset-results.png)

## Gegevens voorbereiden voor leren van computers {#prepare-data-for-machine-learning}

Een doelkolom moet worden geïdentificeerd om een model voor machinaal leren op te leiden. Aangezien de neiging om te kopen het doel voor dit gebruiksgeval is, wordt de `analytic_action` kolom gekozen als doelkolom van de resultaten van de Luma. De waarde `productPurchase` is de indicator van een klantenaankoop. De kolommen `purchase_value` en `purchase_num` worden ook verwijderd omdat ze rechtstreeks verband houden met de actie voor het aanschaffen van het product.

De opdrachten voor het uitvoeren van deze acties zijn als volgt:

```python
#define the target label for prediction
df['target'] = (df['analytic_action'] == 'productPurchase').astype(int)
#remove columns that are dependent on the label
df.drop(['analytic_action','purchase_value'],axis=1,inplace=True)
```

Daarna, moeten de gegevens van de dataset van de Luma in aangewezen vertegenwoordiging worden omgezet. Er zijn twee stappen vereist:

1. Transformeer de kolommen die getallen vertegenwoordigen in numerieke kolommen. Om dit te doen zet uitdrukkelijk het gegevenstype in `dataframe` om.
1. U kunt categorische kolommen ook transformeren in numerieke kolommen.

```python
#convert columns that represent numbers
num_cols = ['purchase_num', 'value_cart', 'value_lifetime']
df[num_cols] = df[num_cols].apply(pd.to_numeric, errors='coerce')
```

Een techniek genoemd *één heet het coderen* wordt gebruikt om de categoriale gegevensvariabelen voor gebruik met machine en diepe het leren algoritmen om te zetten. Dit verbetert op zijn beurt de voorspellingen en de classificatienauwkeurigheid van een model. Gebruik de `Sklearn` -bibliotheek om elke categorische waarde in een aparte kolom te vertegenwoordigen.

```python
from sklearn.preprocessing import OneHotEncoder

#get the categorical columns
cat_columns = list(set(df.columns) - set(num_cols + ['target']))

#get the dataframe with categorical columns only
df_cat = df.loc[:,cat_columns]

#initialize sklearn's OneHotEncoder
enc = OneHotEncoder(handle_unknown='ignore')

#fit the data into the encoder
enc.fit(df_cat)

#define OneHotEncoder's columns names
ohc_columns = [[c+'='+c_ for c_ in cat] for c,cat in zip(cat_columns,enc.categories_)]
ohc_columns = [item for sublist in ohc_columns for item in sublist]

#finalize the data input to the ML models
X = pd.DataFrame( np.concatenate((enc.transform(df_cat).toarray(),df[num_cols]),axis=1),
                 columns =  ohc_columns + num_cols)

#define target column
y = df['target']
```

De gegevens die als `X` worden gedefinieerd, worden als volgt in tabelvorm weergegeven:

![ de in tabelvorm gebrachte output van X binnen [!DNL Jupyter Notebook].](../images/use-cases/x-output-table.png)


Nu de benodigde gegevens voor machinetlering beschikbaar zijn, kunnen de vooraf geconfigureerde modellen voor machinetlering in de [!DNL Python] `sklearn` -bibliotheek worden geplaatst. [!DNL Logistics Regression] wordt gebruikt om het aandrijfmodel op te leiden en geeft u de nauwkeurigheid van de testgegevens weer. In dit geval is het ongeveer 85%.

Het algoritme [!DNL Logistic Regression] en de splitsingsmethode voor treintests, die worden gebruikt om de prestaties van machinaal leeralgoritmen te ramen, worden in het onderstaande codeblok geïmporteerd:

```python
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.33, random_state=42)

clf = LogisticRegression(max_iter=2000, random_state=0).fit(X_train, y_train)

print("Test data accuracy: {}".format(clf.score(X_test, y_test)))
```

De nauwkeurigheid van de testgegevens is 0,8518518518518519.

Door het gebruik van Logistics Regression, kunt u de redenen voor een aankoop visualiseren en de eigenschappen sorteren die macht door hun gerangschikte belang in dalende orden bepalen. De eerste kolommen geven een hoger oorzakelijk verband aan dat tot het aankoopgedrag leidt. De laatste kolommen geven factoren aan die niet tot aankoopgedrag leiden.

De code voor het visualiseren van de resultaten als twee staafdiagrammen ziet er als volgt uit:

```python
from matplotlib import pyplot as plt

#get feature importance as a sorted list of columns
feature_importance = np.argsort(-clf.coef_[0])
top_10_features_purchase_names = X.columns[feature_importance[:10]]
top_10_features_purchase_values = clf.coef_[0][feature_importance[:10]]
top_10_features_not_purchase_names = X.columns[feature_importance[-10:]]
top_10_features_not_purchase_values = clf.coef_[0][feature_importance[-10:]]

#plot the figures
fig, (ax1, ax2) = plt.subplots(1, 2,figsize=(10,5))

ax1.bar(np.arange(10),top_10_features_purchase_values)
ax1.set_xticks(np.arange(10))
ax1.set_xticklabels(top_10_features_purchase_names,rotation = 90)
ax1.set_ylim([np.min(clf.coef_[0])-0.1,np.max(clf.coef_[0])+0.1])
ax1.set_title("Top 10 features to define \n a propensity to purchase")

ax2.bar(np.arange(10),top_10_features_not_purchase_values, color='#E15750')
ax2.set_xticks(np.arange(10))
ax2.set_xticklabels(top_10_features_not_purchase_names,rotation = 90)
ax2.set_ylim([np.min(clf.coef_[0])-0.1,np.max(clf.coef_[0])+0.1])
ax2.set_title("Top 10 features to define \n a propensity to NOT purchase")

plt.show()
```

Hieronder ziet u een verticale visualisatie van de resultaten in het staafdiagram:

![ de visualisatie van top 10 eigenschappen die een neiging om al dan niet te kopen bepalen te kopen.](../images/use-cases/visualized-results.png)

Uit het staafdiagram kunnen verschillende patronen worden afgeleid. De onderwerpen van het verkooppunt (POS) en van de Vraag van het kanaal als terugbetaling zijn de belangrijkste factoren die een aankoopgedrag bepalen. Terwijl de onderwerpen van de Vraag als klachten en facturen belangrijke rollen zijn om het niet het kopen gedrag te bepalen. Dit zijn kwantificeerbare, activeerbare inzichten die marketeers kunnen gebruiken om marketingcampagnes te voeren om de neiging tot aankoop van deze klanten aan te pakken.

## De Dienst van de Vraag van het gebruik om het getrainde model toe te passen {#use-query-service-to-apply-trained-model}

Nadat het getrainde model is gemaakt, moet het worden toegepast op de gegevens in Experience Platform. Om dit te doen, moet de logica van de machine het leren pijpleiding in SQL worden omgezet. De twee belangrijkste onderdelen van deze overgang zijn:

- Ten eerste moet SQL de module [!DNL Logistics Regression] vervangen om de waarschijnlijkheid van een voorspellingslabel te verkrijgen. Het model dat door Logistics Regression is gemaakt, heeft het regressiemodel `y = wX + c` opgeleverd, waarbij de gewichten `w` en intercept `c` de uitvoer van het model zijn. SQL-functies kunnen worden gebruikt om de gewichten te vermenigvuldigen om een waarschijnlijkheid te verkrijgen.

- Ten tweede moet het engineeringproces dat in [!DNL Python] met één hot encoding wordt uitgevoerd, ook in SQL worden opgenomen. In de oorspronkelijke database hebben we bijvoorbeeld `geo_county` -kolom om het land op te slaan, maar de kolom wordt omgezet in `geo_county=Bexar` , `geo_county=Dallas` , `geo_county=DeKalb` . De volgende SQL-instructie voert dezelfde transformatie uit, waarbij `w1` , `w2` en `w3` kunnen worden vervangen door de dikten die in [!DNL Python] uit het model zijn geleerd:

```sql
SELECT  CASE WHEN geo_state = 'Bexar' THEN FLOAT(w1) ELSE 0 END AS f1,
        CASE WHEN geo_state = 'Dallas' THEN FLOAT(w2) ELSE 0 END AS f2,
        CASE WHEN geo_state = 'Bexar' THEN FLOAT(w3) ELSE 0 END AS f3,
```

Voor numerieke functies kunt u de kolommen rechtstreeks vermenigvuldigen met de gewichten, zoals in de SQL-instructie hieronder wordt getoond.

```sql
SELECT FLOAT(purchase_num) * FLOAT(w4) AS f4,
```

Nadat de aantallen zijn verkregen, kunnen zij aan een sigmoïdfunctie worden overgebracht waar het Logistics Regression algoritme de definitieve voorspellingen veroorzaakt. In de onderstaande instructie is `intercept` het nummer van de onderschepping in de regressie.
        

```sql
SELECT CASE WHEN 1 / (1 + EXP(- (f1 + f2 + f3 + f4 + FLOAT(intercept)))) > 0.5 THEN 1 ELSE 0 END AS Prediction;
```

 

### Een voorbeeld van begin tot eind

Wanneer u twee kolommen hebt (`c1` en `c2` ) en `c1` twee categorieën heeft, wordt het algoritme [!DNL Logistic Regression] getraind met de volgende functie:
 

```python
y = 0.1 * "c1=category 1"+ 0.2 * "c1=category 2" +0.3 * c2+0.4
```

 
Het equivalent in SQL is als volgt:

```sql
SELECT
  CASE WHEN 1 / (1 + EXP(- (f1 + f2 + f3 + FLOAT(0.4)))) > 0.5 THEN 1 ELSE 0 END AS Prediction
FROM
  (
    SELECT
      CASE WHEN c1 = 'Cateogry 1' THEN FLOAT(0.1) ELSE 0 END AS f1,
      CASE WHEN c1 = 'Cateogry 2' THEN FLOAT(0.2) ELSE 0 END AS f2,
      FLOAT(c2) * FLOAT(0.3) AS f3
    FROM TABLE
  )
```

 
De code van [!DNL Python] om het vertaalproces te automatiseren is als volgt:

```python
def generate_lr_inference_sql(ohc_columns, num_cols, clf, db):
    features_sql = []
    category_sql_text = "case when {col} = '{val}' then float({coef}) else 0 end as f{name}"
    numerical_sql_text = "float({col}) * float({coef}) as f{name}"
    for i, (column, coef) in enumerate(zip(ohc_columns+num_cols, clf.coef_[0])):
        if i < len(ohc_columns):
            col,val = column.split('=')
            val = val.replace("'","%''%")
            sql = category_sql_text.format(col=col,val=val,coef=coef,name=i+1)
        else:
            sql = numerical_sql_text.format(col=column,coef=coef,name=i+1)
        features_sql.append(sql)
    features_sum = '+'.join(['f{}'.format(i) for i in range(1,len(features_sql)+1)])
    final_sql = '''
    select case when 1/(1 + EXP(-({features} + float({intercept})))) > 0.5 then 1 else 0 end as Prediction
    from
        (select {cols}
        from {db})
    '''.format(features=features_sum,cols=",".join(features_sql),intercept=clf.intercept_[0],db=db)
    return final_sql
```

Wanneer SQL wordt gebruikt om het gegevensbestand af te leiden, is de output als volgt:

```python
sql = generate_lr_inference_sql(ohc_columns, num_cols, clf, "fdu_luma_raw")
cur.execute(sql)    
samples = [r for r in cur]
colnames = [desc[0] for desc in cur.description]
pd.DataFrame(samples,columns=colnames)
```

De resultaten met tabularisering geven de neiging aan om te kopen voor elke klantsessie met `0` wat betekent dat er geen koopneiging is en `1` wat een bevestigde koopneiging betekent.

![ de in tabelvorm gemaakte resultaten van de gegevensbestandinvloed die SQL gebruiken.](../images/use-cases/inference-results.png)

## Werken met gesamplede gegevens: Bootstrapping {#working-on-sampled-data}

Als de gegevensgrootte te groot is voor uw lokale computer om de gegevens voor modeltraining op te slaan, kunt u monsters nemen in plaats van de volledige gegevens van de Query Service. Om te weten hoeveel gegevens aan steekproef van de Dienst van de Vraag nodig zijn, kunt u een techniek toepassen genoemd bootstrapping. In dit verband betekent bootstrapping dat het model meerdere keren met verschillende monsters wordt opgeleid en dat de variantie van de nauwkeurigheid van het model tussen de verschillende monsters wordt gecontroleerd. Als u het bovenstaande voorbeeld van het aandrijfmodel wilt aanpassen, moet u eerst de gehele werkstroom voor machinaal leren inkapselen in een functie. De code ziet er als volgt uit:

```python
def end_to_end_pipeline(df):
    
    #define the target label for prediction
    df['target'] = (df['analytic_action'] == 'productPurchase').astype(int)
    #remove columns that are dependent on the label
    df.drop(['analytic_action','purchase_value'],axis=1,inplace=True)
    
    num_cols = ['purchase_num','value_cart','value_lifetime']
    df[num_cols] = df[num_cols].apply(pd.to_numeric, errors='coerce')
    
    #get the categorical columns
    cat_columns = list(set(df.columns) - set(num_cols + ['target']))

    #get the dataframe with categorical columns only
    df_cat = df.loc[:,cat_columns]

    #initialize sklearn's One Hot Encoder
    enc = OneHotEncoder(handle_unknown='ignore')

    #fit the data into the encoder
    enc.fit(df_cat)

    #define one hot encoder's columns names
    ohc_columns = [[c+'='+c_ for c_ in cat] for c,cat in zip(cat_columns,enc.categories_)]
    ohc_columns = [item for sublist in ohc_columns for item in sublist]

    #finalize the data input to the ML models
    X = pd.DataFrame( np.concatenate((enc.transform(df_cat).toarray(),df[num_cols]),axis=1),
                     columns =  ohc_columns + num_cols)

    #define target column
    y = df['target']
    
    X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.33, random_state=42)

    clf = LogisticRegression(max_iter=2000,random_state=0).fit(X_train, y_train)

    return clf.score(X_test, y_test)
```

Deze functie kan vervolgens meerdere keren in een lus worden uitgevoerd, bijvoorbeeld tien keer. Het verschil met de vorige code is dat het voorbeeld nu niet uit de hele tabel wordt genomen, maar alleen uit een voorbeeld van rijen. De voorbeeldcode hieronder neemt bijvoorbeeld slechts 1000 rijen. De nauwkeurigheden voor elke herhaling kunnen worden opgeslagen.

```python
from tqdm import tqdm

bootstrap_accuracy = []
for i in tqdm(range(100)):
    
    #sample data from QS
    cur.execute('''SELECT *
    FROM fdu_luma_raw
    ORDER BY random()
    LIMIT 1000
    ''')    
    samples = [r for r in cur]
    colnames = [desc[0] for desc in cur.description]
    df_samples = pd.DataFrame(samples,columns=colnames)
    df_samples.fillna(0,inplace=True)
    
    #train the propensity model with sampled data and output its accuracy
    bootstrap_accuracy.append(end_to_end_pipeline(df_samples))
    
bootstrap_accuracy = np.sort(bootstrap_accuracy)
```

De nauwkeurigheid van het bootstrapped model wordt dan gesorteerd. Daarna worden de 10e en 90e kwantiteit van de nauwkeurigheid van het model een 95% betrouwbaarheidsinterval voor de nauwkeurigheid van het model met de aangegeven steekproefgrootte.

![ het drukbevel om het betrouwbaarheidsinterval van de volheidsscore te tonen.](../images/use-cases/confidence-interval.png)

In het bovenstaande cijfer staat dat als u slechts 1000 rijen nodig hebt om uw modellen te trainen, u kunt verwachten dat de nauwkeurigheid tussen ongeveer 84% en 88% zal dalen. U kunt de `LIMIT` clausule in de vragen van de Dienst van de Vraag aanpassen die op uw behoeften worden gebaseerd om de prestaties van de modellen te verzekeren.
