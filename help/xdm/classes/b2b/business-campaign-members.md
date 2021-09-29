---
title: Klasse XDM Business Campaign-leden
description: Dit document biedt een overzicht van de klasse XDM Business Campaign members in Experience Data Model (XDM).
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 2%

---

# [!UICONTROL XDM Business Campaign Members] klasse (bèta)

>[!IMPORTANT]
>
>Deze klasse is beschikbaar als onderdeel van Real-time Customer Data Platform B2B Edition, dat momenteel in bèta wordt weergegeven. De documentatie en functionaliteit kunnen worden gewijzigd.

[!UICONTROL XDM Business Campaign Members] is een standaardklasse van de Gegevens van de Ervaring van het Model (XDM) die een contact of een lood verbonden aan een bedrijfscampagne beschrijft.

![](../../images/classes/b2b/business-campaign-members.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de bijbehorende campagne. |
| `campaignMemberKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de entiteit die lid is van de campagne. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Als het campagnerelid uit een extern bronsysteem komt, vangt dit voorwerp controleattributen voor dat systeem. |
| `personKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de persoon die lid is van de bijbehorende campagne. |
| `_id` | Tekenreeks | Een unieke id voor de record. Dit is een door het systeem gegenereerde waarde die los staat van `campaignMemberID`. |
| `campaignID` | Tekenreeks | Een unieke id voor de bijbehorende campagne. |
| `campaignMemberID` | Tekenreeks | Een unieke id voor de entiteit die lid is van de campagne. |
| `personId` | Tekenreeks | Een unieke id voor de persoon die lid is van de bijbehorende campagne. |

{style=&quot;table-layout:auto&quot;}

Zie de gids op [schemaverhoudingen in Real-time CDP B2B Uitgave](../../tutorials/relationship-b2b.md) leren hoe deze klasse conceptueel met de andere B2B klassen verwant en hoe u deze verhoudingen in Adobe Experience Platform UI kunt vestigen.
