---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;ExperienceEvent;fields;schema's;Schema's;Schema-ontwerp;mixin;mixin;omgeving;omgevingsdetails;
solution: Experience Platform
title: Mengsel met omgevingsdetails
topic: overview
description: Dit document biedt een overzicht van de mix ExperienceEvent Environment Details.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 1%

---


# [!UICONTROL Omgeving ] detailsmix

>[!NOTE]
>
>De namen van verschillende mengsels zijn gewijzigd. Zie het document op [mixin naamupdates](../name-updates.md) voor meer informatie.

[!UICONTROL Omgeving ] detailleert een standaardmix voor de  [[!DNL XDM ExperienceEvent] ](../../classes/individual-profile.md) klasse die wordt gebruikt om informatie over omgevingsdetails met betrekking tot een Experience Event vast te leggen, zoals apparaatdetails, browserinformatie, lokale tijd en andere geografische informatie.

<img src="../../images/mixins/environment-details.png" width="500" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `device` | [Apparaat](../../data-types/device.md) | Beschrijft een geïdentificeerd apparaat, toepassing of apparaat browser instantie die over zittingen, normaal door koekjes traceerbaar is. |
| `environment` | [Omgeving](../../data-types/environment.md) | Beschrijft informatie over de situationele context van de gebeurtenisobservatie, specifiek die overgangsinformatie zoals de netwerk of softwareversies detailleert. |
| `placeContext` | [Context plaatsen](../../data-types/place-context.md) | Beschrijft de overgangsomstandigheden met betrekking tot de gebeurteniswaarneming. Voorbeelden zijn landspecifieke informatie zoals weer, lokale tijd, verkeer, dag van de week, werkdag vs. vakantie en werkuren. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de mix:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.schema.json)
