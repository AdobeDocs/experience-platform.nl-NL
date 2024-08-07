---
title: Sitetool Details schema Field Group
description: Meer informatie over de veldgroep Sitetool Details.
exl-id: 472c0a3f-efda-49af-9490-f2de90b348c0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# [!UICONTROL Sitetool Details] schemaveldgroep

[!UICONTROL Sitetool Details] is een standaardgroep van het schemagebied voor de [[!DNL XDM ExperienceEvent]  klasse ](../../classes/experienceevent.md). De veldgroep biedt één `sitetool` -object aan een schema, dat informatie vastlegt die door een sitetool is verzameld.

![ de groepsstructuur van het Gebied ](../../images/field-groups/sitetool-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `dataGatheringEvent` | Object | Geeft aan of deze gebeurtenis samen met andere gerelateerde details een gebeurtenis voor het verzamelen van gegevens is. Bevat de volgende eigenschappen:<ul><li>`data`: (Kaart) Bevat de JSON-gegevens die zijn verzameld en verzonden als onderdeel van de verzendgebeurtenis voor quiz, enquête of opiniepeiling.</li><li>`isTrue`: (Boolean) Geeft aan of deze gebeurtenis een gebeurtenis voor het verzamelen van gegevens is, zoals quiz, enquête of opiniepeiling.</li><li>`score`: (Geheel getal) De score die de actor heeft behaald op basis van gebeurtenisreacties.</li></ul> |
| `actor` | String | Een persoon/lid die de handeling heeft verricht. |
| `actorID` | String | Een unieke id voor de persoon/het lid die de handeling heeft uitgevoerd. |
| `isKeyEvent` | Boolean | Geeft aan of deze gebeurtenis een toetsgebeurtenis is. |
| `name` | String | De naam van de sitetool, zoals chatbot, enquête, enzovoort. |
| `section` | String | De relevante sectie van de sitetool, zoals hoofd of sub. |

{style="table-layout:auto"}

Voor meer details op de gebiedsgroep, verwijs naar de [ openbare bewaarplaats XDM ](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-healthcare-sitetool.schema.json).
