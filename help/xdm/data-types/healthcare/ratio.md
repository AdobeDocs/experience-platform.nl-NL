---
title: Gegevenstype verhouding
description: Leer over het gegevenstype van het Gegevensmodel van de Ervaring van de Verhouding (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7d33c5474629b2b02c19e752cdf2cb0a2ba19f19
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# [!UICONTROL Ratio] gegevenstype

[!UICONTROL Ratio] is een standaard XDM-gegevenstype (Experience Data Model) dat een verhouding van twee [[!UICONTROL Quantity]](../healthcare/quantity.md) -waarden biedt via een teller en een noemer. Dit gegevenstype wordt gecreeerd volgens de specificaties van Versie 5 van HL7 FHIR.

![ structuur van het gegevenstype van de Verhouding ](../../images/data-types/healthcare/ratio.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Denominator] | `denominator` | [[!UICONTROL Simple Quantity]](../healthcare/simple-quantity.md) | De waarde van de noemer. |
| [!UICONTROL Numerator] | `numerator` | [[!UICONTROL Quantity]](../healthcare/quantity.md) | De waarde van de teller. |

>[!NOTE]
>
> De `denominator` en `numerator` hebben verschillende gegevenstypen vanwege de specificatie die is gemaakt in overeenstemming met HL7 FHIR Release 5.

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.schema.json)
