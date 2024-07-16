---
title: Soorten kijkers
description: Ontdek SQL die uw publiek inzicht en gebruik deze vragen aanstuurt om douaneinzichten te produceren om publieksgegevens van Adobe Experience Platform verder te onderzoeken.
exl-id: 99624234-c4e1-44bb-9567-505bc0c4723e
source-git-commit: 34eb9151cc6bb8551553b0a8427e58871acb4dbb
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 0%

---

# Inzichten van soorten publiek

De inzichten die zijn afgeleid van de analyse van uw gegevensmodel maken uw Adobe Real-time Customer Data Platform-gegevens toegankelijker, begrijpelijker en effectiever voor de besluitvorming.

Begrijp uw publieksinzichten door tot SQL toegang te hebben die hen macht, dan uw eigen inzichten produceert om de identiteiten en de profielen verder te onderzoeken die uw publiek maken. Transformeer uw onbewerkte gegevens in nieuwe inzichten die kunnen worden gebruikt door het bestaande Real-Time CDP-gegevensmodel SQL als inspiratie te gebruiken voor het maken van query&#39;s voor uw unieke bedrijfsbehoeften.

Zie de [ documentatie van de Mening SQL ](../view-sql.md) voor meer informatie over hoe te om SQL van uw inzichten direct door PLatform UI aan te passen.

De volgende inzichten zijn allen beschikbaar voor u om als deel van het [ dashboard van Soorten Soorten publiek ](../guides/audiences.md) of een douane [ user-defined dashboard ](../user-defined-dashboards.md) te gebruiken. Zie het [ aanpassingsoverzicht ](../customize/overview.md) voor instructies op hoe te om uw dashboard aan te passen of [ creeer en geef nieuwe widgets ](../customize/custom-widgets.md) in de widgetbibliotheek en [ user-defined dashboard ](../user-defined-dashboards.md#create-widget) uit.

De volgende inzichten zijn allen beschikbaar voor u om als deel van het [ dashboard van Soorten Soorten publiek ](../guides/audiences.md) of een douanedashboard te gebruiken.

## Rapport publiek overlappen {#audience-overlap-report}

Vragen beantwoord door dit inzicht:

- Wat zijn de hoogste 50 overlappende doelgroepen van een bepaald gefilterd publiek?
- Wat zijn het 50 minst overlappende publiek van een bepaald gefilterd publiek?
- Hoe verandert het overlappende patroon voor een verschillend gefilterd publiek?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT source_segment_name,
        source_segment_id,
        overlap_segment_name,
        overlap_segment_id,
        max(source_segment_audience_count) source_segment_audience_count,
        max(overlap_segment_audience_count) overlap_segment_audience_count,
        max(overlap_audience_count) overlap_audience_count,
        CASE
            WHEN (max(source_segment_audience_count) + max(overlap_segment_audience_count) - max(overlap_audience_count)) > 0 THEN (cast(max(overlap_audience_count) AS DECIMAL(18, 2)) / cast((max(source_segment_audience_count) + max(overlap_segment_audience_count) - max(overlap_audience_count)) AS DECIMAL(18, 2))) * 100::DECIMAL(9, 2)
            ELSE 100.00
        END overlapping_percentage
  FROM
    (SELECT adwh_fact_profile_overlap_of_segments.Segment1 source_segment_id,
            adwh_fact_profile_overlap_of_segments.Segment2 overlap_segment_id,
            Sum(count_of_overlap) overlap_audience_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.date_key = '2024-01-10'
    GROUP BY qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.Segment2 ,
              qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.Segment1) a
  INNER JOIN
    (SELECT sum(count_of_profiles) source_segment_audience_count,
            adwh_dim_segments.segment_name source_segment_name,
            adwh_fact_profile_by_segment_trendlines.merge_policy_id,
            adwh_fact_profile_by_segment_trendlines.segment_Id segment1
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_dim_segments.segment_id = qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
    GROUP BY qsaccel.profile_agg.adwh_dim_segments.segment_name,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id) b ON a.source_segment_id = b.segment1
  INNER JOIN
    (SELECT sum(count_of_profiles) overlap_segment_audience_count,
            adwh_dim_segments.segment_name overlap_segment_name,
            adwh_fact_profile_by_segment_trendlines.merge_policy_id,
            adwh_fact_profile_by_segment_trendlines.segment_Id segment2
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_segments ON adwh_dim_segments.segment_id = adwh_fact_profile_by_segment_trendlines.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
    GROUP BY qsaccel.profile_agg.adwh_dim_segments.segment_name,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id) c ON a.overlap_segment_id = c.segment2
  GROUP BY source_segment_name,
          source_segment_id,
          overlap_segment_name,
          overlap_segment_id
  ORDER BY overlapping_percentage DESC
  LIMIT 5;
```

+++

Zie het [ publiek overlappen rapport widget documentatie ](../guides/audiences.md#audience-overlap-report) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Audioverlap {#audience-overlap}

Vragen beantwoord door dit inzicht:

- Welke profielen gelden voor beide doelgroepen?
- Hoe beïnvloedt de overlapping de betrokkenheid of de omrekeningskoersen?
- Hoe kunnen marketingstrategieën worden afgestemd op het overlappende segment?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT Sum(overlap_col1) overlap_col1,
        Sum(overlap_col2) overlap_col2,
        Sum(overlap_count) Overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            sum(count_of_overlap)Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.merge_policy_id = 1133248113
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.date_key = '2024-01-10'
      AND ((qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment1=1870062812
            AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment2=2080256533)
            OR (qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment1=2080256533
                AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment2=1870062812))
    UNION ALL SELECT sum(count_of_profiles) overlap_col1,
                      0 overlap_col2,
                      0 overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    LEFT JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id = qsaccel.profile_agg.adwh_dim_segments.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 1133248113
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_segments.segment_Id = 1870062812
    UNION ALL SELECT 0 overlap_col1,
                      sum(count_of_profiles) overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id = qsaccel.profile_agg.adwh_dim_segments.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 1133248113
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_segments.segment_Id = 2080256533 ) a;
```

+++

Zie het [ publiek overlappen widget documentatie ](../guides/audiences.md#audience-overlap) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Ontwikkeling van de omvang van het publiek {#audience-size-change-trend}

Vragen beantwoord door dit inzicht:

- Zijn er significante pieken of dalingen in publieksgrootte binnen de laatste 30 dagen, 90 dagen, of 12 maanden?
- Hoe verandert de omvang van het publiek tijdens specifieke dagen?
- Zijn er in de afgelopen twaalf maanden anomalieën of herhalingspatronen van pieken of dipsen vastgesteld?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT date_key,
      Profiles_added
  FROM
    (SELECT rn_num,
            date_key,
            (count_of_profiles-lag(count_of_profiles, 1, 0) over(
                                                                ORDER BY date_key))Profiles_added
    FROM
      (SELECT date_key,
              sum(x.count_of_profiles)count_of_profiles,
              row_number() OVER (
                                  ORDER BY date_key) rn_num
        FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
        INNER JOIN
          (SELECT MAX(process_date) last_process_date,
                  merge_policy_id
          FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
          WHERE process_name = 'FACT_TABLES_PROCESSING'
            AND process_status = 'SUCCESSFUL'
          GROUP BY merge_policy_id) y ON x.merge_policy_id = y.merge_policy_id
        WHERE segment_id = 1333234510
          AND x.date_key >= dateadd(DAY, -30 -1, y.last_process_date)
        GROUP BY x.date_key) a)b
  WHERE rn_num > 1;
```

+++

Zie de [ documentatie van de de veranderingstrend van de grootte van het publiek ](../guides/audiences.md#audience-size-change-trend) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Ontwikkeling van de omvang van het publiek naar identiteit {#audience-size-trend-by-identity}

Vragen beantwoord door dit inzicht:

- Steunt mijn publiek constant, stabiliseert, of ervaart fluctuaties?
- Is er een specifieke identiteit die pieken of dalingen in publieksgroei in tijd heeft?
- Zijn er in de loop der tijd anomalieën in mijn identiteitsgroei?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT sum(count_of_profiles) AS identities,
        date_key
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines x
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) y ON x.merge_policy_id = y.merge_policy_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_namespaces z ON x.namespace_id = z.namespace_id
  AND x.merge_policy_id = z.merge_policy_id
  WHERE x.date_key >= dateadd(DAY, -30, y.last_process_date)
    AND x.segment_id = 1333234510
    AND z.namespace_description = 'crmid'
  GROUP BY date_key;
```

+++

Zie de [ trend van de grootte van het publiek door de documentatie van de identiteitswidget ](../guides/audiences.md#audience-size-trend-by-identity) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Ontwikkeling van de omvang van het publiek {#audience-size-trend}

Vragen beantwoord door dit inzicht:

- Hoe is de omvang van het publiek in de loop der tijd veranderd, inclusief eventuele anomalieën?
- Hoe kan ik de algemene trend in de omvang van het publiek over de perioden vinden: 30 dagen, 90 dagen en 12 maanden?
- Wat zijn de belangrijkste kenmerken van het publiek die tot zijn grootte bijdragen? Dit is bijvoorbeeld het gevolg van marketingcampagnes via e-mail.

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT date_key,
        sum(count_of_profiles) AS audience_size
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) y ON x.merge_policy_id = y.merge_policy_id
  WHERE date_key >= dateadd(DAY, -30, y.last_process_date)
    AND x.segment_id = 1333234510
  GROUP BY date_key,
          segment_id;
```

+++

Zie de [ documentatie van de de groottewidget van de Grootte van het Publiek ](../guides/audiences.md#audience-size-trend) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Grootte publiek {#audience-size}

Vragen beantwoord door dit inzicht:

- Wat is de huidige totale publieksgrootte?
- Hoe verhoudt de huidige publieksgrootte zich tot eerdere periodes of specifieke doelgroepen?
- Wat is het effect van recente marketingcampagnes op de omvang van het publiek?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT
  sum(
    qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.count_of_profiles
  ) count_of_profiles
FROM
  qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id = qsaccel.profile_agg.adwh_dim_segments.segment_id
WHERE
  qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id = -1323307941
  AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 1914917902
  AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-12';
```

+++

Zie de [ documentatie van de de groottewidget van de Audience ](../guides/audiences.md#audience-size) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## AI-distributie van scores door klant {#customer-ai-distribution-of-scores}

Vragen beantwoord door dit inzicht:

- Wat is de scoreverdeling voor elk emmertje van mijn AI-model van de Klant, gefilterd door een geselecteerd publiek?
- Wat is de scoreverdeling van hoog, gemiddeld en laag voor een bepaald publiek?
- Wat is de verdeling van de scores over de verschillende belangengroepen?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT b.model_name,
      b.model_type,
      c.segment_name,
      c.segment_id,
      CASE
        WHEN score >= 0
          AND score < 25 THEN 'LOW'
        WHEN score >= 25
          AND score < 75 THEN 'MEDIUM'
        WHEN score >= 75
          AND score <= 100 THEN 'HIGH'
        END bucket_name,
      CASE
        WHEN score >= 0
          AND score < 5 THEN '02.50'
        WHEN score >= 5
          AND score < 10 THEN '07.50'
        WHEN score >= 10
          AND score < 15 THEN '12.50'
        WHEN score >= 15
          AND score < 20 THEN '17.50'
        WHEN score >= 20
          AND score < 25 THEN '22.50'
        WHEN score >= 25
          AND score < 30 THEN '27.50'
        WHEN score >= 30
          AND score < 35 THEN '32.50'
        WHEN score >= 35
          AND score < 40 THEN '37.50'
        WHEN score >= 40
          AND score < 45 THEN '42.50'
        WHEN score >= 45
          AND score < 50 THEN '47.50'
        WHEN score >= 50
          AND score < 55 THEN '52.50'
        WHEN score >= 55
          AND score < 60 THEN '57.50'
        WHEN score >= 60
          AND score < 65 THEN '62.50'
        WHEN score >= 65
          AND score < 70 THEN '67.50'
        WHEN score >= 70
          AND score < 75 THEN '72.50'
        WHEN score >= 75
          AND score < 80 THEN '77.50'
        WHEN score >= 80
          AND score < 85 THEN '82.50'
        WHEN score >= 85
          AND score < 90 THEN '87.50'
        WHEN score >= 90
          AND score < 95 THEN '92.50'
        WHEN score >= 95
          AND score <= 100 THEN '97.50'
        END score_bins,
      Sum(CASE
            WHEN score >= 0
              AND score < 25 THEN count_of_profiles
            WHEN score >= 25
              AND score < 75 THEN count_of_profiles
            WHEN score >= 75
              AND score <= 100 THEN count_of_profiles
        END) count_of_profiles
   FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_ai_models a
          JOIN qsaccel.profile_agg.adwh_dim_ai_models b ON a.merge_policy_id = b.merge_policy_id
     AND a.model_id = b.model_id
          JOIN qsaccel.profile_agg.adwh_dim_segments c ON a.segment_id = c.segment_id
   WHERE a.merge_policy_id = 1133248113
     AND a.model_id = 1829081696
     AND a.segment_id = 1870062812
     AND score_date =
         (SELECT MAX(score_date)
          FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_ai_models d
          WHERE d.model_id = a.model_id) GROUP  BY b.model_name,
             b.model_type,
             c.segment_name,
             c.segment_id,
             CASE
               WHEN score >= 0
                 AND score < 25 THEN 'LOW'
               WHEN score >= 25
                 AND score < 75 THEN 'MEDIUM'
               WHEN score >= 75
                 AND score <= 100 THEN 'HIGH'
               END,
             CASE
               WHEN score >= 0
                 AND score < 5 THEN '02.50'
               WHEN score >= 5
                 AND score < 10 THEN '07.50'
               WHEN score >= 10
                 AND score < 15 THEN '12.50'
               WHEN score >= 15
                 AND score < 20 THEN '17.50'
               WHEN score >= 20
                 AND score < 25 THEN '22.50'
               WHEN score >= 25
                 AND score < 30 THEN '27.50'
               WHEN score >= 30
                 AND score < 35 THEN '32.50'
               WHEN score >= 35
                 AND score < 40 THEN '37.50'
               WHEN score >= 40
                 AND score < 45 THEN '42.50'
               WHEN score >= 45
                 AND score < 50 THEN '47.50'
               WHEN score >= 50
                 AND score < 55 THEN '52.50'
               WHEN score >= 55
                 AND score < 60 THEN '57.50'
               WHEN score >= 60
                 AND score < 65 THEN '62.50'
               WHEN score >= 65
                 AND score < 70 THEN '67.50'
               WHEN score >= 70
                 AND score < 75 THEN '72.50'
               WHEN score >= 75
                 AND score < 80 THEN '77.50'
               WHEN score >= 80
                 AND score < 85 THEN '82.50'
               WHEN score >= 85
                 AND score < 90 THEN '87.50'
               WHEN score >= 90
                 AND score < 95 THEN '92.50'
               WHEN score >= 95
                 AND score <= 100 THEN '97.50'
               END;
```

+++

Zie de [ AI distributie van de Klant van de documentatie van de scores widget ](../guides/audiences.md#customer-ai-distribution-of-scores) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Overzicht van AI-scores van klant {#customer-ai-scoring-summary}

Vragen beantwoord door dit inzicht:

- Wat is het scoresamenvatting voor elk van mijn AI-modellen van de Klant voor een bepaald publiek?
- Hoe veranderen mijn AI-proENTIECores van mijn klant voor verschillende soorten publiek?
- Hoe vergelijk mijn het scoren samenvatting met andere KPIs in het publieksoverzicht?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT model_name,
         model_type,
         segment_name,
         CASE
             WHEN score BETWEEN 0 AND 24 THEN 'LOW'
             WHEN score BETWEEN 25 AND 74 THEN 'MEDIUM'
             WHEN score BETWEEN 75 AND 100 THEN 'HIGH'
         END score_buckets,
         sum(count_of_profiles) count_of_profiles
  FROM QSAccel.profile_agg.adwh_fact_profile_by_segment_ai_models a
  JOIN QSAccel.profile_agg.adwh_dim_ai_models b ON a.merge_policy_id=b.merge_policy_id
  AND a.model_id=b.model_id
  JOIN QSAccel.profile_agg.adwh_dim_segments c ON a.segment_id=c.segment_id
  WHERE a.merge_policy_id=1133248113
    AND a.model_id =1829081696
    AND a.segment_id=1870062812
    AND score_date=
      (SELECT max(score_date)
       FROM QSAccel.profile_agg.adwh_fact_profile_by_segment_ai_models d
       WHERE d.model_id=a.model_id)
  GROUP BY model_name,
           model_type,
           segment_name,
           CASE
               WHEN score BETWEEN 0 AND 24 THEN 'LOW'
               WHEN score BETWEEN 25 AND 74 THEN 'MEDIUM'
               WHEN score BETWEEN 75 AND 100 THEN 'HIGH'
           END;
```

+++

Zie de [ AI van de Klant die summiere widget documentatie ](../guides/audiences.md#customer-ai-scoring-summary) voor informatie over de verschijning en de functionaliteit van dit inzicht scoren.

## Identiteitsoverlapping {#identity-overlap}

Vragen beantwoord door dit inzicht:

- Wat is het algemene snijpunt tussen [!UICONTROL Identity Type A] en [!UICONTROL Identity Type B] voor een gefilterd publiek?
- Hoe verfijn ik klantenpubliek dat op de overlapping van specifieke identiteitstypes wordt gebaseerd, om de gerichte marketing strategieën te verbeteren?
- Welke inzichten kunnen worden verkregen bij de evaluatie van de prestaties van de campagne op de elkaar kruisende gebieden?
- Op basis van deze inzichten, hoe kunnen toekomstige marketinginspanningen worden geoptimaliseerd?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT Sum(overlap_col1) overlap_col1,
        Sum(overlap_col2) overlap_col2,
        Sum(overlap_count) Overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            Sum(count_of_profiles) Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.segment_id = 1333234510
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.merge_policy_id = 1709997014
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.overlap_id IN
        (SELECT a.overlap_id
          FROM
            (SELECT qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id overlap_id,
                    count(*) cnt_num
            FROM qsaccel.profile_agg.adwh_dim_overlap_namespaces
            WHERE qsaccel.profile_agg.adwh_dim_overlap_namespaces.merge_policy_id = 1709997014
              AND qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_namespaces in ('crmid',
                                                                                          'email')
            GROUP BY qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id)a
          WHERE a.cnt_num>1 )
    UNION ALL SELECT count_of_profiles overlap_col1,
                      0 overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines
    LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'crmid'
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.segment_id = 1333234510
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = 1709997014
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.date_key = '2024-01-10'
    UNION ALL SELECT 0 overlap_col1,
                      count_of_profiles overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines
    LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'email'
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.segment_id = 1333234510
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = 1709997014
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.date_key = '2024-01-10' ) a;
```

+++

Zie de [ documentatie van de overlap van de Identiteit ](../guides/audiences.md#identity-overlap) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Profielen op identiteit {#profiles-by-identity}

Vragen beantwoord door dit inzicht:

- Welk identiteitstype heeft het hoogste aandeel binnen het totale aantal profielen voor een geselecteerd publiek?
- Zijn er aanzienlijke verschillen tussen de identiteitstypen voor een geselecteerd publiek?
- Wat is de algemene verdeling van identiteitstypen per publiek?
- Zijn er voor verschillende doelgroepen aanzienlijke verschillen of anomalieën in het aantal identiteitsbewijzen?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.count_of_profiles) count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
  AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.segment_id = 1333234510
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = 1709997014
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.date_key = '2024-01-10'
  GROUP BY qsaccel.profile_agg.adwh_dim_namespaces.namespace_description
  ORDER BY count_of_profiles DESC;
```

+++

Zie [ Profielen door de documentatie van de identiteitswidget ](../guides/audiences.md#profiles-by-identity) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Geplande activeringen {#scheduled-activations}

Vragen beantwoord door dit inzicht:

- Wat zijn de begin- en einddatum van de best presterende activeringen voor een bepaald publiek op een specifiek platform?
- Welke platforms werden het meest gebruikt voor geplande activeringen van een bepaald publiek?
- Zijn er patronen in platformgebruik die besluiten bij het voorrang geven aan of het diversifiëren van activeringsstrategieën voor een specifiek publiek zouden kunnen begeleiden?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT p.destination_platform ,
       p.destination_platform_name AS platform ,
       d.destination_name ,
       d.destination ,
       br.start_date ,
       CASE
           WHEN br.end_date = '9999-12-31' THEN 'Ongoing'
           ELSE br.end_date
       END AS end_date
  FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations br
  JOIN qsaccel.profile_agg.adwh_dim_destination d ON br.destination_id = d.destination_id
  JOIN qsaccel.profile_agg.adwh_dim_destination_platform p ON d.destination_platform_id = p.destination_platform_id
  JOIN
    (SELECT MAX(process_date) AS last_process_date
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL' ) lpd ON lpd.last_process_date BETWEEN br.start_date AND br.end_date
  AND br.segment_id = 1333234510;
```

+++

Zie de [ Geplande documentatie van de activeringswidget ](../guides/audiences.md#scheduled-activations) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Volgende stappen

Door dit document te lezen, begrijpt u nu de SQL die dashboardinzichten produceert en welke gemeenschappelijke vragen deze analyse oplost. U kunt nu de SQL bewerken en doorlopen om uw eigen inzichten te genereren.

Zie de [ documentatie van de Mening SQL ](../view-sql.md) voor meer informatie over hoe te om SQL van uw inzichten direct door PLatform UI aan te passen.

U kunt SQL ook lezen en begrijpen die inzichten voor [ Profielen ](./profiles.md), [ Profielen van de Rekening ](./account-profiles.md) en [ Doelen ](./destinations.md) dashboards van Doelen {produceert.
