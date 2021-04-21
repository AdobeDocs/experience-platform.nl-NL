---
keywords: Experience Platform;huis;populaire onderwerpen;schema;Schema;XDM;gebieden;schema's;Schema's;betalings punt;datatype;gegeven-type;gegevenstype;
solution: Experience Platform
title: Gegevenstype betalingsobject
topic-legacy: overview
description: Dit document biedt een overzicht van het gegevenstype Data Model (XDM) van het betalingsitemervaringsgegevensmodel.
exl-id: d25a358b-73c1-468b-a9c5-808385689932
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 2%

---

# [!UICONTROL Payment Item] gegevenstype

[!UICONTROL Payment Item] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat een betaling verbonden aan een orde beschrijft die het type van betaling, het bedrag, en de bijbehorende munt bepaalt.

<img src="../images/data-types/payment-item.PNG" width="400" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `currencyCode` | Tekenreeks | De ISO 4217-valutacode die wordt gebruikt voor de totalen van de orders. Alle instanties moeten aan de regelmatige uitdrukking `^[A-Z]{3}$` voldoen. Voorbeelden zijn `USD` en `EUR`. |
| `paymentAmount` | Dubbel | De waarde van de betaling. |
| `paymentType` | Tekenreeks | De betalingsmethode voor deze bestelling. Tot de geaccepteerde opsommingswaarden behoren: <li> `cash` </li> <li> `credit_card` </li> <li> `debit_card` </li> <li> `gift_card` </li> <li> `check` </li> <li> `paypal` </li> <li> `wire_transfer` </li> <li> `credit_card_reference` </li> <li> `other` </li> |
| `transactionID` | Tekenreeks | De unieke transactie-id voor dit betalingsobject. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.schema.json)
