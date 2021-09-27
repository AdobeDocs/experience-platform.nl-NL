---
title: Klasse met XDM Business Marketing List-leden
description: Dit document biedt een overzicht van de XDM Business Marketing List-klasse Leden in het XDM-model (Experience Data Model).
source-git-commit: d83ad2870b6099d3c6359dcc7cd000ecad8a238f
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 2%

---

# [!UICONTROL XDM Business Marketing List Members] klasse (bèta)

>[!IMPORTANT]
>
>Deze klasse is beschikbaar als onderdeel van Real-time Customer Data Platform B2B Edition, dat momenteel in bèta wordt weergegeven. De documentatie en functionaliteit kunnen worden gewijzigd.

[!UICONTROL XDM Business Marketing List Members] is een standaardklasse van de Gegevens van de Ervaring Model (XDM) die leden, personen, of contacten verbonden aan een marketing lijst beschrijft.

![](../../images/classes/b2b/business-marketing-list-members.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Als het lidmaatschap van de marketinglijst afkomstig is van een extern bronsysteem, legt dit object auditkenmerken voor dat systeem vast. |
| `marketingListKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de marketinglijst waarvan de persoon lid is. |
| `marketingListMemberKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de entiteit die lid is van de marketinglijst. |
| `personKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de persoon die lid is van de marketinglijst. |
| `_id` | Tekenreeks | Een unieke id voor de record. Dit is een door het systeem gegenereerde waarde die los staat van `marketingListMemberID`. |
| `marketingListID` | Tekenreeks | Een unieke id voor de marketinglijst. |
| `marketingListMemberID` | Tekenreeks | Een unieke id voor de entiteit die lid is van de marketinglijst. |
| `personId` | Tekenreeks | Een unieke id voor de persoon. |

Zie de gids op [schemaverhoudingen in Real-time CDP B2B Uitgave](../../tutorials/relationship-b2b.md) leren hoe deze klasse conceptueel met de andere B2B klassen verwant en hoe u deze verhoudingen in Adobe Experience Platform UI kunt vestigen.
