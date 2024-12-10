---
title: Gegevenstype hoeveelheid
description: Meer informatie over het gegevenstype Quantity Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 881fe8a4-0253-4b75-9833-b97bb50cc87e
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# [!UICONTROL Quantity] gegevenstype

[!UICONTROL Quantity] is een standaard XDM-gegevenstype (Experience Data Model) dat een gemeten of meetbare hoeveelheid biedt. Dit gegevenstype wordt gecreeerd volgens de specificaties van Versie 5 van HL7 FHIR.

![ structuur van het gegevenstype van de Hoeveelheid ](../../../images/healthcare/data-types/quantity.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | String | De gecodeerde vorm van de eenheid. |
| [!UICONTROL Comparator] | `comparator` | String | De vergelijkingsoperator. De waarde van deze eigenschap moet gelijk zijn aan een van de volgende bekende opsommingswaarden. <li> `<` </li> <li> `<=` </li> <li> `>=` </li> <li> `>`</li> <li> `ad`</li> |
| [!UICONTROL System] | `system` | String | Het systeem dat de gecodeerde eenheidsvorm bepaalt, die als URI wordt vertegenwoordigd. |
| [!UICONTROL Unit] | `unit` | String | De eenheidrepresentatie. |
| [!UICONTROL Value] | `value` | Dubbel | De numerieke waarde. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/quantity.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/quantity.schema.json)
