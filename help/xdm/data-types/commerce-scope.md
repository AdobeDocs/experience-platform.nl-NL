---
title: Gegevenstype handelsbereik
description: Leer over het gegevenstype van het Gegevensmodel van de Ervaring van het Bereik van de Handel (XDM).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---

# [!UICONTROL Commerce Scope] gegevenstype

[!UICONTROL Commerce Scope] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat herkenningstekens bepaalt voor waar een gebeurtenis binnen een handelsecosysteem voorkwam. Het onderscheidt omgevingen, websites, winkels en winkelweergaven.

![Een diagram van het gegevenstype Commerce Scope.](../images/data-types/commerce-scope.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|---------------------------------|-------------------|-----------|-------------------------------------------------------|
| [!UICONTROL Environment ID] | `environmentID` | string | De milieu-id. Een alfanumerieke id van 32 cijfers. |
| [!UICONTROL Website Code] | `websiteCode` | string | De unieke websitecode in een omgeving. |
| [!UICONTROL Store Code] | `storeCode` | string | De unieke opslagcode in een website. |
| [!UICONTROL Store View Code] | `storeViewCode` | string | De unieke code van de opslagmening binnen een opslag. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.schema.json)
