---
title: Gegevenstype retourneren
description: Leer over het gegevenstype van de Gegevens van de Ervaring van de Terugkeer Model (XDM).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 1%

---

# [!UICONTROL Return] gegevenstype

[!UICONTROL Return] is een standaardgegevenstype van de Gegevens van de Ervaring Model (XDM) dat de essentiële informatie met betrekking tot een Vergunning van de Goederen van de Terugkeer (RMA) vangt.

![Een diagram van het gegevenstype Return.](../images/data-types/return.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|----------------------------------|----------------------|-----------|--------------------------------------------------|
| [!UICONTROL Return ID] | `returnID` | string | De unieke id voor deze RMA. |
| [!UICONTROL Return Status] | `returnStatus` | string | De huidige status van de RMA (bijvoorbeeld In behandeling of Gesloten). |
| [!UICONTROL Order Purchase ID] | `purchaseID` | string | De unieke id van de order/aankoop waarop de RMA betrekking heeft. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/return.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/return.schema.json)

