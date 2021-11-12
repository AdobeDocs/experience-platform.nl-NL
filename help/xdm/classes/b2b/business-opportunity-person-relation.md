---
title: XDM Business Opportunity Person Relatie Klasse
description: Dit document biedt een overzicht van de XDM Business Opportunity Person Relation-klasse in Experience Data Model (XDM).
exl-id: 7be193d2-52eb-4b28-953b-5e0fc21d8f93
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 2%

---

# [!UICONTROL XDM Business Opportunity Person Relation] class

[!UICONTROL XDM Business Opportunity Person Relation] is een standaard klasse van de Gegevens van de Ervaring Model (XDM) die de minimum vereiste eigenschappen van een persoon vangt die met een bedrijfskans wordt geassocieerd.

![](../../images/classes/b2b/business-opportunity-person-relation.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Als de relatie met de ondernemer uit een extern bronsysteem komt, vangt dit voorwerp controleattributen voor dat systeem. |
| `opportunityKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de opportuniteit in de opportuniterelatie. |
| `opportunityPersonKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde identificatiecode voor de opportuniteits-persoonrelatie-entiteit. |
| `personKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de persoon in de opportuniteits-persoonrelatie. |
| `_id` | Tekenreeks | Een unieke id voor de record. Dit is een door het systeem gegenereerde waarde die los staat van de andere id-velden die door de klasse worden vastgelegd. |
| `opportunityID` | Tekenreeks | Een unieke id voor de opportuniteit in de opportuniterelatie. |
| `opportunityPersonID` | Tekenreeks | Een unieke identificatiecode voor de opportuniteits-relatie-entiteit |
| `isPrimary` | Boolean | Geeft aan of de persoon de primaire contactpersoon voor deze kans is. |
| `personID` | Tekenreeks | Een unieke id voor de persoon in de opportuniterelatie. |
| `personRole` | Tekenreeks | De rol voor de persoon in de opportuniteits-persoonverhouding. |

{style=&quot;table-layout:auto&quot;}

Zie de handleiding op [schema-relaties in Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) om te leren hoe deze klasse conceptueel op de andere klassen B2B betrekking heeft en hoe u deze verhoudingen in Adobe Experience Platform UI kunt vestigen.
