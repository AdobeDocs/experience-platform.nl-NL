---
title: Gegevenstype Advertentie-einde
description: Dit document biedt een overzicht van het XDM-gegevenstype (Ad break Experience Data Model).
exl-id: dfe0c386-8459-440d-95b5-b2139fac0fc3
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 2%

---

# [!UICONTROL Ad break] gegevenstype

[!UICONTROL Ad break] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat beschrijft hoe een getimed advertentie in een getimed stuk media wordt opgenomen.

![Gegevenstypestructuur](../images/data-types/ad-break.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_dc.title` | Tekenreeks | Een vriendelijke naam voor het advertentieeinde. |
| `_id` | Tekenreeks | Een unieke id voor het advertentie-einde. |
| `offset` | Geheel | De verschuiving, in seconden, van het advertentieeinde vanaf het begin van de primaire inhoud. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.schema.json)
