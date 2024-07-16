---
title: XDM Business Opportunity Person Relatie Klasse
description: Leer over de klasse van de Verhouding van de Person van de Onderneming XDM in het Model van de Gegevens van de Ervaring (XDM).
exl-id: 7be193d2-52eb-4b28-953b-5e0fc21d8f93
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# [!UICONTROL XDM Business Opportunity Person Relation] -klasse

>[!IMPORTANT]
>
>Deze klasse is bedoeld om door organisaties met toegang tot [ Adobe Real-time Customer Data Platform B2B Uitgave ](../../../rtcdp/b2b-overview.md) worden gebruikt. U moet toegang tot de Uitgave van Real-Time CDP B2B hebben opdat deze klasse aan [ in real time het Profiel van de Klant ](../../../profile/home.md) deelneemt.

[!UICONTROL XDM Business Opportunity Person Relation] is een standaard klasse van het Gegevensmodel van de Ervaring (XDM) die de minimum vereiste eigenschappen van een persoon vangt die met een bedrijfskans wordt geassocieerd.

![ de structuur van de XDM klasse van de Person van de BedrijfsOpportunity zoals het in UI ](../../images/classes/b2b/business-opportunity-person-relation.png) verschijnt

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Als de relatie met de ondernemer uit een extern bronsysteem komt, vangt dit voorwerp controleattributen voor dat systeem. |
| `opportunityKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de opportuniteit in de opportuniterelatie. |
| `opportunityPersonKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde identificatiecode voor de relatie tussen opportuniteit en persoon. |
| `personKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de persoon in de opportuniteits-persoonrelatie. |
| `_id` | String | Een unieke id voor de record. Dit is een door het systeem gegenereerde waarde die los staat van de andere id-velden die door de klasse worden vastgelegd. |
| `isDeleted` | Boolean | Geeft aan of deze marketinglijstentiteit in het Marketo Engage is verwijderd.<br><br> wanneer het gebruiken van de [ Marketo bronschakelaar ](../../../sources/connectors/adobe-applications/marketo/marketo.md), worden om het even welke verslagen die in Marketo worden geschrapt automatisch weerspiegeld in Real-Time Profiel van de Klant. In het Data Lake kunnen echter nog steeds gegevens over deze profielen worden bewaard. Door `isDeleted` in te stellen op `true` , kunt u het veld gebruiken om uit te filteren welke records uit uw bronnen zijn verwijderd wanneer u een query uitvoert op het gegevensmeer. |
| `isPrimary` | Boolean | Geeft aan of de persoon de primaire contactpersoon voor deze kans is. |
| `opportunityID` | String | Een unieke id voor de opportuniteit in de opportuniterelatie. |
| `opportunityPersonID` | String | Een unieke identificatiecode voor de opportuniteits-relatie-entiteit |
| `personID` | String | Een unieke id voor de persoon in de opportuniterelatie. |
| `personRole` | String | De rol voor de persoon in de opportuniteits-persoonverhouding. |

{style="table-layout:auto"}

Zie de gids op [ schemaverhoudingen in de Uitgave van Real-Time CDP B2B ](../../tutorials/relationship-b2b.md) leren hoe deze klasse conceptueel op de andere klassen B2B betrekking heeft en hoe u deze verhoudingen in Adobe Experience Platform UI kunt vestigen.
