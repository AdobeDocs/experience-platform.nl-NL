---
title: XDM Business Account-klasse
description: Meer informatie over de XDM Business Account-klasse in Experience Data Model (XDM).
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# [!UICONTROL XDM Business Account] -klasse

>[!IMPORTANT]
>
>Deze klasse is bedoeld om door organisaties met toegang tot [&#x200B; Adobe Real-time Customer Data Platform B2B Uitgave &#x200B;](../../../rtcdp/b2b-overview.md) worden gebruikt. U moet toegang tot de Uitgave van Real-Time CDP B2B hebben opdat deze klasse aan [&#x200B; in real time het Profiel van de Klant &#x200B;](../../../profile/home.md) deelneemt.

[!UICONTROL XDM Business Account] is een standaard XDM-klasse (Experience Data Model) waarmee de minimaal vereiste eigenschappen van een zakelijke account worden vastgelegd.

![&#x200B; de structuur van de XDM klasse Bedrijfs van de Rekening aangezien het in UI &#x200B;](../../images/classes/b2b/business-account.png) verschijnt

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde identificator voor de rekeningentiteit. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Als de rekening uit een extern bronsysteem komt, vangt dit voorwerp controleattributen voor dat systeem. |
| `_id` | String | Een unieke id voor de record. Dit is een door het systeem gegenereerde waarde die los staat van de id `accountKey` . |
| `isDeleted` | Boolean | Geeft aan of deze accountentiteit in het Marketo Engage is verwijderd.<br><br> wanneer het gebruiken van de [&#x200B; Marketo bronschakelaar &#x200B;](../../../sources/connectors/adobe-applications/marketo/marketo.md), worden om het even welke verslagen die in Marketo worden geschrapt automatisch weerspiegeld in Real-Time Profiel van de Klant. In het Data Lake kunnen echter nog steeds gegevens over deze profielen worden bewaard. Door `isDeleted` in te stellen op `true` , kunt u het veld gebruiken om uit te filteren welke records uit uw bronnen zijn verwijderd wanneer u een query uitvoert op het gegevensmeer. |

{style="table-layout:auto"}

Zie de gids op [&#x200B; schemaverhoudingen in de Uitgave van Real-Time CDP B2B &#x200B;](../../tutorials/relationship-b2b.md) leren hoe deze klasse conceptueel op de andere klassen B2B betrekking heeft en hoe u deze verhoudingen in Adobe Experience Platform UI kunt vestigen.
