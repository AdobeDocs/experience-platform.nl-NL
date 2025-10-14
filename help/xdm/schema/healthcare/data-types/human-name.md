---
title: Gegevenstype naam
description: Leer over het gegevenstype van het Gegevensmodel van de Ervaring van de Menselijke (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 5dd6fda4-c076-4c34-bdd9-259203b6ea73
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# [!UICONTROL Human Name] gegevenstype

[!UICONTROL Human Name] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat informatie over de naam van een mens of een andere levende entiteit verstrekt. Dit gegevenstype wordt gecreeerd volgens de specificaties van Versie 5 van HL7 FHIR.

![&#x200B; het gegevenstype van de Naam van het Mens structuur &#x200B;](../../../images/healthcare/data-types/human-name.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Period] | `period` | [[!UICONTROL Period]](../data-types/period.md) | De tijdsperiode waarin de naam wordt of werd gebruikt. |
| [!UICONTROL Family] | `family` | String | De familie of achternaam. |
| [!UICONTROL Given] | `given` | Array van tekenreeksen | De opgegeven naam, met inbegrip van alle middelste namen. |
| [!UICONTROL Prefix] | `prefix` | Array van tekenreeksen | Alle delen van de naam vóór de opgegeven of voornaam. |
| [!UICONTROL Suffix] | `suffix` | Array van tekenreeksen | Alle delen van de naam na de familie of achternaam. |
| [!UICONTROL Text] | `text` | String | De representatie van de volledige naam in normale tekst. |
| [!UICONTROL Use] | `use` | String | Het gebruik van de naam. De waarden van deze eigenschap moeten gelijk zijn aan een of meer van de volgende bekende opsommingswaarden. <li> `usual` </li> <li> `offical` </li> <li> `temp` </li> <li> `nickname` </li> <li> `anonymous` </li> <li> `old` </li> <li> `maiden` </li> |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/humanname.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/humanname.schema.json)
