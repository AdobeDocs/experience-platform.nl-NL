---
title: XDM Business Opportunity-klasse
description: Dit document biedt een overzicht van de XDM Business Opportunity-klasse in Experience Data Model (XDM).
exl-id: d816b0f9-fd37-45da-aa55-247f7f662da0
source-git-commit: 50e5fe8573d828f88867ed33fe86e974c85de60a
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 2%

---

# [!UICONTROL XDM Business Opportunity] class

>[!IMPORTANT]
>
>Deze klasse is bedoeld om te worden gebruikt door organisaties die toegang hebben tot [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Deze klasse kan alleen deelnemen aan CDP B2B Edition in realtime als u toegang hebt tot CDP B2B Edition [Klantprofiel in realtime](../../../profile/home.md).

[!UICONTROL XDM Business Opportunity] is een standaardklasse van de Gegevens van de Ervaring van het Model (XDM) die de minimum vereiste eigenschappen van een bedrijfskans vangt.

![De structuur van de XDM Business Opportunity-klasse zoals deze wordt weergegeven in de gebruikersinterface](../../images/classes/b2b/business-opportunity.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de account waaraan deze kans is gekoppeld. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Als de kans uit een extern bronsysteem komt, vangt dit voorwerp controleattributen voor dat systeem. |
| `opportunityKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de opportuniteitsentiteit. |
| `_id` | Tekenreeks | Een unieke id voor de record. Dit is een door het systeem gegenereerde waarde die los staat van de `opportunityID`. |
| `accountID` | Tekenreeks | Een unieke id voor het account waaraan deze kans is gekoppeld. |
| `isDeleted` | Boolean | Geeft aan of deze entiteit voor de marketinglijst is verwijderd in Marketo Engage.<br><br>Wanneer u de [Marketo-bronaansluiting](../../../sources/connectors/adobe-applications/marketo/marketo.md), worden alle records die in Marketo worden verwijderd, automatisch weergegeven in het realtime profiel van de klant. In het Data Lake kunnen echter nog steeds gegevens over deze profielen worden bewaard. Door in te stellen `isDeleted` tot `true`, kunt u het gebied gebruiken om uit te filteren welke verslagen uit uw bronnen zijn geschrapt wanneer het vragen van het meer van Gegevens. |
| `opportunityDescription` | Tekenreeks | Een beschrijving van de mogelijkheid. |
| `opportunityID` | Tekenreeks | Een unieke id voor de opportuniteitsentiteit. |
| `opportunityName` | Tekenreeks | De naam van de opportuniteit. |
| `opportunityStage` | Tekenreeks | De verkoopfase van de opportuniteit. |
| `opportunityType` | Tekenreeks | Het soort kans. |

{style=&quot;table-layout:auto&quot;}

Zie de handleiding op [schema-relaties in Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) om te leren hoe deze klasse conceptueel op de andere klassen B2B betrekking heeft en hoe u deze verhoudingen in Adobe Experience Platform UI kunt vestigen.
