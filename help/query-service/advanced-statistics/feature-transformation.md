---
title: Technieken voor kenmerktransformatie
description: Leer essentiële voorbewerkingstechnieken, zoals gegevenstransformatie, codering en schaling met functies, waarmee gegevens worden voorbereid voor training in statistische modellen. Het behandelt het belang van het behandelen van ontbrekende waarden en het omzetten van categoriale gegevens om modelprestaties en nauwkeurigheid te verbeteren.
role: Developer
exl-id: ed7fa9b7-f74e-481b-afba-8690ce50c777
source-git-commit: e7bc30c153f67c59e9c04e8c8df60394f48871d0
workflow-type: tm+mt
source-wordcount: '3450'
ht-degree: 5%

---

# Technieken voor kenmerktransformatie

Transformaties zijn cruciale voorbewerkingsstappen die gegevens omzetten of schalen in een formaat dat geschikt is voor modeltraining en -analyse en die optimale prestaties en nauwkeurigheid garanderen. Dit document fungeert als aanvullende syntaxisbron en biedt uitgebreide informatie over belangrijke technieken voor het transformeren van functies voor het voorbewerken van gegevens.

Machinedesmodellen kunnen tekenreekswaarden of null-waarden niet rechtstreeks verwerken, waardoor gegevensvoorbewerking essentieel is. In deze handleiding wordt uitgelegd hoe u verschillende transformaties kunt gebruiken om ontbrekende waarden toe te passen, categoriale gegevens om te zetten in numerieke indelingen en technieken voor schalen van functies zoals eenwarige codering en vectorisatie toe te passen. Deze methodes laten modellen toe om effectief van de gegevens te interpreteren en te leren, uiteindelijk hun prestaties te verbeteren.

## Automatische functietransformatie {#automatic-transformations}

Als u ervoor kiest de component `TRANSFORM` over te slaan in de opdracht `CREATE MODEL` , wordt de functie automatisch getransformeerd. Automatische gegevensvoorbewerking omvat null-vervanging en standaardfunctietransformaties (op basis van het gegevenstype). Numerieke kolommen en tekstkolommen worden automatisch toegerekend en vervolgens worden functietransformaties uitgevoerd om ervoor te zorgen dat de gegevens een geschikte indeling hebben voor modeltraining in het leren van machines. Dit proces omvat het toerekenen van gegevens en categorische, numerieke en booleaanse transformaties.

>[!IMPORTANT]
>
>De functietransformatie die tijdens de training wordt gebruikt, wordt ook gebruikt voor functietransformatie op het moment van voorspelling en evaluatie.

In de volgende tabellen wordt uitgelegd hoe verschillende gegevenstypen worden verwerkt wanneer de component `TRANSFORM` wordt weggelaten tijdens de opdracht `CREATE MODEL` .

### Null-vervanging {#automatic-null-replacement}

| Gegevenstype | Null-vervanging |
|-----------------|-----------------------------------------------------|
| Numeriek | Nulls worden vervangen door de gemiddelde waarde van de kolom. |
| Categorisch | Nulls worden vervangen door het trefwoord `ml_unknown` . |
| Boolean | Nulls worden vervangen door een `FALSE` -waarde. |
| Tijdstempel | Dit wordt een doorlopend veld verwacht. |
| Geneste/STRUCT | De vervanging hangt van het datatype van de bladknoop af. |

### Eigenschaptransformatie {#automatic-feature-transformation}

| Gegevenstype | Functietransformatie |
|-----------------|-----------------------------------------------------|
| Numeriek | NIET VEREIST - aangezien dit gegevenstype door machine het leren algoritmen wordt begrepen. |
| String | Tekenreeksindexering vindt plaats. |
| Boolean | Tekenreeksindexering vindt plaats. |
| Tijdstempel | Er vindt geen bewerking plaats. |
| STRUCT | De waarde wordt uitgebreid tot het bladknooppunt. Transformatie vindt plaats op basis van het gegevenstype van het bladknooppunt. |

**voorbeeld**

```sql
CREATE model modelname options(model_type='logistic_reg', label='rating') AS SELECT * FROM movie_rating;
```

## Handmatige functietransformaties {#manual-transformations}

Als u aangepaste gegevensvoorbewerking wilt definiëren in de instructie `CREATE MODEL` , gebruikt u de component `TRANSFORM` in combinatie met een willekeurig aantal van de beschikbare transformatiefuncties. Deze handmatige voorbewerkingsfuncties kunnen ook buiten de component `TRANSFORM` worden gebruikt. Alle transformaties die in de [ transformatorsectie hieronder ](#available-transformations) worden besproken, kunnen worden gebruikt om de gegevens manueel vooraf te verwerken.

### Belangrijkste kenmerken {#key-characteristics}

Hier volgt een overzicht van de belangrijkste kenmerken van functietransformatie waarmee u rekening moet houden wanneer u de voorbewerkingsfuncties definieert:

- **Syntaxis**: `TRANSFORM(functionName(colName, parameters) <aliasNAME>)`
   - De naam van de alias is verplicht in de syntaxis. U moet een aliasnaam opgeven anders mislukt de query.

- **Parameters**: De parameters zijn positionele argumenten. Dit betekent dat elke parameter alleen bepaalde waarden kan gebruiken en dat alle voorafgaande parameters moeten worden opgegeven als er aangepaste waarden zijn opgegeven. Raadpleeg de relevante documentatie voor meer informatie over welke functie het argument gebruikt.

- **het Ketsen transformatoren**: De output van één transformator kan de input aan een andere transformator worden.

- **het gebruik van de Eigenschap**: De laatste eigenschaptransformatie wordt gebruikt als eigenschap van het machine het leren model.

**Voorbeeld**

```sql
CREATE MODEL modelname 
TRANSFORM(
  string_imputer(language, 'adding_null') AS imp_language, 
  numeric_imputer(users_count, 'mode') AS imp_users_count, 
  string_indexer(imp_language) AS si_lang,  
  vector_assembler(array(imp_users_count, si_lang, watch_minutes)) AS features
)  
OPTIONS(MODEL_TYPE='logistic_reg', LABEL='rating') 
AS SELECT * FROM df;
```

## Beschikbare transformaties {#available-transformations}

Er zijn 19 beschikbare transformaties. Deze transformaties zijn verdeeld in [ Algemene transformaties ](#general-transformations), [ Numerieke transformaties ](#numeric-transformations), [ Categorische transformaties ](#categorical-transformations), en [ Textual transformaties ](#textual-transformations).

### Algemene transformaties {#general-transformations}

Lees deze sectie voor details op de transformatoren die voor een brede waaier van gegevenstypes worden gebruikt. Deze informatie is essentieel als u transformaties moet toepassen die niet specifiek zijn voor categoriale of tekstuele gegevens.

>[!NOTE]
>
>Het gegevenstype van de invoergegevens verwijst naar de kolom waarop de toerekening wordt toegepast. Het gegevenstype output verwijst naar de kolom die als output wordt geproduceerd nadat de transformatie van kracht is geworden.

#### Numerieke invoer {#numeric-imputer}

De **Numerieke invoertransformator** voltooit ontbrekende waarden in een dataset. Dit gebruikt of het gemiddelde, mediaan, of wijze van de kolommen waarin de ontbrekende waarden worden gevestigd. De invoerkolommen moeten `DoubleType` of `FloatType` zijn. Meer informatie en voorbeelden kunnen in de [ documentatie van het het algoritme van de Vonk ](https://spark.apache.org/docs/2.2.0/ml-features.html#imputer) worden gevonden.

>[!NOTE]
>
>Alle null-waarden in invoerkolommen worden beschouwd als ontbrekend en worden daarom ook toegerekend.

**Datatypen**

- Datatype invoer: Numeriek
- Datatype uitvoer: Numeriek

**Definitie**

```sql
transformer(numeric_imputer(hour, 'mean') hour_imputed)
```

**Parameters**

| Parameter | Beschrijving | Type | Standaard | Optioneel |
| -------- | ------------ | ----- | -------- | -------- |
| `STRATEGY` | Een toerekeningsstrategie. De beschikbare waarden zijn: [`mean` , `median` , `mode`] . | string | gemiddelde | optioneel |

{style="table-layout:auto"}

**Voorbeeld vóór toerekening**

| id | uur |
|---|---|
| 0 | 18,0 |
| 1 | null |
| 2 | 8,0 |

**Voorbeeld na toerekening (gebruikend gemiddelde strategie)**

| id | uur |
|---|---|
| 0 | 18,0 |
| 1 | 13,0 |
| 2 | 8,0 |

#### Tekeninvoer {#string-imputer}

De **uitvoerder van het Koord** transformator voltooit ontbrekende waarden in een dataset gebruikend een koord dat door de gebruiker als functieargument wordt verstrekt. De invoer- en uitvoerkolommen moeten het gegevenstype `string` hebben.

>[!NOTE]
>
>Alle null-waarden in invoerkolommen worden beschouwd als ontbrekend en worden vervangen door de opgegeven tekenreeks.

**Datatypen**

- Input datatype: String
- Output datatype: String

**Definitie**

```sql
transform(string_imputer(name, 'unknown_name') as name_imputed)
```

**Parameters**

| Parameter | Beschrijving | Type | Standaard | Optioneel |
| -------- | ------------ | ----- | -------- | -------- |
| `NULL_REPLACEMENT` | De waarde die null vervangt. | string | ml_unknown | optioneel |

{style="table-layout:auto"}

**Voorbeeld vóór toerekening**

| id | name |
|---|---|
| 0 | John |
| 1 | null |
| 2 | Alice |

**Voorbeeld na toerekening (gebruikend &quot;ml_unknown&quot;als vervanging)**

| id | name |
|---|---|
| 0 | John |
| 1 | ml_unknown |
| 2 | Alice |

#### Booleaanse invoer {#boolean-imputer}

De **invoertransformator Van Boole** voltooit ontbrekende waarden in een dataset voor een booleaanse kolom. De invoer- en uitvoerkolommen moeten van het `Boolean` type zijn.

>[!NOTE]
>
>Alle null-waarden in invoerkolommen worden beschouwd als ontbrekend en worden vervangen door de opgegeven Booleaanse waarde.

**Datatypen**

- Input datatype: Boolean
- Output datatype: Boolean

**Definitie**

```sql
transform(boolean_imputer(name, true) as name_imputed)
```

**Parameters**

| Parameter | Beschrijving | Type | Standaard | Optioneel |
| -------- | ------------ | ----- | -------- | -------- |
| `NULL_REPLACEMENT` | Booleaanse imputer. Toegestane waarden: [`true`, `false`]. | boolean | false | optioneel |

**Voorbeeld vóór toerekening**

| id | markeren |
|---|---|
| 0 | true |
| 1 | null |
| 2 | false |

**Voorbeeld na toerekening (het gebruiken &quot;waar&quot;als vervanging)**

| id | markeren |
|---|---|
| 0 | true |
| 1 | true |
| 2 | false |

#### Vectorassembleur {#vector-assembler}

De transformator `VectorAssembler` combineert een gespecificeerde lijst van inputkolommen in één enkele vectorkolom, die het gemakkelijker maken om veelvoudige eigenschappen in machine het leren modellen te beheren. Dit is met name handig als u onbewerkte functies en functies die door verschillende functietransformatoren zijn gegenereerd, wilt samenvoegen tot één verenigde eigenschapvector. `VectorAssembler` accepteert invoerkolommen van numerieke, booleaanse en vectortypen. In elke rij worden de waarden van de invoerkolommen in de opgegeven volgorde samengevoegd tot een vector.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#vectorassembler) -->

**Datatypen**

- Datatype van de input: `array[string]` (kolomnamen met numerieke/serie [ numerieke ] waarden)
- Datatype uitvoer: `Vector[double]`

**Definitie**

```sql
transform(vector_assembler(id, hour, mobile, userFeatures) as features)
```

**Parameters**

| Parameter | Beschrijving | Type | Standaard | Optioneel |
| -------- | ------------ | ----- | -------- | -------- |
| NA | Voor deze transformator zijn geen aanvullende parameters vereist. | NA | NA | NA |

{style="table-layout:auto"}

**Voorbeeld vóór transformatie**

| id | uur | mobiel | userFeatures | geklikt |
|---|-------|--------|------------------|---------|
| 0 | 18 | 1,0 | [ 0.0, 10.0, 0.5 ] | 1,0 |

{style="table-layout:auto"}

**Voorbeeld na transformatie**

| id | uur | mobiel | userFeatures | geklikt | functies |
|---|------|--------|------------------|---------|-------------------------------|
| 0 | 18 | 1,0 | [ 0.0, 10.0, 0.5 ] | 1,0 | [ 18.0, 1.0, 0.0, 10.0, 0.5 ] |

{style="table-layout:auto"}

### Numerieke transformaties {#numeric-transformations}

Lees deze sectie voor meer informatie over de beschikbare transformatoren voor het verwerken en schalen van numerieke gegevens. Deze transformatoren zijn noodzakelijk om numerieke eigenschappen in uw datasets te behandelen en te optimaliseren.

#### Binarizer {#binarizer}

De transformator `Binarizer` zet numerieke eigenschappen in binaire (0/1) eigenschappen door een proces om genoemd binarization. De waarden van de eigenschap groter dan de gespecificeerde drempel worden omgezet in 1.0, terwijl de waarden gelijk aan of minder dan de drempel in 0.0 worden omgezet. De `Binarizer` ondersteunt zowel `Vector` - als `Double` -typen voor de invoerkolom.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#binarizer). -->

**Datatypen**

- Datatype invoer: Numerieke kolom
- Datatype uitvoer: Numeriek

**Definitie**

```sql
transform(numeric_imputer(rating, 'mode') rating_imp, binarizer(rating_imp) rating_binarizer)
```

**Parameters**

| Parameter | Beschrijving | Type | Standaard | Optioneel |
|------------|----------------------------------------------------------------------------------------------------------|----------|----------|----------|
| `THRESHOLD` | Param voor de drempel die wordt gebruikt om ononderbroken eigenschappen binariseren. Functies die hoger zijn dan de drempelwaarde, worden binariseerd aan 1,0, terwijl kenmerken die gelijk zijn aan of kleiner zijn dan de drempelwaarde, worden gebonden aan 0,0. | int/double | 0,0 | optioneel |

{style="table-layout:auto"}

**input van het Voorbeeld vóór binarization**

| id | beoordeling |
|---|---------|
| 0 | -18,0 |
| 1 | 13,0 |
| 2 | 8,0 |

**output van het Voorbeeld na binarization (standaarddrempel van 0.0)**

| id | beoordeling |
|---|---------|
| 0 | 0,0 |
| 1 | 1,0 |
| 2 | 1,0 |

**Definitie met douanedrempel**

```sql
transform(numeric_imputer(age, 'mode') age_imp, binarizer(age_imp, 14.0) age_binarizer)
```

**output van het Voorbeeld na binarization (met een drempel van 14.0)**

| id | ouderdom |
|---|-------|
| 0 | 0,0 |
| 1 | 0,0 |
| 2 | 1,0 |

#### Bucketizer {#bucketizer}

De transformator `Bucketizer` zet een kolom van ononderbroken eigenschappen in een kolom van eigenschapemmers om, die op user-specified drempels worden gebaseerd. Dit proces is nuttig om ononderbroken gegevens in discrete banden of emmers te segmenteren. Voor `Bucketizer` is een parameter `splits` vereist die de grenzen van de emmers definieert.

**Datatypen**

- Datatype invoer: Numerieke kolom
- Datatype uitvoer: Numeriek (bindwaarden)

**Definitie**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

**Parameters**

| Parameter | Beschrijving | Type | Standaard | Optioneel |
|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|----------|----------|
| `splits` | Een parameter voor het in kaart brengen van ononderbroken eigenschappen in emmers. Met `n+1` splitsingen zijn er `n` emmers. Splits moeten in strikt toenemende volgorde staan en het bereik (x,y) wordt gebruikt voor elk emmertje behalve het laatste segment, dat y omvat. | array(dubbel) | N.v.t. | optioneel |

{style="table-layout:auto"}

**Voorbeelden van splitsingen**

- Array(Double.NegativeInfinity, 0.0, 1.0, Double.PositiveInfinity)
- Array(0.0, 1.0, 2.0)

Splits moeten het gehele bereik van Dubbele waarden bestrijken; anders worden waarden buiten de opgegeven splitsingen als fouten behandeld.

**transformatie van het Voorbeeld**

Dit voorbeeld neemt een kolom van ononderbroken eigenschappen (`course_duration`), bindt het volgens verstrekte `splits`, en assembleert dan de resulterende emmers met andere eigenschappen.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

#### MinMaxScaler {#minmaxscaler}

De `MinMaxScaler` transformator schrapt opnieuw elke eigenschap in een dataset van vectorrijen aan een gespecificeerde waaier, typisch [ 0, 1 ]. Dit zorgt ervoor dat alle eigenschappen gelijkwaardig aan het model bijdragen. Dit is vooral handig voor modellen die gevoelig zijn voor functie-schaling, zoals op verloop gebaseerde algoritmen met descent. `MinMaxScaler` werkt met de volgende parameters:

- **min**: De ondergrens van de transformatie, die door alle eigenschappen wordt gedeeld. De standaardwaarde is `0.0` .
- **maximum**: De bovengrens van de transformatie, die door alle eigenschappen wordt gedeeld. De standaardwaarde is `1.0` .

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#minmaxscaler).  -->

**Datatypen**

- Datatype invoer: `Array[Double]`
- Datatype uitvoer: `Array[Double]`

**Definitie**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

**Parameters**

| Parameter | Beschrijving | Type | Standaard | Optioneel |
|-----------|--------------------------------------------------------------------------------------------------|------|---------|----------|
| `min` | Ondergrens na transformatie, gedeeld door alle functies. | double | 0,0 | optioneel |
| `max` | Bovengrens na transformatie, die door alle eigenschappen wordt gedeeld. | double | 1,0 | optioneel |

**transformatie van het Voorbeeld**

In dit voorbeeld wordt een set functies getransformeerd en worden deze met MinMaxScaler opnieuw geschaald naar het opgegeven bereik nadat verschillende andere transformaties zijn toegepast.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

#### MaxAbsScaler {#maxabsscaler}

De `MaxAbsScaler` transformator schrapt elke eigenschap in een dataset van vectorrijen aan waaier [ - 1, 1 ] door door de maximumabsolute waarde van elke eigenschap te delen. Deze transformatie is ideaal voor het behouden van de flexibiliteit in gegevenssets met zowel positieve als negatieve waarden, aangezien de gegevens niet worden verschoven of gecentreerd. Dit maakt `MaxAbsScaler` bijzonder geschikt voor modellen die gevoelig zijn voor de schaal van inputeigenschappen, zoals die met afstandsberekeningen.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#maxabsscaler). -->

**Datatypen**

- Datatype invoer: `Array[Double]`
- Datatype uitvoer: `Array[Double]`

**Definitie**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling)
```

**Parameters**

| Parameter | Beschrijving | Type | Standaard | Optioneel |
|-----------|---------------------------------------------------------------------------------------------------------|------|---------|----------|
| NA | MaxAbsScaler vereist geen extra parameters voor zijn verrichting. | NA | NA | NA |

**transformatie van het Voorbeeld**

Dit voorbeeld past verscheidene transformaties, met inbegrip van `MaxAbsScaler`, toe om eigenschappen in waaier [ - 1, 1 ] opnieuw te schalen.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling)
```

#### Normalizer {#normalizer}

`Normalizer` is een transformator die elke vector in een dataset van vectorrijen normaliseert om een eenheidsnorm te hebben. Dit proces zorgt voor een consistente schaal zonder de richting van de vectoren te wijzigen. Deze transformatie is met name handig in modellen voor machinaal leren die afhankelijk zijn van afstandsmetingen of andere op vectoren gebaseerde berekeningen, vooral wanneer de grootte van vectoren aanzienlijk varieert.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#normalizer) -->

**Datatypen**

- Datatype invoer: `array[double]` / `vector[double]`
- Datatype uitvoer: `vector[double]`

**Definitie**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, normalizer(vec_assembler, 3) as normalized)
```

**Parameters**

| Parameter | Beschrijving | Type | Standaard | Optioneel |
|-----------|----------------------------------------------------------------------------------------|---------|---------|----------|
| `p` | Geeft aan welke `p-norm` wordt gebruikt voor normalisatie (bijvoorbeeld `1-norm` , `2-norm` , enzovoort). | integer | 2 | optioneel |

**transformatie van het Voorbeeld**

In dit voorbeeld wordt getoond hoe u verschillende transformaties kunt toepassen, waaronder de `Normalizer` , om een set functies te normaliseren met de opgegeven `p-norm` .

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, normalizer(vec_assembler, 3) as normalized)
```

#### QuantileDiscretizer {#quantilediscretizer}

`QuantileDiscretizer` is een transformator die een kolom met ononderbroken eigenschappen in binden categoriale eigenschappen omzet, met het aantal banden die door de `numBuckets` parameter worden bepaald. In sommige gevallen kan het werkelijke aantal emmers kleiner zijn dan het opgegeven aantal als er te weinig duidelijke waarden zijn om voldoende hoeveelheden te maken.

Deze transformatie is vooral handig voor het vereenvoudigen van de weergave van doorlopende gegevens of het voorbereiden van algoritmen die beter werken met categoriale invoer.

**Datatypen**

- Datatype invoer: Numerieke kolom
- Datatype uitvoer: numerieke kolom (categorisch)

**Definitie**

```sql
TRANSFORM(quantile_discretizer(hour, 3) as result)
```

**Parameters**

| Parameter | Beschrijving | Type | Standaard | Optioneel |
|--------------|--------------------------------------------------------------------------------------------------------------------------|---------|---------|----------|
| `NUM_BUCKETS` | Het aantal emmers (cijfers of categorieën) waarin de gegevenspunten worden gegroepeerd. Dit getal moet groter dan of gelijk aan twee zijn. | integer | 2 | optioneel |

**transformatie van het Voorbeeld**

In dit voorbeeld wordt getoond hoe `QuantileDiscretizer` een kolom met doorlopende functies ( `hour` ) in drie categoriale emmers bindt.

```sql
TRANSFORM(quantile_discretizer(hour, 3) as result)
```

**Voorbeeld vóór en na discretization**

| id | uur | resultaat |
|---|------|--------|
| 0 | 18,0 | 2,0 |
| 1 | 19,0 | 2,0 |
| 2 | 8,0 | 1,0 |
| 3 | 5,0 | 1,0 |
| 4 | 2,2 | 0,0 |

#### StandardScaler {#standardscaler}

`StandardScaler` is een transformator die elke eigenschap in een dataset van vectorrijen normaliseert om een eenheidsstandaardafwijking en/of nulgemiddelde te hebben. Dit proces maakt de gegevens geschikter voor algoritmen die veronderstellen de eigenschappen rond nul met een verenigbare schaal worden gecentreerd. Deze transformatie is met name van belang voor modellen voor machinaal leren, zoals SVM, logistieke regressie en neurale netwerken, waar ongestandaardiseerde gegevens kunnen leiden tot convergentieproblemen of een geringere nauwkeurigheid.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#standardscaler).  -->

**Datatypen**

- Datatype invoer: Vector
- Uitvoergegevenstype: Vector

**Definitie**

```sql
TRANSFORM(standard_scaler(feature) as ss_features)
```

**Parameters**

| Parameter | Beschrijving | Type | Standaard | Optioneel |
|------------|------------------------------------------------------------------------------------------------------|---------|---------|----------|
| `withStd` | Hiermee schaalt u de gegevens zodat deze een standaardafwijking per eenheid hebben. | boolean | Waar | optioneel |
| `withMean` | Hiermee centreert u de gegevens met het gemiddelde voordat u gaat schalen. Deze optie produceert dichte output, dus gebruik voorzichtigheid met dunne input. | boolean | Onwaar | optioneel |

**transformatie van het Voorbeeld**

In dit voorbeeld wordt getoond hoe u StandardScaler toepast op een reeks functies en deze normaliseert met de standaardafwijking per eenheid en het gemiddelde nul.

```sql
TRANSFORM(standard_scaler(feature) as ss_features)
```

### Categorische transformaties {#categorical-transformations}

Lees deze sectie voor een overzicht van de beschikbare transformatoren die zijn ontworpen om categoriale gegevens voor modellen voor machinaal leren om te zetten en vooraf te verwerken. Deze transformaties zijn ontworpen voor gegevenspunten die verschillende categorieën of labels vertegenwoordigen, in plaats van numerieke waarden.

#### StringIndex {#stringindexer}

`StringIndexer` is een transformator die een koordkolom van etiketten in een kolom van numerieke indexen codeert. De indexen variëren van 0 tot `numLabels` en worden geordend met labelfrequentie (het meest frequente label krijgt een index van 0). Als de inputkolom numeriek is, wordt het gegoten aan een koord alvorens te indexeren. Onzichtbare labels kunnen aan de index `numLabels` worden toegewezen als dat door de gebruiker is opgegeven.

Deze transformatie is vooral handig voor het omzetten van categoriale tekenreeksgegevens in numerieke vormen, waardoor deze geschikt zijn voor machinaal leermodellen die numerieke invoer vereisen.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#stringindexer) -->

**Datatypen**

- Input datatype: String
- Datatype uitvoer: Numeriek

**Definitie**

```sql
TRANSFORM(string_indexer(category) as si_category)
```

**Parameters**

| Parameter | Beschrijving | Type | Standaard | Optioneel |
|-----------|-------------|------|---------|----------|
| NA | Voor de bewerking van `StringIndexer` zijn geen aanvullende parameters vereist. | NA | NA | NA |

**transformatie van het Voorbeeld**

In dit voorbeeld wordt getoond hoe u `StringIndexer` toepast op een categorische functie en deze omzet in een numerieke index.

```sql
TRANSFORM(string_indexer(category) as si_category)
```

#### OneHotEncoder {#onehotencoder}

`OneHotEncoder` is een transformator die een kolom van etiketindexen in een kolom van dunne binaire vectoren omzet, waar elke vector hoogstens één-waarde heeft. Deze codering is vooral handig om algoritmen die numerieke invoer vereisen, zoals Logistische regressie, toe te staan categoriale gegevens op effectieve wijze op te nemen.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#onehotencoder).  -->

**Datatypen**

- Datatype invoer: Numeriek
- Datatype van de output: Vector [ int ]

**Definitie**

```sql
TRANSFORM(string_indexer(category) as si_category, one_hot_encoder(si_category) as ohe_category)
```

**Parameters**

| Parameter | Beschrijving | Type | Standaard | Optioneel |
|-----------|-------------|------|---------|----------|
| NA | OneHotEncoder heeft geen aanvullende parameters nodig voor de werking ervan. | NA | NA | NA |

**transformatie van het Voorbeeld**

In dit voorbeeld wordt getoond hoe u `StringIndexer` eerst toepast op een categorische functie en vervolgens de `OneHotEncoder` gebruikt om de geïndexeerde waarden om te zetten in een binaire vector.

```sql
TRANSFORM(string_indexer(category) as si_category, one_hot_encoder(si_category) as ohe_category)
```

### Teksttransformaties {#textual-transformations}

Deze sectie bevat informatie over de transformatoren die beschikbaar zijn voor het verwerken en converteren van tekstgegevens naar indelingen die kunnen worden gebruikt door modellen voor machinaal leren. Dit gedeelte is van cruciaal belang voor ontwikkelaars die werken met gegevens over natuurlijke talen en tekstanalyse.

#### CountVectorizer {#countvectorizer}

`CountVectorizer` is een transformator die een inzameling van tekstdocumenten in vectoren van symbolische tellingen omzet, die onduidelijke vertegenwoordiging veroorzaken die op de woordenschat wordt gebaseerd die uit het corpus wordt gehaald. Deze transformatie is essentieel voor het omzetten van tekstgegevens in een numerieke indeling die kan worden gebruikt door machinaal leeralgoritmen, zoals LDA (Latent Dirichlet Allocation), door de frequentie van tokens in elk document te vertegenwoordigen.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#countvectorizer). -->

**Datatypen**

- Datatype van de input: Serie [ Koord ]
- Datatype uitvoer: Dichte vector

**Definitie**

```sql
TRANSFORM(count_vectorizer(texts) as cv_output)
```

**Parameters**

| Parameter | Beschrijving | Type | Standaard | Optioneel |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------|---------|----------|
| `VOCAB_SIZE` | Maximale grootte van de woordenlijst. CountVectorizer bouwt een woordenlijst die slechts de hoogste `vocabSize` termijnen overweegt die door termijnfrequentie over het corpus worden bevolen. | Int | 218 | optioneel |
| `MIN_DOC_FREQ` | Hiermee geeft u het minimale aantal verschillende documenten op waarin een term moet voorkomen om in de woordenlijst te worden opgenomen. Dit kan een absoluut getal of een fractie van documenten zijn (bij een dubbele waarde). | Dubbel | 1,0 | optioneel |
| `MAX_DOC_FREQ` | Hiermee geeft u het maximum aantal verschillende documenten op waarin een term kan voorkomen om in de woordenlijst te worden opgenomen. Dit kan een absoluut getal of een fractie van documenten zijn (bij een dubbele waarde). | Dubbel | (263)-1 | optioneel |
| `MIN_TERM_FREQ` | Hiermee filtert u zeldzame woorden in een document uit. Termen met een frequentie/aantal dat lager is dan de opgegeven drempel worden genegeerd. Dit kan een absoluut getal of een fractie zijn van het tokenaantal van het document. | Dubbel | 1,0 | optioneel |

{style="table-layout:auto"}

**transformatie van het Voorbeeld**

Dit voorbeeld toont aan hoe CountVectorizer een inzameling van tekstseries in vectoren van symbolische tellingen omzet, die een dunne vertegenwoordiging veroorzaken.

```sql
TRANSFORM(count_vectorizer(texts) as cv_output)
```

**Voorbeeld vóór en na vectorization**

| id | teksten | cv_output |
|----|---------------------------------|-----------------------------------|
| 0 | Array(&quot;a&quot;, &quot;b&quot;, &quot;c&quot;) | (3, [ 0,1,2 ], [ 1.0,1.0,1.0 ]) |
| 1 | Array(&quot;a&quot;, &quot;b&quot;, &quot;b&quot;, &quot;c&quot;, &quot;a&quot;) | (3, [ 0,1,2 ], [ 2.0,2.0,1.0 ]) |

{style="table-layout:auto"}

#### NGram {#ngram}

`NGram` is een transformator die een opeenvolging van n-grammen produceert, waar n-gram een opeenvolging van (&#39;??&#39;) tokens (typisch woorden) voor wat geheel (`𝑛`) is. De uitvoer bestaat uit in de ruimte afgebakende reeksen opeenvolgende woorden van &#39;??&#39;, die kunnen worden gebruikt als functies in modellen voor machinaal leren, met name als deze gericht zijn op het verwerken van natuurlijke talen.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#n-gram). -->

**Datatypen**

- Datatype van de input: Serie [ Koord ]
- Datatype van de output: Serie [ Koord ]

**Definitie**

```sql
TRANSFORM(tokenizer(review_comments) as token_comments, ngram(token_comments, 3) as n_tokens)
```

**Parameters**

| Parameter | Beschrijving | Type | Standaard | Optioneel |
|-----------|-----------------------------------------------------------------------------------------------|---------|-------------------|----------|
| `N` | De minimale lengte n-gram moet groter zijn dan of gelijk zijn aan 1. | integer | 2 (bigramfuncties) | optioneel |

{style="table-layout:auto"}

**transformatie van het Voorbeeld**

In dit voorbeeld wordt getoond hoe de NGram-transformator een reeks van 3 gram maakt op basis van een lijst met tokens die zijn afgeleid van tekstgegevens.

```sql
TRANSFORM(tokenizer(review_comments) as token_comments, ngram(token_comments, 3) as n_tokens)
```

**Voorbeeld vóór en na transformatie n-gram**

| id | teksten | n_tokens |
|----|-------------------------------------------------------|-------------------------------------------------------|
| 0 | [ &quot;this&quot;, &quot;was&quot;, &quot;an&quot;, &quot;enterining&quot;, &quot;movie&quot;] | [ &quot;this was an&quot;, &quot;was an enterining&quot;, &quot;an enterining movie&quot;] |

{style="table-layout:auto"}

#### StopWordsRemover {#stopwordsremover}

`StopWordsRemover` is een transformator die stopwoorden uit een opeenvolging van koorden verwijdert, die gemeenschappelijke woorden filtreren die geen significante betekenis hebben. Deze neemt als invoer een reeks tekenreeksen aan (zoals de uitvoer van een kenizer) en verwijdert alle stopwoorden die door de parameter `stopWords` zijn opgegeven.

Deze transformatie is nuttig voor het vooraf verwerken van tekstgegevens, waardoor de effectiviteit van modellen voor het leren van downstreammachines wordt verbeterd door woorden te verwijderen die niet veel bijdragen aan de algemene betekenis.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#stopwordsremover) -->

**Datatypen**

- Datatype van de input: Serie [ Koord ]
- Datatype van de output: Serie [ Koord ]

**Definitie**

```sql
TRANSFORM(stop_words_remover(raw) as filtered)
```

**Parameters**

| Parameter | Beschrijving | Type | Standaard | Optioneel |
|--------------------|--------------------------------------------------------------------------------------------------|---------------|-------------------------|----------|
| `stopWords` | De woorden die moeten worden uitgefilterd. | serie [ koord ] | Standaard: Engelse stopwoorden | optioneel |

{style="table-layout:auto"}

<!-- Q) should this be the `CUSTOM_STOP_WORDS` parameter or the `stopWords` parameter?  -->

**transformatie van het Voorbeeld**

In dit voorbeeld wordt getoond hoe de `StopWordsRemover` algemene Engelse stopwoorden uit een lijst met tokens filtert.

```sql
TRANSFORM(stop_words_remover(raw) as filtered)
```

**Voorbeeld voor en na de verwijdering van eindewoorden**

| id | ruw | gefilterd |
|----|------------------------------|--------------------------|
| 0 | [ I, zag, rood, ballon ] | [ zag, rood, ballon ] |
| 1 | [ Mary, had, a, weinig, lamb ] | [ Mary, klein, lammeren ] |

**Voorbeeld met de woorden van het douaneeinde**

In dit voorbeeld wordt getoond hoe u een aangepaste lijst met stopwoorden gebruikt om specifieke woorden uit de invoerreeksen te filteren.

```sql
TRANSFORM(stop_words_remover(raw, array("red", "I", "had")) as filtered)
```

**Voorbeeld vóór en na de verwijdering van de douanestopwoorden**

| id | ruw | gefilterd |
|----|------------------------------|--------------------------|
| 0 | [ I, zag, rood, ballon ] | [ zag, ballon ] |
| 1 | [ Mary, had, a, weinig, lamb ] | [ Mary, a, klein, lammeren ] |

#### TF-IDF {#tf-idf}

`TF-IDF` (Term Frequency-Inverse Document Frequency) is een transformator die wordt gebruikt om het belang van een woord binnen een document met betrekking tot een corpus te meten. Term frequency (TF) verwijst naar het aantal keren dat een term \(t\) voorkomt in een document \(d\), terwijl documentfrequency (DF) meet hoeveel documenten in het corpus \(D\) de term \(t\) bevatten. Deze methode wordt op grote schaal gebruikt in tekstmijnbouw om de invloed te verminderen van veelvoorkomende woorden, zoals &quot;a&quot;, &quot;the&quot; en &quot;of&quot;, die weinig unieke informatie bevatten.

Deze transformatie is met name van belang voor het winnen van tekst en het verwerken van natuurlijke talen, omdat hiermee een numerieke waarde wordt toegewezen aan het belang van elk woord in een document en over het gehele corpus.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#tf-idf) -->

**Datatypen**

- Datatype van de input: Serie [ Koord ]
- Datatype van de output: Vector [ int ]

**Definitie**

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

**Parameters**

| Parameter | Beschrijving | Type | Standaard | Optioneel |
|-----------------|----------------------------------------------------------------------------------------|------|---------|----------|
| `NUM_FEATURES` | Het aantal functies dat moet worden gegenereerd. Moet groter zijn dan 0. | Int | 262144 | optioneel |
| `MIN_DOC_FREQ` | Het minimumaantal documenten waarin een term in het model moet worden opgenomen. | Int | 0 | optioneel |

{style="table-layout:auto"}

**transformatie van het Voorbeeld**

In dit voorbeeld wordt getoond hoe u TF-IDF kunt gebruiken om verdeelde zinnen om te zetten in een eigenschapvector die het belang van elke term in de context van het gehele corpus vertegenwoordigt.

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

#### Tokenizer {#tokenizer}

`Tokenizer` is een transformator die tekst, zoals een zin, in individuele termijnen, typisch woorden opsplitst. Het zet zinnen om in series van tokens, die een fundamentele stap in tekstpreprocessing verstrekken die de gegevens voor verdere tekstanalyse of modelleringsprocessen voorbereidt.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#tokenizer) -->

**Datatypen**

- Datatype invoer: tekstzin
- Datatype van de output: Serie [ Koord ]

**Definitie**

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

**Parameters**

| Parameter | Beschrijving | Type | Standaard | Optioneel |
|-----------|-------------|------|---------|----------|
| NA | Voor de bewerking van `Tokenizer` zijn geen aanvullende parameters vereist. | NA | NA | NA |

**transformatie van het Voorbeeld**

In dit voorbeeld wordt getoond hoe zinnen in `Tokenizer` worden onderverdeeld in afzonderlijke woorden (tokens) als onderdeel van een tekstverwerkingspijplijn.

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

#### Word2Vec {#word2vec}

`Word2Vec` is een schatter die opeenvolgingen van woorden verwerkt die documenten vertegenwoordigen en `Word2VecModel` traint. Dit model wijst elk woord aan een unieke vector met een vaste grootte toe en transformeert elk document in een vector door het gemiddelde te nemen van de vectoren van alle woorden in het document. `Word2Vec` wordt op grote schaal gebruikt in verwerkingstaken voor natuurlijke talen en maakt woordinsluiting waarmee semantische betekenis wordt vastgelegd en tekstgegevens worden omgezet in numerieke vectoren die de relaties tussen woorden vertegenwoordigen en die een effectievere tekstanalyse en modellen voor machinaal leren mogelijk maken.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#word2vec) -->

**Datatypen**

- Datatype van de input: Serie [ Koord ]
- Datatype van de output: Vector [ Dubbel ]

**Definitie**

```sql
TRANSFORM(tokenizer(review) as tokenized, word2Vec(tokenized, 10, 1) as word2Vec)
```

**Parameters**

| Parameter | Beschrijving | Type | Standaard | Optioneel |
|--------------|-----------------------------------------------------------------------------------------------------|---------|---------|----------|
| `VECTOR_SIZE` | De afmetingen van de vector waarin elk woord wordt getransformeerd. | Geheel | 100 | optioneel |
| `MIN_COUNT` | Het minimale aantal keren dat een token moet worden opgenomen in de woordenlijst van het model `Word2Vec` . | Geheel | 5 | optioneel |

{style="table-layout:auto"}

**transformatie van het Voorbeeld**

In dit voorbeeld wordt getoond hoe `Word2Vec` een verdeelde revisie omzet in een vector met een vaste grootte die het gemiddelde van de woordvectoren in het document vertegenwoordigt.

```sql
TRANSFORM(tokenizer(review) as tokenized, word2Vec(tokenized, 10, 1) as word2Vec)
```

**Voorbeeld vóór en na transformatie Word2Vec**

| revisie | verward | word2Vec |
|-------------------------------|--------------------------------------|---------------------------------|
| dit was een entertainmentfilm | [ dit, was, een, onderhoudend, film ] | [ -0.025713888928294182,0.0081879975157899,0.0092235435 731709,-0.01515385233797133,0.012175946310162545,3.11290 5901041035E-4,0.0025145105042611252,0.00575701978523284 3,-0.021328244300093502,0.009335877187550069 ] |

{style="table-layout:auto"}
