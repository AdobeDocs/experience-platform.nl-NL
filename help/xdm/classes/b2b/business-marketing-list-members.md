---
title: Klasse met XDM Business Marketing List-leden
description: Dit document biedt een overzicht van de XDM Business Marketing List-klasse Leden in het XDM-model (Experience Data Model).
exl-id: 069002c2-5583-4c59-84ee-c071e2acaaec
source-git-commit: 8718512a9768158183b9fb6b9e336081e47cd889
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 2%

---

# [!UICONTROL XDM Business Marketing List Members] class

>[!IMPORTANT]
>
>Deze klasse is bedoeld om te worden gebruikt door organisaties die toegang hebben tot [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Deze klasse kan alleen deelnemen aan CDP B2B Edition in realtime als u toegang hebt tot CDP B2B Edition [Klantprofiel in realtime](../../../profile/home.md).

[!UICONTROL XDM Business Marketing List Members] is een standaardklasse van de Gegevens van de Ervaring Model (XDM) die leden, personen, of contacten verbonden aan een marketing lijst beschrijft.

![](../../images/classes/b2b/business-marketing-list-members.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Als het lidmaatschap van de marketinglijst afkomstig is van een extern bronsysteem, legt dit object auditkenmerken voor dat systeem vast. |
| `marketingListKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de marketinglijst waarvan de persoon lid is. |
| `marketingListMemberKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de entiteit die lid is van de marketinglijst. |
| `personKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de persoon die lid is van de marketinglijst. |
| `_id` | Tekenreeks | Een unieke id voor de record. Dit is een door het systeem gegenereerde waarde die los staat van de `marketingListMemberID`. |
| `marketingListID` | Tekenreeks | Een unieke id voor de marketinglijst. |
| `marketingListMemberID` | Tekenreeks | Een unieke id voor de entiteit die lid is van de marketinglijst. |
| `personId` | Tekenreeks | Een unieke id voor de persoon. |

{style=&quot;table-layout:auto&quot;}

Zie de handleiding op [schema-relaties in Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) om te leren hoe deze klasse conceptueel op de andere klassen B2B betrekking heeft en hoe u deze verhoudingen in Adobe Experience Platform UI kunt vestigen.
