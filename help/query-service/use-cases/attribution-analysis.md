---
title: Attributieanalyse
description: In dit document wordt uitgelegd hoe u met Query Service een techniek voor het meten van de marketingeffectiviteit kunt maken op basis van het marketingtoewijzingsmodel van eerste en laatste aanraking.
exl-id: d62cd349-06fc-4ce6-a5e8-978f11186927
source-git-commit: e33d59c4ac28f55ba6ae2fc073d02f8738159263
workflow-type: tm+mt
source-wordcount: '1419'
ht-degree: 0%

---

# Attributieanalyse

Attributie is een analytisch concept dat helpt om de marketing tactiek zoals kanalen, aanbiedingen, en berichten te bepalen, die tot bedrijfsverkoop of omzettingen bijdragen. Dit concept evalueert de reis van de consument (het proces waardoor een klant met een bedrijf in wisselwerking staat om een doel te bereiken) die in een aankoop of een verwerving resulteert die op klantenaanraakpunten (om het even welk ogenblik een consument met uw merk in wisselwerking staat). Door attributieanalyse kunnen marketers het rendement van investeringen beoordelen van de kanalen die hen met een potentiële klant verbinden.

## Aan de slag

De SQL-voorbeelden in dit document zijn query&#39;s die veel worden gebruikt met Adobe Analytics-gegevens. Deze zelfstudie vereist een goed begrip van de volgende componenten:

* [De Adobe Analytics-bronconnector voor het overzicht van rapportsuite-gegevens](../../sources/connectors/adobe-applications/mapping/analytics.md).
* [De documentatie over toewijzingen in het veld Analytics](../../sources/connectors/adobe-applications/mapping/analytics.md) Verstrekt meer informatie over het opnemen van en het in kaart brengen van analysegegevens voor gebruik met de Dienst van de Vraag.
* [Overzicht van de Attribution IQ](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html)
* [De handleiding in het deelvenster Adobe Analytics-kenmerken](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution.html).

Een uitleg van de parameters binnen de `OVER()` kan worden gevonden in de [sectie vensterfuncties](../sql/adobe-defined-functions.md#window-functions). De [Verklarende woordenlijst Adobe Marketing en Commerce](https://business.adobe.com/glossary/index.html) kan ook nuttig zijn.

Voor elk van de volgende gebruiksgevallen wordt een geparametriseerd SQL vraagvoorbeeld verstrekt als malplaatje voor u aan te passen. Geef parameters op waar u ze ziet `{ }` in de SQL-voorbeelden die u wilt evalueren.

## Doelstellingen

Een attributiegebruikscase gebruikt Adobe Analytics-gegevens om acties van klanten te helpen koppelen aan een succesvol resultaat. Deze vereniging is een kritiek deel van het begrip van de factoren die klantenervaringen beïnvloeden. De gegevens van de attributieanalyse kunnen worden gebruikt om het belang van het aanraakpunt van een klant tijdens de klantenreis te begrijpen.

De queryvoorbeelden in dit document ondersteunen verschillende gebruiksgevallen voor eerste aanraking en laatste aanraakkenmerk met verschillende vervalinstellingen. In deze handleiding worden de volgende belangrijke concepten geïllustreerd:

* Eerste aanraking en laatste aanraakkenmerk.
* Eerste aanraking en laatste aanraking met vervalonderbreking.
* Eerste aanraking en laatste aanraakkenmerk met vervalvoorwaarde.

## Parameters voor kenmerkquery {#attribution-query-parameters}

In de onderstaande tabel vindt u een overzicht van de parameters en de beschrijvingen die worden gebruikt bij query&#39;s voor eerste aanraking en laatste aanraakkenmerk:

| Parameter | Beschrijving |
|---|---|
| `{TIMESTAMP}` | Het tijdstempelveld in de gegevensset. |
| `{CHANNEL_NAME}` | Het label voor het geretourneerde object. |
| `{CHANNEL_VALUE}` | De kolom of het gebied dat het doelkanaal voor de vraag is. |
| `{EXP_TIMEOUT}` | Het tijdvenster voorafgaand aan de kanaalgebeurtenis, in seconden, waarin de query zoekt naar een eerste aanraakgebeurtenis. |
| `{EXP_CONDITION}` | De voorwaarde die het verlooppunt van het kanaal bepaalt. |
| `{EXP_BEFORE}` | Een Booleaanse waarde die aangeeft of het kanaal voor of na de opgegeven voorwaarde vervalt. `{EXP_CONDITION}`, is voldaan. Deze optie is vooral ingeschakeld voor de vervalvoorwaarden van een sessie, zodat de eerste aanraking niet wordt geselecteerd uit een vorige sessie. Deze waarde is standaard ingesteld op `false`. |

## Kolomcomponenten van zoekresultaten {#query-result-column-components}

De resultaten voor de toewijzingsquery&#39;s worden gegeven in de `first_touch` of de `last_touch` kolom. Deze kolommen bestaan uit de volgende componenten:

```console
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parameters | Beschrijving |
| ---------- | ----------- |
| `{NAME}` | De `{CHANNEL_NAME}`, ingevoerd als label in de Azure Data Factory (ADF). |
| `{VALUE}` | De waarde van `{CHANNEL_VALUE}` dat de laatste aanraking binnen gespecificeerde is `{EXP_TIMEOUT}` interval |
| `{TIMESTAMP}` | De tijdstempel van de [!DNL Experience Event] waar de laatste aanraking heeft plaatsgevonden |
| `{FRACTION}` | De attributie van de laatste aanraking, uitgedrukt als decimale breuk. |

### Eerste aanraakkenmerk {#first-touch}

Met Eerste aanraakattributie wordt 100% van de verantwoordelijkheid voor een succesvol resultaat van het oorspronkelijke kanaal dat de consument heeft gekend, erkend. Dit SQL voorbeeld wordt gebruikt om de interactie te benadrukken die tot een verdere reeks klantenacties leidde.

Met de onderstaande query worden de eerste aanraakwaarde en details van het kanaal in het doel geretourneerd [!DNL Experience Event] dataset. Het geeft ook een `struct` -object voor het geselecteerde kanaal met de eerste aanraakwaarde, tijdstempel en kenmerk voor elke rij.

>[!NOTE]
>
>De Experience Cloud-id (ECID) wordt ook wel MCID genoemd en wordt nog steeds gebruikt in naamruimten.

**Zoeksyntaxis**

```sql
ATTRIBUTION_FIRST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

Voor een volledige lijst van potentieel vereiste parameters en hun beschrijvingen, zie [sectie met toewijzingsqueryparameters](#attribution-query-parameters).

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

In de onderstaande resultaten wordt de eerste trackingcode `em:946426` wordt genomen uit de [!DNL Experience Event] dataset. Deze volgcode wordt toegewezen met 100% (`1.0`) van de verantwoordelijkheid voor de acties van de klant omdat dit de eerste interactie was.

```console
                 id                 |       timestamp       | trackingCode |                   first_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
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

Voor een uitsplitsing van de resultaten die in de `first_touch` kolom, zie [sectie kolomcomponenten](#query-result-column-components).

### Laatste aanraakkenmerk {#second-touch}

De laatste aanraakeigenschap erkent 100% van de verantwoordelijkheid voor een succesvol resultaat van het laatste kanaal dat de consument heeft ontmoet. Dit SQL voorbeeld wordt gebruikt om de definitieve interactie in een reeks klantenacties te benadrukken.

De query retourneert de laatste aanraakwaarde en details van het kanaal in het doel [!DNL Experience Event] dataset. Het geeft ook een `struct` -object voor het geselecteerde kanaal met de laatste aanraakwaarde, tijdstempel en kenmerk voor elke rij.

**Zoeksyntaxis**

```sql
ATTRIBUTION_LAST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

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

In de hieronder weergegeven resultaten is de trackingcode in het geretourneerde object de laatste interactie in elke [!DNL Experience Event] opnemen. Aan elke code wordt 100% toegewezen (`1.0`) verantwoordelijkheid voor de acties van de klant, aangezien het de laatste interactie was.

```console
                 id                |       timestamp       | trackingCode |                   last_touch                   
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

Voor een uitsplitsing van de resultaten die in de `last_touch` kolom, zie [sectie kolomcomponenten](#query-result-column-components).

### Eerste aanraakkenmerk met vervalvoorwaarde {#first-touch-attribution-with-expiration-condition}

Deze vraag wordt gebruikt om te zien welke interactie tot een reeks klantenacties binnen een gedeelte van leidde [!DNL Experience Event] dataset die door een voorwaarde van uw het kiezen wordt bepaald.

De query retourneert de eerste aanraakwaarde en details voor één kanaal in het doel [!DNL Experience Event] dataset, die na of vóór een voorwaarde verloopt. Het geeft ook een `struct` -object met de eerste aanraakwaarde, tijdstempel en kenmerk voor elke rij die wordt geretourneerd voor het geselecteerde kanaal.

**Zoeksyntaxis**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

Voor een volledige lijst van potentieel vereiste parameters en hun beschrijvingen, zie [sectie met toewijzingsqueryparameters](#attribution-query-parameters).

**Voorbeeldquery**

In het onderstaande voorbeeld wordt een aankoop opgenomen (`commerce.purchases.value IS NOT NULL`) op elk van de vier dagen in de resultaten (15, 21, 23 en 29 juli), en de initiële volgcode op elke dag wordt toegewezen aan 100% (`1.0`) verantwoordelijkheid voor de acties van de klant.

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
                 id               |       timestamp       | trackingCode |                   first_touch                   
----------------------------------+-----------------------+--------------+-------------------------------------------------
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

Voor een uitsplitsing van de resultaten die in de `first_touch` kolom, zie [sectie kolomcomponenten](#query-result-column-components).

### Eerste aanraakkenmerk met verlooptime-out {#first-touch-attribution-with-expiration-timeout}

Deze vraag wordt gebruikt om de interactie, binnen een geselecteerde tijdspanne te vinden, die tot de succesvolle klantenactie leidde.

De onderstaande query retourneert de eerste aanraakwaarde en details voor één kanaal in het doel [!DNL Experience Event] dataset voor een gespecificeerde tijdspanne. De query retourneert een `struct` -object met de eerste aanraakwaarde, tijdstempel en kenmerk voor elke rij die wordt geretourneerd voor het geselecteerde kanaal.

**Zoeksyntaxis**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

Voor een volledige lijst van potentieel vereiste parameters en hun beschrijvingen, zie [sectie met toewijzingsqueryparameters](#attribution-query-parameters).

**Voorbeeldquery**

In het onderstaande voorbeeld is de eerste aanraking die voor elke actie van de klant wordt geretourneerd, de vroegste interactie binnen de voorafgaande zeven dagen (expTimeout = 86400 * 7).

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
-----------------------------------+-----------------------+--------------+-------------------------------------------------
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

Voor een uitsplitsing van de resultaten die in de `first_touch` kolom, zie [sectie kolomcomponenten](#query-result-column-components).

### Laatste aanraakkenmerk met vervalvoorwaarde {#last-touch-attribution-with-expiration-condition}

Deze vraag wordt gebruikt om de laatste interactie in een reeks klantenacties binnen een gedeelte van te vinden [!DNL Experience Event] dataset die door een voorwaarde van uw het kiezen wordt bepaald.

De onderstaande query retourneert de laatste aanraakwaarde en details voor één kanaal in het doel [!DNL Experience Event] dataset, die na of vóór een voorwaarde verloopt. De query retourneert een `struct` -object met de laatste aanraakwaarde, tijdstempel en kenmerk voor elke rij die wordt geretourneerd voor het geselecteerde kanaal.

**Zoeksyntaxis**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

Voor een volledige lijst van potentieel vereiste parameters en hun beschrijvingen, zie [sectie met toewijzingsqueryparameters](#attribution-query-parameters).

**Voorbeeldquery**

In het onderstaande voorbeeld wordt een aankoop opgenomen (`commerce.purchases.value IS NOT NULL`) op elk van de vier dagen in de resultaten (15, 21, 23 en 29 juli), en de laatste volgcode op elke dag wordt toegewezen aan 100% (`1.0`) verantwoordelijkheid voor de acties van de klant.

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
                id                 |       timestamp       | trackingCode |                   last_touch                   
-----------------------------------+-----------------------+--------------+------------------------------------------------
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

Voor een uitsplitsing van de resultaten die in de `last_touch` kolom, zie [sectie kolomcomponenten](#query-result-column-components).

### Laatste aanraakkenmerk met eindtime-out {#last-touch-attribution-with-expiration-timeout}

Deze vraag wordt gebruikt om de laatste interactie binnen een geselecteerd tijdinterval te vinden. De query retourneert de laatste aanraakkenmerkwaarde en details voor één kanaal in het doel [!DNL Experience Event] dataset voor een gespecificeerde tijdspanne. De query retourneert een `struct` -object met de laatste aanraakwaarde, tijdstempel en kenmerk voor elke rij die wordt geretourneerd voor het geselecteerde kanaal.

**Zoeksyntaxis**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

Voor een volledige lijst van potentieel vereiste parameters en hun beschrijvingen, zie [sectie met toewijzingsqueryparameters](#attribution-query-parameters).

**Voorbeeldquery**

In het onderstaande voorbeeld is de laatste aanraking die voor elke actie van de klant wordt geretourneerd, de laatste interactie binnen de volgende zeven dagen (`expTimeout = 86400 * 7`).

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

Voor een uitsplitsing van de resultaten die in de `last_touch` kolom, zie [sectie kolomcomponenten](#query-result-column-components).
