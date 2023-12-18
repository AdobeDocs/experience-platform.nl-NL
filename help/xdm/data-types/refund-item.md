---
title: Gegevenstype item terugbetalen
description: Meer informatie over het gegevenstype Data Model (XDM) van het gegevensmodel Beleving van item herstellen.
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# [!UICONTROL Refund Item] gegevenstype

[!UICONTROL Refund Item] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat informatie met betrekking tot een restitutie verbonden aan een orde beschrijft.

![Een diagram van het gegevenstype Item terugbetalen.](../images/data-types/refund-item.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|--------------------|-----------------------|-----------|---------------------------------------------------------------------------------------------------|
| [!UICONTROL Transaction ID] | `transactionID` | string | De unieke transactie-id voor dit restitutieobject. |
| [!UICONTROL Refund Amount] | `refundAmount` | getal | De waarde van de restitutie. |
| [!UICONTROL Refund Reason] | `refundReason` | string | De reden waarom een restitutie is toegekend. |
| [!UICONTROL Refund Payment Type] | `refundPaymentType` | string | De betalingsmethode voor deze bestelling. Aangepaste waarden zijn toegestaan. |
| [!UICONTROL Currency Code] | `currencyCode` | string | De ISO 4217-valutacode die wordt gebruikt voor dit restitutieobject. Bijvoorbeeld: &quot;USD&quot;, &quot;EUR&quot;. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.schema.json)
