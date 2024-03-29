---
title: XDM Business Marketing List-klasse
description: Leer over de klasse XDM Business Marketing List in het Model van de Gegevens van de Ervaring (XDM).
exl-id: 510c5608-054d-4bed-91eb-22d84b5dc625
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---

# [!UICONTROL XDM Business Marketing List] class

>[!IMPORTANT]
>
>Deze klasse is bedoeld om te worden gebruikt door organisaties met toegang tot [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). U moet toegang hebben tot Real-Time CDP B2B Edition om deze klasse te laten deelnemen aan [Klantprofiel in realtime](../../../profile/home.md).

[!UICONTROL XDM Business Marketing List] is een standaard-XDM-klasse (Experience Data Model) waarmee de minimaal vereiste eigenschappen van een marketinglijst worden vastgelegd. Op de markt brengende lijsten staan u toe om aan potentiële cliënten voorrang te geven die zeer waarschijnlijk uw product zullen kopen.

![De structuur van de XDM Business Marketing List-klasse zoals deze wordt weergegeven in de gebruikersinterface](../../images/classes/b2b/business-marketing-list.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Als de marketing lijst uit een extern bronsysteem komt, vangt dit voorwerp controleattributen voor dat systeem. |
| `marketingListKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de entiteit van de marketinglijst. |
| `_id` | String | Een unieke id voor de record. Dit is een door het systeem gegenereerde waarde die los staat van de `marketingListID`. |
| `isDeleted` | Boolean | Geeft aan of deze marketinglijstentiteit in het Marketo Engage is verwijderd.<br><br>Wanneer u de opdracht [Marketo-bronaansluiting](../../../sources/connectors/adobe-applications/marketo/marketo.md), worden alle records die in Marketo worden verwijderd, automatisch weergegeven in Real-Time klantprofiel. In het Data Lake kunnen echter nog steeds gegevens over deze profielen worden bewaard. Door in te stellen `isDeleted` tot `true`, kunt u het gebied gebruiken om uit te filteren welke verslagen uit uw bronnen zijn geschrapt wanneer het vragen van het meer van Gegevens. |
| `marketingListDescription` | String | Een beschrijving voor de marketinglijst. |
| `marketingListID` | String | Een unieke id voor de marketinglijstentiteit. |
| `marketingListName` | String | De naam van de marketinglijst. |

{style="table-layout:auto"}

Zie de handleiding op [schema-relaties in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) om te leren hoe deze klasse conceptueel op de andere klassen B2B betrekking heeft en hoe u deze verhoudingen in Adobe Experience Platform UI kunt vestigen.
