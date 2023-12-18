---
title: Gegevenstype winkelwagentje
description: Meer informatie over het gegevenstype XDM (Cart Experience Data Model).
source-git-commit: c3590dc2cfe47eb634136eeb88578f965598760d
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# [!UICONTROL Cart] gegevenstype

[!UICONTROL Cart] is een standaard gegevenstype van het Gegevensmodel van de Ervaring (XDM) dat eigenschappen met betrekking tot een het winkelwagentje verstrekt. Gebruik dit gegevenstype om de unieke id vast te leggen die door de verkoper is toegewezen (`Cart ID`) en de bron (`Cart Source`) wanneer een of meer producten aan de kar zijn toegevoegd.

![Een schema van de [!UICONTROL Cart] gegevenstype.](../images/data-types/cart.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|----------------|-------------------|-----------|------------------------------------------------------------|
| [!UICONTROL Cart ID] | `cartID` | string | Unieke identificatiecode die door de verkoper voor het winkelwagentje is toegekend. |
| [!UICONTROL Cart Source] | `cartSource` | string | Wanneer een of meer producten aan het karretje zijn toegevoegd. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json)
