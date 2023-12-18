---
title: Gegevenstype implementatiedetails
description: Meer informatie over het gegevenstype Experience Data Model (XDM) voor implementatiedetails.
exl-id: d3d16bae-196b-489d-8590-fd22150eedf1
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 1%

---

# [!UICONTROL Implementation details] gegevenstype

[!UICONTROL Implementation details] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat een technologieimplementatie, zoals API of SDK beschrijft.

![Gegevenstypestructuur](../images/data-types/implementation-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `environment` | String | De omgeving van de uitvoering. |
| `name` | String | De id voor de SDK of het eindpunt. Alle SDK&#39;s of eindpunten worden geïdentificeerd aan de hand van een URI, inclusief extensies. |
| `version` | String | De versie van de API of SDK. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json)
