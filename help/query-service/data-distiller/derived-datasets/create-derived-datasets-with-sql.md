---
title: Afgeleide gegevensbestanden maken met SQL
description: Leer hoe te om SQL te gebruiken om een afgeleide dataset tot stand te brengen die voor profiel wordt toegelaten, en hoe te om de dataset voor de Dienst van het Profiel en van de Segmentatie van de Klant in real time te gebruiken.
exl-id: bb1a1d8d-4662-40b0-857a-36efb8e78746
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1238'
ht-degree: 0%

---

# Afgeleide datasets maken met SQL

Leer hoe te om SQL vragen te gebruiken om gegevens van bestaande datasets te manipuleren en om te zetten om een afgeleide dataset tot stand te brengen die voor Profiel wordt toegelaten. Dit werkschema verstrekt een efficiënte, alternatieve methode om afgeleide datasets voor uw zaken van het bedrijfsgebruik van het Profiel van de Klant in real time te creëren.

Dit document schetst diverse geschikte SQL uitbreidingen die een afgeleide dataset voor gebruik met het Profiel van de Klant in real time produceren. De workflow vereenvoudigt het proces dat u anders zou moeten voltooien via verschillende API-aanroepen of Experience Platform UI-interacties.

Typisch, zou het produceren van en het publiceren van een afgeleide dataset voor het Profiel van de Klant in real time de volgende stappen impliceren:

* Maak een naamruimte voor identiteiten als deze nog niet bestaat.
* Creeer het datatype om de afgeleide dataset op te slaan, indien nodig.
* Creeer een gebiedsgroep met dat datatype om de afgeleide datasetinformatie op te slaan.
* Maak of wijs een primaire identiteitskolom toe met de naamruimte die u eerder hebt gemaakt.
* Maak een schema met de veldgroep en het datatype dat u eerder hebt gemaakt.
* Creeer een nieuwe dataset gebruikend uw schema en laat het voor profiel toe, indien nodig.
* Markeer optioneel een dataset als profiel-toegelaten.

Nadat u de hierboven vermelde stappen hebt uitgevoerd, kunt u de gegevensset vullen. Als u de dataset voor profiel toeliet, kunt u segmenten tot stand brengen die naar de nieuwe dataset verwijzen en beginnen inzichten te produceren.

De Dienst van de vraag staat u toe om alle hierboven vermelde acties uit te voeren gebruikend SQL vragen. Dit omvat het aanbrengen van veranderingen in uw datasets en gebiedsgroepen indien nodig.

## Een tabel maken met een optie om deze in te schakelen voor profiel {#enable-dataset-for-profile}

>[!NOTE]
>
>De hieronder opgegeven SQL-query gaat uit van het gebruik van een bestaande naamruimte.

Gebruik een Create Lijst als Uitgezochte vraag (CTAS) om een dataset tot stand te brengen, datatypes toe te wijzen, een primaire identiteit te plaatsen, een schema tot stand te brengen, en het te merken als profiel-toegelaten. De voorbeeld-SQL-instructie hieronder maakt een gegevensset en stelt deze beschikbaar voor Real-Time Customer Data Platform (Real-Time CDP). Uw SQL-query heeft de indeling die in het onderstaande voorbeeld wordt getoond:

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

U kunt gegevenssets ook inschakelen voor profielen via de gebruikersinterface van Experience Platform. Voor meer informatie bij het merken van een dataset zoals toegelaten voor profiel, zie [ een dataset voor de documentatie van het Profiel van de Klant in real time ](../../../catalog/datasets/user-guide.md#enable-profile) toelaten.

In de onderstaande voorbeeldquery wordt de `decile_table` dataset gemaakt met `id` als de primaire identiteitskolom en heeft deze de naamruimte `IDFA` . Het heeft ook een gebied genoemd `decile1Month` van het gegevenstype van de kaart. De gemaakte tabel (`decile_table`) is ingeschakeld voor het profiel.

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

Gebruik `label='PROFILE'` voor een `CREATE TABLE` -opdracht om een voor profielen geschikte gegevensset te maken. De functie `upsert` is standaard ingeschakeld. De functie `upsert` kan worden overschreven met de opdracht `ALTER` , zoals in het onderstaande voorbeeld wordt getoond.

```sql
ALTER TABLE <your_table_name> DROP label upsert;
```

Zie de SQl syntaxisdocumentatie voor meer informatie over het gebruik van [ VERANDERT het bevel van de LIJST ](../../sql/syntax.md#alter-table) en [ etiket als deel van een vraag CTAS ](../../sql/syntax.md#create-table-as-select).

## Construeert om met het beheren van afgeleide datasets door SQL te helpen

De hieronder beschreven eigenschappen zijn van groot nut wanneer het beheren van afgeleide datasets door SQL.

### Bestaande gegevenssets wijzigen die moeten worden ingeschakeld voor profiel {#enable-existing-dataset-for-profile}

De SQL-constructie ALTER TABLE kan worden gebruikt om bestaande gegevenssets geschikt te maken voor profiel. Dit vereist dat een profiel-toegelaten markering aan zowel het schema als de overeenkomstige dataset wordt toegevoegd.

```sql
ALTER TABLE your_decile_table ADD label 'PROFILE';
```

>[!NOTE]
>
>Wanneer de opdracht `ALTER TABLE` met succes is uitgevoerd, retourneert de console `ALTER SUCCESS` .

### Een primaire identiteit toevoegen aan een bestaande gegevensset {#add-primary-identity}

Markeer een bestaande kolom in een dataset als primaire identiteitsreeks, anders, resulteert het in een fout. Als u een primaire identiteit wilt instellen met SQL, gebruikt u de hieronder weergegeven query-indeling.

```sql
ALTER TABLE <your_table_name> ADD CONSTRAINT primary identity NAMESPACE
```

Bijvoorbeeld:

```sql
ALTER TABLE test1_dataset ADD CONSTRAINT PRIMARY KEY(id2) NAMESPACE 'IDFA';
```

In het opgegeven voorbeeld is `id2` een bestaande kolom in `test1_dataset` .

### Een gegevensset voor profiel uitschakelen {#disable-dataset-for-profile}

Als u uw lijst voor profielgebruik wilt onbruikbaar maken, moet u het bevel DROP gebruiken. Een voorbeeld van een SQL-instructie die USES `DROP` gebruikt, wordt hieronder weergegeven.

```sql
ALTER TABLE table_name DROP LABEL 'PROFILE';
```

Bijvoorbeeld:

```sql
ALTER TABLE decile_table DROP label 'PROFILE';
```

Deze SQL-instructie biedt een efficiënte alternatieve methode voor het gebruik van een API-aanroep. Voor meer informatie, zie de documentatie over hoe te [ een dataset voor gebruik met Real-Time CDP onbruikbaar maken gebruikend datasets API ](../../../catalog/datasets/enable-upsert.md#disable-the-dataset-for-profile).

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

Deze SQL-instructie biedt een efficiënte alternatieve methode voor het gebruik van een API-aanroep. Voor meer informatie, zie de documentatie over hoe te [ een dataset voor gebruik met Real-Time CDP en UPSERT toelaten gebruikend datasets API ](../../../catalog/datasets/enable-upsert.md#enable-the-dataset).

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

Aanvullende metagegevens worden bewaard voor gegevenssets waarvoor profielen zijn ingeschakeld. Gebruik de opdracht `SHOW TABLES` om een extra `labels` -kolom weer te geven die informatie bevat over eventuele labels die aan tabellen zijn gekoppeld.

Een voorbeeld van de output van dit bevel kan hieronder worden gezien:

```sql
       name          |        dataSetId         |     dataSet    | description | labels 
|---------------------+--------------------------+----------------+-------------+----------
 luma_midvalues      | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues     | 5c86b896b3c162151785b43c | Luma midValues |             | false
 table_with_a_decile | 5c86b896b3c162151785b43c | Luma midValues |             | 'UPSERT', 'PROFILE'
(3 rows)
```

U kunt van het voorbeeld zien dat `table_with_a_decile` voor profiel is toegelaten en met etiketten zoals [ &quot;UPSERT&quot;](#enable-upsert-functionality-for-dataset), [ &quot;PROFILE&quot;](#enable-existing-dataset-for-profile) zoals vroeger beschreven.

### Een veldgroep met SQL maken

Veldgroepen kunnen nu worden gemaakt met SQL. Dit verstrekt een alternatief aan het gebruiken van de Redacteur van het Schema binnen Experience Platform UI of het maken van een API vraag aan de schemaregistratie.

Een voorbeeldinstructie voor het maken van een veldgroep vindt u hieronder.

```sql
CREATE FIELDGROUP <field_group_name> [IF NOT EXISTS]  (field_name <data_type> primary identity namespace <namespace>, [field_name_2 >data_type>]) [ WITH(LABEL='PROFILE') ];
```

>[!IMPORTANT]
>
>Het maken van veldgroepen via SQL mislukt als de markering `label` niet wordt opgegeven in de instructie of als de veldgroep al bestaat.
>>Zorg ervoor dat de query een `IF NOT EXISTS` -component bevat om te voorkomen dat de query mislukt omdat de veldgroep al bestaat.

Een echt voorbeeld lijkt misschien op het onderstaande voorbeeld.

```sql
CREATE FIELDGROUP field_group_for_test123 (decile1Month map<text, integer>, decile3Month map<text, integer>, decile6Month map<text, integer>, decile9Month map<text, integer>, decile12Month map<text, integer>, decilelietime map<text, integer>) WITH (LABEL-'PROFILE');
```

Als deze instructie met succes wordt uitgevoerd, wordt de gemaakte veldgroep-id geretourneerd. Bijvoorbeeld `c731a1eafdfdecae1683c6dca197c66ed2c2b49ecd3a9525` .

Zie de documentatie op hoe te [ een nieuwe gebiedsgroep in de Redacteur van het Schema ](../../../xdm/ui/resources/field-groups.md#create) tot stand brengen of het gebruiken van de [ schemaregistratie API ](../../../xdm/api/field-groups.md#create) voor meer informatie over alternatieve methodes.

### Een veldgroep neerzetten

Soms is het nodig een veldgroep uit het schemaregister te verwijderen. Dit wordt gedaan door het bevel `DROP FIELDGROUP` met gebiedsgroep identiteitskaart uit te voeren

```sql
DROP FIELDGROUP [IF EXISTS] <your_field_group_id>;
```

Bijvoorbeeld:

```sql
DROP FIELDGROUP field_group_for_test123;
```

>[!IMPORTANT]
>
>Het verwijderen van een veldgroep via SQL mislukt als de veldgroep niet bestaat. Zorg ervoor dat de instructie een `IF EXISTS` -component bevat om mislukken van de query te voorkomen.

### Alle veldgroepnamen en id&#39;s voor uw tabellen weergeven

De opdracht `SHOW FIELDGROUPS` retourneert een tabel die de naam, veldgroupId en eigenaar van de tabellen bevat.

Een voorbeeld van de output van dit bevel kan hieronder worden gezien:

```sql
       name                      |        fieldgroupId                             |     owner      |
|---------------------------------+-------------------------------------------------+-----------------
 AEP Mobile Lifecycle Details    | _experience.aep-mobile-lifecycle-details        | Luma midValues |
 AEP Web SDK ExperienceEvent     | _experience.aep-web-sdk-experienceevent         | Luma midValues |
 AJO Classification Fields       | _experience.journeyOrchestration.classification | Luma midValues |
 AJO Entity Fields               | _experience.customerJourneyManagement.entities  | Luma midValues |
(4 rows)
```

## Volgende stappen

Na het lezen van dit document, hebt u een beter inzicht in hoe te om SQL te gebruiken om een profiel en upsert-Toegelaten dataset tot stand te brengen die op afgeleide datasets wordt gebaseerd. U bent nu klaar om deze dataset met de werkschema&#39;s van de partijopname te gebruiken om updates aan uw profielgegevens te maken. Om meer over het opnemen van gegevens in Adobe Experience Platform te leren, gelieve te beginnen door het [ overzicht van de gegevensinvoer te lezen ](../../../ingestion/home.md).
