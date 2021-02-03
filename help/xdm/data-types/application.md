---
keywords: Experience Platform;thuis;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;toepassing;datatype;data-type;data-type;
solution: Experience Platform
title: Gegevenstype toepassing
topic: overview
description: Dit document biedt een overzicht van het gegevenstype Application Experience Data Model (XDM).
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 1%

---


# [!UICONTROL Het ] gegevenstype ApplicationData

[!UICONTROL De ] toepassing is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat details met betrekking tot de toepassing beschrijft geproduceerde interactie. Een toepassing verwijst naar een softwareervaring, zoals een mobiele toepassing of bureaubladtoepassing die door een eindgebruiker kan worden geïnstalleerd, uitgevoerd, gesloten of verwijderd. De eigenschappen voor dit gegevenstype zijn niet bedoeld voor het beschrijven van agents zoals chatbots, browsergebaseerde plug-ins of andere ervaringen die niet van toepassing zijn op toepassingen.

<img src="../images/data-types/application.PNG" width="500" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL Meetlat]](./measure.md) | Beschrijft details over de beëindiging van een toepassing. |
| `crashes` | [[!UICONTROL Meetlat]](./measure.md) | Deze eigenschap wordt geactiveerd wanneer de toepassing niet volgens plan wordt afgesloten. |
| `featureUsages` | [[!UICONTROL Meetlat]](./measure.md) | Beschrijft om het even welke gegevens van de activering van een toepassingseigenschap die worden gemeten. |
| `firstLaunches` | [[!UICONTROL Meetlat]](./measure.md) | Bevat gegevens over de eerste keer starten. Deze eigenschap wordt geactiveerd bij de eerste keer dat de toepassing na de installatie wordt gestart. |
| `installs` | [[!UICONTROL Meetlat]](./measure.md) | Registreert de installatie van een toepassing op een apparaat wanneer een specifieke installatiegebeurtenis beschikbaar is. |
| `launches` | [[!UICONTROL Meetlat]](./measure.md) | Beschrijft een waarde verbonden aan de lancering van een toepassing. Dit wordt geactiveerd bij elke uitvoering, inclusief crashes, installaties en het hervatten vanaf de achtergrond wanneer de sessietime-out is overschreden. |
| `upgrades` | [[!UICONTROL Meetlat]](./measure.md) | Bevat gegevens over de verbetering van een toepassing die eerder geïnstalleerd is. Dit wordt geactiveerd bij de eerste introductie na een upgrade. |
| `id` | Tekenreeks | Een unieke id voor de toepassing. |
| `name` | Tekenreeks | De naam van de toepassing. |
| `userPerspective` | Tekenreeks | Het perspectief of de fysieke relatie tussen de gebruiker en de app of het merk op het moment dat een gebeurtenis plaatsvond. Als u het perspectief van de gebruiker ten opzichte van de app begrijpt, kunt u beter sessies op de juiste wijze genereren omdat het grootste deel van de tijd dat u geen gebeurtenissen `background` en `detached` wilt opnemen als onderdeel van een &quot;actieve&quot; sessie. De waarde van deze eigenschap moet gelijk zijn aan een van de onderstaande opsommingswaarden. <li> `foreground`: De gebruiker en de toepassing communiceren rechtstreeks met elkaar. </li> <li> `background`: De toepassing en de gebruiker communiceren indirect met elkaar. De app kan bijvoorbeeld een waarde meten en vernieuwen terwijl het scherm vergrendeld is of een andere app op de voorgrond wordt gebruikt.  </li> <li> `detached`: Ontkoppeld betekent dat de gebeurtenis gerelateerd was aan de app, maar niet rechtstreeks afkomstig was uit de app, zoals het verzenden van een e-mail- of pushmelding vanuit een extern systeem. |
| `version` | Tekenreeks | De versie van de toepassing. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)