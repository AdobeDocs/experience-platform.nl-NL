---
title: Gegevenstype contactpunt
description: Leer over het de gegevenstype van de Gegevens van de Ervaring van het Punt van het Contact Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: bbb9a5e1-b0d5-4c07-93a9-c1573dacad73
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# [!UICONTROL Contact Point] gegevenstype

[!UICONTROL Contact Point] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat contactdetails voor een persoon beschrijft. Dit gegevenstype wordt gecreeerd volgens de specificaties van Versie 5 van HL7 FHIR.

![&#x200B; het gegevenstype van het Punt van het Contact structuur &#x200B;](../../../images/healthcare/data-types/contact-point.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Period] | `period` | [[!UICONTROL Period]](../data-types/period.md) | De periode waarin het contactpunt in gebruik was/is. |
| [!UICONTROL Rank] | `rank` | Geheel | De rang die op het aangewezen gebruik van het contactpunt wijst. De minimumwaarde is `1` en de maximumwaarde is `2147483647` waarbij `1` de hoogste specificiteit heeft. |
| [!UICONTROL System] | `system` | String | Het systeem waarmee contact met hen kan worden opgenomen. De waarde van deze eigenschap moet gelijk zijn aan een van de volgende bekende opsommingswaarden. <li> `phone` </li> <li> `fax` </li> <li> `email` </li> <li> `pager`</li> <li> `url`</li> <li> `sms`</li> <li> `other`</li> |
| [!UICONTROL Use] | `use` | String | Het doel van het contactpunt. De waarde van deze eigenschap moet gelijk zijn aan een van de volgende bekende opsommingswaarden. <li> `home` </li> <li> `work` </li> <li> `temp` </li> <li> `old`</li> <li> `mobile`</li> |
| [!UICONTROL Value] | `value` | String | De gegevens van het contactpunt. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/contactpoint.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/contactpoint.schema.json)
