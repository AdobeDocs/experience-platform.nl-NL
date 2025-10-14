---
title: Gegevenstype winkelwagentje
description: Meer informatie over het gegevenstype XDM (Cart Experience Data Model).
exl-id: 24ae3882-60f3-4962-b0b5-7dba48170da8
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# [!UICONTROL Cart] gegevenstype

[!UICONTROL Cart] is een standaard XDM-gegevenstype (Experience Data Model) dat eigenschappen biedt die verwant zijn aan een winkelwagentje. Gebruik dit gegevenstype om de unieke id vast te leggen die door de verkoper (`Cart ID`) is toegewezen en de bron (`Cart Source`) waar een of meer producten aan het winkelwagentje zijn toegevoegd.

![&#x200B; een diagram van het [!UICONTROL Cart] gegevenstype.](../images/data-types/cart.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|----------------|-------------------|-----------|------------------------------------------------------------|
| [!UICONTROL Cart ID] | `cartID` | string | Unieke identificatiecode die door de verkoper voor het winkelwagentje is toegekend. |
| [!UICONTROL Cart Source] | `cartSource` | string | Wanneer een of meer producten aan het karretje zijn toegevoegd. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json)
