---
title: Gegevenstype Commerce-bereik
description: Meer informatie over het gegevenstype Commerce Scope Experience Data Model (XDM).
exl-id: c2888c3a-a49c-43c4-8d36-0a485cb76a58
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---

# [!UICONTROL Commerce Scope] gegevenstype

[!UICONTROL Commerce Scope] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat herkenningstekens bepaalt voor waar een gebeurtenis binnen een handels ecosysteem voorkwam. Het onderscheidt omgevingen, websites, winkels en winkelweergaven.

![ een diagram van het gegevenstype van het Bereik van Commerce.](../images/data-types/commerce-scope.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|---------------------------------|-------------------|-----------|-------------------------------------------------------|
| [!UICONTROL Environment ID] | `environmentID` | string | De milieu-id. Een alfanumerieke id van 32 cijfers. |
| [!UICONTROL Website Code] | `websiteCode` | string | De unieke websitecode in een omgeving. |
| [!UICONTROL Store Code] | `storeCode` | string | De unieke opslagcode in een website. |
| [!UICONTROL Store View Code] | `storeViewCode` | string | De unieke code van de opslagmening binnen een opslag. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.schema.json)
