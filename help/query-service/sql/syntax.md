---
keywords: Experience Platform;home;populaire onderwerpen;queryservice;Query-service;sql syntaxis;sql;ctas;CTAS;Tabel maken als selectie
solution: Experience Platform
title: SQL-syntaxis in Query-service
topic-legacy: syntax
description: In dit document wordt SQL-syntaxis weergegeven die wordt ondersteund door Adobe Experience Platform Query Service.
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
source-git-commit: 5ec37ee797ec297b2e5c275dc0e6091e4ee8ecae
workflow-type: tm+mt
source-wordcount: '3160'
ht-degree: 2%

---

# SQL-syntaxis in Query Service

Adobe Experience Platform Query Service biedt de mogelijkheid om standaard ANSI SQL te gebruiken voor `SELECT` instructies en andere beperkte opdrachten. In dit document wordt de SQL-syntaxis beschreven die wordt ondersteund door [!DNL Query Service].

## Vragen SELECTEREN {#select-queries}

De volgende syntaxis definieert een `SELECT` query ondersteund door [!DNL Query Service]:

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

waar `from_item` Dit kan een van de volgende opties zijn:

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

en `grouping_element` Dit kan een van de volgende opties zijn:

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

en `with_query` is:

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
```

De volgende subsecties bevatten details over extra clausules die u in uw vragen kunt gebruiken, op voorwaarde dat zij het hierboven geschetste formaat volgen.

### component SNAPSHOT

Deze clausule kan worden gebruikt om gegevens over een lijst incrementeel te lezen die op momentopname IDs wordt gebaseerd. Een momentopname identiteitskaart is een controlepuntteller die door een aantal wordt vertegenwoordigd van het type Long dat op een lijst van het gegevenshoeveeltal wordt toegepast telkens als het gegeven aan het wordt geschreven. De `SNAPSHOT` -component wordt gekoppeld aan de tabelrelatie die naast de component wordt gebruikt.

```sql
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
```

#### Voorbeeld

```sql
SELECT * FROM Customers SNAPSHOT SINCE 123;

SELECT * FROM Customers SNAPSHOT AS OF 345;

SELECT * FROM Customers SNAPSHOT BETWEEN 123 AND 345;

SELECT * FROM Customers SNAPSHOT BETWEEN HEAD AND 123;

SELECT * FROM Customers SNAPSHOT BETWEEN 345 AND TAIL;

SELECT * FROM (SELECT id FROM CUSTOMERS BETWEEN 123 AND 345) C 

SELECT * FROM Customers SNAPSHOT SINCE 123 INNER JOIN Inventory AS OF 789 ON Customers.id = Inventory.id;
```

Houd er rekening mee dat een `SNAPSHOT` clausule werkt met een lijst of lijstalias maar niet bovenop een sub-vraag of een mening. A `SNAPSHOT` clausule zal overal werken `SELECT` de vraag op een lijst kan worden toegepast.

Bovendien kunt u `HEAD` en `TAIL` als speciale verschuivingswaarden voor momentopnameclausules. Gebruiken `HEAD` verwijst naar een verschuiving vóór de eerste opname, terwijl `TAIL` verwijst naar een verschuiving na de laatste opname.

>[!NOTE]
>
>Als u tussen twee momentopname IDs en de beginmomentopname vraagt is verlopen, kunnen de volgende twee scenario&#39;s voorkomen, afhankelijk van als de facultatieve fallback gedragsvlag (`resolve_fallback_snapshot_on_failure`) is ingesteld:
>
>- Als de facultatieve fallback gedragsvlag wordt geplaatst, zal de Dienst van de Vraag de vroegste beschikbare momentopname kiezen, zal het als beginmomentopname plaatsen, en de gegevens tussen de vroegste beschikbare momentopname en de gespecificeerde eindmomentopname terugkeren. Deze gegevens zijn **inclusief** van de vroegste beschikbare momentopname.
>
>- Als de optionele fallback-gedragmarkering niet is ingesteld, wordt een fout geretourneerd.


### WHERE-component

Standaard worden overeenkomsten gemaakt door een `WHERE` clausule inzake een `SELECT` de vraag is case-sensitive. Als u wilt dat overeenkomsten hoofdlettergevoelig zijn, kunt u het trefwoord `ILIKE` in plaats van `LIKE`.

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

A `SELECT` query die gebruikmaakt van verbindingen heeft de volgende syntaxis:

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### UNIE, INTERSECT EN BEHALVE

De `UNION`, `INTERSECT`, en `EXCEPT` de clausules worden gebruikt om als rijen van twee of meer lijsten te combineren of uit te sluiten:

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### TABEL MAKEN ALS SELECT

De volgende syntaxis definieert een `CREATE TABLE AS SELECT` (CTAS)-query:

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false') ] AS (select_query)
```

| Parameters | Beschrijving |
| ----- | ----- |
| `schema` | De titel van het XDM-schema. Gebruik deze clausule slechts als u wenst om een bestaand schema XDM voor de nieuwe dataset te gebruiken die door de vraag CTAS wordt gecreeerd. |
| `rowvalidation` | (Optioneel) Hiermee wordt aangegeven of de gebruiker validatie op rijniveau wil toepassen voor alle nieuwe batches die worden ingevoerd voor de nieuwe gegevensset. De standaardwaarde is `true`. |
| `select_query` | A `SELECT` instructie. De syntaxis van de `SELECT` query kan worden gevonden in de [Sectie Vragen SELECTEREN](#select-queries). |

**Voorbeeld**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>De `SELECT` instructie moet een alias hebben voor de statistische functies, zoals `COUNT`, `SUM`, `MIN`, enzovoort. Daarnaast worden de `SELECT` -instructie kan worden opgegeven met of zonder haakjes (). U kunt een `SNAPSHOT` clausule om stijgende delta&#39;s in de doellijst te lezen.

## INVOEGEN IN

De `INSERT INTO` wordt als volgt gedefinieerd:

```sql
INSERT INTO table_name select_query
```

| Parameters | Beschrijving |
| ----- | ----- |
| `table_name` | De naam van de tabel waarin u de query wilt invoegen. |
| `select_query` | A `SELECT` instructie. De syntaxis van de `SELECT` query kan worden gevonden in de [Sectie Vragen SELECTEREN](#select-queries). |

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
> De `SELECT` statement **mogen** tussen haakjes (). Bovendien, het schema van het resultaat van `SELECT` moet voldoen aan de tabel in het `INSERT INTO` instructie. U kunt een `SNAPSHOT` clausule om stijgende delta&#39;s in de doellijst te lezen.

De meeste velden in een echt XDM-schema zijn niet gevonden op het hoofdniveau en SQL staat het gebruik van puntnotatie niet toe. Als u een realistisch resultaat wilt bereiken met geneste velden, moet u elk veld in uw `INSERT INTO` pad.

Naar `INSERT INTO` geneste paden, gebruik de volgende syntaxis:

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

De `DROP TABLE` een bestaande tabel neerzet en de aan de tabel gekoppelde map uit het bestandssysteem verwijdert als dit geen externe tabel is. Als de tabel niet bestaat, treedt een uitzondering op.

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

| Parameters | Beschrijving |
| ------ | ------ |
| `IF EXISTS` | Als dit wordt opgegeven, wordt geen uitzondering gegenereerd als de tabel wel **niet** bestaan. |

## DATABASE MAKEN

De `CREATE DATABASE` maakt een ADLS-database.

```sql
CREATE DATABASE [IF NOT EXISTS] db_name
```

## DATABASE DROP

De `DROP DATABASE` verwijdert de database uit een instantie.

```sql
DROP DATABASE [IF EXISTS] db_name
```

| Parameters | Beschrijving |
| ------ | ------ |
| `IF EXISTS` | Als dit wordt gespecificeerd, wordt geen uitzondering geworpen als het gegevensbestand doet **niet** bestaan. |

## DROP SCHEMA

De `DROP SCHEMA` een bestaand schema neerzet.

```sql
DROP SCHEMA [IF EXISTS] db_name.schema_name [ RESTRICT | CASCADE]
```

| Parameters | Beschrijving |
| ------ | ------ |
| `IF EXISTS` | Als dit wordt gespecificeerd, wordt geen uitzondering geworpen als het schema doet **niet** bestaan. |
| `RESTRICT` | Standaardwaarde voor de modus. Als dit wordt gespecificeerd, zal het schema slechts vallen als het **niet** bevatten tabellen. |
| `CASCADE` | Als dit wordt gespecificeerd, zal het schema samen met alle lijsten huidig in het schema worden gelaten vallen. |

## WEERGAVE MAKEN

De volgende syntaxis definieert een `CREATE VIEW` query:

```sql
CREATE VIEW view_name AS select_query
```

| Parameters | Beschrijving |
| ------ | ------ |
| `view_name` | De naam van de weergave die moet worden gemaakt. |
| `select_query` | A `SELECT` instructie. De syntaxis van de `SELECT` query kan worden gevonden in de [Sectie Vragen SELECTEREN](#select-queries). |

**Voorbeeld**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

## DROP VIEW

De volgende syntaxis definieert een `DROP VIEW` query:

```sql
DROP VIEW [IF EXISTS] view_name
```

| Parameters | Beschrijving |
| ------ | ------ |
| `IF EXISTS` | Als dit wordt opgegeven, wordt geen uitzondering gegenereerd als de weergave **niet** bestaan. |
| `view_name` | De naam van de weergave die moet worden verwijderd. |

**Voorbeeld**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## Anoniem blok

Een anoniem blok bestaat uit twee secties: secties voor uitvoerbaar en uitzonderingsbeheer. In een anoniem blok, is de uitvoerbare sectie verplicht. De sectie voor de afhandeling van uitzonderingen is echter optioneel.

In het volgende voorbeeld ziet u hoe u een blok maakt met een of meer instructies die samen moeten worden uitgevoerd:

```sql
BEGIN
  statementList
[EXCEPTION exceptionHandler]
END

exceptionHandler:
      WHEN OTHER
      THEN statementList

statementList:
    : (statement (';')) +
```

Hieronder ziet u een voorbeeld waarin anonieme blokken worden gebruikt.

```sql
BEGIN
   SET @v_snapshot_from = select parent_id  from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_snapshot_to = select snapshot_id from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_log_id = select now();
   CREATE TABLE tracking_email_id_incrementally
     AS SELECT _id AS id FROM email_tracking_experience_event_dataset SNAPSHOT BETWEEN @v_snapshot_from AND @v_snapshot_to;

EXCEPTION
  WHEN OTHER THEN
    DROP TABLE IF EXISTS tracking_email_id_incrementally;
    SELECT 'ERROR';
END;
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

Zie de handleiding op [logische organisatie van gegevenselementen](../best-practices/organize-data-assets.md) voor meer een gedetailleerde verklaring over de beste praktijken van de Dienst van de Vraag.

## Tabel bestaat

De `table_exists` SQL het bevel wordt gebruikt om te bevestigen of een lijst momenteel in het systeem bestaat of niet. De opdracht retourneert een Booleaanse waarde: `true` if de tabel **doet** bestaan, en `false` als de tabel dat doet **niet** bestaan.

Door te controleren of een tabel bestaat voordat de instructies worden uitgevoerd, `table_exists` de functie vereenvoudigt het schrijven van een anoniem blok om zowel het `CREATE` en `INSERT INTO` gebruik.

De volgende syntaxis definieert de `table_exists` opdracht:

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

De `inline` De functie scheidt de elementen van een serie van structs en produceert de waarden in een lijst. Het kan alleen in het dialoogvenster `SELECT` lijst of een `LATERAL VIEW`.

De `inline` function **kan** worden geplaatst in een uitgezocht lijst waar er andere generatorfuncties zijn.

Door gebrek, worden de geproduceerde kolommen genoemd &quot;col1&quot;, &quot;col2&quot;, etc. Als de expressie `NULL` dan worden geen rijen geproduceerd.

>[!TIP]
>
>De namen van kolommen kunnen worden hernoemd met de `RENAME` gebruiken.

**Voorbeeld**

```sql
> SELECT inline(array(struct(1, 'a'), struct(2, 'b'))), 'Spark SQL';
```

In het voorbeeld wordt het volgende geretourneerd:

```text
1  a Spark SQL
2  b Spark SQL
```

In dit tweede voorbeeld worden het concept en de toepassing van het `inline` functie. Het gegevensmodel voor het voorbeeld wordt in de onderstaande afbeelding weergegeven.

![Een schemadiagram voor productListItems](../images/sql/productListItems.png)

**Voorbeeld**

```sql
select inline(productListItems) from source_dataset limit 10;
```

De uit de `source_dataset` worden gebruikt om de doeltabel te vullen.

| SKU | _experience | hoeveelheid | priceTotal |
|---------------------|-----------------------------------|----------|--------------|
| product-id-1 | (&quot;(&quot;(&quot;(&quot;(A,pas,B,NULL)&quot;)&quot;)&quot;) | 5 | 10,5 |
| product-id-5 | (&quot;(&quot;(&quot;(A, pass, B, NULL)&quot;)&quot;) |  |  |
| product-id-2 | (&quot;(&quot;(&quot;(&quot;(AF, C, D, NULL)&quot;)&quot;)&quot;) | 6 | 40 |
| product-id-4 | (&quot;(&quot;(&quot;(&quot;(BM, pass, NA, NULL)&quot;)&quot;)&quot;) | 3 | 12 |

## [!DNL Spark] SQL-opdrachten

De subsectie hieronder behandelt de SQL bevelen van de Vonk die door de Dienst van de Vraag worden gesteund.

### SET

De `SET` plaatst een bevel een bezit en of keert de waarde van een bestaand bezit terug of maakt een lijst van alle bestaande eigenschappen. Als een waarde wordt opgegeven voor een bestaande eigenschapsleutel, wordt de oude waarde overschreven.

```sql
SET property_key = property_value
```

| Parameters | Beschrijving |
| ------ | ------ |
| `property_key` | De naam van de eigenschap die u wilt weergeven of wijzigen. |
| `property_value` | De waarde waarop u de eigenschap wilt instellen. |

Als u de waarde voor een instelling wilt retourneren, gebruikt u `SET [property key]` zonder `property_value`.

## PostgreSQL-opdrachten

De subsecties hieronder behandelen de bevelen PostgreSQL die door de Dienst van de Vraag worden gesteund.

### TABEL ANALYSEREN

De `ANALYZE TABLE` het bevel berekent statistieken voor een lijst op de versnelde opslag. De statistieken worden berekend over uitgevoerde vragen CTAS of ITAS voor een bepaalde lijst op versnelde opslag.

**Voorbeeld**

```sql
ANALYZE TABLE <original_table_name>
```

Hieronder volgt een lijst met statistische berekeningen die beschikbaar zijn na gebruik van de `ANALYZE TABLE` opdracht:-

| Berekende waarden | Beschrijving |
|---|---|
| `field` | De naam van de kolom in een tabel. |
| `data-type` | Het acceptabele type gegevens voor elke kolom. |
| `count` | Het aantal rijen dat een waarde bevat die niet gelijk is aan null voor dit veld. |
| `distinct-count` | Het aantal unieke of verschillende waarden voor dit veld. |
| `missing` | Het aantal rijen met een null-waarde voor dit veld. |
| `max` | De maximumwaarde uit de geanalyseerde tabel. |
| `min` | De minimumwaarde uit de geanalyseerde tabel. |
| `mean` | De gemiddelde waarde van de geanalyseerde tabel. |
| `stdev` | De standaardafwijking van de geanalyseerde tabel. |

### BEGINNEN

De `BEGIN` of als alternatief de `BEGIN WORK` of `BEGIN TRANSACTION` , wordt een transactieblok gestart. Om het even welke verklaringen die na het begin bevel worden ingevoerd zullen in één enkele transactie worden uitgevoerd tot een expliciete COMMIT of bevel ROLLBACK wordt gegeven. Deze opdracht is gelijk aan `START TRANSACTION`.

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### SLUITEN

De `CLOSE` maakt de middelen vrij verbonden aan een open curseur. Nadat de cursor is gesloten, zijn er geen verdere bewerkingen meer toegestaan. Een cursor moet worden gesloten wanneer deze niet meer nodig is.

```sql
CLOSE name
CLOSE ALL
```

Indien `CLOSE name` wordt gebruikt, `name` vertegenwoordigt de naam van een open curseur die moet worden gesloten. Indien `CLOSE ALL` wordt gebruikt, worden alle open cursors gesloten.

### VERWIJDEREN

De `DEALLOCATE` kunt u een eerder voorbereide SQL-instructie opnieuw opzoeken. Als u een voorbereide instructie niet expliciet zoekt, wordt de toewijzing ongedaan gemaakt wanneer de sessie wordt beëindigd. Meer informatie over voorbereide instructies vindt u in het gedeelte [PREPARE, opdracht](#prepare) sectie.

```sql
DEALLOCATE name
DEALLOCATE ALL
```

Indien `DEALLOCATE name` wordt gebruikt, `name` staat voor de naam van de voorbereide instructie die moet worden gedetoewijzingsd. Indien `DEALLOCATE ALL` wordt gebruikt, worden alle voorbereide instructies gedeallocatie.

### VERKLAREN

De `DECLARE` staat een gebruiker toe om een curseur tot stand te brengen, die kan worden gebruikt om een klein aantal rijen uit een grotere vraag terug te winnen. Nadat de cursor is gemaakt, worden er rijen uit opgehaald met `FETCH`.

```sql
DECLARE name CURSOR FOR query
```

| Parameters | Beschrijving |
| ------ | ------ |
| `name` | De naam van de cursor die moet worden gemaakt. |
| `query` | A `SELECT` of `VALUES` bevel dat de rijen verstrekt die door de curseur moeten zijn teruggekeerd. |

### UITVOEREN

De `EXECUTE` wordt gebruikt om een eerder voorbereide instructie uit te voeren. Aangezien voorbereide instructies alleen bestaan voor de duur van een sessie, moet de voorbereide instructie zijn gemaakt door een `PREPARE` eerder in de huidige sessie uitgevoerd. Meer informatie over het gebruik van voorbereide instructies vindt u in het gedeelte [`PREPARE` command](#prepare) sectie.

Als de `PREPARE` een instructie die de instructie heeft gemaakt, bepaalde parameters heeft opgegeven, moet een compatibele set parameters worden doorgegeven aan de `EXECUTE` instructie. Als deze parameters niet binnen worden overgegaan, zal een fout worden opgeheven.

```sql
EXECUTE name [ ( parameter ) ]
```

| Parameters | Beschrijving |
| ------ | ------ |
| `name` | De naam van de voorbereide instructie die moet worden uitgevoerd. |
| `parameter` | De werkelijke waarde van een parameter voor de voorbereide instructie. Dit moet een expressie zijn die een waarde oplevert die compatibel is met het gegevenstype van deze parameter, zoals bepaald toen de voorbereide instructie werd gemaakt.  Als er meerdere parameters zijn voor de voorbereide instructie, worden deze door komma&#39;s gescheiden. |

### VERKLAREN

De `EXPLAIN` toont het bevel het uitvoeringsplan voor de geleverde verklaring. In het uitvoeringsplan ziet u hoe de tabellen waarnaar door de instructie wordt verwezen, worden gescand.  Als er naar meerdere tabellen wordt verwezen, wordt aangegeven welke samenvoegalgoritmen worden gebruikt om de vereiste rijen van elke invoertabel samen te voegen.

```sql
EXPLAIN statement
```

Gebruik de `FORMAT` trefwoord met de `EXPLAIN` gebruiken om de indeling van de reactie te definiëren.

```sql
EXPLAIN FORMAT { TEXT | JSON } statement
```

| Parameters | Beschrijving |
| ------ | ------ |
| `FORMAT` | Gebruik de `FORMAT` gebruiken om de uitvoerindeling op te geven. De beschikbare opties zijn `TEXT` of `JSON`. Niet-tekstuele uitvoer bevat dezelfde informatie als de indeling voor tekstuitvoer, maar kan gemakkelijker door programma&#39;s worden geparseerd. Deze parameter wordt standaard ingesteld op `TEXT`. |
| `statement` | Alle `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `VALUES`, `EXECUTE`, `DECLARE`, `CREATE TABLE AS`, of `CREATE MATERIALIZED VIEW AS` de verklaring, waarvan uitvoeringsplan u wilt zien. |

>[!IMPORTANT]
>
>Elke uitvoer die een `SELECT` de verklaring zou kunnen terugkeren wordt verworpen wanneer looppas met `EXPLAIN` trefwoord. Andere bijwerkingen van de instructie treden op zoals gebruikelijk.

**Voorbeeld**

Het volgende voorbeeld toont het plan voor een eenvoudige vraag op een lijst met één enkele `integer` kolom en 10000 rijen:

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

De `FETCH` Hiermee worden rijen opgehaald met een eerder gemaakte cursor.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

| Parameters | Beschrijving |
| ------ | ------ |
| `num_of_rows` | Het aantal rijen dat moet worden opgehaald. |
| `cursor_name` | De naam van de curseur u informatie van terugwint. |

### PREPARE {#prepare}

De `PREPARE` kunt u een voorbereide instructie maken. Een voorbereide instructie is een serverobject dat kan worden gebruikt om vergelijkbare SQL-instructies te sjablonen.

Bereide instructies kunnen parameters hebben. Dit zijn waarden die in de instructie worden vervangen wanneer deze wordt uitgevoerd. Parameters worden naar positie verwezen, waarbij $1, $2, enz. wordt gebruikt bij het gebruik van voorbereide instructies.

U kunt ook een lijst met parametergegevenstypen opgeven. Als het gegevenstype van een parameter niet wordt vermeld, kan het type van de context worden afgeleid.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

| Parameters | Beschrijving |
| ------ | ------ |
| `name` | De naam voor de voorbereide instructie. |
| `data_type` | De gegevenstypen van de parameters van de voorbereide instructie. Als het gegevenstype van een parameter niet wordt vermeld, kan het type van de context worden afgeleid. Als u meerdere gegevenstypen wilt toevoegen, kunt u deze toevoegen in een door komma&#39;s gescheiden lijst. |

### ROLLBACK

De `ROLLBACK` maakt het bevel de huidige transactie ongedaan en verwerpt alle updates die door de transactie worden gemaakt.

```sql
ROLLBACK
ROLLBACK WORK
```

### SELECTEREN IN

De `SELECT INTO` maakt een nieuwe tabel en vult deze met gegevens die door een query zijn berekend. De gegevens worden niet aan de client geretourneerd, omdat ze normaal zijn `SELECT` gebruiken. De kolommen van de nieuwe lijst hebben de namen en de gegevenstypes verbonden aan de outputkolommen van `SELECT` gebruiken.

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

Meer informatie over de standaard SELECT-queryparameters vindt u in het gedeelte [Query-sectie SELECTEREN](#select-queries). In deze sectie worden alleen parameters vermeld die exclusief zijn voor de `SELECT INTO` gebruiken.

| Parameters | Beschrijving |
| ------ | ------ |
| `TEMPORARY` of `TEMP` | Een optionele parameter. Indien gespecificeerd, zal de lijst die wordt gecreeerd een tijdelijke lijst zijn. |
| `UNLOGGED` | Een optionele parameter. Indien gespecificeerd, zal de lijst die zoals wordt gecreeerd een niet geregistreerde lijst zijn. Meer informatie over niet-geregistreerde tabellen vindt u in de [PostSQL-documentatie](https://www.postgresql.org/docs/current/sql-createtable.html). |
| `new_table` | De naam van de tabel die moet worden gemaakt. |

**Voorbeeld**

Met de volgende query wordt een nieuwe tabel gemaakt `films_recent` bestaande uit alleen recente gegevens uit de tabel `films`:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### TONEN

De `SHOW` geeft de huidige instelling van runtimeparameters weer. Deze variabelen kunnen worden ingesteld met de `SET` door de `postgresql.conf` configuratiebestand, via de `PGOPTIONS` omgevingsvariabele (bij gebruik van libpq of een libpq-toepassing) of opdrachtregelmarkeringen wanneer de Postgres-server wordt gestart.

```sql
SHOW name
SHOW ALL
```

| Parameters | Beschrijving |
| ------ | ------ |
| `name` | De naam van de runtimeparameter waarover u informatie wilt. Mogelijke waarden voor de runtime parameter zijn de volgende waarden:<br>`SERVER_VERSION`: Deze parameter toont het versienummer van de server.<br>`SERVER_ENCODING`: Deze parameter toont de codering van de tekenset aan de serverzijde.<br>`LC_COLLATE`: Deze parameter toont de landinstelling van de database voor sortering (tekstvolgorde).<br>`LC_CTYPE`: Deze parameter toont de landinstelling van de database voor tekenclassificatie.<br>`IS_SUPERUSER`: Deze parameter toont of heeft de huidige rol supergebruikersvoorrechten. |
| `ALL` | Toon de waarden van alle configuratieparameters met beschrijvingen. |

**Voorbeeld**

De volgende vraag toont het huidige plaatsen van de parameter `DateStyle`.

```sql
SHOW DateStyle;
```

```console
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### KOPIËREN

De `COPY` bevel dupliceert de output van om het even welk `SELECT` zoeken naar een opgegeven locatie. Deze opdracht is alleen succesvol als de gebruiker toegang heeft tot deze locatie.

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

| Parameters | Beschrijving |
| ------ | ------ |
| `query` | De query die u wilt kopiëren. |
| `format_name` | De indeling waarin u de query wilt kopiëren. De `format_name` kan één van `parquet`, `csv`, of `json`. De standaardwaarde is `parquet`. |

>[!NOTE]
>
>Het volledige uitvoerpad wordt `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### ALTER TABLE {#alter-table}

De `ALTER TABLE` Met deze opdracht kunt u primaire of buitenlandse toetsbeperkingen toevoegen of neerzetten en kolommen aan de tabel toevoegen.


#### BEPERKING TOEVOEGEN OF VERWIJDEREN

De volgende SQL-query&#39;s geven voorbeelden van het toevoegen of neerzetten van beperkingen aan een tabel.

```sql
ALTER TABLE table_name ADD CONSTRAINT PRIMARY KEY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT PRIMARY IDENTITY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT IDENTITY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name DROP CONSTRAINT PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT FOREIGN KEY ( column_name )

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
>Het tabelschema moet uniek zijn en mag niet worden gedeeld door meerdere tabellen. Bovendien, is namespace verplicht voor primaire sleutel, primaire identiteit, en identiteitsbeperkingen.

#### Primaire en secundaire identiteiten toevoegen of verwijderen

De `ALTER TABLE` bevel staat u toe om beperkingen voor zowel primaire als secundaire kolommen van de identiteitslijst direct door SQL toe te voegen of te schrappen.

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

Document weergeven op [het plaatsen van identiteiten in een ad hoc datasets](../data-governance/ad-hoc-schema-identities.md) voor meer gedetailleerde informatie.

#### KOLOM TOEVOEGEN

De volgende SQL-query&#39;s geven voorbeelden van het toevoegen van kolommen aan een tabel.

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

##### Ondersteunde gegevenstypen

De volgende lijst maakt een lijst van de toegelaten gegevenstypes voor het toevoegen van kolommen aan een lijst met [!DNL Postgres SQL], XDM en de [!DNL Accelerated Database Recovery] (ADR) in Azure SQL.

| — | PSQL-client | XDM | ADR | Beschrijving |
|---|---|---|---|---|
| 1 | `bigint` | `int8` | `bigint` | Een numeriek gegevenstype dat wordt gebruikt voor de opslag van grote gehele getallen tussen -9.223.372.036.854.775.807 en 9.223.372.036.854.775.807 in 8 bytes. |
| 2 | `integer` | `int4` | `integer` | Een numeriek gegevenstype dat wordt gebruikt om gehele getallen op te slaan, van -2.147.483.648 tot 2.147.483.647 in 4 bytes. |
| 3 | `smallint` | `int2` | `smallint` | Een numeriek gegevenstype dat wordt gebruikt voor het opslaan van gehele getallen tussen -32.768 en 215-1 32.767 in 2 bytes. |
| 4 | `tinyint` | `int1` | `tinyint` | Een numeriek gegevenstype dat wordt gebruikt om gehele getallen tussen 0 en 255 op te slaan in 1 byte. |
| 5 | `varchar(len)` | `string` | `varchar(len)` | Een gegevenstype van een teken dat een variabele grootte heeft. `varchar` wordt het best gebruikt wanneer de grootte van de ingangen van kolomgegevens aanzienlijk varieert. |
| 6 | `double` | `float8` | `double precision` | `FLOAT8` en `FLOAT` zijn geldige synoniemen voor `DOUBLE PRECISION`. `double precision` is een gegevenstype met drijvende komma. Zwevende-kommawaarden worden opgeslagen in 8 bytes. |
| 7 | `double precision` | `float8` | `double precision` | `FLOAT8` is een geldige synoniem voor `double precision`.`double precision` is een gegevenstype met drijvende komma. Zwevende-kommawaarden worden opgeslagen in 8 bytes. |
| 8 | `date` | `date` | `date` | De `date` Het gegevenstype is 4-byte opgeslagen kalenderdatumwaarden zonder tijdstempelinformatie. De geldige datumnotatie loopt van 01-01-0001 tot en met 12-31-9999. |
| 9 | `datetime` | `datetime` | `datetime` | Een gegevenstype dat wordt gebruikt om een instant in de tijd op te slaan, uitgedrukt als een kalenderdatum en tijd van dag. `datetime` omvat de kwalificatoren van: jaar, maand, dag, uur, seconde, en fractie. A `datetime` de verklaring kan om het even welke ondergroep van deze tijdeenheden omvatten die in die opeenvolging worden aangesloten, of zelfs slechts één enkele tijdeenheid omvatten. |
| 10 | `char(len)` | `string` | `char(len)` | De `char(len)` trefwoord wordt gebruikt om aan te geven dat het item een teken met een vaste lengte is. |

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
| `data_type` | Het gegevenstype van de kolom die u wilt toevoegen. Tot de ondersteunde gegevenstypen behoren: bigint, char, string, date, datetime, double, double precision, integer, small int, tinyint, varchar. |

### PRIMAIRE TOETSEN TONEN

De `SHOW PRIMARY KEYS` bevel maakt een lijst van alle primaire zeer belangrijke beperkingen voor het bepaalde gegevensbestand.

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

De `SHOW FOREIGN KEYS` bevel maakt een lijst van alle buitenlandse zeer belangrijke beperkingen voor het bepaalde gegevensbestand.

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

De `SHOW DATAGROUPS` keert een lijst van alle bijbehorende gegevensbestanden terug. Voor elke database bevat de tabel een schema, een groepstype, een onderliggend type, een onderliggende naam en een onderliggende id.

```sql
SHOW DATAGROUPS
```

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                       |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   adls_db     | adls_scheema      | ADLS      | Data Lake Table      | adls_table1                                        | 6149ff6e45cfa318a76ba6d3
   adls_db     | adls_scheema      | ADLS      | Data Warehouse Table | _table_demo1                                       | 22df56cf-0790-4034-bd54-d26d55ca6b21
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view1                                         | c2e7ddac-d41c-40c5-a7dd-acd41c80c5e9
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view4                                         | b280c564-df7e-405f-80c5-64df7ea05fc3
```


### DATAGROEPEN TONEN VOOR tabel

De `SHOW DATAGROUPS FOR` Het bevel &#39;table_name&#39; keert een lijst van alle bijbehorende gegevensbestanden terug die de parameter als zijn kind bevatten. Voor elke database bevat de tabel een schema, een groepstype, een onderliggend type, een onderliggende naam en een onderliggende id.

```sql
SHOW DATAGROUPS FOR 'table_name'
```

**Parameters**

- `table_name`: De naam van de tabel waarvoor u gekoppelde databases wilt zoeken.

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                      |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   dwh_db_demo | schema2           | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   dwh_db_demo | schema1           | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   qsaccel     | profile_aggs      | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
```
