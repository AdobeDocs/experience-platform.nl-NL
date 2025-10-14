---
title: Gegevenstype Eenvoudige hoeveelheid
description: Leer meer over het gegevenstype Eenvoudig Quantity Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 92d3d6a8-1d0f-43a4-a93f-8df79605c4e6
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---

# [!UICONTROL Simple Quantity] gegevenstype

[!UICONTROL Simple Quantity] is een standaard XDM-gegevenstype (Experience Data Model) dat een gemeten of meetbare hoeveelheid biedt. Dit gegevenstype wordt gecreeerd volgens de specificaties van Versie 5 van HL7 FHIR.

![&#x200B; Eenvoudige structuur van het gegevenstype van de Hoeveelheid &#x200B;](../../../images/healthcare/data-types/simple-quantity.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | String | De gecodeerde vorm van de eenheid. |
| [!UICONTROL System] | `system` | String | Het systeem dat gecodeerde eenheidsvorm bepaalt, die als URI wordt vertegenwoordigd. |
| [!UICONTROL Unit] | `unit` | String | De representatie van de eenheid. |
| [!UICONTROL Value] | `value` | Dubbel | De numerieke waarde. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.schema.json)
