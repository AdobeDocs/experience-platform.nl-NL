---
title: Gegevenstype Codeable Concept
description: Leer over het Codeable Concept Gegevenstype van de Ervaring van het Concept (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: c172a7cd-24c6-484b-8552-8745dfd3a8e9
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 1%

---

# [!UICONTROL Codeable Concept] gegevenstype

[!UICONTROL Codeable Concept] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat een verwijzing van één middel aan een andere beschrijft. Dit gegevenstype wordt gecreeerd volgens de specificaties van Versie 5 van HL7 FHIR.

![&#x200B; Codeable Concept gegevenstype structuur &#x200B;](../../../images/healthcare/data-types/codeable-concept.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Coding] | `coding` | Array van [[!UICONTROL Coding]](../data-types/coding.md) | Code gedefinieerd door een terminologiesysteem. |
| [!UICONTROL Text] | `text` | String | De representatie van het concept in normale tekst. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeableconcept.schema.json)
