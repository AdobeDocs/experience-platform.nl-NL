---
title: XDM Business Campaign-klasse
description: Dit document biedt een overzicht van de XDM Business Campaign-klasse in het XDM-model (Experience Data Model).
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 3%

---

# [!UICONTROL XDM Business Campaign] class

[!UICONTROL XDM Business Campaign] is een standaardklasse van de Gegevens van de Ervaring van het Model (XDM) die de minimum vereiste eigenschappen van een bedrijfscampagne vangt.

![](../../images/classes/b2b/business-campaign.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de campagneentiteit. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Als de campagne uit een extern bronsysteem komt, vangt dit voorwerp controleattributen voor dat systeem. |
| `_id` | Tekenreeks | Een unieke id voor de record. Dit is een door het systeem gegenereerde waarde die los staat van de `campaignID`. |
| `campaignDescription` | Tekenreeks | Een beschrijving van de campagne. |
| `campaignID` | Tekenreeks | Een unieke id voor de campagneentiteit. |
| `campaignName` | Tekenreeks | De naam van de campagne. |
| `campaignType` | Tekenreeks | Het type campagne of doelpubliek. |

{style=&quot;table-layout:auto&quot;}

Zie de handleiding op [schema-relaties in Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) om te leren hoe deze klasse conceptueel op de andere klassen B2B betrekking heeft en hoe u deze verhoudingen in Adobe Experience Platform UI kunt vestigen.
