---
title: Sitetool Details schema Field Group
description: Dit document biedt een overzicht van de veldgroep Sitetool Details.
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 2%

---

# [!UICONTROL Sitetool Details] schemaveldgroep

[!UICONTROL Sitetool Details] is een standaardschemagebiedgroep voor [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). De veldgroep bevat één `sitetool` object naar een schema, waarin informatie wordt vastgelegd die door een sitetool is verzameld.

![Groepsstructuur van veld](../../images/field-groups/sitetool-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `dataGatheringEvent` | Object | Geeft aan of deze gebeurtenis samen met andere gerelateerde details een gebeurtenis voor het verzamelen van gegevens is. Bevat de volgende eigenschappen:<ul><li>`data`: (Kaart) Bevat de JSON-gegevens die worden verzameld en verzonden als onderdeel van de gebeurtenis quizzen, enquêtes of opiniepeilingen verzenden.</li><li>`isTrue`: (Boolean) Geeft aan of deze gebeurtenis een gebeurtenis voor het verzamelen van gegevens is, zoals quiz, enquête of opiniepeiling.</li><li>`score`: (Geheel getal) De score die door de actor is behaald op basis van gebeurtenisreacties.</li></ul> |
| `actor` | Tekenreeks | Een persoon/lid die de handeling heeft verricht. |
| `actorID` | Tekenreeks | Een unieke id voor de persoon/het lid die de handeling heeft uitgevoerd. |
| `isKeyEvent` | Boolean | Geeft aan of deze gebeurtenis een toetsgebeurtenis is. |
| `name` | Tekenreeks | De naam van de sitetool, zoals chatbot, enquête, enzovoort. |
| `section` | Tekenreeks | De relevante sectie van de sitetool, zoals hoofd of sub. |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over de veldgroep raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-healthcare-sitetool.schema.json).
