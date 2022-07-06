---
title: Productklasse
description: Dit document biedt een overzicht van de productklasse in het XDM (Experience Data Model).
exl-id: 911680ae-b761-4945-9ad3-0233eaea89b0
source-git-commit: fdd68e5a94d841992a6f8abe10f3cffe0ebb6794
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 2%

---

# [!UICONTROL Product] class

In het Model van de Gegevens van de Ervaring (XDM), [!UICONTROL Product] klasse legt de minimumreeks eigenschappen vast die een handelsproduct definiëren.

![](../images/classes/product.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `productListPrice` | [Valuta](../data-types/currency.md) | Beschrijft de standaardprijs van het product vóór verkoop en discontering. |
| `_id` | Tekenreeks | Een unieke, door het systeem gegenereerde tekenreeks-id voor de record. Dit veld wordt gebruikt om het unieke karakter van een individueel record te volgen, om te voorkomen dat gegevens dubbel worden opgeslagen en om dat record op te zoeken in downstreamdiensten.<br><br>Aangezien dit veld door het systeem wordt gegenereerd, wordt er geen expliciete waarde opgegeven tijdens het invoeren van gegevens. U kunt er echter desgewenst nog voor kiezen om uw eigen unieke id-waarden op te geven. |
| `productDescription` | Tekenreeks | Een beschrijving van het product. |
| `productID` | Tekenreeks | Een unieke id voor het product. |
| `productLastModifiedDate` | DateTime | An [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) tijdstempel van wanneer dit product voor het laatst is gewijzigd voor updates. |
| `productManufacturedDate` | DateTime | An [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) tijdstempel van wanneer dit product is gemaakt. |
| `productName` | Tekenreeks | De naam van het product. |
| `productRating` | Tekenreeks | De beoordeling van het product door de klant. |

{style=&quot;table-layout:auto&quot;}

## Compatibele veldgroepen {#field-groups}

Adobe biedt verschillende standaardveldgroepen voor gebruik met de [!UICONTROL Product] klasse. Hieronder volgt een lijst met enkele veelgebruikte veldgroepen voor de klasse:

* [[!UICONTROL Product catalog]](../field-groups/product/product-catalog.md)
* [[!UICONTROL Product category]](../field-groups/product/product-category.md)
