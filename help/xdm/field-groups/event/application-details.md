---
title: Toepassingsdetails, schema, veldgroep
description: Leer meer over de het schemagebiedgroep van de Details van de Toepassing.
exl-id: 5df99f9a-b36a-4c2b-a4a4-d3cf054f09b8
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# [!UICONTROL Application Details] schemaveldgroep

[!UICONTROL Application Details] is een standaardgroep van het schemagebied voor de [[!DNL XDM ExperienceEvent]  klasse ](../../classes/experienceevent.md). De veldgroep biedt één `application` -object aan een schema dat toepassingsgerelateerde details zoals vastlopen, eigenschapgebruik, opstarten en upgrades vastlegt.

![](../../images/field-groups/application-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `application` | [[!UICONTROL Application]](../../data-types/financial-account.md) | Hiermee worden toepassingsgegevens vastgelegd die betrekking hebben op een gebeurtenis, zoals de naam van de toepassing, de toepassingsversie, de installatie, het starten, het vastlopen en het sluiten van de toepassing. Het kan ofwel de toepassing zijn waarop de gebeurtenis betrekking heeft (zoals de bestemming voor een pushmelding die wordt verzonden) of de toepassing die de gebeurtenis veroorzaakt (zoals een klik of een aanmelding). |

{style="table-layout:auto"}

Voor meer details op de gebiedsgroep, verwijs naar de [ openbare bewaarplaats XDM ](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-application.schema.json).
