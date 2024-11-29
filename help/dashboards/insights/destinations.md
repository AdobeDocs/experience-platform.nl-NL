---
title: Invoer doelen
description: Ontdek SQL die uw bestemmingsinzichten en gebruik deze vragen aandrijft om douaneinzichten te produceren om de activering van gegevens van Adobe Experience Platform verder te onderzoeken.
exl-id: 762a9960-e7a5-4796-80c7-ef745157cc04
source-git-commit: cce576c00823a0c02e4b639f0888a466a5af6a0c
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 0%

---

# bestemmingsinzichten

De inzichten die zijn afgeleid van de analyse van uw gegevensmodel maken uw Adobe Real-Time CDP-gegevens toegankelijker, begrijpelijker en effectiever voor de besluitvorming.

Begrijp uw bestemmingsinzicht door tot SQL toegang te hebben die hen macht, dan uw eigen inzichten produceert om de activering van gegevens van Adobe Experience Platform aan uw bestemmingsplatforms verder te onderzoeken. Transformeer uw onbewerkte gegevens in nieuwe inzichten die kunnen worden gebruikt door het bestaande Real-Time CDP-gegevensmodel SQL als inspiratie te gebruiken voor het maken van query&#39;s voor uw unieke bedrijfsbehoeften.

Zie de [ documentatie van de Mening SQL ](../view-sql.md) voor meer informatie over hoe te om SQL van uw inzichten direct door PLatform UI aan te passen.

De volgende inzichten zijn allen beschikbaar voor u als deel van het [ dashboard van Doelen ](../guides/destinations.md) of een douane [ user-defined dashboard ](../standard-dashboards.md) te gebruiken. Zie het [ aanpassingsoverzicht ](../customize/overview.md) voor instructies op hoe te om uw dashboard aan te passen of [ creeer en geef nieuwe widgets ](../customize/custom-widgets.md) in de widgetbibliotheek en [ user-defined dashboard ](../standard-dashboards.md#create-widget) uit.

## Geactiveerd publiek {#activated-audiences}

Vragen beantwoord door dit inzicht:

- Wat is het totale aantal actieve doelgroepen dat door een bepaalde bestemming wordt gefilterd?
- Wat is de geactiveerde publiekstelling door elke bestemming?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT
  COUNT(segment_id) AS Activated_Audiences_Count
FROM
  qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE
  (
    SELECT
      MAX(process_date)
    FROM
      qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE
      process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
  ) BETWEEN start_date AND end_date
  AND destination_id = 1458738325;
```

+++

Zie de [ Geactiveerde documentatie van publiek widget ](../guides/destinations.md#activated-audiences) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Geactiveerd publiek voor alle bestemmingen {#activated-audiences-across-all-destinations}

Vragen beantwoord door dit inzicht:

- Hoeveel soorten publiek worden op alle bestemmingen geactiveerd?
- Wat is het totale aantal actieve doelgroepen?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT count(segment_id) AS Activated_Audiences_Count
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE
    (SELECT MAX(process_date)
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL' ) BETWEEN start_date AND end_date;
```

+++

Zie het [ Geactiveerde publiek over alle documentatie van bestemmingen widget ](../guides/destinations.md#activated-audiences-across-all-destinations) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Actieve bestemmingen door bestemmingsplatform {#active-destinations-by-destination-platform}

Vragen beantwoord door dit inzicht:

- Hoeveel bestemmingen zijn actief?
- Wat is de uitsplitsing van actieve bestemmingen per bestemmingsplatform?
- Wat is de telling van actieve bestemmingen die door elk bestemmingsplatform worden verdeeld?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT destination_platform_name AS Destination_Platform_Name,
       COUNT(destination_id) AS Active_Destinations_Count
  FROM qsaccel.profile_agg.adwh_dim_destination a
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination_platform b ON a.destination_platform_id = b.destination_platform_id
  WHERE destination_status='enabled'
  GROUP BY destination_platform_name
  ORDER BY Active_Destinations_Count DESC
  LIMIT 20;
```

+++

Zie de [ Actieve bestemmingen door de documentatie van de widget van het bestemmingsplatform ](../guides/destinations.md#active-destinations-by-destination-platform) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Ontwikkeling van de omvang van het publiek {#audience-size-trend}

Vragen beantwoord door dit inzicht:

- Hoe is de publieksgrootte veranderd in tijd, met inbegrip van anomalieën voor een publiek dat aan een bestemming in kaart wordt gebracht?
- Hoe vind ik de algemene trend in publieksgrootte, door bestemming, over de gespecificeerde periodes van 30 dagen, 90 dagen, en 12 maanden?
- Wat zijn de belangrijkste kenmerken van het publiek dat tot de grootte bijdraagt, bijvoorbeeld, spikes betreffende om het even welke e-mailmarketing campagnes?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT d.destination_name,
        d.destination,
        d.destination_id,
        b.segment_name,
        b.segment,
        c.segment_id,
        a.date_key,
        sum(a.count_of_profiles) AS profile_count
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations c ON a.segment_id = c.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination d ON c.destination_id = d.destination_id
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) f ON a.merge_policy_id = f.merge_policy_id
  WHERE a.date_key >= dateadd(DAY, -30-1, f.last_process_date)
    AND d.destination_id = -1275507046
    AND c.segment_id = -1452100519
  GROUP BY d.destination_name,
          d.destination,
          d.destination_id,
          b.segment_name,
          b.segment,
          c.segment_id,
          a.date_key;
```

+++

Zie de [ documentatie van de de groottewidget van de Grootte van het Publiek ](../guides/destinations.md#audience-size-trend) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Algemeen publiek {#common-audiences}

Vragen beantwoord door dit inzicht:

- Welk publiek zijn de verschillende bestemmingen gemeenschappelijk?
- Hoeveel profielen hebben elk van de gemeenschappelijke doelgroepen tussen twee verschillende bestemmingen?
- Welk is het grootste publiek waaraan twee bestemmingen in kaart worden gebracht?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT k.destination_name1,
       k.destination_1,
       k.destination_id1,
       k.destination_name2,
       k.destination_2,
       k.destination_id2,
       b.segment_name,
       b.segment,
       b.segment_id,
       sum(a.count_of_profiles) AS profile_count
  FROM
    (SELECT i.destination_name AS destination_name1,
            i.destination AS destination_1,
            i.destination_id AS destination_id1,
            j.destination_name AS destination_name2,
            j.destination AS destination_2,
            j.destination_id AS destination_id2,
            i.segment_id
     FROM
       (SELECT b.destination_name,
               b.destination,
               b.destination_id,
               a.segment_id
        FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
        INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id=b.destination_id
        WHERE b.destination_id=1458738325) AS i
     INNER JOIN
       (SELECT b.destination_name,
               b.destination,
               b.destination_id,
               a.segment_id
        FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
        INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id=b.destination_id
        WHERE b.destination_id=-635802802) AS j ON i.segment_id=j.segment_id) AS k
  INNER JOIN qsaccel.profile_agg.adwh_fact_profile_by_segment a ON a.segment_id = k.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON b.segment_id = k.segment_id
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL'
     GROUP BY merge_policy_id) c ON a.merge_policy_id = c.merge_policy_id
  WHERE a.date_key = c.last_process_date
  GROUP BY k.destination_name1,
           k.destination_1,
           k.destination_id1,
           k.destination_name2,
           k.destination_2,
           k.destination_id2,
           b.segment_name,
           b.segment,
           b.segment_id
  ORDER BY profile_count DESC
  LIMIT 20;
```

+++

Zie de [ Gemeenschappelijke documentatie van publiek widget ](../guides/destinations.md#common-audiences) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Status van bestemming {#destination-status}

Vragen beantwoord door dit inzicht:

- Wat is het totale aantal bestemmingen toegelaten voor gebruik?
- Wat is het totale aantal gehandicapte bestemmingen?
- Wat is het percentage verdeeld tussen toegelaten en gehandicapte bestemmingen?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT COUNT(CASE
                 WHEN destination_status='enabled' THEN 1
             END) AS count_of_active_destinations,
       COUNT(CASE
                 WHEN destination_status='disabled' THEN 1
             END) AS count_of_inactive_destinations
FROM qsaccel.profile_agg.adwh_dim_destination;
```

+++

Zie de [ documentatie van de statuswidget van de Bestemming ](../guides/destinations.md#destination-status) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Aantal doelen {#destinations-count}

Vragen beantwoord door dit inzicht:

- Hoeveel bestemmingen zijn momenteel gevormd?
- Hoe is het totale aantal bestemmingen in de loop der tijd veranderd?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT count(destination_id) AS total_number_of_destinations
  FROM qsaccel.profile_agg.adwh_dim_destination;
```

+++

Zie de [ documentatie van de de tellingswidget van Doelen ](../guides/destinations.md#destinations-count) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Gewijzigde volksgezondheid {#mapped-audience-health}

Vragen beantwoord door dit inzicht:

- Welk publiek dat aan een bestemming in kaart wordt gebracht heeft significante variaties in de laatste 30 dagen?
- Wat is de laatste grootte van een in kaart gebracht publiek en of het de afgelopen maand is veranderd?
- Hoe maak ik een lijst van alle publiek dat aan een bestemming wordt toegewezen die op de strengheid van hun grootteveranderingen in de afgelopen maand wordt gebaseerd?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT destination_name,
        SEGMENT,
        segment_id,
        segment_name,
        avg_profile_count,
        latest_profile_count,
        stddev_profile_count,
        profile_count_z_factor
  FROM
    (SELECT b.destination_name,
            f.segment_id,
            c.segment_name,
            c.segment,
            f.avg_profile_count,
            f.latest_profile_count,
            f.stddev_profile_count,
            CASE
                WHEN stddev_profile_count = 0 THEN 0 ELSE(f.latest_profile_count - f.avg_profile_count)/f.stddev_profile_count
            END AS profile_count_z_factor
    FROM
      (SELECT segment_id,
              avg(profile_count) AS avg_profile_count,
              sum(CASE
                      WHEN last_process_date = date_key THEN profile_count
                      ELSE 0
                  END) AS latest_profile_count,
              stdevp(profile_count) AS stddev_profile_count
        FROM
          (SELECT x.date_key,
                  x.segment_id,
                  d.last_process_date,
                  sum(x.count_of_profiles) AS profile_count
          FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
          INNER JOIN
            (SELECT MAX(process_date) last_process_date,
                    merge_policy_id
              FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
              WHERE process_name = 'FACT_TABLES_PROCESSING'
                AND process_status = 'SUCCESSFUL'
              GROUP BY merge_policy_id) d ON x.merge_policy_id = d.merge_policy_id
          WHERE x.date_key >= dateadd (DAY, -30, d.last_process_date)
          GROUP BY x.date_key,
                    x.segment_id,
                    d.last_process_date) AS t
        GROUP BY segment_id) AS f
    INNER JOIN qsaccel.profile_agg.adwh_dim_segments c ON f.segment_id = c.segment_id
    INNER JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations a ON a.segment_id = c.segment_id
    INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id = b.destination_id
    WHERE b.destination_id = 1458738325) AS m
  WHERE abs(m.profile_count_z_factor) >= 1
  ORDER BY m.latest_profile_count DESC
  LIMIT 20;
```

+++

Zie de [ In kaart gebrachte documentatie van de publieksgezondheid widget ](../guides/destinations.md#mapped-audience-health) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Toegewezen publiek {#mapped-audiences}

Vragen beantwoord door dit inzicht:

- Hoeveel publiek wordt toegewezen aan een bepaalde bestemming?
- Hoe is het aantal toegewezen doelgroepen in de loop der tijd veranderd?
- Waar kan ik twee bestemmingen vergelijken om het publiek te zien overlappen in kaart gebracht aan elke bestemming?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT COUNT(segment_id) AS mapped_audiences_count
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE destination_id = 1458738325;
```

+++

Zie de [ In kaart gebrachte documentatie van publiek widget ](../guides/destinations.md#mapped-audiences) voor informatie over de verschijning en de functionaliteit van dit inzicht.

<!-- Commented out until the Jan release as the SQL IS MISSING:
## Mapped audiences by identity {#mapped-audiences-by-identity}

Questions answered by this insight:

- How do I find a list of audiences that are mapped to a destination?
- What is the count of identities for audiences mapped to a destination?
- Which audiences have the highest count of identities mapped to a particular destination?

+++Select to reveal the SQL that generates this insight

```sql
```

+++

See the [Mapped audiences by identity widget documentation](../guides/destinations.md#mapped-audiences-by-identity) for information on the appearance and functionality of this insight.
-->

## Meest gebruikte bestemmingen {#most-used-destinations}

Vragen beantwoord door dit inzicht:

- Wat zijn de meest gebruikte bestemmingen?
- Hoeveel publiek worden in kaart gebracht aan elke bestemming, die door het meest aan het minst wordt gesorteerd?
- Hoe verandert het in kaart brengen van publiek aan bestemmingen van één momentopname in een andere?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT qsaccel.profile_agg.adwh_dim_destination.destination_name,
       qsaccel.profile_agg.adwh_dim_destination.destination_id,
       qsaccel.profile_agg.adwh_dim_destination.destination,
       count(DISTINCT qsaccel.profile_agg.adwh_dim_br_segment_destinations.segment_id) segment_count
  FROM qsaccel.profile_agg.adwh_dim_destination
  JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations ON qsaccel.profile_agg.adwh_dim_destination.destination_id = qsaccel.profile_agg.adwh_dim_br_segment_destinations.destination_id
  WHERE qsaccel.profile_agg.adwh_dim_destination.destination_name IS NOT NULL
  GROUP BY qsaccel.profile_agg.adwh_dim_destination.destination_name,
           qsaccel.profile_agg.adwh_dim_destination.destination,
           qsaccel.profile_agg.adwh_dim_destination.destination_id
  ORDER BY segment_count DESC
  LIMIT 20;
```

+++

Zie de [ Meest gebruikte documentatie van bestemmingen widget ](../guides/destinations.md#most-used-destinations) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Onlangs geactiveerd publiek {#recently-activated-audiences}

Vragen beantwoord door dit inzicht:

- Aan welk doel is een publiek geactiveerd dat het laatst is geactiveerd?
- Hoe vind ik een lijst van alle bestemmingen die door de laatste bijgewerkte datum worden gesorteerd?
- Hoe kan ik twee bestemmingen vergelijken die op de meest recente activeringen worden gebaseerd?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT
  segment_name,
  segment,
  destination_name,
  a.create_time create_time
FROM
  qsaccel.profile_agg.adwh_dim_br_segment_destinations a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id = c.destination_id
ORDER BY
  create_time DESC,
  segment
LIMIT
  20;
```

+++

Zie de [ onlangs geactiveerde documentatie van publiek widget ](../guides/destinations.md#recently-activated-audiences) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Onlangs geactiveerd publiek naar bestemming {#recently-activated-audiences-by-destination}

Vragen beantwoord door dit inzicht:

- Wat wordt het publiek geactiveerd voor een bepaalde bestemming?
- Hoe vind ik een lijst van publiek geactiveerd door een bepaald publiek van het meest tot het minst recent?
- Hoe vind ik een lijst van publiek tegen de datum het voor een specifieke bestemming werd geactiveerd?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT c.destination_name,
       c.destination,
       c.destination_id,
       b.segment_name,
       b.segment,
       b.segment_id,
       a.create_time activated
  FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id=b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id=c.destination_id
  WHERE c.destination_id=-1275507046
  ORDER BY a.create_time DESC,
           a.segment_id
  LIMIT 20;
```

+++

Zie het [ onlangs geactiveerde publiek door de documentatie van bestemmingswidget ](../guides/destinations.md#recently-activated-audiences-by-destination) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Onlangs gemaakte doelen {#recently-created-destinations}

Vragen beantwoord door dit inzicht:

- Welke zijn de onlangs gecreeerde bestemmingen?
- Hoe vind ik een lijst van bestemmingen met de datum zij werden gecreeerd?
- Welke nieuwe bestemming werd onlangs gecreeerd?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT DISTINCT
  destination,
  destination_name,
  create_time
FROM
  qsaccel.profile_agg.adwh_dim_destination
WHERE
  destination_status = 'enabled'
ORDER BY
  create_time DESC
LIMIT
  20;
```

+++

Zie de [ onlangs gecreeerde documentatie van de bestemmingswidget ](../guides/destinations.md#recently-created-destinations) voor informatie over de verschijning en de functionaliteit van dit inzicht.

<!-- Commented out until the Jan release as SQL MISSING FROM WIKI:

## Unmapped audiences by identity {#unmapped-audiences-by-identity}

Questions answered by this insight:

- How do I find a list of audiences that are not mapped to a destination?
- What is the count of identities for audiences that are not mapped to a destination?
- Which audiences have the highest count of identities not mapped to a particular destination?

+++Select to reveal the SQL that generates this insight

```sql
```

+++

See the [Unmapped audiences by identity widget documentation](../guides/destinations.md#unmapped-audiences-by-identity) for information on the appearance and functionality of this insight.

-->

## Volgende stappen {#next-steps}

Door dit document te lezen, begrijpt u nu de SQL die dashboardinzichten produceert en welke gemeenschappelijke vragen deze analyse oplost. U kunt deze SQL-query&#39;s nu bewerken en doorlopen om uw eigen inzichten te genereren.

Zie de [ documentatie van de Mening SQL ](../view-sql.md) voor meer informatie over hoe te om SQL van uw inzichten direct door PLatform UI aan te passen.

U kunt SQL ook lezen en begrijpen die inzichten voor [ Profielen ](./profiles.md), [ Profielen van de Rekening ](./account-profiles.md) en [ Publiek ](./audiences.md) dashboards produceert.
