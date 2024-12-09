---
title: Gegevenstype codering
description: Meer informatie over het gegevenstype XDM (Coding Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---

# [!UICONTROL Coding] gegevenstype

[!UICONTROL Coding] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat een verwijzing naar een code beschrijft die door een terminologiesysteem wordt bepaald. Dit gegevenstype wordt gecreeerd volgens de specificaties van Versie 5 van HL7 FHIR.

![ Coderende gegevenstypestructuur ](../../images/data-types/healthcare/coding.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | String | Het symbool in de syntaxis die door het systeem wordt bepaald. |
| [!UICONTROL Display] | `display` | String | De representatie die door het systeem is gedefinieerd. |
| [!UICONTROL System] | `system` | String | De naamruimte voor de id-waarde, uitgedrukt als een URI. |
| [!UICONTROL Is Selected By User] | `userSelected` | Boolean | Geeft aan of deze codering door de gebruiker is gekozen. De standaardwaarde is false. |
| [!UICONTROL Version] | `version` | String | De versie van het systeem. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/coding.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/coding.schema.json)
