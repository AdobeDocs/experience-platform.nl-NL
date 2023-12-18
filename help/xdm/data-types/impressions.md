---
title: Gegevenstype Impressies
description: Leer meer over het XDM-gegevenstype Impressions.
exl-id: 1e758043-a41e-45f7-ae8b-514990d0649e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# [!UICONTROL Impressions] gegevenstype

[!UICONTROL Impressions] is een standaard XDM-gegevenstype dat een marketingindruk beschrijft. Dit is een maatstaf die wordt gebruikt om het aantal digitale weergaven of opdrachten voor inhoud zoals een advertentie, digitale post of webpagina te kwantificeren.

![](../images/data-types/impressions.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `ID` | String | Een unieke id voor de indruk. |
| `displays` | Geheel | Het aantal keren dat het impositie-item aan een klant is getoond. |
| `selected` | Geheel | Het aantal keren dat het afbeeldingsitem is geselecteerd of geklikt. |
| `type` | String | Het type indruk. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.schema.json)
