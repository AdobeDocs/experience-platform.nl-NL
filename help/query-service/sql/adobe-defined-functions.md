---
keywords: Experience Platform;home;popular topics;query service;Query service;adobe defined functions;sql;
solution: Experience Platform
title: Adobe-gedefinieerde functies
topic: functions
description: Dit document verstrekt informatie voor Adobe-bepaalde functies beschikbaar in de Dienst van de Vraag.
translation-type: tm+mt
source-git-commit: c95f976efd4a281640d2f47888b34bdd12a6c7a8
workflow-type: tm+mt
source-wordcount: '2889'
ht-degree: 1%

---


# Adobe-gedefinieerde functies

Adobe-bepaalde functies, hier genoemd ADFs, zijn prebuilt functies in de Dienst van de Vraag van Adobe Experience Platform die helpen gemeenschappelijke zaken-gerelateerde taken op [!DNL Experience Event] gegevens uitvoeren. Dit zijn onder andere functies voor [Sessionisatie](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html) en [Attributie](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html), zoals die in Adobe Analytics.

Dit document bevat informatie over door Adobe gedefinieerde functies die beschikbaar zijn in [!DNL Query Service].

## Vensterfuncties {#window-functions}

De meerderheid van de bedrijfslogica vereist het verzamelen van de aanraakpunten voor een klant en het opdracht geven tot hen tegen tijd. Deze ondersteuning wordt geleverd door SQL in de vorm van vensterfuncties. [!DNL Spark] Vensterfuncties maken deel uit van standaard-SQL en worden ondersteund door vele andere SQL-engines.

Een vensterfunctie werkt een samenvoeging bij en retourneert één item voor elke rij in de geordende subset. De eenvoudigste aggregatiefunctie is `SUM()`. `SUM()` neemt uw rijen en geeft u één totaal. Als u in plaats daarvan `SUM()` op een venster toepast en het in een vensterfunctie omzet, ontvangt u een cumulatief bedrag met elke rij.

De meeste [!DNL Spark] SQL helpers zijn vensterfuncties die elke rij in uw venster bijwerken, met de staat van die toegevoegde rij.

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

Wanneer u werkt met [!DNL Experience Event]-gegevens die afkomstig zijn van een website, mobiele toepassing, interactief spraakantwoordsysteem of een ander kanaal voor klantinteractie, is het nuttig als gebeurtenissen kunnen worden gegroepeerd rond een verwante periode. Doorgaans hebt u een specifieke intentie om uw activiteiten te sturen, zoals het zoeken naar een product, het betalen van een rekening, het controleren van de balans, het invullen van een toepassing, enzovoort.

Deze groepering, of zitting van gegevens, helpt de gebeurtenissen associëren om meer context over de klantenervaring te ontdekken.

Raadpleeg de documentatie over [contextbewuste sessies](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html) voor meer informatie over sessionisatie in Adobe Analytics.

**Zoeksyntaxis**

```sql
SESS_TIMEOUT({TIMESTAMP}, {EXPIRATION_IN_SECONDS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{TIMESTAMP}` | Het tijdstempelveld in de gegevensset. |
| `{EXPIRATION_IN_SECONDS}` | Het aantal seconden dat nodig is tussen gebeurtenissen om het einde van de huidige sessie en het begin van een nieuwe sessie te kwalificeren. |

Een uitleg van de parameters binnen de functie `OVER()` vindt u in de sectie [vensterfuncties](#window-functions).

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

Voor de gegeven steekproefvraag, worden de resultaten gegeven in `session` kolom. De kolom `session` bestaat uit de volgende componenten:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parameters | Beschrijving |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Het verschil in tijd, in seconden, tussen de huidige record en de vorige record. |
| `{NUM}` | Een uniek sessienummer, te beginnen bij 1, voor de sleutel die is gedefinieerd in de `PARTITION BY` van de vensterfunctie. |
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

Een uitleg van de parameters binnen de functie `OVER()` vindt u in de sectie [vensterfuncties](#window-functions).

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

Voor de gegeven steekproefvraag, worden de resultaten gegeven in `session` kolom. De kolom `session` bestaat uit de volgende componenten:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parameters | Beschrijving |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Het verschil in tijd, in seconden, tussen de huidige record en de vorige record. |
| `{NUM}` | Een uniek sessienummer, te beginnen bij 1, voor de sleutel die is gedefinieerd in de `PARTITION BY` van de vensterfunctie. |
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

Een uitleg van de parameters binnen de functie `OVER()` vindt u in de sectie [vensterfuncties](#window-functions).

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

Voor de gegeven steekproefvraag, worden de resultaten gegeven in `session` kolom. De kolom `session` bestaat uit de volgende componenten:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parameters | Beschrijving |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Het verschil in tijd, in seconden, tussen de huidige record en de vorige record. |
| `{NUM}` | Een uniek sessienummer, te beginnen bij 1, voor de sleutel die is gedefinieerd in de `PARTITION BY` van de vensterfunctie. |
| `{IS_NEW}` | Een Booleaanse waarde die wordt gebruikt om te bepalen of een record de eerste van een sessie is. |
| `{DEPTH}` | De diepte van de huidige record in de sessie. |

## Attributie

Het koppelen van klantenacties aan succes is een belangrijk deel van het begrip van de factoren die klantenervaringen beïnvloeden. De volgende ADF&#39;s ondersteunen first-touch-kenmerk en last-touch-kenmerk met verschillende vervalinstellingen.

Zie [Attribution IQ overview](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution.html) in de handleiding van het [!DNL Analytics] deelvenster Kenmerken voor meer informatie over attributie in Adobe Analytics.

### Kenmerk eerste aanraking

Deze vraag keert de eerste-aanraak attributiewaarde en details voor één enkel kanaal in de doel [!DNL Experience Event] dataset terug. De query retourneert een `struct`-object met de eerste aanraakwaarde, tijdstempel en attributie voor elke rij die voor het geselecteerde kanaal wordt geretourneerd.

Deze vraag is nuttig als u wilt zien welke interactie tot een reeks klantenacties leidde. In het onderstaande voorbeeld wordt de initiële volgcode (`em:946426`) in de [!DNL Experience Event] gegevens toegewezen aan 100% (`1.0`) verantwoordelijkheid voor de acties van de klant, aangezien dit de eerste interactie was.

**Zoeksyntaxis**

```sql
ATTRIBUTION_FIRST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{TIMESTAMP}` | Het tijdstempelveld in de gegevensset. |
| `{CHANNEL_NAME}` | Het label voor het geretourneerde object. |
| `{CHANNEL_VALUE}` | De kolom of het gebied dat het doelkanaal voor de vraag is. |

Een verklaring van de parameters binnen `OVER()` kan in [vensterfuncties sectie](#window-functions) worden gevonden.

**Voorbeeldquery**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH(timestamp, 'Paid First', marketing.trackingCode)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
LIMIT 10
```

**Resultaten**

```console
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:06:12.0 | em:946426    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:07:02.0 | em:946426    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:07:55.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:08:44.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:50:10.0 | em:513526    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:50:43.0 | em:513526    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:53:02.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-26 20:37:12.0 | sms:70175    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-26 20:37:57.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2019-01-02 19:41:38.0 | em:526702    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
(10 rows)
```

Voor de gegeven steekproefvraag, worden de resultaten gegeven in `first_touch` kolom. De kolom `first_touch` bestaat uit de volgende componenten:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{NAME}` | De `{CHANNEL_NAME}`, die als label in ADF is ingevoerd. |
| `{VALUE}` | De waarde van `{CHANNEL_VALUE}` die de eerste aanraking in [!DNL Experience Event] is |
| `{TIMESTAMP}` | Het tijdstempel van de [!DNL Experience Event] waar de eerste aanraking plaatsvond. |
| `{FRACTION}` | De attributie van de eerste aanraking, uitgedrukt als decimale breuk. |

### Last-touch-kenmerk

Deze query retourneert de laatste aanraakwaarde en details voor één kanaal in de gegevensset [!DNL Experience Event] van het doel. De query retourneert een `struct`-object met de laatste aanraakwaarde, tijdstempel en attributie voor elke rij die voor het geselecteerde kanaal wordt geretourneerd.

Deze vraag is nuttig als u de definitieve interactie in een reeks klantenacties wilt zien. In het onderstaande voorbeeld is de trackingcode in het geretourneerde object de laatste interactie in elke [!DNL Experience Event]-record. Elke code krijgt 100% (`1.0`) verantwoordelijkheid voor de acties van de klant, aangezien dit de laatste interactie was.

**Zoeksyntaxis**

```sql
ATTRIBUTION_LAST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{TIMESTAMP}` | Het tijdstempelveld in de gegevensset. |
| `{CHANNEL_NAME}` | Het label van het geretourneerde object. |
| `{CHANNEL_VALUE}` | De kolom of het gebied dat het doelkanaal voor de vraag is. |

Een verklaring van de parameters binnen `OVER()` kan in [vensterfuncties sectie](#window-functions) worden gevonden.

**Voorbeeldquery**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH(timestamp, 'trackingCode', marketing.trackingCode)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Resultaten**

```console
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:06:12.0 | em:946426    | (Paid Last,em:946426,2017-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:07:02.0 | em:946426    | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:07:55.0 |              | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:08:44.0 |              | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:50:10.0 | em:513526    | (Paid Last,em:513526,2017-12-23 17:50:10.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:50:43.0 | em:513526    | (Paid Last,em:513526,2017-12-23 17:50:43.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:53:02.0 |              | (Paid Last,em:513526,2017-12-23 17:50:43.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-26 20:37:12.0 | sms:70175    | (Paid Last,sms:70175,2017-12-26 20:37:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-26 20:37:57.0 |              | (Paid Last,sms:70175,2017-12-26 20:37:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-01-02 19:41:38.0 | em:526702    | (Paid Last,em:526702,2018-01-02 19:41:38.0,1.0)
(10 rows)
```

Voor de gegeven steekproefvraag, worden de resultaten gegeven in `last_touch` kolom. De kolom `last_touch` bestaat uit de volgende componenten:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parameters | Beschrijving |
| ---------- | ----------- |
| `{NAME}` | De `{CHANNEL_NAME}`, die als label in ADF is ingevoerd. |
| `{VALUE}` | De waarde van `{CHANNEL_VALUE}` die de laatste aanraking in [!DNL Experience Event] is |
| `{TIMESTAMP}` | Het tijdstempel van de [!DNL Experience Event] waar `channelValue` werd gebruikt. |
| `{FRACTION}` | De attributie van de laatste aanraking, uitgedrukt als decimale breuk. |

### First-touch-kenmerk met vervalvoorwaarde

Deze vraag keert de eerste-aanraak attributiewaarde en details voor één enkel kanaal in de doel [!DNL Experience Event] dataset terug, die na of vóór een voorwaarde vervalt. De query retourneert een `struct`-object met de eerste aanraakwaarde, tijdstempel en attributie voor elke rij die voor het geselecteerde kanaal wordt geretourneerd.

Deze vraag is nuttig als u wilt zien welke interactie tot een reeks klantenacties binnen een gedeelte van [!DNL Experience Event] dataset leidde die door een voorwaarde van uw keuze wordt bepaald. In het onderstaande voorbeeld wordt een aankoop geregistreerd (`commerce.purchases.value IS NOT NULL`) op elk van de vier dagen die in de resultaten worden weergegeven (15 juli, 21 juli, 23 en 29) en wordt de initiële volgcode op elke dag toegewezen aan 100% (`1.0`) verantwoordelijkheid voor de acties van de klant.

**Zoeksyntaxis**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{TIMESTAMP}` | Het tijdstempelveld in de gegevensset. |
| `{CHANNEL_NAME}` | Het label voor het geretourneerde object. |
| `{CHANNEL_VALUE}` | De kolom of het gebied dat het doelkanaal voor de vraag is. |
| `{EXP_CONDITION}` | De voorwaarde die het verlooppunt van het kanaal bepaalt. |
| `{EXP_BEFORE}` | Een Booleaanse waarde die aangeeft of het kanaal vervalt vóór of na de opgegeven voorwaarde `{EXP_CONDITION}`. Deze optie is vooral ingeschakeld voor de vervalvoorwaarden van een sessie, zodat de eerste aanraking niet wordt geselecteerd uit een vorige sessie. Deze waarde wordt standaard ingesteld op `false`. |

Een uitleg van de parameters binnen de functie `OVER()` vindt u in de sectie [vensterfuncties](#window-functions).

**Voorbeeldquery**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH_EXP_IF(timestamp, 'Paid First', marketing.trackingCode, commerce.purchases.value IS NOT NULL, false)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Resultaten**

```console
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:05.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid First,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

Voor de gegeven steekproefvraag, worden de resultaten gegeven in `first_touch` kolom. De kolom `first_touch` bestaat uit de volgende componenten:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parameters | Beschrijving |
| ---------- | ----------- |
| `{NAME}` | De `{CHANNEL_NAME}`, die als label in ADF is ingevoerd. |
| `{VALUE}` | De waarde van `CHANNEL_VALUE}` die de eerste aanraking in [!DNL Experience Event], voorafgaand aan `{EXP_CONDITION}` is. |
| `{TIMESTAMP}` | Het tijdstempel van de [!DNL Experience Event] waar de eerste aanraking plaatsvond. |
| `{FRACTION}` | De attributie van de eerste aanraking, uitgedrukt als decimale breuk. |

### First-touch-kenmerk met time-out bij verlopen

Deze vraag keert de eerste-aanraak attributiewaarde en details voor één enkel kanaal in de doel [!DNL Experience Event] dataset voor een gespecificeerde tijdspanne terug. De query retourneert een `struct`-object met de eerste aanraakwaarde, tijdstempel en attributie voor elke rij die voor het geselecteerde kanaal wordt geretourneerd.

Deze vraag is nuttig als u wilt zien welke interactie, binnen een geselecteerd tijdinterval, tot een klantenactie leidde. In het onderstaande voorbeeld is de eerste aanraking die voor elke actie van de klant wordt geretourneerd, de vroegste interactie binnen de voorafgaande zeven dagen (`expTimeout = 86400 * 7`).

**Specificatie**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{TIMESTAMP}` | Het tijdstempelveld in de gegevensset. |
| `{CHANNEL_NAME}` | Het label voor het geretourneerde object. |
| `{CHANNEL_VALUE}` | De kolom of het gebied dat het doelkanaal voor de vraag is. |
| `{EXP_TIMEOUT}` | Het tijdvenster voorafgaand aan de kanaalgebeurtenis, in seconden, waarin de query zoekt naar een eerste aanraakgebeurtenis. |

Een uitleg van de parameters binnen de functie `OVER()` vindt u in de sectie [vensterfuncties](#window-functions).

**Voorbeeldquery**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(timestamp, 'Paid First', marketing.trackingCode, 86400 * 7)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Resultaten**

```console
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:05.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid First,em:483339,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid First,em:483339,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid First,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

Voor de gegeven steekproefvraag, worden de resultaten gegeven in `first_touch` kolom. De kolom `first_touch` bestaat uit de volgende componenten:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parameters | Beschrijving |
| ---------- | ----------- |
| `{NAME}` | De `{CHANNEL_NAME}`, die als label in ADF is ingevoerd. |
| `{VALUE}` | De waarde van `CHANNEL_VALUE}` die de eerste aanraking binnen het gespecificeerde `{EXP_TIMEOUT}` interval is. |
| `{TIMESTAMP}` | Het tijdstempel van de [!DNL Experience Event] waar de eerste aanraking plaatsvond. |
| `{FRACTION}` | De attributie van de eerste aanraking, uitgedrukt als decimale breuk. |

### Last-touch kenmerk met vervaldatum

Deze query retourneert de laatste aanraakwaarde en details voor één kanaal in de gegevensset [!DNL Experience Event] van het doel, die na of vóór een voorwaarde vervalt. De query retourneert een `struct`-object met de laatste aanraakwaarde, tijdstempel en attributie voor elke rij die voor het geselecteerde kanaal wordt geretourneerd.

Deze vraag is nuttig als u de laatste interactie in een reeks klantenacties binnen een gedeelte van [!DNL Experience Event] dataset wilt zien die door een voorwaarde van uw kiezen wordt bepaald. In het onderstaande voorbeeld wordt een aankoop geregistreerd (`commerce.purchases.value IS NOT NULL`) op elk van de vier dagen die in de resultaten worden weergegeven (15 juli, 21 juli, 23 en 29) en wordt de laatste trackingcode op elke dag toegewezen aan 100% (`1.0`) verantwoordelijkheid voor de acties van de klant.

**Zoeksyntaxis**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{TIMESTAMP}` | Het tijdstempelveld in de gegevensset. |
| `{CHANNEL_NAME}` | Het label voor het geretourneerde object. |
| `{CHANNEL_VALUE}` | De kolom of het gebied dat het doelkanaal voor de vraag is. |
| `{EXP_CONDITION}` | De voorwaarde die het verlooppunt van het kanaal bepaalt. |
| `{EXP_BEFORE}` | Een Booleaanse waarde die aangeeft of het kanaal vervalt vóór of na de opgegeven voorwaarde `{EXP_CONDITION}`. Deze optie is vooral ingeschakeld voor de vervalvoorwaarden van een sessie, zodat de eerste aanraking niet wordt geselecteerd uit een vorige sessie. Deze waarde wordt standaard ingesteld op `false`. |

**Voorbeeldquery**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH_EXP_IF(timestamp, 'trackingCode', marketing.trackingCode, commerce.purchases.value IS NOT NULL, false)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Voorbeelden van resultaten**

```console
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 | em:1024841   | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 | em:550984    | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid Last,em:380097,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 | em:380097    | (Paid Last,em:380097,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

Voor de gegeven steekproefvraag, worden de resultaten gegeven in `last_touch` kolom. De kolom `last_touch` bestaat uit de volgende componenten:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parameters | Beschrijving |
| ---------- | ----------- |
| `{NAME}` | De `{CHANNEL_NAME}`, die als label in ADF is ingevoerd. |
| `{VALUE}` | De waarde van `{CHANNEL_VALUE}` die de laatste aanraking in [!DNL Experience Event], voorafgaand aan `{EXP_CONDITION}` is. |
| `{TIMESTAMP}` | Het tijdstempel van de [!DNL Experience Event] waar de laatste aanraking plaatsvond. |
| `{FRACTION}` | De attributie van de laatste aanraking, uitgedrukt als decimale breuk. |

### Last-touch-kenmerk met time-out bij verlopen

Deze query retourneert de laatste aanraakwaarde en details voor één kanaal in de doelgegevensset [!DNL Experience Event] voor een opgegeven tijdsperiode. De query retourneert een `struct`-object met de laatste aanraakwaarde, tijdstempel en attributie voor elke rij die voor het geselecteerde kanaal wordt geretourneerd.

Deze query is nuttig als u de laatste interactie binnen een geselecteerd tijdinterval wilt zien. In het onderstaande voorbeeld is de laatste aanraking die voor elke actie van de klant wordt geretourneerd, de laatste interactie binnen de volgende zeven dagen (`expTimeout = 86400 * 7`).

**Zoeksyntaxis**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{TIMESTAMP}` | Het tijdstempelveld in de gegevensset. |
| `{CHANNEL_NAME}` | Het label voor het geretourneerde object |
| `{CHANNEL_VALUE}` | De kolom of het gebied dat het doelkanaal voor de vraag is |
| `{EXP_TIMEOUT}` | Het tijdsvenster na de kanaalgebeurtenis, in seconden, waarin de query zoekt naar een laatste aanraakgebeurtenis. |

Een uitleg van de parameters binnen de functie `OVER()` vindt u in de sectie [vensterfuncties](#window-functions).

**Voorbeeldquery**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(timestamp, 'trackingCode', marketing.trackingCode, 86400 * 7)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Resultaten**

```console
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 | em:1024841   | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

Voor de gegeven steekproefvraag, worden de resultaten gegeven in `last_touch` kolom. De kolom `last_touch` bestaat uit de volgende componenten:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parameters | Beschrijving |
| ---------- | ----------- |
| `{NAME}` | De `{CHANNEL_NAME}`, ingegaan als etiket in ADF. |
| `{VALUE}` | De waarde van `{CHANNEL_VALUE}` die de laatste aanraking binnen het gespecificeerde `{EXP_TIMEOUT}` interval is |
| `{TIMESTAMP}` | De tijdstempel van de [!DNL Experience Event] waar de laatste aanraking heeft plaatsgevonden |
| `{FRACTION}` | De attributie van de laatste aanraking, uitgedrukt als decimale breuk. |

## Padcontrole

Pathing kan worden gebruikt om inzicht te krijgen in de diepte van de service van de klant, om te bevestigen dat de bedoelde stappen van een ervaring werken zoals deze zijn ontworpen, en om mogelijke pijnpunten te identificeren die gevolgen hebben voor de klant.

De volgende ADFs steunt het vestigen van het kleven meningen van hun vorige en volgende verhoudingen. U kunt vorige en volgende pagina&#39;s maken of meerdere gebeurtenissen doorlopen om te tekenen.

### Vorige pagina

Hiermee bepaalt u de vorige waarde van een bepaald veld met een opgegeven aantal stappen buiten het venster. In het voorbeeld wordt de functie `WINDOW` geconfigureerd met een frame van `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` dat ADF instelt om naar de huidige rij en alle volgende rijen te kijken.

**Zoeksyntaxis**

```sql
PREVIOUS({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{KEY}` | De kolom of het veld van de gebeurtenis. |
| `{SHIFT}` | (Optioneel) Het aantal gebeurtenissen dat zich niet bij de huidige gebeurtenis bevindt. De standaardwaarde is 1. |
| `{IGNORE_NULLS}` | (Optioneel) Een Booleaanse waarde die aangeeft of waarden `{KEY}` met de waarde null moeten worden genegeerd. De standaardwaarde is `false`. |

Een uitleg van de parameters binnen de functie `OVER()` vindt u in de sectie [vensterfuncties](#window-functions).

**Voorbeeldquery**

```sql
SELECT endUserIds._experience.mcid.id, _experience.analytics.session.num, timestamp, web.webPageDetails.name
    PREVIOUS(web.webPageDetails.name, 3)
      OVER(PARTITION BY endUserIds._experience.mcid.id, _experience.analytics.session.num
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, _experience.analytics.session.num, timestamp ASC
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

Voor de gegeven steekproefvraag, worden de resultaten gegeven in `previous_page` kolom. De waarde binnen de `previous_page` kolom is gebaseerd op `{KEY}` die in ADF wordt gebruikt.

### Volgende pagina

Hiermee bepaalt u de volgende waarde van een bepaald veld met een opgegeven aantal stappen buiten het venster. In het voorbeeld wordt de functie `WINDOW` geconfigureerd met een frame van `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` dat ADF instelt om naar de huidige rij en alle volgende rijen te kijken.

**Zoeksyntaxis**

```sql
NEXT({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{KEY}` | De kolom of het veld van de gebeurtenis. |
| `{SHIFT}` | (Optioneel) Het aantal gebeurtenissen dat zich niet bij de huidige gebeurtenis bevindt. De standaardwaarde is 1. |
| `{IGNORE_NULLS}` | (Optioneel) Een Booleaanse waarde die aangeeft of waarden `{KEY}` met de waarde null moeten worden genegeerd. De standaardwaarde is `false`. |

Een uitleg van de parameters binnen de functie `OVER()` vindt u in de sectie [vensterfuncties](#window-functions).

**Voorbeeldquery**

```sql
SELECT endUserIds._experience.aaid.id, timestamp, web.webPageDetails.name,
    NEXT(web.webPageDetails.name, 1, true)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
      AS previous_page
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

Voor de gegeven steekproefvraag, worden de resultaten gegeven in `previous_page` kolom. De waarde binnen de `previous_page` kolom is gebaseerd op `{KEY}` die in ADF wordt gebruikt.

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

Een uitleg van de parameters binnen de functie `OVER()` vindt u in de sectie [vensterfuncties](#window-functions).

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

Voor de gegeven steekproefvraag, worden de resultaten gegeven in `average_minutes_since_registration` kolom. De waarde in de kolom `average_minutes_since_registration` is het tijdsverschil tussen de huidige en vorige gebeurtenissen. De tijdseenheid is eerder gedefinieerd in `{TIME_UNIT}`.

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

Een uitleg van de parameters binnen de functie `OVER()` vindt u in de sectie [vensterfuncties](#window-functions).

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

Voor de gegeven steekproefvraag, worden de resultaten gegeven in `average_minutes_until_order_confirmation` kolom. De waarde in de kolom `average_minutes_until_order_confirmation` is het tijdsverschil tussen de huidige en volgende gebeurtenissen. De tijdseenheid is eerder gedefinieerd in `{TIME_UNIT}`.

## Volgende stappen

Gebruikend de hier beschreven functies, kunt u vragen schrijven om tot uw eigen [!DNL Experience Event] datasets toegang te hebben gebruikend [!DNL Query Service]. Voor meer informatie over auteursvragen in [!DNL Query Service], zie de documentatie over [het creëren van vragen](../creating-queries/creating-queries.md).

## Aanvullende bronnen

In de volgende video ziet u hoe u query&#39;s uitvoert in de Adobe Experience Platform-interface en in een PSQL-client. Bovendien gebruikt de video ook voorbeelden met afzonderlijke eigenschappen in een XDM-object, met gebruik van door Adobe gedefinieerde functies en met gebruik van CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)