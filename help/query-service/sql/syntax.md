---
keywords: Experience Platform;home;populaire onderwerpen;queryservice;Query-service;sql syntaxis;sql;ctas;CTAS;Tabel maken als selectie
solution: Experience Platform
title: SQL-syntaxis in Query-service
topic: syntax
description: In dit document wordt SQL-syntaxis weergegeven die wordt ondersteund door Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: 78707257c179101b29e68036bf9173d74f01e03a
workflow-type: tm+mt
source-wordcount: '1981'
ht-degree: 1%

---


# SQL-syntaxis in Query Service

De Dienst van de Vraag van Adobe Experience Platform verstrekt de capaciteit om standaardANSI SQL voor `SELECT` verklaringen en andere beperkte bevelen te gebruiken. In dit document wordt de SQL-syntaxis beschreven die wordt ondersteund door [!DNL Query Service].

## query&#39;s SELECTEREN {#select-queries}

De volgende syntaxis bepaalt een `SELECT` vraag die door [!DNL Query Service] wordt gesteund:

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

waarbij `from_item` een van de volgende opties kan zijn:

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

en `grouping_element` kan één van de volgende opties zijn:

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

Deze clausule kan worden gebruikt om gegevens over een lijst incrementeel te lezen die op momentopname IDs wordt gebaseerd. Een momentopname identiteitskaart is een controlepuntteller die door een aantal wordt vertegenwoordigd van het type Long dat op een lijst van het gegevenshoeveeltal wordt toegepast telkens als het gegeven aan het wordt geschreven. De `SNAPSHOT` clausule maakt zich aan de lijstverhouding vast het naast wordt gebruikt.

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

Een `SNAPSHOT`-component werkt met een tabel- of tabelalias, maar niet boven op een subquery of weergave. Een `SNAPSHOT` clausule zal overal werken `SELECT` vraag op een lijst kan worden toegepast.

Daarnaast kunt u `HEAD` en `TAIL` gebruiken als speciale verschuivingswaarden voor momentopnameclausules. Het gebruiken van `HEAD` verwijst naar een compensatie vóór de eerste momentopname, terwijl `TAIL` naar een compensatie na de laatste momentopname verwijst.

### WHERE-component

Door gebrek, zijn de gelijken die door een `WHERE` clausule op een `SELECT` vraag worden veroorzaakt case-sensitive. Als u gelijken case-insensitive wilt zijn, kunt u het sleutelwoord `ILIKE` in plaats van `LIKE` gebruiken.

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

Een `SELECT` vraag die gebruikt verbindt zich heeft de volgende syntaxis:

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### UNIE, INTERSECT EN BEHALVE

De `UNION`, `INTERSECT`, en `EXCEPT` clausules worden gebruikt om als rijen van twee of meer lijsten te combineren of uit te sluiten:

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### TABEL MAKEN ALS SELECT

De volgende syntaxis bepaalt een `CREATE TABLE AS SELECT` (CTAS) vraag:

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false') ] AS (select_query)
```

**Parameters**

- `schema`: De titel van het XDM-schema. Gebruik deze clausule slechts als u wenst om een bestaand schema XDM voor de nieuwe dataset te gebruiken die door de vraag CTAS wordt gecreeerd.
- `rowvalidation`: (Optioneel) Hiermee wordt opgegeven of de gebruiker validatie op rijniveau wil toepassen voor alle nieuwe batches die worden ingevoerd voor de nieuwe gegevensset. De standaardwaarde is `true`.
- `select_query`: Een  `SELECT` instructie. De syntaxis van de `SELECT` vraag kan in [SELECT vragen sectie](#select-queries) worden gevonden.

**Voorbeeld**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>De instructie `SELECT` moet een alias hebben voor de statistische functies zoals `COUNT`, `SUM`, `MIN` enzovoort. Daarnaast kan de instructie `SELECT` met of zonder haakjes () worden geleverd. U kunt een `SNAPSHOT` clausule verstrekken om stijgende delta&#39;s in de doellijst te lezen.

## INVOEGEN IN

De opdracht `INSERT INTO` wordt als volgt gedefinieerd:

```sql
INSERT INTO table_name select_query
```

**Parameters**

- `table_name`: De naam van de tabel waarin u de query wilt invoegen.
- `select_query`: Een  `SELECT` instructie. De syntaxis van de `SELECT` vraag kan in [SELECT vragen sectie](#select-queries) worden gevonden.

**Voorbeeld**

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!NOTE]
> De `SELECT`-instructie **mag niet** tussen haakjes () staan. Daarnaast moet het schema van het resultaat van de instructie `SELECT` overeenkomen met dat van de tabel die is gedefinieerd in de instructie `INSERT INTO`. U kunt een `SNAPSHOT` clausule verstrekken om stijgende delta&#39;s in de doellijst te lezen.

## DROP TABLE

Met de opdracht `DROP TABLE` wordt een bestaande tabel verwijderd en wordt de aan de tabel gekoppelde map uit het bestandssysteem verwijderd als dit geen externe tabel is. Als de tabel niet bestaat, treedt een uitzondering op.

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

**Parameters**

- `IF EXISTS`: Als dit is opgegeven, wordt geen uitzondering gegenereerd als de tabel  **** niet bestaat.

## WEERGAVE MAKEN

De volgende syntaxis bepaalt een `CREATE VIEW` vraag:

```sql
CREATE VIEW view_name AS select_query
```

**Parameters**

- `view_name`: De naam van de weergave die moet worden gemaakt.
- `select_query`: Een  `SELECT` instructie. De syntaxis van de `SELECT` vraag kan in [SELECT vragen sectie](#select-queries) worden gevonden.

**Voorbeeld**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

## DROP VIEW

De volgende syntaxis bepaalt een `DROP VIEW` vraag:

```sql
DROP VIEW [IF EXISTS] view_name
```

**Parameter**

- `IF EXISTS`: Als dit wordt opgegeven, wordt geen uitzondering gegenereerd als de weergave  **** niet bestaat.
- `view_name`: De naam van de weergave die moet worden verwijderd.

**Voorbeeld**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## [!DNL Spark] SQL-opdrachten

De subsectie hieronder behandelt de SQL bevelen van de Vonk die door de Dienst van de Vraag worden gesteund.

### SET

Met de opdracht `SET` wordt een eigenschap ingesteld en wordt de waarde van een bestaande eigenschap geretourneerd of worden alle bestaande eigenschappen weergegeven. Als een waarde wordt opgegeven voor een bestaande eigenschapsleutel, wordt de oude waarde overschreven.

```sql
SET property_key = property_value
```

**Parameters**

- `property_key`: De naam van de eigenschap die u wilt weergeven of wijzigen.
- `property_value`: De waarde waarop u de eigenschap wilt instellen.

Als u de waarde voor een instelling wilt retourneren, gebruikt u `SET [property key]` zonder een `property_value`.

## PostgreSQL-opdrachten

De subsecties hieronder behandelen de bevelen PostgreSQL die door de Dienst van de Vraag worden gesteund.

### BEGINNEN

Met de opdracht `BEGIN`, of met de opdracht `BEGIN WORK` of `BEGIN TRANSACTION`, wordt een transactieblok gestart. Om het even welke verklaringen die na het begin bevel worden ingevoerd zullen in één enkele transactie worden uitgevoerd tot een expliciete COMMIT of bevel ROLLBACK wordt gegeven. Deze opdracht is hetzelfde als `START TRANSACTION`.

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### SLUITEN

Met de opdracht `CLOSE` worden de bronnen vrijgemaakt die aan een open cursor zijn gekoppeld. Nadat de cursor is gesloten, zijn er geen verdere bewerkingen meer toegestaan. Een cursor moet worden gesloten wanneer deze niet meer nodig is.

```sql
CLOSE name
CLOSE ALL
```

Als `CLOSE name` wordt gebruikt, `name` vertegenwoordigt de naam van een open curseur die moet worden gesloten. Als `CLOSE ALL` wordt gebruikt, worden alle open cursors gesloten.

### VERWIJDEREN

Met de opdracht `DEALLOCATE` kunt u een eerder voorbereide SQL-instructie opnieuw opzoeken. Als u een voorbereide instructie niet expliciet zoekt, wordt de toewijzing ongedaan gemaakt wanneer de sessie wordt beëindigd. Meer informatie over voorbereide instructies vindt u in de sectie [PREPARE command](#prepare).

```sql
DEALLOCATE name
DEALLOCATE ALL
```

Als `DEALLOCATE name` wordt gebruikt, `name` vertegenwoordigt de naam van de voorbereide verklaring die moet worden deassign. Als `DEALLOCATE ALL` wordt gebruikt, zullen alle voorbereide verklaringen worden gedesalloceerd.

### VERKLAREN

Met de opdracht `DECLARE` kan een gebruiker een cursor maken die kan worden gebruikt om een klein aantal rijen op te halen uit een grotere query. Nadat de curseur wordt gecreeerd, worden de rijen opgehaald van het gebruikend `FETCH`.

```sql
DECLARE name CURSOR FOR query
```

**Parameters**

- `name`: De naam van de cursor die moet worden gemaakt.
- `query`: Een  `SELECT` of  `VALUES` opdracht die de rijen bevat die door de cursor moeten worden geretourneerd.

### UITVOEREN

De opdracht `EXECUTE` wordt gebruikt om een eerder voorbereide instructie uit te voeren. Aangezien voorbereide instructies alleen bestaan voor de duur van een sessie, moet de voorbereide instructie zijn gemaakt door een instructie `PREPARE` die eerder in de huidige sessie is uitgevoerd. Meer informatie over het gebruik van voorbereide instructies vindt u in de sectie [`PREPARE` command](#prepare).

Als de instructie `PREPARE` die de instructie heeft gemaakt enkele parameters heeft opgegeven, moet een compatibele set parameters worden doorgegeven aan de instructie `EXECUTE`. Als deze parameters niet binnen worden overgegaan, zal een fout worden opgeheven.

```sql
EXECUTE name [ ( parameter ) ]
```

**Parameters**

- `name`: De naam van de voorbereide instructie die moet worden uitgevoerd.
- `parameter`: De werkelijke waarde van een parameter voor de voorbereide instructie. Dit moet een expressie zijn die een waarde oplevert die compatibel is met het gegevenstype van deze parameter, zoals bepaald toen de voorbereide instructie werd gemaakt.  Als er meerdere parameters zijn voor de voorbereide instructie, worden deze door komma&#39;s gescheiden.

### VERKLAREN

Met de opdracht `EXPLAIN` wordt het uitvoeringsplan voor de opgegeven instructie weergegeven. In het uitvoeringsplan ziet u hoe de tabellen waarnaar door de instructie wordt verwezen, worden gescand.  Als er naar meerdere tabellen wordt verwezen, wordt aangegeven welke samenvoegalgoritmen worden gebruikt om de vereiste rijen van elke invoertabel samen te voegen.

```sql
EXPLAIN option statement
```

Waarbij `option` een van de volgende kan zijn:

```sql
ANALYZE
FORMAT { TEXT | JSON }
```

**Parameters**

- `ANALYZE`: Als het  `option` bevat  `ANALYZE`, worden de runtime en andere statistieken getoond.
- `FORMAT`: Als het  `option` bevat  `FORMAT`, geeft het de uitvoerindeling op, die kan zijn  `TEXT` of  `JSON`. Niet-tekstuele uitvoer bevat dezelfde informatie als de indeling voor tekstuitvoer, maar kan gemakkelijker door programma&#39;s worden geparseerd. Deze parameter is standaard `TEXT`.
- `statement`: Om het even welk  `SELECT`,  `INSERT`,  `UPDATE`,  `DELETE`,  `VALUES`,  `EXECUTE`,  `DECLARE`,  `CREATE TABLE AS`, of  `CREATE MATERIALIZED VIEW AS` verklaring, waarvan uitvoeringsplan u wilt zien.

>[!IMPORTANT]
>
>Onthoud dat de instructie daadwerkelijk wordt uitgevoerd wanneer de optie `ANALYZE` wordt gebruikt. Hoewel `EXPLAIN` om het even welke output verwerpt die `SELECT` terugkeert, gebeuren andere bijwerkingen van de verklaring zoals gewoonlijk.

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

Met de opdracht `FETCH` worden rijen opgehaald met een eerder gemaakte cursor.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

**Parameters**

- `num_of_rows`: Het aantal rijen dat moet worden opgehaald.
- `cursor_name`: De naam van de curseur u informatie van terugwint.

### {#prepare} VOORBEREIDEN

Met de opdracht `PREPARE` kunt u een voorbereide instructie maken. Een voorbereide instructie is een serverobject dat kan worden gebruikt om vergelijkbare SQL-instructies te sjablonen.

Bereide instructies kunnen parameters hebben. Dit zijn waarden die in de instructie worden vervangen wanneer deze wordt uitgevoerd. Parameters worden naar positie verwezen, waarbij $1, $2, enz. wordt gebruikt bij het gebruik van voorbereide instructies.

U kunt ook een lijst met parametergegevenstypen opgeven. Als het gegevenstype van een parameter niet wordt vermeld, kan het type van de context worden afgeleid.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

**Parameters**

- `name`: De naam voor de voorbereide instructie.
- `data_type`: De gegevenstypen van de parameters van de voorbereide instructie. Als het gegevenstype van een parameter niet wordt vermeld, kan het type van de context worden afgeleid. Als u meerdere gegevenstypen wilt toevoegen, kunt u deze toevoegen in een door komma&#39;s gescheiden lijst.

### ROLLBACK

Met de opdracht `ROLLBACK` wordt de huidige transactie ongedaan gemaakt en worden alle updates die door de transactie zijn gemaakt, genegeerd.

```sql
ROLLBACK
ROLLBACK WORK
```

### SELECTEREN IN

Met de opdracht `SELECT INTO` maakt u een nieuwe tabel en vult u deze met gegevens die door een query zijn berekend. De gegevens worden niet aan de client geretourneerd, omdat deze een normale opdracht `SELECT` hebben. De kolommen van de nieuwe lijst hebben de namen en de gegevenstypes verbonden aan de outputkolommen van `SELECT` bevel.

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

Meer informatie over de standaard UITGEZOCHTE vraagparameters kan in [UITGEZOCHTE vraagsectie](#select-queries) worden gevonden. In deze sectie worden alleen parameters vermeld die exclusief zijn voor de opdracht `SELECT INTO`.

- `TEMPORARY` of  `TEMP`: Een optionele parameter. Indien gespecificeerd, zal de lijst die wordt gecreeerd een tijdelijke lijst zijn.
- `UNLOGGED`: Een optionele parameter. Indien gespecificeerd, zal de lijst die zoals wordt gecreeerd een niet geregistreerde lijst zijn. Meer informatie over niet-geregistreerde lijsten kan in de [documentatie worden gevonden PostgreSQL](https://www.postgresql.org/docs/current/sql-createtable.html).
- `new_table`: De naam van de tabel die moet worden gemaakt.

**Voorbeeld**

Met de volgende query wordt een nieuwe tabel `films_recent` gemaakt die alleen recente items uit de tabel `films` bevat:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### TONEN

Met de opdracht `SHOW` wordt de huidige instelling van runtimeparameters weergegeven. Deze variabelen kunnen worden geplaatst gebruikend de `SET` verklaring, door het `postgresql.conf` configuratiedossier, door `PGOPTIONS` milieuvariabele (wanneer het gebruiken van libpq of een libpq-Gebaseerde toepassing), of door bevel-lijn vlaggen uit te geven wanneer het beginnen van de server van Postgres.

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

Met de opdracht `COPY` laat u de uitvoer van een `SELECT`-query op een opgegeven locatie dumpen. Deze opdracht is alleen succesvol als de gebruiker toegang heeft tot deze locatie.

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

**Parameters**

- `query`: De query die u wilt kopiëren.
- `format_name`: De indeling waarin u de query wilt kopiëren. `format_name` kan één van `parquet`, `csv`, of `json` zijn. De standaardwaarde is `parquet`.

>[!NOTE]
>
>Het volledige uitvoerpad is `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### ALTER TABLE

Met de opdracht `ALTER TABLE` kunt u primaire of buitenlandse toetsbeperkingen toevoegen of neerzetten en kolommen aan de tabel toevoegen.

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

Het `SHOW PRIMARY KEYS` bevel maakt een lijst van alle primaire zeer belangrijke beperkingen voor het bepaalde gegevensbestand.

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

Het `SHOW FOREIGN KEYS` bevel maakt een lijst van alle buitenlandse zeer belangrijke beperkingen voor het bepaalde gegevensbestand.

```sql
SHOW FOREIGN KEYS
```

```console
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```
