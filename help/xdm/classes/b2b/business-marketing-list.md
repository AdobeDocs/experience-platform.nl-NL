---
title: XDM Business Marketing List-klasse
description: Dit document biedt een overzicht van de XDM Business Marketing List-klasse in het XDM (Experience Data Model).
exl-id: 510c5608-054d-4bed-91eb-22d84b5dc625
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 2%

---

# [!UICONTROL XDM Business Marketing List] class

[!UICONTROL XDM Business Marketing List] is een standaard-XDM-klasse (Experience Data Model) waarmee de minimaal vereiste eigenschappen van een marketinglijst worden vastgelegd. Op de markt brengende lijsten staan u toe om aan potentiële cliënten voorrang te geven die zeer waarschijnlijk uw product zullen kopen.

![](../../images/classes/b2b/business-marketing-list.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Als de marketing lijst uit een extern bronsysteem komt, vangt dit voorwerp controleattributen voor dat systeem. |
| `marketingListKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de entiteit van de marketinglijst. |
| `_id` | Tekenreeks | Een unieke id voor de record. Dit is een door het systeem gegenereerde waarde die los staat van de `marketingListID`. |
| `marketingListDescription` | Tekenreeks | Een beschrijving voor de marketinglijst. |
| `marketingListID` | Tekenreeks | Een unieke id voor de marketinglijstentiteit. |
| `marketingListName` | Tekenreeks | De naam van de marketinglijst. |

{style=&quot;table-layout:auto&quot;}

Zie de handleiding op [schema-relaties in Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) om te leren hoe deze klasse conceptueel op de andere klassen B2B betrekking heeft en hoe u deze verhoudingen in Adobe Experience Platform UI kunt vestigen.
