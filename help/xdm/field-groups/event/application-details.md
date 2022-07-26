---
title: Toepassingsdetails, schema, veldgroep
description: Dit document biedt een overzicht van de veldgroep Application Details-schema.
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# [!UICONTROL Application Details] schemaveldgroep

[!UICONTROL Application Details] is een standaardschemagebiedgroep voor [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). De veldgroep bevat één `application` object naar een schema waarin toepassingsgerelateerde details zoals vastlopen, gebruik van functies, opstarten en upgrades worden vastgelegd.

![](../../images/field-groups/application-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `application` | [[!UICONTROL Application]](../../data-types/financial-account.md) | Hiermee worden toepassingsgegevens vastgelegd die betrekking hebben op een gebeurtenis, zoals de naam van de toepassing, de toepassingsversie, de installatie, het starten, het vastlopen en het sluiten van de toepassing. Het kan ofwel de toepassing zijn waarop de gebeurtenis betrekking heeft (zoals de bestemming voor een pushmelding die wordt verzonden) of de toepassing die de gebeurtenis veroorzaakt (zoals een klik of een aanmelding). |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over de veldgroep raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-application.schema.json).
