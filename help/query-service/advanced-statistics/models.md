---
title: Modellen
description: Model levenscyclusbeheer met de extensie Data Distiller SQL. Leer hoe u geavanceerde statistische modellen kunt maken, trainen en beheren met SQL, inclusief belangrijke processen zoals modelversioning, evaluatie en voorspelling, om actioneerbare inzichten van uw gegevens af te leiden.
role: Developer
source-git-commit: b248e8f8420b617a117d36aabad615e5bbf66b58
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 0%

---

# Modellen

>[!AVAILABILITY]
>
>Deze functionaliteit is beschikbaar voor klanten die de Data Distiller-add hebben aangeschaft. Neem voor meer informatie contact op met uw Adobe-vertegenwoordiger.

De Dienst van de vraag steunt nu de kernprocessen om een model te bouwen en op te stellen. U kunt SQL gebruiken om het model te trainen gebruikend uw gegevens, zijn nauwkeurigheid te evalueren, en dan treinmodel toe te passen om voorspellingen over nieuwe gegevens te maken. U kunt het model dan gebruiken om van uw vroegere gegevens te generaliseren om geïnformeerde besluiten over echte scenario&#39;s te nemen.

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

## Een model bijwerken {#update}

Leer hoe te om een bestaand machine het leren model bij te werken door nieuwe eigenschappen technische transformaties toe te passen en opties zoals het type van algoritme en etiketkolom te vormen. In de onderstaande SQL ziet u hoe u het versienummer van het model verhoogt bij elke update en hoe u ervoor zorgt dat wijzigingen worden bijgehouden, zodat het model opnieuw kan worden gebruikt in toekomstige evaluatie- of voorspellingsstappen.

```sql
UPDATE model <model_alias> transform( one_hot_encoder(NAME) ohe_name, string_indexer(gender) gendersi) options ( type = 'LogisticRegression', label = <label-COLUMN>, ) ASSELECT col1,
       col2,
       col3
FROM   training-dataset.
```

Om u te helpen begrijpen hoe te om modelversies te beheren en transformaties effectief toe te passen, verklaren de volgende nota&#39;s de belangrijkste componenten en de opties in het werkschema van de modelupdate.

- `UPDATE model <model_alias>`: de opdracht Bijwerken verwerkt het versienummer en verhoogt het versienummer van het model bij elke update.
- `version`: Een optioneel trefwoord dat alleen tijdens updates wordt gebruikt om een nieuwe versie van het model te maken.

## Modellen evalueren {#evaluate-model}

Voor betrouwbare resultaten moet u de nauwkeurigheid en effectiviteit van het model beoordelen voordat u het voor voorspellingen implementeert met het trefwoord `model_evaluate` . De SQL verklaring specificeert hieronder een testdataset, specifieke kolommen, en de versie van het model om het model te testen door zijn prestaties te evalueren.

```sql
SELECT *
FROM   model_evaluate(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   test -dataset)
```

De functie `model_evaluate` neemt `model-alias` als eerste argument en een flexibele instructie `SELECT` als tweede argument. De Service van de vraag voert eerst de `SELECT` verklaring uit en brengt de resultaten aan de `model_evaluate` Adobe Gedefinieerde Functie (ADF) in kaart. Het systeem verwacht dat de kolomnamen en gegevenstypen in het resultaat van de instructie `SELECT` overeenkomen met de namen die in de trainingsstap worden gebruikt. Deze kolomnamen en gegevenstypen worden behandeld als testgegevens en etiketgegevens voor evaluatie.

>[!IMPORTANT]
>
>Bij de evaluatie (`model_evaluate`) en het voorspellen (`model_predict`), worden de transformatie(s) gebruikt die op het tijdstip van opleiding worden uitgevoerd.

## Voorspelend {#predict}

Gebruik vervolgens het trefwoord `model_predict` om het opgegeven model en de versie toe te passen op een gegevensset en om voorspellingen voor de geselecteerde kolommen te genereren. De onderstaande SQL demonstreert dit proces en toont hoe u resultaten kunt voorspellen met behulp van de alias en versie van het model.

```sql
SELECT *
FROM   model_predict(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   dataset)
```

`model_predict` accepteert de alias van het model als het eerste argument en een flexibele instructie `SELECT` als het tweede argument. De Query Service voert eerst de instructie `SELECT` uit en wijst de resultaten toe aan de `model_predict` ADF. Het systeem verwacht dat de kolomnamen en gegevenstypen in het resultaat van de instructie `SELECT` overeenkomen met die van de trainingsstap. Deze gegevens worden vervolgens gebruikt voor het scoren en het genereren van voorspellingen.

>[!IMPORTANT]
>
>Bij de evaluatie (`model_evaluate`) en het voorspellen (`model_predict`), worden de transformatie(s) gebruikt die op het tijdstip van opleiding worden uitgevoerd.

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
