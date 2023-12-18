---
title: XDM Business Campaign-klasse
description: Leer over de klasse van de Campagne XDM Bedrijfs in het Model van de Gegevens van de Ervaring (XDM).
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# [!UICONTROL XDM Business Campaign] class

>[!IMPORTANT]
>
>Deze klasse is bedoeld om te worden gebruikt door organisaties met toegang tot [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). U moet toegang hebben tot Real-Time CDP B2B Edition om deze klasse te laten deelnemen aan [Klantprofiel in realtime](../../../profile/home.md).

[!UICONTROL XDM Business Campaign] is een standaardklasse van de Gegevens van de Ervaring van het Model (XDM) die de minimum vereiste eigenschappen van een bedrijfscampagne vangt.

![De structuur van de XDM Business Campaign-klasse zoals deze wordt weergegeven in de gebruikersinterface](../../images/classes/b2b/business-campaign.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de campagneentiteit. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Als de campagne uit een extern bronsysteem komt, vangt dit voorwerp controleattributen voor dat systeem. |
| `_id` | String | Een unieke id voor de record. Dit is een door het systeem gegenereerde waarde die los staat van de `campaignID`. |
| `campaignDescription` | String | Een beschrijving van de campagne. |
| `campaignID` | String | Een unieke id voor de campagneentiteit. |
| `campaignName` | String | De naam van de campagne. |
| `campaignType` | String | Het type campagne of doelpubliek. |

{style="table-layout:auto"}

Als u wilt leren hoe deze klasse conceptueel betrekking heeft op de andere B2B-klassen en hoe u deze relaties kunt instellen in de gebruikersinterface van Adobe Experience Platform, raadpleegt u de handleiding op [schema-relaties in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md)

Zie de veldgroepverwijzing voor aanvullende velden die compatibel zijn met deze klasse [[!UICONTROL XDM Business Campaign Details]](../../field-groups/b2b-campaign/details.md).
