---
keywords: Experience Platform;home;populaire onderwerpen;query-service;Query-service;adobe defined functies;sql;
solution: Experience Platform
title: Adobe-Gedefinieerde SQL Functies in de Dienst van de Vraag
topic-legacy: functions
description: Dit document bevat informatie over door Adobe gedefinieerde functies die beschikbaar zijn in Adobe Experience Platform Query Service.
exl-id: 275aa14e-f555-4365-bcd6-0dd6df2456b3
source-git-commit: e0cdfc514a9e1277134d4c0d5396fc0bdf9d9958
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 2%

---

# Adobe bepaalde SQL functies in de Dienst van de Vraag

Adobe-bepaalde functies, hier genoemd ADFs, zijn prebuilt functies in de Dienst van de Vraag van Adobe Experience Platform die helpen gemeenschappelijke zaken-gerelateerde taken op uitvoeren [!DNL Experience Event] gegevens. Hieronder vallen functies voor [Sessionering](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html) en [Attributie](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html) zoals in Adobe Analytics.

Dit document bevat informatie over door Adobe gedefinieerde functies die beschikbaar zijn in [!DNL Query Service].

## Vensterfuncties {#window-functions}

De meerderheid van de bedrijfslogica vereist het verzamelen van de aanraakpunten voor een klant en het opdracht geven tot hen tegen tijd. Deze steun wordt verleend door [!DNL Spark] SQL in de vorm van vensterfuncties. Vensterfuncties maken deel uit van standaard-SQL en worden ondersteund door vele andere SQL-engines.

Een vensterfunctie werkt een samenvoeging bij en retourneert één item voor elke rij in de geordende subset. De eenvoudigste aggregatiefunctie is `SUM()`. `SUM()` neemt uw rijen en geeft u één totaal. Als u in plaats daarvan `SUM()` aan een venster, dat het in een vensterfunctie verandert, ontvangt u een cumulatief bedrag met elke rij.

De meerderheid van de [!DNL Spark] SQL helpers zijn vensterfuncties die elke rij in uw venster bijwerken, met de staat van die rij toegevoegde.

**Zoeksyntaxis**

```sql
OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschrijving | Voorbeeld |
| --------- | ----------- | ------- |
| `{PARTITION}` | Een subgroep van rijen op basis van een kolom of een beschikbaar veld. | `PARTITION BY endUserIds._experience.mcid.id` |
| `{ORDER}` | Een kolom of beschikbaar veld dat wordt gebruikt om de subset of rijen te bestellen. | `ORDER BY timestamp` |
| `{FRAME}` | Een subgroep van de rijen in een verdeling. | `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## Sessionering

Wanneer u met werkt [!DNL Experience Event] gegevens die afkomstig zijn van een website, mobiele toepassing, interactief spraakreactiesysteem of een ander kanaal voor klantinteractie, helpen bij het groeperen van gebeurtenissen rond een verwante periode van activiteit. Doorgaans hebt u een specifieke intentie om uw activiteiten te sturen, zoals het zoeken naar een product, het betalen van een rekening, het controleren van de balans, het invullen van een toepassing, enzovoort.

Deze groepering, of zitting van gegevens, helpt de gebeurtenissen associëren om meer context over de klantenervaring te ontdekken.

Zie de documentatie over [contextbewuste sessies](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html).

**Zoeksyntaxis**

```sql
SESS_TIMEOUT({TIMESTAMP}, {EXPIRATION_IN_SECONDS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{TIMESTAMP}` | Het tijdstempelveld in de gegevensset. |
| `{EXPIRATION_IN_SECONDS}` | Het aantal seconden dat nodig is tussen gebeurtenissen om het einde van de huidige sessie en het begin van een nieuwe sessie te kwalificeren. |

Een uitleg van de parameters binnen de `OVER()` kan worden gevonden in de [sectie vensterfuncties](#window-functions).

**Voorbeeldquery**

```sql
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp,
  SESS_TIMEOUT(timestamp, 60 * 30)
    OVER (PARTITION BY endUserIds._experience.mcid.id
        ORDER BY timestamp
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
    AS session
FROM experience_events
ORDER BY id, timestamp ASC
LIMIT 10
```

**Resultaten**

```console
                id                |       timestamp       |      session       
----------------------------------+-----------------------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | (40,1,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | (55,1,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | (1361821,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | (54,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | (49,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | (33,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | (31,2,false,5)
(10 rows)
```

Voor de voorbeeldquery die wordt gegeven, worden de resultaten gegeven in het dialoogvenster `session` kolom. De `session` de kolom bestaat uit de volgende onderdelen:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parameters | Beschrijving |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Het verschil in tijd, in seconden, tussen de huidige record en de vorige record. |
| `{NUM}` | Een uniek sessienummer, dat begint bij 1, voor de sleutel die is gedefinieerd in het dialoogvenster `PARTITION BY` van de vensterfunctie. |
| `{IS_NEW}` | Een Booleaanse waarde die wordt gebruikt om te bepalen of een record de eerste van een sessie is. |
| `{DEPTH}` | De diepte van de huidige record in de sessie. |

### SESS_START_IF

Deze query retourneert de status van de sessie voor de huidige rij, gebaseerd op de huidige tijdstempel en de opgegeven expressie, en start een nieuwe sessie met de huidige rij.

**Zoeksyntaxis**

```sql
SESS_START_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{TIMESTAMP}` | Het tijdstempelveld in de gegevensset. |
| `{TEST_EXPRESSION}` | Een expressie waarmee u de velden van de gegevens wilt controleren. Bijvoorbeeld, `application.launches > 0`. |

Een uitleg van de parameters binnen de `OVER()` kan worden gevonden in de [sectie vensterfuncties](#window-functions).

**Voorbeeldquery**

```sql
SELECT
    endUserIds._experience.mcid.id AS id,
    timestamp,
    IF(application.launches.value > 0, true, false) AS isLaunch,
    SESS_START_IF(timestamp, application.launches.value > 0)
        OVER (PARTITION BY endUserIds._experience.mcid.id
            ORDER BY timestamp
            ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
        AS session
    FROM experience_events
    ORDER BY id, timestamp ASC
    LIMIT 10
```

**Resultaten**

```console
                id                |       timestamp       | isLaunch |      session       
----------------------------------+-----------------------+----------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | true     | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | false    | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | false    | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | true     | (40,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | false    | (55,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | false    | (1361821,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | false    | (54,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | false    | (49,2,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | false    | (33,2,false,6)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | false    | (31,2,false,7)
(10 rows)
```

Voor de voorbeeldquery die wordt gegeven, worden de resultaten gegeven in het dialoogvenster `session` kolom. De `session` de kolom bestaat uit de volgende onderdelen:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parameters | Beschrijving |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Het verschil in tijd, in seconden, tussen de huidige record en de vorige record. |
| `{NUM}` | Een uniek sessienummer, dat begint bij 1, voor de sleutel die is gedefinieerd in het dialoogvenster `PARTITION BY` van de vensterfunctie. |
| `{IS_NEW}` | Een Booleaanse waarde die wordt gebruikt om te bepalen of een record de eerste van een sessie is. |
| `{DEPTH}` | De diepte van de huidige record in de sessie. |

### SESS_END_IF

Deze query retourneert de status van de sessie voor de huidige rij, gebaseerd op de huidige tijdstempel en de opgegeven expressie, beëindigt de huidige sessie en start een nieuwe sessie op de volgende rij.

**Zoeksyntaxis**

```sql
SESS_END_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{TIMESTAMP}` | Het tijdstempelveld in de gegevensset. |
| `{TEST_EXPRESSION}` | Een expressie waarmee u de velden van de gegevens wilt controleren. Bijvoorbeeld, `application.launches > 0`. |

Een uitleg van de parameters binnen de `OVER()` kan worden gevonden in de [sectie vensterfuncties](#window-functions).

**Voorbeeldquery**

```sql
SELECT
    endUserIds._experience.mcid.id AS id,
    timestamp,
    IF(application.applicationCloses.value > 0 OR application.crashes.value > 0, true, false) AS isExit,
    SESS_END_IF(timestamp, application.applicationCloses.value > 0 OR application.crashes.value > 0)
        OVER (PARTITION BY endUserIds._experience.mcid.id
            ORDER BY timestamp
            ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
        AS session
    FROM experience_events
    ORDER BY id, timestamp ASC
    LIMIT 10
```

**Resultaten**

```console
                id                |       timestamp       | isExit   |      session       
----------------------------------+-----------------------+----------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | false    | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | false    | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | true     | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | false    | (40,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | false    | (55,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | false    | (1361821,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | false    | (54,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | false    | (49,2,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | false    | (33,2,false,6)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | false    | (31,2,false,7)
(10 rows)
```

Voor de voorbeeldquery die wordt gegeven, worden de resultaten gegeven in het dialoogvenster `session` kolom. De `session` de kolom bestaat uit de volgende onderdelen:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parameters | Beschrijving |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Het verschil in tijd, in seconden, tussen de huidige record en de vorige record. |
| `{NUM}` | Een uniek sessienummer, dat begint bij 1, voor de sleutel die is gedefinieerd in het dialoogvenster `PARTITION BY` van de vensterfunctie. |
| `{IS_NEW}` | Een Booleaanse waarde die wordt gebruikt om te bepalen of een record de eerste van een sessie is. |
| `{DEPTH}` | De diepte van de huidige record in de sessie. |


## Padcontrole

Pathing kan worden gebruikt om inzicht te krijgen in de diepte van de service van de klant, om te bevestigen dat de bedoelde stappen van een ervaring werken zoals deze zijn ontworpen, en om mogelijke pijnpunten te identificeren die gevolgen hebben voor de klant.

De volgende ADFs steunt het vestigen van het kleven meningen van hun vorige en volgende verhoudingen. U kunt vorige en volgende pagina&#39;s maken of meerdere gebeurtenissen doorlopen om te tekenen.

### Vorige pagina

Hiermee bepaalt u de vorige waarde van een bepaald veld met een opgegeven aantal stappen buiten het venster. Let in het voorbeeld op het volgende: `WINDOW` functie is geconfigureerd met een frame van `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` het plaatsen ADF om de huidige rij en alle verdere rijen te bekijken.

**Zoeksyntaxis**

```sql
PREVIOUS({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{KEY}` | De kolom of het veld van de gebeurtenis. |
| `{SHIFT}` | (Optioneel) Het aantal gebeurtenissen dat zich niet bij de huidige gebeurtenis bevindt. De standaardwaarde is 1. |
| `{IGNORE_NULLS}` | (Optioneel) Een Booleaanse waarde die aangeeft of deze null is `{KEY}` waarden moeten worden genegeerd. De standaardwaarde is `false`. |

Een uitleg van de parameters binnen de `OVER()` kan worden gevonden in de [sectie vensterfuncties](#window-functions).

**Voorbeeldquery**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, web.webPageDetails.name
    PREVIOUS(web.webPageDetails.name, 3)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Resultaten**

```console
                id                 |       timestamp       |                 name                |                    previous_page                    
-----------------------------------+-----------------------+-------------------------------------+-----------------------------------------------------
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:15:28.0 |                                     | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:05.0 | Home                                | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:45.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 19:22:34.0 |                                     | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:12.0 | Home                                | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:57.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:03:36.0 | Search Results                      | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:04:30.0 | Product Details: Pemmican Power Bar | (Search Results)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:05:27.0 | Shopping Cart: Cart Details         | (Product Details: Pemmican Power Bar)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:06:07.0 | Shopping Cart: Shipping Information | (Shopping Cart: Cart Details)
(10 rows)
```

Voor de voorbeeldquery die wordt gegeven, worden de resultaten gegeven in het dialoogvenster `previous_page` kolom. De waarde binnen de `previous_page` de kolom is gebaseerd op de `{KEY}` gebruikt in de ADF.

### Volgende pagina

Hiermee bepaalt u de volgende waarde van een bepaald veld met een opgegeven aantal stappen buiten het venster. Let in het voorbeeld op het volgende: `WINDOW` functie is geconfigureerd met een frame van `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` het plaatsen ADF om de huidige rij en alle verdere rijen te bekijken.

**Zoeksyntaxis**

```sql
NEXT({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{KEY}` | De kolom of het veld van de gebeurtenis. |
| `{SHIFT}` | (Optioneel) Het aantal gebeurtenissen dat zich niet bij de huidige gebeurtenis bevindt. De standaardwaarde is 1. |
| `{IGNORE_NULLS}` | (Optioneel) Een Booleaanse waarde die aangeeft of deze null is `{KEY}` waarden moeten worden genegeerd. De standaardwaarde is `false`. |

Een uitleg van de parameters binnen de `OVER()` kan worden gevonden in de [sectie vensterfuncties](#window-functions).

**Voorbeeldquery**

```sql
SELECT endUserIds._experience.aaid.id, timestamp, web.webPageDetails.name,
    NEXT(web.webPageDetails.name, 1, true)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
      AS next_page
FROM experience_events
ORDER BY endUserIds._experience.aaid.id, timestamp ASC
LIMIT 10
```

**Resultaten**

```console
                id                 |       timestamp       |                name                 |             previous_page             
-----------------------------------+-----------------------+-------------------------------------+---------------------------------------
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:15:28.0 |                                     | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:05.0 | Home                                | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:45.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 19:22:34.0 |                                     | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:12.0 | Home                                | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:57.0 | Kids                                | (Search Results)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:03:36.0 | Search Results                      | (Product Details: Pemmican Power Bar)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:04:30.0 | Product Details: Pemmican Power Bar | (Shopping Cart: Cart Details)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:05:27.0 | Shopping Cart: Cart Details         | (Shopping Cart: Shipping Information)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:06:07.0 | Shopping Cart: Shipping Information | (Shopping Cart: Billing Information)
(10 rows)
```

Voor de voorbeeldquery die wordt gegeven, worden de resultaten gegeven in het dialoogvenster `previous_page` kolom. De waarde binnen de `previous_page` de kolom is gebaseerd op de `{KEY}` gebruikt in de ADF.

## Tijd-tussen

De tijd-tussen staat u toe om latent klantengedrag binnen een bepaalde tijdspanne vóór of na een gebeurtenis te onderzoeken voorkomt.

### Tijd tussen vorige overeenkomst

Deze vraag keert een aantal terug dat de eenheid van tijd vertegenwoordigt aangezien de vorige passende gebeurtenis werd gezien. Als er geen overeenkomende gebeurtenis is gevonden, wordt null geretourneerd.

**Zoeksyntaxis**

```sql
TIME_BETWEEN_PREVIOUS_MATCH(
    {TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT})
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{TIMESTAMP}` | Een tijdstempelveld dat wordt gevonden in de gegevensset die wordt gevuld op alle gebeurtenissen. |
| `{EVENT_DEFINITION}` | De expressie die de vorige gebeurtenis moet kwalificeren. |
| `{TIME_UNIT}` | De eenheid van output. Mogelijke waarden zijn dagen, uren, minuten en seconden. De standaardwaarde is seconden. |

Een uitleg van de parameters binnen de `OVER()` kan worden gevonden in de [sectie vensterfuncties](#window-functions).

**Voorbeeldquery**

```sql
SELECT 
  page_name,
  SUM (time_between_previous_match) / COUNT(page_name) as average_minutes_since_registration
FROM
(
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp, web.webPageDetails.name as page_name, 
  TIME_BETWEEN_PREVIOUS_MATCH(timestamp, web.webPageDetails.name='Account Registration|Confirmation', 'minutes')
    OVER(PARTITION BY endUserIds._experience.mcid.id
       ORDER BY timestamp
       ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
    AS time_between_previous_match
FROM experience_events
)
WHERE time_between_previous_match IS NOT NULL
GROUP BY page_name
ORDER BY average_minutes_since_registration
LIMIT 10
```

**Resultaten**

```console
             page_name             | average_minutes_since_registration 
-----------------------------------+------------------------------------
                                   |                                   
 Account Registration|Confirmation |                                0.0
 Seasonal                          |                   5.47029702970297
 Equipment                         |                  6.532110091743119
 Women                             |                  7.287081339712919
 Men                               |                  7.640918580375783
 Product List                      |                  9.387459807073954
 Unlimited Blog|February           |                  9.954545454545455
 Product Details|Buffalo           |                 13.304347826086957
 Unlimited Blog|June               |                  770.4285714285714
(10 rows)
```

Voor de voorbeeldquery die wordt gegeven, worden de resultaten gegeven in het dialoogvenster `average_minutes_since_registration` kolom. De waarde binnen de `average_minutes_since_registration` kolom is het tijdsverschil tussen de huidige en vorige gebeurtenissen. De tijdseenheid is eerder gedefinieerd in de `{TIME_UNIT}`.

### Tijd tussen volgende overeenkomst

Deze query retourneert een negatief getal dat de tijdseenheid achter de volgende overeenkomende gebeurtenis vertegenwoordigt. Als er geen overeenkomende gebeurtenis wordt gevonden, wordt null geretourneerd.

**Zoeksyntaxis**

```sql
TIME_BETWEEN_NEXT_MATCH({TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{TIMESTAMP}` | Een tijdstempelveld dat wordt gevonden in de gegevensset die wordt gevuld op alle gebeurtenissen. |
| `{EVENT_DEFINITION}` | De expressie waarmee de volgende gebeurtenis wordt gekwalificeerd. |
| `{TIME_UNIT}` | (Optioneel) De uitvoereenheid. Mogelijke waarden zijn dagen, uren, minuten en seconden. De standaardwaarde is seconden. |

Een uitleg van de parameters binnen de `OVER()` kan worden gevonden in de [sectie vensterfuncties](#window-functions).

**Voorbeeldquery**

```sql
SELECT 
  page_name,
  SUM (time_between_next_match) / COUNT(page_name) as average_minutes_until_order_confirmation
FROM
(
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp, web.webPageDetails.name as page_name, 
  TIME_BETWEEN_NEXT_MATCH(timestamp, web.webPageDetails.name='Shopping Cart|Order Confirmation', 'minutes')
    OVER(PARTITION BY endUserIds._experience.mcid.id
       ORDER BY timestamp
       ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
    AS time_between_next_match
FROM experience_events
)
WHERE time_between_next_match IS NOT NULL
GROUP BY page_name
ORDER BY average_minutes_until_order_confirmation DESC
LIMIT 10
```

**Resultaten**

```console
             page_name             | average_minutes_until_order_confirmation 
-----------------------------------+------------------------------------------
 Shopping Cart|Order Confirmation  |                                      0.0
 Men                               |                       -9.465295629820051
 Equipment                         |                       -9.682098765432098
 Product List                      |                       -9.690661478599221
 Women                             |                       -9.759459459459459
 Seasonal                          |                                  -10.295
 Shopping Cart|Order Review        |                      -366.33567364956144
 Unlimited Blog|February           |                       -615.0327868852459
 Shopping Cart|Billing Information |                       -775.6200495367711
 Product Details|Buffalo           |                      -1274.9571428571428
(10 rows)
```

Voor de voorbeeldquery die wordt gegeven, worden de resultaten gegeven in het dialoogvenster `average_minutes_until_order_confirmation` kolom. De waarde binnen de `average_minutes_until_order_confirmation` kolom is het tijdsverschil tussen de huidige en volgende gebeurtenissen. De tijdseenheid is eerder gedefinieerd in de `{TIME_UNIT}`.

## Volgende stappen

Met de hier beschreven functies kunt u query&#39;s schrijven voor toegang tot uw eigen functies [!DNL Experience Event] gegevenssets met [!DNL Query Service]. Voor meer informatie over het schrijven van vragen in [!DNL Query Service], zie de documentatie op [query&#39;s maken](../best-practices/writing-queries.md).

## Aanvullende bronnen

In de volgende video ziet u hoe u query&#39;s uitvoert in de Adobe Experience Platform-interface en in een PSQL-client. Bovendien gebruikt de video ook voorbeelden met afzonderlijke eigenschappen in een XDM-object, met gebruik van door Adobe gedefinieerde functies en met gebruik van CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)
