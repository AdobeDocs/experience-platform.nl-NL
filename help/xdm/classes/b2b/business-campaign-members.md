---
title: Klasse XDM Business Campaign-leden
description: Dit document biedt een overzicht van de klasse XDM Business Campaign members in Experience Data Model (XDM).
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 2%

---

# [!UICONTROL XDM Business Campaign Members] class

[!UICONTROL XDM Business Campaign Members] is een standaardklasse van de Gegevens van de Ervaring van het Model (XDM) die een contact of een lood verbonden aan een bedrijfscampagne beschrijft.

![](../../images/classes/b2b/business-campaign-members.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de bijbehorende campagne. |
| `campaignMemberKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de entiteit die lid is van de campagne. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Als het campagnerelid uit een extern bronsysteem komt, vangt dit voorwerp controleattributen voor dat systeem. |
| `personKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de persoon die lid is van de bijbehorende campagne. |
| `_id` | Tekenreeks | Een unieke id voor de record. Dit is een door het systeem gegenereerde waarde die los staat van de `campaignMemberID`. |
| `campaignID` | Tekenreeks | Een unieke id voor de bijbehorende campagne. |
| `campaignMemberID` | Tekenreeks | Een unieke id voor de entiteit die lid is van de campagne. |
| `personId` | Tekenreeks | Een unieke id voor de persoon die lid is van de bijbehorende campagne. |

{style=&quot;table-layout:auto&quot;}

Zie de handleiding op [schema-relaties in Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) om te leren hoe deze klasse conceptueel op de andere klassen B2B betrekking heeft en hoe u deze verhoudingen in Adobe Experience Platform UI kunt vestigen.
