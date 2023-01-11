---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;Webpagina-details;datatype;gegevenstype;gegevenstype;webpagina
solution: Experience Platform
title: Gegevenstype webgegevens
description: Dit document biedt een overzicht van het gegevenstype van het XDM (Web Information Experience Data Model).
exl-id: bfb00835-5908-4baf-af2a-6d845710e340
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# [!UICONTROL Web information] gegevenstype

[!UICONTROL Web information] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat informatie beschrijft die via een Gebeurtenis van de Ervaring wordt geregistreerd die voor het World Wide Web kanaal, met inbegrip van de Web-pagina, de verwijzer, en/of de verbinding met betrekking tot de op-pagina interactie specifiek is.

![](../images/data-types/web-information.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `webInteraction` | [[!UICONTROL Web interaction]](./web-interaction.md) | Beschrijft de details over de Webverbinding of URL die aan de interactie beantwoordt. |
| `webPageDetails` | [[!UICONTROL Web page details]](./webpage-details.md) | Beschrijft de details over de Web-pagina waar de Webinteractie voorkwam. |
| `webReferrer` | [!UICONTROL Object] | Beschrijft de referentie van een Webinteractie, die URL is een bezoeker van onmiddellijk vóór de huidige Webinteractie kwam werd geregistreerd. Bevat de volgende subeigenschappen: <ul><li>`URL`: De referentie-URL.</li><li>`type`: Het verwijzingstype.</li></ul> |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.schema.json)
