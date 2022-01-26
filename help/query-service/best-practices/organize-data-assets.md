---
title: Beste praktijken voor de Organisatie van gegevensactiva in de Dienst van de Vraag
description: Dit document schetst een logisch middel om gegevens voor gebruiksgemak met de Dienst van de Vraag te organiseren.
source-git-commit: ed9fa7b83f9e1c974bc74e9dde018a87823954ee
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# Gegevenselementen organiseren in Query Service

Dit document biedt richtlijnen over aanbevolen procedures voor het ordenen van gegevenselementen, zoals gegevenssets, weergaven en tijdelijke tabellen voor gebruik met de Adobe Experience Platform Query Service. Hierin wordt beschreven hoe u uw gegevens kunt structureren en hoe u deze gegevens kunt openen, bijwerken en verwijderen.

Het is belangrijk om uw gegevenselementen logisch te ordenen binnen het Platform [!DNL Data Lake] als ze groeien. De Dienst van de vraag breidt SQL constructies uit die u toelaten om gegevensactiva binnen een zandbak logisch gezien te groeperen. Deze organisatiemethode staat voor het delen van gegevensactiva tussen schema&#39;s toe zonder de behoefte om hen fysiek te bewegen.

## Aan de slag

Voordat u doorgaat met dit document, hebt u een goed inzicht in [Query-service](../home.md) functies en hebben de [gebruikersinterfacegids](../ui/user-guide.md).

## Gegevens ordenen in Query Service

In de volgende voorbeelden worden de constructies getoond die beschikbaar zijn via Adobe Experience Platform Query Service om uw gegevens logisch te ordenen met behulp van de standaard SQL-syntaxis. U moet eerst een database maken die fungeert als container voor uw gegevenspunten. Een gegevensbestand kan één of meerdere schema&#39;s bevatten, en elk schema kan één of meerdere verwijzingen naar een gegevenselement (datasets, meningen, tijdelijke lijsten, enz.) dan hebben. Deze verwijzingen omvatten om het even welke verhouding of associaties tussen de datasets.

Zie de [Gebruikershandleiding voor de Query Editor](../ui/user-guide.md) voor gedetailleerde begeleiding op hoe te om de Dienst UI van de Vraag te gebruiken om SQL vragen tot stand te brengen.

De volgende SQL-constructies om gegevenssets logisch te organiseren in een sandbox worden ondersteund.

```SQL
CREATE DATABASE databaseA;
CREATE SCHEMA databaseA.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

In het voorbeeld (iets afgekapt voor de beknoptheid) wordt deze methode getoond waar `databaseA` bevat schema `schema1`.

## Gegevenselementen aan een schema koppelen

Zodra een schema is gecreeerd om als container voor de gegevensactiva te handelen, kan elke dataset met één of meerdere schema&#39;s in het gegevensbestand worden geassocieerd door standaard SQL te gebruiken ALTER syntaxis van de LIJST.

In het volgende voorbeeld wordt het volgende toegevoegd `dataset1`, `dataset2`, `dataset3` en `v1` aan de `databaseA.schema1` in het vorige voorbeeld gemaakte container.

```SQL
ALTER TABLE dataset1 SET SCHEMA databaseA.schema1;
 
ALTER TABLE dataset2 SET SCHEMA databaseA.schema1;
 
ALTER TABLE dataset3 SET SCHEMA databaseA.schema1;
 
ALTER VIEW v1  SET SCHEMA databaseA.schema1;
```

## Gegevenselementen openen vanuit de gegevenscontainer

Door de databasenaam op de juiste manier te kwalificeren, [!DNL PostgreSQL] client kan verbinding maken met elke gegevensstructuur die u hebt gemaakt met het trefwoord SHOW. Zie voor meer informatie over het trefwoord SHOW de [sectie TONEN in de SQL-syntaxisdocumentatie](../sql/syntax.md#show).

&quot;all&quot; is de standaarddatabasenaam die elke database- en schemacontainer in een sandbox bevat. Wanneer u een [!DNL PostgreSQL] verbinding gebruiken `dbname="all"`, kunt u **alle** database en schema die u hebt gemaakt om uw gegevens op logische wijze te ordenen.

Alle databases weergeven onder `dbname="all"` geeft drie beschikbare databases weer.

```sql
SHOW DATABASES;
  
name     
---------
databaseA
databaseB
databaseC
```

Alle schema&#39;s weergeven onder `dbname="all"` geeft de drie schema&#39;s weer die betrekking hebben op elke database in de sandbox.

```SQL
SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
databaseB      | schema3
```

Wanneer u een [!DNL PostgreSQL] verbinding gebruiken `dbname="databaseA"`kunt u elk schema openen dat aan die specifieke database is gekoppeld, zoals in het onderstaande voorbeeld wordt getoond.

```sql
SHOW DATABASES;
  
name     
---------
databaseA
 

SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
```

Met puntnotatie hebt u toegang tot elke tabel die is gekoppeld aan een specifiek schema dat is verbonden met de gekozen database. Door verbinding te maken met `DBNAME = databaseA.schema1;`, alle tabellen die aan dat specifieke schema zijn gekoppeld (`schema1`) worden weergegeven. Dit verstrekt informatie over welke dataset bevat welke lijst.

```sql
SHOW DATABASES;
  
name     
---------
databaseA


SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1


SHOW tables;
name       | type
----------------------
dataset1| table
dataset2| table
dataset3| table
```

## Gegevenselementen bijwerken of verwijderen uit een gegevenscontainer

Naarmate de hoeveelheid gegevenselementen in uw IMS-organisatie (of sandbox) toeneemt, wordt het nodig gegevenselementen bij te werken of te verwijderen uit een gegevenscontainer. Individuele elementen kunnen uit de organisatiecontainer worden verwijderd door met behulp van puntnotatie te verwijzen naar de juiste database- en schemanaam. De tabel en weergave (`t1` en `v1` respectievelijk) toegevoegd aan `databaseA.schema1` in het eerste voorbeeld worden verwijderd met behulp van de syntaxis in het volgende voorbeeld.

```sql
ALTER TABLE databaseA.schema2.t1 REMOVE SCHEMA databaseA.schema2;
ALTER VIEW databaseA.schema2.v1 REMOVE SCHEMA databaseA.schema2;
```

### Gegevenselementen verwijderen

De [DROP TABLE](../sql/syntax.md#drop-table) functie verwijdert een gegevenselement alleen fysiek uit het [!DNL Data Lake] wanneer er één verwijzing naar de tabel bestaat voor alle databases in uw IMS-organisatie.

```sql
DROP TABLE databaseA.schema2.t1;
```

### Een container van gegevenselementen verwijderen

Zowel de database als het schema kunnen ook worden verwijderd met behulp van standaard SQL-functies.

#### Een database verwijderen

Als er andere verwijzingen naar gegevensactiva verbonden aan het gegevensbestand zijn, zal de functie een fout veroorzaken wanneer het proberen om het gegevensbestand te verwijderen.

```sql
DROP DATABASE databaseA;
```

#### Een schema verwijderen

Er zijn drie belangrijke overwegingen om op te merken wanneer het verwijderen van een schema:

- Als u een schema verwijdert, worden gegevenselementen zoals tabellen, weergaven of tijdelijke tabellen niet fysiek verwijderd.
- Als er om het even welke gegevensactiva zijn die in het doelschema van verwijzingen worden voorzien en de wijze is RESTRICT, zal een uitzondering worden geworpen.
- Als er om het even welke gegevensactiva zijn die in het doelschema van verwijzingen worden voorzien en de wijze is CASCADE, verwijdert het systeem alle gegevensactiva die door de schemacontainer van verwijzingen worden voorzien en schrapt dan de schemacontainer.

```sql
DROP SCHEMA databaseA.schema2;
```

## Volgende stappen

Door dit document te lezen, hebt u nu een beter inzicht in de beste praktijken betreffende de organisatie en de structuur van uw gegevensactiva voor gebruik met de Dienst van de Vraag van Adobe Experience Platform. Het wordt geadviseerd verder te leren over de beste praktijken van de Dienst van de Vraag door te lezen over [documentatie over gegevensdeduplicatie](./deduplication.md).
