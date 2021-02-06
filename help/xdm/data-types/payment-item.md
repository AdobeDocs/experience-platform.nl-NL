---
keywords: Experience Platform;huis;populaire onderwerpen;schema;Schema;XDM;gebieden;schema's;Schema's;betalings punt;datatype;gegeven-type;gegevenstype;
solution: Experience Platform
title: Gegevenstype betalingsobject
topic: overview
description: Dit document biedt een overzicht van het gegevenstype Data Model (XDM) van het betalingsitemervaringsgegevensmodel.
translation-type: tm+mt
source-git-commit: 8bbb062df47b6e94630626d0a89a179d759d922d
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 2%

---


# [!UICONTROL Gegevenstype ] betalingsitem

[!UICONTROL Betalingsitems ] zijn een standaard XDM-gegevenstype (Experience Data Model) waarmee een betaling wordt beschreven voor een bestelling die het type betaling, het bedrag en de bijbehorende valuta definieert.

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