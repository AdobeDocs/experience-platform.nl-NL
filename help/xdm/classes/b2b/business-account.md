---
title: XDM Business Account-klasse
description: Dit document biedt een overzicht van de XDM Business Account-klasse in Experience Data Model (XDM).
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 2%

---

# [!UICONTROL XDM Business Account] class

[!UICONTROL XDM Business Account] is een standaardklasse van het Gegevensmodel van de Ervaring (XDM) die de minimum vereiste eigenschappen van een bedrijfsrekening vangt.

![](../../images/classes/b2b/business-account.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde identificator voor de rekeningentiteit. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Als de rekening uit een extern bronsysteem komt, vangt dit voorwerp controleattributen voor dat systeem. |
| `_id` | Tekenreeks | Een unieke id voor de record. Dit is een door het systeem gegenereerde waarde die los staat van de `accountID`. |
| `accountID` | Tekenreeks | Een unieke identificatiecode voor de rekeningentiteit. |

{style=&quot;table-layout:auto&quot;}

Zie de handleiding op [schema-relaties in Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) om te leren hoe deze klasse conceptueel op de andere klassen B2B betrekking heeft en hoe u deze verhoudingen in Adobe Experience Platform UI kunt vestigen.
