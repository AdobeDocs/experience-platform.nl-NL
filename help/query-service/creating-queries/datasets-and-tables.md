---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Datasets vs tabellen en schema's
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# Datasets vs tabellen en schema&#39;s

Bekijk de lijst met gegevenssets die beschikbaar is in de gebruikersinterface [van het](https://platform.adobe.com/datasets)Adobe Experience Platform, waarbij u zeker weet dat u de namen van de gegevenssets wilt observeren.
>[!NOTE] Sommige namen van gegevenssets hebben spaties en zijn anders mogelijk niet SQL veilig.

![](../images/queries/datasets-and-tables/dataset-names.png)


Herzie de hiërarchische structuur van het schema van de Dataset in UI door op een schemanaam in de datasetlijst te klikken.

![](../images/queries/datasets-and-tables/schema-information.png)

Open de PSQL-opdrachtregel en gebruik de verbindingsdetails vanaf hier: [https://platform.adobe.com/query/configuration](https://platform.adobe.com/query/configuration).

![](../images/clients/psql/connect-bi.png)

Als u de beschikbare tabellen op Platform met SQL wilt weergeven, kunt u een van deze tabellen gebruiken `\d` of `SHOW TABLES;`.


`\d` geeft de standaard PostSQL-weergave weer

```
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

`SHOW TABLES;` is een douanebevel dat een meer gedetailleerde mening geeft en de lijst, evenals de datasetnaam voorstelt die in Platform UI wordt gevonden.

```
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

Als u het hoofdschema van een tabel wilt weergeven, gebruikt u de `\d table_name` opdracht.

>[!NOTE] Het voorgestelde schema toont de wortelgebieden, die de meesten complex zijn, die naar een type van Objecten in het schema UI van de Dataset worden verwezen.

`\d luma_midvalues`

```
                         Table "public.luma_midvalues"
      Column       |             Type            | Collation | Nullable | Default 
-------------------+-----------------------------+-----------+----------+---------
 timestamp         | timestamp                   |           |          | 
 _id               | text                        |           |          | 
 productlistitems  | anyarray                    |           |          | 
 commerce          | luma_midvalues_commerce     |           |          | 
 receivedtimestamp | timestamp                   |           |          | 
 enduserids        | luma_midvalues_enduserids   |           |          | 
 datasource        | datasource                  |           |          | 
 web               | luma_midvalues_web          |           |          | 
 placecontext      | luma_midvalues_placecontext |           |          | 
 identitymap       | anymap                      |           |          | 
 marketing         | marketing                   |           |          | 
 environment       | luma_midvalues_environment  |           |          | 
 _experience       | luma_midvalues__experience  |           |          | 
 device            | device                      |           |          | 
 search            | search                      |           |          | 
```

Om verder in het schema te gaan, gebruik onderstrepingstekens (`_`) om de kolom in de lijst te verklaren u wilt beschrijven. Bijvoorbeeld: `\d table_name_column`

`\d luma_midvalues_web`

```
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```
