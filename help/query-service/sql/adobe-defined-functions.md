---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Door Adobe gedefinieerde functies
topic: functions
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# Door Adobe gedefinieerde functies

De door Adobe-bepaalde functies (ADFs) zijn prebuilt functies in de Dienst van de Vraag die helpen gemeenschappelijke bedrijfsgerelateerde taken op de gegevens van ExperienceEvent uitvoeren. Dit zijn onder andere functies voor sessionisatie en Attributie, zoals die in Adobe Analytics zijn gevonden. Raadpleeg de documentatie [bij](https://docs.adobe.com/content/help/en/analytics/landing/home.html) Adobe Analytics voor meer informatie over Adobe Analytics en de concepten achter de ADF&#39;s die op deze pagina zijn gedefinieerd. Dit document bevat informatie over door Adobe gedefinieerde functies die beschikbaar zijn in Query Service.

## Vensterfuncties

De meerderheid van de bedrijfslogica vereist het verzamelen van de aanraakpunten voor een klant en het opdracht geven tot hen tegen tijd. Deze steun wordt verleend door SQL van de Vonk in de vorm van vensterfuncties. Vensterfuncties maken deel uit van standaard-SQL en worden ondersteund door vele andere SQL-engines.

Een vensterfunctie werkt een samenvoeging bij en retourneert één item voor elke rij in de geordende subset. De eenvoudigste aggregatiefunctie is `SUM()`. `SUM()` neemt uw rijen en geeft u één totaal. Als u in plaats daarvan `SUM()` op een venster toepast en het verandert in een vensterfunctie, ontvangt u bij elke rij een cumulatief bedrag.

De meerderheid van de SQL helpers van de Vonk zijn vensterfuncties die elke rij in uw venster bijwerken, met de staat van die toegevoegde rij.

### Specificatie

Syntaxis: `OVER ([partition] [order] [frame])`

| Parameter | Beschrijving |
| --- | --- |
| [partitie] | Een subgroep van de rijen op basis van een kolom of een beschikbaar veld. Voorbeeld: `PARTITION BY endUserIds._experience.mcid.id` |
| [bestellen] | Een kolom of beschikbaar veld dat wordt gebruikt om de subset of rijen te bestellen. Voorbeeld: `ORDER BY timestamp` |
| [frame] | Een subgroep van de rijen in een verdeling. Voorbeeld: `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## Sessionering

Wanneer u werkt met ExperienceEvent-gegevens die afkomstig zijn van een website, mobiele toepassing, interactief spraakreactiesysteem of een ander kanaal voor klantinteractie, is het handig als gebeurtenissen kunnen worden gegroepeerd rond een verwante periode van activiteit. Doorgaans hebt u een specifieke intentie om uw activiteiten te sturen, zoals het zoeken naar een product, het betalen van een rekening, het controleren van de balans, het invullen van een toepassing, enzovoort. Deze groepering helpt de gebeurtenissen associëren om meer context over de klantenervaring te ontdekken.

Raadpleeg de documentatie over [contextbewuste sessies](https://docs.adobe.com/content/help/en/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html)voor meer informatie over sessies in Adobe Analytics.

### Specificatie

Syntaxis: `SESS_TIMEOUT(timestamp, expirationInSeconds) OVER ([partition] [order] [frame])`

| Parameter | Beschrijving |
| --- | --- |
| `timestamp` | Tijdstempelveld gevonden in gegevensset |
| `expirationInSeconds` | Aantal seconden nodig tussen gebeurtenissen om het einde van de huidige sessie te kwalificeren en het begin van een nieuwe sessie |

| Parameters van geretourneerd object | Beschrijving |
| ---------------------- | ------------- |
| `timestamp_diff` | Tijd in seconden tussen huidige record en vorige record |
| `num` | Een uniek sessienummer, te beginnen bij 1, voor de sleutel die is gedefinieerd in de functie `PARTITION BY` van het venster. |
| `is_new` | Een Booleaanse waarde die wordt gebruikt om te bepalen of een record de eerste van een sessie is |
| `depth` | Diepte van de huidige record binnen de sessie |

#### Voorbeeldquery

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

#### Resultaten

```
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

## Attributie

Het koppelen van klantenacties aan succes is een belangrijk deel van het begrip van de factoren die klantenervaring beïnvloeden. De volgende ADFs steunt Eerste en laatste attributie met verschillende vervalmontages.

Zie het overzicht [van](https://docs.adobe.com/content/help/en/analytics/analyze/analysis-workspace/panels/attribution.html) Attributie-IQ in de Analyse Guide voor meer informatie over attributie in Adobe Analytics.

### Eerste aanraakkenmerk

Retourneert de eerste aanraakattributiewaarde en details voor één kanaal in de gegevensset van de target ExperienceEvent. De query retourneert een `struct` object met de eerste aanraakwaarde, tijdstempel en attributie voor elke rij die voor het geselecteerde kanaal wordt geretourneerd.

Deze vraag is nuttig als u wilt zien welke interactie tot een reeks klantenacties leidde. In het onderstaande voorbeeld wordt de eerste trackingcode (`em:946426`) in de ExperienceEvent-gegevens toegewezen aan 100% (`1.0`) verantwoordelijkheid voor de acties van de klant, aangezien dit de eerste interactie was.

### Specificatie

Syntaxis: `ATTRIBUTION_FIRST_TOUCH(timestamp, channelName, channelValue) OVER ([partition] [order] [frame])`

| Parameter | Beschrijving |
| --- | --- |
| `timestamp` | Tijdstempelveld gevonden in gegevensset |
| `channelName` | Een vriendelijke naam die als label in het geretourneerde object moet worden gebruikt |
| `channelValue` | De kolom of het gebied dat het doelkanaal voor de vraag is |


| Parameters van geretourneerd object | Beschrijving |
| ---------------------- | ------------- |
| `name` | De `channelName` ingevoerde gegevens als een label in de ADF |
| `value` | De waarde van `channelValue` dat is de eerste aanraking in de ExperienceEvent |
| `timestamp` | De tijdstempel van de ExperienceEvent waar de eerste aanraking plaatsvond |
| `fraction` | De toerekening van de eerste aanraking uitgedrukt als fractioneel krediet |

#### Voorbeeldquery

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

#### Resultaten

```
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

### Laatste aanraakkenmerk

Retourneert de laatste aanraakattributiewaarde en details voor één kanaal in de gegevensset van de target ExperienceEvent. De query retourneert een `struct` object met de laatste aanraakwaarde, tijdstempel en attributie voor elke rij die voor het geselecteerde kanaal wordt geretourneerd.

Deze vraag is nuttig als u de definitieve interactie in een reeks klantenacties wilt zien. In het onderstaande voorbeeld is de trackingcode in het geretourneerde object de laatste interactie in elke ExperienceEvent-record. Aan elke code wordt 100% (`1.0`) verantwoordelijkheid voor de acties van de klant toegewezen, aangezien dit de laatste interactie was.

### Specificatie

Syntaxis: `ATTRIBUTION_LAST_TOUCH(timestamp, channelName, channelValue) OVER ([partition] [order] [frame])`

| Parameter | Beschrijving |
| --- | --- |
| `timestamp` | Tijdstempelveld gevonden in gegevensset |
| `channelName` | Een vriendelijke naam die als label in het geretourneerde object moet worden gebruikt |
| `channelValue` | De kolom of het gebied dat het doelkanaal voor de vraag is |


| Parameters van geretourneerd object | Beschrijving |
| ---------------------- | ------------- |
| `name` | De `channelName` ingevoerde gegevens als een label in de ADF |
| `value` | De waarde van `channelValue` die de laatste aanraking in de ExperienceEvent is |
| `timestamp` | Het tijdstempel van de ExperienceEvent waar het `channelValue` werd gebruikt |
| `fraction` | Toekenning van de laatste aanraking uitgedrukt als fractioneel krediet |

#### Voorbeeldquery

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

#### Resultaten

```
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

### Eerste aanraakkenmerk met vervalvoorwaarde

Retourneert de eerste aanraakattributiewaarde en de details voor één kanaal in de gegevensset met doel-ExperienceEvent, die na of vóór een voorwaarde verlopen. De query retourneert een `struct` object met de eerste aanraakwaarde, tijdstempel en attributie voor elke rij die voor het geselecteerde kanaal wordt geretourneerd.

Deze vraag is nuttig als u wilt zien welke interactie tot een reeks klantenacties binnen een gedeelte van de dataset van ExperienceEvent leidde die door een voorwaarde van uw keuze wordt bepaald. In het onderstaande voorbeeld wordt een aankoop geregistreerd (`commerce.purchases.value IS NOT NULL`) op elk van de vier dagen die in de resultaten worden weergegeven (15 juli, 21 juli, 23 en 29 juli) en wordt de initiële volgcode op elke dag toegewezen aan 100% (`1.0`) verantwoordelijkheid voor de acties van de klant.

#### Specificatie

Syntaxis: `ATTRIBUTION_FIRST_TOUCH_EXP_IF(timestamp, channelName, channelValue, expCondition, expBefore) OVER ([partition] [order] [frame])`

| Parameter | Beschrijving |
| --- | --- |
| `timestamp` | Tijdstempelveld gevonden in gegevensset |
| `channelName` | Een vriendelijke naam die als label in het geretourneerde object moet worden gebruikt |
| `channelValue` | De kolom of het gebied dat het doelkanaal voor de vraag is |
| `expCondition` | De voorwaarde die het verlooppunt van het kanaal bepaalt |
| `expBefore` | Wordt standaard ingesteld op `false`. Booleaanse waarde die aangeeft of het kanaal vervalt voordat of nadat aan de opgegeven voorwaarde is voldaan. Primair ingeschakeld voor de vervalvoorwaarden van een sessie (bijvoorbeeld `sess.depth = 1, true`) om ervoor te zorgen dat de eerste aanraking niet wordt geselecteerd uit een vorige sessie. |

| Parameters van geretourneerd object | Beschrijving |
| ---------------------- | ------------- |
| `name` | De `channelName` ingevoerde gegevens als een label in de ADF |
| `value` | De waarde van `channelValue` dat is de eerste aanraking in de ExperienceEvent voorafgaand aan de `expCondition` |
| `timestamp` | De tijdstempel van de ExperienceEvent waar de eerste aanraking plaatsvond |
| `fraction` | De toerekening van de eerste aanraking uitgedrukt als fractioneel krediet |

#### Voorbeeldquery

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

#### Resultaten

```
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

### Eerste aanraakkenmerk met verlooptime-out

Retourneert de eerste aanraakattributiewaarde en details voor één kanaal in de gegevensset van de targetEvent voor een opgegeven tijdsperiode. De query retourneert een `struct` object met de eerste aanraakwaarde, tijdstempel en attributie voor elke rij die voor het geselecteerde kanaal wordt geretourneerd. Deze vraag is nuttig als u wilt zien welke interactie, binnen een geselecteerd tijdinterval, tot een klantenactie leidde. In het onderstaande voorbeeld is de eerste aanraking die voor elke actie van de klant wordt geretourneerd, de vroegste interactie binnen de voorafgaande zeven dagen (`expTimeout = 86400 * 7`).

#### Specificatie

Syntaxis: `ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(timestamp, channelName, channelValue, expTimeout) OVER ([partition] [order] [frame])`

| Parameter | Beschrijving |
| --- | --- |
| `timestamp` | Tijdstempelveld gevonden in gegevensset |
| `channelName` | Een vriendelijke naam die als label in het geretourneerde object moet worden gebruikt |
| `channelValue` | De kolom of het gebied dat het doelkanaal voor de vraag is |
| `expTimeout` | Het tijdsvenster (in seconden) voorafgaand aan de kanaalgebeurtenis dat de query zoekt naar een eerste aanraakgebeurtenis |

| Parameters van geretourneerd object | Beschrijving |
| ---------------------- | ------------- |
| `name` | De `channelName` ingevoerde gegevens als een label in de ADF |
| `value` | De waarde van `channelValue` dat is de eerste aanraking binnen het opgegeven `expTimeout` interval |
| `timestamp` | De tijdstempel van de ExperienceEvent waar de eerste aanraking plaatsvond |
| `fraction` | De toerekening van de eerste aanraking uitgedrukt als fractioneel krediet |

#### Voorbeeldquery

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

#### Resultaten

```
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

### Laatste aanraakkenmerk met vervalvoorwaarde

Retourneert de laatste aanraakattributiewaarde en de details voor één kanaal in de gegevensset van de ExperienceEvent-target, die verlopen na of vóór een voorwaarde. De query retourneert een `struct` object met de laatste aanraakwaarde, tijdstempel en attributie voor elke rij die voor het geselecteerde kanaal wordt geretourneerd. Deze vraag is nuttig als u de laatste interactie in een reeks klantenacties binnen een gedeelte van de dataset wilt zien ExperienceEvent die door een voorwaarde van uw het kiezen wordt bepaald. In het onderstaande voorbeeld wordt een aankoop geregistreerd (`commerce.purchases.value IS NOT NULL`) op elk van de vier dagen die in de resultaten worden weergegeven (15 juli, 21 juli, 23 en 29 juli) en wordt de laatste trackingcode op elke dag toegewezen aan 100% (`1.0`) verantwoordelijkheid voor de acties van de klant.

#### Specificatie

Syntaxis: `ATTRIBUTION_LAST_TOUCH_EXP_IF(timestamp, channelName, channelValue, expCondition, expBefore) OVER ([partition] [order] [frame])`

| Parameter | Beschrijving |
| --- | --- |
| `timestamp` | Tijdstempelveld gevonden in gegevensset |
| `channelName` | Een vriendelijke naam die als label in het geretourneerde object moet worden gebruikt |
| `channelValue` | De kolom of het gebied dat het doelkanaal voor de vraag is |
| `expCondition` | De voorwaarde die het verlooppunt van het kanaal bepaalt |
| `expBefore` | Wordt standaard ingesteld op `false`. Booleaanse waarde die aangeeft of het kanaal vervalt voordat of nadat aan de opgegeven voorwaarde is voldaan. Primair ingeschakeld voor de voorwaarden bij het verlopen van de sessie (bijvoorbeeld `sess.depth = 1, true`) om ervoor te zorgen dat de laatste aanraking niet wordt geselecteerd uit een vorige sessie. |

| Parameters van geretourneerd object | Beschrijving |
| ---------------------- | ------------- |
| `name` | De `channelName` ingevoerde gegevens als een label in de ADF |
| `value` | De waarde van `channelValue` dat is de laatste aanraking in de ExperienceEvent voorafgaand aan de `expCondition` |
| `timestamp` | Het tijdstempel van de ExperienceEvent waar de laatste aanraking plaatsvond |
| `percentage` | Toekenning van de laatste aanraking uitgedrukt als fractioneel krediet |

#### Voorbeeldquery

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

#### Resultaten

```
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

### Laatste aanraakkenmerk met eindtime-out

Retourneert de laatste aanraakattributiewaarde en de details voor één kanaal in de gegevensset van de targetExperienceEvent voor een opgegeven tijdsperiode. De query retourneert een `struct` object met de laatste aanraakwaarde, tijdstempel en attributie voor elke rij die voor het geselecteerde kanaal wordt geretourneerd. Deze query is nuttig als u de laatste interactie binnen een geselecteerd tijdinterval wilt zien. In het onderstaande voorbeeld is de laatste aanraking die voor elke actie van de klant wordt geretourneerd, de laatste interactie binnen de volgende zeven dagen (`expTimeout = 86400 * 7`).

#### Specificatie

Syntaxis: `ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(timestamp, channelName, channelValue, expTimeout) OVER ([partition] [order] [frame])`

| Parameter | Beschrijving |
| --- | --- |
| `timestamp` | Tijdstempelveld gevonden in gegevensset |
| `channelName` | Een vriendelijke naam die als label in het geretourneerde object moet worden gebruikt |
| `channelValue` | De kolom of het gebied dat het doelkanaal voor de vraag is |
| `expTimeout` | Het tijdsvenster (in seconden) na de kanaalgebeurtenis waarin de query zoekt naar een laatste aanraakgebeurtenis |

| Parameters van geretourneerd object | Beschrijving |
| ---------------------- | ------------- |
| `name` | De `channelName` ingevoerde gegevens als een label in de ADF |
| `value` | De waarde van `channelValue` dat de laatste aanraking binnen het opgegeven `expTimeout` interval is |
| `timestamp` | De tijdstempel van de ExperienceEvent waar de laatste aanraking plaatsvond |
| `percentage` | Toekenning van de laatste aanraking uitgedrukt als fractioneel krediet |

#### Voorbeeldquery

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

#### Resultaten

```
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

## Vorige/volgende aanraking

Het is belangrijk te begrijpen hoe klanten binnen een ervaring navigeren. Het kan worden gebruikt om inzicht te krijgen in de diepte van de service van de klant, om te bevestigen dat de beoogde stappen van een ervaring werken zoals deze zijn ontworpen, en om mogelijke pijnpunten te identificeren die gevolgen hebben voor de klant. De volgende ADFs steunt het vestigen van het kleven meningen van hun Vorige en Volgende verhoudingen. U kunt Vorige pagina en Volgende pagina maken of meerdere gebeurtenissen doorlopen om Pathing te maken.

### Vorige aanraking

Hiermee bepaalt u de vorige waarde van een bepaald veld met een opgegeven aantal stappen buiten het venster. Bericht in het voorbeeld dat de `WINDOW` Functie met een kader wordt gevormd om ADF te `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` plaatsen om de huidige rij en allen vóór het te bekijken.

#### Specificatie

Syntaxis: `PREVIOUS(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])`

| Parameter | Beschrijving |
| --- | --- |
| `key` | De kolom of het veld van de gebeurtenis. |
| `shift` | (optioneel) Het aantal gebeurtenissen dat zich niet bij de huidige gebeurtenis bevindt. De standaardwaarde is 1. |
| `ingnoreNulls` | Booleaanse waarde die wordt aangegeven als null- `key` waarden moeten worden genegeerd. Standaard is dit `false`. |


| Parameters van geretourneerd object | Beschrijving |
| ---------------------- | ------------- |
| `value` | De waarde die wordt gebaseerd op de `key` gebruikte ADF |

#### Voorbeeldquery

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

#### Resultaten

```
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

### Volgende aanraking

Hiermee bepaalt u de volgende waarde van een bepaald veld met een opgegeven aantal stappen buiten het venster. Bericht in het voorbeeld dat de `WINDOW` `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` Functie met een kader van het plaatsen ADF wordt gevormd om de huidige rij en allen na het te bekijken.

#### Specificatie

Syntaxis: `NEXT(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])`

| Parameter | Beschrijving |
| --- | --- |
| `key` | De kolom of het veld van de gebeurtenis |
| `shift` | (optioneel) Het aantal gebeurtenissen dat zich niet bij de huidige gebeurtenis bevindt. De standaardwaarde is 1. |
| `ingnoreNulls` | Booleaanse waarde die wordt aangegeven als null- `key` waarden moeten worden genegeerd. Standaard is dit `false`. |


| Parameters van geretourneerd object | Beschrijving |
| ---------------------- | ------------- |
| `value` | De waarde die wordt gebaseerd op de `key` gebruikte ADF |

#### Voorbeeldquery

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

#### Resultaten

```
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

## Tijd-tussen

De tijd-tussen staat u toe om latent klantengedrag binnen een periode vóór of na een gebeurtenis te onderzoeken voorkomt. Bekijk de gebeurtenissen binnen 7 dagen na een campagne of een ander type gebeurtenis voor al uw klanten.

### Tijd tussen vorige overeenkomst

Verstrekt een nieuwe dimensie, die de tijd meet die sinds een bepaald incident is verstreken.

#### Specificatie

Syntaxis: `TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventDefintion, [timeUnit]) OVER ([partition] [order] [frame])`

| Parameter | Beschrijving |
| --- | --- |
| `timestamp` | Tijdstempelveld gevonden in de gegevensset die is ingevuld bij alle gebeurtenissen. |
| `eventDefintion` | Uitdrukking om de vorige gebeurtenis te kwalificeren. |
| `timeUnit` | Uitvoereenheid: dagen, uren, minuten en seconden. De standaardwaarde is seconden. |

Uitvoer: Retourneert een getal dat de tijdseenheid vertegenwoordigt sinds de vorige overeenkomende gebeurtenis werd weergegeven of blijft null als er geen overeenkomende gebeurtenis is gevonden.

#### Voorbeeldquery

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

#### Resultaten

```
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

### Tijd tussen volgende overeenkomst

Verstrekt een nieuwe dimensie, die de tijd meet alvorens een bepaalde gebeurtenis voorkomt.

#### Specificatie

Syntaxis: `TIME_BETWEEN_NEXT_MATCH(timestamp, eventDefintion, [timeUnit]) OVER ([partition] [order] [frame])`

| Parameter | Beschrijving |
| --- | --- |
| `timestamp` | Tijdstempelveld gevonden in de gegevensset die is ingevuld bij alle gebeurtenissen. |
| `eventDefintion` | Uitdrukking om de volgende gebeurtenis te kwalificeren. |
| `timeUnit` | Uitvoereenheid: dagen, uren, minuten en seconden. De standaardwaarde is seconden. |

Uitvoer: Retourneert een negatief getal dat de tijdseenheid achter de volgende overeenkomende gebeurtenis vertegenwoordigt of blijft null als er geen overeenkomende gebeurtenis wordt gevonden.

#### Voorbeeldquery

```
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

#### Resultaten

```
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

## Volgende stappen

Gebruikend de hier beschreven functies, kunt u vragen schrijven om tot uw eigen datasets toegang te hebben ExperienceEvent gebruikend de Dienst van de Vraag. Voor meer informatie over auteursvragen in de Dienst van de Vraag, zie de documentatie bij het [creëren van vragen](../creating-queries/creating-queries.md).
