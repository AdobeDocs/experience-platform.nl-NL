---
title: Klasse XDM Business Campaign-leden
description: Leer over de klasse van de Leden van de Campagne XDM Business in het Model van de Gegevens van de Ervaring (XDM).
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# [!UICONTROL XDM Business Campaign Members] -klasse

>[!IMPORTANT]
>
>Deze klasse is bedoeld om door organisaties met toegang tot [&#x200B; Adobe Real-time Customer Data Platform B2B Uitgave &#x200B;](../../../rtcdp/b2b-overview.md) worden gebruikt. U moet toegang tot de Uitgave van Real-Time CDP B2B hebben opdat deze klasse aan [&#x200B; in real time het Profiel van de Klant &#x200B;](../../../profile/home.md) deelneemt.

[!UICONTROL XDM Business Campaign Members] is een standaard klasse van het Gegevensmodel van de Ervaring (XDM) die een contact of een lood beschrijft verbonden aan een bedrijfscampagne.

![&#x200B; de structuur van de XDM BedrijfsCampagne Leden klasse aangezien het in UI &#x200B;](../../images/classes/b2b/business-campaign-members.png) verschijnt

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de bijbehorende campagne. |
| `campaignMemberKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de entiteit die lid is van de campagne. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Als het campagnerelid uit een extern bronsysteem komt, vangt dit voorwerp controleattributen voor dat systeem. |
| `personKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de persoon die lid is van de bijbehorende campagne. |
| `_id` | String | Een unieke id voor de record. Dit is een door het systeem gegenereerde waarde die los staat van de `campaignMemberID` . |

{style="table-layout:auto"}

Om te leren hoe deze klasse conceptueel op de andere B2B klassen betrekking heeft en hoe u deze verhoudingen in Adobe Experience Platform UI kunt vestigen, zie de gids op [&#x200B; schemaverhoudingen in Real-Time CDP B2B Uitgave &#x200B;](../../tutorials/relationship-b2b.md)

Zie de veldgroepverwijzing voor [[!UICONTROL XDM Business Campaign Member Details]](../../field-groups/b2b-campaign-members/details.md) voor aanvullende velden die compatibel zijn met deze klasse.
