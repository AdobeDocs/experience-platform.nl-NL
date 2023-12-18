---
title: Boot Detection Field Group
description: Leer over de het gebiedsgroep van de Detectie van de Bot (XDM) schemagebiedgroep.
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 1%

---

# [!UICONTROL Bot Detection] veldgroep

[!UICONTROL Bot Detection] is een standaardschemagebiedgroep voor [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). De veldgroep biedt informatie over het door beide gegenereerde verkeer.

![Een schema van de [!UICONTROL Bot Detection] veldgroep.](../../images/field-groups/bot-detection-information.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|----------------------------|-----------------|-----------|---------------------------------------------------------|
| [!UICONTROL Bot Detection] | `botDetection` | object | Verstrekt informatie over allebei-geproduceerd verkeer. |
| [!UICONTROL Score] | `score` | getal | De beide waarschijnlijkheid scoren van nul tot en met één. Een score van nul betekent dat het verkeer geen bot is. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.schema.json)

