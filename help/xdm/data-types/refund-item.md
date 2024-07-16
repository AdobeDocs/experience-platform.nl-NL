---
title: Gegevenstype item terugbetalen
description: Meer informatie over het gegevenstype Data Model (XDM) van het gegevensmodel Beleving van item herstellen.
exl-id: 9968d314-c6f3-49d9-b860-709d7478c43a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# [!UICONTROL Refund Item] gegevenstype

[!UICONTROL Refund Item] is een standaard XDM-gegevenstype (Experience Data Model) waarmee wordt beschreven welke gegevens betrekking hebben op een restitutie voor een bestelling.

![ een diagram van het gegevenstype van het Punt van de Terugbetaling.](../images/data-types/refund-item.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|--------------------|-----------------------|-----------|---------------------------------------------------------------------------------------------------|
| [!UICONTROL Transaction ID] | `transactionID` | string | De unieke transactie-id voor dit restitutieobject. |
| [!UICONTROL Refund Amount] | `refundAmount` | getal | De waarde van de restitutie. |
| [!UICONTROL Refund Reason] | `refundReason` | string | De reden waarom een restitutie is toegekend. |
| [!UICONTROL Refund Payment Type] | `refundPaymentType` | string | De betalingsmethode voor deze bestelling. Aangepaste waarden zijn toegestaan. |
| [!UICONTROL Currency Code] | `currencyCode` | string | De ISO 4217-valutacode die wordt gebruikt voor dit restitutieobject. Bijvoorbeeld: &quot;USD&quot;, &quot;EUR&quot;. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.schema.json)
