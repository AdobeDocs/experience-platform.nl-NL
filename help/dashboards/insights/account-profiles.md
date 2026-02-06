---
title: Accountprofielgegevens
description: Ontdek SQL die uw inzicht van het Profiel van de Rekening en gebruik deze vragen aandrijft om douaneinzichten te produceren die uw klanten en hun ervaringen van de consument verder onderzoeken.
badgeB2B: null
exl-id: a953dd56-7dd8-4cd0-baa0-85f92d192789
source-git-commit: a32064848809d1cad07f769f04d82c35df451e38
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 0%

---

# Accountprofielinzichten

[ de profielen van de Rekening ](../../rtcdp/accounts/account-profile-overview.md) worden gebruikt om rekeningsinformatie uit diverse bronnen, met inbegrip van veelvoudige marketing kanalen en organisatorische systemen te consolideren. Deze verenigde mening laat een uitvoerig inzicht in klantenrekeningen toe, die B2B marketing campagnes verbeteren. De inzichten die zijn afgeleid van de analyse van uw gegevensmodel maken uw Adobe Real-Time CDP B2B-gegevens toegankelijker, begrijpelijker en effectiever voor de besluitvorming.

Met toegang tot SQL die uw inzichten drijft, kunt u beter uw B2B gegevens begrijpen en uw eigen hoogst aangepaste herbruikbare inzichten produceren om uw informatie van de klantenrekening verder te onderzoeken. Transformeer uw onbewerkte gegevens in nieuwe inzichten die kunnen worden gebruikt door het bestaande Real-Time CDP-gegevensmodel SQL als inspiratie te gebruiken voor het maken van query&#39;s voor uw unieke bedrijfsbehoeften.

<!-- Add link to new generate insights with SQL workflow doc after April release.-->

De volgende inzichten zijn allen beschikbaar voor u als deel van het [ dashboard van Profielen van de Rekening ](../guides/account-profiles.md) of a [ douanedashboard ](../standard-dashboards.md) te gebruiken. Zie het [ aanpassingsoverzicht ](../customize/overview.md) voor instructies op hoe te om uw dashboard aan te passen of [ creeer en geef nieuwe widgets ](../customize/custom-widgets.md) in de widgetbibliotheek en [ user-defined dashboard ](../standard-dashboards.md#create-widget) uit.

## Accountprofielen toegevoegd {#account-profiles-added}

Door deze insight beantwoorde vragen:

- Hoeveel accountprofielen zijn in een bepaalde periode toegevoegd?

+++Selecteer deze optie om de SQL die deze insight genereert weer te geven

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

Door deze insight beantwoorde vragen:

- Wat zijn de vijf belangrijkste sectoren waar de accountprofielen bij horen?

+++Selecteer deze optie om de SQL die deze insight genereert weer te geven

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

Door deze insight beantwoorde vragen:

- Wat is het aantal rekeningen per type?

+++Selecteer deze optie om de SQL die deze insight genereert weer te geven

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

Door deze insight beantwoorde vragen:

- Hoeveel kansen zijn er in een bepaalde periode toegevoegd?

+++Selecteer deze optie om de SQL die deze insight genereert weer te geven

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

Door deze insight beantwoorde vragen:

- Wat is de relatieve omvang en het aantal van de verschillende rollen in een kans?

+++Selecteer deze optie om de SQL die deze insight genereert weer te geven

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

Door deze insight beantwoorde vragen:

- Wat zijn de top 20 van de mogelijkheden die hun inkomsten (in USD) bieden?

+++Selecteer deze optie om de SQL die deze insight genereert weer te geven

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

Door deze insight beantwoorde vragen:

- Welke open mogelijkheden zijn er en in welk stadium bevinden zich de verkoop of de verkoop van funnel?
- Welke gesloten mogelijkheden zijn er en in welk stadium van de verkoop of marketing van funnel?

+++Selecteer deze optie om de SQL die deze insight genereert weer te geven

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

Door deze insight beantwoorde vragen:

- Wat is het aantal kansen dat met succes is gesloten of afgerond?

+++Selecteer deze optie om de SQL die deze insight genereert weer te geven

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

Door deze insight beantwoorde vragen:

- Hoeveel kansen zijn er in een bepaalde periode met succes afgesloten of afgerond (gewonnen)?

+++Selecteer deze optie om de SQL die deze insight genereert weer te geven

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

## Overzicht van klanten per account {#customers-per-account-overview}

>[!NOTE]
>
>Het [!UICONTROL Customers per Account Overview] -diagram bevat drie doorboor-inzichten: [!UICONTROL Customers per Account Detail], [!UICONTROL Opportunities per Account Overview] en [!UICONTROL Opportunities per Account Detail] . Deze boor-productie verstrekt meer korrelige inzichten, die klanten en opportuniteittellingen door categorieën (zoals directe en indirecte klanten) en waaiers (zoals klant en opportuniteitentellingen) verdelen. Deze grafieken worden niet beïnvloed door globale datumfilters u kunt plaatsen.

Door deze insight beantwoorde vragen:

- Wat is de verdeling van de rekeningen op basis van de vraag of zij directe of indirecte klanten hebben?

+++Selecteer deze optie om de SQL die deze insight genereert weer te geven

```sql
WITH LatestDate AS (SELECT MAX(inserted_date) AS max_inserted_date FROM adwh_b2b_account_person_association),
     CategorizedData AS (
         SELECT CASE 
                    WHEN is_direct = 'true' AND person_count = 0 THEN 'Accounts without Direct Customers' 
                    WHEN is_direct = 'false' AND person_count = 0 THEN 'Accounts without Indirect Customers' 
                    WHEN is_direct = 'true' AND person_count > 0 THEN 'Accounts with Direct Customers' 
                    WHEN is_direct = 'false' AND person_count > 0 THEN 'Accounts with Indirect Customers' 
                END AS Account_Category, 
                account_count 
         FROM adwh_b2b_account_person_association 
         WHERE inserted_date = (SELECT max_inserted_date FROM LatestDate)
     ),
     AggregatedData AS (
         SELECT Account_Category, SUM(account_count) AS Accounts 
         FROM CategorizedData 
         GROUP BY Account_Category
     ),
     AllCategories AS (
         SELECT 'Accounts without Direct Customers' AS Account_Category 
         UNION ALL SELECT 'Accounts without Indirect Customers' 
         UNION ALL SELECT 'Accounts with Direct Customers' 
         UNION ALL SELECT 'Accounts with Indirect Customers'
     )
SELECT ac.Account_Category AS Account_Category, COALESCE(ad.Accounts, 0) AS Accounts 
FROM AllCategories ac 
LEFT JOIN AggregatedData ad ON ac.Account_Category = ad.Account_Category 
ORDER BY ac.Account_Category;
```

+++

## Klanten per accountgegevens {#customers-per-account-detail}

>[!NOTE]
>
>Deze insight wordt niet beïnvloed door globale datumfilters.

Door deze insight beantwoorde vragen:

- Hoeveel rekeningen hebben verschillende waaier van directe of indirecte klanten?

+++Selecteer deze optie om de SQL die deze insight genereert weer te geven

```sql
WITH customer_ranges AS (
    SELECT 'Direct Customer' AS customer_type, '1-10 Customers' AS person_range 
    UNION ALL
    SELECT 'Direct Customer', '11-100 Customers' 
    UNION ALL
    SELECT 'Direct Customer', '101-1000 Customers' 
    UNION ALL
    SELECT 'Direct Customer', '1000+ Customers' 
    UNION ALL
    SELECT 'Indirect Customer', '1-10 Customers' 
    UNION ALL
    SELECT 'Indirect Customer', '11-100 Customers' 
    UNION ALL
    SELECT 'Indirect Customer', '101-1000 Customers' 
    UNION ALL
    SELECT 'Indirect Customer', '1000+ Customers'
)
SELECT 
    cr.customer_type, 
    cr.person_range, 
    COALESCE(SUM(ap.account_count), 0) AS Accounts
FROM customer_ranges cr
LEFT JOIN (
    SELECT 
        CASE 
            WHEN is_direct = 'true' THEN 'Direct Customer' 
            ELSE 'Indirect Customer' 
        END AS customer_type,
        CASE 
            WHEN person_count BETWEEN 1 AND 10 THEN '1-10 Customers' 
            WHEN person_count BETWEEN 11 AND 100 THEN '11-100 Customers' 
            WHEN person_count BETWEEN 101 AND 1000 THEN '101-1000 Customers' 
            WHEN person_count > 1000 THEN '1000+ Customers' 
        END AS person_range,
        SUM(account_count) AS account_count
    FROM adwh_b2b_account_person_association 
    WHERE inserted_date = (SELECT MAX(inserted_date) FROM adwh_b2b_account_person_association) 
    GROUP BY 
        CASE 
            WHEN is_direct = 'true' THEN 'Direct Customer' 
            ELSE 'Indirect Customer' 
        END,
        CASE 
            WHEN person_count BETWEEN 1 AND 10 THEN '1-10 Customers' 
            WHEN person_count BETWEEN 11 AND 100 THEN '11-100 Customers' 
            WHEN person_count BETWEEN 101 AND 1000 THEN '101-1000 Customers' 
            WHEN person_count > 1000 THEN '1000+ Customers' 
        END
) ap ON cr.customer_type = ap.customer_type AND cr.person_range = ap.person_range
GROUP BY cr.customer_type, cr.person_range
ORDER BY cr.customer_type, 
    CASE cr.person_range 
        WHEN '1-10 Customers' THEN 1 
        WHEN '11-100 Customers' THEN 2 
        WHEN '101-1000 Customers' THEN 3 
        WHEN '1000+ Customers' THEN 4 
    END;
```

+++

## Overzicht van mogelijkheden per account {#opportunities-per-account-overview}

>[!NOTE]
>
>Deze insight wordt niet beïnvloed door globale datumfilters.

Door deze insight beantwoorde vragen:

- Wat is de verdeling van de rekeningen op basis van de vraag of zij daaraan mogelijkheden hebben?

+++Selecteer deze optie om de SQL die deze insight genereert weer te geven

```sql
WITH LatestDate AS (
    SELECT MAX(inserted_date) AS max_inserted_date 
    FROM adwh_b2b_account_opportunity_association
),
CategorizedData AS (
    SELECT 
        CASE 
            WHEN opportunity_count = 0 THEN 'Accounts without Opportunities'
            WHEN opportunity_count > 0 THEN 'Accounts with Opportunities'
        END AS Opportunity_Category, 
        account_count 
    FROM adwh_b2b_account_opportunity_association 
    WHERE inserted_date = (SELECT max_inserted_date FROM LatestDate)
),
AggregatedData AS (
    SELECT 
        Opportunity_Category,
        SUM(account_count) AS Accounts 
    FROM CategorizedData 
    GROUP BY Opportunity_Category
),
AllCategories AS (
    SELECT 'Accounts without Opportunities' AS Opportunity_Category 
    UNION ALL 
    SELECT 'Accounts with Opportunities'
)
SELECT 
    ac.Opportunity_Category AS Opportunity_Category, 
    COALESCE(ad.Accounts, 0) AS Accounts 
FROM AllCategories ac 
LEFT JOIN AggregatedData ad 
    ON ac.Opportunity_Category = ad.Opportunity_Category 
ORDER BY ac.Opportunity_Category;
```

+++

## Opportuniteiten per accountdetails {#opportunities-per-account-detail}

>[!NOTE]
>
>Deze insight wordt niet beïnvloed door globale datumfilters.

Door deze insight beantwoorde vragen:

- Hoeveel rekeningen hebben verschillende waaier van bijbehorende kansen?

+++Selecteer deze optie om de SQL die deze insight genereert weer te geven

```sql
WITH opportunity_ranges AS (
    SELECT '1-10 Opportunities' AS opportunity_range 
    UNION ALL 
    SELECT '11-50 Opportunities' 
    UNION ALL 
    SELECT '51-100 Opportunities' 
    UNION ALL 
    SELECT '100+ Opportunities'
)
SELECT opportunity_ranges.opportunity_range AS OPPORTUNITIES, 
       COALESCE(SUM(accounts.total_accounts), 0) AS ACCOUNTS 
FROM opportunity_ranges 
LEFT JOIN (
    SELECT 
        CASE 
            WHEN opportunity_count BETWEEN 1 AND 10 THEN '1-10 Opportunities' 
            WHEN opportunity_count BETWEEN 11 AND 50 THEN '11-50 Opportunities' 
            WHEN opportunity_count BETWEEN 51 AND 100 THEN '51-100 Opportunities' 
            WHEN opportunity_count > 100 THEN '100+ Opportunities' 
        END AS opportunity_range, 
        SUM(account_count) AS total_accounts 
    FROM adwh_b2b_account_opportunity_association 
    WHERE inserted_date = (SELECT MAX(inserted_date) FROM adwh_b2b_account_opportunity_association) 
      AND opportunity_count > 0 
    GROUP BY 
        CASE 
            WHEN opportunity_count BETWEEN 1 AND 10 THEN '1-10 Opportunities' 
            WHEN opportunity_count BETWEEN 11 AND 50 THEN '11-50 Opportunities' 
            WHEN opportunity_count BETWEEN 51 AND 100 THEN '51-100 Opportunities' 
            WHEN opportunity_count > 100 THEN '100+ Opportunities' 
        END
) AS accounts ON opportunity_ranges.opportunity_range = accounts.opportunity_range 
GROUP BY opportunity_ranges.opportunity_range 
ORDER BY CASE opportunity_ranges.opportunity_range 
            WHEN '1-10 Opportunities' THEN 1 
            WHEN '11-50 Opportunities' THEN 2 
            WHEN '51-100 Opportunities' THEN 3 
            WHEN '100+ Opportunities' THEN 4 
        END;
```

+++

## Volgende stappen

Door dit document te lezen, begrijpt u nu de SQL die dashboardinzichten van het accountprofiel produceert en welke gemeenschappelijke vragen deze analyse oplost. U kunt nu de SQL bewerken en doorlopen om uw eigen inzichten te genereren. Verwijs naar het [ Pro overzicht van de Wijze van de Vraag ](../sql-insights-query-pro-mode/overview.md) om te leren hoe te om douaneinzichten met SQL te produceren.

U kunt SQL ook lezen en begrijpen die inzichten voor de [ Profielen ](./profiles.md), [ Soorten publiek ](./audiences.md), en [ Doelen ](./destinations.md) dashboards van Doelen produceert.
