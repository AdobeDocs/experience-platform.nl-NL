---
title: Gegevenstype periode
description: Leer over het gegevenstype van het Gegevensmodel van de Ervaring van de Periode (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: aecd09e4-2797-4d2d-be62-acad28fb7bba
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 1%

---

# [!UICONTROL Period] gegevenstype

[!UICONTROL Period] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat een tijdspanne verstrekt die door een begin en einddatum/tijd wordt bepaald. Dit gegevenstype wordt gecreeerd volgens de specificaties van Versie 5 van HL7 FHIR.

![&#x200B; het gegevenstype van de Periode structuur &#x200B;](../../../images/healthcare/data-types/period.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL End] | `end` | DateTime | De einddatum en -tijd. |
| [!UICONTROL Start] | `start` | DateTime | De begindatum en -tijd. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.schema.json)
