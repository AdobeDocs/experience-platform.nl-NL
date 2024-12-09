---
title: Gegevenstype
description: Leer over het gegevenstype van het Gegevensmodel van de Ervaring van het Geld (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 1%

---

# [!UICONTROL Money] gegevenstype

[!UICONTROL Money] is een standaard XDM-gegevenstype (Experience Data Model) dat een hoeveelheid economisch nut in een erkende valuta biedt. Dit gegevenstype wordt gecreeerd volgens de specificaties van Versie 5 van HL7 FHIR.

![ het gegevenstype van het Geld structuur ](../../images/data-types/healthcare/money.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Currency] | `currency` | String | De ISO 4217-valutacode. |
| [!UICONTROL Value] | `value` | Dubbel | De numerieke waarde. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/money.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/money.schema.json)
