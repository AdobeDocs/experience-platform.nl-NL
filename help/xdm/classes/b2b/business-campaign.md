---
title: XDM Business Campaign-klasse
description: Dit document biedt een overzicht van de XDM Business Campaign-klasse in het XDM-model (Experience Data Model).
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: 0084492ed467c5996a94c5c55a79c9faf8f5046e
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 2%

---

# [!UICONTROL XDM Business Campaign] class

>[!IMPORTANT]
>
>Deze klasse is bedoeld om te worden gebruikt door organisaties die toegang hebben tot [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Deze klasse kan alleen deelnemen aan CDP B2B Edition in realtime als u toegang hebt tot CDP B2B Edition [Klantprofiel in realtime](../../../profile/home.md).

[!UICONTROL XDM Business Campaign] is een standaardklasse van de Gegevens van de Ervaring van het Model (XDM) die de minimum vereiste eigenschappen van een bedrijfscampagne vangt.

![De structuur van de XDM Business Campaign-klasse zoals deze wordt weergegeven in de gebruikersinterface](../../images/classes/b2b/business-campaign.png)

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

Als u wilt leren hoe deze klasse conceptueel betrekking heeft op de andere B2B-klassen en hoe u deze relaties kunt instellen in de gebruikersinterface van Adobe Experience Platform, raadpleegt u de handleiding op [schema-relaties in Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md)

Zie de veldgroepverwijzing voor aanvullende velden die compatibel zijn met deze klasse [[!UICONTROL XDM Business Campaign Details]](../../field-groups/b2b-campaign/details.md).
