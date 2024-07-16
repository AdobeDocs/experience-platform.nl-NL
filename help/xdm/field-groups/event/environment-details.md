---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;ExperienceEvent;fields;schema's;Schema's;Schema-ontwerp;veldgroep;veldgroep;milieu;omgevingsdetails;
solution: Experience Platform
title: Environment Details Schema Field Group
description: Leer over de het schemagebiedgroep van de Details van het Milieu ExperienceEvent.
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---


# [!UICONTROL Environment Details] schemaveldgroep

>[!NOTE]
>
>De namen van verschillende groepen schemavelden zijn gewijzigd. Zie het document op [ de naamupdates van de gebiedsgroep ](../name-updates.md) voor meer informatie.

[!UICONTROL Environment Details] is een standaardgroep van het schemagebied voor de [[!DNL XDM ExperienceEvent]  klasse ](../../classes/experienceevent.md) wordt gebruikt om informatie betreffende omgevingsdetails met betrekking tot een Gebeurtenis van de Ervaring zoals apparatendetails, browser informatie, lokale tijd, en andere geografische informatie te vangen die.

<img src="../../images/field-groups/environment-details.png" width="500" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `device` | [ Apparaat ](../../data-types/device.md) | Beschrijft een geïdentificeerd apparaat, toepassing of apparaat browser instantie die over zittingen, normaal door koekjes traceerbaar is. |
| `environment` | [ Milieu ](../../data-types/environment.md) | Beschrijft informatie over de situationele context van de gebeurtenisobservatie, specifiek die overgangsinformatie zoals de netwerk of softwareversies detailleert. |
| `placeContext` | [ context van de Plaats ](../../data-types/place-context.md) | Beschrijft de overgangsomstandigheden met betrekking tot de gebeurteniswaarneming. Voorbeelden zijn landspecifieke informatie zoals weer, lokale tijd, verkeer, dag van de week, werkdag vs. vakantie en werkuren. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.schema.json)
