---
title: XDM Business Opportunity-klasse
description: Meer informatie over de XDM Business Opportunity-klasse in Experience Data Model (XDM).
exl-id: d816b0f9-fd37-45da-aa55-247f7f662da0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# [!UICONTROL XDM Business Opportunity] -klasse

>[!IMPORTANT]
>
>Deze klasse is bedoeld om door organisaties met toegang tot [ Adobe Real-time Customer Data Platform B2B Uitgave ](../../../rtcdp/b2b-overview.md) worden gebruikt. U moet toegang tot de Uitgave van Real-Time CDP B2B hebben opdat deze klasse aan [ in real time het Profiel van de Klant ](../../../profile/home.md) deelneemt.

[!UICONTROL XDM Business Opportunity] is een standaard klasse van het Gegevensmodel van de Ervaring (XDM) die de minimaal vereiste eigenschappen van een bedrijfskans vangt.

![ de structuur van de XDM klasse Business Opportunity zoals het in UI ](../../images/classes/b2b/business-opportunity.png) verschijnt

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de account waaraan deze kans is gekoppeld. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Als de kans uit een extern bronsysteem komt, vangt dit voorwerp controleattributen voor dat systeem. |
| `opportunityKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de opportuniteitsentiteit. |
| `_id` | String | Een unieke id voor de record. Dit is een door het systeem gegenereerde waarde die los staat van de `opportunityID` . |
| `accountID` | String | Een unieke id voor het account waaraan deze kans is gekoppeld. |
| `isDeleted` | Boolean | Geeft aan of deze marketinglijstentiteit in het Marketo Engage is verwijderd.<br><br> wanneer het gebruiken van de [ Marketo bronschakelaar ](../../../sources/connectors/adobe-applications/marketo/marketo.md), worden om het even welke verslagen die in Marketo worden geschrapt automatisch weerspiegeld in Real-Time Profiel van de Klant. In het Data Lake kunnen echter nog steeds gegevens over deze profielen worden bewaard. Door `isDeleted` in te stellen op `true` , kunt u het veld gebruiken om uit te filteren welke records uit uw bronnen zijn verwijderd wanneer u een query uitvoert op het gegevensmeer. |
| `opportunityDescription` | String | Een beschrijving van de mogelijkheid. |
| `opportunityID` | String | Een unieke id voor de opportuniteitsentiteit. |
| `opportunityName` | String | De naam van de mogelijkheid. |
| `opportunityStage` | String | De verkoopfase van de mogelijkheid. |
| `opportunityType` | String | Het soort kans. |

{style="table-layout:auto"}

Zie de gids op [ schemaverhoudingen in de Uitgave van Real-Time CDP B2B ](../../tutorials/relationship-b2b.md) leren hoe deze klasse conceptueel op de andere klassen B2B betrekking heeft en hoe u deze verhoudingen in Adobe Experience Platform UI kunt vestigen.
