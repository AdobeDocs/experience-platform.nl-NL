---
title: Merchandising-variabelen uit analysegegevens retourneren en gebruiken
description: Leer hoe te om gebieden XDM en steekproefvragen te verstrekken om tot de het verhandelen variabelen in uw datasets van Analytics toegang te hebben.
exl-id: 1e2ae095-4152-446f-8b66-dae5512d690e
source-git-commit: 7cde32f841497edca7de0c995cc4c14501206b1a
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 0%

---

# Commerciële variabelen uit analysegegevens retourneren en gebruiken

De Dienst van de Vraag van het gebruik om de gegevens te beheren die van Adobe Analytics in Adobe Experience Platform als datasets worden opgenomen. De volgende secties verstrekken steekproefvragen die u kunt gebruiken om tot de het verhandelen variabelen in uw datasets van Analytics toegang te hebben. Zie de documentatie voor meer informatie over [ hoe te om de gegevens van Adobe Analytics in te voeren en in kaart te brengen ](../../sources/connectors/adobe-applications/mapping/analytics.md) door de bron van Analytics

## Merchandiings-variabelen {#merchandising-variables}

De variabelen van de koophandel kunnen één van twee syntaxis volgen:

* **Syntaxis van het Product**: Vendeert de waarde van eVar aan een product. 
* **Veranderlijke Syntaxis van de Omzetting**: Verleent de eVar met een product slechts als een bindende gebeurtenis voorkomt. U kunt de gebeurtenissen selecteren die als bindingsgebeurtenissen fungeren.

## Productsyntaxis {#product-syntax}

In Adobe Analytics kunnen aangepaste productgegevens worden verzameld via speciaal geconfigureerde variabelen, de zogenaamde &#39;merchandising&#39;-variabelen. Deze zijn gebaseerd op een eVar of aangepaste gebeurtenissen. Het verschil tussen deze variabelen en hun typische gebruik is dat zij een afzonderlijke waarde voor elk product vertegenwoordigen dat op de treffer wordt gevonden eerder dan slechts één waarde voor de treffer.

Deze variabelen worden ook wel handelsvariabelen in de productsyntaxis genoemd. Op deze manier kunt u informatie verzamelen, zoals een &quot;kortingsbedrag&quot; per product of informatie over de &quot;locatie op pagina&quot; van het product in de zoekresultaten van de klant.

Meer leren over het gebruiken van de productsyntaxis, te lezen gelieve de documentatie van Adobe Analytics op [ uitvoerend eVars gebruikend productsyntaxis ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=nl-NL#implement-using-product-syntax).

In de volgende secties worden de XDM-velden beschreven die nodig zijn voor toegang tot de variabelen voor handelsdoeleinden in uw gegevensset [!DNL Analytics] :

### eVars

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

* `#`: De index van de array die u opent.
* `evar#`: De specifieke variabele eVar die u opent.

### Aangepaste gebeurtenissen

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

* `#`: De index van de array die u opent.
* `event#`: De specifieke aangepaste gebeurtenisvariabele die u opent.

## Gebruiksscenario&#39;s voor productsyntaxis {#product-use-cases}

In de volgende gebruiksgevallen wordt de focus op het retourneren van een eVar van de array `productListItems` met SQL.

### Retourneer een eVar voor handelsdoeleinden en een gebeurtenis

De onderstaande query retourneert een eVar en gebeurtenis voor het eerste product dat in de array `productListItems` wordt gevonden.

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

Met deze volgende query wordt de array `productListItems` geëxplodeerd en wordt elke eVar en gebeurtenis per product geretourneerd. Het veld `_id` wordt opgenomen om de relatie met de oorspronkelijke hit weer te geven. De `_id` -waarde is een unieke primaire sleutel voor de gegevensset.

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
>```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### Syntaxis conversievariabele {#conversion-variable-syntax}

Een ander type handelsvariabele dat in Adobe Analytics wordt gevonden, is de syntaxis van de conversievariabele. De syntaxis van de conversievariabele wordt gebruikt wanneer de waarde van eVar niet beschikbaar is om in de productvariabele te worden geplaatst. Dit scenario betekent doorgaans dat de pagina geen context heeft van het kanaal voor handelsdoeleinden of de zoekmethode. In deze gevallen moet u de variabele voor het wijzigen van de handelswaarde instellen voordat de gebruiker bij de productpagina aankomt. De waarde blijft bestaan totdat de gebeurtenis binding plaatsvindt.

Het onderstaande productzoekingsscenario illustreert bijvoorbeeld hoe de vereiste gegevens op een pagina aanwezig kunnen zijn voordat de conversie of gebeurtenis met betrekking tot het product plaatsvindt.

1. Een gebruiker voert een intern onderzoek naar &quot;winterhoed&quot;uit die de omzettingssyntaxis toegelaten merchandising eVar6 aan &quot;intern onderzoek:winterhoed&quot;plaatst.
2. De gebruiker klikt op &quot;wafelbeanie&quot; en landt op de pagina met productdetails.\
   a. Met de landing hier wordt een `Product View` -gebeurtenis voor de &quot;waffle beanie&quot; voor $12,99 geactiveerd.\
   b. Aangezien `Product View` is geconfigureerd als een bindingsgebeurtenis, is het product &quot;waffle beanie&quot; nu gebonden aan de eVar6-waarde van &quot;internal search:winter hat&quot;. Telkens wanneer het &quot;wafelbeanie&quot;-product wordt verzameld, wordt het gekoppeld aan &quot;interne zoekactie:winterhoed&quot;. Dit gebeurt totdat de eVar-instelling voor verlopen is bereikt of er een nieuwe eVar6-waarde is ingesteld en de bindingsgebeurtenis opnieuw met dat product plaatsvindt.
3. De gebruiker voegt het product aan zijn winkelwagentje toe en activeert de gebeurtenis `Cart Add` .
4. De gebruiker voert een andere interne zoekopdracht naar &quot;zomershirt&quot; uit, die de omzettingssyntaxis voor merchandising eVar6 instelt op &quot;intern zoeken:zomershirt&quot;.
5. De gebruiker selecteert &quot;sporty t-shirt&quot; en landt op de pagina met productdetails.\
   a. Met de landing hier wordt een `Product View` -evenement voor &#39;sportt-shirt voor $19,99 gestart.\
   b. Aangezien het `Product View` -evenement het bindende evenement is, is het product &#39;sporty t-shirt&#39; nu gebonden aan de eVar6-waarde van &#39;internal search:zomer shirt&#39;. Het vorige product &quot;wafelbeanie&quot; is nog steeds gebonden aan een eVar6-waarde van &quot;internal search:waffle beanie&quot;.
6. De gebruiker voegt het product aan zijn winkelwagentje toe en activeert de gebeurtenis `Cart Add` .
7. De gebruiker checkt beide producten uit.

Bij het rapporteren zijn de bestellingen, opbrengsten, productweergaven en winkelwagentjes rapporteerbaar ten opzichte van eVar6 en zijn ze afgestemd op de activiteit van het gebonden product.

| eVar6 (productbepalingsmethode) | omzet | orders | productweergave | cartografische objecten |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| intern zoeken:zomershirt | 19,99 | 1 | 1 | 1 |
| interne zoekopdracht:winterhoed | 12,99 | 1 | 1 | 1 |

Om meer over het gebruiken van de syntaxis van de omzetvariabele te leren, te lezen gelieve de documentatie van Adobe Analytics op [ uitvoerend eVars gebruikend de syntaxis van de omzettingsvariabele ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=nl-NL#implement-using-conversion-variable-syntax).

Hieronder worden de XDM-velden weergegeven die de syntaxis van de conversievariabele in uw [!DNL Analytics] -dataset produceren:

#### eVars

```console
_experience.analytics.customDimensions.evars.evar#
```

* `evar#`: De specifieke variabele eVar die u opent.

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

Door dit document te lezen, zou u beter inzicht in moeten hebben hoe te om een koopvaardigende eVar terug te keren gebruikend productsyntaxis en een waarde aan een specifiek product met de syntaxis van de omzettingsvariabele te binden.

Als u dit nog niet hebt gedaan, zou u de [ inzichten van Analytics voor Web en mobiele interactieverklaring ](./analytics-insights.md) daarna moeten lezen. Het verstrekt gemeenschappelijke gebruiksgevallen en toont hoe te om de Dienst van de Vraag te gebruiken om actionable inzichten van Web en mobiele gegevens van Adobe Analytics tot stand te brengen.
