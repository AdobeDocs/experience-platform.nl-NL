---
title: Codeerbaar referentietype
description: Leer over het Codeable Gegevenstype van de Ervaring van de Referentie van het Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 5ac4bc82-3c8e-4622-8a4e-c954bd6e6411
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 1%

---

# [!UICONTROL Codeable Reference] gegevenstype

[!UICONTROL Codeable Reference] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat een verwijzing naar een middel of een concept beschrijft. Dit gegevenstype wordt gecreeerd volgens de specificaties van Versie 5 van HL7 FHIR.

![ Codeable het gegevenstype van de Verwijzing structuur ](../../../images/healthcare/data-types/codeable-reference.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Concept] | `concept` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Een verwijzing naar een concept (per klasse). |
| [!UICONTROL Reference] | `reference` | [[!UICONTROL Reference]](../data-types/reference.md) | Een verwijzing naar een bron. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.schema.json)
