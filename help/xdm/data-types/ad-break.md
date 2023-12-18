---
title: Gegevenstype Advertentie-einde
description: Leer over het gegevenstype Adbreak Experience Data Model (XDM).
exl-id: dfe0c386-8459-440d-95b5-b2139fac0fc3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 1%

---

# [!UICONTROL Ad break] gegevenstype

[!UICONTROL Ad break] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat beschrijft hoe een getimed advertentie in een getimed stuk media wordt opgenomen.

![Gegevenstypestructuur](../images/data-types/ad-break.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_dc.title` | String | Een vriendelijke naam voor het advertentieeinde. |
| `_id` | String | Een unieke id voor het advertentie-einde. |
| `offset` | Geheel | De verschuiving, in seconden, van het advertentieeinde vanaf het begin van de primaire inhoud. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.schema.json)
