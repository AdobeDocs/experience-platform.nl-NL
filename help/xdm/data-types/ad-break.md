---
title: Gegevenstype Advertentie-einde
description: Dit document biedt een overzicht van het XDM-gegevenstype (Ad break Experience Data Model).
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# [!UICONTROL Ad break] gegevenstype

[!UICONTROL Ad break] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat beschrijft hoe een getimed advertentie in een getimed stuk media wordt opgenomen.

![Gegevenstypestructuur](../images/data-types/ad-break.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_dc.title` | Tekenreeks | Een vriendelijke naam voor het advertentieeinde. |
| `_id` | Tekenreeks | Een unieke id voor het advertentie-einde. |
| `offset` | Geheel | De verschuiving, in seconden, van het advertentieeinde vanaf het begin van de primaire inhoud. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.schema.json)
