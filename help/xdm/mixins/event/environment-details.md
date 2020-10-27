---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;mixin;mixin;environment;environment details;
solution: Experience Platform
title: Mengsel van omgevingsdetails
topic: overview
description: Dit document biedt een overzicht van de mix ExperienceEvent Environment Details.
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 1%

---


# [!UICONTROL Mengsel van omgevingsdetails]

>[!NOTE]
>
>De namen van verschillende mengsels zijn gewijzigd. Zie het document over de updates [van de](../name-updates.md) mixnaam voor meer informatie.

[!UICONTROL De Details] van het milieu is een standaardmengeling voor de [[!DNL XDM ExperienceEvent] klasse](../../classes/individual-profile.md) die wordt gebruikt om informatie betreffende omgevingsdetails met betrekking tot een Gebeurtenis van de Ervaring zoals apparatendetails, browser informatie, lokale tijd, en andere geografische informatie te vangen.

<img src="../../images/mixins/environment-details.png" width="500" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `device` | [Apparaat](../../data-types/device.md) | Beschrijft een geïdentificeerd apparaat, toepassing of apparaat browser instantie die over zittingen, normaal door koekjes traceerbaar is. |
| `environment` | [Omgeving](../../data-types/environment.md) | Beschrijft informatie over de situationele context van de gebeurtenisobservatie, specifiek die overgangsinformatie zoals de netwerk of softwareversies detailleert. |
| `placeContext` | [Context plaatsen](../../data-types/place-context.md) | Beschrijft de overgangsomstandigheden met betrekking tot de gebeurteniswaarneming. Voorbeelden zijn landspecifieke informatie zoals weer, lokale tijd, verkeer, dag van de week, werkdag vs. vakantie en werkuren. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de mix:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.schema.json)
