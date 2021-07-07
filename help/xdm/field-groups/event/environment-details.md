---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;field group;field group;environment;environment details;
solution: Experience Platform
title: Environment Details Schema Field Group
topic-legacy: overview
description: Dit document biedt een overzicht van de veldgroep met de gegevens van het schema ExperienceEvent Environment.
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# [!UICONTROL Environment Details] schema field group

>[!NOTE]
>
>The names of several schema field groups have changed. See the document on [field group name updates](../name-updates.md) for more information.

[!UICONTROL Environment Details] is een standaardschemagebiedgroep voor de  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) klasse die wordt gebruikt om informatie betreffende omgevingsdetails met betrekking tot een Gebeurtenis van de Ervaring zoals apparatendetails, browser informatie, lokale tijd, en andere geografische informatie te vangen.

<img src="../../images/field-groups/environment-details.png" width="500" /><br />

| Eigenschap | Data type | Beschrijving |
| --- | --- | --- |
| `device` | [Apparaat](../../data-types/device.md) | Beschrijft een geïdentificeerd apparaat, toepassing of apparaat browser instantie die over zittingen, normaal door koekjes traceerbaar is. |
| `environment` | [Omgeving](../../data-types/environment.md) | Beschrijft informatie over de situationele context van de gebeurtenisobservatie, specifiek die overgangsinformatie zoals de netwerk of softwareversies detailleert. |
| `placeContext` | [Context plaatsen](../../data-types/place-context.md) | Describes the transient circumstances related to the event observation. Voorbeelden zijn landspecifieke informatie zoals weer, lokale tijd, verkeer, dag van de week, werkdag vs. vakantie en werkuren. |

{style=&quot;table-layout:auto&quot;}

For more details on the field group, refer to the public XDM repository:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.schema.json)
