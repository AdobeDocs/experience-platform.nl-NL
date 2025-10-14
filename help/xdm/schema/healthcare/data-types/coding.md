---
title: Gegevenstype codering
description: Meer informatie over het gegevenstype XDM (Coding Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 23b789da-1feb-4001-8268-f0d7e2e8563b
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---

# [!UICONTROL Coding] gegevenstype

[!UICONTROL Coding] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat een verwijzing naar een code beschrijft die door een terminologiesysteem wordt bepaald. Dit gegevenstype wordt gecreeerd volgens de specificaties van Versie 5 van HL7 FHIR.

![&#x200B; Coderende gegevenstypestructuur &#x200B;](../../../images/healthcare/data-types/coding.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | String | Het symbool in de syntaxis die door het systeem wordt bepaald. |
| [!UICONTROL Display] | `display` | String | De representatie die door het systeem is gedefinieerd. |
| [!UICONTROL System] | `system` | String | De naamruimte voor de id-waarde, uitgedrukt als een URI. |
| [!UICONTROL Is Selected By User] | `userSelected` | Boolean | Geeft aan of deze codering door de gebruiker is gekozen. De standaardwaarde is false. |
| [!UICONTROL Version] | `version` | String | De versie van het systeem. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/coding.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/coding.schema.json)
