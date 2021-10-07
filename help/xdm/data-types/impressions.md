---
title: Gegevenstype Impressies
description: Dit document biedt een overzicht van het XDM-gegevenstype voor afdrukken.
source-git-commit: 7fc16546176d196582a3cdfcee51f799eeef9788
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 2%

---

# [!UICONTROL Impressions] gegevenstype

[!UICONTROL Impressions] is een standaard XDM-gegevenstype dat een marketingindruk beschrijft. Dit is een maatstaf die wordt gebruikt om het aantal digitale weergaven of opdrachten voor inhoud zoals een advertentie, digitale post of webpagina te kwantificeren.

![](../images/data-types/impressions.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `ID` | Tekenreeks | Een unieke id voor de indruk. |
| `displays` | Geheel | Het aantal keren dat het impositie-item aan een klant is getoond. |
| `selected` | Geheel | Het aantal keren dat het afbeeldingsitem is geselecteerd of geklikt. |
| `type` | Tekenreeks | Het type indruk. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.schema.json)
