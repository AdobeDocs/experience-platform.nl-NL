---
title: XDM Business Opportunity-klasse
description: Dit document biedt een overzicht van de XDM Business Opportunity-klasse in Experience Data Model (XDM).
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 4%

---

# [!UICONTROL XDM Business Opportunity] class

>[!NOTE]
>
>Deze klasse is alleen beschikbaar voor organisaties die toegang hebben tot Real-time Customer Data Platform B2B Edition.

[!UICONTROL XDM Business Opportunity] is een standaardklasse van de Gegevens van de Ervaring van het Model (XDM) die de minimum vereiste eigenschappen van een bedrijfskans vangt.

![](../../images/classes/b2b/business-opportunity.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de account waaraan deze kans is gekoppeld. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Als de kans uit een extern bronsysteem komt, vangt dit voorwerp controleattributen voor dat systeem. |
| `opportunityKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de opportuniteitsentiteit. |
| `_id` | Tekenreeks | Een unieke id voor de record. Dit is een door het systeem gegenereerde waarde die los staat van `opportunityID`. |
| `accountID` | Tekenreeks | Een unieke id voor het account waaraan deze kans is gekoppeld. |
| `opportunityDescription` | Tekenreeks | Een beschrijving van de mogelijkheid. |
| `opportunityID` | Tekenreeks | Een unieke id voor de opportuniteitsentiteit. |
| `opportunityName` | Tekenreeks | De naam van de opportuniteit. |
| `opportunityStage` | Tekenreeks | De verkoopfase van de opportuniteit. |
| `opportunityType` | Tekenreeks | Het soort kans. |

Zie de gids op [schemaverhoudingen in Real-time CDP B2B Uitgave](../../tutorials/relationship-b2b.md) leren hoe deze klasse conceptueel met de andere B2B klassen verwant en hoe u deze verhoudingen in Adobe Experience Platform UI kunt vestigen.
