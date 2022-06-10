---
title: Activiteitenanalyse met Adobe Target
description: Dit document verklaart hoe te om de Dienst van de Vraag te gebruiken om actionable inzichten van datasets tot stand te brengen die met uw gegevens van Adobe Target worden gecreeerd.
source-git-commit: 870626f25b1aabdcb5739bbb1ab85bdad44df195
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 2%

---

# Activiteitenanalyse met Adobe Target

Adobe Experience Platform staat u toe om gegevens van Adobe Target in te voeren gebruikend de gebieden van het Gegevensmodel van de Ervaring (XDM) om datasets voor gebruik met de Dienst van de Vraag tot stand te brengen. Aangezien Adobe Target wordt ontworpen om inhoud aan te passen en gebruikerservaringen te personaliseren, staan de vragen die op deze datasets worden in werking gesteld voor hoogst gepersonaliseerde en geconcentreerde inzichten toe door gebruikersactiviteit door SQL te analyseren.

Dit document verstrekt een verscheidenheid van steekproefSQL vragen die gemeenschappelijke gebruiksgevallen aantonen die op het gedrag en de kenmerken van de klanten worden gebaseerd.

## Aan de slag

Voor elk van de volgende gebruiksgevallen wordt een geparametriseerd SQL vraagvoorbeeld verstrekt als malplaatje voor u aan te passen. Geef parameters op waar u ze ziet `{ }` in de SQL-voorbeelden die u wilt evalueren.

## Partiële XDM-veldtoewijzing op hoog niveau

De volgende tabel bevat een lijst met veelvoorkomende doelvelden en de bijbehorende XDM-velden die eraan zijn toegewezen.

>[!NOTE]
>
>Het gebruik van `[ ]` in het XDM-veld een array aanduidt.

| Naam doelveld | XDM-veldnaam | Notities |
|---|---|---|
| `mboxName` | `_experience.target.mboxname` | N.v.t. |
| Activiteits-id | `_experience.target.activities.activityID` | N.v.t. |
| Ervaring-id | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID` | N.v.t. |
| Segment-id | `_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id` | N.v.t. |
| Gebeurtenisbereik | `_experience.target.activities[].activityEvents[].eventScope` | In dit veld worden nieuwe bezoekers en bezoeken bijgehouden. |
| Stap-id | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID` | Dit veld is een aangepaste stap-id voor Adobe Campaign. |
| Prijs totaal | commerce.order.priceTotal | N.v.t. |

>[!IMPORTANT]
>
>De naam van een gegevensset die automatisch wordt gemaakt met behulp van doelgegevens is &quot;Adobe Target Experience Events&quot;. Wanneer het gebruiken van deze dataset met vragen, gebruik de naam `adobe_target_experience_events`.

## Doelstellingen

Door gebruikersactiviteiten te analyseren, kunt u inhoud voor een specifiek publiek personaliseren en verschillende versies van de inhoud voor een individuele entiteit testen. Door een specifieke activiteit gedurende een bepaalde periode of voor individuele gebruikers te analyseren, kunnen de prestaties van elke afzonderlijke activiteit beter worden begrepen. De resultaten van deze gecombineerde analyse kunnen worden gebruikt om inzicht te krijgen in de prestaties van elke afzonderlijke activiteit.

De volgende zaken van het verpersoonlijkingsgebruik worden gecreeerd gebruikend de gegevens van Adobe Target en nadruk op gebruikersactiviteiten om waardevolle inzichten in het gedrag van klanten over bedrijfstoepassingen tot stand te brengen.

In deze handleiding worden de volgende belangrijke concepten geïllustreerd aan de hand van voorbeelden van gebruiksgevallen:

* Om inzicht te krijgen in de prestaties van een activiteit-id voor een bepaalde dag, zoals telling, details en bijbehorende ervaring-id&#39;s.
* De bezoeker en het gebeurtenisbereik voor een activiteit bepalen.
* Om het aantal bezoekers, bezoeken en beeldinformatie voor Ervaring ID, Segment ID en identiteitskaart van de Activiteit te verzamelen.

### Aantal per uur activiteit genereren voor een bepaalde dag

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

### Gegevens per uur genereren voor een specifieke

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

### De lijst met ervaring-id&#39;s voor een specifieke activiteit voor een bepaalde dag bepalen

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

### Het aantal bezoekers, bezoeken en indrukken per activiteit voor een bepaalde dag bepalen

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

### Bepaal bezoekers, bezoeken, en beelden voor Ervings identiteitskaart, Identiteitskaart van het Segment en EventScope voor een bepaalde dag

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
