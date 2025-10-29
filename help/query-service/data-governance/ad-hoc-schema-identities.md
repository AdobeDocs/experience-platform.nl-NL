---
title: Primaire id's instellen in een ad-hocgegevensset
description: Met de Adobe Experience Platform Query Service kunt u een identiteit of een primaire identiteit voor de gegevenssetvelden van een ad-hocschema rechtstreeks instellen via de SQL-opdracht ALTER TABLE. Het document verklaart hoe te om het ALTER bevel van de LIJST te gebruiken om een primaire identiteit of een secundaire identiteit te plaatsen.
exl-id: b8e6b87e-c6e5-4688-a936-a3a1510a3c5b
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# Primaire id&#39;s instellen in een ad-hocgegevensset

Met Adobe Experience Platform Query Service kunt u gegevenssetkolommen markeren als primaire of secundaire identiteiten met behulp van beperkingen voor de SQL-opdracht `ALTER TABLE` . U kunt deze functie gebruiken om ervoor te zorgen dat gemarkeerde velden voldoen aan de privacyvereisten voor gegevens. Dit bevel staat u toe om beperkingen voor zowel primaire als secundaire kolommen van de identiteitslijst direct door SQL toe te voegen of te schrappen.

## Aan de slag

Voor het labelen van gegevenssetkolommen als primaire of secundaire identiteit is een goed begrip van de SQL-opdracht van `ALTER TABLE` en van de privacyvereisten voor gegevens vereist. Lees de volgende documentatie voordat u doorgaat met dit document:

* [ de SQL syntaxisgids voor het `ALTER TABLE` bevel ](../sql/syntax.md).
* [ het overzicht van het Beleid van Gegevens ](../../data-governance/home.md) voor meer informatie.

## Beperkingen toevoegen {#add-constraints}

Met de opdracht `ALTER TABLE` kunt u een gegevenssetkolom labelen als de identiteit van een persoon en dat label vervolgens gebruiken als een primaire identiteit door de bijbehorende metagegevens bij te werken met SQL. Dit is vooral nuttig wanneer de datasets door SQL eerder dan direct van een schema door Experience Platform UI worden gecreeerd. U kunt deze opdracht gebruiken om ervoor te zorgen dat uw gegevensbewerkingen in Experience Platform compatibel zijn met het beleid voor gegevensgebruik.

**Voorbeelden**

In het volgende voorbeeld wordt een beperking toegevoegd aan de bestaande `t1` -tabel. De waarden van de kolom `id` worden nu gemarkeerd als primaire identiteiten onder de naamruimte `IDFA` . Een naamruimte van een identiteit is een trefwoord dat het type identiteitsgegevens declareert dat het veld vertegenwoordigt.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
```

Het tweede voorbeeld zorgt ervoor dat de kolom `id` als secundaire identiteit duidelijk is.

```sql
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

## Beperkingen voor neerzetten {#drop-constraints}

Restricties kunnen ook uit tabelkolommen worden verwijderd met de opdracht `ALTER TABLE` .

**Voorbeelden**

In het volgende voorbeeld wordt de vereiste verwijderd dat de kolom `c1` een primaire identiteit in de bestaande `t1` -tabel krijgt.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
```

Zoals u hieronder ziet, wordt dezelfde syntaxis gebruikt voor het verwijderen van een identiteitsbeperking.

```sql
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

## Identiteiten tonen

Gebruik de opdracht Metagegevens `show identities` in de opdrachtregelinterface om een tabel weer te geven met alle kenmerken die als identiteit zijn toegewezen.

```shell
> show identities;
```

Hieronder wordt een voorbeeld van een geretourneerde tabel weergegeven.

```console
 tableName | columnName | datatype | namespace | ifPrimary
|-----------+------------+----------+-----------+----------
(0 rows)
```

## XDM-beperkingen {#limitations}

In de volgende lijst worden belangrijke overwegingen beschreven voor het bijwerken van identiteiten in bestaande gegevenssets bij het gebruik van XDM.

* Om een kolom als identiteit te specificeren, moet u **** ook namespace bepalen die als meta-gegevens voor de kolom moet worden bewaard.
* XDM ondersteunt het opgeven van een kolomnaam in het naamruimtekenmerk niet.
* Als uw schema het `identityMap` XDM gebied gebruikt, moet het wortel of top-level `identityMap` voorwerp **** als identiteit of primaire identiteit worden geëtiketteerd.
