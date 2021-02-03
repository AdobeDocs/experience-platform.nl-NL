---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;webinteractie;datatype;data-type;data-type;
solution: Experience Platform
title: Gegevenstype webinteractie
topic: overview
description: Dit document biedt een overzicht van het gegevenstype Data Model (XDM) van het webinteractiemodel.
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 2%

---


# [!UICONTROL Web ] interactiondata type

[!UICONTROL De ] interactie van het Web is een standaardgegevenstype van de Gegevens van de Ervaring (XDM) dat informatie over interactie beschrijft die op een Web-pagina gebeurde nadat het aanvankelijke paginadaad werd voltooid. Het is bedoeld voor het opnemen van interacties in veelzijdige webtoepassingen die geen nieuwe pagina&#39;s laden, zoals webapps van één pagina (SPA).

<img src="../images/data-types/web-interaction.PNG" width="500" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL Meetlat]](./measure.md) | Een meting waarmee de klik van een webkoppeling wordt gevolgd. |
| `URL` | Tekenreeks | De werkelijke koppeling of URL die voor deze webinteractie wordt gebruikt. |
| `name` | Tekenreeks | De normatieve naam die voor deze webkoppeling wordt gebruikt. Dit wordt gebruikt voor classificatiedoeleinden. |
| `type` | Tekenreeks | Het koppelingstype. Deze eigenschap moet gelijk zijn aan een van de volgende opsommingswaarden: <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinteraction.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinteraction.schema.json)