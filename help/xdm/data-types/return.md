---
title: Gegevenstype retourneren
description: Leer over het gegevenstype van de Gegevens van de Ervaring van de Terugkeer Model (XDM).
exl-id: 1fd99a25-547f-49e7-8980-dda7db2ebb8a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 1%

---

# [!UICONTROL Return] gegevenstype

[!UICONTROL Return] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat de essentiële informatie met betrekking tot een Vergunning van de Handel van de Terugkeer (RMA) vangt.

![ A diagram van het gegevenstype van de Terugkeer.](../images/data-types/return.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|----------------------------------|----------------------|-----------|--------------------------------------------------|
| [!UICONTROL Return ID] | `returnID` | string | De unieke id voor deze RMA. |
| [!UICONTROL Return Status] | `returnStatus` | string | De huidige status van de RMA (bijvoorbeeld In behandeling of Gesloten). |
| [!UICONTROL Order Purchase ID] | `purchaseID` | string | De unieke id van de order/aankoop waarop de RMA betrekking heeft. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/components/datatypes/return.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/components/datatypes/return.schema.json)
