---
title: Klasse XDM Business Campaign-leden
description: Dit document biedt een overzicht van de klasse XDM Business Campaign members in Experience Data Model (XDM).
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: 0084492ed467c5996a94c5c55a79c9faf8f5046e
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# [!UICONTROL XDM Business Campaign Members] class

>[!IMPORTANT]
>
>Deze klasse is bedoeld om te worden gebruikt door organisaties die toegang hebben tot [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Deze klasse kan alleen deelnemen aan CDP B2B Edition in realtime als u toegang hebt tot CDP B2B Edition [Klantprofiel in realtime](../../../profile/home.md).

[!UICONTROL XDM Business Campaign Members] is een standaardklasse van de Gegevens van de Ervaring van het Model (XDM) die een contact of een lood verbonden aan een bedrijfscampagne beschrijft.

![De structuur van de XDM-klasse Business Campaign-leden zoals deze wordt weergegeven in de gebruikersinterface](../../images/classes/b2b/business-campaign-members.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de bijbehorende campagne. |
| `campaignMemberKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de entiteit die lid is van de campagne. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Als het campagnerelid uit een extern bronsysteem komt, vangt dit voorwerp controleattributen voor dat systeem. |
| `personKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de persoon die lid is van de bijbehorende campagne. |
| `_id` | Tekenreeks | Een unieke id voor de record. Dit is een door het systeem gegenereerde waarde die los staat van de `campaignMemberID`. |

{style=&quot;table-layout:auto&quot;}

Als u wilt leren hoe deze klasse conceptueel betrekking heeft op de andere B2B-klassen en hoe u deze relaties kunt instellen in de gebruikersinterface van Adobe Experience Platform, raadpleegt u de handleiding op [schema-relaties in Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md)

Zie de veldgroepverwijzing voor aanvullende velden die compatibel zijn met deze klasse [[!UICONTROL XDM Business Campaign Member Details]](../../field-groups/b2b-campaign-members/details.md).
