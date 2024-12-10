---
title: Gegevenstype verhouding
description: Leer over het gegevenstype van het Gegevensmodel van de Ervaring van de Verhouding (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 8b530af6-0e64-4c30-a7d7-eb221b0b6181
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# [!UICONTROL Ratio] gegevenstype

[!UICONTROL Ratio] is een standaard XDM-gegevenstype (Experience Data Model) dat een verhouding van twee [[!UICONTROL Quantity]](../data-types/quantity.md) -waarden biedt via een teller en een noemer. Dit gegevenstype wordt gecreeerd volgens de specificaties van Versie 5 van HL7 FHIR.

![ structuur van het gegevenstype van de Verhouding ](../../../images/healthcare/data-types/ratio.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Denominator] | `denominator` | [[!UICONTROL Simple Quantity]](../data-types/simple-quantity.md) | De waarde van de noemer. |
| [!UICONTROL Numerator] | `numerator` | [[!UICONTROL Quantity]](../data-types/quantity.md) | De waarde van de teller. |

>[!NOTE]
>
> De `denominator` en `numerator` hebben verschillende gegevenstypen vanwege de specificatie die is gemaakt in overeenstemming met HL7 FHIR Release 5.

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.schema.json)
