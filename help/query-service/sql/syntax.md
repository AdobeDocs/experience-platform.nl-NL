---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: SQL-syntaxis
topic: syntax
translation-type: tm+mt
source-git-commit: f5bc9beb59e83b0411d98d901d5055122a124d07

---


# SQL-syntaxis

De Dienst van de vraag verstrekt de capaciteit om standaardANSI SQL voor `SELECT` verklaringen en andere beperkte bevelen te gebruiken. Dit document toont SQL syntaxis die door de Dienst van de Vraag wordt gesteund.

## Een SELECT-query definiëren

De volgende syntaxis bepaalt een `SELECT` vraag die door de Dienst van de Vraag wordt gesteund:

```
[ WITH with_query [, ...] ]
SELECT [ ALL | DISTINCT [( expression [, ...] ) ] ]
    [ * | expression [ [ AS ] output_name ] [, ...] ]
    [ FROM from_item [, ...] ]
    [ WHERE condition ]
    [ GROUP BY grouping_element [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT | MINUS } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start ]
```

waarbij `from_item` een van de volgende kan worden gebruikt:

```
table_name [ * ] [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    [ LATERAL ] ( select ) [ AS ] alias [ ( column_alias [, ...] ) ]
    with_query_name [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    from_item [ NATURAL ] join_type from_item [ ON join_condition | USING ( join_column [, ...] ) ]
```

en `grouping_element` kan een van de volgende zijn:

```
( )
    expression
    ( expression [, ...] )
    ROLLUP ( { expression | ( expression [, ...] ) } [, ...] )
    CUBE ( { expression | ( expression [, ...] ) } [, ...] )
    GROUPING SETS ( grouping_element [, ...] )
```

en `with_query` is:

```
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
 
TABLE [ ONLY ] table_name [ * ]
```

### WHERE ILIKE, component

Het sleutelwoord ILIKE kan in plaats van LIKE worden gebruikt om gelijken op WAAR clausule van de UITGEZOCHTE vraag ongevoelig te maken.

```
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

De logica van de clausules LIKE en ILIKE is als volgt:
- ```WHERE condition LIKE pattern```, ```~~``` is gelijk aan patroon
- ```WHERE condition NOT LIKE pattern```, ```!~~``` is gelijk aan patroon
- ```WHERE condition ILIKE pattern```, gelijk aan ```~~*``` patroon
- ```WHERE condition NOT ILIKE pattern```, gelijk aan ```!~~*``` patroon


#### Voorbeeld

```
SELECT * FROM Customers
WHERE CustomerName ILIKE 'a%';
```

Keert klanten met namen terug die in &quot;A&quot;of &quot;a&quot;beginnen.

## JOINS

Een `SELECT` query die gebruikmaakt van verbindingen heeft de volgende syntaxis:

```
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```


## UNIE, INTERSECT EN BEHALVE

De `UNION`, `INTERSECT`, en de `EXCEPT` clausules worden gesteund om als rijen van twee of meer lijsten te combineren of uit te sluiten:

```
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

## TABEL MAKEN ALS SELECT

De volgende syntaxis bepaalt een vraag `CREATE TABLE AS SELECT` (CTAS) die door de Dienst van de Vraag wordt gesteund:

```
CREATE TABLE table_name [ WITH (schema='target_schema_title') ] AS (select_query)
```

waarbij `target_schema_title` is de titel van het XDM-schema. Gebruik deze clausule slechts als u wenst om een bestaand schema XDM voor de nieuwe dataset te gebruiken die door vraag CTAS wordt gecreeerd.

en `select_query` is een `SELECT` instructie waarvan de syntaxis hierboven in dit document wordt gedefinieerd.


### Voorbeeld

```
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
```

Houd er rekening mee dat voor een bepaalde CTAS-query:

1. De `SELECT` instructie moet een alias hebben voor de statistische functies, zoals `COUNT`, `SUM`, `MIN`enzovoort.
2. De `SELECT` instructie kan met of zonder haakjes () worden geleverd.

## INVOEGEN IN

De volgende syntaxis bepaalt een `INSERT INTO` vraag die door de Dienst van de Vraag wordt gesteund:

```
INSERT INTO table_name select_query
```

waarbij `select_query` een `SELECT` instructie is waarvan de syntaxis hierboven in dit document is gedefinieerd.

### Voorbeeld

```
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;
```

Houd er rekening mee dat voor een bepaalde INSERT INTO-query:

1. De `SELECT` instructie MAG NIET tussen haakjes () staan.
2. Het schema van het resultaat van de `SELECT` instructie moet overeenkomen met dat van de tabel die in de `INSERT INTO` instructie is gedefinieerd.

### DROP TABLE

Zet een tabel neer en verwijder de map die aan de tabel is gekoppeld uit het bestandssysteem als dit geen EXTERNE tabel is. Als de te laten vallen tabel niet bestaat, treedt een uitzondering op.

```
DROP [TEMP] TABLE [IF EXISTS] [db_name.]table_name
```

### Parameters

- `IF EXISTS`: Als de tabel niet bestaat, gebeurt er niets
- `TEMP`: Tijdelijke tabel

## WEERGAVE MAKEN

De volgende syntaxis bepaalt een `CREATE VIEW` vraag die door de Dienst van de Vraag wordt gesteund:

```
CREATE [ OR REPLACE ] VIEW view_name AS select_query
```

Waar `view_name` is de naam van de weergave die moet worden gemaakt en `select_query` is een `SELECT` instructie waarvan de syntaxis hierboven in dit document is gedefinieerd.

Voorbeeld:

```
CREATE VIEW V1 AS SELECT color, type FROM Inventory
CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

### DROP VIEW

De volgende syntaxis bepaalt een `DROP VIEW` vraag die door de Dienst van de Vraag wordt gesteund:

```
DROP VIEW [IF EXISTS] view_name
```

Waar `view_name` is de naam van de weergave die moet worden verwijderd

Voorbeeld:

```
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## SQL-opdrachten parkeren

### SET

Stel een eigenschap in, retourneer de waarde van een bestaande eigenschap of vermeld alle bestaande eigenschappen. Als een waarde wordt opgegeven voor een bestaande eigenschapsleutel, wordt de oude waarde overschreven.

```
SET property_key [ To | =] property_value
```

Als u de waarde voor een instelling wilt retourneren, gebruikt u `SHOW [setting name]`.

## PostgreSQL-opdrachten

### BEGINNEN

Dit bevel wordt ontleed en het voltooide bevel wordt teruggestuurd naar de cliënt. Dit is het zelfde als het `START TRANSACTION` bevel.

```
BEGIN [ TRANSACTION ]
```

#### Parameters

- `TRANSACTION`: Optionele sleutelwoorden. Als je het luistert, wordt er geen actie ondernomen.

### SLUITEN

`CLOSE` bevrijdt de middelen verbonden aan een open curseur. Nadat de cursor is gesloten, zijn er geen verdere bewerkingen meer toegestaan. Een cursor moet worden gesloten wanneer deze niet meer nodig is.

```
CLOSE { name }
```

#### Parameters

- `name`: de naam van een open cursor die moet worden gesloten.

### DOEN

Er wordt geen actie ondernomen in de Dienst van de Vraag als antwoord op begaat transactieverklaring.

```
COMMIT [ WORK | TRANSACTION ]
```

#### Parameters

- `WORK`
- `TRANSACTION`: Optionele sleutelwoorden. Ze hebben geen effect.

### VERWIJDEREN

Gebruik deze methode `DEALLOCATE` om een eerder voorbereide SQL-instructie te zoeken. Als u een voorbereide instructie niet expliciet zoekt, wordt de toewijzing ongedaan gemaakt wanneer de sessie wordt beëindigd.

```
DEALLOCATE [ PREPARE ] { name | ALL }
```

#### Parameters

- `Prepare`: Dit trefwoord wordt genegeerd.
- `name`: De naam van de voorbereide instructie die moet worden gedistribueerd.
- `ALL`: Wijs alle voorbereide instructies uit.

### VERKLAREN

`DECLARE` Hiermee kan een gebruiker cursors maken die kunnen worden gebruikt om een klein aantal rijen tegelijk op te halen uit een grotere query. Nadat de cursor is gemaakt, worden er rijen van opgehaald met `FETCH`.

```
DECLARE name CURSOR [ WITH  HOLD ] FOR query
```

#### Parameters

- `name`: De naam van de cursor die moet worden gemaakt.
- `WITH HOLD`: Geeft aan dat de cursor kan blijven worden gebruikt nadat de transactie die deze heeft gemaakt, correct is toegewezen.
- `query`: Een `SELECT` of `VALUES` opdracht die de rijen bevat die door de cursor moeten worden geretourneerd.

### UITVOEREN

`EXECUTE` wordt gebruikt om een eerder voorbereide instructie uit te voeren. Omdat voorbereide instructies alleen bestaan voor de duur van een sessie, moet de voorbereide instructie zijn gemaakt door een `PREPARE` instructie die eerder in de huidige sessie is uitgevoerd.

Als de `PREPARE` verklaring die tot de verklaring leidde sommige parameters specificeerde, moet een compatibele reeks parameters tot de `EXECUTE` verklaring worden overgegaan, anders wordt een fout opgeheven. Let op: instructies die zijn voorbereid (anders dan functies) worden niet overbelast op basis van het type of het aantal parameters. De naam van een voorbereide instructie moet uniek zijn binnen een databasesessie.

```
EXECUTE name [ ( parameter [, ...] ) ]
```

#### Parameters

- `name`: De naam van de voorbereide instructie die moet worden uitgevoerd.
- `parameter`: De werkelijke waarde van een parameter voor de voorbereide instructie. Dit moet een expressie zijn die een waarde oplevert die compatibel is met het gegevenstype van deze parameter, zoals bepaald toen de voorbereide instructie werd gemaakt.

### VERKLAREN

Dit bevel toont het uitvoeringsplan dat de planner PostgreSQL voor de geleverde verklaring produceert. Het uitvoeringsplan toont hoe de tabellen waarnaar door de instructie wordt verwezen, worden gescand — door gewone sequentiële scan, indexscan enzovoort — en als er naar meerdere tabellen wordt verwezen, welke samenvoegalgoritmen worden gebruikt om de vereiste rijen van elke invoertabel samen te voegen.

Het meest kritieke deel van de vertoning is de geschatte kosten van de verklaringsuitvoering, die de gok van de planner bij hoe lang het zal duren om de verklaring in werking te stellen (die in kosteneenheden wordt gemeten die willekeurig zijn, maar gewoonlijk schijfpaginafhalen betekent). Eigenlijk worden twee getallen weergegeven: de opstartkosten vóór de eerste rij kunnen worden geretourneerd en de totale kosten voor het retourneren van alle rijen. Voor de meeste vragen, is de totale kosten wat belangrijk is, maar in contexten zoals subquery in EXISTS, kiest de planner de kleinste startkosten in plaats van de kleinste totale kosten (omdat de uitvoerder na het krijgen van één rij, hoe dan ook stopt). Ook, als u het aantal rijen beperkt om met een `LIMIT` clausule terug te keren, maakt de planner een aangewezen interpolatie tussen de eindpuntkosten om te schatten welk plan werkelijk het goedkoopst is.

De `ANALYZE` optie zorgt ervoor dat de instructie wordt uitgevoerd, niet alleen gepland. Dan, worden de daadwerkelijke runtime statistieken toegevoegd aan de vertoning, met inbegrip van de totale verstreken tijd die binnen elke planknoop (in milliseconden) wordt uitgegeven en het totale aantal rijen het teruggekeerde. Dit is nuttig om te zien of de ramingen van de planner dicht bij de realiteit staan.

```
EXPLAIN [ ( option [, ...] ) ] statement
EXPLAIN [ ANALYZE ] statement

where option can be one of:
    ANALYZE [ boolean ]
    TYPE VALIDATE
    FORMAT { TEXT | JSON }
```

#### Parameters

- `ANALYZE`: Voer het bevel uit en toon daadwerkelijke runtime en andere statistieken. Deze parameter is standaard ingesteld op `FALSE`.
- `FORMAT`: Geef de uitvoerindeling op, die TEXT, XML, JSON of YAML kan zijn. Niet-tekstuele uitvoer bevat dezelfde informatie als de indeling voor tekstuitvoer, maar kan gemakkelijker door programma&#39;s worden geparseerd. Deze parameter is standaard ingesteld op `TEXT`.
- `statement`: Om het even welk `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `VALUES`, `EXECUTE`, `DECLARE`, `CREATE TABLE AS`, of `CREATE MATERIALIZED VIEW AS` verklaring, waarvan uitvoeringsplan u wilt zien.

>[!IMPORTANT] Onthoud dat de instructie daadwerkelijk wordt uitgevoerd wanneer de `ANALYZE` optie wordt gebruikt. Hoewel `EXPLAIN` `SELECT` alle uitvoer die een instructie retourneert, wordt genegeerd, treden andere bijwerkingen van de instructie op de gebruikelijke manier op.

#### Voorbeeld

Om het plan voor een eenvoudige vraag op een lijst met één enkele `integer` kolom en 10000 rijen te tonen:

```
EXPLAIN SELECT * FROM foo;

                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)
(1 row)
```

### FETCH

`FETCH` Hiermee worden rijen opgehaald met een eerder gemaakte cursor.

Een cursor heeft een bijbehorende positie, die wordt gebruikt door `FETCH`. De cursorpositie kan vóór de eerste rij van het vraagresultaat, op om het even welke bepaalde rij van het resultaat, of na de laatste rij van het resultaat zijn. Wanneer u een cursor maakt, wordt deze vóór de eerste rij geplaatst. Na het halen van sommige rijen, wordt de curseur geplaatst op de rij onlangs teruggewonnen. Als de cursor aan het einde van de beschikbare rijen `FETCH` loopt, wordt deze na de laatste rij geplaatst. Als er geen dergelijke rij is, wordt een leeg resultaat geretourneerd en worden de cursors vóór de eerste rij of na de laatste rij geplaatst, al naargelang wat van toepassing is.

```
FETCH num_of_rows [ IN | FROM ] cursor_name
```

#### Parameters

- `num_of_rows`: Een mogelijk ondertekende geheel-getalconstante die de plaats of het aantal rijen bepaalt om te halen.
- `cursor_name`: De naam van een open cursor.

### PREPARE

`PREPARE` maakt een voorbereide instructie. Een voorbereide instructie is een serverobject dat kan worden gebruikt om de prestaties te optimaliseren. Wanneer de `PREPARE` instructie wordt uitgevoerd, wordt de opgegeven instructie geparseerd, geanalyseerd en herschreven. Wanneer een `EXECUTE` bevel daarna wordt uitgegeven, wordt de voorbereide verklaring gepland en uitgevoerd. Deze arbeidsverdeling vermijdt herhalende parsanalyses, terwijl het uitvoeringsplan afhangt van de opgegeven specifieke parameterwaarden.

Bereide instructies kunnen parameters hebben, waarden die in de instructie worden vervangen wanneer deze wordt uitgevoerd. Wanneer het creëren van de voorbereide verklaring, verwijs naar parameters door positie, gebruikend $1, $2, etc. U kunt desgewenst een corresponderende lijst met parametergegevenstypen opgeven. Wanneer het gegevenstype van een parameter niet is opgegeven of als onbekend is gedeclareerd, wordt het type afgeleid van de context waarin voor het eerst naar de parameter wordt verwezen, indien mogelijk. Geef bij het uitvoeren van de instructie de werkelijke waarden voor deze parameters op in de `EXECUTE` instructie.

Bereide instructies gelden alleen voor de duur van de huidige databasesessie. Wanneer de sessie wordt beëindigd, wordt de voorbereide instructie vergeten. U moet deze dus opnieuw maken voordat u de instructie opnieuw kunt gebruiken. Dit betekent ook dat één enkele voorbereide verklaring niet door veelvoudige gelijktijdige gegevensbestandcliënten kan worden gebruikt. Elke client kan echter een eigen voorbereide instructie maken die u wilt gebruiken. Vooraf voorbereide instructies kunnen handmatig worden opgeschoond met de `DEALLOCATE` opdracht.

Bereide instructies hebben mogelijk het grootste prestatievoordeel wanneer één sessie wordt gebruikt om een groot aantal vergelijkbare instructies uit te voeren. Het prestatiesverschil is met name significant als de verklaringen complex zijn om te plannen of te herschrijven, bijvoorbeeld als de vraag zich bij vele lijsten impliceert of de toepassing van verscheidene regels vereist. Als de verklaring vrij eenvoudig is om te plannen en te herschrijven maar vrij duur om uit te voeren, is het prestatievoordeel van voorbereide verklaringen minder merkbaar.

```
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

#### Parameters

- `name`: Een willekeurige naam die aan deze bepaalde voorbereide instructie wordt gegeven. Deze moet uniek zijn binnen één sessie en wordt vervolgens gebruikt om een eerder voorbereide instructie uit te voeren of te distribueren.
- `data-type`: Het gegevenstype van een parameter voor de voorbereide instructie. Wanneer het gegevenstype van een bepaalde parameter niet is opgegeven of als onbekend is opgegeven, wordt dit afgeleid van de context waarin de parameter voor het eerst wordt genoemd. Als u naar de parameters in de voorbereide instructie zelf wilt verwijzen, gebruikt u $1, $2 enzovoort.


### ROLLBACK

`ROLLBACK` rolt terug de huidige transactie en veroorzaakt alle updates die door de transactie worden gemaakt om worden verworpen.

```
ROLLBACK [ WORK ]
```

#### Parameters

- `WORK`

### SELECTEREN IN

`SELECT INTO` Hiermee maakt u een nieuwe tabel en vult u deze met gegevens die door een query zijn berekend. De gegevens worden niet aan de client geretourneerd, zoals bij een normale waarde `SELECT`. De kolommen van de nieuwe lijst hebben de namen en de gegevenstypes verbonden aan de outputkolommen van `SELECT`.

```
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

#### Parameters

- `TEMPORARAY` of `TEMP`: Indien opgegeven, wordt de tabel gemaakt als een tijdelijke tabel.
- `UNLOGGED:` indien opgegeven, wordt de tabel gemaakt als een niet-geregistreerde tabel.
- `new_table` De naam (optioneel gekwalificeerd voor schema) van de tabel die moet worden gemaakt.

#### Voorbeeld

Een nieuwe tabel maken die alleen recente items uit de tabel `films_recent` bevat `films`:

```
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### TONEN

`SHOW` geeft de huidige instelling van runtimeparameters weer. Deze variabelen kunnen worden geplaatst gebruikend de `SET` verklaring, door het postgresql.conf configuratiedossier, door de `PGOPTIONS` milieuvariabele (wanneer het gebruiken van libpq of een libpq-Gebaseerde toepassing), of door bevel-lijn vlaggen te bewerken wanneer het beginnen van de postgres server.

```
SHOW name
```

#### Parameters

- `name`:
   - `SERVER_VERSION`: Geeft het versienummer van de server weer.
   - `SERVER_ENCODING`: Toont de codering van de tekenset aan de serverzijde. Deze parameter kan op dit moment wel worden weergegeven, maar niet worden ingesteld, omdat de codering tijdens het maken van de database wordt bepaald.
   - `LC_COLLATE`: Geeft de landinstelling van de database voor sortering (tekstvolgorde) weer. Deze parameter kan op dit moment wel worden weergegeven, maar niet worden ingesteld, omdat de instelling tijdens het maken van de database wordt bepaald.
   - `LC_CTYPE`: Geeft de landinstelling van de database voor tekenclassificatie weer. Deze parameter kan op dit moment wel worden weergegeven, maar niet worden ingesteld, omdat de instelling tijdens het maken van de database wordt bepaald.
      `IS_SUPERUSER`: True if the current role has superuser privileges.
- `ALL`: Toon de waarden van alle configuratieparameters met beschrijvingen.

#### Voorbeeld

Huidige instelling van parameter weergeven `DateStyle`

```
SHOW DateStyle;
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### TRANSACTIE STARTEN

Dit bevel wordt ontleed en verzendt het voltooide bevel terug naar cliënt. Dit is het zelfde als het `BEGIN` bevel.

```
START TRANSACTION [ transaction_mode [, ...] ]

where transaction_mode is one of:

    ISOLATION LEVEL { SERIALIZABLE | REPEATABLE READ | READ COMMITTED | READ UNCOMMITTED }
    READ WRITE | READ ONLY
```
