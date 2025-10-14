---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;ExperienceEvent;fields;schema's;Schema's;Schema-ontwerp;veldgroep;veldgroep;milieu;omgevingsdetails;
solution: Experience Platform
title: Environment Details Schema Field Group
description: Leer over de het schemagebiedgroep van de Details van het Milieu ExperienceEvent.
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---


# [!UICONTROL Environment Details] schemaveldgroep

>[!NOTE]
>
>De namen van verschillende groepen schemavelden zijn gewijzigd. Zie het document op [&#x200B; de naamupdates van de gebiedsgroep &#x200B;](../name-updates.md) voor meer informatie.

[!UICONTROL Environment Details] is een standaardgroep van het schemagebied voor de [[!DNL XDM ExperienceEvent]  klasse &#x200B;](../../classes/experienceevent.md) wordt gebruikt om informatie betreffende omgevingsdetails met betrekking tot een Gebeurtenis van de Ervaring zoals apparatendetails, browser informatie, lokale tijd, en andere geografische informatie te vangen die.

![](../../images/field-groups/environment-details.png){width=500}

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `device` | [&#x200B; Apparaat &#x200B;](../../data-types/device.md) | Beschrijft een geïdentificeerd apparaat, toepassing of apparaat browser instantie die over zittingen, normaal door koekjes traceerbaar is. |
| `environment` | [&#x200B; Milieu &#x200B;](../../data-types/environment.md) | Beschrijft informatie over de situationele context van de gebeurtenisobservatie, specifiek die overgangsinformatie zoals de netwerk of softwareversies detailleert. |
| `placeContext` | [&#x200B; context van de Plaats &#x200B;](../../data-types/place-context.md) | Beschrijft de overgangsomstandigheden met betrekking tot de gebeurteniswaarneming. Voorbeelden zijn landspecifieke informatie zoals weer, lokale tijd, verkeer, dag van de week, werkdag vs. vakantie en werkuren. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.schema.json)
