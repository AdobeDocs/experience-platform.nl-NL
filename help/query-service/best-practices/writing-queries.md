---
keywords: Experience Platform;huis;populaire onderwerpen;vraagdienst;de dienst van de vraag;het schrijven van vragen;het schrijven vraag;
solution: Experience Platform
title: Algemene begeleiding voor de Uitvoering van de Vraag in de Dienst van de Vraag
topic: queries
type: Tutorial
description: Dit document bevat belangrijke details die u moet weten wanneer u query's schrijft in Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: 97dc0b5fb44f5345fd89f3f56bd7861668da9a6e
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 2%

---


# Algemene begeleiding voor vraaguitvoering in [!DNL Query Service]

Dit document bevat belangrijke details die u moet weten wanneer u query&#39;s schrijft in Adobe Experience Platform [!DNL Query Service].

Lees de [SQL-syntaxisdocumentatie](../sql/syntax.md) voor gedetailleerde informatie over de SQL-syntaxis die in [!DNL Query Service] wordt gebruikt.

## Uitvoeringsmodellen voor query

Adobe Experience Platform [!DNL Query Service] heeft twee modellen van vraaguitvoering: interactief en niet-interactief. De interactieve uitvoering wordt gebruikt voor vraagontwikkeling en rapportgeneratie in bedrijfsintelligentiehulpmiddelen, terwijl niet-interactief voor grotere banen en operationele vragen als deel van een werkschema van de gegevensverwerking wordt gebruikt.

### Interactieve queryuitvoering

U kunt query&#39;s interactief uitvoeren door ze via de gebruikersinterface [!DNL Query Service] of [via een verbonden client](../clients/overview.md) te verzenden. Wanneer het lopen [!DNL Query Service] door een verbonden cliënt, een actieve zittingslooppas tussen de cliënt en [!DNL Query Service] tot of de voorgelegde vraag terugkeert of tijden uit.

De interactieve vraaguitvoering heeft de volgende beperkingen:

| Parameter | Beperking |
| --------- | ---------- |
| Time-out query | 10 minuten |
| Maximumaantal geretourneerde rijen | 50 000 |
| Maximum aantal gelijktijdige query&#39;s | 5 |

>[!NOTE]
>
>Als u de maximale rijbeperking wilt overschrijven, neemt u `LIMIT 0` op in de query. De zoektime-out van 10 minuten is nog steeds van toepassing.

Standaard worden de resultaten van interactieve query&#39;s geretourneerd aan de client en **not** blijft bestaan. Om de resultaten als dataset in [!DNL Experience Platform] voort te zetten, moet de vraag `CREATE TABLE AS SELECT` syntaxis gebruiken.

### Niet-interactieve query-uitvoering

Vragen die via de [!DNL Query Service] API worden ingediend, worden niet-interactief uitgevoerd. De niet-interactieve uitvoering betekent dat [!DNL Query Service] de API vraag ontvangt en de vraag in de orde uitvoert het wordt ontvangen. Niet-interactieve query&#39;s resulteren altijd in het genereren van een nieuwe dataset in [!DNL Experience Platform] om de resultaten te ontvangen, of in het invoegen van nieuwe rijen in een bestaande dataset.

## Een specifiek veld binnen een object openen

Om tot een gebied binnen een voorwerp in uw vraag toegang te hebben, kunt u of puntaantekening (`.`) of haakjesaantekening (`[]`) gebruiken. De volgende SQL-instructie gebruikt puntnotatie om het `endUserIds`-object omlaag te verplaatsen naar het `mcid`-object.

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | De naam van de analystabel. |

De volgende SQL-instructie gebruikt haakjesnotatie om het `endUserIds`-object omlaag te verplaatsen naar het `mcid`-object.

```sql
SELECT endUserIds['_experience']['mcid']
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | De naam van de analystabel. |

>[!NOTE]
>
>Aangezien elk notatietype dezelfde resultaten retourneert, blijft de notatie die u wilt gebruiken bij uw voorkeur.

Beide voorbeeldquery&#39;s hierboven retourneren een samengevoegd object in plaats van één waarde:

```console
              endUserIds._experience.mcid   
--------------------------------------------------------
 (48168239533518554367684086979667672499,"(ECID)",true)
(1 row)
```

Het geretourneerde `endUserIds._experience.mcid`-object bevat de overeenkomende waarden voor de volgende parameters:

- `id`
- `namespace`
- `primary`

Wanneer de kolom alleen omlaag wordt gedeclareerd naar het object, wordt het gehele object als een tekenreeks geretourneerd. Als u alleen de id wilt weergeven, gebruikt u:

```sql
SELECT endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

```console
     endUserIds._experience.mcid.id 
----------------------------------------
 48168239533518554367684086979667672499
(1 row)
```

## Aanhalingstekens

De enige citaten, de dubbele citaten, en de achtercitaten hebben verschillend gebruik binnen de vragen van de Dienst van de Vraag.

### Enkele aanhalingstekens

Het enkele citaat (`'`) wordt gebruikt om tekstkoorden tot stand te brengen. Het kan bijvoorbeeld worden gebruikt in de instructie `SELECT` om een statische tekstwaarde in het resultaat te retourneren en in de component `WHERE` om de inhoud van een kolom te evalueren.

Met de volgende query wordt een statische tekstwaarde (`'datasetA'`) gedeclareerd voor een kolom:

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

De volgende vraag gebruikt één-geciteerde koord (`'homepage'`) in zijn WAAR clausule om gebeurtenissen voor een specifieke pagina terug te keren.

```sql
SELECT 
  timestamp,
  endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE web.webPageDetails.name = 'homepage'
LIMIT 10
```

### Dubbele aanhalingstekens

Het dubbele aanhalingsteken (`"`) wordt gebruikt om een herkenningsteken met ruimten te verklaren.

De volgende query gebruikt dubbele aanhalingstekens om waarden uit opgegeven kolommen te retourneren wanneer één kolom een spatie in de id bevat:

```sql
SELECT
  no_space_column,
  "space column"
FROM
( SELECT 
    'column1' as no_space_column,
    'column2' as "space column"
)
```

>[!NOTE]
>
>Dubbele aanhalingstekens **kunnen niet** worden gebruikt met toegang tot puntnotatieveld.

### Achter aanhalingstekens

Het achtercitaat `` ` `` wordt gebruikt om gereserveerde kolomnamen **only** te ontsnappen wanneer het gebruiken van de syntaxis van de puntnotatie. Aangezien `order` bijvoorbeeld een gereserveerd woord is in SQL, moet u backquotes gebruiken om het veld `commerce.order` te openen:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

Achteraanhalingstekens worden ook gebruikt om toegang te krijgen tot een veld dat met een getal begint. Als u bijvoorbeeld toegang wilt krijgen tot het veld `30_day_value`, moet u een notatie voor een backcitaat gebruiken.

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

Achter citaten zijn **niet** nodig als u steun-aantekening gebruikt.

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 LIMIT 10
```

## Tabelgegevens weergeven

Na het verbinden met de Dienst van de Vraag, kunt u al uw beschikbare lijsten op Platform zien door of `\d` of `SHOW TABLES` bevelen te gebruiken.

### Standaardtabelweergave

Met de opdracht `\d` wordt de standaardweergave van PostSQL voor het weergeven van tabellen weergegeven. Een voorbeeld van de output van dit bevel kan hieronder worden gezien:

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

### Gedetailleerde tabelweergave

`SHOW TABLES` bevel is een douanebevel dat gedetailleerdere informatie over de lijsten verstrekt. Een voorbeeld van de output van dit bevel kan hieronder worden gezien:

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

### Schema-informatie

Als u meer gedetailleerde informatie over de schema&#39;s in de tabel wilt weergeven, kunt u de opdracht `\d {TABLE_NAME}` gebruiken, waarbij `{TABLE_NAME}` de naam is van de tabel waarvan u de schemagegevens wilt weergeven.

Het volgende voorbeeld toont de schemainformatie voor de `luma_midvalues` lijst, die door `\d luma_midvalues` te gebruiken zou worden gezien:

```sql
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

Bovendien kunt u meer informatie over een bepaalde kolom krijgen door de naam van de kolom aan de lijstnaam toe te voegen. Dit zou in het formaat `\d {TABLE_NAME}_{COLUMN}` worden geschreven.

Het volgende voorbeeld toont extra informatie voor de `web` kolom, en zou worden aangehaald door het volgende bevel te gebruiken: `\d luma_midvalues_web`:

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```

## Gegevenssets samenvoegen

U kunt zich bij veelvoudige datasets aansluiten samen om gegevens van andere datasets in uw vraag te omvatten.

In het volgende voorbeeld worden de volgende twee datasets (`your_analytics_table` en `custom_operating_system_lookup`) samengevoegd en wordt een instructie `SELECT` voor de bovenste 50 besturingssystemen gemaakt op basis van het aantal paginaweergaven.

**Query**

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE TIMESTAMP >= ('2018-01-01') AND TIMESTAMP <= ('2018-12-31')
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

**Resultaten**

| Besturingssysteem | PageViews |
| --------------- | --------- |
| Windows 7 | 2781979,0 |
| Windows XP | 1669824,0 |
| Windows 8 | 420024,0 |
| Adobe AIR | 315032,0 |
| Windows Vista | 173566,0 |
| Mobiele iOS 6.1.3 | 119069,0 |
| Linux | 56516,0 |
| OSX 10.6.8 | 53652,0 |
| Android 4.0.4 | 46167,0 |
| Android 4.0.3 | 31852,0 |
| Windows Server 2003 en XP x64 Edition | 2883,0 |
| Android 4.1.1 | 2436,0 |
| Android 2.3.6 | 15735,0 |
| OSX 10.6 | 1357,0 |
| Windows Phone 7.5 | 11054,0 |
| Android 4.3 | 9221,0 |

## Deduplicatie

De Dienst van de vraag steunt gegevensdeduplicatie, of de verwijdering van dubbele rijen uit gegevens. Lees voor meer informatie over deduplicatie de [Handleiding voor het dedupliceren van Query Service](./deduplication.md).

## Volgende stappen

Door dit document te lezen, bent u aan sommige belangrijke overwegingen geïntroduceerd wanneer het schrijven van vragen gebruikend [!DNL Query Service]. Voor meer informatie over hoe te om de SQL syntaxis te gebruiken om uw eigen vragen te schrijven, te lezen gelieve [SQL syntaxisdocumentatie](../sql/syntax.md).

Voor meer voorbeelden van vragen die binnen de Dienst van de Vraag kunnen worden gebruikt, te lezen gelieve de gidsen op [Adobe Analytics steekproefvragen](./adobe-analytics.md), [Adobe Target steekproefvragen](./adobe-target.md), of [ExperienceEvent steekproefvragen](./experience-event-queries.md).