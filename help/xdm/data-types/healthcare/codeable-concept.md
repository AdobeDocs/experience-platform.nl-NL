---
title: Gegevenstype Codeable Concept
description: Leer over het Codeable Concept Gegevenstype van de Ervaring van het Concept (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 1%

---

# [!UICONTROL Codeable Concept] gegevenstype

[!UICONTROL Codeable Concept] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat een verwijzing van één middel aan een andere beschrijft. Dit gegevenstype wordt gecreeerd volgens de specificaties van Versie 5 van HL7 FHIR.

![ Codeable Concept gegevenstype structuur ](../../images/data-types/healthcare/codeable-concept.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Coding] | `coding` | Array van [[!UICONTROL Coding]](../healthcare/coding.md) | Code gedefinieerd door een terminologiesysteem. |
| [!UICONTROL Text] | `text` | String | De representatie van het concept in normale tekst. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeableconcept.schema.json)
