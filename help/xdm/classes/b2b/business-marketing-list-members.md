---
title: Klasse met XDM Business Marketing List-leden
description: Leer over de XDM Business Marketing List Member class in het Model van de Gegevens van de Ervaring (XDM).
exl-id: 069002c2-5583-4c59-84ee-c071e2acaaec
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# [!UICONTROL XDM Business Marketing List Members] -klasse

>[!IMPORTANT]
>
>Deze klasse is bedoeld om door organisaties met toegang tot [ Adobe Real-time Customer Data Platform B2B Uitgave ](../../../rtcdp/b2b-overview.md) worden gebruikt. U moet toegang tot de Uitgave van Real-Time CDP B2B hebben opdat deze klasse aan [ in real time het Profiel van de Klant ](../../../profile/home.md) deelneemt.

[!UICONTROL XDM Business Marketing List Members] is een standaard-XDM-klasse (Experience Data Model) waarmee leden, personen of contactpersonen worden beschreven die aan een marketinglijst zijn gekoppeld.

![ De structuur van de XDM Bedrijfs van de Marketing Lijst Leden klasse zoals het in UI ](../../images/classes/b2b/business-marketing-list-members.png) verschijnt

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Als het lidmaatschap van de marketinglijst afkomstig is van een extern bronsysteem, legt dit object auditkenmerken voor dat systeem vast. |
| `marketingListKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de marketinglijst waarvan de persoon lid is. |
| `marketingListMemberKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de entiteit die lid is van de marketinglijst. |
| `personKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de persoon die lid is van de marketinglijst. |
| `_id` | String | Een unieke id voor de record. Dit is een door het systeem gegenereerde waarde die los staat van de `marketingListMemberID` . |
| `isDeleted` | Boolean | Geeft aan of dit lid van de marketinglijst in het Marketo Engage is verwijderd.<br><br> wanneer het gebruiken van de [ Marketo bronschakelaar ](../../../sources/connectors/adobe-applications/marketo/marketo.md), worden om het even welke verslagen die in Marketo worden geschrapt automatisch weerspiegeld in Real-Time Profiel van de Klant. In het Data Lake kunnen echter nog steeds gegevens over deze profielen worden bewaard. Door `isDeleted` in te stellen op `true` , kunt u het veld gebruiken om uit te filteren welke records uit uw bronnen zijn verwijderd wanneer u een query uitvoert op het gegevensmeer. |
| `marketingListID` | String | Een unieke id voor de marketinglijst. |
| `marketingListMemberID` | String | Een unieke id voor de lidmaatschapsentiteit voor marketinglijsten. |
| `personId` | String | Een unieke id voor de persoon. |

{style="table-layout:auto"}

Zie de gids op [ schemaverhoudingen in de Uitgave van Real-Time CDP B2B ](../../tutorials/relationship-b2b.md) leren hoe deze klasse conceptueel op de andere klassen B2B betrekking heeft en hoe u deze verhoudingen in Adobe Experience Platform UI kunt vestigen.
