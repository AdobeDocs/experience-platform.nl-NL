---
title: Modellen
description: Model levenscyclusbeheer met de extensie Data Distiller SQL. Leer hoe u geavanceerde statistische modellen kunt maken, trainen en beheren met SQL, inclusief belangrijke processen zoals modelversioning, evaluatie en voorspelling, om actioneerbare inzichten van uw gegevens af te leiden.
role: Developer
exl-id: c609a55a-dbfd-4632-8405-55e99d1e0bd8
source-git-commit: 09129d9d19816b4d93b4979305f4ad532e5ffde4
workflow-type: tm+mt
source-wordcount: '1645'
ht-degree: 0%

---

# Modellen

>[!AVAILABILITY]
>
>Deze functionaliteit is beschikbaar voor klanten die de Data Distiller-add hebben aangeschaft. Neem voor meer informatie contact op met uw Adobe-vertegenwoordiger.

De Dienst van de vraag steunt nu de kernprocessen om een model te bouwen en op te stellen. U kunt SQL gebruiken om het model te trainen gebruikend uw gegevens, zijn nauwkeurigheid te evalueren, en dan het getrainde model te gebruiken om voorspellingen over nieuwe gegevens te maken. U kunt het model dan gebruiken om van uw vroegere gegevens te generaliseren om geïnformeerde besluiten over echte scenario&#39;s te nemen.

De drie stappen in de levenscyclus van het model voor het genereren van actioneerbare inzichten zijn:

1. **Opleiding**: Het model leert patronen van de verstrekte dataset. (model maken of vervangen)
2. **het Testen/de Evaluatie**: De prestaties van het model worden beoordeeld gebruikend een afzonderlijke dataset. (`model_evaluate`)
3. **Voorspelling**: Het opgeleide model wordt gebruikt om voorspellingen over nieuwe, onzichtbare gegevens te maken.

Gebruik de modelSQL uitbreiding, die aan de bestaande SQL grammatica wordt toegevoegd, om de modellevenscyclus volgens uw bedrijfsbehoeften te beheren. Dit document behandelt SQL die wordt vereist om een model tot stand te brengen of te vervangen, een model op te leiden, te evalueren, wanneer nodig opnieuw op te leiden, en inzichten te voorspellen.

## Modelontwikkeling en -training {#create-and-train}

Leer hoe te om, een machine het leren model te bepalen te vormen en op te leiden gebruikend SQL bevelen. SQL toont hieronder aan hoe te om een model tot stand te brengen, eigenschaptechniektransformaties toe te passen, en het opleidingsproces in werking te stellen om het model voor toekomstig gebruik correct te verzekeren wordt gevormd. In de volgende SQL-opdrachten worden verschillende opties voor het maken en beheren van modellen beschreven:

- **CREEER MODEL**: Creeert en tredt een nieuw model op een gespecificeerde dataset. Als er al een model met dezelfde naam bestaat, retourneert deze opdracht een fout.
- **CREEER MODEL ALS NIET** BESTAAT: Creeert en tredt een nieuw model slechts als een model met de zelfde naam niet reeds op de gespecificeerde dataset bestaat.
- **CREEER OF VERVANG MODEL**: Creeert en tredt een model, dat de recentste versie van een bestaand model met de zelfde naam op de gespecificeerde dataset vervangt.

```sql
CREATE MODEL | CREATE MODEL IF NOT EXISTS | CREATE OR REPLACE MODEL}
model_alias
[TRANSFORM (select_list)]
[OPTIONS(model_option_list)]
[AS {select_query}]
 
model_option_list:
    MODEL_TYPE = { 'LINEAR_REG' |
                   'LOGISTIC_REG' |
                   'KMEANS' }
  [, MAX_ITER = int64_value ]
 [, LABEL = string_array ]
[, REG_PARAM = float64_value ]
```

**Voorbeeld**

```sql
CREATE MODEL churn_model
TRANSFORM (vector_assembler(array(current_customers, previous_customers)) features) 
OPTIONS(MODEL_TYPE='linear_reg', LABEL='churn_rate') 
AS
SELECT *
FROM churn_with_rate
ORDER BY period;
```

Om u te helpen de belangrijkste componenten en de configuraties in het modelverwezenlijking en het trainingsproces begrijpen, verklaren de volgende nota&#39;s het doel en de functie van elk element in het SQL voorbeeld hierboven.

- `<model_alias>`: De alias van het model is een herbruikbare naam die aan het model is toegewezen, waarnaar later kan worden verwezen. U moet het model een naam geven.
- `transform`: De transformatieclausule wordt gebruikt om eigenschapengineering-transformaties (bijvoorbeeld, het één-hete coderen en koord indexeren) op de dataset toe te passen alvorens het model te leiden. De laatste component van de instructie `TRANSFORM` moet een `vector_assembler` zijn met een lijst met kolommen waaruit de functies voor modeltraining zouden bestaan, of een afgeleid type van de instructie `vector_assembler` (zoals `max_abs_scaler(feature)` , `standard_scaler(feature)` , enzovoort). Alleen de kolommen die in de laatste component worden vermeld, worden gebruikt voor training. Alle andere kolommen, zelfs als deze worden opgenomen in de query `SELECT` , worden uitgesloten.
- `label = <label-COLUMN>`: De labelkolom in de trainingsdataset die het doel of het resultaat opgeeft dat het model beoogt te voorspellen.
- `training-dataset`: met deze syntaxis selecteert u de gegevens die worden gebruikt om het model te trainen.
- `type = 'LogisticRegression'`: Deze syntaxis geeft het type leeralgoritme voor machines aan dat moet worden gebruikt. De opties zijn `LinearRegression` , `LogisticRegression` en `KMeans` .
- `options`: Dit sleutelwoord verstrekt een flexibele reeks sleutel-waarde paren om het model te vormen.
   - `Key model_type`: `model_type = '<supported algorithm>'` - Geeft het type leeralgoritme voor machines aan dat moet worden gebruikt. Tot de ondersteunde opties behoren `LinearRegression` , `LogisticRegression` en `KMeans` .
   - `Key label`: `label = <label_COLUMN>`: definieert de labelkolom in de trainingsdataset, die het doel of het resultaat aangeeft dat het model beoogt te voorspellen.

Gebruik SQL om naar de dataset te verwijzen die voor opleiding wordt gebruikt.

>[!TIP]
>
>Voor een volledige verwijzing op de `TRANSFORM` clausule, met inbegrip van gesteunde functies en gebruik over zowel `CREATE MODEL` als `CREATE TABLE`, zie de [`TRANSFORM` clausule in de SQL documentatie van de Syntaxis ](../sql/syntax.md#transform).

## Een model bijwerken {#update}

Leer hoe te om een bestaand machine het leren model bij te werken door nieuwe eigenschappen technische transformaties toe te passen en opties zoals het algoritmetype en etiketkolom te vormen. Bij elke update wordt een nieuwe versie van het model gemaakt, die vanaf de laatste versie wordt verhoogd. Dit zorgt ervoor dat de wijzigingen worden bijgehouden en dat het model opnieuw kan worden gebruikt in toekomstige evaluatie- of voorspellingsstappen.

In het volgende voorbeeld ziet u hoe u een model bijwerkt met nieuwe transformaties en opties:

```sql
UPDATE MODEL <model_alias> TRANSFORM (vector_assembler(array(current_customers, previous_customers)) features)  OPTIONS(MODEL_TYPE='logistic_reg', LABEL='churn_rate')  AS SELECT * FROM churn_with_rate ORDER BY period;
```

**Voorbeeld**

Om u te helpen het versioning proces begrijpen, overweeg het volgende bevel:

```sql
UPDATE MODEL model_vdqbrja OPTIONS(MODEL_TYPE='logistic_reg', LABEL='Survived') AS SELECT * FROM titanic_e2e_dnd;
```

Nadat deze opdracht is uitgevoerd, heeft het model een nieuwe versie, zoals in de onderstaande tabel wordt getoond:

| Bijgewerkte model-id | Bijgewerkt model | Nieuwe versie |
|--------------------------------------------|---------------|-------------|
| a8f6a254-8f28-42ec-8b26-94edeb4698e8 | model_vdqbrja | 2 |

In de volgende notities worden de belangrijkste componenten en opties in de workflow voor modelupdates beschreven.

- `UPDATE model <model_alias>`: de opdracht Bijwerken verwerkt het versiebeheer en maakt een nieuwe modelversie die is verhoogd vanaf de laatste versie.
- `version`: Een optioneel trefwoord dat alleen tijdens updates wordt gebruikt om expliciet op te geven dat een nieuwe versie moet worden gemaakt. Als deze waarde wordt weggelaten, wordt de versie automatisch door het systeem verhoogd.

### Getransformeerde functies voorvertonen en behouden {#preview-transform-output}

Gebruik de component `TRANSFORM` in de instructies `CREATE TABLE` en `CREATE TEMP TABLE` om een voorvertoning van de uitvoer van functietransformaties weer te geven en door te zetten vóór modeltraining. Deze verbetering verstrekt zicht in hoe de transformatiefuncties (zoals het coderen, tokenization, en vectorassembleer) op uw dataset worden toegepast.

Door getransformeerde gegevens in een standalone lijst te materialiseren, kunt u tussenliggende eigenschappen inspecteren, verwerkingslogica bevestigen, en eigenschapkwaliteit verzekeren alvorens een model te creëren. Dit verbetert de transparantie over de machineleiding van het leren en steunt meer geïnformeerde besluitvorming tijdens modelontwikkeling.

#### Syntaxis {#syntax}

Gebruik de component `TRANSFORM` binnen een instructie `CREATE TABLE` of `CREATE TEMP TABLE` , zoals hieronder wordt getoond:

```sql
CREATE TABLE [IF NOT EXISTS] table_name
[WITH (tableProperties)]
TRANSFORM (transformFunctionExpression1, transformFunctionExpression2, ...)
AS SELECT * FROM source_table;
```

Of:

```sql
CREATE TEMP TABLE [IF NOT EXISTS] table_name
[WITH (tableProperties)]
TRANSFORM (transformFunctionExpression1, transformFunctionExpression2, ...)
AS SELECT * FROM source_table;
```

**Voorbeeld**

Een tabel maken met behulp van basistransformaties:

```sql
CREATE TABLE ctas_transform_table
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) as ohe_add_comments,
  tokenizer(comments) as token_comments
)
AS SELECT * FROM movie_review;
```

Maak een tijdelijke tabel met extra technische stappen:

```sql
CREATE TEMP TABLE ctas_transform_table
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) as ohe_add_comments,
  tokenizer(comments) as token_comments,
  stop_words_remover(token_comments, array('and','very','much')) stp_token,
  ngram(stp_token, 3) ngram_token,
  tf_idf(ngram_token, 20) ngram_idf,
  count_vectorizer(stp_token, 13) cnt_vec_comments,
  tf_idf(token_comments, 10, 1) as cmts_idf
)
AS SELECT * FROM movie_review;
```

Dan vraag de output:

```sql
SELECT * FROM ctas_transform_table LIMIT 1;
```

#### Belangrijke overwegingen {#considerations}

Hoewel deze functie de transparantie verbetert en functievalidatie ondersteunt, zijn er belangrijke beperkingen waarmee u rekening moet houden wanneer u de component `TRANSFORM` buiten het maken van het model gebruikt.

- **Vectoroutput**: Als de transformatie vector-type output produceert, worden zij automatisch omgezet in series.
- **de beperking van het hergebruik van de partij**: De Lijsten die met `TRANSFORM` worden gecreeerd kunnen transformaties tijdens lijstverwezenlijking slechts toepassen. De nieuwe partijen gegevens die met `INSERT INTO` worden opgenomen worden **niet automatisch getransformeerd**. Als u dezelfde transformatielogica wilt toepassen op nieuwe gegevens, moet u de tabel opnieuw maken met een nieuwe instructie `CREATE TABLE AS SELECT` (CTAS).
- **Model heruse beperking**: De lijsten die het gebruiken van `TRANSFORM` worden gecreeerd kunnen niet direct in `CREATE MODEL` verklaringen worden gebruikt. U moet de `TRANSFORM` -logica opnieuw definiëren tijdens het maken van het model. Transformaties die uitvoer van vectortypen produceren, worden niet ondersteund tijdens modeltraining. Voor meer informatie, zie de [ types van de transformatieoutputgegevens van de Eigenschap ](./feature-transformation.md#available-transformations).

>[!NOTE]
>
>Deze functie is ontworpen voor inspectie en validatie. Het is geen substituut voor herbruikbare pijpleidingslogica. Transformaties die zijn bedoeld voor invoer van het model moeten expliciet opnieuw worden gedefinieerd in de stap voor het maken van het model.

## Modellen evalueren {#evaluate-model}

Voor betrouwbare resultaten moet u de nauwkeurigheid en effectiviteit van het model beoordelen voordat u het voor voorspellingen implementeert met het trefwoord `model_evaluate` . De SQL verklaring specificeert hieronder een testdataset, specifieke kolommen, en de versie van het model om het model te testen door zijn prestaties te evalueren.

```sql
SELECT *
FROM   model_evaluate(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   test_dataset)
```

De functie `model_evaluate` neemt `model-alias` als eerste argument en een flexibele instructie `SELECT` als tweede argument. De Query Service voert eerst de instructie `SELECT` uit en wijst de resultaten toe aan de `model_evaluate` Adobe Defined Function (ADF). Het systeem verwacht dat de kolomnamen en gegevenstypen in het resultaat van de instructie `SELECT` overeenkomen met de namen die in de trainingsstap worden gebruikt. Deze kolomnamen en gegevenstypen worden behandeld als testgegevens en etiketgegevens voor evaluatie.

>[!IMPORTANT]
>
>Bij de evaluatie (`model_evaluate`) en het voorspellen (`model_predict`), worden de transformatie(s) gebruikt die op het tijdstip van opleiding worden uitgevoerd.

## Voorspelend {#predict}

>[!IMPORTANT]
>
>De verbeterde kolomselectie en aliasing voor `model_predict` worden gecontroleerd door een eigenschapvlag. Tussenvelden zoals `probability` en `rawPrediction` worden standaard niet opgenomen in de voorspelling-uitvoer.\
>Als u toegang tot deze tussenliggende velden wilt inschakelen, voert u de volgende opdracht uit voordat u `model_predict` uitvoert:
>
>`set advanced_statistics_show_hidden_fields=true;`

Gebruik het trefwoord `model_predict` om het opgegeven model en de versie toe te passen op een gegevensset en om voorspellingen te genereren. U kunt alle uitvoerkolommen selecteren, specifieke kolommen kiezen of aliassen toewijzen om de uitvoerhelderheid te verbeteren.

Door gebrek, slechts zijn de basiskolommen en de definitieve voorspelling teruggekeerd tenzij de eigenschapvlag wordt toegelaten.

```sql
SELECT * FROM model_predict(model-alias, version-number, SELECT col1, col2 FROM dataset);
```

### Specifieke uitvoervelden selecteren {#select-specific-output-fields}

Wanneer de functiemarkering is ingeschakeld, kunt u een subset van velden ophalen uit de uitvoer van `model_predict` . Gebruik dit om tussenliggende resultaten, zoals voorspellingskansen, onbewerkte voorspellingsscores, en basiskolommen van de inputvraag terug te winnen.

**Geval 1: Terugkeer alle beschikbare outputgebieden**

```sql
SELECT * FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

**Geval 2: Terugkeer geselecteerde kolommen**

```sql
SELECT a, b, c, probability, predictionCol FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

**Geval 3: Terugkeer geselecteerde kolommen met aliassen**

```sql
SELECT a, b, c, probability AS p1, predictionCol AS pdc FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

In elk geval worden de buitenste `SELECT` besturingselementen geretourneerd die resulteren in velden. Dit zijn basisvelden van de invoerquery, samen met voorspellingsuitvoer zoals `probability` , `rawPrediction` en `predictionCol` .

### Voorspelingen behouden met CREATE TABLE of INVOEGEN IN

U kunt voorspellingen voortzetten met &#39;TABEL MAKEN ALS SELECT&#39; of &#39;INVOEGEN IN SELECT&#39;, inclusief indien gewenst voorspelling-uitvoer.

**Voorbeeld: Creeer lijst met alle gebieden van de voorspellingsoutput**

```sql
CREATE TABLE scored_data AS SELECT * FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

**Voorbeeld: Voeg geselecteerde outputgebieden met aliassen in**

```sql
INSERT INTO scored_data SELECT a, b, c, probability AS p1, predictionCol AS pdc FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

Dit biedt flexibiliteit om alleen de relevante voorspellingsoutputvelden en basiskolommen voor downstreamanalyse of rapportage te selecteren en aan te houden.

## Uw modellen evalueren en beheren

Gebruik de opdracht `SHOW MODELS` om alle beschikbare modellen weer te geven die u hebt gemaakt. Gebruik het om de modellen te bekijken die zijn opgeleid en voor evaluatie of voorspelling beschikbaar zijn. Wanneer de vraag, wordt de informatie opgehaald van de modelbewaarplaats die tijdens modelverwezenlijking wordt bijgewerkt. De teruggekeerde details zijn: modelidentiteitskaart, modelnaam, versie, brondataset, algoritmedetails, opties/parameters, gecreeerde/bijgewerkte tijd, en de gebruiker die het model creeerde.

```sql
SHOW MODELS;
```

De resultaten worden weergegeven in een tabel die vergelijkbaar is met de onderstaande tabel:

| model-id | model-naam | versie | bron-dataset | type | opties | transformeren | velden | gemaakt | bijgewerkt | gemaakt door |
|--------------------|---------------|---------|------------------|-----------------------|------------------------------|---------------------------------------------------------------------------|----------------------|---------------------|---------------------|------------|
| `model-84362-mdunj` | `SalesModel` | 1,0 | `sales_data_2023` | `LogisticRegression` | `{"label": "label-field"}` | `one_hot_encoder(name)`, `ohe_name`, `string_indexer(gender)`, `genderSI` | \[&quot;naam&quot;, &quot;geslacht&quot;\] | 2024-08-14 10:30 | 2024-08-14 11:00 | `JohnSnow@adobe.com` |

## Uw modellen opschonen en onderhouden

Gebruik de opdracht `DROP MODELS` om de modellen te verwijderen die u in het modelregister hebt gemaakt. U kunt het gebruiken om verouderde, ongebruikte, of ongewenste modellen te verwijderen. Hierdoor worden middelen vrijgemaakt en worden alleen relevante modellen in stand gehouden. U kunt ook een optionele modelnaam toevoegen voor een betere specificiteit. Hiermee laat u alleen het model vallen met de meegeleverde modelversie.

```sql
DROP MODEL IF EXISTS modelName
DROP MODEL IF EXISTS modelName modelVersion ;
```

## Volgende stappen

Na het lezen van dit document, begrijpt u nu de basisSQL syntaxis die wordt vereist om vertrouwde modellen tot stand te brengen, op te leiden en te beheren gebruikend Gegevens Distiller. Daarna, onderzoek het [ document van het Implementeren van geavanceerde statistische modellen ](./implement-models/implement-models.md) om over de diverse vertrouwde op beschikbare modellen te leren en hoe te om hen effectief binnen uw SQL werkschema uit te voeren. Als u niet reeds hebt, zorg ervoor om het ](./feature-engineering.md) document van de Techniek van de Eigenschap te herzien 0} om ervoor te zorgen dat uw gegevens optimaal voor modelopleiding worden voorbereid.[
