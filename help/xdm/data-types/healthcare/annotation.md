---
title: Gegevenstype aantekening
description: Leer over het gegevenstype van het gegevensmodel van de Ervaring van de Annotatie (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# [!UICONTROL Annotation] gegevenstype

[!UICONTROL Annotation] is een standaard XDM-gegevenstype (Experience Data Model) dat een tekstknooppunt bevat met kenmerk aan de auteur. Dit gegevenstype wordt gecreeerd volgens de specificaties van Versie 5 van HL7 FHIR.

![ structuur van het gegevenstype van de Annotatie ](../../images/data-types/healthcare/annotation.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Author Reference] | `authorReference` | [[!UICONTROL Reference]](../healthcare/reference.md) | Een verwijzing naar de auteur. |
| [!UICONTROL Author] | `authorString` | String | De persoon die verantwoordelijk is voor de aantekening. |
| [!UICONTROL Text] | `text` | String | De inhoud van de aantekening. |
| [!UICONTROL Time] | `time` | DateTime | Toen de annotatie werd gemaakt. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.schema.json)
