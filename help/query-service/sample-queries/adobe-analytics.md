---
keywords: Experience Platform;huis;populaire onderwerpen;de vraagdienst;de dienst van de Vraag;steekproefvragen;steekproefvraag;adobe analytics;
solution: Experience Platform
title: Voorbeeldquery's voor Adobe Analytics-gegevens
topic-legacy: queries
description: Gegevens uit geselecteerde Adobe Analytics-rapportsuites worden getransformeerd in XDM ExperienceEvents en als datasets opgenomen in Adobe Experience Platform. Dit document schetst een aantal gebruiksgevallen waarin de Dienst van de Vraag van deze gegevens gebruik maakt en steekproefvragen omvat die worden ontworpen om met uw datasets van Adobe Analytics te werken.
exl-id: 96da3713-c7ab-41b3-9a9d-397756d9dd07
source-git-commit: e0cdfc514a9e1277134d4c0d5396fc0bdf9d9958
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 1%

---

# Voorbeeldquery&#39;s voor Adobe Analytics-gegevens

Gegevens uit geselecteerde Adobe Analytics-rapportsuites worden omgezet in gegevens die overeenkomen met de [!DNL XDM ExperienceEvent] klasse en opgenomen in Adobe Experience Platform als datasets.

In dit document wordt een aantal gebruiksgevallen beschreven waarbij Adobe Experience Platform [!DNL Query Service] maakt gebruik van deze gegevens. Zie de documentatie op [Toewijzing van het veld Analytics](../../sources/connectors/adobe-applications/mapping/analytics.md) voor meer informatie over toewijzing aan [!DNL Experience Events].

Zie de [documentatie over het gebruik van analysemogelijkheden](../use-cases/analytics-insights.md) om te leren hoe te om de Dienst van de Vraag te gebruiken om actionable inzichten van ingebedde gegevens van Adobe Analytics tot stand te brengen.

## Deduplicatie

[!DNL Query Service] ondersteunt gegevensdeduplicatie. Zie de [Gegevensdeduplicatie in [!DNL Query Service] documentatie](../best-practices/deduplication.md) voor informatie over hoe u nieuwe waarden kunt genereren op het moment dat u een query uitvoert [!DNL Experience Event] datasets.

## Merchandising-variabelen (productsyntaxis)

De volgende secties verstrekken XDM gebieden en steekproefvragen die u kunt gebruiken om tot de handelsveranderende variabelen in uw [!DNL Analytics] dataset.

### Productsyntaxis

In Adobe Analytics kunnen aangepaste productgegevens worden verzameld via speciaal geconfigureerde variabelen, de zogenaamde &#39;merchandising&#39;-variabelen. Deze zijn gebaseerd op een eVar of aangepaste gebeurtenissen. Het verschil tussen deze variabelen en hun typische gebruik is dat zij een afzonderlijke waarde voor elk product vertegenwoordigen dat op de slag wordt gevonden eerder dan slechts ????n waarde voor de slag.

Deze variabelen worden ook wel handelsvariabelen in de productsyntaxis genoemd. Op deze manier kunt u informatie verzamelen, zoals een &quot;kortingsbedrag&quot; per product of informatie over de &quot;locatie op pagina&quot; van het product in de zoekresultaten van de klant.

Meer informatie over het gebruik van de productsyntaxis vindt u in de Adobe Analytics-documentatie op [eVars implementeren met productsyntaxis](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-product-syntax).

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

Hier volgt een voorbeeldquery die een eVar en gebeurtenis retourneert voor het eerste product dat in het dialoogvenster `productListItems`.

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

In deze volgende query wordt het dialoogvenster `productListItems` array en retourneert elke eVar en gebeurtenis die door de handel wordt verwerkt per product. De `_id` wordt opgenomen om de relatie met de originele hit te tonen. De `_id` value is een unieke primaire sleutel voor de dataset.

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

Een ander type handelsvariabele dat in Adobe Analytics wordt gevonden, is de conversiesyntaxis. Met productsyntaxis wordt de waarde verzameld op hetzelfde moment als het product, maar hiervoor moeten de gegevens op dezelfde pagina aanwezig zijn. Er zijn scenario&#39;s waarin de gegevens op een pagina v????r de conversie of het geval van belang met betrekking tot het product voorkomen. Neem bijvoorbeeld het gebruiksgeval voor de productzoekmethode.

1. Een gebruiker voert en intern onderzoek naar &quot;winterhoed&quot;uit die de Syntaxis van de Omzetting toelaat Merchandising eVar6 aan &quot;intern onderzoek:winterhoed&quot;
2. De gebruiker klikt op &quot;wafelbeanie&quot; en landt op de pagina met productdetails.\
   a. Het landen hier vuurt een `Product View` gebeurtenis voor de &quot;waffle beanie&quot; voor $12,99.\
   b. Sinds `Product View` is geconfigureerd als een bindende gebeurtenis, is het product &quot;waffle beanie&quot; nu gebonden aan de eVar6-waarde van &quot;internal search:winter hat&quot;. Telkens wanneer het product &quot;waffle beanie&quot; wordt verzameld, wordt het gekoppeld aan &quot;internal search:winter hat&quot; totdat (1) de instelling voor de vervaldatum is bereikt of (2) een nieuwe waarde voor eVar6 is ingesteld en de gebeurtenis binding met dat product opnieuw plaatsvindt.
3. De gebruiker voegt het product aan zijn winkelwagentje toe en ontslaat het `Cart Add` gebeurtenis.
4. De gebruiker voert een andere interne zoekopdracht uit naar &quot;zomershirt&quot; waarmee de omzettingssyntaxis Merchandising eVar6 instelt op &quot;intern zoeken:zomershirt&quot;
5. De gebruiker klikt op &quot;sporty t-shirt&quot; en landt op de pagina met productdetails.\
   a. Het landen hier vuurt een `Product View` evenement voor &quot;sporty t-shirt voor $19,99.\
   b. De `Product View` Het evenement is nog steeds ons bindende evenement, dus nu is het product &quot;sporty t-shirt&quot; nu gebonden aan de eVar6-waarde van &quot;internal search:zomer shirt&quot; en het eerdere product &quot;waffle beanie&quot; is nog steeds gebonden aan de eVar &quot;internal search:waffle beanie&quot;.
6. De gebruiker voegt het product aan zijn winkelwagentje toe en ontslaat het `Cart Add` gebeurtenis.
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
