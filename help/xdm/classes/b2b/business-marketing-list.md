---
title: XDM Business Marketing List-klasse
description: Leer over de klasse XDM Business Marketing List in het Model van de Gegevens van de Ervaring (XDM).
exl-id: 510c5608-054d-4bed-91eb-22d84b5dc625
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---

# [!UICONTROL XDM Business Marketing List] -klasse

>[!IMPORTANT]
>
>Deze klasse is bedoeld om door organisaties met toegang tot [&#x200B; Adobe Real-time Customer Data Platform B2B Uitgave &#x200B;](../../../rtcdp/b2b-overview.md) worden gebruikt. U moet toegang tot de Uitgave van Real-Time CDP B2B hebben opdat deze klasse aan [&#x200B; in real time het Profiel van de Klant &#x200B;](../../../profile/home.md) deelneemt.

[!UICONTROL XDM Business Marketing List] is een standaard-XDM-klasse (Experience Data Model) waarmee de minimaal vereiste eigenschappen van een marketinglijst worden vastgelegd. Op de markt brengende lijsten staan u toe om aan potentiële cliënten voorrang te geven die zeer waarschijnlijk uw product zullen kopen.

![&#x200B; De structuur van de XDM Bedrijfs van de Marketing klasse van de Lijst aangezien het in UI &#x200B;](../../images/classes/b2b/business-marketing-list.png) verschijnt

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Als de marketing lijst uit een extern bronsysteem komt, vangt dit voorwerp controleattributen voor dat systeem. |
| `marketingListKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de entiteit van de marketinglijst. |
| `_id` | String | Een unieke id voor de record. Dit is een door het systeem gegenereerde waarde die los staat van de `marketingListID` . |
| `isDeleted` | Boolean | Geeft aan of deze marketinglijstentiteit in het Marketo Engage is verwijderd.<br><br> wanneer het gebruiken van de [&#x200B; Marketo bronschakelaar &#x200B;](../../../sources/connectors/adobe-applications/marketo/marketo.md), worden om het even welke verslagen die in Marketo worden geschrapt automatisch weerspiegeld in Real-Time Profiel van de Klant. In het Data Lake kunnen echter nog steeds gegevens over deze profielen worden bewaard. Door `isDeleted` in te stellen op `true` , kunt u het veld gebruiken om uit te filteren welke records uit uw bronnen zijn verwijderd wanneer u een query uitvoert op het gegevensmeer. |
| `marketingListDescription` | String | Een beschrijving voor de marketinglijst. |
| `marketingListID` | String | Een unieke id voor de marketinglijstentiteit. |
| `marketingListName` | String | De naam van de marketinglijst. |

{style="table-layout:auto"}

Zie de gids op [&#x200B; schemaverhoudingen in de Uitgave van Real-Time CDP B2B &#x200B;](../../tutorials/relationship-b2b.md) leren hoe deze klasse conceptueel op de andere klassen B2B betrekking heeft en hoe u deze verhoudingen in Adobe Experience Platform UI kunt vestigen.
