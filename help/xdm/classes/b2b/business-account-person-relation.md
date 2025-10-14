---
title: XDM Business Account Person Relation Class
description: Meer informatie over de XDM Business Account Person Relation-klasse in Experience Data Model (XDM).
exl-id: d51abe9b-d936-4c84-96e2-35a81ca6b67f
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# [!UICONTROL XDM Business Account Person Relation] -klasse

>[!IMPORTANT]
>
>Deze klasse is bedoeld om door organisaties met toegang tot [&#x200B; Adobe Real-time Customer Data Platform B2B Uitgave &#x200B;](../../../rtcdp/b2b-overview.md) worden gebruikt. U moet toegang tot de Uitgave van Real-Time CDP B2B hebben opdat deze klasse aan [&#x200B; in real time het Profiel van de Klant &#x200B;](../../../profile/home.md) deelneemt.

[!UICONTROL XDM Business Account Person Relation] is een standaard klasse van het Gegevensmodel van de Ervaring (XDM) die de minimum vereiste eigenschappen van een persoon vangt die met een bedrijfsrekening wordt geassocieerd.

![&#x200B; de structuur van de XDM klasse van de Verhouding van de Onderneming van de Rekening zoals het in UI &#x200B;](../../images/classes/b2b/business-account-person-relation.png) verschijnt

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde identificatiecode voor de rekening in de relatie tussen de rekeninghouder en persoon. |
| `accountPersonKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde identificator voor de relatie-entiteit van de rekeningpersoon. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Als de account-persoonverhouding uit een extern bronsysteem komt, vangt dit voorwerp controleattributen voor dat systeem. |
| `personKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde identificator voor de persoon in de relatie tussen de rekeninghouder en de persoon. |
| `_id` | String | Een unieke id voor de record. Dit is een door het systeem gegenereerde waarde die los staat van de andere id-velden die door de klasse worden vastgelegd. |
| `accountID` | String | Een unieke identificatiecode voor de rekening in de relatie tussen de account en de persoon. |
| `accountPersonID` | String | Een unieke identificatiecode voor de relatie-entiteit van de rekeningpersoon. |
| `currencyCode` | String | De ISO 4217-valutacode die wordt gebruikt voor de relatie tussen de rekening en de persoon. |
| `isActive` | Boolean | Geeft aan of de relatie tussen de account en de persoon actief is. |
| `isDeleted` | Boolean | Geeft aan of deze relatie tussen account en persoon in het Marketo Engage is verwijderd.<br><br> wanneer het gebruiken van de [&#x200B; Marketo bronschakelaar &#x200B;](../../../sources/connectors/adobe-applications/marketo/marketo.md), worden om het even welke verslagen die in Marketo worden geschrapt automatisch weerspiegeld in Real-Time Profiel van de Klant. In het Data Lake kunnen echter nog steeds gegevens over deze profielen worden bewaard. Door `isDeleted` in te stellen op `true` , kunt u het veld gebruiken om uit te filteren welke records uit uw bronnen zijn verwijderd wanneer u een query uitvoert op het gegevensmeer. |
| `isDirect` | Boolean | Geeft aan of dit een directe relatie is tussen de rekening en de persoon. |
| `isPrimary` | Boolean | Geeft aan of de persoon de primaire contactpersoon voor deze account is. |
| `personID` | String | Een unieke identificatiecode voor de persoon in de relatie tussen de account en de persoon. |
| `personRoles` | Array van tekenreeksen | Vermeldt de rollen voor de persoon in de account-persoonrelatie. |
| `relationEndDate` | DateTime | De datum waarop de relatie tussen de rekening en de persoon eindigde. |
| `relationStartDate` | DateTime | De datum waarop de relatie tussen de rekening en de persoon is begonnen. |
| `relationshipSource` | String | De bron van de relatie tussen de rekeningpersoon. |

{style="table-layout:auto"}

Zie de gids op [&#x200B; schemaverhoudingen in de Uitgave van Real-Time CDP B2B &#x200B;](../../tutorials/relationship-b2b.md) leren hoe deze klasse conceptueel op de andere klassen B2B betrekking heeft en hoe u deze verhoudingen in Adobe Experience Platform UI kunt vestigen.
