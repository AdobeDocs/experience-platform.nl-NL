---
title: Klasse XDM Business Campaign-leden
description: Dit document biedt een overzicht van de klasse XDM Business Campaign members in Experience Data Model (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 3%

---

# [!UICONTROL XDM Business Campaign Members] class

>[!NOTE]
>
>Deze klasse is alleen beschikbaar voor organisaties die toegang hebben tot de B2B-editie van Real-time Customer Data Platform.

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
