---
keywords: Experience Platform;huis;populaire onderwerpen;schema;Schema;XDM;gebieden;schema's;Schema's;betalings punt;datatype;gegeven-type;gegevenstype;
solution: Experience Platform
title: Gegevenstype betalingsobject
description: Meer informatie over het gegevenstype Data Model (XDM) van het betalingsitemervaringsgegevensmodel.
exl-id: d25a358b-73c1-468b-a9c5-808385689932
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# [!UICONTROL Payment Item] gegevenstype

[!UICONTROL Payment Item] is een standaard XDM-gegevenstype (Experience Data Model) waarmee een betaling wordt beschreven voor een bestelling die het type betaling, het bedrag en de bijbehorende valuta definieert.

{het beeld van het 0} betalingspunt ![&#128279;](../images/data-types/payment-item.PNG) {width= 400}

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `currencyCode` | String | De ISO 4217-valutacode die wordt gebruikt voor de totalen van de orders. Alle instanties moeten overeenkomen met de reguliere expressie `^[A-Z]{3}$` . Voorbeelden zijn `USD` en `EUR` . |
| `paymentAmount` | Dubbel | De waarde van de betaling. |
| `paymentType` | String | De betalingsmethode voor deze bestelling. Tot de geaccepteerde opsommingswaarden behoren: <li> `cash` </li> <li> `credit_card` </li> <li> `debit_card` </li> <li> `gift_card` </li> <li> `check` </li> <li> `paypal` </li> <li> `wire_transfer` </li> <li> `credit_card_reference` </li> <li> `other` </li> |
| `transactionID` | String | De unieke transactie-id voor dit betalingsobject. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.schema.json)
