---
title: Gegevenstype retouritem
description: Leer over het gegevenstype van de Gegevens van de Ervaring van het Punt van de Terugkeer Model (XDM).
exl-id: e703d65b-a133-484e-96d6-6b1f50fc1e48
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# [!UICONTROL Return Item] gegevenstype

[!UICONTROL Return Item] is een standaard XDM-gegevenstype (Experience Data Model) waarmee essentiële details worden vastgelegd met betrekking tot het retourproces voor een aangeschaft item.

![&#x200B; A diagram van het gegevenstype van het Punt van de Terugkeer.](../images/data-types/return-item.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|-----------------------------|------------------------------|-----------|--------------------------------------------------------|
| [!UICONTROL Return Status] | `returnStatus` | string | De status van het geretourneerde item (bijvoorbeeld In behandeling of goedgekeurd). |
| [!UICONTROL Return Reason] | `returnReason` | string | De reden waarom de return is aangevraagd voor het object. |
| [!UICONTROL Return Item Condition] | `returnItemCondition` | string | De voorwaarde van het item waarvoor de return wordt aangevraagd. |
| [!UICONTROL Return Resolution] | `returnResolution` | string | De gewenste resolutie of het gewenste resultaat dat van het rendement wordt verwacht (bijvoorbeeld Terugbetaling of Uitwisseling). |
| [!UICONTROL Return Quantity Requested] | `returnQuantityRequested` | integer | De hoeveelheid van het object die de verkoper heeft aangevraagd om terug te sturen. |
| [!UICONTROL Return Quantity Authorized] | `returnQuantityAuthorized` | integer | De hoeveelheid van het object die mag worden geretourneerd. |
| [!UICONTROL Return Quantity Received] | `returnQuantityReceived` | integer | Het aantal geretourneerde objecten dat is ontvangen. |
| [!UICONTROL Return Quantity Approved] | `returnQuantityApproved` | integer | De hoeveelheid van het artikel met een volledig ingevulde en goedgekeurde terugzending. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.schema.json)
