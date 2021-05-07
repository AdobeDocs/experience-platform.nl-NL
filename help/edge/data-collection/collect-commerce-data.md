---
title: Handel en productinformatie verzamelen met de SDK van Adobe Experience Platform Web
description: Leer hoe u gegevens met betrekking tot producten of een winkelwagentje toevoegt met de Adobe Experience Platform Web SDK.
keywords: producten;handel;maatregelen;maatregel;order;cartAbandons;checkouts;productListAdds;productListOpens;productListRemovals;productListViews;productListViews;productViews;aankopen;saveForLaters;currencyCode;payments;paymentAmount;paymentType;transactionID;priceTotal;purchaseID;purchaseNumber;
exl-id: 3c79e776-89ef-494b-a2ea-3c23efce09ae
translation-type: tm+mt
source-git-commit: 7d7502b238f96eda1a15b622ba10bbccc289b725
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 1%

---

# Verzamelen van handel en productinformatie

Als u producten op uw site hebt, is dit een standaardset van dingen die u wilt verzenden om de meeste mogelijkheden van Adobe in te schakelen. Hoewel dit een suggestie is, biedt het vanaf het begin een zeer sterke set gegevens.

In dit document wordt de schemaveldgroep [ExperienceEvent Commerce Details](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) gebruikt. De `commerce`-veldgroep bestaat uit twee delen: het `commerce`-object en de `productListItems`-array. Met het object `commerce` kunt u aangeven welke handelingen met de array `productListItems` worden uitgevoerd.

>[!TIP]
>
>Als u bekend bent met Adobe Analytics, is `commerce` het nauwst verwant aan `events` variabele. De `productListItems` is nauwer verwant met de `products` variabele.

## Acties in verband met producten

Hieronder ziet u een lijst met `measures` beschikbaar in het object `commerce`.

>[!TIP]
>
>Een maatregel heeft twee velden: `id` en `value`. Meestal zult u alleen het veld `value` gebruiken (bijvoorbeeld `'value':1`). In het veld `id` kunt u een unieke id instellen die u kunt gebruiken om bij te houden wanneer de maatregel is verzonden. Zie de XDM documentatie voor [Maatregel](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/measure.schema.md).

| **Meetlat** | **Aanbeveling** | **Beschrijving** |
|---|---|---|
| [karAbandons](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcartabandons) | Optioneel | Een winkelwagentje is niet meer toegankelijk of kan niet meer door de gebruiker worden gekocht. |
| [kassa](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcheckouts) | Zeer aanbevolen | Een gebruiker zoekt niet meer naar producten, maar koopt een product. |
| [productListAdds](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistadds) | Zeer aanbevolen | Er wordt een product aan een lijst toegevoegd. Zorg ervoor dat u het product tegelijkertijd instelt in `productListItems`. |
| [productListOpens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistopens) | Optioneel | Er wordt een nieuwe productlijst gemaakt. (Er wordt bijvoorbeeld een nieuw winkelwagentje gemaakt.) |
| [productListRemovals](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistremovals) | Zeer aanbevolen | Een product wordt uit een productlijst verwijderd. |
| [productListReopen](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistreopens) | Optioneel | Een productlijst wordt opnieuw geactiveerd door de gebruiker. Dit gebeurt vaak bij hermarketingcampagnes. |
| [productListViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistviews) | Zeer aanbevolen | Er wordt een lijst met producten weergegeven. |
| [productViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductviews) | Zeer aanbevolen | Een weergave van een product is opgetreden. Zorg ervoor dat u het product instelt dat wordt weergegeven in `productListItems`. |
| [aankopen](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmpurchases) | Zeer aanbevolen | Een bestelling wordt geaccepteerd. Moet een productlijst hebben. |
| [saveForLaters](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmsaveforlaters) | Optioneel | Een product wordt opgeslagen voor toekomstig gebruik. |

Hier is een voorbeeld van hoe u deze `Measures` in SDK zou plaatsen.

```javascript
alloy("sendEvent", {
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    }
  }
});
```

Het handelsobject heeft ook een speciaal veld voor het verzamelen van ordergegevens met de naam `order`.

| **Volgorde** | **Optie** | **Aanbeveling** | **Beschrijving** |
|---|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) |  |  | De [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) valuta voor het totaal van de order. |
| [betalingen[betalingspunten]](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpayments) |  |  | De lijst met betalingen op een bestelling. Een [paymentItem](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#payment-item-schema) omvat het volgende. |
|  | [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) | Optioneel | De [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) valuta voor deze betalingsmethode. |
|  | [paymentAmount](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymentamount) | Zeer aanbevolen | De waarde van de betaling in de opgegeven valutacode. |
|  | [paymentType](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype) | Zeer aanbevolen | Het type betaling (bijvoorbeeld `credit_card`, `gift_card`, `paypal`). Zie de lijst met [bekende waarden](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype-known-values) voor meer informatie. |
|  | [transactionID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmtransactionid) | Optioneel | Een unieke id voor deze betalingstransactie. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpricetotal) |  | Zeer aanbevolen | Het totaal voor deze bestelling nadat alle kortingen en belastingen zijn toegepast. |
| [purchaseID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseid) |  | Zeer aanbevolen | De unieke id die door de verkoper is toegewezen voor deze aankoop. |
| [purchaseOrderNumber](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseordernumber) |  | Optioneel | Een unieke id die door de koper voor deze aankoop is toegewezen. |

Hier is een voorbeeld van een typische aankoop in SDK.

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "order":{
        "purchaseID":"123456789",
        "currencyCode":"USD",
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
        "quantity":1
      }
    ]
  }
});
```

## Lijst van producten

De productlijst geeft aan welke producten gerelateerd zijn aan de corresponderende actie. Het is een lijst van [productListItems](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md). Elk product heeft een aantal facultatieve gebieden.

| **Veld** | **Aanbeveling** | **Beschrijving** |
|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmcurrencycode) | Optioneel | De [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)-valuta voor het product. Dit is alleen handig wanneer u producten met verschillende valutacodes kunt gebruiken en wanneer deze van toepassing zijn. Bijvoorbeeld wanneer er een aankoop is of een winkelwagentje wordt toegevoegd. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmpricetotal) | Zeer aanbevolen | Moet alleen worden vastgesteld wanneer dit van toepassing is. Het is bijvoorbeeld mogelijk dat niet kan worden ingesteld op `productView` omdat verschillende variaties van het product verschillende prijzen kunnen hebben, maar op een `productListAdds`. |
| [product](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproduct) | Zeer aanbevolen | De XDM-id voor het product. |
| [productAddMethod](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproductaddmethod) | Zeer aanbevolen | De methode die door de bezoeker is gebruikt om een product-item aan de lijst toe te voegen. Stel dit in met `productListAdds` maateenheden en moet alleen worden gebruikt wanneer een product aan de lijst wordt toegevoegd. Voorbeelden zijn `add to cart button`, `quick add` en `upsell`. |
| [productName](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmname) | Zeer aanbevolen | Deze wordt ingesteld op de weergavenaam of leesbare naam van het product. |
| [hoeveelheid](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmquantity) | Zeer aanbevolen | Het aantal eenheden dat de klant heeft aangegeven van het product te verlangen. Moet worden ingesteld op `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters` enzovoort. |
| [SKU](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md) | Zeer aanbevolen | Bewaar bewaareenheid. Het is de unieke id voor het product. |

## Voorbeelden

`productView` event

```javascript
alloy("sendEvent",{
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
alloy("sendEvent",{
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
alloy("sendEvent",{
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
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "order":{
        "purchaseID":"123456789",
        "currencyCode":"USD",
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
        "quantity":1
      }
    ]
  }
});
```
