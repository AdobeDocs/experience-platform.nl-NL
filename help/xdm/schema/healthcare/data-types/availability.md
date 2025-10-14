---
title: Gegevenstype beschikbaarheid
description: Leer over het gegevenstype van het Gegevensmodel van de Ervaring van de Beschikbaarheid (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 18c0b767-adf0-480e-9cf2-63e21d05b362
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 1%

---

# [!UICONTROL Availability] gegevenstype

[!UICONTROL Availability] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat beschikbaarheidsgegevens voor een punt beschrijft. Dit gegevenstype wordt gecreeerd volgens de specificaties van Versie 5 van HL7 FHIR.

![&#x200B; het gegevenstype van de Beschikbaarheid structuur &#x200B;](../../../images/healthcare/data-types/availability/availability.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Available Time] | `availableTime` | Array van objecten | De tijd waarop het item beschikbaar is. Zie de [&#x200B; sectie hieronder &#x200B;](#available-time) voor meer informatie. |
| [!UICONTROL Not Available Time] | `notAvailableTime` | String | De tijd waarop het object niet beschikbaar is, met een opgegeven reden. Zie de [&#x200B; sectie hieronder &#x200B;](#not-available-time) voor meer informatie. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/availability.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/availability.schema.json)

## `availableTime` {#available-time}

`availableTime` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![&#x200B; Beschikbare tijdstructuur &#x200B;](../../../images/healthcare/data-types/availability/available-time.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL All Day] | `allDay` | Boolean | Een Booleaanse waarde die aangeeft of het item altijd beschikbaar is. |
| [!UICONTROL Available End Time] | `availableEndTime` | String | De tijd van de dag dat het item niet meer beschikbaar is. Dit wordt genegeerd als `allDay` `true` is. |
| [!UICONTROL Available Start Time] | `availableStartTime` | String | De tijd van de dag waarop het item beschikbaar wordt. Dit wordt genegeerd als `allDay` `true` is. |
| [!UICONTROL Days Of Week] | `daysOfWeek` | Array van tekenreeksen | Een array met tekenreeksen waarin wordt aangegeven welke dagen beschikbaar zijn. De waarden van deze eigenschap moeten gelijk zijn aan een of meer van de volgende bekende opsommingswaarden. <li> `mon` </li> <li> `tues` </li> <li> `wed` </li> <li> `thurs`</li>  <li> `fri` </li> <li> `sat`</li> <li> `sun`</li> |

## `notAvailableTime` {#not-available-time}

`notAvailableTime` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![&#x200B; niet beschikbare tijdstructuur &#x200B;](../../../images/healthcare/data-types/availability/not-available-time.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL During] | `during` | [[!UICONTROL Period]](../data-types/period.md) | De periode waarin het item niet meer beschikbaar is. |
| [!UICONTROL Description] | `description` | String | De reden waarom het object niet beschikbaar is. |
