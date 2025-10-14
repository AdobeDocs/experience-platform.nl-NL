---
title: Gegevenstype Referentie
description: Leer over het gegevenstype van het Gegevensmodel van de Ervaring van de Referentie (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: eb724dbb-2918-43b5-8e50-c8aabfe6e96c
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# [!UICONTROL Reference] gegevenstype

[!UICONTROL Reference] is een standaard XDM-gegevenstype (Experience Data Model) dat een verwijzing van de ene bron naar de andere biedt. Dit gegevenstype wordt gecreeerd volgens de specificaties van Versie 5 van HL7 FHIR.

![&#x200B; het gegevenstype van de Verwijzing structuur &#x200B;](../../../images/healthcare/data-types/reference.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Identifier] | `identifier` | [[!UICONTROL Identifier]](../data-types/identifier.md) | De logische verwijzing wanneer de letterlijke verwijzing onbekend is. |
| [!UICONTROL Display] | `display` | String | Het tekstalternatief voor de verwijzing. |
| [!UICONTROL Reference] | `reference` | String | De letterlijke verwijzing, relatieve, interne of absolute URL. |
| [!UICONTROL Type] | `type` | String | Het type waarnaar de verwijzing verwijst, aangeduid als een URI. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/reference.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/reference.schema.json)
