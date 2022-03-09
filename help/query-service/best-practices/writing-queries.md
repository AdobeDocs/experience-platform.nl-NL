---
keywords: Experience Platform;huis;populaire onderwerpen;vraagdienst;de dienst van de vraag;het schrijven van vragen;het schrijven vraag;
solution: Experience Platform
title: Algemene begeleiding voor de Uitvoering van de Vraag in de Dienst van de Vraag
topic-legacy: queries
type: Tutorial
description: Dit document bevat belangrijke details die u moet weten wanneer u query's schrijft in Adobe Experience Platform Query Service.
exl-id: a7076c31-8f7c-455e-9083-cbbb029c93bb
source-git-commit: c0e7ae8f65aa0373d35a55d4da46e0ffcb0e60f9
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 2%

---

# Algemene richtlijnen voor het uitvoeren van query&#39;s in [!DNL Query Service]

In dit document worden belangrijke gegevens vermeld die u moet weten wanneer u query&#39;s schrijft in Adobe Experience Platform [!DNL Query Service].

Voor gedetailleerde informatie over de SQL-syntaxis die wordt gebruikt in [!DNL Query Service], lees de [SQL-syntaxisdocumentatie](../sql/syntax.md).

## Uitvoeringsmodellen voor query

Adobe Experience Platform [!DNL Query Service] heeft twee modellen van vraaguitvoering: interactief en niet-interactief. De interactieve uitvoering wordt gebruikt voor vraagontwikkeling en rapportgeneratie in bedrijfsintelligentiehulpmiddelen, terwijl niet-interactief voor grotere banen en operationele vragen als deel van een werkschema van de gegevensverwerking wordt gebruikt.

### Interactieve queryuitvoering

De vragen kunnen interactief worden uitgevoerd door hen door voor te leggen [!DNL Query Service] UI of [via een verbonden client](../clients/overview.md). Bij uitvoering [!DNL Query Service] via een verbonden client een actieve sessie wordt uitgevoerd tussen de client en [!DNL Query Service] tot of de voorgelegde vraagwinst of tijden uit.

De interactieve vraaguitvoering heeft de volgende beperkingen:

| Parameter | Beperking |
| --------- | ---------- |
| Time-out query | 10 minuten |
| Maximumaantal geretourneerde rijen | 50 000 |
| Maximum aantal gelijktijdige query&#39;s | 5 |

>[!NOTE]
>
>Als u de maximale rijbeperking wilt overschrijven, neemt u `LIMIT 0` in uw query. De zoektime-out van 10 minuten is nog steeds van toepassing.

Standaard worden de resultaten van interactieve query&#39;s geretourneerd aan de client en zijn deze **niet** aanhoudend. Om de resultaten als dataset in [!DNL Experience Platform], moet de query de `CREATE TABLE AS SELECT` syntaxis.

### Niet-interactieve query-uitvoering

Vragen ingediend via [!DNL Query Service] API wordt niet-interactief uitgevoerd. Niet-interactieve uitvoering betekent dat [!DNL Query Service] ontvangt de API-aanroep en voert de query uit in de volgorde waarin deze is ontvangen. Niet-interactieve query&#39;s resulteren altijd in het genereren van een nieuwe dataset in [!DNL Experience Platform] om de resultaten te ontvangen, of de toevoeging van nieuwe rijen in een bestaande dataset.

## Een specifiek veld binnen een object openen

Als u toegang wilt krijgen tot een veld binnen een object in de query, kunt u beide puntnotaties gebruiken (`.`) of vierkante haakjes (`[]`). De volgende SQL-instructie gebruikt puntnotatie om de `endUserIds` object naar beneden `mcid` object.

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | De naam van de analystabel. |

De volgende SQL-instructie gebruikt haakjes om de `endUserIds` object naar beneden `mcid` object.

```sql
SELECT endUserIds['_experience']['mcid']
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
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

De geretourneerde `endUserIds._experience.mcid` object bevat de overeenkomende waarden voor de volgende parameters:

- `id`
- `namespace`
- `primary`

Wanneer de kolom alleen omlaag wordt gedeclareerd naar het object, wordt het gehele object als een tekenreeks geretourneerd. Als u alleen de id wilt weergeven, gebruikt u:

```sql
SELECT endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
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

Het enkele citaat (`'`) wordt gebruikt om tekstreeksen te maken. Deze kan bijvoorbeeld worden gebruikt in het dialoogvenster `SELECT` instructie om een statische tekstwaarde te retourneren in het resultaat en in de `WHERE` clausule om de inhoud van een kolom te evalueren.

Met de volgende query wordt een statische tekstwaarde gedeclareerd (`'datasetA'`) voor een kolom:

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

De volgende query gebruikt een tekenreeks tussen aanhalingstekens (`'homepage'`) in de WHERE-component om gebeurtenissen voor een specifieke pagina te retourneren.

```sql
SELECT 
  timestamp,
  endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE web.webPageDetails.name = 'homepage'
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

### Dubbele aanhalingstekens

Het dubbele aanhalingsteken (`"`) wordt gebruikt om een id met spaties te declareren.

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
>Dubbele aanhalingstekens **kan** worden gebruikt met toegang tot puntnotatievelden.

### Achter aanhalingstekens

The back quote `` ` `` wordt gebruikt om gereserveerde kolomnamen te omzeilen **alleen** bij gebruik van puntnotatiesyntaxis. Bijvoorbeeld sinds `order` is een gereserveerd woord in SQL, moet u backquotes gebruiken om tot het gebied toegang te hebben `commerce.order`:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

Achteraanhalingstekens worden ook gebruikt om toegang te krijgen tot een veld dat met een getal begint. Als u bijvoorbeeld toegang wilt krijgen tot het veld `30_day_value`, moet u de notatie voor aanhalingstekens gebruiken.

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

Achter aanhalingstekens zijn **niet** nodig als u haakjes gebruikt.

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
 LIMIT 10
```

## Tabelgegevens weergeven

Na het verbinden met de Dienst van de Vraag, kunt u al uw beschikbare lijsten op Platform zien door of `\d` of `SHOW TABLES` opdrachten.

### Standaardtabelweergave

De `\d` toont de standaard PostSQL-weergave voor het weergeven van tabellen. Een voorbeeld van de output van dit bevel kan hieronder worden gezien:

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

Als u meer gedetailleerde informatie over de schema&#39;s in de tabel wilt weergeven, kunt u de opdracht `\d {TABLE_NAME}` opdracht, waar `{TABLE_NAME}` is de naam van de lijst waarvan schemainformatie u wilt bekijken.

In het volgende voorbeeld worden de schemagegevens voor het `luma_midvalues` tabel, die u kunt zien met `\d luma_midvalues`:

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

Bovendien kunt u meer informatie over een bepaalde kolom krijgen door de naam van de kolom aan de lijstnaam toe te voegen. Dit wordt in de notatie geschreven `\d {TABLE_NAME}_{COLUMN}`.

In het volgende voorbeeld wordt aanvullende informatie voor het `web` kolom, en zou worden aangehaald door het volgende bevel te gebruiken: `\d luma_midvalues_web`:

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```

## Gegevenssets samenvoegen

U kunt zich bij veelvoudige datasets aansluiten samen om gegevens van andere datasets in uw vraag te omvatten.

Het volgende voorbeeld zou zich bij de volgende twee datasets (`your_analytics_table` en `custom_operating_system_lookup`) en maakt een `SELECT` voor de bovenste 50 besturingssystemen op basis van het aantal paginaweergaven.

**Query**

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE TIMESTAMP >= TO_TIMESTAMP('2018-01-01') AND TIMESTAMP <= TO_TIMESTAMP('2018-12-31')
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
| Mobile iOS 6.1.3 | 119069,0 |
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

De Dienst van de vraag steunt gegevensdeduplicatie, of de verwijdering van dubbele rijen uit gegevens. Lees voor meer informatie over deduplicatie de [Handleiding voor deduplicatie van Query Service](./deduplication.md).

## De berekeningen van de tijdzone in de Dienst van de Vraag

De Service van de vraag normaliseert persisted gegevens in Adobe Experience Platform gebruikend het timestamp formaat UTC. Voor meer informatie over hoe te om uw tijdzonevereiste aan en van een timestamp UTC te vertalen, gelieve te zien [sectie Veelgestelde vragen over het wijzigen van de tijdzone van en naar een UTC-tijdstempel](../troubleshooting-guide.md#How-do-I-change-the-time-zone-to-and-from-a-UTC-Timestamp?).

## Volgende stappen

Door dit document te lezen, bent u op enkele belangrijke overwegingen geïntroduceerd wanneer het schrijven van vragen gebruikend [!DNL Query Service]. Voor meer informatie over hoe u de SQL-syntaxis kunt gebruiken om uw eigen query&#39;s te schrijven, leest u de [SQL-syntaxisdocumentatie](../sql/syntax.md).

Voor meer steekproeven van vragen die binnen de Dienst van de Vraag kunnen worden gebruikt, te lezen gelieve de gidsen op [Adobe Analytics-voorbeeldvragen](../sample-queries/adobe-analytics.md), [Adobe Target-voorbeeldvragen](../sample-queries/adobe-target.md), of [Voorbeeldquery&#39;s van ExperienceEvent](../sample-queries/experience-event.md).
