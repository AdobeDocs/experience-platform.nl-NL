---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;ExperienceEvent;fields;schema's;Schema's;Schema-ontwerp;veldgroep;veldgroep;
solution: Experience Platform
title: Veld groep kanaaldetails
topic-legacy: overview
description: Dit document biedt een overzicht van de veldgroep Kanaaldetails.
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# [!UICONTROL Channel Details] schemaveldgroep

>[!NOTE]
>
>De namen van verschillende groepen schemavelden zijn gewijzigd. Zie het document op [updates van de gebiedsgroepnaam](../name-updates.md) voor meer informatie.

[!UICONTROL Channel Details] is een standaardschemaveldgroep voor de  [[!DNL XDM ExperienceEvent] klasse](../../classes/experienceevent.md), die wordt gebruikt om kanaalinformatie zoals identiteitskaart, kanaaltype, media type, en plaatstype te beschrijven.

![](../../images/field-groups/channel-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `channel` | [Experience Channel](../../data-types/experience-channel.md) | Een object dat productretourneert, garantieregistratie en processen voor winkelwagentjes/bestellingen beschrijft. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.schema.json)
