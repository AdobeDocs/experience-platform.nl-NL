---
title: Gegevenstype herhalen
description: Meer informatie over het gegevenstype XDM (Repeat Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# [!UICONTROL Repeat] gegevenstype

[!UICONTROL Repeat] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat een reeks regels verstrekt die beschrijven wanneer een gebeurtenis gepland is. Dit gegevenstype wordt gecreeerd volgens de specificaties van Versie 5 van HL7 FHIR.

![ herhalen gegevenstypestructuur ](../../images/data-types/healthcare/reference.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Bound Period] | `boundsPeriod` | [[!UICONTROL Period]](../healthcare/period.md) | De begin- en eindtijd. |
| [!UICONTROL Bound Range] | `boundsRange` | [[!UICONTROL Range]](../healthcare/range.md) | De bereiklimiet. |
| [!UICONTROL Bound Duration] | `boundsDuration` | [[!UICONTROL Duration]](../healthcare/duration.md) | De tijdsbeperking. |
| [!UICONTROL Count] | `count` | Geheel | Het aantal keren dat moet worden herhaald, met een minimumwaarde van `0`. |
| [!UICONTROL Maximum Count] | `countMax` | Geheel | Het maximale aantal keren dat moet worden herhaald, met een minimumwaarde van `0`. |
| [!UICONTROL Day Of Week] | `dayOfWeek` | Array van tekenreeksen | Een array met tekenreeksen waarin wordt aangegeven welke dagen beschikbaar zijn. De waarden van deze eigenschap moeten gelijk zijn aan een of meer van de volgende bekende opsommingswaarden. <li> `mon` </li> <li> `tues` </li> <li> `wed` </li> <li> `thurs`</li>  <li> `fri` </li> <li> `sat`</li> <li> `sun`</li> |
| [!UICONTROL Duration] | `duration` | Dubbel | De tijdsduur. |
| [!UICONTROL Maximum Duration] | `durationMax` | Dubbel | De maximale tijdsduur. |
| [!UICONTROL Duration Unit] | `durationUnit` | String | De eenheid van duur. De waarden van deze eigenschap moeten gelijk zijn aan een of meer van de volgende bekende opsommingswaarden. <li> `s` (seconden) </li> <li> `min` (minuten) </li> <li> `h` (uur) </li> <li> `d` (dagelijks) </li>  <li> `wk` (wekelijks) </li> <li> `mo` (maandelijks) </li> <li> `a` (jaarlijks)</li> |
| [!UICONTROL Frequency] | `frequency` | Dubbel | Het aantal herhalingen dat binnen een periode moet plaatsvinden, met een minimumwaarde van `0`. |
| [!UICONTROL Maximum Frequency] | `frequencyMax` | Dubbel | Het maximumaantal herhalingen dat met een punt, met een minimumwaarde van `0` zou moeten voorkomen. |
| [!UICONTROL Offset] | `offset` | Geheel | De minuten tot de gebeurtenis (voor of na). |
| [!UICONTROL Period] | `period` | Dubbel | De duur van de frequentie. |
| [!UICONTROL Maximum Period] | `periodMax` | Dubbel | De bovengrens van de periode. |
| [!UICONTROL Period Unit] | `periodUnit` | String | De tijdseenheid. De waarden van deze eigenschap moeten gelijk zijn aan een of meer van de volgende bekende opsommingswaarden. <li> `s` (seconden) </li> <li> `min` (minuten) </li> <li> `h` (uur) </li> <li> `d` (dagelijks) </li>  <li> `wk` (wekelijks) </li> <li> `mo` (maandelijks) </li> <li> `a` (jaarlijks)</li> |
| [!UICONTROL Time Of Day] | `timeOfDay` | Array van tekenreeksen | Het tijdstip van de dag waarop de actie wordt uitgevoerd. |
| [!UICONTROL When] | `when` | Array van tekenreeksen | De code voor de tijdsperiode van de actie. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/repeat.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/repeat.schema.json)
