---
keywords: Experience Platform;home;populaire onderwerpen;queryservice;Query-service;sql syntaxis;sql;ctas;CTAS;Tabel maken als selectie
solution: Experience Platform
title: SQL-syntaxis in Query-service
description: In dit document wordt de SQL-syntaxis beschreven die wordt ondersteund door de Adobe Experience Platform Query Service.
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
source-git-commit: d2cb7c3d1968a33300d480e63c4cb007df3cce7b
workflow-type: tm+mt
source-wordcount: '4305'
ht-degree: 1%

---

# SQL-syntaxis in Query Service

U kunt standaard ANSI SQL voor `SELECT` verklaringen en andere beperkte bevelen in de Dienst van de Vraag van Adobe Experience Platform gebruiken. In dit document wordt de SQL-syntaxis beschreven die wordt ondersteund door [!DNL Query Service] .

## Vragen SELECTEREN {#select-queries}

De volgende syntaxis definieert een query `SELECT` die wordt ondersteund door [!DNL Query Service] :

```sql
[ WITH with_query [, ...] ]
SELECT [ ALL | DISTINCT [( expression [, ...] ) ] ]
    [ * | expression [ [ AS ] output_name ] [, ...] ]
    [ FROM from_item [, ...] ]
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
    [ WHERE condition ]
    [ GROUP BY grouping_element [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT | MINUS } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start ]
```

In de sectie met tabbladen hieronder vindt u de beschikbare opties voor de trefwoorden FROM, GROUP en WITH.

>[!BEGINTABS]

>[!TAB `from_item`]

```sql
table_name [ * ] [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
```

```sql
[ LATERAL ] ( select ) [ AS ] alias [ ( column_alias [, ...] ) ]
```

```sql
with_query_name [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
```

```sql
from_item [ NATURAL ] join_type from_item [ ON join_condition | USING ( join_column [, ...] ) ]
```

>[!TAB `grouping_element`]

```sql
( )
```

```sql
expression
```

```sql
( expression [, ...] )
```

```sql
ROLLUP ( { expression | ( expression [, ...] ) } [, ...] )
```

```sql
CUBE ( { expression | ( expression [, ...] ) } [, ...] )
```

```sql
GROUPING SETS ( grouping_element [, ...] )
```

>[!TAB `with_query`]

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
```

>[!ENDTABS]

De volgende subsecties bevatten details over extra clausules die u in uw vragen kunt gebruiken, op voorwaarde dat zij het hierboven geschetste formaat volgen.

### component SNAPSHOT

Deze clausule kan worden gebruikt om gegevens over een lijst incrementeel te lezen die op momentopname IDs wordt gebaseerd. Een momentopname identiteitskaart is een controlepuntteller die door een aantal wordt vertegenwoordigd van het type Long dat op een lijst van het gegevenshoeveeltal wordt toegepast telkens als het gegeven aan het wordt geschreven. De component `SNAPSHOT` koppelt zich aan de tabelrelatie waarmee deze wordt gebruikt.

```sql
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
```

#### Voorbeeld

```sql
SELECT * FROM table_to_be_queried SNAPSHOT SINCE start_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT AS OF end_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT BETWEEN start_snapshot_id AND end_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT BETWEEN HEAD AND start_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT BETWEEN end_snapshot_id AND TAIL;

SELECT * FROM (SELECT id FROM table_to_be_queried BETWEEN start_snapshot_id AND end_snapshot_id) C 

(SELECT * FROM table_to_be_queried SNAPSHOT SINCE start_snapshot_id) a
  INNER JOIN 
(SELECT * from table_to_be_joined SNAPSHOT AS OF your_chosen_snapshot_id) b 
  ON a.id = b.id;
```

In de onderstaande tabel wordt de betekenis van elke syntaxisoptie in de component SNAPSHOT uitgelegd.

| Syntaxis | Betekenis |
|-------------------------------------------------------------------|------------------------------------------------------------------------------------------|
| `SINCE start_snapshot_id` | Leest gegevens die beginnen met de opgegeven opname-id (exclusief). |
| `AS OF end_snapshot_id` | Gegevens worden gelezen zoals deze zich op de opgegeven opname-id bevonden (inclusief). |
| `BETWEEN start_snapshot_id AND end_snapshot_id` | Leest gegevens tussen de opgegeven begin- en eindopname-id&#39;s. Deze is exclusief voor `start_snapshot_id` en inclusief de `end_snapshot_id` . |
| `BETWEEN HEAD AND start_snapshot_id` | Leest gegevens vanaf het begin (vóór de eerste opname) tot en met de opgegeven start-opname-id. Hiermee worden alleen rijen in `start_snapshot_id` geretourneerd. |
| `BETWEEN end_snapshot_id AND TAIL` | Leest gegevens van net na gespecificeerde `end-snapshot_id` aan het eind van de dataset (exclusief momentopname ID). Dit betekent dat als `end_snapshot_id` de laatste momentopname in de dataset is, de vraag nul rijen zal terugkeren omdat er geen momentopnamen voorbij die laatste momentopname zijn. |
| `SINCE start_snapshot_id INNER JOIN table_to_be_joined AS OF your_chosen_snapshot_id ON table_to_be_queried.id = table_to_be_joined.id` | Leest gegevens die beginnen met de opgegeven momentopname-id uit `table_to_be_queried` en koppelt deze aan de gegevens uit `table_to_be_joined` zoals deze zich op `your_chosen_snapshot_id` bevonden. Verbinden is gebaseerd op passende IDs van de kolommen van identiteitskaart van de twee lijsten die worden aangesloten bij. |

Een `SNAPSHOT` -component werkt met een tabel- of tabelalias, maar niet boven op een subquery of weergave. Een `SNAPSHOT` -component werkt overal waar een `SELECT` -query op een tabel kan worden toegepast.

U kunt `HEAD` en `TAIL` ook gebruiken als speciale verschuivingswaarden voor opnamen. Het gebruik van `HEAD` verwijst naar een verschuiving vóór de eerste opname, terwijl `TAIL` verwijst naar een verschuiving na de laatste opname.

>[!NOTE]
>
>Als u tussen twee momentopname IDs vraagt, kunnen de volgende twee scenario&#39;s voorkomen als de beginmomentopname is verlopen en de facultatieve markering van het fallback gedrag (`resolve_fallback_snapshot_on_failure`) wordt geplaatst:
>
>- Als de facultatieve fallback gedragsvlag wordt geplaatst, kiest de Dienst van de Vraag de vroegste beschikbare momentopname, plaatst het als beginmomentopname, en keert de gegevens tussen de vroegste beschikbare momentopname en de gespecificeerde eindmomentopname terug. Dit gegeven is **inclusief** van de vroegste beschikbare momentopname.

### WHERE-component

Standaard zijn overeenkomsten die worden geproduceerd door een `WHERE` -component op een `SELECT` -query hoofdlettergevoelig. Als u wilt dat overeenkomsten niet hoofdlettergevoelig zijn, kunt u het trefwoord `ILIKE` gebruiken in plaats van `LIKE` .

```sql
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

De logica van de clausules LIKE en ILIKE wordt verklaard in de volgende lijst:

| Clausule | Operator |
| ------ | -------- |
| `WHERE condition LIKE pattern` | `~~` |
| `WHERE condition NOT LIKE pattern` | `!~~` |
| `WHERE condition ILIKE pattern` | `~~*` |
| `WHERE condition NOT ILIKE pattern` | `!~~*` |

**Voorbeeld**

```sql
SELECT * FROM Customers
WHERE CustomerName ILIKE 'a%';
```

Deze vraag keert klanten met namen terug die in &quot;A&quot;of &quot;a&quot;beginnen.

### VERBINDEN

Een `SELECT` -query die gebruikmaakt van verbindingen, heeft de volgende syntaxis:

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### UNIE, INTERSECT EN BEHALVE

De clausules `UNION`, `INTERSECT` en `EXCEPT` worden gebruikt om vergelijkbare rijen van twee of meer tabellen te combineren of uit te sluiten:

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### TABEL MAKEN ALS SELECT {#create-table-as-select}

De volgende syntaxis definieert een query `CREATE TABLE AS SELECT` (CTAS):

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false', label='PROFILE') ] AS (select_query)
```

| Parameters | Beschrijving |
| ----- | ----- |
| `schema` | De titel van het XDM-schema. Gebruik deze clausule slechts als u wenst om een bestaand schema XDM voor de nieuwe dataset te gebruiken die door de vraag CTAS wordt gecreeerd. |
| `rowvalidation` | (Optioneel) Hiermee wordt aangegeven of de gebruiker validatie op rijniveau wil toepassen voor elke nieuwe batch die wordt opgenomen voor de nieuwe dataset. De standaardwaarde is `true` . |
| `label` | Wanneer u een dataset met een vraag CTAS creeert, gebruik dit etiket met de waarde van `profile` om uw dataset zoals toegelaten voor profiel te etiketteren. Dit betekent dat uw dataset automatisch voor profiel duidelijk wordt aangezien het wordt gecreeerd. Zie het afgeleide document met kenmerkextensies voor meer informatie over het gebruik van `label` . |
| `select_query` | Een instructie `SELECT` . De syntaxis van de `SELECT` vraag kan in de [ UITGEZOCHTE vraagsectie ](#select-queries) worden gevonden. |

**Voorbeeld**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title', label='PROFILE') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>De instructie `SELECT` moet een alias hebben voor de statistische functies zoals `COUNT` , `SUM` , `MIN` , enzovoort. De instructie `SELECT` kan ook met of zonder haakjes () worden geleverd. U kunt een `SNAPSHOT` -component opgeven om incrementele delta&#39;s in de doeltabel te lezen.

## INVOEGEN IN

De opdracht `INSERT INTO` wordt als volgt gedefinieerd:

```sql
INSERT INTO table_name select_query
```

| Parameters | Beschrijving |
| ----- | ----- |
| `table_name` | De naam van de tabel waarin u de query wilt invoegen. |
| `select_query` | Een instructie `SELECT` . De syntaxis van de `SELECT` vraag kan in de [ UITGEZOCHTE vraagsectie ](#select-queries) worden gevonden. |

**Voorbeeld**

>[!NOTE]
>
>Het volgende is een verbeterd voorbeeld en eenvoudig voor educatieve doeleinden.

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!INFO]
> 
>Plaats **niet** de `SELECT` verklaring tussen haakjes (). Het schema van het resultaat van de instructie `SELECT` moet bovendien overeenkomen met het schema van de tabel die is gedefinieerd in de instructie `INSERT INTO` . U kunt een `SNAPSHOT` -component opgeven om incrementele delta&#39;s in de doeltabel te lezen.

De meeste velden in een echt XDM-schema zijn niet gevonden op het hoofdniveau en SQL staat het gebruik van puntnotatie niet toe. Als u een realistisch resultaat wilt bereiken met geneste velden, moet u elk veld in het `INSERT INTO` -pad toewijzen.

Als u geneste paden wilt `INSERT INTO` , gebruikt u de volgende syntaxis:

```sql
INSERT INTO [dataset]
SELECT struct([source field1] as [target field in schema],
[source field2] as [target field in schema],
[source field3] as [target field in schema]) [tenant name]
FROM [dataset]
```

**Voorbeeld**

```sql
INSERT INTO Customers SELECT struct(SupplierName as Supplier, City as SupplierCity, Country as SupplierCountry) _Adobe FROM OnlineCustomers;
```

## DROP TABLE

Met de opdracht `DROP TABLE` wordt een bestaande tabel verwijderd en wordt de aan de tabel gekoppelde map uit het bestandssysteem verwijderd als dit geen externe tabel is. Als de tabel niet bestaat, treedt een uitzondering op.

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

| Parameters | Beschrijving |
| ------ | ------ |
| `IF EXISTS` | Als dit wordt gespecificeerd, wordt geen uitzondering geworpen als de lijst **niet** bestaat. |

## DATABASE MAKEN

Met de opdracht `CREATE DATABASE` maakt u een ADLS-database (Azure Data Lake Storage).

```sql
CREATE DATABASE [IF NOT EXISTS] db_name
```

## DATABASE DROP

Met de opdracht `DROP DATABASE` verwijdert u de database uit een instantie.

```sql
DROP DATABASE [IF EXISTS] db_name
```

| Parameters | Beschrijving |
| ------ | ------ |
| `IF EXISTS` | Als dit wordt gespecificeerd, wordt geen uitzondering geworpen als het gegevensbestand **niet** bestaat. |

## DROP SCHEMA

De opdracht `DROP SCHEMA` laat een bestaand schema vallen.

```sql
DROP SCHEMA [IF EXISTS] db_name.schema_name [ RESTRICT | CASCADE]
```

| Parameters | Beschrijving |
| ------ | ------ |
| `IF EXISTS` | Als deze parameter wordt gespecificeerd en het schema **niet** bestaat, wordt geen uitzondering geworpen. |
| `RESTRICT` | De standaardwaarde voor de modus. Indien gespecificeerd, daalt het schema slechts als het **** geen lijsten bevat. |
| `CASCADE` | Indien opgegeven, wordt het schema neergezet samen met alle tabellen in het schema. |

## WEERGAVE MAKEN {#create-view}

Een SQL-weergave is een virtuele tabel die is gebaseerd op de resultaatset van een SQL-instructie. Maak een weergave met de instructie `CREATE VIEW` en geef deze een naam. U kunt die naam dan gebruiken om naar de resultaten van de vraag terug te verwijzen. Hierdoor is het gemakkelijker om complexe query&#39;s opnieuw te gebruiken.

De volgende syntaxis bepaalt een `CREATE VIEW` vraag voor een dataset. Deze dataset kan een ADLS of versnelde opslagdataset zijn.

```sql
CREATE VIEW view_name AS select_query
```

| Parameters | Beschrijving |
| ------ | ------ |
| `view_name` | De naam van de weergave die moet worden gemaakt. |
| `select_query` | Een instructie `SELECT` . De syntaxis van de `SELECT` vraag kan in de [ UITGEZOCHTE vraagsectie ](#select-queries) worden gevonden. |

**Voorbeeld**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

De volgende syntaxis definieert een query `CREATE VIEW` die een weergave maakt in de context van een database en schema.

**Voorbeeld**

```sql
CREATE VIEW db_name.schema_name.view_name AS select_query
CREATE OR REPLACE VIEW db_name.schema_name.view_name AS select_query
```

| Parameters | Beschrijving |
| ------ | ------ |
| `db_name` | De naam van de database. |
| `schema_name` | De naam van het schema. |
| `view_name` | De naam van de weergave die moet worden gemaakt. |
| `select_query` | Een instructie `SELECT` . De syntaxis van de `SELECT` vraag kan in de [ UITGEZOCHTE vraagsectie ](#select-queries) worden gevonden. |

**Voorbeeld**

```sql
CREATE VIEW <dbV1 AS SELECT color, type FROM Inventory;

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory;
```

## WEERGAVEN TONEN

De volgende vraag toont de lijst van meningen.

```sql
SHOW VIEWS;
```

```console
 Db Name  | Schema Name | Name  | Id       |  Dataset Dependencies | Views Dependencies | TYPE
----------------------------------------------------------------------------------------------
 qsaccel  | profile_agg | view1 | view_id1 | dwh_dataset1          |                    | DWH
          |             | view2 | view_id2 | adls_dataset          | adls_views         | ADLS
(2 rows)
```

## DROP VIEW

De volgende syntaxis definieert een query `DROP VIEW` :

```sql
DROP VIEW [IF EXISTS] view_name
```

| Parameters | Beschrijving |
| ------ | ------ |
| `IF EXISTS` | Als dit wordt gespecificeerd, wordt geen uitzondering geworpen als de mening **niet** bestaat. |
| `view_name` | De naam van de weergave die moet worden verwijderd. |

**Voorbeeld**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## Anoniem blok {#anonymous-block}

Een anoniem blok bestaat uit twee secties: uitvoerbaar en uitzondering-behandelend secties. In een anoniem blok, is de uitvoerbare sectie verplicht. De sectie voor de afhandeling van uitzonderingen is echter optioneel.

In het volgende voorbeeld ziet u hoe u een blok maakt met een of meer instructies die samen moeten worden uitgevoerd:

```sql
$$BEGIN
  statementList
[EXCEPTION exceptionHandler]
$$END

exceptionHandler:
      WHEN OTHER
      THEN statementList

statementList:
    : (statement (';')) +
```

Hieronder ziet u een voorbeeld waarin anonieme blokken worden gebruikt.

```sql
$$BEGIN
   SET @v_snapshot_from = select parent_id  from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_snapshot_to = select snapshot_id from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_log_id = select now();
   CREATE TABLE tracking_email_id_incrementally
     AS SELECT _id AS id FROM email_tracking_experience_event_dataset SNAPSHOT BETWEEN @v_snapshot_from AND @v_snapshot_to;

EXCEPTION
  WHEN OTHER THEN
    DROP TABLE IF EXISTS tracking_email_id_incrementally;
    SELECT 'ERROR';
$$END;
```

### Voorwaardelijke instructies in een anoniem blok {#conditional-anonymous-block-statements}

De IF-THEN-ELSE controlestructuur laat de voorwaardelijke uitvoering van een lijst van verklaringen toe wanneer een voorwaarde als WAAR wordt geëvalueerd. Deze controlestructuur is alleen van toepassing binnen een anoniem blok. Als deze structuur als standalone bevel wordt gebruikt, resulteert het in een syntaxisfout (&quot;Ongeldig bevel buiten Anoniem Blok&quot;).

Het codefragment hieronder demonstreert de juiste indeling voor een voorwaardelijke instructie IF-THEN-ELSE in een anoniem blok.

```javascript
IF booleanExpression THEN
   List of statements;
ELSEIF booleanExpression THEN 
   List of statements;
ELSEIF booleanExpression THEN 
   List of statements;
ELSE
   List of statements;
END IF
```

**Voorbeeld**

In het onderstaande voorbeeld wordt `SELECT 200;` uitgevoerd.

```sql
$$BEGIN
    SET @V = SELECT 2;
    SELECT @V;
    IF @V = 1 THEN
       SELECT 100;
    ELSEIF @V = 2 THEN
       SELECT 200;
    ELSEIF @V = 3 THEN
       SELECT 300;
    ELSE    
       SELECT 'DEFAULT';
    END IF;   

 END$$;
```

Deze structuur kan met `raise_error();` worden gebruikt om een aangepast foutbericht te retourneren. Het codeblok dat hieronder wordt weergegeven, eindigt het anonieme blok met &#39;aangepast foutbericht&#39;.

**Voorbeeld**

```sql
$$BEGIN
    SET @V = SELECT 5;
    SELECT @V;
    IF @V = 1 THEN
       SELECT 100;
    ELSEIF @V = 2 THEN
       SELECT 200;
    ELSEIF @V = 3 THEN
       SELECT 300;
    ELSE    
       SELECT raise_error('custom error message');
    END IF;   

 END$$;
```

#### Geneste IF-instructies

Geneste IF-instructies worden ondersteund binnen anonieme blokken.

**Voorbeeld**

```sql
$$BEGIN
    SET @V = SELECT 1;
    IF @V = 1 THEN
       SELECT 100;
       IF @V > 0 THEN
         SELECT 1000;
       END IF;   
    END IF;   

 END$$; 
```

#### Uitzonderingsblokken

Uitzonderingsblokken worden ondersteund binnen anonieme blokken.

**Voorbeeld**

```sql
$$BEGIN
    SET @V = SELECT 2;
    IF @V = 1 THEN
       SELECT 100;
    ELSEIF @V = 2 THEN
       SELECT raise_error(concat('custom-error for v= ', '@V' ));

    ELSEIF @V = 3 THEN
       SELECT 300;
    ELSE    
       SELECT 'DEFAULT';
    END IF;  
EXCEPTION WHEN OTHER THEN 
  SELECT 'THERE WAS AN ERROR';    
 END$$;
```

### Automatisch naar JSON {#auto-to-json}

De Dienst van de vraag steunt een facultatieve zitting-vlakke instelling om complexe gebieden van het hoogste niveau van interactieve UITGEZOCHTE vragen als koorden van JSON terug te keren. Met de instelling `auto_to_json` kunnen gegevens van complexe velden worden geretourneerd als JSON en vervolgens in JSON-objecten worden geparseerd met behulp van standaardbibliotheken.

STEL de functiemarkering `auto_to_json` in op true voordat u de SELECT-query met complexe velden uitvoert.

```sql
set auto_to_json=true; 
```

#### Voordat u de markering `auto_to_json` instelt

De volgende tabel bevat een voorbeeld van een queryresultaat voordat de instelling `auto_to_json` wordt toegepast. In beide scenario&#39;s werd dezelfde SELECT-query (zoals hieronder wordt weergegeven) gebruikt die een tabel met complexe velden als doel had.

```sql
SELECT * FROM TABLE_WITH_COMPLEX_FIELDS LIMIT 2;
```

De resultaten zijn als volgt:

```console
                _id                |                                _experience                                 | application  |                   commerce                   | dataSource |                               device                               |                       endUserIDs                       |                                                                                                environment                                                                                                |                     identityMap                     |                              placeContext                               |   receivedTimestamp   |       timestamp       | userActivityRegion |                                         web                                          | _adcstageforpqs
-----------------------------------+----------------------------------------------------------------------------+--------------+----------------------------------------------+------------+--------------------------------------------------------------------+--------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------+-------------------------------------------------------------------------+-----------------------+-----------------------+--------------------+--------------------------------------------------------------------------------------+-----------------
 31892EE15DE00000-401D52664FF48A52 | ("("("(1,1)","(1,1)")","(-209479095,4085488201,-2105158467,2189808829)")") | (background) | (NULL,"(USD,NULL)",NULL,NULL,NULL,NULL,NULL) | (475341)   | (32,768,1024,205202,https://ns.adobe.com/xdm/external/deviceatlas) | ("("(31892EE080007B35-E6CE00000000000,"(AAID)",t)")")  | ("(en-US,f,f,t,1.6,"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7",490,1125)",xo.net,64.3.235.13)     | [AAID -> "{(31892EE080007B35-E6CE00000000000,t)}"]  | ("("(34.01,-84.0)",lawrenceville,US,524,30043,ga)",600)                 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | (UT1)              | ("(f,Search Results,"(1.0)")","(http://www.google.com/search?ie=UTF-8&q=,internal)") |
 31892EE15DE00000-401B92664FF48AE8 | ("("("(1,1)","(1,1)")","(-209479095,4085488201,-2105158467,2189808829)")") | (background) | (NULL,"(USD,NULL)",NULL,NULL,NULL,NULL,NULL) | (475341)   | (32,768,1024,205202,https://ns.adobe.com/xdm/external/deviceatlas) | ("("(31892EE100007BF3-215FE00000000001,"(AAID)",t)")") | ("(en-US,f,f,t,1.5,"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7",768,556)",ntt.net,219.165.108.145) | [AAID -> "{(31892EE100007BF3-215FE00000000001,t)}"] | ("("(34.989999999999995,138.42)",shizuoka,JP,392005,420-0812,22)",-240) | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | (UT1)              | ("(f,Home - JJEsquire,"(1.0)")","(NULL,typed_bookmarked)")                           |
(2 rows)  
```

#### Na het instellen van de markering `auto_to_json`

In de volgende tabel ziet u het verschil in resultaten dat de instelling `auto_to_json` heeft op de resulterende gegevensset. Dezelfde SELECT-query werd in beide scenario&#39;s gebruikt.

```console
                _id                |   receivedTimestamp   |       timestamp       |                                                                                                                   _experience                                                                                                                   |           application            |             commerce             |    dataSource    |                                                                  device                                                                   |                                                   endUserIDs                                                   |                                                                                                                                                                                           environment                                                                                                                                                                                            |                             identityMap                              |                                                                                            placeContext                                                                                            |      userActivityRegion      |                                                                                     web                                                                                      | _adcstageforpqs
-----------------------------------+-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+----------------------------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------
 31892EE15DE00000-401D52664FF48A52 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | {"analytics":{"customDimensions":{"eVars":{"eVar1":"1","eVar2":"1"},"props":{"prop1":"1","prop2":"1"}},"environment":{"browserID":-209479095,"browserIDStr":"4085488201","operatingSystemID":-2105158467,"operatingSystemIDStr":"2189808829"}}} | {"userPerspective":"background"} | {"order":{"currencyCode":"USD"}} | {"_id":"475341"} | {"colorDepth":32,"screenHeight":768,"screenWidth":1024,"typeID":"205202","typeIDService":"https://ns.adobe.com/xdm/external/deviceatlas"} | {"_experience":{"aaid":{"id":"31892EE080007B35-E6CE00000000000","namespace":{"code":"AAID"},"primary":true}}}  | {"browserDetails":{"acceptLanguage":"en-US","cookiesEnabled":false,"javaEnabled":false,"javaScriptEnabled":true,"javaScriptVersion":"1.6","userAgent":"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7","viewportHeight":490,"viewportWidth":1125},"domain":"xo.net","ipV4":"64.3.235.13"}     | {"AAID":[{"id":"31892EE080007B35-E6CE00000000000","primary":true}]}  | {"geo":{"_schema":{"latitude":34.01,"longitude":-84.0},"city":"lawrenceville","countryCode":"US","dmaID":524,"postalCode":"30043","stateProvince":"ga"},"localTimezoneOffset":600}                 | {"dataCenterLocation":"UT1"} | {"webPageDetails":{"isHomePage":false,"name":"Search Results","pageViews":{"value":1.0}},"webReferrer":{"URL":"http://www.google.com/search?ie=UTF-8&q=","type":"internal"}} |
 31892EE15DE00000-401B92664FF48AE8 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | {"analytics":{"customDimensions":{"eVars":{"eVar1":"1","eVar2":"1"},"props":{"prop1":"1","prop2":"1"}},"environment":{"browserID":-209479095,"browserIDStr":"4085488201","operatingSystemID":-2105158467,"operatingSystemIDStr":"2189808829"}}} | {"userPerspective":"background"} | {"order":{"currencyCode":"USD"}} | {"_id":"475341"} | {"colorDepth":32,"screenHeight":768,"screenWidth":1024,"typeID":"205202","typeIDService":"https://ns.adobe.com/xdm/external/deviceatlas"} | {"_experience":{"aaid":{"id":"31892EE100007BF3-215FE00000000001","namespace":{"code":"AAID"},"primary":true}}} | {"browserDetails":{"acceptLanguage":"en-US","cookiesEnabled":false,"javaEnabled":false,"javaScriptEnabled":true,"javaScriptVersion":"1.5","userAgent":"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7","viewportHeight":768,"viewportWidth":556},"domain":"ntt.net","ipV4":"219.165.108.145"} | {"AAID":[{"id":"31892EE100007BF3-215FE00000000001","primary":true}]} | {"geo":{"_schema":{"latitude":34.989999999999995,"longitude":138.42},"city":"shizuoka","countryCode":"JP","dmaID":392005,"postalCode":"420-0812","stateProvince":"22"},"localTimezoneOffset":-240} | {"dataCenterLocation":"UT1"} | {"webPageDetails":{"isHomePage":false,"name":"Home - JJEsquire","pageViews":{"value":1.0}},"webReferrer":{"type":"typed_bookmarked"}}                                        |
(2 rows)
```

### Resolve fallback snapshot on failure {#resolve-fallback-snapshot-on-failure}

De optie `resolve_fallback_snapshot_on_failure` wordt gebruikt om het probleem van een verlopen opname-id op te lossen. Metagegevens voor momentopnamen verlopen na twee dagen en een verlopen momentopname kan de logica van een script ongeldig maken. Dit kan een probleem zijn wanneer anonieme blokken worden gebruikt.

Stel de optie `resolve_fallback_snapshot_on_failure` in op true als u een opname wilt overschrijven met een vorige opname-id.

```sql
SET resolve_fallback_snapshot_on_failure=true;
```

De volgende coderegel overschrijft de `@from_snapshot_id` met de oudste beschikbare `snapshot_id` op basis van metagegevens.

```sql
$$ BEGIN
    SET resolve_fallback_snapshot_on_failure=true;
    SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a JOIN
                            (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                on a.process_timestamp=b.process_timestamp;
    SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
    SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
    INSERT INTO DIM_TABLE_ABC_Incremental
     SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id WHERE NOT EXISTS (SELECT _id FROM DIM_TABLE_ABC_Incremental a WHERE _id=a._id);

Insert Into
   checkpoint_log
   SELECT
       'DIM_TABLE_ABC' process_name,
       'SUCCESSFUL' process_status,
      cast( @to_snapshot_id AS string) last_snapshot_id,
      cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
EXCEPTION
  WHEN OTHER THEN
    SELECT 'ERROR';
END
$$;
```


## Gegevensmiddelenorganisatie

Het is belangrijk om uw gegevensactiva logisch te organiseren binnen het gegevenshoop van Adobe Experience Platform aangezien zij groeien. De Dienst van de vraag breidt SQL constructies uit die u toelaten om gegevensactiva binnen een zandbak logisch gezien te groeperen. Deze organisatiemethode staat voor het delen van gegevensactiva tussen schema&#39;s toe zonder de behoefte om hen fysiek te bewegen.

De volgende SQL-constructies die gebruikmaken van de standaard SQL-syntaxis, worden ondersteund voor het logisch organiseren van uw gegevens.

```SQL
CREATE DATABASE dg1;
CREATE SCHEMA dg1.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

Zie de [ logische organisatie van gegevensactiva ](../best-practices/organize-data-assets.md) gids voor een meer gedetailleerde verklaring over de beste praktijken van de Dienst van de Vraag.

## Tabel bestaat

De SQL-opdracht `table_exists` wordt gebruikt om te bevestigen of een tabel momenteel in het systeem bestaat. Het bevel keert een booleaanse waarde terug: `true` als de lijst **** bestaat, en `false` als de lijst **niet** bestaat.

Door te controleren of een tabel bestaat voordat de instructies worden uitgevoerd, vereenvoudigt de functie `table_exists` het schrijven van een anoniem blok, zodat zowel de gebruiksgevallen `CREATE` als `INSERT INTO` worden behandeld.

De volgende syntaxis definieert de opdracht `table_exists` :

```SQL
$$
BEGIN

#Set mytableexist to true if the table already exists.
SET @mytableexist = SELECT table_exists('target_table_name');

#Create the table if it does not already exist (this is a one time operation).
CREATE TABLE IF NOT EXISTS target_table_name AS
  SELECT *
  FROM   profile_dim_date limit 10;

#Insert data only if the table already exists. Check if @mytableexist = 'true'
 INSERT INTO target_table_name           (
                     select *
                     from   profile_dim_date
                     WHERE  @mytableexist = 'true' limit 20
              ) ;
EXCEPTION
WHEN other THEN SELECT 'ERROR';

END $$; 
```

## Inline {#inline}

De functie `inline` scheidt de elementen van een array van structs en genereert de waarden in een tabel. Deze kan alleen in de lijst `SELECT` of een `LATERAL VIEW` worden geplaatst.

De `inline` functie **kan** niet in een uitgezochte lijst worden geplaatst waar er andere generatorfuncties zijn.

Door gebrek, worden de geproduceerde kolommen genoemd &quot;col1&quot;, &quot;col2&quot;, etc. Als de expressie `NULL` is, worden geen rijen gemaakt.

>[!TIP]
>
>U kunt de naam van kolommen wijzigen met de opdracht `RENAME` .

**Voorbeeld**

```sql
> SELECT inline(array(struct(1, 'a'), struct(2, 'b'))), 'Spark SQL';
```

In het voorbeeld wordt het volgende geretourneerd:

```text
1  a Spark SQL
2  b Spark SQL
```

In dit tweede voorbeeld wordt verder het concept en de toepassing van de functie `inline` getoond. Het gegevensmodel voor het voorbeeld wordt in de onderstaande afbeelding weergegeven.

![ het schemadiagram van A voor productListItems.](../images/sql/productListItems.png)

**Voorbeeld**

```sql
select inline(productListItems) from source_dataset limit 10;
```

De waarden die uit `source_dataset` zijn opgehaald, worden gebruikt om de doeltabel te vullen.

| SKU | _experience | hoeveelheid | priceTotal |
|---------------------|-----------------------------------|----------|--------------|
| product-id-1 | (&quot;(&quot;(&quot;(&quot;(A,pas,B,NULL)&quot;)&quot;)&quot;) | 5 | 10,5 |
| product-id-5 | (&quot;(&quot;(&quot;(A, pass, B, NULL)&quot;)&quot;) |          |              |
| product-id-2 | (&quot;(&quot;(&quot;(AF, C, D, NULL)&quot;)&quot;) | 6 | 40 |
| product-id-4 | (&quot;(&quot;(&quot;(&quot;(BM, pass, NA, NULL)&quot;)&quot;)&quot;) | 3 | 12 |

## [!DNL Spark] SQL-opdrachten

De onderafdeling hieronder behandelt de SQL bevelen van de Vonk die door de Dienst van de Vraag worden gesteund.

### SET

De opdracht `SET` stelt een eigenschap in en retourneert de waarde van een bestaande eigenschap of geeft alle bestaande eigenschappen weer. Als een waarde wordt opgegeven voor een bestaande eigenschapsleutel, wordt de oude waarde overschreven.

```sql
SET property_key = property_value
```

| Parameters | Beschrijving |
| ------ | ------ |
| `property_key` | De naam van de eigenschap die u wilt weergeven of wijzigen. |
| `property_value` | De waarde waarop u de eigenschap wilt instellen. |

Als u de waarde voor een instelling wilt retourneren, gebruikt u `SET [property key]` zonder een `property_value` .

## [!DNL PostgreSQL] opdrachten

De subsecties hieronder behandelen de [!DNL PostgreSQL] bevelen die door de Dienst van de Vraag worden gesteund.

### TABEL ANALYSEREN {#analyze-table}

De opdracht `ANALYZE TABLE` voert een distributieanalyse en statistische berekeningen uit voor de benoemde tabel of tabellen. Het gebruik van `ANALYZE TABLE` varieert afhankelijk van of de datasets op de [ versnelde opslag ](#compute-statistics-accelerated-store) of het [ gegevens meer ](#compute-statistics-data-lake) worden opgeslagen. Zie de desbetreffende secties voor meer informatie over het gebruik ervan.

#### COMPUTE STATISTIEKEN OP DE versnelde opslag {#compute-statistics-accelerated-store}

Met de opdracht `ANALYZE TABLE` worden statistieken voor een tabel in de versnelde opslag berekend. De statistieken worden berekend over uitgevoerde vragen CTAS of ITAS voor een bepaalde lijst op de versnelde opslag.

**Voorbeeld**

```sql
ANALYZE TABLE <original_table_name>
```

Hieronder volgt een lijst met statistische berekeningen die beschikbaar zijn na gebruik van de opdracht `ANALYZE TABLE` :-

| Berekende waarden | Beschrijving |
|---|---|
| `field` | De naam van de kolom in een tabel. |
| `data-type` | Het acceptabele type gegevens voor elke kolom. |
| `count` | Het aantal rijen dat een andere waarde dan null bevat voor dit veld. |
| `distinct-count` | Het aantal unieke of verschillende waarden voor dit veld. |
| `missing` | Het aantal rijen met een null-waarde voor dit veld. |
| `max` | De maximumwaarde uit de geanalyseerde tabel. |
| `min` | De minimumwaarde uit de geanalyseerde tabel. |
| `mean` | De gemiddelde waarde van de geanalyseerde tabel. |
| `stdev` | De standaardafwijking van de geanalyseerde tabel. |

#### STATISTIEKEN COMPUTEREN op het datumpeer {#compute-statistics-data-lake}

U kunt nu statistieken op kolomniveau over [!DNL Azure Data Lake Storage] (ADLS)-gegevenssets berekenen met de SQL-opdracht `COMPUTE STATISTICS` . Bereid kolomstatistieken over of de volledige dataset, een ondergroep van een dataset, alle kolommen, of een ondergroep van kolommen samen.

`COMPUTE STATISTICS` breidt de opdracht `ANALYZE TABLE` uit. De opdrachten `COMPUTE STATISTICS`, `FILTERCONTEXT` en `FOR COLUMNS` worden echter niet ondersteund in versnelde winkeltabellen. Deze extensies voor de opdracht `ANALYZE TABLE` worden momenteel alleen ondersteund voor ADLS-tabellen.

**Voorbeeld**

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS  FOR COLUMNS (commerce, id, timestamp);
```

De opdracht `FILTER CONTEXT` berekent statistieken over een subset van de gegevensset op basis van de opgegeven filtervoorwaarde. De opdracht `FOR COLUMNS` richt zich op specifieke kolommen voor analyse.

>[!NOTE]
>
>De `Statistics ID` en de gegenereerde statistieken zijn alleen geldig voor elke sessie en kunnen niet worden geopend voor verschillende PSQL-sessies.<br><br> Beperkingen:<ul><li>Het genereren van statistieken wordt niet ondersteund voor array- of kaartgegevenstypen</li><li>De gegevens verwerkte statistieken zijn **niet** voortgeduurd over zittingen.</li></ul><br><br> Opties:<br><ul><li>`skip_stats_for_complex_datatypes`</li></ul><br> door gebrek, wordt de vlag geplaatst aan waar. Als daarom statistieken worden aangevraagd voor een gegevenstype dat niet wordt ondersteund, wordt er geen foutmelding weergegeven, maar worden velden zonder toezicht overgeslagen met de niet-ondersteunde datatypen.<br> om berichten over fouten toe te laten wanneer de statistieken over niet gestaafd datatype worden gevraagd, gebruik: `SET skip_stats_for_complex_datatypes = false`.

De uitvoer van de console wordt weergegeven zoals hieronder wordt weergegeven.

```console
|     Statistics ID      | 
| ---------------------- |
| adc_geometric_stats_1  |
(1 row)
```

Vervolgens kunt u de berekende statistieken rechtstreeks opvragen door naar de `Statistics ID` te verwijzen. Gebruik de naam `Statistics ID` of de naam van de alias, zoals hieronder in de voorbeeldinstructie wordt getoond, om de uitvoer volledig weer te geven. Meer over deze eigenschap leren, zie de [ documentatie van de aliasnaam ](../key-concepts/dataset-statistics.md#alias-name).

```sql
-- This statement gets the statistics generated for `alias adc_geometric_stats_1`.
SELECT * FROM adc_geometric_stats_1;
```

Gebruik de opdracht `SHOW STATISTICS` om de metagegevens weer te geven voor alle tijdelijke statistieken die in de sessie worden gegenereerd. Met deze opdracht kunt u het bereik van uw statistische analyse verfijnen.

```sql
SHOW STATISTICS;
```

Hieronder ziet u een voorbeelduitvoer van SHOW STATISTICS.

```console
      statsId         |   tableName   | columnSet |         filterContext       |      timestamp
----------------------+---------------+-----------+-----------------------------+--------------------
adc_geometric_stats_1 | adc_geometric |   (age)   |                             | 25/06/2023 09:22:26
demo_table_stats_1    |  demo_table   |    (*)    |       ((age > 25))          | 25/06/2023 12:50:26
age_stats             | castedtitanic |   (age)   | ((age > 25) AND (age < 40)) | 25/06/2023 09:22:26
```

Zie de [ documentatie van de datasetstatistieken ](../key-concepts/dataset-statistics.md) voor meer informatie.

#### TABLESAMPLE {#tablesample}

De Dienst van de Vraag van Adobe Experience Platform verstrekt steekproefdatasets als deel van zijn benaderende mogelijkheden van de vraagverwerking.

Gegevenssetvoorbeelden kunnen het best worden gebruikt wanneer u geen exact antwoord nodig hebt voor een geaggregeerde bewerking via een gegevensset. Om efficiëntere verkennende vragen op grote datasets te leiden door een benaderende vraag uit te geven om een benaderend antwoord terug te keren, gebruik de `TABLESAMPLE` eigenschap.

De datasets van de steekproef worden gecreeerd met eenvormige willekeurige steekproeven van bestaande [!DNL Azure Data Lake Storage] (ADLS) datasets, gebruikend slechts een percentage verslagen van origineel. De voorbeeldfunctie van de gegevensset breidt de opdracht `ANALYZE TABLE` uit met de SQL-opdrachten `TABLESAMPLE` en `SAMPLERATE` .

In het onderstaande voorbeeld demonstreert regel 1 hoe u een 5%-monster van de tabel berekent. Regel twee toont aan hoe te om een 5% steekproef van een gefilterde mening van de gegevens binnen de lijst te berekenen.

**Voorbeeld**

```sql {line-numbers="true"}
ANALYZE TABLE tableName TABLESAMPLE SAMPLERATE 5;
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-01-01')) TABLESAMPLE SAMPLERATE 5:
```

Zie de [ documentatie van de datasetsteekproeven ](../key-concepts/dataset-samples.md) voor meer informatie.

### BEGINNEN

Met de opdracht `BEGIN` of de opdracht `BEGIN WORK` of `BEGIN TRANSACTION` wordt een transactiekanaal gestart. Om het even welke verklaringen die na het begin bevel worden ingevoerd zullen in één enkele transactie worden uitgevoerd tot een expliciete COMMIT of bevel ROLLBACK wordt gegeven. Deze opdracht is hetzelfde als `START TRANSACTION` .

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### SLUITEN

Met de opdracht `CLOSE` maakt u de bronnen vrij die aan een open cursor zijn gekoppeld. Nadat de cursor is gesloten, zijn er geen verdere bewerkingen meer toegestaan. Een cursor moet worden gesloten wanneer deze niet meer nodig is.

```sql
CLOSE name
CLOSE ALL
```

Als `CLOSE name` wordt gebruikt, vertegenwoordigt `name` de naam van een open curseur die moet worden gesloten. Als `CLOSE ALL` wordt gebruikt, worden alle open cursors gesloten.

### VERWIJDEREN

Als u een eerder voorbereide SQL-instructie wilt zoeken, gebruikt u de opdracht `DEALLOCATE` . Als u niet expliciet een voorbereide instructie hebt gedistribueerd, wordt de toewijzing ongedaan gemaakt wanneer de sessie wordt beëindigd. Meer informatie over voorbereide verklaringen kan in de [ bevelPREPARE ](#prepare) sectie worden gevonden.

```sql
DEALLOCATE name
DEALLOCATE ALL
```

Als `DEALLOCATE name` wordt gebruikt, vertegenwoordigt `name` de naam van de voorbereide instructie die moet worden gedeallocatie. Als `DEALLOCATE ALL` wordt gebruikt, worden alle voorbereide instructies gedeallocatie.

### VERKLAREN

Met de opdracht `DECLARE` kan de gebruiker een cursor maken die kan worden gebruikt om een klein aantal rijen op te halen uit een grotere query. Nadat de cursor is gemaakt, worden er rijen van opgehaald met `FETCH` .

```sql
DECLARE name CURSOR FOR query
```

| Parameters | Beschrijving |
| ------ | ------ |
| `name` | De naam van de cursor die moet worden gemaakt. |
| `query` | Een opdracht `SELECT` of `VALUES` die de rijen bevat die door de cursor moeten worden geretourneerd. |

### UITVOEREN

De opdracht `EXECUTE` wordt gebruikt om een eerder voorbereide instructie uit te voeren. Aangezien voorbereide instructies alleen tijdens een sessie bestaan, moet de voorbereide instructie zijn gemaakt met een instructie `PREPARE` die eerder in de huidige sessie is uitgevoerd. Meer informatie over het gebruik van voorbereide instructies vindt u in de sectie [`PREPARE` command ](#prepare) .

Als de instructie `PREPARE` die de instructie heeft gemaakt enkele parameters heeft opgegeven, moet een compatibele set parameters worden doorgegeven aan de instructie `EXECUTE` . Als deze parameters niet worden doorgegeven, treedt een fout op.

```sql
EXECUTE name [ ( parameter ) ]
```

| Parameters | Beschrijving |
| ------ | ------ |
| `name` | De naam van de voorbereide instructie die moet worden uitgevoerd. |
| `parameter` | De werkelijke waarde van een parameter voor de voorbereide instructie. Dit moet een expressie zijn die een waarde oplevert die compatibel is met het gegevenstype van deze parameter, zoals bepaald toen de voorbereide instructie werd gemaakt. Als er meerdere parameters zijn voor de voorbereide instructie, worden deze door komma&#39;s gescheiden. |

### VERKLAREN

Met de opdracht `EXPLAIN` geeft u het uitvoeringsplan voor de opgegeven instructie weer. Het uitvoeringsplan toont hoe de tabellen waarnaar door de instructie wordt verwezen, worden gescand. Als er naar meerdere tabellen wordt verwezen, wordt aangegeven welke samenvoegalgoritmen worden gebruikt om de vereiste rijen van elke invoertabel samen te voegen.

```sql
EXPLAIN statement
```

Als u de indeling van de reactie wilt definiëren, gebruikt u het trefwoord `FORMAT` met de opdracht `EXPLAIN` .

```sql
EXPLAIN FORMAT { TEXT | JSON } statement
```

| Parameters | Beschrijving |
| ------ | ------ |
| `FORMAT` | Gebruik de opdracht `FORMAT` om de uitvoerindeling op te geven. De beschikbare opties zijn `TEXT` of `JSON` . Niet-tekstuele uitvoer bevat dezelfde informatie als de indeling voor tekstuitvoer, maar kan gemakkelijker door programma&#39;s worden geparseerd. Deze parameter is standaard ingesteld op `TEXT` . |
| `statement` | Elke instructie `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `VALUES`, `EXECUTE`, `DECLARE`, `CREATE TABLE AS` of `CREATE MATERIALIZED VIEW AS` waarvan u het uitvoeringsplan wilt zien. |

>[!IMPORTANT]
>
>De uitvoer die een instructie `SELECT` retourneert, wordt genegeerd wanneer deze wordt uitgevoerd met het trefwoord `EXPLAIN` . Andere bijwerkingen van de instructie treden op zoals gebruikelijk.

**Voorbeeld**

In het volgende voorbeeld wordt het plan getoond voor een eenvoudige query op een tabel met één `integer` -kolom en 10000-rijen:

```sql
EXPLAIN SELECT * FROM foo;
```

```console
                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo (dataSetId = "6307eb92f90c501e072f8457", dataSetName = "foo") [0,1000000242,6973776840203d3d,6e616c58206c6153,6c6c6f430a3d4d20,74696d674c746365]
(1 row)
```

### FETCH

Met de opdracht `FETCH` haalt u rijen op met behulp van een eerder gemaakte cursor.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

| Parameters | Beschrijving |
| ------ | ------ |
| `num_of_rows` | Het aantal rijen dat moet worden opgehaald. |
| `cursor_name` | De naam van de curseur u informatie van terugwint. |

### PREPARE {#prepare}

Met de opdracht `PREPARE` kunt u een voorbereide instructie maken. Een voorbereide instructie is een object aan de serverzijde dat kan worden gebruikt om vergelijkbare SQL-instructies te sjablonen.

Bereide instructies kunnen parameters hebben. Dit zijn waarden die in de instructie worden vervangen wanneer deze wordt uitgevoerd. De parameters worden bedoeld door positie, gebruikend $1, $2, etc., wanneer het gebruiken van voorbereide verklaringen.

U kunt ook een lijst met parametergegevenstypen opgeven. Als het gegevenstype van een parameter niet wordt vermeld, kan het type van de context worden afgeleid.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

| Parameters | Beschrijving |
| ------ | ------ |
| `name` | De naam voor de voorbereide instructie. |
| `data_type` | De gegevenstypen van de parameters van de voorbereide instructie. Als het gegevenstype van een parameter niet wordt vermeld, kan het type van de context worden afgeleid. Als u meerdere gegevenstypen moet toevoegen, kunt u deze toevoegen in een lijst met door komma&#39;s gescheiden waarden. |

### ROLLBACK

De opdracht `ROLLBACK` maakt de huidige transactie ongedaan en verwijdert alle updates die door de transactie zijn aangebracht.

```sql
ROLLBACK
ROLLBACK WORK
```

### SELECTEREN IN

Met de opdracht `SELECT INTO` maakt u een nieuwe tabel en vult u deze met gegevens die door een query zijn berekend. De gegevens worden niet aan de client geretourneerd, omdat deze een normale opdracht `SELECT` hebben. De kolommen van de nieuwe lijst hebben de namen en de gegevenstypes verbonden aan de outputkolommen van het `SELECT` bevel.

```sql
[ WITH [ RECURSIVE ] with_query [, ...] ]
SELECT [ ALL | DISTINCT [ ON ( expression [, ...] ) ] ]
    * | expression [ [ AS ] output_name ] [, ...]
    INTO [ TEMPORARY | TEMP | UNLOGGED ] [ TABLE ] new_table
    [ FROM from_item [, ...] ]
    [ WHERE condition ]
    [ GROUP BY expression [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start [ ROW | ROWS ] ]
    [ FETCH { FIRST | NEXT } [ count ] { ROW | ROWS } ONLY ]
    [ FOR { UPDATE | SHARE } [ OF table_name [, ...] ] [ NOWAIT ] [...] ]
```

Meer informatie over de standaard UITGEZOCHTE vraagparameters kan in de [ UITGEZOCHTE vraagsectie ](#select-queries) worden gevonden. Deze sectie bevat alleen parameters die exclusief zijn voor de opdracht `SELECT INTO` .

| Parameters | Beschrijving |
| ------ | ------ |
| `TEMPORARY` of `TEMP` | Een optionele parameter. Als de parameter wordt gespecificeerd, is de gecreeerde lijst een tijdelijke lijst. |
| `UNLOGGED` | Een optionele parameter. Als de parameter wordt gespecificeerd, is de gecreeerde lijst een niet geregistreerde lijst. Meer informatie over niet-geregistreerde lijsten kan in de [[!DNL PostgreSQL]  documentatie ](https://www.postgresql.org/docs/current/sql-createtable.html) worden gevonden. |
| `new_table` | De naam van de tabel die moet worden gemaakt. |

**Voorbeeld**

Met de volgende query wordt een nieuwe tabel `films_recent` gemaakt die alleen bestaat uit recente items in de tabel `films` :

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### TONEN

De opdracht `SHOW` geeft de huidige instelling van runtimeparameters weer. Deze variabelen kunnen worden ingesteld met de instructie `SET` , door het configuratiebestand van `postgresql.conf` te bewerken, via de omgevingsvariabele `PGOPTIONS` (bij het gebruik van libpq of een libpq-toepassing) of via opdrachtregelmarkeringen wanneer de Postgres-server wordt gestart.

```sql
SHOW name
SHOW ALL
```

| Parameters | Beschrijving |
| ------ | ------ |
| `name` | De naam van de runtimeparameter waarover u informatie wilt. Mogelijke waarden voor de runtime parameter omvatten de volgende waarden:<br>`SERVER_VERSION`: Deze parameter toont het de versieaantal van de server.<br>`SERVER_ENCODING`: deze parameter toont de codering van de tekenset aan de serverzijde.<br>`LC_COLLATE`: deze parameter toont de landinstelling van de database voor sortering (tekstvolgorde).<br>`LC_CTYPE`: deze parameter toont de landinstelling van de database voor tekenclassificatie.<br>`IS_SUPERUSER`: Deze parameter laat zien of de huidige rol supergebruikersrechten heeft. |
| `ALL` | Toon de waarden van alle configuratieparameters met beschrijvingen. |

**Voorbeeld**

De volgende query toont de huidige instelling van de parameter `DateStyle` .

```sql
SHOW DateStyle;
```

```console
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### KOPIE

Met de opdracht `COPY` wordt de uitvoer van een `SELECT` -query naar een opgegeven locatie gedupliceerd. Deze opdracht is alleen succesvol als de gebruiker toegang heeft tot deze locatie.

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

| Parameters | Beschrijving |
| ------ | ------ |
| `query` | De query die u wilt kopiëren. |
| `format_name` | De indeling waarin u de query wilt kopiëren. De `format_name` kan een van `parquet` , `csv` of `json` zijn. De standaardwaarde is `parquet` . |

>[!NOTE]
>
>Het volledige uitvoerpad is `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### ALTER TABLE {#alter-table}

Met de opdracht `ALTER TABLE` kunt u primaire of buitenlandse toetsbeperkingen toevoegen of neerzetten en kolommen aan de tabel toevoegen.

#### BEPERKING TOEVOEGEN OF VERWIJDEREN

De volgende SQL-query&#39;s geven voorbeelden van het toevoegen of neerzetten van beperkingen aan een tabel. De primaire sleutel en de buitenlandse zeer belangrijke beperkingen kunnen aan veelvoudige kolommen met komma-gescheiden waarden worden toegevoegd. U kunt samengestelde sleutels tot stand brengen door twee of meer kolomnaamwaarden over te gaan zoals die in de voorbeelden hieronder worden gezien.

**bepalen primaire of samengestelde sleutels**

```sql
ALTER TABLE table_name ADD CONSTRAINT PRIMARY KEY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT PRIMARY KEY ( column_name1, column_name2 ) NAMESPACE namespace
```

**bepaalt een verband tussen lijsten die op één of meerdere sleutels worden gebaseerd**

```sql
ALTER TABLE table_name ADD CONSTRAINT FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT FOREIGN KEY ( column_name1, column_name2 ) REFERENCES referenced_table_name ( primary_column_name1, primary_column_name2 )
```

**bepaal een identiteitskolom**

```sql
ALTER TABLE table_name ADD CONSTRAINT PRIMARY IDENTITY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT IDENTITY ( column_name ) NAMESPACE namespace
```

**Daling een beperking/verhouding/identiteit**

```sql
ALTER TABLE table_name DROP CONSTRAINT PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT PRIMARY KEY ( column_name1, column_name2 )

ALTER TABLE table_name DROP CONSTRAINT FOREIGN KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT FOREIGN KEY ( column_name1, column_name2 )

ALTER TABLE table_name DROP CONSTRAINT PRIMARY IDENTITY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT IDENTITY ( column_name )
```

| Parameters | Beschrijving |
| ------ | ------ |
| `table_name` | De naam van de tabel die u bewerkt. |
| `column_name` | De naam van de kolom waaraan u een beperking toevoegt. |
| `referenced_table_name` | De naam van de tabel waarnaar wordt verwezen door de buitenlandse sleutel. |
| `primary_column_name` | De naam van de kolom waarnaar wordt verwezen door de buitenlandse sleutel. |

>[!NOTE]
>
>Het tabelschema moet uniek zijn en mag niet worden gedeeld door meerdere tabellen. Ook, is namespace verplicht voor primaire sleutel, primaire identiteit, en identiteitsbeperkingen.

#### Primaire en secundaire identiteiten toevoegen of verwijderen

Als u beperkingen voor zowel de kolommen van de primaire als de secundaire identiteitstabel wilt toevoegen of verwijderen, gebruikt u de opdracht `ALTER TABLE` .

De volgende voorbeelden voegen een primaire identiteit en een secundaire identiteit toe door beperkingen toe te voegen.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

Identiteiten kunnen ook worden verwijderd door beperkingen neer te zetten, zoals in het onderstaande voorbeeld wordt getoond.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

Voor meer gedetailleerde informatie, zie het document over [ plaatsende identiteiten in een ad hoc datasets ](../data-governance/ad-hoc-schema-identities.md).

#### KOLOM TOEVOEGEN

De volgende SQL-query&#39;s geven voorbeelden van het toevoegen van kolommen aan een tabel.

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

##### Ondersteunde gegevenstypen

In de volgende tabel worden de geaccepteerde gegevenstypen weergegeven voor het toevoegen van kolommen aan een tabel met [!DNL Postgres SQL] , XDM en [!DNL Accelerated Database Recovery] (ADR) in Azure SQL.

| — | PSQL-client | XDM | ADR | Beschrijving |
|---|---|---|---|---|
| 1 | `bigint` | `int8` | `bigint` | Een numeriek gegevenstype dat wordt gebruikt voor de opslag van grote gehele getallen tussen -9.223.372.036.854.775.807 en 9.223.372.036.854.775.807 in 8 bytes. |
| 2 | `integer` | `int4` | `integer` | Een numeriek gegevenstype dat wordt gebruikt om gehele getallen op te slaan, van -2.147.483.648 tot 2.147.483.647 in 4 bytes. |
| 3 | `smallint` | `int2` | `smallint` | Een numeriek gegevenstype dat wordt gebruikt voor het opslaan van gehele getallen tussen -32.768 en 215-1 32.767 in 2 bytes. |
| 4 | `tinyint` | `int1` | `tinyint` | Een numeriek gegevenstype dat wordt gebruikt om gehele getallen tussen 0 en 255 op te slaan in 1 byte. |
| 5 | `varchar(len)` | `string` | `varchar(len)` | Een gegevenstype van een teken dat een variabele grootte heeft. `varchar` kan het best worden gebruikt wanneer de grootte van de ingevoerde kolomgegevens aanzienlijk kan variëren. |
| 6 | `double` | `float8` | `double precision` | `FLOAT8` en `FLOAT` zijn geldige synoniemen voor `DOUBLE PRECISION` . `double precision` is een gegevenstype met drijvende komma. Zwevende-kommawaarden worden opgeslagen in 8 bytes. |
| 7 | `double precision` | `float8` | `double precision` | `FLOAT8` is een geldige synoniem voor `double precision` .`double precision` is een gegevenstype met drijvende komma. Zwevende-kommawaarden worden opgeslagen in 8 bytes. |
| 8 | `date` | `date` | `date` | De gegevenstypen van `date` zijn 4-byte opgeslagen kalenderdatumwaarden zonder tijdstempelinformatie. De geldige datumnotatie loopt van 01-01-0001 tot en met 12-31-9999. |
| 9 | `datetime` | `datetime` | `datetime` | Een gegevenstype dat wordt gebruikt om een instant in de tijd op te slaan, uitgedrukt als een kalenderdatum en tijd van dag. `datetime` bevat de kwalificatietekens: jaar, maand, dag, uur, seconde en fractie. Een declaratie `datetime` kan elke subset van deze tijdseenheden bevatten die in die reeks zijn samengevoegd, of bestaat zelfs uit slechts één tijdseenheid. |
| 10 | `char(len)` | `string` | `char(len)` | Het trefwoord `char(len)` wordt gebruikt om aan te geven dat het item een teken met een vaste lengte heeft. |

#### SCHEMA TOEVOEGEN

De volgende SQL-query toont een voorbeeld van het toevoegen van een tabel aan een database/schema.

```sql
ALTER TABLE table_name ADD SCHEMA database_name.schema_name
```

>[!NOTE]
>
> ADLS-tabellen en -weergaven kunnen niet worden toegevoegd aan DWH-databases / -schema&#39;s.


#### SCHEMA VERWIJDEREN

De volgende SQL-query toont een voorbeeld van het verwijderen van een tabel uit een database/schema.

```sql
ALTER TABLE table_name REMOVE SCHEMA database_name.schema_name
```

>[!NOTE]
>
> DWH-tabellen en -weergaven kunnen niet worden verwijderd uit fysiek gekoppelde DWH-databases/-schema&#39;s.


**Parameters**

| Parameters | Beschrijving |
| ------ | ------ |
| `table_name` | De naam van de tabel die u bewerkt. |
| `column_name` | De naam van de kolom die u wilt toevoegen. |
| `data_type` | Het gegevenstype van de kolom die u wilt toevoegen. Ondersteunde gegevenstypen zijn onder andere: bigint, char, string, date, datetime, double, double precision, integer, small int, tinyint, varchar. |

### PRIMAIRE TOETSEN TONEN

De opdracht `SHOW PRIMARY KEYS` geeft een overzicht van alle primaire toetsbeperkingen voor de opgegeven database.

```sql
SHOW PRIMARY KEYS
```

```console
    tableName | columnName    | datatype | namespace
------------------+----------------------+----------+-----------
 table_name_1 | column_name1  | text     | "ECID"
 table_name_2 | column_name2  | text     | "AAID"
```

### BUITENLANDSE TOETSEN TONEN

De opdracht `SHOW FOREIGN KEYS` geeft een overzicht van alle externe toetsbeperkingen voor de opgegeven database.

```sql
SHOW FOREIGN KEYS
```

```console
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```


### DATAGROEPEN TONEN

De opdracht `SHOW DATAGROUPS` retourneert een tabel met alle bijbehorende databases. Voor elke database bevat de tabel een schema, groepstype, onderliggend type, onderliggende naam en onderliggende id.

```sql
SHOW DATAGROUPS
```

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                       |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   adls_db     | adls_scheema      | ADLS      | Data Lake Table      | adls_table1                                        | 6149ff6e45cfa318a76ba6d3
   adls_db     | adls_scheema      | ADLS      | Accelerated Store | _table_demo1                                       | 22df56cf-0790-4034-bd54-d26d55ca6b21
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view1                                         | c2e7ddac-d41c-40c5-a7dd-acd41c80c5e9
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view4                                         | b280c564-df7e-405f-80c5-64df7ea05fc3
```


### DATAGROEPEN TONEN VOOR tabel

De opdracht `SHOW DATAGROUPS FOR 'table_name'` retourneert een tabel met alle gekoppelde databases die de parameter als onderliggend element bevatten. Voor elke database bevat de tabel een schema, groepstype, onderliggend type, onderliggende naam en onderliggende id.

```sql
SHOW DATAGROUPS FOR 'table_name'
```

**Parameters**

- `table_name`: De naam van de tabel waarvoor u gekoppelde databases wilt zoeken.

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                      |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   dwh_db_demo | schema2           | QSACCEL   | Accelerated Store | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   dwh_db_demo | schema1           | QSACCEL   | Accelerated Store | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   qsaccel     | profile_aggs      | QSACCEL   | Accelerated Store | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
```
