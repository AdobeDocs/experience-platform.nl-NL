---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;order;datatype;data-type;data-type;
solution: Experience Platform
title: Gegevenstype Volgorde
topic: overview
description: Dit document biedt een overzicht van het gegevenstype Order Experience Data Model (XDM).
translation-type: tm+mt
source-git-commit: 8bbb062df47b6e94630626d0a89a179d759d922d
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 2%

---


# [!UICONTROL Het ] gegevenstype Orderdata

[!UICONTROL Hiermee ] wordt een standaard XDM-gegevenstype (Experience Data Model) geordend waarmee de volgorde wordt beschreven die voor een productlijst is geplaatst.

<img src="../images/data-types/order.PNG" width="400" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `payments` | Array van [[!UICONTROL Betalingsitems]](./payment-item.md) | De lijst met betalingen voor deze bestelling. |
| `currencyCode` | Tekenreeks | De ISO 4217-valutacode die wordt gebruikt voor de totalen van de orders. Alle instanties moeten aan de regelmatige uitdrukking `^[A-Z]{3}$` voldoen. Voorbeelden zijn `USD` en `EUR`. |
| `priceTotal` | Dubbel | De totale prijs van deze bestelling nadat alle kortingen en belastingen zijn toegepast. |
| `purchaseID` | Tekenreeks | Een unieke id die door de verkoper is toegewezen voor deze aankoop of dit contract. Omdat deze is gedefinieerd door de verkoper, is er geen garantie dat de id uniek is. |
| `purchaseOrderNumber` | Tekenreeks | De unieke id die door de koper voor deze aankoop of dit contract is toegewezen. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)