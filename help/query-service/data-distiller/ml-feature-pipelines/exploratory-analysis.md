---
title: Analyse van verkennende gegevens
description: Leer hoe u Data Distiller kunt gebruiken om gegevens van een Python-laptop te verkennen en te analyseren.
exl-id: 1dd4cf6e-f7cc-4f4b-afbd-bfc1d342a2c3
source-git-commit: f9c49dbcc1820cf70c85368114c2a1ab30b87807
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 14%

---

# Verkennende gegevensanalyse

Dit document bevat enkele basisvoorbeelden en aanbevolen procedures voor het gebruik van Data Distiller voor het verkennen en analyseren van gegevens van een [!DNL Python] -laptop.

## Aan de slag

Voordat u verdergaat met deze handleiding, moet u controleren of u een verbinding met Data Distiller hebt gemaakt in uw [!DNL Python] -laptop. Zie de documentatie voor instructies over hoe u kunt [een verbinding maken [!DNL Python] notebook naar Data Distiller](./establish-connection.md).

## Verkrijgen van basisstatistieken {#basic-statistics}

Gebruik de code hieronder om het aantal rijen en verschillende profielen in een dataset terug te winnen.

```python
table_name = 'ecommerce_events'

basic_statistics_query = f"""
SELECT
    COUNT(_id) as "totalRows",
    COUNT(DISTINCT _id) as "distinctUsers"
FROM {table_name}"""

df = qs_cursor.query(basic_statistics_query, output="dataframe")
df
```

**Voorbeelduitvoer**

|     | totalRows | differentUsers |
| --- | ----------- | -------------- |
| 0 | 1276563 | 1276563 |

## Een gesamplede versie van grote gegevenssets maken {#create-dataset-sample}

Als de dataset u wenst te vragen zeer groot is, of als de nauwkeurige resultaten van verkennende vragen niet noodzakelijk zijn, gebruik [bemonsteringsfunctionaliteit](../../essential-concepts/dataset-samples.md) beschikbaar voor Distiller-query&#39;s voor gegevens. Dit is een proces in twee stappen:

- Eerste, **analyseren** de dataset om een bemonsterde versie met een gespecificeerde steekproefverhouding te creëren
- Daarna, vraag de bemonsterde versie van de dataset. Afhankelijk van de functies die u op de gesamplede dataset toepast, kunt u de uitvoer naar de getallen schalen naar de volledige dataset

### Een 5%-voorbeeld maken {#create-sample}

In het onderstaande voorbeeld wordt de gegevensset geanalyseerd en wordt een monster van 5% gemaakt:

```python
# A sampling rate of 10 is 100% in Query Service, so for 5% use a sampling rate 0.5
sampling_rate = 0.5

analyze_table_query=f"""
SET aqp=true;
ANALYZE TABLE {table_name} TABLESAMPLE SAMPLERATE {sampling_rate}"""

qs_cursor.query(analyze_table_query, output="raw")
```

### Bekijk uw voorbeelden {#view-sample}

U kunt de `sample_meta` functie om het even welke steekproeven te bekijken die van een bepaalde dataset zijn gecreeerd. In het codefragment hieronder ziet u hoe u het `sample_meta` functie.

```python
sampled_version_of_table_query = f'''SELECT sample_meta('{table_name}')'''

df_samples = qs_cursor.query(sampled_version_of_table_query, output="dataframe")
df_samples
```

**Voorbeelduitvoer**:

|   | sample_table_name | sample_dataset_id | parent_dataset_id | sample_type | sampling_rate | filter_condition_on_source_dataset | sample_num_rows | gemaakt |
|---|---|---|---|---|---|---|---|---|
| 0 | cmle_synthetische_data_experience_event_dataset_c... | 650f7a09ed6c3e28d34d7fc2 | 64fb4d7a7d748828d304a2f4 | uniform | 0.5 | 6427 | 23/09/2023 | 11:51:37 |

{style="table-layout:auto"}

### Vraag uw voorbeeld {#query-sample-data}

U kunt uw steekproef direct vragen door de naam van de steekproeflijst van de teruggekeerde meta-gegevens van verwijzingen te voorzien. Vervolgens kunt u de resultaten vermenigvuldigen met de bemonsteringsverhouding om een schatting te krijgen.

```python
sample_table_name = df_samples[df_samples["sampling_rate"] == sampling_rate]["sample_table_name"].iloc[0]

count_query=f'''SELECT count(*) as cnt from {sample_table_name}'''

df = qs_cursor.query(count_query, output="dataframe")
# Divide by the sampling rate to extrapolate to the full dataset
approx_count = df["cnt"].iloc[0] / (sampling_rate / 100)

print(f"Approximate count: {approx_count} using {sampling_rate *10}% sample")
```

**Voorbeelduitvoer**

```console
Approximate count: 1284600.0 using 5.0% sample
```

## Analyse van e-mailtrechter {#email-funnel-analysis}

Een trechter-analyse is een methode om te begrijpen welke stappen nodig zijn om een doelresultaat te bereiken en hoeveel gebruikers elk van deze stappen doorlopen. In het onderstaande voorbeeld ziet u een eenvoudige trechter-analyse van de stappen die leiden tot een gebruiker die zich abonneert op een nieuwsbrief. Het resultaat van het abonnement wordt weergegeven als een gebeurtenistype van `web.formFilledOut`.

Eerst, stel een vraag in werking om het aantal gebruikers bij elke stap te krijgen.

```python
simple_funnel_analysis_query = f'''SELECT eventType, COUNT(DISTINCT _id) as "distinctUsers",COUNT(_id) as "distinctEvents" FROM {table_name} GROUP BY eventType ORDER BY distinctUsers DESC'''

funnel_df = qs_cursor.query(simple_funnel_analysis_query, output="dataframe")
funnel_df
```

**Voorbeelduitvoer**

|   | eventType | differentUsers | differentEvents |
|---|---|---|---|
| 0 | directMarketing.emailSent | 598840 | 598840 |
| 1 | directMarketing.emailOpened | 239028 | 239028 |
| 2 | web.webpagedetails.pageViews | 120118 | 120118 |
| 3 | advertising.impressions | 119669 | 119669 |
| 4 | directMarketing.emailClicked | 51581 | 51581 |
| 5 | commerce.productViews | 37915 | 37915 |
| 6 | decisioning.propositionDisplay | 37650 | 37650 |
| 7 | web.webinteraction.linkClicks | 37581 | 37581 |
| 8 | web.formFilledOut | 17860 | 17860 |
| 9 | advertising.clicks | 7610 | 7610 |
| 10 | decisioning.propositionInteract | 2964 | 2964 |
| 11 | decisioning.propositionDismiss | 2889 | 2889 |
| 12 | commerce.purchases | 2858 | 2858 |

{style="table-layout:auto"}

### Zoekresultaten voor plotten {#plot-results}

Vervolgens plaatst u de queryresultaten met de [!DNL Python] `plotly` bibliotheek:

```python
import plotly.express as px

email_funnel_events = ["directMarketing.emailSent", "directMarketing.emailOpened", "directMarketing.emailClicked", "web.formFilledOut"]
email_funnel_df = funnel_df[funnel_df["eventType"].isin(email_funnel_events)]

fig = px.funnel(email_funnel_df, y='eventType', x='distinctUsers')
fig.show()
```

**Voorbeelduitvoer**

![An infographic of the eventType email trechter.](../../images/data-distiller/email-funnel.png)

## Gebeurteniscorrelaties {#event-correlations}

Een andere algemene analyse is het berekenen van correlaties tussen gebeurtenistypen en een gebeurtenistype voor doelconversie. In dit voorbeeld wordt de abonnementsgebeurtenis vertegenwoordigd door `web.formFilledOut`. In dit voorbeeld wordt het [!DNL Spark] functies beschikbaar in de vragen van Distiller van Gegevens om de volgende stappen te bereiken:

1. Telt het aantal gebeurtenissen voor elk gebeurtenistype door profiel.
2. De tellingen van elk gebeurtenistype over profielen samenvoegen en de correlaties van elk gebeurtenistype berekenen met `web,formFilledOut`.
3. Transformeer het dataframe van tellingen en correlaties in een lijst van de Coëfficiënten van de Correlatie van Pearson van elke eigenschap (gebeurtenistype tellingen) met de doelgebeurtenis.
4. U kunt de resultaten in een waarnemingspunt visualiseren.

De [!DNL Spark] De functies voegen de gegevens samen om een kleine lijst van resultaten terug te keren, zodat kunt u dit type van vraag op de volledige dataset uitvoeren.

```python
large_correlation_query=f'''
SELECT SUM(webFormsFilled) as webFormsFilled_totalUsers,
       SUM(advertisingClicks) as advertisingClicks_totalUsers,
       SUM(productViews) as productViews_totalUsers,
       SUM(productPurchases) as productPurchases_totalUsers,
       SUM(propositionDismisses) as propositionDismisses_totaUsers,
       SUM(propositionDisplays) as propositionDisplays_totaUsers,
       SUM(propositionInteracts) as propositionInteracts_totalUsers,
       SUM(emailClicks) as emailClicks_totalUsers,
       SUM(emailOpens) as emailOpens_totalUsers,
       SUM(webLinkClicks) as webLinksClicks_totalUsers,
       SUM(webPageViews) as webPageViews_totalusers,
       corr(webFormsFilled, emailOpens) as webForms_EmailOpens,
       corr(webFormsFilled, advertisingClicks) as webForms_advertisingClicks,
       corr(webFormsFilled, productViews) as webForms_productViews,
       corr(webFormsFilled, productPurchases) as webForms_productPurchases,
       corr(webFormsFilled, propositionDismisses) as webForms_propositionDismisses,
       corr(webFormsFilled, propositionInteracts) as webForms_propositionInteracts,
       corr(webFormsFilled, emailClicks) as webForms_emailClicks,
       corr(webFormsFilled, emailOpens) as webForms_emailOpens,
       corr(webFormsFilled, emailSends) as webForms_emailSends,
       corr(webFormsFilled, webLinkClicks) as webForms_webLinkClicks,
       corr(webFormsFilled, webPageViews) as webForms_webPageViews
FROM(
    SELECT _{tenant_id}.cmle_id as userID,
            SUM(CASE WHEN eventType='web.formFilledOut' THEN 1 ELSE 0 END) as webFormsFilled,
            SUM(CASE WHEN eventType='advertising.clicks' THEN 1 ELSE 0 END) as advertisingClicks,
            SUM(CASE WHEN eventType='commerce.productViews' THEN 1 ELSE 0 END) as productViews,
            SUM(CASE WHEN eventType='commerce.productPurchases' THEN 1 ELSE 0 END) as productPurchases,
            SUM(CASE WHEN eventType='decisioning.propositionDismiss' THEN 1 ELSE 0 END) as propositionDismisses,
            SUM(CASE WHEN eventType='decisioning.propositionDisplay' THEN 1 ELSE 0 END) as propositionDisplays,
            SUM(CASE WHEN eventType='decisioning.propositionInteract' THEN 1 ELSE 0 END) as propositionInteracts,
            SUM(CASE WHEN eventType='directMarketing.emailClicked' THEN 1 ELSE 0 END) as emailClicks,
            SUM(CASE WHEN eventType='directMarketing.emailOpened' THEN 1 ELSE 0 END) as emailOpens,
            SUM(CASE WHEN eventType='directMarketing.emailSent' THEN 1 ELSE 0 END) as emailSends,
            SUM(CASE WHEN eventType='web.webinteraction.linkClicks' THEN 1 ELSE 0 END) as webLinkClicks,
            SUM(CASE WHEN eventType='web.webinteraction.pageViews' THEN 1 ELSE 0 END) as webPageViews
    FROM {table_name}
    GROUP BY userId
)
'''
large_correlation_df = qs_cursor.query(large_correlation_query, output="dataframe")
large_correlation_df
```

**Voorbeelduitvoer**:

|   | webFormsFilled_totalUsers | advertentieKliks_totalUsers | productViews_totalUsers | productPurchases_totalUsers | propositionDisses_totaUsers | propositionDisplay_totaUsers | propositionInteracts_totalUsers | emailClicks_totalUsers | emailOpens_totalUsers | webLinksClicks_totalUsers | ... | webForms_advertenceClicks | webForms_productViews | webForms_productPurchases | webForms_propositionDisses | webForms_propositionInteracts | webForms_emailClicks | webForms_emailOpens | webForms_emailSends | webForms_webLinkClicks | webForms_webPageViews |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 17860 | 7610 | 37915 | 0 | 2889 | 37650 | 2964 | 51581 | 239028 | 37581 | … | 0.026805 | 0.2779 | Geen | 0.06014 | 0.143656 | 0.305657 | 0.218874 | 0.192836 | 0.259353 | Geen |

{style="table-layout:auto"}

### Rij omzetten in correlatie van gebeurtenistype {#event-type-correlation}

Daarna, zet de enige rij gegevens in de vraagoutput hierboven om in een lijst die de correlaties van elk gebeurtenistype met de gebeurtenis van het doelabonnement toont:

```python
cols = large_correlation_df.columns
corrdf = large_correlation_df[[col for col in cols if ("webForms_"  in col)]].melt()
corrdf["feature"] = corrdf["variable"].apply(lambda x: x.replace("webForms_", ""))
corrdf["pearsonCorrelation"] = corrdf["value"]

corrdf.fillna(0)
```

**Voorbeelduitvoer**:

|    | variabel | value | functie | pearsonCorrelation |
| --- | ---  |  ---  |  ---  | --- |
| 0 | `webForms_EmailOpens` | 0.218874 | EmailOpens | 0.218874 |
| 1 | `webForms_advertisingClicks` | 0.026805 | adverterenKliks | 0.026805 |
| 2 | `webForms_productViews` | 0.277900 | productViews | 0.277900 |
| 3 | `webForms_productPurchases` | 0.000000 | productPurchases | 0.000000 |
| 4 | `webForms_propositionDismisses` | 0.060140 | propositionDisses | 0.060140 |
| 5 | `webForms_propositionInteracts` | 0.143656 | propositionInteracts | 0.143656 |
| 6 | `webForms_emailClicks` | 0.305657 | emailClicks | 0.305657 |
| 7 | `webForms_emailOpens` | 0.218874 | emailOpens | 0.218874 |
| 8 | `webForms_emailSends` | 0.192836 | emailSends | 0.192836 |
| 9 | `webForms_webLinkClicks` | 0.259353 | webLinkClicks | 0.259353 |
| 10 | `webForms_webPageViews` | 0.000000 | webPageViews | 0.000000 |


Tot slot kunt u de correlaties met de `matplotlib` [!DNL Python] bibliotheek:

```python
import matplotlib.pyplot as plt
fig, ax = plt.subplots(figsize=(5,10))
sns.barplot(data=corrdf.fillna(0), y="feature", x="pearsonCorrelation")
ax.set_title("Pearson Correlation of Events with the outcome event")
```

![Een staafgrafiek van de Pearson-correlatie van gebeurtenissen met uitkomsten van gebeurtenissen](../../images/data-distiller/pearson-correlations.png)

## Volgende stappen

Door dit document te lezen, hebt u geleerd hoe u Data Distiller kunt gebruiken om gegevens van een [!DNL Python] -laptop. De volgende stap bij het maken van functiepijpleidingen van Experience Platform naar aangepaste modellen in uw computerleeromgeving is: [engineeringfuncties voor het leren van machines](./feature-engineering.md).
