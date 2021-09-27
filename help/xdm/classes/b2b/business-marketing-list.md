---
title: XDM Business Marketing List-klasse
description: Dit document biedt een overzicht van de XDM Business Marketing List-klasse in het XDM (Experience Data Model).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 3%

---

# [!UICONTROL XDM Business Marketing List] class

>[!NOTE]
>
>Deze klasse is alleen beschikbaar voor organisaties die toegang hebben tot de B2B-editie van Real-time Customer Data Platform.

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
