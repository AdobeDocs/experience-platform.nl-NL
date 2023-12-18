---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schemas;adres;xdm:adres;datatype;data-type;gegevenstype;
solution: Experience Platform
title: Gegevenstype van productlijst
description: Meer informatie over het XDM-gegevenstype van het item in de productlijst.
exl-id: 056fdb5b-6782-4e29-9d62-90b270c05795
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# [!UICONTROL Product list item] gegevenstype

[!UICONTROL Product list item] is een standaard XDM gegevenstype dat een product beschrijft dat door een klant met specifieke opties, tarifering, en gebruikscontext voor een specifiek tijdspunt wordt geselecteerd.

De waarden die in dit gegevenstype worden vastgelegd, kunnen afwijken van de productrecord. Het productdossier bevat bijvoorbeeld gegevens uit het productinformatiesysteem die consistent zijn voor alle klanten, waarbij het product in de productlijst de werkelijke prijs heeft die aan de klant wordt aangeboden op het moment van aankoop, die kan variëren als gevolg van verkoopcampagnes of seizoensgebonden prijzen.

![](../images/data-types/product-list-item.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `selectedOptions` | Array van objecten | Bevat aangepaste opties die zijn gekozen voor een configureerbaar product. Elk lijstitem is een object met de volgende eigenschappen:<ul><li>`attribute`: Een naam voor het configureerbare kenmerk.</li><li>`value`: De waarde van het kenmerk.</li></ul> |
| `SKU` | [!UICONTROL String] | Stock keeping unit (SKU), de unieke identificator voor een product dat door de verkoper wordt gedefinieerd. |
| `_id` | [!UICONTROL String] | The line item identifier for this product entry. Het product zelf wordt geïdentificeerd door `product`. |
| `currencyCode` | [!UICONTROL String] | De [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) alfabetische valutacode die wordt gebruikt voor de prijsstelling van het product. |
| `discountAmount` | [!UICONTROL Double] | Als het product wordt verdisconteerd, is dit het verschil tussen de normale prijs en de speciale prijs voor het product. |
| `name` | [!UICONTROL String] | De weergavenaam van het product zoals deze aan de gebruiker wordt getoond voor deze productweergave. |
| `priceTotal` | [!UICONTROL Double] | De totale prijs voor het item van de productlijn. |
| `product` | [!UICONTROL String] (URI) | De URI `$id` van het XDM-schema dat het product zelf vastlegt. |
| `productAddMethod` | [!UICONTROL String] | De methode die door de bezoeker is gebruikt om een product-item aan de lijst toe te voegen. |
| `productImageUrl` | [!UICONTROL String] | Een URL voor de hoofdafbeelding van het product. |
| `quantity` | [!UICONTROL Integer] | Het aantal eenheden dat de klant heeft aangegeven van het product te verlangen. |
| `unitOfMeasureCode` | [!UICONTROL String] | De norm [maateenheid](https://ucum.org/ucum) voor het product als gerelateerd aan de `quantity` eigenschap. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype van het postadres:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json)
