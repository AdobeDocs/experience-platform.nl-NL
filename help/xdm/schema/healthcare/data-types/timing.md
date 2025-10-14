---
title: Gegevenstype timing
description: Leer over het gegevenstype van het Model van de Gegevens van de Ervaring van de Timing (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: e1bc16ed-4dd8-4316-b3c8-88d49d393859
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# [!UICONTROL Timing] gegevenstype

[!UICONTROL Timing] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat een timingsprogramma beschrijft dat informatie over een gebeurtenis verstrekt die veelvoudige tijden kan voorkomen. Dit gegevenstype wordt gecreeerd volgens de specificaties van Versie 5 van HL7 FHIR.

![&#x200B; het timing gegevenstype structuur &#x200B;](../../../images/healthcare/data-types/timing.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Event] | `event` | Array van DateTime | Wanneer de gebeurtenis plaatsvindt. |
| [!UICONTROL Repeat] | `repeat` | [[!UICONTROL Repeat]](../data-types/repeat.md) | Informatie over wanneer de gebeurtenis plaatsvindt. |
| [!UICONTROL Code] | `code` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | De code voor de gebeurtenis. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.schema.json)
