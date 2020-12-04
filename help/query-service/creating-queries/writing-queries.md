---
keywords: Experience Platform;home;popular topics;query service;Query service;writing queries;writing query;
solution: Experience Platform
title: Bezig met schrijven van query's
topic: queries
type: Tutorial
description: Dit document bevat belangrijke details die u moet weten wanneer u query's schrijft in Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# Algemene richtlijnen voor het uitvoeren van query&#39;s in [!DNL Query Service]

Dit document bevat belangrijke informatie die u moet weten wanneer u query&#39;s schrijft in Adobe Experience Platform [!DNL Query Service].

Lees voor meer informatie over de SQL-syntaxis die wordt gebruikt in [!DNL Query Service]de [SQL-syntaxisdocumentatie](../sql/syntax.md).

## Uitvoeringsmodellen voor query

Adobe Experience Platform [!DNL Query Service] heeft twee modellen van vraaguitvoering: interactief en niet-interactief. De interactieve uitvoering wordt gebruikt voor vraagontwikkeling en rapportgeneratie in bedrijfsintelligentiehulpmiddelen, terwijl niet-interactief voor grotere banen en operationele vragen als deel van een werkschema van de gegevensverwerking wordt gebruikt.

### Interactieve queryuitvoering

De vragen kunnen interactief worden uitgevoerd door hen door [!DNL Query Service] UI of [door een verbonden cliënt](../clients/overview.md)voor te leggen. Wanneer het lopen [!DNL Query Service] door een verbonden cliënt, loopt een actieve zitting tussen de cliënt en [!DNL Query Service] tot of de voorgelegde vraagwinst of tijden uit.

De interactieve vraaguitvoering heeft de volgende beperkingen:

| Parameter | Beperking |
| --------- | ---------- |
| Time-out query | 10 minuten |
| Maximumaantal geretourneerde rijen | 50,000 |
| Maximum aantal gelijktijdige query&#39;s | 5 |

>[!NOTE]
>
>Als u de maximale rijbeperking wilt overschrijven, neemt u `LIMIT 0` de query op. De zoektime-out van 10 minuten is nog steeds van toepassing.

Standaard worden de resultaten van interactieve query&#39;s geretourneerd aan de client en worden deze **niet** voortgezet. Om de resultaten als dataset binnen te handhaven [!DNL Experience Platform], moet de vraag de `CREATE TABLE AS SELECT` syntaxis gebruiken.

### Niet-interactieve query-uitvoering

Vragen die via de [!DNL Query Service] API worden ingediend, worden niet-interactief uitgevoerd. De niet-interactieve uitvoering betekent dat de API vraag [!DNL Query Service] ontvangt en de vraag in de orde uitvoert het wordt ontvangen. De niet-interactieve vragen resulteren altijd in of de generatie van een nieuwe dataset binnen [!DNL Experience Platform] om de resultaten te ontvangen, of de toevoeging van nieuwe rijen in een bestaande dataset.

## Een specifiek veld binnen een object openen

Als u toegang wilt krijgen tot een veld binnen een object in de query, kunt u puntnotatie (`.`) of vierkante haakjes (`[]`) gebruiken. De volgende SQL-instructie gebruikt puntnotatie om het `endUserIds` object omlaag te doorlopen naar het `mcid` object.

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | De naam van de analystabel. |

De volgende SQL-instructie gebruikt haakjesnotatie om het `endUserIds` object omlaag te doorlopen naar het `mcid` object.

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

Het geretourneerde `endUserIds._experience.mcid` object bevat de overeenkomende waarden voor de volgende parameters:

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

## Wanneer gebruikt u enkele aanhalingstekens, dubbele aanhalingstekens en dubbele aanhalingstekens

Deze sectie verklaart wanneer om enige citaten, dubbele citaten, en achtercitaten in vragen te gebruiken.

### Enkele aanhalingstekens

Het enkele citaat (`'`) wordt gebruikt om tekstkoorden tot stand te brengen. U kunt deze bijvoorbeeld gebruiken in de `SELECT` instructie om een statische tekstwaarde te retourneren in het resultaat en in de `WHERE` component om de inhoud van een kolom te evalueren.

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
>Dubbele aanhalingstekens **kunnen niet** worden gebruikt met toegang tot puntnotatievelden.

### Achter aanhalingstekens

Het achteraanhalingsteken `` ` `` wordt gebruikt om gereserveerde kolomnamen **alleen** te omzeilen bij gebruik van puntnotatiesyntaxis. Omdat SQL bijvoorbeeld een gereserveerd woord `order` is, moet u backquotes gebruiken om toegang te krijgen tot het veld `commerce.order`:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

Achteraanhalingstekens worden ook gebruikt om toegang te krijgen tot een veld dat met een getal begint. Als u bijvoorbeeld toegang wilt krijgen tot het veld, moet u de notatie voor aanhalingstekens gebruiken. `30_day_value`

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

Achteraanhalingstekens zijn **niet** nodig als u haakje notatie gebruikt.

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 LIMIT 10
```

## Volgende stappen

Door dit document te lezen, bent u aan sommige belangrijke overwegingen toegevoegd wanneer het schrijven van vragen gebruikend [!DNL Query Service]. Voor meer informatie over hoe te om de SQL syntaxis te gebruiken om uw eigen vragen te schrijven, gelieve de [SQL syntaxisdocumentatie](../sql/syntax.md)te lezen.