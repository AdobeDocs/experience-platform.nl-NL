---
keywords: Experience Platform;home;populaire onderwerpen;queryservice;Query-service;sql syntaxis;sql;ctas;CTAS;Tabel maken als selectie
solution: Experience Platform
title: SQL-syntaxis in Query-service
topic-legacy: syntax
description: In dit document wordt SQL-syntaxis weergegeven die wordt ondersteund door Adobe Experience Platform Query Service.
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
source-git-commit: b0cd372589be1db3d7ae571edaac68df9a3c493f
workflow-type: tm+mt
source-wordcount: '2207'
ht-degree: 1%

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

**Parameters**

- `schema`: De titel van het XDM-schema. Gebruik deze clausule slechts als u wenst om een bestaand schema XDM voor de nieuwe dataset te gebruiken die door de vraag CTAS wordt gecreeerd.
- `rowvalidation`: (Optioneel) Hiermee wordt aangegeven of de gebruiker validatie op rijniveau wil toepassen voor alle nieuwe batches die worden ingevoerd voor de nieuwe gegevensset. De standaardwaarde is `true`.
- `select_query`: A `SELECT` instructie. De syntaxis van de `SELECT` query kan worden gevonden in de [Sectie Vragen SELECTEREN](#select-queries).

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

**Parameters**

- `table_name`: De naam van de tabel waarin u de query wilt invoegen.
- `select_query`: A `SELECT` instructie. De syntaxis van de `SELECT` query kan worden gevonden in de [Sectie Vragen SELECTEREN](#select-queries).

**Voorbeeld**

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!NOTE]
> De `SELECT` statement **mogen** tussen haakjes (). Bovendien, het schema van het resultaat van `SELECT` moet voldoen aan de tabel in het `INSERT INTO` instructie. U kunt een `SNAPSHOT` clausule om stijgende delta&#39;s in de doellijst te lezen.

## DROP TABLE

De `DROP TABLE` een bestaande tabel neerzet en de aan de tabel gekoppelde map uit het bestandssysteem verwijdert als dit geen externe tabel is. Als de tabel niet bestaat, treedt een uitzondering op.

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

**Parameters**

- `IF EXISTS`: Als dit wordt opgegeven, wordt geen uitzondering gegenereerd als de tabel wel **niet** bestaan.

## DATABASE DROP

De `DROP DATABASE` een bestaande database neerzetten.

```sql
DROP DATABASE [IF EXISTS] db_name
```

**Parameters**

- `IF EXISTS`: Als dit wordt gespecificeerd, wordt geen uitzondering geworpen als het gegevensbestand doet **niet** bestaan.

## DROP SCHEMA

De `DROP SCHEMA` een bestaand schema neerzet.

```sql
DROP SCHEMA [IF EXISTS] db_name.schema_name [ RESTRICT | CASCADE]
```

**Parameters**

- `IF EXISTS`: Als dit wordt gespecificeerd, wordt geen uitzondering geworpen als het schema doet **niet** bestaan.

- `RESTRICT`: Standaardwaarde voor de modus. Als dit wordt gespecificeerd, zal het schema slechts vallen als het **niet** bevatten tabellen.

- `CASCADE`: Als dit wordt gespecificeerd, zal het schema samen met alle lijsten huidig in het schema worden gelaten vallen.

## WEERGAVE MAKEN

De volgende syntaxis definieert een `CREATE VIEW` query:

```sql
CREATE VIEW view_name AS select_query
```

**Parameters**

- `view_name`: De naam van de weergave die moet worden gemaakt.
- `select_query`: A `SELECT` instructie. De syntaxis van de `SELECT` query kan worden gevonden in de [Sectie Vragen SELECTEREN](#select-queries).

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

**Parameter**

- `IF EXISTS`: Als dit wordt opgegeven, wordt geen uitzondering gegenereerd als de weergave **niet** bestaan.
- `view_name`: De naam van de weergave die moet worden verwijderd.

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
$$
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
END$$;
```

## [!DNL Spark] SQL-opdrachten

De subsectie hieronder behandelt de SQL bevelen van de Vonk die door de Dienst van de Vraag worden gesteund.

### SET

De `SET` plaatst een bevel een bezit en of keert de waarde van een bestaand bezit terug of maakt een lijst van alle bestaande eigenschappen. Als een waarde wordt opgegeven voor een bestaande eigenschapsleutel, wordt de oude waarde overschreven.

```sql
SET property_key = property_value
```

**Parameters**

- `property_key`: De naam van de eigenschap die u wilt weergeven of wijzigen.
- `property_value`: De waarde waarop u de eigenschap wilt instellen.

Als u de waarde voor een instelling wilt retourneren, gebruikt u `SET [property key]` zonder `property_value`.

## PostgreSQL-opdrachten

De subsecties hieronder behandelen de bevelen PostgreSQL die door de Dienst van de Vraag worden gesteund.

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

**Parameters**

- `name`: De naam van de cursor die moet worden gemaakt.
- `query`: A `SELECT` of `VALUES` bevel dat de rijen verstrekt die door de curseur moeten zijn teruggekeerd.

### UITVOEREN

De `EXECUTE` wordt gebruikt om een eerder voorbereide instructie uit te voeren. Aangezien voorbereide instructies alleen bestaan voor de duur van een sessie, moet de voorbereide instructie zijn gemaakt door een `PREPARE` eerder in de huidige sessie uitgevoerd. Meer informatie over het gebruik van voorbereide instructies vindt u in het gedeelte [`PREPARE` command](#prepare) sectie.

Als de `PREPARE` een instructie die de instructie heeft gemaakt, bepaalde parameters heeft opgegeven, moet een compatibele set parameters worden doorgegeven aan de `EXECUTE` instructie. Als deze parameters niet binnen worden overgegaan, zal een fout worden opgeheven.

```sql
EXECUTE name [ ( parameter ) ]
```

**Parameters**

- `name`: De naam van de voorbereide instructie die moet worden uitgevoerd.
- `parameter`: De werkelijke waarde van een parameter voor de voorbereide instructie. Dit moet een expressie zijn die een waarde oplevert die compatibel is met het gegevenstype van deze parameter, zoals bepaald toen de voorbereide instructie werd gemaakt.  Als er meerdere parameters zijn voor de voorbereide instructie, worden deze door komma&#39;s gescheiden.

### VERKLAREN

De `EXPLAIN` toont het bevel het uitvoeringsplan voor de geleverde verklaring. In het uitvoeringsplan ziet u hoe de tabellen waarnaar door de instructie wordt verwezen, worden gescand.  Als er naar meerdere tabellen wordt verwezen, wordt aangegeven welke samenvoegalgoritmen worden gebruikt om de vereiste rijen van elke invoertabel samen te voegen.

```sql
EXPLAIN option statement
```

Wanneer `option` kan één van zijn:

```sql
ANALYZE
FORMAT { TEXT | JSON }
```

**Parameters**

- `ANALYZE`: Als de `option` contains `ANALYZE`, worden de runtime en andere statistieken weergegeven.
- `FORMAT`: Als de `option` contains `FORMAT`wordt de uitvoerindeling opgegeven die `TEXT` of `JSON`. Niet-tekstuele uitvoer bevat dezelfde informatie als de indeling voor tekstuitvoer, maar kan gemakkelijker door programma&#39;s worden geparseerd. Deze parameter wordt standaard ingesteld op `TEXT`.
- `statement`: Alle `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `VALUES`, `EXECUTE`, `DECLARE`, `CREATE TABLE AS`, of `CREATE MATERIALIZED VIEW AS` de verklaring, waarvan uitvoeringsplan u wilt zien.

>[!IMPORTANT]
>
>Houd er rekening mee dat de instructie daadwerkelijk wordt uitgevoerd wanneer de instructie `ANALYZE` wordt gebruikt. Hoewel `EXPLAIN` verwijdert uitvoer die een `SELECT` retourneert, treden andere bijwerkingen van de instructie op zoals gewoonlijk.

**Voorbeeld**

Het volgende voorbeeld toont het plan voor een eenvoudige vraag op een lijst met één enkele `integer` kolom en 10000 rijen:

```sql
EXPLAIN SELECT * FROM foo;
```

```console
                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)
(1 row)
```

### FETCH

De `FETCH` Hiermee worden rijen opgehaald met een eerder gemaakte cursor.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

**Parameters**

- `num_of_rows`: Het aantal rijen dat moet worden opgehaald.
- `cursor_name`: De naam van de curseur u informatie van terugwint.

### PREPARE {#prepare}

De `PREPARE` kunt u een voorbereide instructie maken. Een voorbereide instructie is een serverobject dat kan worden gebruikt om vergelijkbare SQL-instructies te sjablonen.

Bereide instructies kunnen parameters hebben. Dit zijn waarden die in de instructie worden vervangen wanneer deze wordt uitgevoerd. Parameters worden naar positie verwezen, waarbij $1, $2, enz. wordt gebruikt bij het gebruik van voorbereide instructies.

U kunt ook een lijst met parametergegevenstypen opgeven. Als het gegevenstype van een parameter niet wordt vermeld, kan het type van de context worden afgeleid.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

**Parameters**

- `name`: De naam voor de voorbereide instructie.
- `data_type`: De gegevenstypen van de parameters van de voorbereide instructie. Als het gegevenstype van een parameter niet wordt vermeld, kan het type van de context worden afgeleid. Als u meerdere gegevenstypen wilt toevoegen, kunt u deze toevoegen in een door komma&#39;s gescheiden lijst.

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

**Parameters**

Meer informatie over de standaard SELECT-queryparameters vindt u in het gedeelte [Query-sectie SELECTEREN](#select-queries). In deze sectie worden alleen parameters vermeld die exclusief zijn voor de `SELECT INTO` gebruiken.

- `TEMPORARY` of `TEMP`: Een optionele parameter. Indien gespecificeerd, zal de lijst die wordt gecreeerd een tijdelijke lijst zijn.
- `UNLOGGED`: Een optionele parameter. Indien gespecificeerd, zal de lijst die zoals wordt gecreeerd een niet geregistreerde lijst zijn. Meer informatie over niet-geregistreerde tabellen vindt u in de [PostSQL-documentatie](https://www.postgresql.org/docs/current/sql-createtable.html).
- `new_table`: De naam van de tabel die moet worden gemaakt.

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

**Parameters**

- `name`: De naam van de runtimeparameter waarover u informatie wilt. Mogelijke waarden voor de runtime parameter zijn de volgende waarden:
   - `SERVER_VERSION`: Deze parameter toont het versienummer van de server.
   - `SERVER_ENCODING`: Deze parameter toont de codering van de tekenset aan de serverzijde.
   - `LC_COLLATE`: Deze parameter toont de landinstelling van de database voor sortering (tekstvolgorde).
   - `LC_CTYPE`: Deze parameter toont de landinstelling van de database voor tekenclassificatie.
      `IS_SUPERUSER`: Deze parameter toont of heeft de huidige rol supergebruikersvoorrechten.
- `ALL`: Toon de waarden van alle configuratieparameters met beschrijvingen.

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

De `COPY` dumpt de uitvoer van `SELECT` zoeken naar een opgegeven locatie. Deze opdracht is alleen succesvol als de gebruiker toegang heeft tot deze locatie.

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

**Parameters**

- `query`: De query die u wilt kopiëren.
- `format_name`: De indeling waarin u de query wilt kopiëren. De `format_name` kan één van `parquet`, `csv`, of `json`. De standaardwaarde is `parquet`.

>[!NOTE]
>
>Het volledige uitvoerpad wordt `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### ALTER TABLE

De `ALTER TABLE` Met deze opdracht kunt u primaire of buitenlandse toetsbeperkingen toevoegen of neerzetten en kolommen aan de tabel toevoegen.

#### BEPERKING TOEVOEGEN OF VERWIJDEREN

De volgende SQL-query&#39;s geven voorbeelden van het toevoegen of neerzetten van beperkingen aan een tabel.

```sql
ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY column_name NAMESPACE namespace

ALTER TABLE table_name DROP CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT constraint_name FOREIGN KEY ( column_name )
```

**Parameters**

- `table_name`: De naam van de tabel die u bewerkt.
- `constraint_name`: De naam van de restrictie die u wilt toevoegen of verwijderen.
- `column_name`: De naam van de kolom waaraan u een beperking toevoegt.
- `referenced_table_name`: De naam van de tabel waarnaar wordt verwezen door de buitenlandse sleutel.
- `primary_column_name`: De naam van de kolom waarnaar wordt verwezen door de buitenlandse sleutel.

>[!NOTE]
>
>Het tabelschema moet uniek zijn en mag niet worden gedeeld door meerdere tabellen. Daarnaast is de naamruimte verplicht voor primaire-sleutelbeperkingen.

#### KOLOM TOEVOEGEN

De volgende SQL-query&#39;s geven voorbeelden van het toevoegen van kolommen aan een tabel.

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

**Parameters**

- `table_name`: De naam van de tabel die u bewerkt.
- `column_name`: De naam van de kolom die u wilt toevoegen.
- `data_type`: Het gegevenstype van de kolom die u wilt toevoegen. Tot de ondersteunde gegevenstypen behoren: bigint, char, string, date, datetime, double, double precision, integer, small int, tinyint, varchar.

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
