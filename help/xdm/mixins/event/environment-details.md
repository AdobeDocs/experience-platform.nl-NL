---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;mixin;mixin;environment;environment details;
solution: Experience Platform
title: ExperienceEvent-omgevingsdetails mixen
topic: overview
description: Dit document biedt een overzicht van de mix ExperienceEvent Environment Details.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 1%

---


# [!UICONTROL ExperienceEvent-omgevingsdetails] mixin

[!UICONTROL De de milieudetails] van ExperienceEvent is een standaardmengeling voor de [[!DNL XDM ExperienceEvent] klasse](../../classes/individual-profile.md) die wordt gebruikt om informatie betreffende omgevingsdetails met betrekking tot een Gebeurtenis van de Ervaring zoals apparatendetails, browser informatie, lokale tijd, en andere geografische informatie te vangen.

<img src="../../images/mixins/environment-details.png" width="500" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `device` | [Apparaat](../../data-types/device.md) | Beschrijft een geïdentificeerd apparaat, toepassing of apparaat browser instantie die over zittingen, normaal door koekjes traceerbaar is. |
| `environment` | [Omgeving](../../data-types/environment.md) | Beschrijft informatie over de situationele context van de gebeurtenisobservatie, specifiek die overgangsinformatie zoals de netwerk of softwareversies detailleert. |
| `placeContext` | [Context plaatsen](../../data-types/place-context.md) | Beschrijft de overgangsomstandigheden met betrekking tot de gebeurteniswaarneming. Voorbeelden zijn landspecifieke informatie zoals weer, lokale tijd, verkeer, dag van de week, werkdag vs. vakantie en werkuren. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de mix:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.schema.json)
