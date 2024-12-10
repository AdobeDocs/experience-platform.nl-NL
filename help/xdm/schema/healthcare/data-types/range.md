---
title: Gegevenstype bereik
description: Leer over het gegevenstype van de Gegevens van de Ervaring van de Waaier Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 66f8b574-04d9-435f-8743-4ff89c4c0079
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 1%

---

# [!UICONTROL Range] gegevenstype

[!UICONTROL Range] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat een reeks waarden verstrekt die door lage en hoge waarden worden gebonden. Dit gegevenstype wordt gecreeerd volgens de specificaties van Versie 5 van HL7 FHIR.

![ het gegevenstype van de Waaier structuur ](../../../images/healthcare/data-types/range.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL High] | `high` | [[!UICONTROL Simple Quantity]](../data-types/simple-quantity.md) | De hoogste limiet. |
| [!UICONTROL Low] | `low` | [[!UICONTROL Simple Quantity]](../data-types/simple-quantity.md) | De laagste limiet. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/range.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/range.schema.json)
