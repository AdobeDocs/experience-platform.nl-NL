---
title: 'Analytische inzichten voor web- en mobiele interacties '
description: In dit document wordt uitgelegd hoe u Query Service kunt gebruiken om uitvoerbare inzichten te maken op basis van opgenomen Adobe Analytics-gegevens.
source-git-commit: cdceba9caf035831f4c376edf34356f666b79aa8
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Analyseinzichten voor web- en mobiele interacties

Met Adobe Experience Platform kunt u gegevens uit Adobe Analytics-rapportreeksen invoeren met XDM-velden (Experience Data Model) voor het vullen van gegevenssets. De Dienst van de vraag kan dan gebruik van deze analysegegevens maken door SQL vragen in werking te stellen om waardevolle inzichten van een gebruikersgedrag over de digitale platforms te produceren.

Dit document bevat een groot aantal voorbeeld-SQL-query&#39;s die veelvoorkomende gebruiksgevallen aantonen bij het maken van inzichten van gegevens van Analytics via internet en mobiele apparatuur.

Zie de [Documentatie over veldtoewijzingen voor analyses](../../sources/connectors/adobe-applications/mapping/analytics.md) voor meer informatie over het opnemen en toewijzen van analysegegevens.

## Aan de slag

Voor elk van de volgende gebruiksgevallen wordt een geparametriseerd SQL vraagvoorbeeld verstrekt als malplaatje voor u aan te passen. Geef parameters op waar u ze ziet `{ }` in de SQL voorbeelden voor de dataset, de eVar, de gebeurtenis, of het tijdkader u in evaluatie geinteresseerd bent.

## Doelstellingen

In de volgende voorbeelden worden SQL-query&#39;s getoond voor veelvoorkomende gebruiksscenario&#39;s voor het analyseren van uw Adobe Analytics-gegevens.

### Het aantal bezoekers genereren voor elk uur op een bepaalde dag

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour,
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

### De tien meest bekeken pagina&#39;s op een bepaalde dag identificeren

```SQL
SELECT web.webpagedetails.name AS Page_Name,
       Sum(web.webpagedetails.pageviews.value) AS Page_Views
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY web.webpagedetails.name
ORDER BY page_views DESC
LIMIT  10;
```

### De tien meest actieve gebruikers identificeren

```sql
SELECT enduserids._experience.aaid.id AS aaid,
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### De 10 meest gewenste steden identificeren op basis van gebruikersactiviteit

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city,
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY state_city
ORDER BY Count DESC
LIMIT  10;
```

### De tien meest bekeken producten identificeren

```sql
SELECT Product_SKU,
       Sum(Product_Views) AS Total_Product_Views
FROM  (SELECT Explode(productlistitems.sku) AS Product_SKU,
              commerce.productviews.value   AS Product_Views
       FROM   {TARGET_TABLE}
            WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
              AND commerce.productviews.value IS NOT NULL)
GROUP BY Product_SKU
ORDER BY Total_Product_Views DESC
LIMIT  10;
```

### Identificeer de 10 hoogste orderopbrengsten

```sql
SELECT Purchase_ID,
       Round(Sum(Product_Items.priceTotal * Product_Items.quantity), 2) AS Total_Order_Revenue
FROM   (SELECT commerce.`order`.purchaseid AS Purchase_ID,
               Explode(productlistitems)   AS Product_Items
        FROM   {TARGET_TABLE}
        WHERE  commerce.`order`.purchaseid IS NOT NULL
                AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')

GROUP BY Purchase_ID
ORDER BY total_order_revenue DESC
LIMIT  10;
```
