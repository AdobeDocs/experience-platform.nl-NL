---
title: XDM Business Campaign-klasse
description: Leer over de klasse van de Campagne XDM Bedrijfs in het Model van de Gegevens van de Ervaring (XDM).
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# [!UICONTROL XDM Business Campaign] -klasse

>[!IMPORTANT]
>
>Deze klasse is bedoeld om door organisaties met toegang tot [ Adobe Real-time Customer Data Platform B2B Uitgave ](../../../rtcdp/b2b-overview.md) worden gebruikt. U moet toegang tot de Uitgave van Real-Time CDP B2B hebben opdat deze klasse aan [ in real time het Profiel van de Klant ](../../../profile/home.md) deelneemt.

[!UICONTROL XDM Business Campaign] is een standaard klasse van het Gegevensmodel van de Ervaring (XDM) die de minimum vereiste eigenschappen van een bedrijfscampagne vangt.

![ de structuur van de XDM BedrijfsCampagne klasse aangezien het in UI ](../../images/classes/b2b/business-campaign.png) verschijnt

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de campagneentiteit. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Als de campagne uit een extern bronsysteem komt, vangt dit voorwerp controleattributen voor dat systeem. |
| `_id` | String | Een unieke id voor de record. Dit is een door het systeem gegenereerde waarde die los staat van de `campaignID` . |
| `campaignDescription` | String | Een beschrijving van de campagne. |
| `campaignID` | String | Een unieke id voor de campagneentiteit. |
| `campaignName` | String | De naam van de campagne. |
| `campaignType` | String | Het type campagne of doelpubliek. |

{style="table-layout:auto"}

Om te leren hoe deze klasse conceptueel op de andere B2B klassen betrekking heeft en hoe u deze verhoudingen in Adobe Experience Platform UI kunt vestigen, zie de gids op [ schemaverhoudingen in Real-Time CDP B2B Uitgave ](../../tutorials/relationship-b2b.md)

Zie de veldgroepverwijzing voor [[!UICONTROL XDM Business Campaign Details]](../../field-groups/b2b-campaign/details.md) voor aanvullende velden die compatibel zijn met deze klasse.
