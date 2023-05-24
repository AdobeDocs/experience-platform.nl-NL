---
title: Gegevenstype implementatiedetails
description: Dit document biedt een overzicht van het gegevenstype Experience Data Model (XDM) van de implementatiedetails.
exl-id: d3d16bae-196b-489d-8590-fd22150eedf1
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 3%

---

# [!UICONTROL Implementation details] gegevenstype

[!UICONTROL Implementation details] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat een technologieimplementatie, zoals API of SDK beschrijft.

![Gegevenstypestructuur](../images/data-types/implementation-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `environment` | Tekenreeks | De omgeving van de uitvoering. |
| `name` | Tekenreeks | De id voor de SDK of het eindpunt. Alle SDK&#39;s of eindpunten worden geïdentificeerd aan de hand van een URI, inclusief extensies. |
| `version` | Tekenreeks | De versie van de API of SDK. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json)
