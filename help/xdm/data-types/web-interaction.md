---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;webinteractie;datatype;data-type;data-type;
solution: Experience Platform
title: Gegevenstype webinteractie
description: Meer informatie over het gegevenstype Data Model (XDM) van het webinteractieervaringsgegevensmodel.
exl-id: 772d96c5-9fa3-4fed-8b38-16b8e7101743
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# [!UICONTROL Web interaction] gegevenstype

[!UICONTROL Web interaction] is een standaard gegevenstype van het Gegevensmodel van de Ervaring (XDM) dat informatie over interactie beschrijft die op een Web-pagina gebeurde nadat het aanvankelijke paginading werd voltooid. Het is bedoeld voor het opnemen van interacties in veelzijdige webtoepassingen die geen nieuwe pagina&#39;s laden, zoals webapps van één pagina (SPA).

<img src="../images/data-types/web-interaction.PNG" width="500" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL Measure]](./measure.md) | Een meting waarmee de klik van een webkoppeling wordt bijgehouden. |
| `URL` | String | De werkelijke koppeling of URL die voor deze webinteractie wordt gebruikt. |
| `name` | String | De normatieve naam die voor deze webkoppeling wordt gebruikt. Dit wordt gebruikt voor classificatiedoeleinden. |
| `type` | String | Het koppelingstype. Deze eigenschap moet gelijk zijn aan een van de volgende opsommingswaarden: <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.schema.json)
