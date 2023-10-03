---
title: Naadloze SQL-stroom voor afgeleide kenmerken
description: SQL van de Dienst van de vraag is uitgebreid om naadloze steun voor afgeleide attributen te verlenen. Leer hoe te om deze SQL uitbreiding te gebruiken om een afgeleid attribuut tot stand te brengen dat voor profiel wordt toegelaten, en hoe te om de attributen voor het Profiel en de Dienst van de Segmentatie van de Klant in real time te gebruiken.
exl-id: bb1a1d8d-4662-40b0-857a-36efb8e78746
source-git-commit: e9c4068419b36da6ffaec67f0d1c39fe87c2bc4c
workflow-type: tm+mt
source-wordcount: '1238'
ht-degree: 1%

---

# Naadloze SQL-stroom voor afgeleide kenmerken

SQL van de Dienst van de vraag is uitgebreid om naadloze steun voor afgeleide attributen te verlenen. Dit verstrekt een efficiënte alternatieve methode om afgeleide attributen voor uw zaken gebruiksgevallen van het Profiel van de Klant in real time tot stand te brengen.

Dit document schetst diverse geschikte SQL uitbreidingen die een afgeleid attribuut voor gebruik met het Profiel van de Klant in real time produceren. Het werkschema vereenvoudigt het proces dat u anders door diverse API vraag of de interactie van het Platform UI zou moeten voltooien.

Typisch, zou het produceren van en het publiceren van een attribuut voor het Profiel van de Klant in real time de volgende stappen impliceren:

* Maak een naamruimte voor identiteiten als deze nog niet bestaat.
* Maak indien nodig het gegevenstype om het afgeleide kenmerk op te slaan.
* Maak een veldgroep met dat gegevenstype om de afgeleide kenmerkinformatie op te slaan.
* Maak of wijs een primaire identiteitskolom toe met de naamruimte die u eerder hebt gemaakt.
* Maak een schema met de veldgroep en het datatype dat u eerder hebt gemaakt.
* Creeer een nieuwe dataset gebruikend uw schema en laat het voor profiel toe, indien nodig.
* Markeer optioneel een dataset als profiel-toegelaten.

Nadat u de hierboven vermelde stappen hebt uitgevoerd, kunt u de gegevensset vullen. Als u de dataset voor profiel toeliet, kunt u segmenten ook tot stand brengen die naar de nieuwe attributen verwijzen en beginnen inzichten te produceren.

De Dienst van de vraag staat u toe om alle hierboven vermelde acties uit te voeren gebruikend SQL vragen. Dit omvat het aanbrengen van veranderingen in uw datasets en gebiedsgroepen indien nodig.

## Een tabel maken met een optie om deze in te schakelen voor profiel {#enable-dataset-for-profile}

>[!NOTE]
>
>De hieronder opgegeven SQL-query gaat uit van het gebruik van een bestaande naamruimte.

Gebruik een Create Lijst als Uitgezochte vraag (CTAS) om een dataset tot stand te brengen, datatypes toe te wijzen, een primaire identiteit te plaatsen, een schema tot stand te brengen, en het te merken als profiel-toegelaten. De voorbeeld-SQL-instructie hieronder maakt kenmerken en stelt deze beschikbaar voor Real-time Customer Data Platform (Real-Time CDP). Uw SQL-query heeft de indeling die in het onderstaande voorbeeld wordt getoond:

```sql
CREATE TABLE <your_table_name> [IF NOT EXISTS] (fieldname <your_data_type> primary identity namespace <your_namespace>, [field_name2 <your_data_type>]) [WITH(LABEL='PROFILE')];
```

De volgende gegevenstypen worden ondersteund: boolean, date, datetime, text, float, bigint, integer, map, array en struct/row.

Het SQl-codeblok hieronder biedt voorbeelden om struct/row-, map- en arraydatatypen te definiëren. Regel één toont rijsyntaxis. Regel twee toont kaartsyntaxis, en lijn drie, seriesyntaxis.

```sql {line-numbers="true"}
ROW (Column_name <data_type> [, column name <data_type> ]*)
MAP <data_type, data_type>
ARRAY <data_type>
```

Alternatief, kunnen de datasets ook voor profiel door Platform UI worden toegelaten. Voor meer informatie over het merken van een dataset zoals toegelaten voor profiel, zie [laat een dataset voor de documentatie van het Profiel van de Klant in real time toe](../../../catalog/datasets/user-guide.md#enable-profile).

In de onderstaande voorbeeldquery worden de `decile_table` dataset wordt gecreeerd met `id` als primaire identiteitskolom en heeft de naamruimte `IDFA`. Het heeft ook een veld met de naam `decile1Month` van het gegevenstype Map. De gemaakte tabel (`decile_table`) is ingeschakeld voor profiel.

```sql
CREATE TABLE decile_table (id text PRIMARY KEY NAMESPACE 'IDFA', 
            decile1Month map<text, integer>) WITH (label='PROFILE');
```

Bij succesvolle uitvoering van de vraag, wordt dataset identiteitskaart teruggekeerd aan de console, zoals die in het hieronder voorbeeld wordt gezien.

```console
Created Table DataSet Id
>
637fd84969ba291e62dba79f
(1 row)
```

Gebruiken `label='PROFILE'` op `CREATE TABLE` bevel om een profiel-toegelaten dataset tot stand te brengen. De `upsert` mogelijkheid is standaard ingeschakeld. De `upsert` kan worden overschreven met behulp van de `ALTER` gebruiken, zoals in het onderstaande voorbeeld wordt getoond.

```sql
ALTER TABLE <your_table_name> DROP label upsert;
```

Zie de syntaxisdocumentatie van SQl voor meer informatie over het gebruik van [ALTER TABLE](../../sql/syntax.md#alter-table) en [label als onderdeel van een CTAS-query](../../sql/syntax.md#create-table-as-select).

## Construeert om met het beheren van afgeleide attributen door SQL te helpen

De hieronder beschreven functies zijn van groot nut wanneer het beheren van afgeleide attributen door SQL.

### Bestaande gegevenssets wijzigen die moeten worden ingeschakeld voor profiel {#enable-existing-dataset-for-profile}

De SQL-constructie ALTER TABLE kan worden gebruikt om bestaande gegevenssets geschikt te maken voor profiel. Dit vereist dat een profiel-toegelaten markering aan zowel het schema als de overeenkomstige dataset wordt toegevoegd.

```sql
ALTER TABLE your_decile_table ADD label 'PROFILE';
```

>[!NOTE]
>
>Bij een geslaagde uitvoering van de `ALTER TABLE` bevel, keert de console terug `ALTER SUCCESS`.

### Een primaire identiteit toevoegen aan een bestaande gegevensset {#add-primary-identity}

Markeer een bestaande kolom in een dataset als primaire identiteitsreeks, anders, resulteert het in een fout. Als u een primaire identiteit wilt instellen met SQL, gebruikt u de hieronder weergegeven query-indeling.

```sql
ALTER TABLE <your_table_name> ADD CONSTRAINT primary identity NAMESPACE
```

Bijvoorbeeld:

```sql
ALTER TABLE test1_dataset ADD CONSTRAINT PRIMARY KEY(id2) NAMESPACE 'IDFA';
```

In het gegeven voorbeeld: `id2` is een bestaande kolom in `test1_dataset`.

### Een gegevensset voor profiel uitschakelen {#disable-dataset-for-profile}

Als u uw lijst voor profielgebruik wilt onbruikbaar maken, moet u het bevel DROP gebruiken. Een voorbeeld-SQL-instructie die GEBRUIKT `DROP` is hieronder weergegeven.

```sql
ALTER TABLE table_name DROP LABEL 'PROFILE';
```

Bijvoorbeeld:

```sql
ALTER TABLE decile_table DROP label 'PROFILE';
```

Deze SQL-instructie biedt een efficiënte alternatieve methode voor het gebruik van een API-aanroep. Zie de documentatie over het [een dataset voor gebruik met Real-Time CDP onbruikbaar maken gebruikend datasets API](../../../catalog/datasets/enable-upsert.md#disable-the-dataset-for-profile).

### De functionaliteit voor bijwerken en invoegen van uw gegevensset toestaan {#enable-upsert-functionality-for-dataset}

Met de opdracht UPSERT kunt u een nieuwe record invoegen of bestaande gegevens in een tabel bijwerken. Met name kunt u een bestaande rij bijwerken als een opgegeven waarde al in een tabel bestaat, of een nieuwe rij invoegen als de opgegeven waarde nog niet bestaat.

Een voorbeeldinstructie die de juiste indeling gebruikt, wordt hieronder weergegeven.

```sql
ALTER TABLE table_name ADD LABEL 'UPSERT';
```

Bijvoorbeeld:

```sql
ALTER TABLE table_with_a_decile ADD label 'UPSERT';
```

Deze SQL-instructie biedt een efficiënte alternatieve methode voor het gebruik van een API-aanroep. Zie de documentatie over het [een gegevensset inschakelen voor gebruik met Real-Time CDP en UPSERT met behulp van de API voor gegevenssets](../../../catalog/datasets/enable-upsert.md#enable-the-dataset).

### De update- en invoegfunctionaliteit voor uw gegevensset uitschakelen {#disable-upsert-functionality-for-dataset}

Dit bevel maakt de capaciteit onbruikbaar om rijen in uw dataset bij te werken en op te nemen.

Een voorbeeldinstructie die de juiste indeling gebruikt, wordt hieronder weergegeven.

```sql
ALTER TABLE table_name DROP LABEL 'UPSERT';
```

Bijvoorbeeld:

```sql
ALTER TABLE table_with_a_decile DROP label 'UPSERT';
```

### Aanvullende tabelinformatie voor elke tabel tonen {#show-labels-for-tables}

Aanvullende metagegevens worden bewaard voor gegevenssets waarvoor profielen zijn ingeschakeld. Gebruik de `SHOW TABLES` opdracht om een extra `labels` kolom die informatie over om het even welke etiketten verstrekt verbonden aan lijsten.

Een voorbeeld van de output van dit bevel kan hieronder worden gezien:

```sql
       name          |        dataSetId         |     dataSet    | description | labels 
---------------------+--------------------------+----------------+-------------+----------
 luma_midvalues      | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues     | 5c86b896b3c162151785b43c | Luma midValues |             | false
 table_with_a_decile | 5c86b896b3c162151785b43c | Luma midValues |             | 'UPSERT', 'PROFILE'
(3 rows)
```

Uit het voorbeeld blijkt dat `table_with_a_decile` is ingeschakeld voor profiel en toegepast met labels zoals [&#39;UPSERT&#39;](#enable-upsert-functionality-for-dataset), [&quot;PROFIEL&quot;](#enable-existing-dataset-for-profile) zoals eerder beschreven.

### Een veldgroep met SQL maken

Veldgroepen kunnen nu worden gemaakt met SQL. Dit verstrekt een alternatief aan het gebruiken van de Redacteur van het Schema binnen het Platform UI of het maken van een API vraag aan de schemaregistratie.

Een voorbeeldinstructie voor het maken van een veldgroep vindt u hieronder.

```sql
CREATE FIELDGROUP <field_group_name> [IF NOT EXISTS]  (field_name <data_type> primary identity namespace <namespace>, [field_name_2 >data_type>]) [ WITH(LABEL='PROFILE') ];
```

>[!IMPORTANT]
>
>Het maken van veldgroepen via SQL mislukt als de `label` markering wordt niet opgegeven in de instructie of als de veldgroep al bestaat.
>Zorg ervoor dat de query een `IF NOT EXISTS` component om te voorkomen dat de query mislukt omdat de veldgroep al bestaat.

Een echt voorbeeld lijkt misschien op het onderstaande voorbeeld.

```sql
CREATE FIELDGROUP field_group_for_test123 (decile1Month map<text, integer>, decile3Month map<text, integer>, decile6Month map<text, integer>, decile9Month map<text, integer>, decile12Month map<text, integer>, decilelietime map<text, integer>) WITH (LABEL-'PROFILE');
```

Als deze instructie met succes wordt uitgevoerd, wordt de gemaakte veldgroep-id geretourneerd. Bijvoorbeeld `c731a1eafdfdecae1683c6dca197c66ed2c2b49ecd3a9525`.

Zie de documentatie over hoe u [een nieuwe veldgroep maken in de Schema-editor](../../../xdm/ui/resources/field-groups.md#create) of door [schema-register-API](../../../xdm/api/field-groups.md#create) voor meer informatie over alternatieve methoden.

### Een veldgroep neerzetten

Soms is het nodig een veldgroep uit het schemaregister te verwijderen. Dit wordt gedaan door uit te voeren `DROP FIELDGROUP` gebruiken met de veldgroep-id.

```sql
DROP FIELDGROUP [IF EXISTS] <your_field_group_id>;
```

Bijvoorbeeld:

```sql
DROP FIELDGROUP field_group_for_test123;
```

>[!IMPORTANT]
>
>Het verwijderen van een veldgroep via SQL mislukt als de veldgroep niet bestaat. Zorg ervoor dat de instructie een `IF EXISTS` clausule om de vraag te vermijden ontbreekt.

### Alle veldgroepnamen en id&#39;s voor uw tabellen weergeven

De `SHOW FIELDGROUPS` het bevel keert een lijst terug die de naam, fieldGroupId, en eigenaar van de lijsten bevat.

Een voorbeeld van de output van dit bevel kan hieronder worden gezien:

```sql
       name                      |        fieldgroupId                             |     owner      |
---------------------------------+-------------------------------------------------+-----------------
 AEP Mobile Lifecycle Details    | _experience.aep-mobile-lifecycle-details        | Luma midValues |
 AEP Web SDK ExperienceEvent     | _experience.aep-web-sdk-experienceevent         | Luma midValues |
 AJO Classification Fields       | _experience.journeyOrchestration.classification | Luma midValues |
 AJO Entity Fields               | _experience.customerJourneyManagement.entities  | Luma midValues |
(4 rows)
```

## Volgende stappen

Na het lezen van dit document hebt u een beter inzicht in hoe u SQL kunt gebruiken om een profiel en een voor upsert ingeschakelde gegevensset te maken op basis van afgeleide kenmerken. U bent nu klaar om deze dataset met de werkschema&#39;s van de partijopname te gebruiken om updates aan uw profielgegevens te maken. Als u meer wilt weten over het opnemen van gegevens in Adobe Experience Platform, leest u eerst de [gegevensinvoer - overzicht](../../../ingestion/home.md).
