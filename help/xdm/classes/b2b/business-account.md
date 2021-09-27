---
title: XDM Business Account-klasse
description: Dit document biedt een overzicht van de XDM Business Account-klasse in Experience Data Model (XDM).
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 2%

---

# [!UICONTROL XDM Business Account] class

>[!NOTE]
>
>Deze klasse is alleen beschikbaar voor organisaties die toegang hebben tot Real-time Customer Data Platform B2B Edition.

[!UICONTROL XDM Business Account] is een standaardklasse van het Gegevensmodel van de Ervaring (XDM) die de minimum vereiste eigenschappen van een bedrijfsrekening vangt.

![](../../images/classes/b2b/business-account.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde identificator voor de rekeningentiteit. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Als de rekening uit een extern bronsysteem komt, vangt dit voorwerp controleattributen voor dat systeem. |
| `_id` | Tekenreeks | Een unieke id voor de record. Dit is een door het systeem gegenereerde waarde die los staat van `accountID`. |
| `accountID` | Tekenreeks | Een unieke identificatiecode voor de rekeningentiteit. |

Zie de gids op [schemaverhoudingen in Real-time CDP B2B Uitgave](../../tutorials/relationship-b2b.md) leren hoe deze klasse conceptueel met de andere B2B klassen verwant en hoe u deze verhoudingen in Adobe Experience Platform UI kunt vestigen.
