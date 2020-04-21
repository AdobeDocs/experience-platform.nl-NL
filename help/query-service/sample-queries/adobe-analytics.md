---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Voorbeeldquery's
topic: queries
translation-type: tm+mt
source-git-commit: 75c446aed75100bd2b5b4a3d365c090cb01dcc69

---


# Voorbeeldquery&#39;s voor Adobe Analytics-gegevens

Gegevens uit geselecteerde Adobe Analytics-rapportreeksen worden getransformeerd in XDM ExperienceEvents en opgenomen in Adobe Experience Platform als datasets voor u. In dit document wordt een aantal gebruiksgevallen beschreven waarin Adobe Experience Platform Query Service van deze gegevens gebruikmaakt en de meegeleverde voorbeeldquery&#39;s zouden moeten werken met uw Adobe Analytics-gegevenssets. Zie de documentatie [van de het gebiedstoewijzing van](../../sources/connectors/adobe-applications/mapping/analytics.md) Analytics voor meer informatie over afbeelding aan XDM ExperienceEvents.

## Aan de slag

De SQL voorbeelden door dit document vereisen u om SQL uit te geven en de verwachte parameters voor uw vragen in te vullen die op de dataset, eVar, gebeurtenis, of tijdkader worden gebaseerd u in het evalueren geinteresseerd bent. Geef parameters op `{ }` in de volgende SQL-voorbeelden.

## Algemeen gebruikte SQL-voorbeelden

### Aantal uren bezoekers voor een bepaalde dag

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count 
FROM   {target_table}
WHERE _acp_year = {target_year} 
      AND _acp_month = {target_month}  
      AND _acp_day = {target_day}
GROUP BY Day, Hour
ORDER BY Hour;
```

### De bovenste tien weergegeven pagina&#39;s voor een bepaalde dag

```sql
SELECT web.webpagedetails.name AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP BY web.webpagedetails.name 
ORDER BY page_views DESC 
LIMIT  10;
```

### De tien meest actieve gebruikers

```sql
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp) AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### Top 10 steden per gebruikersactiviteit

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp) AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP BY state_city
ORDER BY Count DESC
LIMIT  10;
```

### De tien meest bekeken producten

```sql
SELECT Product_SKU,
       Sum(Product_Views) AS Total_Product_Views
FROM  (SELECT Explode(productlistitems.sku) AS Product_SKU, 
              commerce.productviews.value   AS Product_Views 
       FROM   {target_table}
       WHERE  _acp_year = {target_year}
              AND _acp_month = {target_month}
              AND _acp_day = {target_day}
              AND commerce.productviews.value IS NOT NULL) 
GROUP BY Product_SKU 
ORDER BY Total_Product_Views DESC
LIMIT  10;
```

### Top 10 van totale orderontvangsten

```sql
SELECT Purchase_ID, 
       Round(Sum(Product_Items.priceTotal * Product_Items.quantity), 2) AS Total_Order_Revenue 
FROM   (SELECT commerce.`order`.purchaseid AS Purchase_ID, 
               Explode(productlistitems)   AS Product_Items 
        FROM   {target_table} 
        WHERE  commerce.`order`.purchaseid IS NOT NULL 
               AND _acp_year = {target_year} 
               AND _acp_month = {target_month}  
               AND _acp_day = {target_day}) 
GROUP BY Purchase_ID 
ORDER BY total_order_revenue DESC 
LIMIT  10;
```

### Aantal gebeurtenissen per dag

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day, 
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Sum(_experience.analytics.event1to100.{target_event}.value) AS Event_Count
FROM   {target_table}
WHERE  _experience.analytics.event1to100.{target_event}.value IS NOT NULL 
        AND _acp_year = {target_year} 
        AND _acp_month = {target_month}  
        AND _acp_day = {target_day}
GROUP BY Day, Hour
ORDER BY Hour;
```

## Merchandising-variabelen (productsyntaxis)

In Adobe Analytics kunnen gegevens op productniveau worden verzameld via speciaal geconfigureerde variabelen, genaamd &#39;Merchandising Variables&#39;. Deze zijn gebaseerd op een eVar of een Gebeurtenis van de Douane. Het verschil tussen deze variabelen en hun standaardgebruik is dat ze een afzonderlijke waarde vertegenwoordigen voor elk product dat op de hit wordt gevonden, in plaats van slechts één waarde voor de hit. Deze variabelen worden bedoeld als Variabelen van de Verkoop van de Syntaxis van het Product. Op deze manier kunt u informatie verzamelen zoals een &quot;kortingsbedrag&quot; per product of informatie over de &quot;locatie op pagina&quot; van het product in de zoekresultaten van de klant.

Hier zijn de gebieden XDM om tot de merchandising variabelen in uw dataset van Analytics toegang te hebben:

### eVars

```
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

Waar `[#]` is een arrayindex en `evar#` is de specifieke eVar-variabele.

### Aangepaste gebeurtenissen

```
productListItems[#]._experience.analytics.event1to100.event#.value
```

Waar `[#]` is een arrayindex en `event#` is de specifieke aangepaste gebeurtenisvariabele.

### Voorbeeldquery&#39;s

Hier is een steekproefvraag die een handelende eVar en een gebeurtenis terugkeert voor het eerste product dat in `productListItems`wordt gevonden.

```sql
SELECT
  productListItems[0]._experience.analytics.customDimensions.evars.eVar1,
  productListItems[0]._experience.analytics.event1to100.event1.value
FROM adobe_analytics_midvalues
WHERE _ACP_YEAR=2019 AND _ACP_MONTH=7 AND _ACP_DAY=23
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
LIMIT 10
```

Deze volgende query &#39;explodeert&#39; de `productListItems` en retourneert elke koopwaar en gebeurtenis per product. Het `_id` veld wordt opgenomen om de relatie met de oorspronkelijke hit weer te geven. De `_id` waarde is een unieke primaire sleutel in de dataset ExperienceEvent.

```sql
SELECT
  _id,
  productItem._experience.analytics.customDimensions.evars.eVar1,
  productItem._experience.analytics.event1to100.event1.value
FROM (
  SELECT
    _id,
    explode(productListItems) as productItem
  FROM adobe_analytics_midvalues
  WHERE _ACP_YEAR=2019 AND _ACP_MONTH=7 AND _ACP_DAY=23
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
)
LIMIT 20
```

### Algemene fout bij het implementeren van voorbeeldquery&#39;s

De fout &quot;Geen dergelijk struct gebied&quot;wordt ontmoet wanneer u probeert om een gebied terug te winnen dat niet in uw huidige dataset bestaat. Evalueer de reden die in het foutenbericht is teruggekeerd om een beschikbaar gebied te identificeren dan uw vraag bij te werken en opnieuw te herhalen.

```
ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
```

## Merchandising-variabelen (conversiesyntaxis)

Een ander type van een Merchandising Variabele die in de Analyse van Adobe wordt gevonden is Syntaxis van de Omzetting. Met de Syntaxis van het Product wordt de waarde verzameld tezelfdertijd zoals het product maar dit vereist dat de gegevens op de zelfde pagina aanwezig zijn. Er zijn scenario&#39;s waarin de gegevens op een pagina vóór de conversie of het geval van belang met betrekking tot het product voorkomen. Neem bijvoorbeeld het gebruik van het rapportvoorbeeld van de productzoekmethode.

1. Een gebruiker voert en intern onderzoek naar &quot;winterhoed&quot;uit die de Syntaxis van de Omzetting toeliet Verkeer eVar6 aan &quot;intern onderzoek:winterhoed&quot;
2. De gebruiker klikt op &quot;wafelbeanie&quot; en landt op de pagina met productdetails.\
   a. Het landen hier vuurt een `Product View` evenement voor de &quot;wafelbeenie&quot; voor $12,99.\
   b. Omdat `Product View` is geconfigureerd als een bindingsgebeurtenis, is het product &quot;waffle beanie&quot; nu gebonden aan de waarde eVar6 van &quot;internal search:winter hat&quot;. Telkens wanneer het product &quot;waffle beanie&quot; wordt verzameld, wordt het gekoppeld aan &quot;internal search:winter hat&quot; totdat (1) de instelling voor verlopen is bereikt of (2) een nieuwe eVar6-waarde is ingesteld en de gebeurtenis binding met dat product opnieuw plaatsvindt.
3. De gebruiker voegt het product aan zijn winkelwagentje toe en start het `Cart Add` evenement.
4. De gebruiker voert een andere interne zoekopdracht uit naar &quot;zomershirt&quot; waarmee de omzettingssyntaxis eVar6 instelt op &quot;intern zoeken:zomershirt&quot;
5. De gebruiker klikt op &quot;sporty t-shirt&quot; en landt op de pagina met productdetails.\
   a. Het landen hier vuurt een `Product View` evenement voor &quot;sporty t-shirt voor $19,99.\
   b. Het `Product View` evenement is nog steeds ons bindende evenement, dus nu is het product &quot;sporty t-shirt&quot; nu gebonden aan de waarde eVar6 van &quot;internal search:zomer shirt&quot; en het eerdere product &quot;waffle beanie&quot; is nog steeds gebonden aan de waarde eVar6 van &quot;internal search:waffle beanie&quot;.
6. De gebruiker voegt het product aan zijn winkelwagentje toe en start het `Cart Add` evenement.
7. De gebruiker checkt beide producten uit.

Bij de rapportage worden de orders, inkomsten, productweergaven en carttoevoegingen tegen eVar6 gemeld en afgestemd op de activiteit van het gebonden product.

| eVar6 (methode voor het zoeken van producten) | inkomsten | orders | productweergave | cartografische objecten |
|---|---|---|---|---|
| intern zoeken:zomershirt | 19.99 | 1 | 1 | 1 |
| interne zoekopdracht:winterhoed | 12.99 | 1 | 1 | 1 |

Hier zijn de XDM gebieden om de Syntaxis van de Omzetting in uw dataset van Analytics te veroorzaken:

### eVars

```
_experience.analytics.customDimensions.evars.evar#
```

Waar `evar#` is de specifieke variabele eVar.

### Product

```
productListItems[#].sku
```

Waar `[#]` is een arrayindex.

### Voorbeeldquery&#39;s

Hier is een steekproefvraag die de waarde aan het specifieke product en gebeurtenispaar bindt, in dit geval de gebeurtenis van de productmening.

```sql
SELECT
  endUserIds._experience.aaid.id AS AAID,
  timestamp,
  CASE WHEN commerce.productViews.value = 1 THEN ATTRIBUTION_LAST_TOUCH(timestamp, 'bindConversionSyntaxMerchVariable_eVar1', _experience.analytics.customDimensions.eVars.eVar1)
  OVER(PARTITION BY endUserIds._experience.aaid.id
       ORDER BY timestamp
       ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
  END AS eVar1Bind,
  EXPLODE(productListItems) AS Product_List,
  commerce.productViews.value AS prodView,
  commerce.purchases.value AS purchase
FROM adobe_analytics_midvalues
WHERE commerce.productViews.value = 1 OR commerce.purchases.value = 1 OR _experience.analytics.customDimensions.eVars.eVar1 IS NOT NULL
LIMIT 100
```

Hier volgt een voorbeeldquery waarin de gebonden waarde wordt doorgevoerd in volgende exemplaren van het desbetreffende product. De laagste subquery vestigt de waardenrelatie met het product op de gedeclareerde bindingsgebeurtenis. De volgende subquery voert de toewijzing van die gebonden waarde uit voor volgende interacties met het desbetreffende product. En het hoogste niveau selecteert aggregeert de resultaten om de rapportering te produceren.

```sql
SELECT
  Product_List.SKU,
  eVar1101ConversionSyntax,
  SUM(prodView) AS Product_Views,
  SUM(purchase) AS Purchases
FROM
(
  SELECT
    Product_List,
    ATTRIBUTION_LAST_TOUCH(timestamp, 'ConversionSyntax_eVar1', eVar1Bind)
      OVER(PARTITION BY AAID, Product_List.SKU
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
    AS eVar1ConversionSyntax,
    prodView,
    purchase
  FROM
  (
    SELECT
      endUserIds._experience.aaid.id AS AAID,
      timestamp,
      CASE WHEN commerce.productViews.value = 1 THEN ATTRIBUTION_LAST_TOUCH(timestamp, 'bindConversionSyntaxMerchVariable_eVar1', _experience.analytics.customDimensions.eVars.eVar1)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
      END AS eVar1Bind,
      EXPLODE(productListItems) AS Product_List,
      commerce.productViews.value AS prodView,
      commerce.purchases.value AS purchase
    FROM adobe_analytics_midvalues
    WHERE commerce.productViews.value = 1 OR commerce.purchases.value = 1 OR _experience.analytics.customDimensions.eVars.eVar1 IS NOT NULL
  )
)
WHERE eVar1ConversionSyntax IS NOT NULL
GROUP BY 1, 2
ORDER BY 3 DESC
LIMIT 100
```
