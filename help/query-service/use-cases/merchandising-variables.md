---
title: Merchandising-variabelen uit analysegegevens retourneren en gebruiken
description: Leer hoe te om gebieden XDM en steekproefvragen te verstrekken om tot de het verhandelen variabelen in uw datasets van Analytics toegang te hebben.
exl-id: 1e2ae095-4152-446f-8b66-dae5512d690e
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 1%

---

# Commerciële variabelen uit analysegegevens retourneren en gebruiken

De Dienst van de Vraag van het gebruik om de gegevens te beheren die van Adobe Analytics in Adobe Experience Platform als datasets worden opgenomen. De volgende secties verstrekken steekproefvragen die u kunt gebruiken om tot de het verhandelen variabelen in uw datasets van Analytics toegang te hebben. Zie de documentatie voor meer informatie over [Adobe Analytics-gegevens opnemen en toewijzen](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/mapping/analytics.html) via de bron Analytics

## Merchandisingvariabelen {#merchandising-variables}

De variabelen van de koophandel kunnen één van twee syntaxis volgen:

* **Productsyntaxis**: Koppelt de waarde van de eVar aan een product. 
* **Conversievariabele syntaxis**: Koppelt de eVar alleen aan een product als zich een bindingsgebeurtenis voordoet. U kunt de gebeurtenissen selecteren die als bindingsgebeurtenissen fungeren.

## Productsyntaxis {#product-syntax}

In Adobe Analytics kunnen aangepaste productgegevens worden verzameld via speciaal geconfigureerde variabelen, de zogenaamde &#39;merchandising&#39;-variabelen. Deze zijn gebaseerd op een eVar of aangepaste gebeurtenissen. Het verschil tussen deze variabelen en hun typische gebruik is dat zij een afzonderlijke waarde voor elk product vertegenwoordigen dat op de slag wordt gevonden eerder dan slechts één waarde voor de slag.

Deze variabelen worden ook wel handelsvariabelen in de productsyntaxis genoemd. Op deze manier kunt u informatie verzamelen, zoals een &quot;kortingsbedrag&quot; per product of informatie over de &quot;locatie op pagina&quot; van het product in de zoekresultaten van de klant.

Meer informatie over het gebruik van de productsyntaxis vindt u in de Adobe Analytics-documentatie op [eVars implementeren met productsyntaxis](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-product-syntax).

In de onderstaande secties worden de XDM-velden beschreven die nodig zijn voor toegang tot de handelsvariabelen in uw [!DNL Analytics] gegevensset:

### eVars

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

* `#`: De index van de array die u opent.
* `evar#`: De specifieke variabele van de eVar die u toegang hebt.

### Aangepaste gebeurtenissen

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

* `#`: De index van de array die u opent.
* `event#`: De specifieke variabele van de douanegebeurtenis die u toegang hebt.

## Gebruiksscenario&#39;s voor productsyntaxis {#product-use-cases}

De volgende gebruiksgevallen zijn gericht op het retourneren van een eVar voor handelsdoeleinden vanuit de `productListItems` array met SQL.

### Een merchandising-eVar en -gebeurtenis retourneren

Met de onderstaande query worden een eVar en een gebeurtenis geretourneerd voor het eerste product dat in het dialoogvenster `productListItems` array.

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

### Explodeer de array productListItems en retourneer de eVar en gebeurtenis voor elk product.

In deze volgende query wordt het dialoogvenster `productListItems` array en retourneert elke eVar en gebeurtenis die door de handel wordt verwerkt per product. De `_id` wordt opgenomen om de relatie met de originele hit te tonen. De `_id` value is een unieke primaire sleutel voor de dataset.

>[!NOTE]
>
>De exploderfunctie scheidt de elementen van een array in meerdere rijen. Null-waarden worden uitgesloten.

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
> Als u probeert om een gebied terug te winnen dat niet in uw huidige dataset bestaat, komt de &quot;Geen zulk struct gebied&quot;fout voor. Evalueer de reden die in het foutenbericht is teruggekeerd om een beschikbaar gebied te identificeren, dan uw vraag bij te werken en het opnieuw uit te voeren.
>
>
```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### Syntaxis conversievariabele {#conversion-variable-syntax}

Een ander type handelsvariabele dat in Adobe Analytics wordt gevonden, is de syntaxis van de conversievariabele. De syntaxis van de conversievariabele wordt gebruikt wanneer de waarde van de eVar niet beschikbaar is om in de productvariabele te worden geplaatst. Dit scenario betekent doorgaans dat de pagina geen context heeft van het kanaal voor handelsdoeleinden of de zoekmethode. In deze gevallen moet u de variabele voor het wijzigen van de handelswaarde instellen voordat de gebruiker bij de productpagina aankomt. De waarde blijft bestaan totdat de gebeurtenis binding plaatsvindt.

Het onderstaande productzoekingsscenario illustreert bijvoorbeeld hoe de vereiste gegevens op een pagina aanwezig kunnen zijn voordat de conversie of gebeurtenis met betrekking tot het product plaatsvindt.

1. Een gebruiker voert een intern onderzoek naar &quot;winterhoed&quot;uit die de omzettingssyntaxis toegelaten merchandising eVar6 aan &quot;intern onderzoek:winterhoed&quot;plaatst.
2. De gebruiker klikt op &quot;wafelbeanie&quot; en landt op de pagina met productdetails.\
   a. Het landen hier vuurt een `Product View` gebeurtenis voor de &quot;waffle beanie&quot; voor $12,99.\
   b. Sinds `Product View` is geconfigureerd als een bindende gebeurtenis, is het product &quot;waffle beanie&quot; nu gebonden aan de eVar6-waarde van &quot;internal search:winter hat&quot;. Telkens wanneer het &quot;wafelbeanie&quot;-product wordt verzameld, wordt het gekoppeld aan &quot;interne zoekactie:winterhoed&quot;. Dit gebeurt totdat de instelling voor het verlopen van de eVar is bereikt of er een nieuwe eVar6-waarde is ingesteld en de gebeurtenis binding opnieuw met dat product plaatsvindt.
3. De gebruiker voegt het product aan zijn winkelwagentje toe en ontslaat het `Cart Add` gebeurtenis.
4. De gebruiker voert een andere interne zoekopdracht naar &quot;zomershirt&quot; uit, die de omzettingssyntaxis voor merchandising eVar6 instelt op &quot;intern zoeken:zomershirt&quot;.
5. De gebruiker selecteert &quot;sporty t-shirt&quot; en landt op de pagina met productdetails.\
   a. Het landen hier vuurt een `Product View` evenement voor &quot;sporty t-shirt voor $19,99.\
   b. Als de `Product View` het evenement is bindend en het product &quot;sporty t-shirt&quot; is nu gebonden aan de eVar 6 van &quot;internal search:zomer shirt&quot;. Het vorige product &quot;wafelbeanie&quot; is nog steeds gebonden aan een eVar6-waarde van &quot;internal search:waffle beanie&quot;.
6. De gebruiker voegt het product aan zijn winkelwagentje toe en ontslaat het `Cart Add` gebeurtenis.
7. De gebruiker checkt beide producten uit.

Bij het rapporteren zijn de bestellingen, opbrengsten, productweergaven en winkelwagentjes rapporteerbaar ten opzichte van eVar6 en afgestemd op de activiteit van het gebonden product.

| eVar6 (productzoekmethode) | omzet | orders | productweergave | cartografische objecten |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| intern zoeken:zomershirt | 19.99 | 1 | 1 | 1 |
| interne zoekopdracht:winterhoed | 12.99 | 1 | 1 | 1 |

Meer informatie over het gebruik van de syntaxis van de conversievariabele vindt u in de Adobe Analytics-documentatie op [implementeren van eVars met syntaxis van conversievariabelen](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-conversion-variable-syntax).

Hieronder worden de XDM-velden weergegeven die de syntaxis van de conversievariabele in uw [!DNL Analytics] gegevensset:

#### eVars

```console
_experience.analytics.customDimensions.evars.evar#
```

* `evar#`: De specifieke variabele van de eVar die u toegang hebt.

#### Product

```console
productListItems[#].sku
```

* `#`: De index van de array die u opent.

## Gebruiksgevallen van conversievariabele {#conversion-variable-use-cases}

In de onderstaande gebruiksgevallen worden scenario&#39;s beschreven waarvoor de syntaxis van conversievariabelen vereist is.

### De waarde binden aan het specifieke product en de gebeurteniscombinatie

De query hieronder bindt de waarde aan het specifieke product en gebeurtenispaar. In dit voorbeeld is de waarde gebonden aan de gebeurtenis van de productweergave.

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

### De gebonden waarde tot volgende exemplaren van het desbetreffende product behouden

De voorbeeldvraag hieronder handhaaft de gebonden waarde aan verdere voorkomen van het respectieve product. De laagste subquery vestigt de relatie van de waarde met het product op de gedeclareerde bindingsgebeurtenis. De volgende subquery voert de toewijzing van die gebonden waarde uit voor volgende interacties met het desbetreffende product. De SELECT op hoofdniveau aggregeert de resultaten om de rapportage te produceren.

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

## Volgende stappen

Door dit document te lezen, zou u beter inzicht in moeten hebben hoe te om een koopwaar terug te keren gebruikend productsyntaxis en een waarde aan een specifiek product met de syntaxis van de omzettingsvariabele te binden.

Als u dit nog niet hebt gedaan, moet u de [Analyseinzichten voor documentatie over webinteracties en mobiele interacties](./analytics-insights.md) volgende. Het verstrekt gemeenschappelijke gebruiksgevallen en toont hoe te om de Dienst van de Vraag te gebruiken om actionable inzichten van Web en mobiele gegevens van Adobe Analytics tot stand te brengen.
