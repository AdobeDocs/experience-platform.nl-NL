---
title: Gegevenstype verzending
description: Meer informatie over het gegevenstype XDM (Shipping Experience Data Model).
exl-id: c3a58e46-c80e-4896-b21c-47dc5a6c869b
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# [!UICONTROL Shipping] gegevenstype

[!UICONTROL Shipping] is een standaard XDM-gegevenstype (Experience Data Model) dat details biedt met betrekking tot de verzending van een of meer producten. Het bevat details over de logistiek en bijzonderheden met betrekking tot de levering van bestelde voorwerpen.


![ een diagram van het [!UICONTROL Shipping] gegevenstype.](../images/data-types/shipping.png)

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

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json)
