---
title: XDM Business Account-klasse
description: Meer informatie over de XDM Business Account-klasse in Experience Data Model (XDM).
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# [!UICONTROL XDM Business Account] class

>[!IMPORTANT]
>
>Deze klasse is bedoeld om te worden gebruikt door organisaties met toegang tot [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). U moet toegang hebben tot Real-Time CDP B2B Edition om deze klasse te laten deelnemen aan [Klantprofiel in realtime](../../../profile/home.md).

[!UICONTROL XDM Business Account] is een standaardklasse van het Gegevensmodel van de Ervaring (XDM) die de minimum vereiste eigenschappen van een bedrijfsrekening vangt.

![De structuur van de XDM Business Account-klasse zoals deze wordt weergegeven in de gebruikersinterface](../../images/classes/b2b/business-account.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde identificator voor de rekeningentiteit. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Als de rekening uit een extern bronsysteem komt, vangt dit voorwerp controleattributen voor dat systeem. |
| `_id` | String | Een unieke id voor de record. Dit is een door het systeem gegenereerde waarde die los staat van de `accountKey` id. |
| `isDeleted` | Boolean | Geeft aan of deze accountentiteit in het Marketo Engage is verwijderd.<br><br>Wanneer u de opdracht [Marketo-bronaansluiting](../../../sources/connectors/adobe-applications/marketo/marketo.md), worden alle records die in Marketo worden verwijderd, automatisch weergegeven in Real-Time klantprofiel. In het Data Lake kunnen echter nog steeds gegevens over deze profielen worden bewaard. Door in te stellen `isDeleted` tot `true`, kunt u het gebied gebruiken om uit te filteren welke verslagen uit uw bronnen zijn geschrapt wanneer het vragen van het meer van Gegevens. |

{style="table-layout:auto"}

Zie de handleiding op [schema-relaties in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) om te leren hoe deze klasse conceptueel op de andere klassen B2B betrekking heeft en hoe u deze verhoudingen in Adobe Experience Platform UI kunt vestigen.
