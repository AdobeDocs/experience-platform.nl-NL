---
title: Gegevenstype tijdsduur
description: Leer over het gegevenstype van de Gegevens van de Ervaring van de Duur Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 01aac0d0-0503-4f8b-a306-cf3c187a76e0
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---

# [!UICONTROL Duration] gegevenstype

[!UICONTROL Duration] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat een tijdsduur beschrijft. Dit gegevenstype wordt gecreeerd volgens de specificaties van Versie 5 van HL7 FHIR.

![&#x200B; het gegevenstype van de Duur structuur &#x200B;](../../../images/healthcare/data-types/duration.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | String | De gecodeerde vorm van de tijdseenheid. |
| [!UICONTROL System] | `system` | String | Het systeem dat de gecodeerde eenheid beschrijft, die als URI wordt vertegenwoordigd. |
| [!UICONTROL Unit] | `unit` | String | De eenheid van tijd die in milliseconden, seconden, notulen, uren, dagen, weken, maanden, of jaren wordt vertegenwoordigd. De waarden van deze eigenschap moeten gelijk zijn aan een of meer van de volgende bekende opsommingswaarden. <li> `ms` (milliseconden) </li> <li> `s` (seconden) </li> <li> `min` (minuten) </li> <li> `h` (uren) </li>  <li> `d` (dagen) </li> <li> `wk` (weken) </li> <li> `mo` (maanden) </li> <li> `a` (jaren) </li> |
| [!UICONTROL Value] | `value` | Dubbel | De numerieke waarde voor de tijdseenheid. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/duration.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/duration.schema.json)
