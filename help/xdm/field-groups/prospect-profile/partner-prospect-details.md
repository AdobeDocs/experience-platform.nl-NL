---
title: Deelvenstergegevens (voorbeeld)
description: Leer over de het schemagebiedgroep van de de Details van het Vooruitzicht van de Partner (Steekproef) (XDM).
exl-id: 2de1eb7a-2e44-4417-9bdd-7a8a4b2d3a7f
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---

# [!UICONTROL Partner Prospect Details (Sample)] veldgroep

[!UICONTROL Partner Prospect Details (Sample)] is een standaardgroep van het schemagebied voor de [[!DNL XDM ExperienceEvent]  klasse ](../../classes/experienceevent.md). [!UICONTROL Partner Prospect Details (Sample)] verstrekt een steekproefkader voor diverse details met betrekking tot het profiel van een vooruitzicht. Dit kader stroomlijnt het proces van het organiseren en beheren van diverse informatie met betrekking tot het vooruitzicht.

Deze gebiedsgroep breidt de [ Individuele klasse van het Profiel van het Vooruitzicht ](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/prospect.html) binnen de context van een partner uit.

![ A diagram van de [!UICONTROL Partner Prospect Details (Sample)] gebiedsgroep.](../../images/field-groups/partner/partner-prospect-details-sample.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|---------------------------------------|-----------------------------|-----------|--------------------------------------------------|
| [!UICONTROL ageRangeInHousehold] | `ageRangeInHousehold` | string | Leeftijdsbereik binnen het huishouden. |
| [!UICONTROL apparelAccessories] | `apparelAccessories` | string | Voorkeuren of betrokkenheid bij kleding/accessoires. |
| [!UICONTROL bicycling] | `bicycling` | string | Belang of betrokkenheid bij fietsactiviteiten. |
| [!UICONTROL cableTv] | `cableTv` | string | Geeft de betrokkenheid met kabeltelevisie aan. |
| [!UICONTROL domestics] | `domestics` | string | Voorkeuren of betrokkenheid bij binnenlandse activiteiten. |
| [!UICONTROL electronics] | `electronics` | string | interesse of betrokkenheid in elektronische apparaten. |
| [!UICONTROL foodAndBeverage] | `foodAndBeverage` | string | Voorkeuren of betrokkenheid bij voedsel/drank. |
| [!UICONTROL footwear] | `footwear` | string | Belang of betrokkenheid bij schoenen. |
| [!UICONTROL healthFoods] | `healthFoods` | string | Voorkeuren of betrokkenheid bij voedingsmiddelen voor de gezondheid. |
| [!UICONTROL hiking] | `hiking` | string | Belang of betrokkenheid bij wandelactiviteiten. |
| [!UICONTROL householdId] | `householdId` | string | Een unieke identificatie voor het huishouden. |
| [!UICONTROL individualId] | `individualId` | string | Een unieke id voor het individu. |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | string | De conclusie dat je een kaarthouder bent. |
| [!UICONTROL inferredPremiumCardholder] | `inferredPremiumCardholder]` | string | De conclusie dat het een premiumkaarthouder is. |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | string | Een indicator van het passende niveau. |
| [!UICONTROL BuyerRating] | `buyerRating` | string | Een beoordeling voor koopgedrag. |
| [!UICONTROL DonorRating] | `donorRating` | string | Een beoordeling die verband houdt met het gedrag van de donor. |
| [!UICONTROL InvestmentRating] | `investmentRating` | string | Een rating die verband houdt met beleggingsgedrag. |
| [!UICONTROL ResponderRating] | `responderRating` | string | Een classificatie die gerelateerd is aan het gedrag van de beantwoorder. |
| [!UICONTROL SpendingVelocity] | `spendingVelocity` | string | De snelheid of het bestedingspercentage. |
| [!UICONTROL SpendingVolume] | `spendingVolume` | string | Het bedrag of de omvang van de uitgaven. |
| [!UICONTROL recordId] | `recordId` | string | Een unieke id voor de record. |
| [!UICONTROL residenceId] | `residenceId` | string | Een unieke id voor de woonplaats. |
| [!UICONTROL sailing] | `sailing` | string | Geeft de interesse of betrokkenheid bij zeilactiviteiten aan. |
| [!UICONTROL seasonalHolidayProducts] | `seasonalHolidayProducts` | string | Hiermee geeft u de voorkeuren of betrokkenheid bij vakantieproducten aan. |
| [!UICONTROL skiing] | `skiing` | string | Geeft de interesse of betrokkenheid bij skiactiviteiten aan. |
| [!UICONTROL tennis] | `tennis` | string | Geeft de belangstelling voor of betrokkenheid bij tennisactiviteiten aan. |
| [!UICONTROL tvShoppers] | `tvShoppers` | string | Geeft de betrokkenheid bij tv-winkelen aan. |

{style="table-layout:auto"}

Voor meer details op de gebiedsgroep, verwijs naar het [ volledige schema ](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-prospect/merkle/prospect-details-partner-sample.schema.json) op de openbare bewaarplaats XDM.
