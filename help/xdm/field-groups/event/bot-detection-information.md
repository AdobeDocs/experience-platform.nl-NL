---
title: Boot Detection Field Group
description: Leer over de het gebiedsgroep van de Detectie van de Bot (XDM) schemagebiedgroep.
exl-id: 8ade14a8-9a34-4060-95b2-812d1a21deeb
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 1%

---

# [!UICONTROL Bot Detection] veldgroep

[!UICONTROL Bot Detection] is een standaardgroep van het schemagebied voor de [[!DNL XDM ExperienceEvent]  klasse ](../../classes/experienceevent.md). De veldgroep biedt informatie over het door beide gegenereerde verkeer.

![ A diagram van de [!UICONTROL Bot Detection] gebiedsgroep.](../../images/field-groups/bot-detection-information.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|----------------------------|-----------------|-----------|---------------------------------------------------------|
| [!UICONTROL Bot Detection] | `botDetection` | object | Verstrekt informatie over allebei-geproduceerd verkeer. |
| [!UICONTROL Score] | `score` | getal | De beide waarschijnlijkheid scoren van nul tot en met één. Een score van nul betekent dat het verkeer geen bot is. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.schema.json)
