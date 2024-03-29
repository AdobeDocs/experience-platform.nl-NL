---
title: Klasse met XDM Business Marketing List-leden
description: Leer over de XDM Business Marketing List Member class in het Model van de Gegevens van de Ervaring (XDM).
exl-id: 069002c2-5583-4c59-84ee-c071e2acaaec
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# [!UICONTROL XDM Business Marketing List Members] class

>[!IMPORTANT]
>
>Deze klasse is bedoeld om te worden gebruikt door organisaties met toegang tot [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). U moet toegang hebben tot Real-Time CDP B2B Edition om deze klasse te laten deelnemen aan [Klantprofiel in realtime](../../../profile/home.md).

[!UICONTROL XDM Business Marketing List Members] is een standaardklasse van de Gegevens van de Ervaring Model (XDM) die leden, personen, of contacten verbonden aan een marketing lijst beschrijft.

![De structuur van de XDM Business Marketing List-lidklasse zoals deze wordt weergegeven in de gebruikersinterface](../../images/classes/b2b/business-marketing-list-members.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Als het lidmaatschap van de marketinglijst afkomstig is van een extern bronsysteem, legt dit object auditkenmerken voor dat systeem vast. |
| `marketingListKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de marketinglijst waarvan de persoon lid is. |
| `marketingListMemberKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de entiteit die lid is van de marketinglijst. |
| `personKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de persoon die lid is van de marketinglijst. |
| `_id` | String | Een unieke id voor de record. Dit is een door het systeem gegenereerde waarde die los staat van de `marketingListMemberID`. |
| `isDeleted` | Boolean | Geeft aan of dit lid van de marketinglijst in het Marketo Engage is verwijderd.<br><br>Wanneer u de opdracht [Marketo-bronaansluiting](../../../sources/connectors/adobe-applications/marketo/marketo.md), worden alle records die in Marketo worden verwijderd, automatisch weergegeven in Real-Time klantprofiel. In het Data Lake kunnen echter nog steeds gegevens over deze profielen worden bewaard. Door in te stellen `isDeleted` tot `true`, kunt u het gebied gebruiken om uit te filteren welke verslagen uit uw bronnen zijn geschrapt wanneer het vragen van het meer van Gegevens. |
| `marketingListID` | String | Een unieke id voor de marketinglijst. |
| `marketingListMemberID` | String | Een unieke id voor de lidmaatschapsentiteit voor marketinglijsten. |
| `personId` | String | Een unieke id voor de persoon. |

{style="table-layout:auto"}

Zie de handleiding op [schema-relaties in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) om te leren hoe deze klasse conceptueel op de andere klassen B2B betrekking heeft en hoe u deze verhoudingen in Adobe Experience Platform UI kunt vestigen.
