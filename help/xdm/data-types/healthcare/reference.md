---
title: Gegevenstype Referentie
description: Leer over het gegevenstype van het Gegevensmodel van de Ervaring van de Referentie (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# [!UICONTROL Reference] gegevenstype

[!UICONTROL Reference] is een standaard XDM-gegevenstype (Experience Data Model) dat een verwijzing van de ene bron naar de andere biedt. Dit gegevenstype wordt gecreeerd volgens de specificaties van Versie 5 van HL7 FHIR.

![ het gegevenstype van de Verwijzing structuur ](../../images/data-types/healthcare/reference.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Identifier] | `identifier` | [[!UICONTROL Identifier]](../healthcare/identifier.md) | De logische verwijzing wanneer de letterlijke verwijzing onbekend is. |
| [!UICONTROL Display] | `display` | String | Het tekstalternatief voor de verwijzing. |
| [!UICONTROL Reference] | `reference` | String | De letterlijke verwijzing, relatieve, interne of absolute URL. |
| [!UICONTROL Type] | `type` | String | Het type waarnaar de verwijzing verwijst, aangeduid als een URI. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/reference.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/reference.schema.json)
