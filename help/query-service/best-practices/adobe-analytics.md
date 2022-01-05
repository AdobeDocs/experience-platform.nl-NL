---
keywords: Experience Platform;huis;populaire onderwerpen;de vraagdienst;de dienst van de Vraag;steekproefvragen;steekproefvraag;adobe analytics;
solution: Experience Platform
title: Voorbeeldquery's voor Adobe Analytics-gegevens
topic-legacy: queries
description: Gegevens uit geselecteerde Adobe Analytics-rapportsuites worden getransformeerd in XDM ExperienceEvents en als datasets voor u opgenomen in Adobe Experience Platform. Dit document schetst een aantal gebruiksgevallen waar de Dienst van de Vraag van Adobe Experience Platform deze gegevens gebruikt, en de inbegrepen steekproefvragen zouden met uw datasets van Adobe Analytics moeten werken.
exl-id: 96da3713-c7ab-41b3-9a9d-397756d9dd07
source-git-commit: b140037ed5f055a8e7c583540910cc6b18bbf0bd
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 1%

---

# Sample queries for Adobe Analytics data

Data from selected Adobe Analytics report suites is transformed into data conforming to the [!DNL XDM ExperienceEvent] class and ingested into Adobe Experience Platform as datasets.

In dit document wordt een aantal gebruiksgevallen beschreven waarbij Adobe Experience Platform [!DNL Query Service] maakt gebruik van deze gegevens, met inbegrip van steekproefvragen zou met uw datasets van Adobe Analytics moeten werken. See the documentation on [Analytics field mapping](../../sources/connectors/adobe-applications/mapping/analytics.md) for more information on mapping to [!DNL Experience Events].

## Aan de slag

De SQL voorbeelden door dit document vereisen u om SQL uit te geven en de verwachte parameters voor uw vragen in te vullen die op de dataset, de eVar, de gebeurtenis, of het tijdkader worden gebaseerd u in het evalueren geinteresseerd bent. Geef parameters op waar u ze ziet `{ }` in de volgende SQL-voorbeelden.

## Algemeen gebruikte SQL-voorbeelden

In de volgende voorbeelden worden veelgebruikte SQL-query&#39;s getoond om uw Adobe Analytics-gegevens te analyseren.

### Aantal uren bezoekers voor een bepaalde dag

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count 
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

### De bovenste tien weergegeven pagina&#39;s voor een bepaalde dag

```sql
SELECT web.webpagedetails.name AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY web.webpagedetails.name 
ORDER BY page_views DESC 
LIMIT  10;
```

### Top 10 most active users

```sql
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### Top 10 steden per gebruikersactiviteit

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
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
       FROM   {TARGET_TABLE}
            WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
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
        FROM   {TARGET_TABLE} 
        WHERE  commerce.`order`.purchaseid IS NOT NULL 
                AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')

GROUP BY Purchase_ID 
ORDER BY total_order_revenue DESC 
LIMIT  10;
```

### Aantal gebeurtenissen per dag

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day, 
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Sum(_experience.analytics.event1to100.{TARGET_EVENT}.value) AS Event_Count
FROM   {TARGET_TABLE}
WHERE  _experience.analytics.event1to100.{TARGET_EVENT}.value IS NOT NULL 
        AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

## Deduplicatie

Adobe Experience Platform Query Service supports data deduplication. Zie de [Gegevensdeduplicatie in de documentatie van de Dienst van de Vraag](./deduplication.md) voor informatie over hoe u nieuwe waarden kunt genereren op het moment dat u een query uitvoert [!DNL Experience Event] datasets.

## Merchandising-variabelen (productsyntaxis)


### Product syntax

In Adobe Analytics kunnen aangepaste productgegevens worden verzameld via speciaal geconfigureerde variabelen, de zogenaamde &#39;merchandising&#39;-variabelen. These are based on either an eVar or custom events. The difference between these variables and their standard use is that they represent a separate value for each product found on the hit rather than only a single value for the hit.

Deze variabelen worden ook wel handelsvariabelen in de productsyntaxis genoemd. This allows for collection of information, such as a per product &quot;discount amount&quot; or information about the product&#39;s &quot;location on page&quot; in the customer&#39;s search results.

To learn more about using the product syntax, please read the Adobe Analytics documentation on [implementing eVars using product syntax](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-product-syntax).

In de onderstaande secties worden de XDM-velden beschreven die nodig zijn voor toegang tot de handelsvariabelen in uw [!DNL Analytics] gegevensset:

#### eVars

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

- `#`: De index van de array die u opent.
- `evar#`: De specifieke variabele van de eVar die u toegang hebt.

#### Aangepaste gebeurtenissen

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

- `#`: De index van de array die u opent.
- `event#`: De specifieke variabele van de douanegebeurtenis die u toegang hebt.

#### Voorbeeldquery&#39;s

Here is a sample query returning a merchandising eVar and event for the first product found in the `productListItems`.

```sql
SELECT
  productListItems[0]._experience.analytics.customDimensions.evars.eVar1,
  productListItems[0]._experience.analytics.event1to100.event1.value
FROM adobe_analytics_midvalues
WHERE timestamp = to_timestamp('2019-07-23')
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
LIMIT 10
```

This next query explodes the `productListItems` array and returns each merchandising eVar and event per product. De `_id` wordt opgenomen om de relatie met de originele hit te tonen. De `_id` value is een unieke primaire sleutel voor de dataset.

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
  WHERE TIMESTAMP = to_timestamp('2019-07-23')
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
)
LIMIT 20
```

>[!NOTE]
>
> Als u probeert om een gebied terug te winnen dat niet in uw huidige dataset bestaat, zal de fout &quot;Geen dergelijk struct gebied&quot;voorkomen. Evalueer de reden die in het foutenbericht is teruggekeerd om een beschikbaar gebied te identificeren, dan uw vraag bij te werken en opnieuw uit te voeren.
>
>
```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### Conversiesyntaxis

Another type of merchandising variable found in Adobe Analytics is conversion syntax. With product syntax, the value is collected at the same time as the product, but this requires the data to be present on the same page. There are scenarios where the data occurs on a page prior to the conversion or event of interest related to the product. Neem bijvoorbeeld het gebruiksgeval voor de productzoekmethode.

1. Een gebruiker voert en intern onderzoek naar &quot;winterhoed&quot;uit die de Syntaxis van de Omzetting toelaat Merchandising eVar6 aan &quot;intern onderzoek:winterhoed&quot;
2. The user clicks on &quot;waffle beanie&quot; and lands on the product detail page.\
   a. Het landen hier vuurt een `Product View` gebeurtenis voor de &quot;waffle beanie&quot; voor $12,99.\
   b. Omdat `Product View` is geconfigureerd als een bindingsgebeurtenis. Het product &quot;waffle beanie&quot; is nu gebonden aan de eVar 6-waarde van &quot;internal search:winter hat&quot;. Telkens wanneer het product &quot;waffle beanie&quot; wordt verzameld, wordt het gekoppeld aan &quot;internal search:winter hat&quot; totdat (1) de instelling voor de vervaldatum is bereikt of (2) een nieuwe waarde voor eVar6 is ingesteld en de gebeurtenis binding met dat product opnieuw plaatsvindt.
3. De gebruiker voegt het product aan zijn winkelwagentje toe en ontslaat het `Cart Add` gebeurtenis.
4. De gebruiker voert een andere interne zoekopdracht uit naar &quot;zomershirt&quot; waarmee de omzettingssyntaxis Merchandising eVar6 instelt op &quot;intern zoeken:zomershirt&quot;
5. De gebruiker klikt op &quot;sporty t-shirt&quot; en landt op de pagina met productdetails.\
   a. Het landen hier vuurt een `Product View` evenement voor &quot;sporty t-shirt voor $19,99.\
   b. De `Product View` Het evenement is nog steeds ons bindende evenement, dus nu is het product &quot;sporty t-shirt&quot; nu gebonden aan de eVar6-waarde van &quot;internal search:zomer shirt&quot; en het eerdere product &quot;waffle beanie&quot; is nog steeds gebonden aan de eVar &quot;internal search:waffle beanie&quot;.
6. The user adds the product to their cart, firing the `Cart Add` event.
7. De gebruiker checkt beide producten uit.

Bij de rapportage worden de orders, opbrengsten, productweergaven en winkelwagentjes gerapporteerd tegen eVar6 en afgestemd op de activiteit van het gebonden product.

| eVar6 (productzoekmethode) | omzet | orders | productweergave | cartografische objecten |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| intern zoeken:zomershirt | 19,99 | 1 | 1 | 1 |
| interne zoekopdracht:winterhoed | 12,99 | 1 | 1 | 1 |

Meer informatie over het gebruik van de conversiesyntaxis vindt u in de Adobe Analytics-documentatie op [eVars implementeren met conversiesyntaxis](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-conversion-variable-syntax).

Hier zijn de XDM-velden die de conversiesyntaxis produceren in uw [!DNL Analytics] gegevensset:

#### eVars

```console
_experience.analytics.customDimensions.evars.evar#
```

- `evar#`: De specifieke variabele van de eVar die u toegang hebt.

#### Product

```console
productListItems[#].sku
```

- `#`: De index van de array die u opent.

#### Voorbeeldquery&#39;s

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
