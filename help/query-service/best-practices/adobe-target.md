---
keywords: Experience Platform;home;popular topics;query service;Query service;sample queries;sample query;adobe target;
solution: Experience Platform
title: Voorbeeldquery's
topic: queries
description: Gegevens uit Adobe Target worden omgezet in XDM-schema voor Experience Event en worden als datasets voor u opgenomen in Experience Platform. Dit document bevat steekproefvragen voor het gebruiken van de Dienst van de Vraag met uw datasets van Adobe Target.
translation-type: tm+mt
source-git-commit: e2c648829bb3268ab319da934f5cc6cc811290b3
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# Voorbeeldquery&#39;s voor Adobe Target-gegevens

Gegevens uit Adobe Target worden omgezet in XDM-schema voor Experience Event en worden als datasets voor u opgenomen in Adobe Experience Platform. Er zijn vele gebruiksgevallen voor de Dienst van de Vraag van Adobe Experience Platform met deze gegevens, en de volgende steekproefvragen zouden met uw datasets van Adobe Target moeten werken.

In Experience Platform, is de naam van auto-gecreeerde dataset &quot;de Gebeurtenissen van de Ervaring van Adobe Target&quot;. Wanneer het gebruiken van deze dataset met vragen, zou u de naam `adobe_target_experience_events` moeten gebruiken.

## Partiële XDM-veldtoewijzing op hoog niveau

In de volgende lijst worden de doelvelden weergegeven die zijn toegewezen aan hun overeenkomstige XDM-velden.

>[!NOTE]
>
> Het gebruik van `[ ]` binnen het XDM gebied wijst op een serie.

- mboxName: `_experience.target.mboxname`
- Activiteit-id: `_experience.target.activities.activityID`
- Ervings-id: `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID`
- Segment-id: `_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id`
- Gebeurtenisbereik: `_experience.target.activities[].activityEvents[].eventScope`
   - In dit veld worden nieuwe bezoekers en bezoeken bijgehouden.
- Stap-id: `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID`
   - Dit veld is een aangepaste stap-id voor Adobe Campaign.
- Prijstotaal: `commerce.order.priceTotal`

## Voorbeeldquery&#39;s

De volgende vragen tonen voorbeelden van algemeen gebruikte vragen met Adobe Target.

In de volgende voorbeelden, zult u SQL moeten uitgeven om de verwachte parameters voor uw vragen in te vullen die op de dataset, variabelen, of timeframe worden gebaseerd u in het evalueren geinteresseerd bent. Geef parameters op waar u `{ }` in de SQL ziet.

### Aantal uren activiteit gedurende een bepaalde dag

```sql
SELECT
  Hour,
  ActivityID,
  COUNT(ActivityID) AS Instances
FROM
(
  SELECT
    date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
    EXPLODE(_experience.target.activities.activityID) AS ActivityID
  FROM adobe_target_experience_events
  WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, ActivityID
ORDER BY Hour DESC, Instances DESC
LIMIT 24
```

### Uurdetails voor een specifieke activiteit voor een bepaalde dag

```sql
SELECT
  date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
  _experience.target.activities.activityID AS ActivityID,
  COUNT(ActivityID) AS Instances
FROM adobe_target_experience_events
WHERE
  array_contains( _experience.target.activities.activityID, {Activity ID} ) AND 
    TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
  _experience.target.activities IS NOT NULL
GROUP BY Hour, ActivityID
ORDER BY Hour DESC
LIMIT 24
```

### Ervings-id&#39;s voor een specifieke activiteit voor een bepaalde dag

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  COUNT(ExperienceID) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents._experience.target.activity.activityevent.context.experienceID) AS ExperienceID
  FROM
  (
    SELECT
      date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
      EXPLODE(_experience.target.activities) AS Activities
    FROM adobe_target_experience_events
    WHERE 
      TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
      _experience.target.activities IS NOT NULL
  )
  WHERE Activities.activityID = {activity_id}
)
GROUP BY Day, Activities.activityID, ExperienceID
ORDER BY Day DESC, Instances DESC
LIMIT 20
```

### Retourneer een lijst met gebeurtenisbereiken (bezoeker, bezoek, indruk) per instantie per activiteit-id voor een bepaalde dag

```sql
SELECT
  Day,
  Activities.activityID,
  EventScope,
  COUNT(EventScope) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents.eventScope) AS EventScope
  FROM
  (
    SELECT
      date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
      EXPLODE(_experience.target.activities) AS Activities
    FROM adobe_target_experience_events
    WHERE 
      TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
      _experience.target.activities IS NOT NULL
  )
)
GROUP BY Day, Activities.activityID, EventScope
ORDER BY Day DESC, Instances DESC
LIMIT 30
```

### Aantal bezoekers, bezoeken, indrukken per activiteit gedurende een bepaalde dag

```sql
SELECT
  Hour,
  Activities.activityid,
  SUM(CASE WHEN array_contains( Activities.activityEvents.eventScope, 'visitor' ) THEN 1 END) as Visitors,
  SUM(CASE WHEN array_contains( Activities.activityEvents.eventScope, 'visit' ) THEN 1 END) as Visits,
  SUM(CASE WHEN array_contains( Activities.activityEvents.eventScope, 'impression' ) THEN 1 END) as Impressions
FROM
(
  SELECT
    date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
    EXPLODE(_experience.target.activities) AS Activities
  FROM adobe_target_experience_events
  WHERE
    TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, Activities.activityid
ORDER BY Hour DESC, Visitors DESC
LIMIT 30
```

### Retourbezoekers, bezoeken, indrukkingen voor belevenis-id, Segment-id en EventScope voor een bepaalde dag

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  SegmentID._id,
  SUM(CASE WHEN ActivityEvent.eventScope = 'visitor' THEN 1 END) as Visitors,
  SUM(CASE WHEN ActivityEvent.eventScope = 'visit' THEN 1 END) as Visits,
  SUM(CASE WHEN ActivityEvent.eventScope = 'impression' THEN 1 END) as Impressions
FROM
(
  SELECT
    Day,
    Activities,
    ActivityEvent,
    ActivityEvent._experience.target.activity.activityevent.context.experienceID AS ExperienceID,
    EXPLODE(ActivityEvent.segmentEvents.segmentID) AS SegmentID
  FROM
  (
    SELECT
      Day,
      Activities,
      EXPLODE(Activities.activityEvents) AS ActivityEvent
    FROM
    (
      SELECT
        date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
        EXPLODE(_experience.target.activities) AS Activities
      FROM adobe_target_experience_events
      WHERE 
        TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
        _experience.target.activities IS NOT NULL
      LIMIT 1000000
    )
    LIMIT 1000000
  )
  LIMIT 1000000
)
GROUP BY Day, Activities.activityID, ExperienceID, SegmentID._id
ORDER BY Day DESC, Activities.activityID, ExperienceID ASC, SegmentID._id ASC, Visitors DESC
LIMIT 20
```

### De namen van de terugkeerdoos en telling van verslagen voor een bepaalde dag

```sql
SELECT
  _experience.target.mboxname,
  COUNT(timestamp) AS records
FROM
  adobe_target_experience_events
WHERE
  TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
  GROUP BY _experience.target.mboxname ORDER BY records DESC
LIMIT 100
```
