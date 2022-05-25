---
title: Primaire id's instellen in een ad-hocgegevensset
description: Met de Adobe Experience Platform Query Service kunt u een identiteit of een primaire identiteit voor de gegevenssetvelden van een ad-hocschema rechtstreeks instellen via de SQL-opdracht ALTER TABLE. Het document verklaart hoe te om het ALTER bevel van de LIJST te gebruiken om een primaire identiteit of een secundaire identiteit te plaatsen.
source-git-commit: bf51fc3e0c9635c0555f87f3389fb4a9542c092d
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---

# Primaire id&#39;s instellen in een ad-hocgegevensset

De Dienst van de Vraag van Adobe Experience Platform staat u toe om datasetkolommen als of primaire of secundaire identiteiten te merken gebruikend beperkingen voor SQL `ALTER TABLE` gebruiken. U kunt deze functie gebruiken om ervoor te zorgen dat gemarkeerde velden voldoen aan de privacyvereisten voor gegevens. Dit bevel staat u toe om beperkingen voor zowel primaire als secundaire kolommen van de identiteitslijst direct door SQL toe te voegen of te schrappen.

## Aan de slag

De kolommen van de gegevensreeks van het etiket als primaire of secundaire identiteit vereisen een begrip van het `ALTER TABLE` SQL-opdracht en een goed begrip van de privacyvereisten voor gegevens. Lees de volgende documentatie voordat u doorgaat met dit document:

* [De SQL-syntaxishandleiding voor de `ALTER TABLE` command](../sql/syntax.md).
* [Overzicht van gegevensbeheer](../../data-governance/home.md) voor meer informatie .

## Beperkingen toevoegen {#add-constraints}

De `ALTER TABLE` staat u toe om een datasetkolom als identiteit van een persoon te etiketteren en dan dat etiket als primaire identiteit te gebruiken door de bijbehorende meta-gegevens bij te werken gebruikend SQL. Dit is vooral nuttig wanneer de datasets door SQL eerder dan direct van een schema door het Platform UI worden gecreeerd. De opdracht kan worden gebruikt om ervoor te zorgen dat uw gegevensbewerkingen in het Platform compatibel zijn met het beleid voor gegevensgebruik.

**Voorbeelden**

In het volgende voorbeeld wordt een beperking toegevoegd aan het bestaande `t1` tabel. De waarden van de `id` de kolom is nu gemarkeerd als primaire identiteiten onder de `IDFA` naamruimte. Een naamruimte van een identiteit is een trefwoord dat het type identiteitsgegevens declareert dat het veld vertegenwoordigt.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
```

Het tweede voorbeeld zorgt ervoor dat de `id` wordt gemarkeerd als een secundaire identiteit.

```sql
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

## Beperkingen voor neerzetten {#drop-constraints}

Restricties kunnen ook uit tabelkolommen worden verwijderd met de opdracht `ALTER TABLE` gebruiken.

**Voorbeelden**

In het volgende voorbeeld wordt de vereiste dat de `c1` een primaire identiteit in de bestaande kolom `t1` tabel.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
```

Zoals u hieronder ziet, wordt dezelfde syntaxis gebruikt voor het verwijderen van een identiteitsbeperking.

```sql
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

## Identiteiten tonen

De opdracht Metagegevens gebruiken `show identities` van de interface van de bevellijn om een lijst met elke attributen te tonen die als identiteit wordt toegewezen.

```shell
> show identities;
```

Hieronder wordt een voorbeeld van een geretourneerde tabel weergegeven.

```console
 tableName | columnName | datatype | namespace | ifPrimary
-----------+------------+----------+-----------+----------
(0 rows)
```

## XDM-beperkingen {#limitations}

In de volgende lijst worden belangrijke overwegingen beschreven voor het bijwerken van identiteiten in bestaande gegevenssets bij het gebruik van XDM.

* Als u een kolom als een identiteit wilt opgeven, **moet** Definieer ook de naamruimte die als metagegevens voor de kolom moet worden behouden.
* XDM ondersteunt het opgeven van een kolomnaam in het naamruimtekenmerk niet.
* Als uw schema het `identityMap` XDM-veld, hoofdveld of hoofdniveau `identityMap` object **moet** als identiteit of primaire identiteit worden geëtiketteerd.
