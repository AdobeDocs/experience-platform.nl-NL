---
keywords: Experience Platform;home;populaire onderwerpen;query-service;Query-service;query's schrijven;query schrijven;
solution: Experience Platform
title: Algemene begeleiding voor de Uitvoering van de Vraag in de Dienst van de Vraag
type: Tutorial
description: In dit document worden belangrijke gegevens beschreven die u moet weten wanneer u query's schrijft in Adobe Experience Platform Query Service.
exl-id: a7076c31-8f7c-455e-9083-cbbb029c93bb
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 2%

---

# Algemene richtlijnen voor het uitvoeren van query&#39;s in [!DNL Query Service]

Dit document bevat belangrijke informatie die u moet weten wanneer u query&#39;s schrijft in Adobe Experience Platform [!DNL Query Service] .

Voor gedetailleerde informatie over de SQL syntaxis die in [!DNL Query Service] wordt gebruikt, te lezen gelieve de [&#x200B; SQL syntaxisdocumentatie &#x200B;](../sql/syntax.md).

## Uitvoeringsmodellen voor query

Adobe Experience Platform [!DNL Query Service] heeft twee modellen voor het uitvoeren van query&#39;s: interactief en niet-interactief. De interactieve uitvoering wordt gebruikt voor vraagontwikkeling en rapportgeneratie in bedrijfsintelligentiehulpmiddelen, terwijl niet-interactief voor grotere banen en operationele vragen als deel van een werkschema van de gegevensverwerking wordt gebruikt.

### Interactieve queryuitvoering

De vragen kunnen interactief worden uitgevoerd door hen door [!DNL Query Service] UI of [&#x200B; door een verbonden cliënt &#x200B;](../clients/overview.md) voor te leggen. Wanneer [!DNL Query Service] via een verbonden client wordt uitgevoerd, wordt een actieve sessie uitgevoerd tussen de client en [!DNL Query Service] totdat de verzonden query terugkeert of de time-out.

De interactieve vraaguitvoering heeft de volgende beperkingen:

| Parameter | Beperking |
| --------- | ---------- |
| Time-out query | 10 minuten |
| Maximumaantal geretourneerde rijen | 50.000 |
| Maximum aantal gelijktijdige query&#39;s | 5 |

>[!NOTE]
>
>Als u de maximale rijbeperking wilt overschrijven, neemt u `LIMIT 0` op in de query. De zoektime-out van 10 minuten is nog steeds van toepassing.

Door gebrek, worden de resultaten van interactieve vragen teruggekeerd aan de cliënt en **niet** voortgeduurd. Om de resultaten als dataset in [!DNL Experience Platform] voort te zetten, moet de vraag de `CREATE TABLE AS SELECT` syntaxis gebruiken.

### Niet-interactieve query-uitvoering

Vragen die via de [!DNL Query Service] API worden verzonden, worden niet-interactief uitgevoerd. Niet-interactieve uitvoering betekent dat [!DNL Query Service] de API-aanroep ontvangt en de query uitvoert in de volgorde waarin deze wordt ontvangen. Niet-interactieve query&#39;s resulteren altijd in het genereren van een nieuwe dataset in [!DNL Experience Platform] om de resultaten te ontvangen, of in het invoegen van nieuwe rijen in een bestaande dataset.

## Een specifiek veld binnen een object openen

Om tot een gebied binnen een voorwerp in uw vraag toegang te hebben, kunt u of puntaantekening (`.`) of haakjesaantekening (`[]`) gebruiken. De volgende SQL-instructie gebruikt puntnotatie om het `endUserIds` -object omlaag te verplaatsen naar het `mcid` -object.

>[!NOTE]
>
>De Experience Cloud-id (ECID) wordt ook wel MCID genoemd en wordt nog steeds gebruikt in naamruimten.

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

De volgende SQL-instructie gebruikt haakjesnotatie om het `endUserIds` -object omlaag te verplaatsen naar het `mcid` -object.

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
|--------------------------------------------------------
 (48168239533518554367684086979667672499,"(ECID)",true)
(1 row)
```

Het geretourneerde `endUserIds._experience.mcid` -object bevat de overeenkomende waarden voor de volgende parameters:

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
|----------------------------------------
 48168239533518554367684086979667672499
(1 row)
```

## Aanhalingen

De enige citaten, de dubbele citaten, en de achtercitaten hebben verschillend gebruik binnen de vragen van de Dienst van de Vraag.

### Enkele aanhalingstekens

Het enige citaat (`'`) wordt gebruikt om tekstkoorden tot stand te brengen. U kunt deze bijvoorbeeld gebruiken in de instructie `SELECT` om een statische tekstwaarde te retourneren in het resultaat en in de component `WHERE` om de inhoud van een kolom te evalueren.

Met de volgende query wordt een statische tekstwaarde (`'datasetA'`) gedeclareerd voor een kolom:

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

De volgende vraag gebruikt één-geciteerde koord (`'homepage'`) in zijn WAAR clausule om gebeurtenissen voor een specifieke pagina terug te keren.

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

Het dubbele citaat (`"`) wordt gebruikt om een herkenningsteken met ruimten te verklaren.

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
>De dubbele citaten **kunnen** niet met het gebiedstoegang van de puntnotatie worden gebruikt.

### Achter aanhalingstekens

Het achtercitaat `` ` `` wordt gebruikt om gereserveerde kolomnamen **slechts** te ontsnappen wanneer het gebruiken van de syntaxis van de puntnotatie. Omdat `order` bijvoorbeeld een gereserveerd woord is in SQL, moet u backquotes gebruiken om toegang te krijgen tot het veld `commerce.order` :

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

Achteraanhalingstekens worden ook gebruikt om toegang te krijgen tot een veld dat met een getal begint. Als u bijvoorbeeld toegang wilt krijgen tot het veld `30_day_value` , moet u de notatie voor aanhalingstekens gebruiken.

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

De achtercitaten zijn **niet** nodig als u steun-aantekening gebruikt.

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
 LIMIT 10
```

## Tabelgegevens weergeven

Nadat u verbinding hebt gemaakt met Query Service, kunt u al uw beschikbare tabellen op Experience Platform weergeven met de opdrachten `\d` of `SHOW TABLES` .

### Standaardtabelweergave

De opdracht `\d` toont de standaardweergave van [!DNL PostgreSQL] voor het weergeven van tabellen. Een voorbeeld van de output van dit bevel kan hieronder worden gezien:

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
|--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

### Gedetailleerde tabelweergave

`SHOW TABLES` is een aangepaste opdracht die gedetailleerdere informatie over de tabellen biedt. Een voorbeeld van de output van dit bevel kan hieronder worden gezien:

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
|-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

### Schema-informatie

Als u meer gedetailleerde informatie over de schema&#39;s in de tabel wilt weergeven, gebruikt u de opdracht `\d {TABLE_NAME}` , waarbij `{TABLE_NAME}` de naam is van de tabel waarvan u de schemagegevens wilt weergeven.

In het volgende voorbeeld worden de schemagegevens voor de tabel `luma_midvalues` weergegeven, die u kunt zien met `\d luma_midvalues` :

```sql
                         Table "public.luma_midvalues"
      Column       |             Type            | Collation | Nullable | Default 
|-------------------+-----------------------------+-----------+----------+---------
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

Bovendien kunt u meer informatie over een bepaalde kolom krijgen door de naam van de kolom aan de lijstnaam toe te voegen. Dit wordt geschreven in de notatie `\d {TABLE_NAME}_{COLUMN}` .

In het volgende voorbeeld wordt aanvullende informatie voor de kolom `web` getoond, die met de volgende opdracht wordt aangeroepen: `\d luma_midvalues_web`

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
|----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```

## Gegevenssets samenvoegen

U kunt zich bij veelvoudige datasets aansluiten samen om gegevens van andere datasets in uw vraag te omvatten.

In het volgende voorbeeld worden de volgende twee gegevenssets (`your_analytics_table` en `custom_operating_system_lookup` ) samengevoegd en wordt een instructie `SELECT` voor de bovenste 50 besturingssystemen gemaakt op basis van het aantal paginaweergaven.

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
| Windows Server 2003 en XP x64 Edition | 28883,0 |
| Android 4.1.1 | 24336,0 |
| Android 2.3.6 | 15735,0 |
| OSX 10.6 | 13357,0 |
| Windows Phone 7.5 | 11054,0 |
| Android 4.3 | 9221,0 |

## Deduplicatie

De Dienst van de vraag steunt gegevensdeduplicatie, of de verwijdering van dubbele rijen uit gegevens. Voor meer informatie over deduplicatie, te lezen gelieve de [&#x200B; gids van de Deduplicatie van de Dienst van de Vraag &#x200B;](../key-concepts/deduplication.md).

## De berekeningen van de tijdzone in de Dienst van de Vraag

De Service van de vraag normaliseert persisted gegevens in Adobe Experience Platform gebruikend het timestamp formaat UTC. Voor meer informatie over hoe te om uw tijdzonevereiste aan en van een timestamp te vertalen UTC, gelieve de [&#x200B; sectie van Veelgestelde vragen te zien over hoe te om de tijdzone aan en van een Tijdstempel van UTC &#x200B;](../troubleshooting-guide.md#How-do-I-change-the-time-zone-to-and-from-a-UTC-Timestamp?) te veranderen.

## Volgende stappen

Door dit document te lezen, bent u op een aantal belangrijke overwegingen geïntroduceerd wanneer het schrijven van vragen gebruikend [!DNL Query Service]. Voor meer informatie over hoe te om de SQL syntaxis te gebruiken om uw eigen vragen te schrijven, te lezen gelieve de [&#x200B; SQL syntaxisdocumentatie &#x200B;](../sql/syntax.md).

Voor meer steekproeven van vragen die binnen de Dienst van de Vraag kunnen worden gebruikt, gelieve de volgende documentatie van het gebruiksgeval te lezen:

- [Analyseinzichten](../use-cases/analytics-insights.md)
- [Een trended-rapport van gebeurtenissen maken](../use-cases/trended-report-of-events.md)
- [Een roll-uprapport van een bezoeker weergeven](../use-cases/roll-up-report-of-a-visitor.md)
- [De paginaweergaven van een gebruiker weergeven](../use-cases/list-visitor-sessions.md)
- [Bezoekers weergeven op basis van hun aantal paginaweergaven](../use-cases/visitors-by-number-of-page-views.md)
