---
title: Accountprofielgegevens
description: Ontdek SQL die uw inzicht van het Profiel van de Rekening en gebruik deze vragen aandrijft om douaneinzichten te produceren die uw klanten en hun ervaringen van de consument verder onderzoeken.
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="B2P Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: a953dd56-7dd8-4cd0-baa0-85f92d192789
source-git-commit: 8b6cd84a31f9cdccef9f342df7f7b8450c2405dc
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---

# Accountprofielinzichten

[ de profielen van de Rekening ](../../rtcdp/accounts/account-profile-overview.md) worden gebruikt om rekeningsinformatie uit diverse bronnen, met inbegrip van veelvoudige marketing kanalen en organisatorische systemen te consolideren. Deze verenigde mening laat een uitvoerig inzicht in klantenrekeningen toe, die B2B marketing campagnes verbeteren. De inzichten die zijn afgeleid van de analyse van uw gegevensmodel maken uw Adobe Real-time Customer Data Platform B2B-gegevens toegankelijker, begrijpelijker en effectiever voor de besluitvorming.

Met toegang tot SQL die uw inzichten drijft, kunt u beter uw B2B gegevens begrijpen en uw eigen hoogst aangepaste herbruikbare inzichten produceren om uw informatie van de klantenrekening verder te onderzoeken. Transformeer uw onbewerkte gegevens in nieuwe inzichten die kunnen worden gebruikt door het bestaande Real-Time CDP-gegevensmodel SQL als inspiratie te gebruiken voor het maken van query&#39;s voor uw unieke bedrijfsbehoeften.

<!-- Add link to new generate insights with SQL workflow doc after April release.-->

De volgende inzichten zijn allen beschikbaar voor u als deel van het [ dashboard van Profielen van de Rekening ](../guides/account-profiles.md) of a [ douanedashboard ](../user-defined-dashboards.md) te gebruiken. Zie het [ aanpassingsoverzicht ](../customize/overview.md) voor instructies op hoe te om uw dashboard aan te passen of [ creeer en geef nieuwe widgets ](../customize/custom-widgets.md) in de widgetbibliotheek en [ user-defined dashboard ](../user-defined-dashboards.md#create-widget) uit.

## Accountprofielen toegevoegd {#account-profiles-added}

Vragen beantwoord door dit inzicht:

- Hoeveel accountprofielen zijn in een bepaalde periode toegevoegd?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
WITH accounts_by_mm_dd AS
(
          SELECT    d.date_key,
                    COALESCE(Sum(a.counts), 0) AS account_counts
          FROM      adwh_b2b_date d
          LEFT JOIN adwh_fact_account a
          ON        d.date_key = a.accounts_created_date
          WHERE     d.date_key BETWEEN Upper(COALESCE('$START_DATE', '')) AND       Upper(COALESCE('$END_DATE', ''))
          GROUP BY  d.date_key)
SELECT   date_key,
         account_counts
FROM     accounts_by_mm_dd
ORDER BY date_key limit 5000;
```

+++

## Nieuwe rekeningen van de industrie {#accounts-by-industry}

Vragen beantwoord door dit inzicht:

- Wat zijn de vijf belangrijkste sectoren waar de accountprofielen bij horen?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
WITH rankedindustries AS
(
           SELECT     i.industry,
                      Sum(f.counts)                                   AS total_accounts,
                      Row_number() OVER (ORDER BY Sum(f.counts) DESC) AS industry_rank
           FROM       adwh_fact_account f
           INNER JOIN adwh_dim_industry i
           ON         f.industry_id = i.industry_id
           WHERE      f.accounts_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND        Upper(COALESCE('$END_DATE', ''))
           GROUP BY   i.industry )
SELECT
         CASE
                  WHEN industry_rank <= 5 THEN industry
                  ELSE 'Others'
         END                 AS industry_group,
         Sum(total_accounts) AS total_accounts
FROM     rankedindustries
GROUP BY
         CASE
                  WHEN industry_rank <= 5 THEN industry
                  ELSE 'Others'
         END
ORDER BY total_accounts DESC limit 5000;
```

+++

## Nieuwe accounts per type {#accounts-by-type}

Vragen beantwoord door dit inzicht:

- Wat is het aantal rekeningen per type?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT t.account_type,
       Sum(f.counts) AS account_count
FROM   adwh_fact_account f
       JOIN adwh_dim_account_type t
         ON f.account_type_id = t.account_type_id
WHERE  accounts_created_date BETWEEN Upper(Coalesce('$START_DATE', '')) AND
                                     Upper(
                                     Coalesce('$END_DATE', ''))
GROUP  BY t.account_type
LIMIT  5000; 
```

+++

## Opportuniteiten toegevoegd {#opportunities-added}

Vragen beantwoord door dit inzicht:

- Hoeveel kansen zijn er in een bepaalde periode toegevoegd?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT d.date_key,
       Coalesce(Sum(o.counts), 0) AS opportunity_counts
FROM   adwh_b2b_date d
       LEFT JOIN adwh_fact_opportunity o
              ON d.date_key = o.opportunities_created_date
WHERE  d.date_key BETWEEN Upper(Coalesce('$START_DATE', '')) AND
                          Upper(Coalesce('$END_DATE', ''))
GROUP  BY d.date_key
ORDER  BY d.date_key
LIMIT  5000; 
```

+++

## Nieuwe mogelijkheden per persoonlijke rol {#opportunities-by-person-role}

Vragen beantwoord door dit inzicht:

- Wat is de relatieve omvang en het aantal van de verschillende rollen in een kans?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
SELECT p.person_role,
       Sum(f.counts) AS opportunity_counts
FROM   adwh_fact_opportunity_person f
       JOIN adwh_dim_person_role p
         ON f.person_role_id = p.person_role_id
WHERE  f.opportunity_person_created_date BETWEEN
       Upper(Coalesce('$START_DATE', '')) AND Upper(Coalesce('$END_DATE', ''))
GROUP  BY p.person_role
LIMIT  5000; 
```

+++

## Nieuwe mogelijkheden door inkomsten {#opportunities-by-revenue}

Vragen beantwoord door dit inzicht:

- Wat zijn de top 20 van de mogelijkheden die hun inkomsten (in USD) bieden?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
WITH ranked_opportunities AS
(
           SELECT     n.opportunity_name,
                      a.expected_revenue,
                      t.source_type,
                      Row_number() OVER (ORDER BY a.expected_revenue DESC) AS rank
           FROM       adwh_opportunity_amount a
           INNER JOIN adwh_dim_opportunity_name n
           ON         a.name_id = n.name_id
           INNER JOIN adwh_dim_opportunity_source_type t
           ON         n.source_type_id = t.source_type_id
           WHERE      a.opportunity_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND        Upper(COALESCE('$END_DATE', ''))
           AND        a.isclosed='false' )
SELECT
         CASE
                  WHEN rank <= 20 THEN opportunity_name
                  ELSE 'Others'
         END                   AS opportunity_name,
         Sum(expected_revenue) AS total_expected_revenue
FROM     ranked_opportunities
GROUP BY
         CASE
                  WHEN rank <= 20 THEN opportunity_name
                  ELSE 'Others'
         END,
         source_type
ORDER BY total_expected_revenue DESC limit 5000;
```

+++

## Nieuwe mogelijkheden per status en podium {#opportunities-by-status-and-stage}

Vragen beantwoord door dit inzicht:

- Welke mogelijkheden zijn er en in welk stadium bevinden zich de verkoop- of handelsketens?
- Welke gesloten mogelijkheden zijn er en in welk stadium bevinden de verkoop- of handelsketens zich?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
WITH opportunities_by_isclosed AS
(
         SELECT   f.isclosed,
                  Sum(f.counts)             AS opportunity_counts,
                  COALESCE(s.stage, 'null') AS stage
         FROM     adwh_fact_opportunity f
         JOIN     adwh_dim_opportunity_stage s
         ON       f.stage_id = s.stage_id
         WHERE    opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY f.isclosed,
                  s.stage)
SELECT
       CASE
              WHEN isclosed='true' THEN 'Closed'
              ELSE 'Open'
       END AS opportunity_closed,
       stage,
       opportunity_counts
FROM   opportunities_by_isclosed limit 5000;
```

+++

## Nieuwe kansen gewonnen {#opportunities-won}

Vragen beantwoord door dit inzicht:

- Wat is het aantal kansen dat met succes is gesloten of afgerond?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
WITH opportunities_by_iswon AS
(
         SELECT   iswon,
                  Sum(counts) AS opportunity_counts
         FROM     adwh_fact_opportunity
         WHERE    opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY iswon)
SELECT
       CASE
              WHEN iswon ='true' THEN 'True'
              ELSE 'False'
       END AS opportunity_won,
       opportunity_counts
FROM   opportunities_by_iswon limit 5000;
```

+++

## Opportuniteiten gewonnen (lijngrafiek) {#opportunities-won-line-graph}

<!-- Q) Can we change this name? -->

Vragen beantwoord door dit inzicht:

- Hoeveel kansen zijn er in een bepaalde periode met succes afgesloten of afgerond (gewonnen)?

+++Selecteer om de SQL te onthullen die dit inzicht produceert

```sql
WITH opportunities_won_counts AS
(
         SELECT   opportunities_created_date,
                  Sum(counts) AS opportunities_counts
         FROM     adwh_fact_opportunity
         WHERE    iswon='true'
         AND      opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY opportunities_created_date)
SELECT    d.date_key,
          COALESCE(o.opportunities_counts, 0) AS opportunity_won_counts
FROM      adwh_b2b_date d
LEFT JOIN opportunities_won_counts o
ON        d.date_key = o.opportunities_created_date
WHERE     d.date_key BETWEEN Upper(COALESCE('$START_DATE', '')) AND       Upper(COALESCE('$END_DATE', ''))
ORDER BY  d.date_key limit 5000;
```

+++

## Volgende stappen

Door dit document te lezen, begrijpt u nu de SQL die dashboardinzichten van het accountprofiel produceert en welke gemeenschappelijke vragen deze analyse oplost. U kunt nu de SQL bewerken en doorlopen om uw eigen inzichten te genereren.

<!-- Add link above Learn how to [generate insights with SQL](). after April release -->

U kunt SQL ook lezen en begrijpen die inzichten voor de [ Profielen ](./profiles.md), [ Soorten publiek ](./audiences.md), en [ Doelen ](./destinations.md) dashboards van Doelen produceert.
