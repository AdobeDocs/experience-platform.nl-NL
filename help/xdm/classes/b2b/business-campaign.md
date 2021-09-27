---
title: XDM Business Campaign-klasse
description: Dit document biedt een overzicht van de XDM Business Campaign-klasse in het XDM-model (Experience Data Model).
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 3%

---

# [!UICONTROL XDM Business Campaign] class

>[!NOTE]
>
>Deze klasse is alleen beschikbaar voor organisaties die toegang hebben tot Real-time Customer Data Platform B2B Edition.

[!UICONTROL XDM Business Campaign] is een standaardklasse van de Gegevens van de Ervaring van het Model (XDM) die de minimum vereiste eigenschappen van een bedrijfscampagne vangt.

![](../../images/classes/b2b/business-campaign.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de campagneentiteit. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Als de campagne uit een extern bronsysteem komt, vangt dit voorwerp controleattributen voor dat systeem. |
| `_id` | Tekenreeks | Een unieke id voor de record. Dit is een door het systeem gegenereerde waarde die los staat van `campaignID`. |
| `campaignDescription` | Tekenreeks | Een beschrijving van de campagne. |
| `campaignID` | Tekenreeks | Een unieke id voor de campagneentiteit. |
| `campaignName` | Tekenreeks | De naam van de campagne. |
| `campaignType` | Tekenreeks | Het type campagne of doelpubliek. |

Zie de gids op [schemaverhoudingen in Real-time CDP B2B Uitgave](../../tutorials/relationship-b2b.md) leren hoe deze klasse conceptueel met de andere B2B klassen verwant en hoe u deze verhoudingen in Adobe Experience Platform UI kunt vestigen.
