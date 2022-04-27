---
title: XDM Business Opportunity Person Relatie Klasse
description: Dit document biedt een overzicht van de XDM Business Opportunity Person Relation-klasse in Experience Data Model (XDM).
exl-id: 7be193d2-52eb-4b28-953b-5e0fc21d8f93
source-git-commit: 50e5fe8573d828f88867ed33fe86e974c85de60a
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 1%

---

# [!UICONTROL XDM Business Opportunity Person Relation] class

>[!IMPORTANT]
>
>Deze klasse is bedoeld om te worden gebruikt door organisaties die toegang hebben tot [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Deze klasse kan alleen deelnemen aan CDP B2B Edition in realtime als u toegang hebt tot CDP B2B Edition [Klantprofiel in realtime](../../../profile/home.md).

[!UICONTROL XDM Business Opportunity Person Relation] is een standaard klasse van de Gegevens van de Ervaring Model (XDM) die de minimum vereiste eigenschappen van een persoon vangt die met een bedrijfskans wordt geassocieerd.

![De structuur van de XDM Business Opportunity Person-klasse zoals deze wordt weergegeven in de gebruikersinterface](../../images/classes/b2b/business-opportunity-person-relation.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Als de relatie met de ondernemer uit een extern bronsysteem komt, vangt dit voorwerp controleattributen voor dat systeem. |
| `opportunityKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de opportuniteit in de opportuniterelatie. |
| `opportunityPersonKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde identificatiecode voor de opportuniteits-persoonrelatie-entiteit. |
| `personKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de persoon in de opportuniteits-persoonrelatie. |
| `_id` | Tekenreeks | Een unieke id voor de record. Dit is een door het systeem gegenereerde waarde die los staat van de andere id-velden die door de klasse worden vastgelegd. |
| `isDeleted` | Boolean | Geeft aan of deze entiteit voor de marketinglijst is verwijderd in Marketo Engage.<br><br>Wanneer u de [Marketo-bronaansluiting](../../../sources/connectors/adobe-applications/marketo/marketo.md), worden alle records die in Marketo worden verwijderd, automatisch weergegeven in het realtime profiel van de klant. In het Data Lake kunnen echter nog steeds gegevens over deze profielen worden bewaard. Door in te stellen `isDeleted` tot `true`, kunt u het gebied gebruiken om uit te filteren welke verslagen uit uw bronnen zijn geschrapt wanneer het vragen van het meer van Gegevens. |
| `isPrimary` | Boolean | Geeft aan of de persoon de primaire contactpersoon voor deze kans is. |
| `opportunityID` | Tekenreeks | Een unieke id voor de opportuniteit in de opportuniterelatie. |
| `opportunityPersonID` | Tekenreeks | Een unieke identificatiecode voor de opportuniteits-relatie-entiteit |
| `personID` | Tekenreeks | Een unieke id voor de persoon in de opportuniterelatie. |
| `personRole` | Tekenreeks | De rol voor de persoon in de opportuniteits-persoonverhouding. |

{style=&quot;table-layout:auto&quot;}

Zie de handleiding op [schema-relaties in Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) om te leren hoe deze klasse conceptueel op de andere klassen B2B betrekking heeft en hoe u deze verhoudingen in Adobe Experience Platform UI kunt vestigen.
