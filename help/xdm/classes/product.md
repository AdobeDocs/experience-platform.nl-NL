---
title: Productklasse
description: Leer over de klasse van het Product in het Model van de Gegevens van de Ervaring (XDM).
exl-id: 911680ae-b761-4945-9ad3-0233eaea89b0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# [!UICONTROL Product] class

In Experience Data Model (XDM), [!UICONTROL Product] klasse legt de minimumreeks eigenschappen vast die een handelsproduct definiëren.

![](../images/classes/product.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `productListPrice` | [Valuta](../data-types/currency.md) | Beschrijft de standaardprijs van het product vóór verkoop en discontering. |
| `_id` | String | Een unieke, door het systeem gegenereerde tekenreeks-id voor de record. Dit veld wordt gebruikt om het unieke karakter van een individueel record te volgen, om te voorkomen dat gegevens dubbel worden opgeslagen en om dat record op te zoeken in downstreamdiensten.<br><br>Aangezien dit veld door het systeem wordt gegenereerd, wordt er geen expliciete waarde opgegeven tijdens het invoeren van gegevens. U kunt er echter desgewenst nog voor kiezen om uw eigen unieke id-waarden op te geven. |
| `productDescription` | String | Een beschrijving van het product. |
| `productID` | String | Een unieke id voor het product. |
| `productLastModifiedDate` | DateTime | An [RFC339](https://datatracker.ietf.org/doc/html/rfc3339) tijdstempel van wanneer dit product voor het laatst is gewijzigd voor updates. |
| `productManufacturedDate` | DateTime | An [RFC339](https://datatracker.ietf.org/doc/html/rfc3339) tijdstempel van wanneer dit product is gemaakt. |
| `productName` | String | De naam van het product. |
| `productRating` | String | De beoordeling van het product door de klant. |

{style="table-layout:auto"}

## Compatibele veldgroepen {#field-groups}

Adobe biedt verschillende standaardveldgroepen voor gebruik met de [!UICONTROL Product] klasse. Hieronder volgt een lijst met enkele veelgebruikte veldgroepen voor de klasse:

* [[!UICONTROL Product catalog]](../field-groups/product/product-catalog.md)
* [[!UICONTROL Product category]](../field-groups/product/product-category.md)
