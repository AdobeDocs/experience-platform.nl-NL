---
title: Producten
seo-title: Producten ondersteunen met Adobe Experience Platform Web SDK
description: Leer hoe te om gegevens toe te voegen als u producten of een het winkelwagentje met het Web SDK van het Platform van de Ervaring hebt
seo-description: Leer hoe te om gegevens toe te voegen als u producten of een het winkelwagentje met het Web SDK van het Platform van de Ervaring hebt
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 1%

---


# Producten

Als u producten op uw site hebt, is dit een standaardset van dingen die u wilt verzenden om de meeste mogelijkheden van Adobe in te schakelen. Hoewel dit een suggestie is, biedt het vanaf het begin een zeer sterke set gegevens.

Dit document gebruikt de [mix ExperienceEvent Commerce Details](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) . Het `commerce` mengsel wordt in twee delen verdeeld: het `commerce` object en de `productListItems` array. Met het `commerce` object kunt u aangeven welke handelingen met de `productListItems` array worden uitgevoerd.

>[!Tip]
>Als u bekend bent met Adobe Analytics, `commerce` is The het meest verwant aan de `events` variabele. Het `productListItems` hangt meer samen met de `products` variabele.

## Acties in verband met producten

Hieronder ziet u een lijst met `measures` beschikbare gegevens in het `commerce` object.

>[!Tip]
>Een maatregel heeft twee velden: `id` en `value`. Meestal zult u alleen het `value` veld gebruiken (bijvoorbeeld `'value':1`). In het `id` veld kunt u een unieke id instellen waarmee u kunt bijhouden wanneer de maatregel is verzonden. Zie de documentatie XDM voor [Maatregel](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/measure.schema.md).

| **Meetlat** | **Aanbeveling** | **Beschrijving** |
|---|---|---|
| [karAbandons](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcartabandons) | Optioneel | Een winkelwagentje is niet meer toegankelijk of kan niet meer door de gebruiker worden gekocht. |
| [kassa](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcheckouts) | Zeer aanbevolen | Een gebruiker zoekt niet meer naar producten, maar koopt een product. |
| [productListAdds](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistadds) | Zeer aanbevolen | Er wordt een product aan een lijst toegevoegd. Zorg ervoor dat u het product `productListItems` tegelijkertijd instelt. |
| [productListOpens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistopens) | Optioneel | Er wordt een nieuwe productlijst gemaakt. (Er wordt bijvoorbeeld een nieuw winkelwagentje gemaakt.) |
| [productListRemovals](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistremovals) | Zeer aanbevolen | Een product wordt uit een productlijst verwijderd. |
| [productListReopen](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistreopens) | Optioneel | Een productlijst wordt opnieuw geactiveerd door de gebruiker. Dit gebeurt vaak bij hermarketingcampagnes. |
| [productListViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistviews) | Zeer aanbevolen | Er wordt een lijst met producten weergegeven. |
| [productViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductviews) | Zeer aanbevolen | Een weergave van een product is opgetreden. Zorg ervoor dat u het product instelt dat in de `productListItems`app wordt weergegeven. |
| [aankopen](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmpurchases) | Zeer aanbevolen | Een bestelling wordt geaccepteerd. Moet een productlijst hebben. |
| [saveForLaters](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmsaveforlaters) | Optioneel | Een product wordt opgeslagen voor toekomstig gebruik. |

Hier is een voorbeeld van hoe u deze zou plaatsen `Measures` in SDK.

```javascript
alloy("event", {
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    }
  }
});
```

Het handelsobject heeft ook een speciaal veld voor het verzamelen van opdrachtdetails `order`.

| **Volgorde** | **Optie** | **Aanbeveling** | **Beschrijving** |
|---|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) |  |  | De [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) -valuta voor het totaal van de orders. |
| [betalingen[betalingspunten]](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpayments) |  |  | De lijst met betalingen op een bestelling. Een [betalingsobject](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#payment-item-schema) bevat het volgende. |
|  | [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) | Optioneel | De [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) -valuta voor deze betalingsmethode. |
|  | [paymentAmount](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymentamount) | Zeer aanbevolen | De waarde van de betaling in de opgegeven valutacode. |
|  | [paymentType](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype) | Zeer aanbevolen | Het type betaling (bijvoorbeeld, `credit_card`, `gift_card`, `paypal`). Zie de lijst met [bekende waarden](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype-known-values) voor meer informatie. |
|  | [transactionID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmtransactionid) | Optioneel | Een unieke id voor deze betalingstransactie. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpricetotal) |  | Zeer aanbevolen | Het totaal voor deze bestelling nadat alle kortingen en belastingen zijn toegepast. |
| [purchaseID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseid) |  | Zeer aanbevolen | De unieke id die door de verkoper is toegewezen voor deze aankoop. |
| [purchaseOrderNumber](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseordernumber) |  | Optioneel | Een unieke id die door de koper voor deze aankoop is toegewezen. |

Hier is een voorbeeld van een typische aankoop in SDK.

```javascript
alloy("event",{
  "xdm":{
    "commerce":{
      "order":{
        "purchaseID":"123456789",
        "currenceCode":"USD",
        "priceTotal":39.98,
        "payments":[
          {
            "transactionID":"amx12345",
            "paymentAmount":39.98,
            "paymentType":"credit_card",
            "currencyCode":"USD"
          }
        ]
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "priceTotal":29.99,
        "quantity":1
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "priceTotal":9.99,
        "qauntity":1
      }
    ]
  }
});
```

## Lijst van producten

De productlijst geeft aan welke producten gerelateerd zijn aan de corresponderende actie. Het is een lijst met [productListItems](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md). Elk product heeft een aantal facultatieve gebieden.

| **Veld** | **Aanbeveling** | **Beschrijving** |
|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmcurrencycode) | Optioneel | De [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) -valuta voor het product. Dit is alleen handig wanneer u producten met verschillende valutacodes kunt gebruiken en wanneer deze van toepassing zijn. Bijvoorbeeld wanneer er een aankoop is of een winkelwagentje wordt toegevoegd. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmpricetotal) | Zeer aanbevolen | Moet alleen worden vastgesteld wanneer dit van toepassing is. Het is bijvoorbeeld mogelijk dat niet kan worden ingesteld `productView` omdat verschillende variaties van het product verschillende prijzen kunnen hebben, maar op een `productListAdds`. |
| [product](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproduct) | Zeer aanbevolen | De XDM-id voor het product. |
| [productAddMethod](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproductaddmethod) | Zeer aanbevolen | De methode die door de bezoeker is gebruikt om een product-item aan de lijst toe te voegen. Stel dit in met `productListAdds` maateenheden en mag alleen worden gebruikt wanneer een product aan de lijst wordt toegevoegd. Voorbeelden zijn `add to cart button`, `quick add`en `upsell`. |
| [productName](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmname) | Zeer aanbevolen | Deze wordt ingesteld op de weergavenaam of leesbare naam van het product. |
| [hoeveelheid](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmquantity) | Zeer aanbevolen | Het aantal eenheden dat de klant heeft aangegeven te vragen voor het product. Moet worden ingesteld op `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters`enzovoort. |
| [SKU](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md) | Zeer aanbevolen | Bewaar bewaareenheid. Het is de unieke id voor het product. |

## Voorbeelden

`productView` event

```javascript
alloy("event",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
      }
    ]
  }
});
```

`productView` event

```javascript
alloy("event",{
  "xdm":{
    "commerce":{
      "productListAdds":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "quantity":1,
        "priceTotal":29.99,
        "productAddMethod":"Add to Cart Button"
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "quantity":1,
        "priceTotal":9.99,
        "productAddMethod":"Add-on"
      }
    ]
  }
});
```

`checkout` event

```javascript
alloy("event",{
  "xdm":{
    "commerce":{
      "checkouts":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "quantity":1,
        "priceTotal":29.99
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "quantity":1,
        "priceTotal":9.99
      }
    ]
  }
});
```

`purchase` event

```javascript
alloy("event",{
  "xdm":{
    "commerce":{
      "order":{
        "purchaseID":"123456789",
        "currenceCode":"USD",
        "priceTotal":39.98,
        "payments":[
          {
            "transactionID":"amx12345",
            "paymentAmount":39.98,
            "paymentType":"credit_card",
            "currencyCode":"USD"
          }
        ]
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "priceTotal":29.99,
        "quantity":1
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "priceTotal":9.99,
        "qauntity":1
      }
    ]
  }
});
```
