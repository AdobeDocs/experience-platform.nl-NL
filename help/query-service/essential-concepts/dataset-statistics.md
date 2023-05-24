---
title: Gegevensset Statistieken berekenen
description: In dit document wordt beschreven hoe u statistieken op kolomniveau kunt berekenen over ADLS-gegevenssets (Azure Data Lake Storage) met SQL-opdrachten.
source-git-commit: b063bcf7b3d2079715ac18fde55f47cea078b609
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# Berekening van gegevenssetstatistieken

U kunt nu statistieken op kolomniveau berekenen over [!DNL Azure Data Lake Storage] (ADLS) datasets met de `COMPUTE STATISTICS` en `SHOW STATISTICS` SQL-opdrachten. De SQL bevelen die datasetstatistieken gegevens verwerken zijn een uitbreiding van `ANALYZE TABLE` gebruiken. Volledige informatie over de `ANALYZE TABLE` kunt u vinden in het dialoogvenster [SQL-naslagdocumentatie](../sql/syntax.md#analyze-table).

>[!NOTE]
>
>De gegenereerde statistieken zijn momenteel alleen geldig voor die sessie en zijn niet blijvend tussen sessies. Deze bestanden zijn niet toegankelijk voor verschillende PSQL-sessies.

Met de `SHOW STATISTICS FOR <alias_name>` bevel, kunt u de statistieken zien die met werden gegevens verwerkt `ANALYZE TABLE COMPUTE STATISTICS` gebruiken. Door de combinatie van deze bevelen, kunt u kolomstatistieken over of de volledige dataset, een ondergroep van een dataset, alle kolommen, of een ondergroep van kolommen nu gegevens verwerken.

>[!IMPORTANT]
>
>De `COMPUTE STATISTICS`, `FILTERCONTEXT`, `FOR COLUMNS`, en `SHOW STATISTICS` bevelen worden niet gesteund op de lijsten van het gegevenspakhuis. Deze uitbreidingen voor de `ANALYZE TABLE` worden momenteel alleen ondersteund voor ADLS-tabellen. Zie voor meer informatie de [TABELsectie ANALYSEREN](../sql/syntax.md#analyze-table) van de SQL-syntaxishandleiding.

Deze gids helpt u uw vragen structureren zodat u de kolomstatistieken van een dataset van ADLS kunt gegevens verwerken. Gebruikend deze bevelen, kunt u de statistieken zien in uw zitting door een cliënt PSQL gebruikend een SQL vraag worden geproduceerd.

## Statistieken berekenen {#compute-statistics}

Er zijn aanvullende constructies toegevoegd aan de `ANALYZE TABLE` opdracht waarmee u **gegevens verwerken statistieken voor een ondergroep van een dataset en voor bepaalde kolommen**. Om dit te doen, moet u gebruiken `ANALYZE TABLE <tableName> COMPUTE STATISTICS` gebruiken.

>[!IMPORTANT]
>
>Het standaardgedrag berekent statistieken voor het **volledige gegevensset** en voor **alle kolommen**. Om statistieken over alle kolommen gegevens te verwerken, zou u het vraagformaat gebruiken `ANALYZE TABLE COMPUTE STATISTICS`. U bent **niet** geadviseerd om dit op een dataset ADLS te gebruiken, aangezien de grootte van de dataset zeer groot (potentieel petabytes van gegevens) kan zijn. In plaats daarvan moet u altijd overwegen de opdracht Analyseren uit te voeren met `FILTERCONTEXT` en een opgegeven lijst met kolommen. Zie de secties op [het beperken van geanalyseerde kolommen](#limit-included-columns) en [toevoegen, filtervoorwaarde](#filter-condition) voor meer informatie .

In het onderstaande voorbeeld worden statistieken voor de `adc_geometric` gegevensset en voor **alles** kolommen in de dataset.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS;
```

>[!NOTE]
>
>`COMPUTE STATISTICS` biedt geen ondersteuning voor de gegevenstypen array of map. U kunt een `skip_stats_for_complex_datatypes` markering die moet worden gewaarschuwd of die moet worden weergegeven als het invoerdataframe kolommen met arrays en kaartgegevenstypen bevat. De markering is standaard ingesteld op true. Gebruik de volgende opdracht om meldingen of fouten in te schakelen: `SET skip_stats_for_complex_datatypes = false`.

<!-- Commented out until the <alias_name> feature is released.
This second example, is a more real-world example as it uses an alias name. See the [alias name section](#alias-name) for more details on this feature.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS as <alias_name>;
``` -->

De consoleoutput toont niet de statistieken in antwoord op de analyze lijst gegevens statistische bevel gegevens. In plaats daarvan, zal de console één enkele rijkolom van tonen `Statistics ID` met een universeel unieke identificatiecode die naar de resultaten verwijst. Wanneer een `COMPUTE STATISTICS` vragen, worden de resultaten getoond als volgt:

```console
| Statistics ID    | 
| ---------------- |
| QqMtDfHQOdYJpZlb |
(1 row)
```

Als u de uitvoer wilt zien, moet u de opdracht `SHOW STATISTICS` gebruiken. Instructies over [hoe de statistieken worden weergegeven](#show-statistics) later in het document worden verstrekt.

## De opgenomen kolommen beperken {#limit-included-columns}

U kunt statistieken voor bepaalde datasetkolommen gegevens verwerken door hen door naam van verwijzingen te voorzien. Gebruik de `FOR COLUMNS (<col1>, <col2>)` syntaxis om specifieke kolommen als doel in te stellen. In het onderstaande voorbeeld worden statistieken voor de kolommen berekend  `commerce`, `id`, en `timestamp` voor de gegevensset `tableName`.

```sql
ANALYZE TABLE tableName COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

U kunt de statistieken voor om het even welk wortelniveau of genestelde kolom berekenen. In het volgende voorbeeld worden deze verwijzingen getoond.

```sql
ANALYZE TABLE adcgeometric COMPUTE STATISTICS FOR columns (commerce, commerce.purchases.value, commerce.productListAdds.value);
```

## Een filtervoorwaarde voor een tijdstempel toevoegen {#filter-condition}

U kunt een filtervoorwaarde toevoegen om de analyse van uw kolommen te concentreren. Dit kan worden gebruikt om historische gegevens uit te filteren of uw gegevensanalyse op een specifieke periode te concentreren. De `FILTERCONTEXT` het bevel berekent statistieken over een ondergroep van de dataset die op de filtervoorwaarde wordt gebaseerd u verstrekt.

In het onderstaande voorbeeld worden statistieken berekend over alle kolommen voor de gegevensset `tableName`, waarbij de kolomtijdstempel waarden bevat tussen het opgegeven bereik van `2023-04-01 00:00:00` en `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR ALL COLUMNS;
```

U kunt de kolomgrens en de filter combineren om hoogst specifieke computervragen voor uw datasetkolommen tot stand te brengen. De volgende query berekent bijvoorbeeld statistieken over de kolommen `commerce`, `id`, en `timestamp` voor de gegevensset `tableName`, waarbij de kolomtijdstempel waarden bevat tussen het opgegeven bereik van `2023-04-01 00:00:00` en `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR (columns commerce, id, timestamp);
```

<!-- ## Create an alias name {#alias-name}

Since the filter condition and the column list can target a large amount of data, it is unrealistic to remember the exact values. Instead, you can provide an `<alias_name>` to store this calculated information. If you do not provide an alias name for these calculations, Query Service generates a universally unique identifier for the alias ID. You can then use this alias ID to look up the computed statistics with the `SHOW STATISTICS` command. 

>[!NOTE]
>
>Although alias names are optional, you are recommended to use them as best practice.

The example below stores the output computed statistics in the `alias_name` for later reference.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS FOR ALL COLUMNS as alias_name;
```

The output for the above example is `SUCCESSFULLY COMPLETED, alias_name`. The console output does not display the statistics in the response of the analyze table compute statistics command. To see the output, you must use the `SHOW STATISTICS` command discussed below. -->

## De statistieken weergeven {#show-statistics}

<!-- Commented out until the <alias_name> feature is released.
The alias name used in the query is available as soon as the `ANALYZE TABLE` command has been run.  -->

Zelfs met een filtervoorwaarde en een kolomlijst, kan de berekening een grote hoeveelheid gegevens richten. De Dienst van de vraag produceert universeel uniek herkenningsteken voor statistiek identiteitskaart om deze berekende informatie op te slaan. U kunt dit statistiekidentiteitskaart dan gebruiken om omhoog de gegevens verwerkte statistieken met te zoeken `SHOW STATISTICS` op elk gewenst moment binnen die sessie.

De statistieken-id en de gegenereerde statistieken zijn alleen geldig voor deze specifieke sessie en kunnen niet worden geopend voor verschillende PSQL-sessies. De berekende statistieken zijn momenteel niet blijvend. Om de statistieken te tonen, gebruik het hieronder getoonde bevel.

```sql
SHOW STATISTICS FOR <STATISTICS_ID>;
```

Een uitvoer kan er ongeveer zo uitzien als in het onderstaande voorbeeld.

```console
                         columnName                         |      mean      |      max       |      min       | standardDeviation | approxDistinctCount | nullCount | dataType  
------------------------------------------------------------+----------------+----------------+----------------+-------------------+---------------------+-----------+-----------
 marketing.trackingcode                                     |            0.0 |            0.0 |            0.0 |               0.0 |              1213.0 |         0 | String
 _experience.analytics.session.timestamp                    |            450 |          -2313 |          21903 |               7.0 |                 0.0 |         0 | Long
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
(13 rows)
```

## Volgende stappen {#next-steps}

Door dit document te lezen, hebt u nu een beter inzicht in hoe te om de statistieken van het kolomniveau van een dataset van ADLS te produceren gebruikend een SQL vraag. U wordt aangeraden de [SQl-syntaxishandleiding](../sql/syntax.md) voor meer functies van de Adobe Experience Platform Query Service.
