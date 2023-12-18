---
title: Gegevenstype verzending
description: Meer informatie over het gegevenstype XDM (Shipping Experience Data Model).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# [!UICONTROL Shipping] gegevenstype

[!UICONTROL Shipping] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat details met betrekking tot de verzending van één of meerdere producten verstrekt. Het bevat details over de logistiek en bijzonderheden met betrekking tot de levering van bestelde voorwerpen.


![Een schema van de [!UICONTROL Shipping] gegevenstype.](../images/data-types/shipping.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|----------------------|-----------------------|-----------|------------------------------------------------------|
| [!UICONTROL Shipping Method] | `shippingMethod` | string | De door de klant gekozen verzendmethode. |
| [!UICONTROL Shipping Amount] | `shippingAmount` | getal | Het bedrag dat de klant voor de verzending moest betalen. |
| [!UICONTROL Currency code] | `currencyCode` | string | De alfabetische ISO 4217-valutacode die wordt gebruikt voor de prijsstelling van het product. |
| [!UICONTROL Shipping Destination] | `shippingDestination` | string | Het schip-aan bestemming die door de gebruiker wordt gespecificeerd (bijvoorbeeld, huis, opslag, etc.). |
| [!UICONTROL Ship Date] | `shipDate` | string | De datum waarop een of meer items van een bestelling worden verzonden. |
| [!UICONTROL Shipping Address] | `address` | [[!UICONTROL address]](./address.md) | Het verzendadres. |
| [!UICONTROL Tracking Number] | `trackingNumber` | getal | Het trackingnummer dat door de verzendende maatschappij is verstrekt. |
| [!UICONTROL Tracking URL] | `trackingURL` | string | De URL waarmee de verzendstatus van een orderitem wordt gevolgd. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json)
