---
title: Gegevenstype timing
description: Leer over het gegevenstype van het Model van de Gegevens van de Ervaring van de Timing (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 0640d0c2daab67ad7a77d3265ccae45851ba45b8
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# [!UICONTROL Timing] gegevenstype

[!UICONTROL Timing] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat een timingsprogramma beschrijft dat informatie over een gebeurtenis verstrekt die veelvoudige tijden kan voorkomen. Dit gegevenstype wordt gecreeerd volgens de specificaties van Versie 5 van HL7 FHIR.

![ het timing gegevenstype structuur ](../../images/data-types/healthcare/timing.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Event] | `event` | Array van DateTime | Wanneer de gebeurtenis plaatsvindt. |
| [!UICONTROL Repeat] | `repeat` | [[!UICONTROL Repeat]](../healthcare/repeat.md) | Informatie over wanneer de gebeurtenis plaatsvindt. |
| [!UICONTROL Code] | `code` | [[!UICONTROL Codeable Concept]](../healthcare/codeable-concept.md) | De code voor de gebeurtenis. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.schema.json)
