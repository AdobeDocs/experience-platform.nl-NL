---
title: Profielinzichten
description: Ontdek SQL dat uw profielinzichten en gebruik deze vragen aandrijft om douaneinzichten te produceren die uw klanten en hun ervaringen van de consument verder onderzoeken.
exl-id: f3792076-3e01-4e26-8788-32927202a2e5
source-git-commit: 34eb9151cc6bb8551553b0a8427e58871acb4dbb
workflow-type: tm+mt
source-wordcount: '1655'
ht-degree: 0%

---

# Profielinzichten

De inzichten die zijn afgeleid van de analyse van uw gegevensmodel maken uw Adobe Real-time Customer Data Platform-gegevens toegankelijker, begrijpelijker en effectiever voor de besluitvorming.

Begrijp uw profielinzichten door tot SQL toegang te hebben die hen macht, dan uw eigen inzichten produceert om uw klanten en hun ervaringen van de consument verder te onderzoeken die omhoog uw profielen maken. Transformeer uw onbewerkte gegevens in nieuwe inzichten die kunnen worden gebruikt door het bestaande Real-Time CDP-gegevensmodel SQL als inspiratie te gebruiken voor het maken van query&#39;s voor uw unieke bedrijfsbehoeften.

Zie de [ documentatie van de Mening SQL ](../view-sql.md) voor meer informatie over hoe te om uw inzichten&#39; SQL direct door Platform UI aan te passen.

De volgende inzichten zijn allen beschikbaar voor u als deel van het [ dashboard van Profielen ](../guides/profiles.md) of een douane [ user-defined dashboard ](../user-defined-dashboards.md) te gebruiken. Zie het [ aanpassingsoverzicht ](../customize/overview.md) voor instructies op hoe te om uw dashboard aan te passen of [ creeer en geef nieuwe widgets ](../customize/custom-widgets.md) in de widgetbibliotheek en [ user-defined dashboard ](../user-defined-dashboards.md#create-widget) uit.

## Publiek overlapt door samenvoegbeleid {#audience-overlap-by-merge-policy}

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
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.date_key = '2024-01-10'
      AND ((qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment1=1333234510
            AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment2=1559754729)
            OR (qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment1=1559754729
                AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment2=1333234510))
    UNION ALL SELECT sum(count_of_profiles) overlap_col1,
                      0 overlap_col2,
                      0 overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    LEFT JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id = qsaccel.profile_agg.adwh_dim_segments.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_segments.segment_Id = 1333234510
    UNION ALL SELECT 0 overlap_col1,
                      sum(count_of_profiles) overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id = qsaccel.profile_agg.adwh_dim_segments.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_segments.segment_Id = 1559754729 ) a;
```

+++

Zie de [ overlap van het Publiek door de documentatie van de widget van het fusiebeleid ](../guides/profiles.md#audience-overlap-by-merge-policy) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Rapport publiek overlappen {#audience-overlap-report}

Vragen beantwoord door dit inzicht:

- Wat zijn de 50 meest overlappende doelgroepen?
- Wat is het 50 minst overlappende publiek?
- Hoe verandert het overlappende patroon door samenvoegbeleid?

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

Zie het [ publiek overlappen rapport widget documentatie ](../guides/profiles.md#audience-overlap-report) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Soorten publiek (aantal) {#audiences}

Vragen beantwoord door dit inzicht:

- Welk samenvoegingsbeleid hoofdzakelijk voor segmentatie wordt gebruikt?
- Wat is de verdeling van publiek over fusiebeleid?
- Zijn er significante veranderingen in publieksaantallen voor specifiek samenvoegbeleid in tijd?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT count(DISTINCT a.segment_id) count_of_segments
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines a
  JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) b ON a.merge_policy_id= b.merge_policy_id
  AND a.date_key = b.last_process_date
  WHERE a.merge_policy_id= 2027892989;
```

+++

Zie de [ documentatie van widgets van het publiek ](../guides/profiles.md#audiences) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Soorten publiek toegewezen aan doelstatus {#audiences-mapped-to-destination-status}

Vragen beantwoord door dit inzicht:

- Wat is de algemene verdeling van het publiek tussen toegewezen en niet in kaart gebrachte bestemmingen?
- Welke specifieke bestemmingen hebben het hoogste in kaart gebrachte publiek?
- Welk percentage van het totale publiek blijft onbepaald?
- Zijn er patronen of verwante trends van deze niet-toegewezen doelgroepen?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT COUNT(DISTINCT (y.segment_id)) AS count_mapped_segments,
        COUNT(DISTINCT (x.segment_id)) - COUNT(DISTINCT (y.segment_id)) AS count_unmapped_segments,
        COUNT(DISTINCT (x.segment_id)) AS total_segments
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
  LEFT JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations y ON x.segment_id = y.segment_id
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) z ON x.merge_policy_id = z.merge_policy_id
  AND x.date_key = z.last_process_date
  WHERE x.merge_policy_id = 2027892989;
```

+++

Zie het [ publiek dat aan de documentatie van widget van de bestemmingsstatus ](../guides/profiles.md#audiences-mapped-to-destination-status) voor informatie over de verschijning en de functionaliteit van dit inzicht in kaart wordt gebracht.

## Grootte publiek {#audiences-size}

Vragen beantwoord door dit inzicht:

- Welk publiekssegment heeft de grootste grootte?
- Wat zijn de vijf grootste doelgroepen?
- Hoe verandert de distributie van de publieksgrootte in tijd voor het hoogste publiek?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key,
        qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
        qsaccel.profile_agg.adwh_dim_segments.segment,
        qsaccel.profile_agg.adwh_dim_segments.segment_name,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.count_of_profiles)count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id = qsaccel.profile_agg.adwh_dim_segments.segment_id
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id=adwh_dim_merge_policies.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id= 2027892989
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key,
          qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
          qsaccel.profile_agg.adwh_dim_segments.segment,
          qsaccel.profile_agg.adwh_dim_segments.segment_name
  ORDER BY count_of_profiles DESC
  LIMIT 20;
```

+++

Zie de [ documentatie van de de groottewidget van het publiek ](../guides/profiles.md#audiences-size) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## AI-distributie van scores door klant {#customer-ai-distribution-of-scores}

Vragen beantwoord door dit inzicht:

- Wat is de verdeling van scores over emmers voor elk van mijn AI-modellen van de Klant?
- Wat is de verdeling van scores door hoge, gemiddelde, en lage scores?
- Wat is de verdeling van de scoring per fusiebeleid?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT b.model_name,
     b.model_type,
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
  FROM qsaccel.profile_agg.adwh_fact_profile_ai_models a
  JOIN qsaccel.profile_agg.adwh_dim_ai_models b ON a.merge_policy_id = b.merge_policy_id
  AND a.model_id = b.model_id
  WHERE a.merge_policy_id = 2027892989
    AND a.model_id = 1829081696
    AND score_date =
      (SELECT Max(score_date)
       FROM qsaccel.profile_agg.adwh_fact_profile_ai_models d
       WHERE d.model_id = a.model_id) GROUP  BY b.model_name,
          model_type,
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

Zie de [ AI distributie van de Klant van de documentatie van de scores widget ](../guides/profiles.md#customer-ai-distribution-of-scores) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Overzicht van AI-scores van klant {#customer-ai-scoring-summary}

Vragen beantwoord door dit inzicht:

- Wat is het scoresamenvatting voor elk van mijn AI-modellen van de Klant?
- Hoe veranderen mijn AI-proENTIECores van mijn klant voor verschillende soorten publiek?
- Hoe verandert mijn het scoren samenvattingsverandering in vergelijking met andere KPIs in het profiel overzicht?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT model_name,
         model_type,
         CASE
             WHEN score BETWEEN 0 AND 24 THEN 'LOW'
             WHEN score BETWEEN 25 AND 74 THEN 'MEDIUM'
             WHEN score BETWEEN 75 AND 100 THEN 'HIGH'
         END score_buckets,
         sum(count_of_profiles) count_of_profiles
  FROM QSAccel.profile_agg.adwh_fact_profile_ai_models a
  JOIN QSAccel.profile_agg.adwh_dim_ai_models b ON a.merge_policy_id=b.merge_policy_id
  AND a.model_id=b.model_id
  WHERE a.merge_policy_id=2027892989
    AND a.model_id =1829081696
    AND score_date=
      (SELECT max(score_date)
       FROM QSAccel.profile_agg.adwh_fact_profile_ai_models d
       WHERE d.model_id=a.model_id)
  GROUP BY model_name,
           model_type,
           CASE
               WHEN score BETWEEN 0 AND 24 THEN 'LOW'
               WHEN score BETWEEN 25 AND 74 THEN 'MEDIUM'
               WHEN score BETWEEN 75 AND 100 THEN 'HIGH'
           END;
```

+++

Zie de [ AI van de Klant die summiere widget documentatie ](../guides/profiles.md#customer-ai-scoring-summary) voor informatie over de verschijning en de functionaliteit van dit inzicht scoren.

## Identiteitsoverlapping {#identity-overlap}

Vragen beantwoord door dit inzicht:

- Wat is het algemene snijpunt tussen [!UICONTROL Identity Type A] en [!UICONTROL Identity Type B]?
- Hoe kan ik klantenpubliek verfijnen dat op de overlapping van specifieke identiteitstypes wordt gebaseerd om gerichte marketing strategieën te verbeteren?
- Welke inzichten kunnen worden verkregen bij de evaluatie van de prestaties van de campagne op de elkaar kruisende gebieden?
- Hoe kunnen toekomstige marketinginspanningen worden geoptimaliseerd aan de hand van dit inzicht in de campagneprestaties?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT Sum(overlap_col1) overlap_col1,
        Sum(overlap_col2) overlap_col2,
        coalesce(Sum(overlap_count), 0) overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            Sum(count_of_profiles) overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace.overlap_id IN
        (SELECT a.overlap_id
          FROM
            (SELECT qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id overlap_id,
                    count(*) cnt_num
            FROM qsaccel.profile_agg.adwh_dim_overlap_namespaces
            WHERE qsaccel.profile_agg.adwh_dim_overlap_namespaces.merge_policy_id = 2027892989
              AND qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_namespaces in ('avid',
                                                                                          'crmid')
            GROUP BY qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id)a
          WHERE a.cnt_num>1 )
    UNION ALL SELECT count_of_profiles overlap_col1,
                      0 overlap_col2,
                      0 overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'avid'
    UNION ALL SELECT 0 overlap_col1,
                      count_of_profiles overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'crmid' )a;
```

+++

Zie de [ documentatie van de overlap van de Identiteit ](../guides/profiles.md#identity-overlap) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Aantal profielen {#profile-count}

Vragen beantwoord door dit inzicht:

- Wat is het totale aantal profielen in de Adobe Real-time Customer Data Platform?
- Hoe worden de profielen verdeeld die op fusiebeleid worden gebaseerd?
- Welk samenvoegbeleid heeft het hoogste profielaantal?

Het SQl dat deze inzichten produceert is als volgt:

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

De volledige informatie over de verschijning en de functionaliteit van dit inzicht kan in de [ gids van de tellingtelling van het Profiel ](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#profile-count) worden gevonden.

Zie de [ documentatie van de tellingswidget van het Profiel ](../guides/profiles.md#profile-count) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Wijziging van aantal profielen {#profile-count-change}

Vragen beantwoord door dit inzicht:

- Wat is de trend in de totale veranderingen in het aantal profielen?
- Wat veroorzaakte significante pieken of dalingen in profieltelling?
- Zijn er specifieke samenvoegingsbeleid die de verandering van het profielaantal drijven?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT (sum(count_of_profiles) - sum(count_of_profiles_days_ago)) profiles_added
  FROM
    (SELECT sum(qsaccel.profile_agg.adwh_fact_profile.count_of_profiles) count_of_profiles,
            0 count_of_profiles_days_ago
    FROM qsaccel.profile_agg.adwh_fact_profile
    WHERE qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile.date_key = '2024-01-10'
    UNION ALL SELECT 0 count_of_profiles,
                      CASE
                          WHEN sum(cntondatediff) =0 THEN sum(cntmin)
                          ELSE sum(cntondatediff)
                      END AS count_of_profiles_days_ago
    FROM
      (SELECT coalesce(sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles), 0) cntondatediff,
              0 cntmin
        FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
        WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id =2027892989
          AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key =dateadd(DAY, - 30, '2024-01-10')
        UNION ALL SELECT 0 cntondatediff,
                        sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles) countMin
        FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
        WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id = 2027892989
          AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key =
            (SELECT min(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key) col
            FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
            WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id =2027892989
              AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key >= dateadd(DAY, - 30, '2024-01-10')
              AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles IS NOT NULL) )b) a;
```

+++

Zie de [ documentatie van de de veranderingsverandering van het Aantal van het Profiel ](../guides/profiles.md#profile-count-change) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Tendens van wijzigingen in aantal profielen {#profile-count-change-trend}

Vragen beantwoord door dit inzicht:

- Wat is de algemene trend in het aantal profielveranderingen in de afgelopen twaalf maanden op basis van het fusiebeleid?
- Zijn er specifieke patronen of fluctuaties in het aantal profielen die in de afgelopen 30 dagen zijn gewijzigd en die aandacht behoeven?
- Hoe verhoudt het aantal profielen zich de afgelopen 90 dagen tot de algemene trend?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT date_key,
         profiles_count_change
  FROM
    (SELECT rn_num,
            date_key,
            (count_of_profiles-lag(count_of_profiles, 1, 0) over(
                                                            ORDER BY date_key))profiles_count_change
    FROM
      (SELECT qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key,
              sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles) count_of_profiles,
              row_number() OVER (
                              ORDER BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key) rn_num
      FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key >=dateadd(DAY, - 30 -1, '2024-01-10')
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key)a)b
  WHERE rn_num > 1;
```

+++

Zie de [ documentatie van de de veranderingstrend widget van de tellingverandering van het Profiel ](../guides/profiles.md#profile-count-change-trend) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Tendens aantal profielen {#profile-count-trend}

Vragen beantwoord door dit inzicht:

- Wat is de algemene trend in het aantal profielen op basis van het fusiebeleid in de afgelopen 30 dagen?
- Hoe verhoudt zij zich op basis van deze trend tot de langetermijntrends (bijvoorbeeld 90 dagen en 12 maanden)?
- Welk samenvoegingsbeleid draagt het meest bij tot de verhoging of de daling van profieltelling over de gespecificeerde tijdsperiodes (30 dagen, 90 dagen, en 12 maanden)?
- Zijn er specifieke pieken of dalingen in profieltelling die met bepaalde gebeurtenissen of periodes binnen het tijdkader van 30 dagen correleren?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT date_key,
       sum(count_of_profiles) AS count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines x
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL'
     GROUP BY merge_policy_id) y ON x.merge_policy_id = y.merge_policy_id
  WHERE date_key >= dateadd(DAY, -365, y.last_process_date)
    AND x.merge_policy_id = 2027892989
  GROUP BY date_key;
```

+++

Zie de [ documentatie van de de telendetrend van het Profiel widget ](../guides/profiles.md#profile-count-trend) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Profielen op identiteit {#profiles-by-identity}

Vragen beantwoord door dit inzicht:

- Van het totale aantal profielen, welk identiteitstype houdt een hoger percentage?
- Zijn er aanzienlijke verschillen tussen de identiteitstypen?
- Wat is de algemene verspreiding van identiteitstypen?
- Zijn er significante verschillen of anomalieën in het aantal identiteitsbewijzen?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.count_of_profiles) count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
  AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
          qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id,
          qsaccel.profile_agg.adwh_dim_namespaces.namespace_description
  ORDER BY count_of_profiles DESC;
```

+++

Zie [ Profielen door de documentatie van de identiteitswidget ](../guides/profiles.md#profiles-by-identity) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Ontwikkeling van aantal profielen {#profiles-count-change-trend}

Vragen beantwoord door dit inzicht:

- Wat is de algemene trend in de verandering van het aantal profielen in de afgelopen twaalf maanden, gebaseerd op het fusiebeleid?
- Zijn er specifieke patronen of schommelingen in de verandering van het profielaantal in de afgelopen 30 dagen die aandacht vergen?
- Hoe verhoudt de verandering van het profiel zich de afgelopen 90 dagen tot de algemene trend?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT date_key,
         profiles_count_change
  FROM
    (SELECT rn_num,
            date_key,
            (count_of_profiles-lag(count_of_profiles, 1, 0) over(
                                                            ORDER BY date_key))profiles_count_change
    FROM
      (SELECT qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key,
              sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles) count_of_profiles,
              row_number() OVER (
                              ORDER BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key) rn_num
      FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key >=dateadd(DAY, - 30 -1, '2024-01-10')
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key)a)b
  WHERE rn_num > 1;
```

+++

Zie de [ documentatie van de de veranderingstrend widget van de Tendens van Profielen ](../guides/profiles.md#profiles-count-change-trend) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Tendens van verandering van aantal profielen door identiteit {#profiles-count-change-trend-by-identity}

Vragen beantwoord door dit inzicht:

- Wat is de algemene trend in de verandering van het aantal profielen in de afgelopen twaalf maanden voor verschillende identiteiten?
- Zijn er specifieke identiteitstendensen die significante veranderingen in de laatste 30 dagen tonen?
- Hoe verschillen de veranderingen in het profielaantal wanneer het vergelijken van de 30 dag, 90 dag, en 12 maandtendensen voor een bepaalde identiteit?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT date_key,
        namespace_description,
        profiles_count_change
  FROM
    (SELECT rn_num,
            date_key,
            namespace_description,
            (count_of_profiles - lag(count_of_profiles, 1, 0) over(PARTITION BY namespace_description
                                                                  ORDER BY date_key)) profiles_count_change
    FROM
      (SELECT qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
              qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
              sum(qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.count_of_profiles) count_of_profiles,
              row_number() OVER (PARTITION BY qsaccel.profile_agg.adwh_dim_namespaces.namespace_description
                                  ORDER BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key) rn_num
        FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
        LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
        AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
        WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
          AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id= -1042977439
          AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key >= dateadd(DAY, - 30 -1, '2024-01-10')
        GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
                adwh_dim_namespaces.namespace_description)a)b
  WHERE rn_num > 1;
```

+++

Zie de [ trend van de verandering van de tellingen van Profielen door de documentatie van de identiteitswidget ](../guides/profiles.md#profiles-count-change-trend-by-identity) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Eén identiteitsprofiel {#single-identity-profiles}

Vragen beantwoord door dit inzicht:

- Zijn mijn gegevens van de klantenidentiteit constant vertegenwoordigd met enige identiteiten?
- Welk percentage van mijn gebruikersbasis bestaat uit profielen met slechts één enkel type van identiteit?
- Hoe is dit effect op de volledigheid van de profielen met slechts één type identiteit?
- Is er een correlatie tussen het gemeenschappelijkste identiteitstype en het enige aantal van het identiteitsprofiel?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_Single_Identity_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

+++

Zie de [ Enige documentatie van de widget van identiteitsprofielen ](../guides/profiles.md#single-identity-profiles) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Eén identiteitsprofiel op basis van identiteit {#single-identity-profiles-by-identity}

Vragen beantwoord door dit inzicht:

- Hoeveel unieke klanten hebben zich met één identiteit geregistreerd (bijvoorbeeld een e-mail- of telefoonnummer)?
- Wat is de distributie van enkele identiteitsprofielen onder verschillende identiteitstypes, zoals e-mail of telefoonaantallen?
- Zijn er identiteitspatronen of verschuivingen binnen de enige identiteitsprofielen?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.count_of_Single_Identity_profiles) count_of_Single_Identity_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
  AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
          qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id,
          qsaccel.profile_agg.adwh_dim_namespaces.namespace_description;
```

+++

Zie [ Enige identiteitsprofielen door de documentatie van de identiteitswidget ](../guides/profiles.md#single-identity-profiles-by-identity) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Niet-gesegmenteerde profielen {#unsegmented-profiles}

Vragen beantwoord door dit inzicht:

- Hoeveel profielen maken geen deel uit van een publiek?
- Welk percentage van het totale publiek wordt vertegenwoordigd door ongesegmenteerde profielen?
- Leidt een fusiebeleid tot een groot aantal ongesegmenteerde profielen?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_Orphan_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

+++

Zie de [ Unsegmented de documentatie van de profielwidget ](../guides/profiles.md#unsegmented-profiles) voor informatie over de verschijning en de functionaliteit van dit inzicht.

## Volgende stappen

Door dit document te lezen, begrijpt u nu de SQL die dashboardinzichten produceert en welke gemeenschappelijke vragen deze analyse oplost. U kunt nu de SQL bewerken en doorlopen om uw eigen inzichten te genereren.

Zie de [ documentatie van de Mening SQL ](../view-sql.md) voor meer informatie over hoe te om SQL van uw inzichten direct door PLatform UI aan te passen.

U kunt SQL ook lezen en begrijpen die inzichten voor het [ publiek ](./audiences.md), [ Profielen van de Rekening ](./account-profiles.md), en [ Doelen ](./destinations.md) dashboards van Doelen produceert.
