---
title: Gegevensset Statistieken berekenen
description: Dit document beschrijft hoe te om kolom-vlakke statistieken over de datasets van de Opslag van de Verkeer van Gegevens van de Azure (ADLS) met SQL bevelen gegevens te verwerken.
source-git-commit: b94536be6e92354e237b99d36af13adf5a49afa7
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 0%

---

# Berekening van gegevenssetstatistieken

U kunt nu statistieken op kolomniveau berekenen over [!DNL Azure Data Lake Storage] (ADLS) datasets met de `COMPUTE STATISTICS` SQL-opdracht. De SQL bevelen die datasetstatistieken gegevens verwerken zijn een uitbreiding van `ANALYZE TABLE` gebruiken. Volledige informatie over de `ANALYZE TABLE` kan worden gevonden in [SQL-naslagdocumentatie](../sql/syntax.md#analyze-table).

>[!NOTE]
>
>De gegevens verwerkte statistieken worden opgeslagen in tijdelijke lijsten die zitting-vlakke persistentie hebben. U kunt de resultaten van de berekeningen op elk gewenst moment tijdens die sessie bekijken. Deze bestanden zijn niet toegankelijk voor verschillende PSQL-sessies.

Om de statistieken te zien die met werden berekend `ANALYZE TABLE COMPUTE STATISTICS` , kunt u een SELECT-query gebruiken voor de naam van de alias of de ID Statistieken. U kunt het werkingsgebied van de statistische analyse tot of de volledige dataset, een ondergroep van een dataset, alle kolommen, of een ondergroep van kolommen ook beperken.

>[!IMPORTANT]
>
>De `COMPUTE STATISTICS`, `FILTERCONTEXT`, en `FOR COLUMNS` opdrachten worden niet ondersteund in versnelde opslagtabellen. Deze uitbreidingen voor de `ANALYZE TABLE` worden momenteel alleen ondersteund voor ADLS-tabellen. Zie de klasse [TABELsectie ANALYSEREN](../sql/syntax.md#analyze-table) van de SQL-syntaxishandleiding.

Deze gids helpt u uw vragen structureren zodat u de kolomstatistieken van een dataset van ADLS kunt gegevens verwerken. Gebruikend deze bevelen, kunt u de statistieken zien in uw zitting door een cliënt PSQL gebruikend een SQL vraag worden geproduceerd.

## Statistieken berekenen {#compute-statistics}

Er zijn aanvullende constructies toegevoegd aan de `ANALYZE TABLE` bevel dat u toestaat **gegevens verwerken statistieken voor een ondergroep van een dataset en voor bepaalde kolommen**. Om gegevenssetstatistieken te berekenen, moet u gebruiken `ANALYZE TABLE <tableName> COMPUTE STATISTICS` gebruiken.

>[!IMPORTANT]
>
>Het standaardgedrag berekent statistieken voor het **volledige gegevensset** en voor **alle kolommen**. Om statistieken over alle kolommen gegevens te verwerken, zou u het vraagformaat gebruiken `ANALYZE TABLE COMPUTE STATISTICS`. U bent **niet** aanbevolen om de `COMPUTE STATISTICS` bevel zonder filters op een dataset ADLS, aangezien de grootte van de dataset zeer groot (potentieel petabytes van gegevens) kan zijn. In plaats daarvan moet u altijd overwegen de opdracht Analyseren uit te voeren met `FILTERCONTEXT` en een opgegeven lijst met kolommen. Zie de secties op [het beperken van geanalyseerde kolommen](#limit-included-columns) en [toevoegen, filtervoorwaarde](#filter-condition) voor meer informatie .

In het onderstaande voorbeeld worden statistieken voor de `adc_geometric` gegevensset en voor **alles** kolommen in de dataset.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS;
```

>[!NOTE]
>
>De `COMPUTE STATISTICS` geen ondersteuning voor de gegevenstypen array of map. U kunt een `skip_stats_for_complex_datatypes` markering die moet worden gewaarschuwd of die moet worden uitgevuld als het invoergegevensframe kolommen met arrays en gegevenstypen met hyperlinks bevat. De markering is standaard ingesteld op true. Gebruik de volgende opdracht om meldingen of fouten in te schakelen: `SET skip_stats_for_complex_datatypes = false`.

## Een alias maken {#alias-name}

Aangezien de resultaten van berekeningen een grote hoeveelheid gegevens kunnen zijn, is het onredelijk om de gegevens die zijn berekend direct in de consoleoutput terug te keren. Hoewel namen van aliassen optioneel zijn, wordt u aangeraden deze als beste praktijken te gebruiken wanneer u statistieken berekent. Geef een naam voor een alias op in de instructie om een beschrijvende verwijzing naar de resultaten in uw SQL-query&#39;s op te nemen. Als alternatief, automatisch geproduceerd `Statistics ID` wordt gegenereerd en gebruikt om de berekende informatie op te slaan.

In het onderstaande voorbeeld worden de berekende uitvoerstatistieken opgeslagen in de `alias_name` voor latere referentie. De in de query gebruikte aliasnaam is beschikbaar ter referentie zodra de `ANALYZE TABLE` is uitgevoerd.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS AS alias_name;
```

De uitvoer voor het bovenstaande voorbeeld is `SUCCESSFULLY COMPLETED, alias_name`. De consoleoutput toont niet de statistieken in de reactie op de analyze lijst gegevens statistische bevel gegevens. Om de gedetailleerde resultaten te zien, moet u een UITGEZOCHTE vraag op de aliasnaam of identiteitskaart van Statistieken gebruiken.

## De uitvoer van berekende statistieken weergeven {#view-output-of-computed-statistics}

Als u vooraf geen alias naam verstrekt, produceert de Dienst van de Vraag automatisch een naam voor `Statistics ID` die de vorm volgt van `<tableName_stats_{incremental_number}>`. Als een alias-naam is opgegeven, wordt deze weergegeven in het dialoogvenster `Statistics ID` kolom.

Een voorbeelduitvoer van een `COMPUTE STATISTICS` De query ziet er als volgt uit:

```console
| Statistics ID         | 
| --------------------- |
| adc_geometric_stats_1 |
(1 row)
```

U kunt vervolgens **vraag direct de gegevens verwerkte statistieken** door te verwijzen naar de `Statistics ID`. Met de onderstaande voorbeeldinstructie kunt u de uitvoer in zijn geheel weergeven wanneer deze wordt gebruikt met de opdracht `Statistics ID` of de naam van de alias.

```sql
SELECT * FROM adc_geometric_stats_1; 
```

De berekende statistische uitvoer kan er ongeveer zo uitzien als in het onderstaande voorbeeld.

```console
 columnName                                                 |      mean      |      max       |      min       | standardDeviation | approxDistinctCount | nullCount | dataType  
------------------------------------------------------------+----------------+----------------+----------------+-------------------+---------------------+-----------+-----------
 marketing.trackingcode                                     |            0.0 |            0.0 |            0.0 |               0.0 |              1213.0 |         0 | String
 _experience.analytics.customdimensions.evars.evar13        |            0.0 |            0.0 |            0.0 |               0.0 |              8765.0 |        20 | String
 _experience.analytics.customdimensions.evars.evar74        |            0.0 |            0.0 |            0.0 |               0.0 |                11.0 |         0 | String
 web.webpagedetails.name                                    |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | String
 _experience.analytics.event1to100.event8.value             |            5.0 |         9077.0 |          123.0 |              10.0 |              1001.0 |        80 | Double
 search.ispaid                                              |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | Boolean
 commerce.productlistviews.value                            |            0.0 |            0.0 |            0.0 |               0.0 |                 0.0 |        10 | Double
 device.typeid                                              |            0.0 |            0.0 |            0.0 |               0.0 |                 0.0 |        10 | String
 commerce.purchases.value                                   |          765.0 |        98760.0 |         -980.0 |              32.0 |                99.0 |        90 | Double
 _experience.analytics.customdimensions.props.prop45        |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | String
 environment.browserdetails.javaenabled                     |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | Boolean
 timestamp                                                  |            0.0 |            0.0 |            0.0 |               0.0 |                98.0 |         3 | Timestamp
(12 rows)
```

## De metagegevens van de statistische analyse weergeven {#show-statistics}

U kunt de `SHOW STATISTICS` gebruiken om de metagegevens weer te geven voor alle tijdelijke statistieken die in de sessie worden gegenereerd. Met deze opdracht kunt u het bereik van uw statistische analyse verfijnen.

Een voorbeeld van uitvoer van `SHOW STATISTICS` is hieronder weergegeven.

```console
      statsId         |   tableName   | columnSet |         filterContext       |      timestamp
----------------------+---------------+-----------+-----------------------------+--------------------
adc_geometric_stats_1 | adc_geometric |   (age)   |                             | 25/06/2023 09:22:26
demo_table_stats_1    |  demo_table   |    (*)    |       ((age > 25))          | 25/06/2023 12:50:26
age_stats             | castedtitanic |   (age)   | ((age > 25) AND (age < 40)) | 25/06/2023 09:22:26
```

Hieronder vindt u een beschrijving van de kolomnamen voor metagegevens.

| Kolomnaam | Beschrijving |
|---|---|
| `statsId` | Deze ID verwijst naar de tabel met tijdelijke statistieken die door de `COMPUTE STATISTICS` gebruiken. |
| `tableName` | De oorspronkelijke tabel die voor analyse is gebruikt. |
| `columnSet` | Een lijst van kolommen die specifiek voor analyse zijn gekozen. Een lege waarde geeft aan dat alle kolommen zijn geanalyseerd. Zie de sectie over [limiterende kolommen](#limit-included-columns) voor meer informatie . |
| `filterContext` | Een lijst met filters die op de analyse zijn toegepast. |
| `timestamp` | Eventuele chronologische filters die op de gegevensanalyse worden toegepast om zich op een bepaalde periode te concentreren. Zie de [sectie met tijdstempelfiltervoorwaarde](#filter-condition) voor meer informatie . |

U kunt de statistiek-id of aliasnaam gebruiken om de berekende statistieken op elk gewenst moment binnen die sessie op te zoeken met een SELECT-instructie. De statistieken-id en de gegenereerde statistieken zijn alleen geldig voor deze specifieke sessie en kunnen niet worden geopend voor verschillende PSQL-sessies. De berekende statistieken zijn momenteel niet blijvend. Zie de sectie over hoe te [bekijk de output van uw gegevens verwerkte statistieken](#view-output-of-computed-statistics) voor meer informatie .

## De opgenomen kolommen beperken {#limit-included-columns}

Om uw analyse te concentreren, kunt u statistieken voor bepaalde datasetkolommen berekenen door hen door naam van verwijzingen te voorzien. Gebruik de `FOR COLUMNS (<col1>, <col2>)` syntaxis om specifieke kolommen als doel in te stellen. In het onderstaande voorbeeld worden statistieken voor de kolommen berekend  `commerce`, `id`, en `timestamp` voor de gegevensset `tableName`.

```sql
ANALYZE TABLE tableName COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

U kunt de statistieken voor om het even welk wortelniveau of genestelde kolom berekenen. In het volgende voorbeeld worden deze verwijzingen getoond.

```sql
ANALYZE TABLE adcgeometric COMPUTE STATISTICS FOR columns (commerce, commerce.purchases.value, commerce.productListAdds.value);
```

## Een filtervoorwaarde voor een tijdstempel toevoegen {#filter-condition}

Als u de analyse van uw kolommen wilt concentreren op chronologie, kunt u een filtervoorwaarde voor een tijdstempel toevoegen. Deze voorwaarde kan worden gebruikt om historische gegevens uit te filteren of uw gegevensanalyse op een specifieke periode te concentreren. De `FILTERCONTEXT` het bevel berekent statistieken over een ondergroep van de dataset die op de filtervoorwaarde wordt gebaseerd die u verstrekt.

In het onderstaande voorbeeld worden statistieken berekend over alle kolommen voor de gegevensset `tableName`, waarbij de kolomtijdstempel waarden bevat tussen het opgegeven bereik van `2023-04-01 00:00:00` en `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR ALL COLUMNS;
```

U kunt de kolomgrens en de filter combineren om hoogst specifieke computervragen voor uw datasetkolommen tot stand te brengen. De volgende query berekent bijvoorbeeld statistieken over de kolommen `commerce`, `id`, en `timestamp` voor de gegevensset `tableName`, waarbij de kolomtijdstempel waarden bevat tussen het opgegeven bereik van `2023-04-01 00:00:00` en `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

## Volgende stappen {#next-steps}

Door dit document te lezen, hebt u nu een beter inzicht in hoe te om kolom-vlakke statistieken van een dataset van ADLS te produceren gebruikend een SQL vraag. U wordt aangeraden de [SQl-syntaxishandleiding](../sql/syntax.md) voor meer functies van de Adobe Experience Platform Query Service.
