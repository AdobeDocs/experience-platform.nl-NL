---
title: Verzamel handel, product, en ordeinformatie gebruikend het Web SDK van Adobe Experience Platform
description: Leer hoe u gegevens met betrekking tot producten of een winkelwagentje toevoegt met de Adobe Experience Platform Web SDK.
exl-id: 3c79e776-89ef-494b-a2ea-3c23efce09ae
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 0%

---

# Verzamel handel, product, en ordeinformatie

Als uw organisatie producten of diensten verkoopt, kunt u deze pagina als gids voor gebruiken hoe te om die producten en de diensten te volgen.

Deze pagina gebruikt de XDM [ gebiedsgroep van het Schema van Commerce 0&rbrace; &lbrace;.](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md)

Deze veldgroep bestaat uit twee hoofddelen:

* Het `commerce` -object. Met dit object kunt u aangeven welke handelingen met de array `productListItems` worden uitgevoerd.
* De array `productListItems` .

>[!TIP]
>
>Als u bekend bent met Adobe Analytics, bevat het `commerce` -object gegevens die lijken op commercegebeurtenissen in de `events` -variabele. De objectarray `productListItems` bevat gegevens die vergelijkbaar zijn met de variabele `products` .

## Het object `commerce` {#commerce-object}

In deze sectie worden de velden beschreven die beschikbaar zijn in het `commerce` -object.

>[!TIP]
>
>Een maat heeft twee velden: `id` en `value` . Meestal gebruikt u alleen het veld `value` (bijvoorbeeld `'value':1` ). In het veld `id` kunt u een unieke id voor bijhouden instellen wanneer de maatregel is verzonden. Zie de documentatie XDM voor [ Maatregel ](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/measure.schema.md) voor meer informatie.

| Meetlat | Aanbeveling | Beschrijving |
|---|---|---|
| [`cartAbandons`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcartabandons) | Optioneel | Een winkelwagentje is niet meer toegankelijk of kan niet meer door de gebruiker worden aangeschaft. |
| [`checkouts`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcheckouts) | Zeer aanbevolen | Een gebruiker zoekt niet meer naar producten, maar is bezig een product te kopen. |
| [`productListAdds`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistadds) | Zeer aanbevolen | Er wordt een product aan een lijst toegevoegd. Zorg ervoor dat u het product tegelijkertijd instelt in de `productListItems` . |
| [`productListOpens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistopens) | Optioneel | Er wordt een nieuwe productlijst gemaakt. Er wordt bijvoorbeeld een nieuw winkelwagentje gemaakt. |
| [`productListRemovals`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistremovals) | Zeer aanbevolen | Een product wordt uit een productlijst verwijderd. |
| [`productListReopens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistreopens) | Optioneel | Een productlijst wordt opnieuw geactiveerd door de gebruiker. Dit gebeurt vaak bij hermarketingcampagnes. |
| [`productListViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistviews) | Zeer aanbevolen | Er wordt een lijst met producten weergegeven. |
| [`productViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductviews) | Zeer aanbevolen | Een beeld van een product gebeurde. Zorg ervoor dat u het product instelt dat wordt weergegeven in de `productListItems` . |
| [`purchases`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmpurchases) | Zeer aanbevolen | Een bestelling wordt geaccepteerd. Moet een productlijst hebben. |
| [`saveForLaters`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmsaveforlaters) | Optioneel | Een product wordt opgeslagen voor toekomstig gebruik. |

{style="table-layout:auto"}

### `Commerce` objectvoorbeelden

Vouw de onderstaande sectie uit om een voorbeeld van een Web SDK-opdracht te zien met behulp van een veld uit het `commerce` -object.

+++`productViews`

Een standaard SDK-aanroep voor het web `sendEvent` die het `productViews` veld instelt op `1` :

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

+++

## Het object `order` {#order-object}

Het `commerce` -object bevat een speciaal object voor het verzamelen van ordergegevens. Dit wordt het `order` -object genoemd.

In deze sectie worden alle velden beschreven die door het object `order` worden ondersteund.

| Veld | Optie | Aanbeveling | Beschrijving |
|---|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmcurrencycode) |  |  | De [ ISO 4217 ](https://en.wikipedia.org/wiki/ISO_4217) munt voor het ordertotaal. |
| [`payments[]`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpayments) |  |  | De lijst met betalingen op een bestelling. A [ paymentItem ](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md) omvat het volgende. |
|  | [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmcurrencycode) | Optioneel | De [ ISO 4217 ](https://en.wikipedia.org/wiki/ISO_4217) munt voor deze betalingsmethode. |
|  | [`paymentAmount`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymentamount) | Zeer aanbevolen | De waarde van de betaling in de opgegeven valutacode. |
|  | [`paymentType`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype) | Zeer aanbevolen | Het type betaling (bijvoorbeeld `credit_card` , `gift_card` , `paypal` ). Zie de lijst van [ gekende waarden ](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype-known-values) voor details. |
|  | [`transactionID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmtransactionid) | Optioneel | Een unieke id voor deze betalingstransactie. |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpricetotal) |  | Zeer aanbevolen | Het totaal voor deze bestelling nadat alle kortingen en belastingen zijn toegepast. |
| [`purchaseID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseid) |  | Zeer aanbevolen | De unieke id die door de verkoper is toegewezen voor deze aankoop. |
| [`purchaseOrderNumber`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseordernumber) |  | Optioneel | Een unieke id die door de koper voor deze aankoop is toegewezen. |

### Voorbeelden van Order-objecten

Vouw de onderstaande sectie uit om een voorbeeld van een Web SDK-opdracht weer te geven met behulp van het `commerce` -object.

+++`Order` objectvoorbeeld

Een Web SDK `sendEvent` -aanroep die het `order` -object instelt dat van toepassing is op meerdere producten in de `productListItems` -array:

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

+++

## Het object productlijst {#product-list-object}

De productlijst geeft aan welke producten gerelateerd zijn aan de corresponderende actie. Het is een lijst van [ productListItems ](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md). Elk product heeft verschillende optionele velden.

| Veld | Aanbeveling | Beschrijving |
|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmcurrencycode) | Optioneel | De [ ISO 4217 ](https://en.wikipedia.org/wiki/ISO_4217) munt voor het product. Dit veld is doorgaans alleen van toepassing wanneer de productlijst meerdere producten bevat met verschillende valutacodes. |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmpricetotal) | Zeer aanbevolen | Stel dit veld alleen in, indien van toepassing. Het is bijvoorbeeld mogelijk niet in te stellen op de gebeurtenis `productView` omdat verschillende variaties van het product verschillende prijzen kunnen hebben, maar op een gebeurtenis `productListAdds` . |
| [`product`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproduct) | Zeer aanbevolen | De XDM-id voor het product. |
| [`productAddMethod`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproductaddmethod) | Zeer aanbevolen | De methode die door de bezoeker is gebruikt om een product-item aan de lijst toe te voegen. Stel dit in met `productListAdds` maten en gebruik het alleen wanneer een product aan de lijst wordt toegevoegd. Voorbeelden zijn `add to cart button` , `quick add` en `upsell` . |
| [`productName`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmname) | Zeer aanbevolen | De weergavenaam of de leesbare naam van het product. |
| [`quantity`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmquantity) | Zeer aanbevolen | Het aantal eenheden dat de klant heeft aangegeven van het product te verlangen. Moet worden ingesteld op `productListAdds` , `productListRemoves` , `purchases` , `saveForLaters` , enzovoort. |
| [`SKU`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmsku) | Zeer aanbevolen | Bewaar de bewaareenheid. Het is de unieke id voor het product. |

### Voorbeelden van productlijsten

Vouw de onderstaande secties uit om voorbeelden van Web SDK-opdrachten weer te geven met behulp van het `productListItems` -object.

+++`productListItems` voorbeeld

Een Web SDK `sendEvent` -aanroep die de `productViews` voor meerdere producten in de `productListItems` -array instelt:

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

+++

+++`productListAdds` voorbeeld

Een Web SDK `sendEvent` -aanroep die de `productListAdds` -gebeurtenis instelt voor meerdere producten in de `productListItems` -array:

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

+++

+++`checkouts` voorbeeld

Een Web SDK `sendEvent` -aanroep die de `checkouts` -gebeurtenis instelt voor meerdere producten in de `productListItems` -array:

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

+++
