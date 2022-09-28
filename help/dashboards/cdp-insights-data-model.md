---
title: Gegevensmodel gegevens klant-Platform (CDP)
description: Leer hoe te om SQL vragen van de Modellen van Gegevens van Gegevens van CDP van Inzichten te gebruiken om uw eigen CDP rapporten voor uw marketing en KPI gebruiksgevallen aan te passen.
exl-id: 61bc7f23-9f79-4c75-a515-85dd9dda2d02
source-git-commit: 2c96bfd2c1b541d30a72fcf2bac414ee06607456
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 0%

---

# Gegevensmodel gegevens klant-Platform (CDP)

De eigenschap van het Model van Gegevens van de Gegevens van de Klant van het Platform van Gegevens (CDP) benadrukt de gegevensmodellen en SQL die de inzichten voor diverse profiel, bestemming, en segmentatiewidgets macht. U kunt deze SQL vraagmalplaatjes aanpassen om CDP- rapporten voor uw marketing en belangrijkste het gebruiksgevallen van de prestatiesindicator (KPI) tot stand te brengen. Deze inzichten kunnen dan als douanewidgets voor uw user-defined dashboards worden gebruikt.

## Vereisten

Deze handleiding vereist een goed begrip van de [door de gebruiker gedefinieerde dashboardfunctie](./user-defined-dashboards.md). Lees de documentatie voordat u verdergaat met deze handleiding.

## CDP-inzichtsrapporten en -gebruiksgevallen

CDP het melden verstrekt inzichten in uw profielgegevens en zijn verhouding met segmenten en bestemmingen. Er zijn verschillende sterschemamodellen ontwikkeld om een aantal veelvoorkomende gevallen van marketinggebruik te beantwoorden en elk gegevensmodel kan meerdere gebruiksgevallen ondersteunen.

>[!IMPORTANT]
>
>De gegevens die voor CDP rapportering worden gebruikt zijn nauwkeurig voor een gekozen samenvoegbeleid en van de meest recente dagmomentopname.

### Profielmodel {#profile-model}

Het profielmodel bestaat uit drie datasets:

- `adwh_dim_date`
- `adwh_fact_profile`
- `adwh_dim_merge_policies`

De afbeelding hieronder bevat de relevante gegevensvelden in elke gegevensset.

![Een ERD van het profielmodel.](./images/cdp-insights/profile-model.png)

#### Het gebruikte hoofdlettergebruik voor het aantal profielen

De logica die wordt gebruikt voor de widget voor het aantal profielen retourneert het totale aantal samengevoegde profielen in de profielenwinkel op het moment dat de momentopname werd gemaakt. Zie de [[!UICONTROL Profile count] widget-documentatie](./guides/profiles.md#profile-count) voor meer informatie .

De SQL die de [!UICONTROL Profile count] De widget wordt weergegeven in de sectie hieronder die kan worden samengevouwen.

+++SQL-query

```sql
SELECT adwh_dim_merge_policies.merge_policy_name,
  sum(adwh_fact_profile.count_of_profiles) CNT
FROM qsaccel.profile_agg.adwh_fact_profile
LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
WHERE adwh_fact_profile.date_key='${lastProcessDate}'
AND adwh_fact_profile.merge_policy_id=${mergePolicyId}
GROUP BY adwh_dim_merge_policies.merge_policy_name;
```

+++

#### Het gebruik van hoofdletters en kleine letters in het profiel Eén identiteit

De logica die wordt gebruikt voor de [!UICONTROL Single identity profiles] widget bevat een aantal profielen van uw organisatie die slechts één type id hebben waarmee hun identiteit wordt gemaakt. Zie de[[!UICONTROL Single identity profiles] widget-documentatie](./guides/profiles.md#single-identity-profiles) voor meer informatie .

De SQL die de [!UICONTROL Single identity profiles] De widget wordt weergegeven in de sectie hieronder die kan worden samengevouwen.

+++SQL-query

```sql
SELECT adwh_dim_merge_policies.merge_policy_name,
  sum(adwh_fact_profile.count_of_Single_Identity_profiles) CNT
FROM QSAccel.profile_agg.adwh_fact_profile
LEFT OUTER JOIN QSAccel.profile_agg.adwh_dim_merge_policies ON adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
WHERE adwh_fact_profile.date_key='${lastProcessDate}'
  AND adwh_fact_profile.merge_policy_id =${mergePolicyId}
GROUP BY adwh_dim_merge_policies.merge_policy_name;
```

+++

### Namespace-model {#namespace-model}

Het naamruimtemodel bestaat uit de volgende gegevenssets:

- `adwh_fact_profile_by_namespace`
- `adwh_dim_date`
- `adwh_dim_namespaces`
- `adwh_dim_merge_policies`

De afbeelding hieronder bevat de relevante gegevensvelden in elke gegevensset.

![Een ERD van het naamruimtemodel.](./images/cdp-insights/namespace-model.png)

#### Profielen op basis van hoofdlettergebruik

De [!UICONTROL Profiles by identity] widget geeft de indeling van de identiteiten in alle samengevoegde profielen in uw profielarchief weer. Zie de [[!UICONTROL Profiles by identity] widget-documentatie](./guides/profiles.md#profiles-by-identity) voor meer informatie .

De SQL die de [!UICONTROL Profiles by identity] De widget wordt weergegeven in de sectie hieronder die kan worden samengevouwen.

+++SQL-query

```sql
SELECT adwh_dim_namespaces.namespace_description,
    sum(adwh_fact_profile_by_namespace.count_of_profiles) count_of_profiles
FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace
JOIN qsaccel.profile_agg.adwh_dim_namespaces ON adwh_fact_profile_by_namespace.namespace_id = adwh_dim_namespaces.namespace_id
AND adwh_fact_profile_by_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
WHERE adwh_fact_profile_by_namespace.merge_policy_id =${mergePolicyId}
AND adwh_fact_profile_by_namespace.date_key = '${lastProcessDate}'
GROUP BY adwh_fact_profile_by_namespace.date_key,
        adwh_fact_profile_by_namespace.merge_policy_id,
        adwh_dim_namespaces.namespace_description
ORDER BY count_of_profiles DESC
LIMIT 5;
```

+++

#### Individuele identiteitsprofielen per geval van identiteitsgebruik

De logica die wordt gebruikt voor de [!UICONTROL Single identity profiles by identity] widget illustreert het totale aantal profielen dat met slechts één unieke id wordt geïdentificeerd. Zie de [Eén identiteitsprofiel op basis van documentatie voor een identiteitswidget](./guides/profiles.md#single-identity-profiles-by-identity) voor meer informatie .

De SQL die de [!UICONTROL Single identity profiles by identity] De widget wordt weergegeven in de sectie hieronder die kan worden samengevouwen.

+++SQL-query

```sql
SELECT
  adwh_dim_namespaces.namespace_description,
  sum(adwh_fact_profile_by_namespace.count_of_Single_Identity_profiles) count_of_Single_Identity_profiles
FROM
  qsaccel.profile_agg.adwh_fact_profile_by_namespace
  LEFT OUTER JOIN
    qsaccel.profile_agg.adwh_dim_namespaces
    ON adwh_fact_profile_by_namespace.namespace_id = adwh_dim_namespaces.namespace_id
AND adwh_fact_profile_by_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
WHERE
  adwh_fact_profile_by_namespace.merge_policy_id=${mergePolicyId}
  AND adwh_fact_profile_by_namespace.date_key='${lastProcessDate}'
GROUP BY
  adwh_fact_profile_by_namespace.date_key,
  adwh_fact_profile_by_namespace.merge_policy_id,
  adwh_dim_namespaces.namespace_description;
```

+++

### Segmentmodel {#segment-model}

Het segmentmodel bestaat uit de volgende datasets:

- `adwh_dim_date`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_fact_profile_by_segment`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

De afbeelding hieronder bevat de relevante gegevensvelden in elke gegevensset.

![Een ERD van het segmentmodel.](./images/cdp-insights/segment-model.png)

#### Gebruiksscenario voor grootte publiek

De logica die wordt gebruikt voor de [!UICONTROL Audience size] widget retourneert het totale aantal samengevoegde profielen binnen het geselecteerde segment op het moment van de meest recente momentopname. Zie de [[!UICONTROL Audience size] widget-documentatie](./guides/segments.md#audience-size) voor meer informatie .

De SQL die de [!UICONTROL Audience size] De widget wordt weergegeven in de sectie hieronder die kan worden samengevouwen.

+++SQL-query

```sql
SELECT adwh_fact_profile_by_segment.date_key,
       adwh_dim_merge_policies.merge_policy_name,
       adwh_dim_segments.segment,
       adwh_dim_segments.segment_name,
       sum(adwh_fact_profile_by_segment.count_of_profiles)count_of_profiles
FROM qsaccel.profile_agg.adwh_fact_profile_by_segment
LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_segments ON adwh_fact_profile_by_segment.segment_id = adwh_dim_segments.segment_id
LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON adwh_fact_profile_by_segment.merge_policy_id=adwh_dim_merge_policies.merge_policy_id
WHERE adwh_fact_profile_by_segment.date_key ='${lastProcessDate}'
  AND adwh_fact_profile_by_segment.merge_policy_id=${mergePolicyId}
GROUP BY adwh_fact_profile_by_segment.date_key,
         adwh_dim_merge_policies.merge_policy_name,
         adwh_dim_segments.segment,
         adwh_dim_segments.segment_name
ORDER BY count_of_profiles DESC
LIMIT 20;
```

+++

#### Omvang van het publiek omwenteling trend gebruikscase

De logica die wordt gebruikt voor de [!UICONTROL Audience size change trend] widget geeft een lijngrafiekillustratie van het verschil in het totale aantal profielen dat voor een bepaald segment in aanmerking kwam tussen de meest recente dagelijkse momentopnamen. Zie de [[!UICONTROL Audience size change trend] widget-documentatie](./guides/segments.md#audience-size-change-trend) voor meer informatie .

De SQL die de [!UICONTROL Audience size change trend] De widget wordt weergegeven in de sectie hieronder die kan worden samengevouwen.

+++SQL-query

```sql
SELECT DISTINCT cast(adwh_dim_segments.create_date AS Date) Date_key, adwh_dim_merge_policies.merge_policy_name,
  count(DISTINCT adwh_dim_segments.segment_id)Segments_Added
FROM qsaccel.profile_agg.adwh_fact_profile_by_segment
JOIN qsaccel.profile_agg.adwh_dim_segments ON adwh_fact_profile_by_segment.segment_id = adwh_dim_segments.segment_id
JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON adwh_fact_profile_by_segment.merge_policy_id=adwh_dim_merge_policies.merge_policy_id
WHERE Cast(adwh_dim_segments.create_date AS date) >= dateadd(DAY, - ${dayRange}, '${lastProcessDate}')
AND adwh_fact_profile_by_segment.merge_policy_id=${mergePolicyId}
GROUP BY cast(adwh_dim_segments.create_date AS date), adwh_dim_merge_policies.merge_policy_name ;
```

+++

#### De meeste gebruikte bestemmingen gebruiken case

De logica die wordt gebruikt in de [!UICONTROL Most used destinations] widget geeft een overzicht van de meest gebruikte doelen van uw organisatie op basis van het aantal segmenten dat aan hen is toegewezen. Deze rangschikking biedt inzicht in welke bestemmingen worden gebruikt en toont mogelijk ook de bestemmingen die mogelijk onderbenut zijn. Zie de documentatie op de [[!UICONTROL Most used destinations] widget](./guides/destinations.md#most-used-destinations) voor meer informatie .

De SQL die de [!UICONTROL Most used destinations] De widget wordt weergegeven in de sectie hieronder die kan worden samengevouwen.

+++SQL-query

```sql
SELECT
   adwh_dim_destination.destination_name, adwh_dim_destination.destination_id,
   count( distinct adwh_dim_br_segment_destinations.segment_id ) segment_count
FROM
   qsaccel.profile_agg.adwh_dim_destination
   join qsaccel.profile_agg.adwh_dim_br_segment_destinations
 ON
   adwh_dim_destination.destination_id = adwh_dim_br_segment_destinations.destination_id
 WHERE
   adwh_dim_destination.destination_name is not null
 group by
   adwh_dim_destination.destination_name,
   adwh_dim_destination.destination_id
   order by segment_count desc limit 5;
```

+++

#### Pas geactiveerde segmenten gebruiken hoofdletters/kleine letters

De logica voor de [!UICONTROL Recently activated segments] widget bevat een lijst met de segmenten die het laatst zijn toegewezen aan een doel. Deze lijst verstrekt een momentopname van de segmenten en de bestemmingen die actief in gebruik in het systeem zijn en in het oplossen van problemen kunnen helpen om het even welke onjuiste afbeeldingen. Zie de [[!UICONTROL Recently activated segments] widget-documentatie](./guides/destinations.md#recently-activated-segments) voor meer informatie .

De SQL die de [!UICONTROL Recently activated segments] De widget wordt weergegeven in de sectie hieronder die kan worden samengevouwen.

+++SQL-query

```sql
SELECT segment_name, segment, destination_name, a.create_time create_time
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id = c.destination_id
ORDER BY create_time desc, segment LIMIT 5;
```

+++

### Model van naamruimte-segment

Het namespace-segment model wordt samengesteld uit de volgende datasets:

- `adwh_dim_date`
- `adwh_dim_merge_policies`
- `adwh_dim_namespaces`
- `adwh_fact_profile_by_segment_and_namespace`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

De afbeelding hieronder bevat de relevante gegevensvelden in elke gegevensset.

![Een ERD van het segmentmodel.](./images/cdp-insights/namespace-segment-model.png)

#### Profielen op identiteit voor een geval van segmentgebruik

De logica die wordt gebruikt in de [!UICONTROL Profiles by identity] widget geeft een overzicht van de identiteiten in alle samengevoegde profielen in uw profielenarchief voor een bepaald segment. Zie de [[!UICONTROL Profiles by identity] widget-documentatie](./guides/segments.md#profiles-by-identity) voor meer informatie .

De SQL die de [!UICONTROL Profiles by identity] De widget wordt weergegeven in de sectie hieronder die kan worden samengevouwen.

+++SQL-query

```sql
SELECT adwh_dim_namespaces.namespace_description,
  sum( adwh_fact_profile_by_segment_and_namespace.count_of_profiles) count_of_profiles
FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace
LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces
ON adwh_fact_profile_by_segment_and_namespace.namespace_id = adwh_dim_namespaces.namespace_id
AND adwh_fact_profile_by_segment_and_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
WHERE adwh_fact_profile_by_segment_and_namespace.segment_id = {segment_id}
AND adwh_fact_profile_by_segment_and_namespace.merge_policy_id = {merge_policy_id}
AND adwh_fact_profile_by_segment_and_namespace.date_key = '{date}'
GROUP BY adwh_dim_namespaces.namespace_description;
```

+++

### Naamruimtemodel overlappen

Het overlap naamruimtemodel bestaat uit de volgende gegevenssets:

- `adwh_dim_date`
- `adwh_dim_namespaces`
- `adwh_fact_profile_overlap_of_namespace`
- `adwh_dim_merge_policies`

De afbeelding hieronder bevat de relevante gegevensvelden in elke gegevensset.

![Een ERD van het segmentmodel.](./images/cdp-insights/overlap-namespace-model.png)

#### Identiteitsoverlapping (profielen) gebruikt hoofdletters/kleine letters

De logica die wordt gebruikt in de [!UICONTROL Identity overlap] widget geeft de overlapping van profielen in uw **Profielopslag** die de twee geselecteerde identiteiten bevatten. Zie voor meer informatie de [[!UICONTROL Identity overlap] widgetsectie van het dialoogvenster [!UICONTROL Profiles] dashboarddocumentatie](./guides/profiles.md#identity-overlap).

De SQL die de [!UICONTROL Identity overlap] De widget wordt weergegeven in de sectie hieronder die kan worden samengevouwen.

+++SQL-query

```sql
SELECT Sum(overlap_col1) overlap_col1,
       Sum(overlap_col2) overlap_col2,
       coalesce(Sum(overlap_count), 0) overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            Sum(count_of_profiles) overlap_count
     FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace
     WHERE adwh_fact_profile_overlap_of_namespace.merge_policy_id = ${mergePolicyId}
       AND adwh_fact_profile_overlap_of_namespace.date_key = '${lastProcessDate}'
       AND adwh_fact_profile_overlap_of_namespace.overlap_id IN
         (SELECT adwh_dim_overlap_namespaces.overlap_id
          FROM qsaccel.profile_agg.adwh_dim_overlap_namespaces
          WHERE adwh_dim_overlap_namespaces.merge_policy_id=${mergePolicyId}
            AND adwh_dim_overlap_namespaces.overlap_namespaces IN ('${namespace1}',
                                                                   '${namespace2}')
          GROUP BY adwh_dim_overlap_namespaces.overlap_id
          HAVING Count(*) > 1)
     UNION ALL SELECT count_of_profiles overlap_col1,
                      0 overlap_col2,
                      0 overlap_count
     FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace
     JOIN qsaccel.profile_agg.adwh_dim_namespaces ON
     adwh_fact_profile_by_namespace.namespace_id = adwh_dim_namespaces.namespace_id
     AND adwh_fact_profile_by_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
     WHERE adwh_fact_profile_by_namespace.merge_policy_id = ${mergePolicyId}
       AND adwh_fact_profile_by_namespace.date_key = '${lastProcessDate}'
       AND adwh_dim_namespaces.namespace_description = '${namespace1}'
     UNION ALL SELECT 0 overlap_col1,
                      count_of_profiles overlap_col2,
                      0 Overlap_count
     FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace
     JOIN qsaccel.profile_agg.adwh_dim_namespaces ON
     adwh_fact_profile_by_namespace.namespace_id = adwh_dim_namespaces.namespace_id
     AND adwh_fact_profile_by_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
     WHERE adwh_fact_profile_by_namespace.merge_policy_id = ${mergePolicyId}
       AND adwh_fact_profile_by_namespace.date_key = '${lastProcessDate}'
       AND adwh_dim_namespaces.namespace_description = '${namespace2}' ) a;
```

+++

### Namespace door segmentmodel overlappen

De overlappende naamruimte per segmentmodel bestaat uit de volgende datasets:

- `adwh_dim_date`
- `adwh_dim_namespaces`
- `adwh_fact_profile_overlap_of_namespace_by_segment`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

De afbeelding hieronder bevat de relevante gegevensvelden in elke gegevensset.

![Een ERD van het segmentmodel.](./images/cdp-insights/overlap-namespace-by-segment-model.png)

#### Identiteitsoverlap (segmenten) gebruiken hoofdletters/kleine letters

De logica die wordt gebruikt in de [!UICONTROL Segments] dashboard [!UICONTROL Identity overlap] widget illustreert de overlapping van profielen die de twee geselecteerde identiteiten voor een bepaald segment bevatten. Zie voor meer informatie de [[!UICONTROL Identity overlap] widgetsectie van het dialoogvenster [!UICONTROL Segmentation] dashboarddocumentatie](./guides/segments.md#identity-overlap).

De SQL die de [!UICONTROL Identity overlap] De widget wordt weergegeven in de sectie hieronder die kan worden samengevouwen.

+++SQL-query

```sql
SELECT
   Sum(overlap_col1) overlap_col1,
   Sum( overlap_col2) overlap_col2,
   Sum(overlap_count) Overlap_count
FROM
   (
      SELECT
         0 overlap_col1,
         0 overlap_col2,
         Sum(count_of_profiles) Overlap_count
      FROM
         qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment
      WHERE
         adwh_fact_profile_overlap_of_namespace_by_segment.segment_id = $ {segmentId}
         and adwh_fact_profile_overlap_of_namespace_by_segment.merge_policy_id =$ {mergePolicyId}
         and adwh_fact_profile_overlap_of_namespace_by_segment.date_key = '${lastProcessDate}'
         and adwh_fact_profile_overlap_of_namespace_by_segment.overlap_id IN
         (
            SELECT
               adwh_dim_overlap_namespaces.overlap_id
            FROM
               qsaccel.profile_agg.adwh_dim_overlap_namespaces
            WHERE
               adwh_dim_overlap_namespaces.merge_policy_id =$ {mergePolicyId}
               AND adwh_dim_overlap_namespaces.overlap_namespaces IN
               (
                  '${namespace1}',
                  '${namespace2}'
               )
            GROUP BY
               adwh_dim_overlap_namespaces.overlap_id
            HAVING
               Count(*) > 1
         )
      UNION ALL
      SELECT
         count_of_profiles overlap_col1,
         0 overlap_col2,
         0 Overlap_count
      FROM
         qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace
         LEFT OUTER JOIN
            qsaccel.profile_agg.adwh_dim_namespaces
            ON adwh_fact_profile_by_segment_and_namespace.namespace_id = adwh_dim_namespaces.namespace_id
            and adwh_fact_profile_by_segment_and_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
      WHERE
         adwh_dim_namespaces.namespace_description = '${namespace1}'
         and adwh_fact_profile_by_segment_and_namespace.segment_id = $ {segmentId}
         and adwh_fact_profile_by_segment_and_namespace.merge_policy_id =$ {mergePolicyId}
         and adwh_fact_profile_by_segment_and_namespace.date_key = '${lastProcessDate}'
      UNION ALL
      SELECT
         0 overlap_col1,
         count_of_profiles overlap_col2,
         0 Overlap_count
      FROM
         qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace
         LEFT OUTER JOIN
            qsaccel.profile_agg.adwh_dim_namespaces
            ON adwh_fact_profile_by_segment_and_namespace.namespace_id = adwh_dim_namespaces.namespace_id
            and adwh_fact_profile_by_segment_and_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
      WHERE
         adwh_dim_namespaces.namespace_description = '${namespace2}'
         and adwh_fact_profile_by_segment_and_namespace.segment_id = $ {segmentId}
         and adwh_fact_profile_by_segment_and_namespace.merge_policy_id =$ {mergePolicyId}
         and adwh_fact_profile_by_segment_and_namespace.date_key = '${lastProcessDate}'
   )
   a;
```

+++
