---
title: XDM Business Marketing List-klasse
description: Dit document biedt een overzicht van de XDM Business Marketing List-klasse in het XDM (Experience Data Model).
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 2%

---

# [!UICONTROL XDM Business Marketing List] class

>[!NOTE]
>
>Deze klasse is alleen beschikbaar voor organisaties die toegang hebben tot Real-time Customer Data Platform B2B Edition.

[!UICONTROL XDM Business Marketing List] is een standaard-XDM-klasse (Experience Data Model) waarmee de minimaal vereiste eigenschappen van een marketinglijst worden vastgelegd. Op de markt brengende lijsten staan u toe om aan potentiële cliënten voorrang te geven die zeer waarschijnlijk uw product zullen kopen.

![](../../images/classes/b2b/business-marketing-list.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Als de marketing lijst uit een extern bronsysteem komt, vangt dit voorwerp controleattributen voor dat systeem. |
| `marketingListKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de entiteit van de marketinglijst. |
| `_id` | Tekenreeks | Een unieke id voor de record. Dit is een door het systeem gegenereerde waarde die los staat van `marketingListID`. |
| `marketingListDescription` | Tekenreeks | Een beschrijving voor de marketinglijst. |
| `marketingListID` | Tekenreeks | Een unieke id voor de marketinglijstentiteit. |
| `marketingListName` | Tekenreeks | De naam van de marketinglijst. |

Zie de gids op [schemaverhoudingen in Real-time CDP B2B Uitgave](../../tutorials/relationship-b2b.md) leren hoe deze klasse conceptueel met de andere B2B klassen verwant en hoe u deze verhoudingen in Adobe Experience Platform UI kunt vestigen.
