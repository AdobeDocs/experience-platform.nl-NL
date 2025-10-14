---
title: B2B Source-gegevenstype
description: Leer meer over het B2B Source Experience Data Model (XDM) gegevenstype.
exl-id: 01b7d41c-1ab6-4cbc-b9b3-77b6af69faf3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# [!UICONTROL B2B Source] gegevenstype

[!UICONTROL B2B Source] is een standaardgegevenstype van de Gegevens van de Ervaring (XDM) dat een samengesteld herkenningsteken voor een entiteit B2B (zoals een [&#x200B; rekening &#x200B;](../classes/b2b/business-account.md), een [&#x200B; kans &#x200B;](../classes/b2b/business-opportunity.md), of a [&#x200B; campagne &#x200B;](../classes/b2b/business-campaign.md)) vertegenwoordigt.

Wanneer u alleen op op tekenreeks gebaseerde id&#39;s vertrouwt, kan er sprake zijn van overlappingen tussen id&#39;s op meerdere systemen (een mogelijkheid kan bijvoorbeeld worden gegeven aan een tekenreeks-id op één CRM-systeem, maar die id kan verwijzen naar een totaal andere mogelijkheid). Dit kan in gegevensconflicten resulteren wanneer het samenvoegen van gegevens in [&#x200B; Real-Time Profiel van de Klant &#x200B;](../../profile/home.md).

Met het gegevenstype [!UICONTROL B2B Source] kunt u de oorspronkelijke tekenreeks-id van een entiteit gebruiken en deze combineren met bronspecifieke contextafhankelijke informatie om ervoor te zorgen dat deze volledig uniek blijft in het Experience Platform-systeem, ongeacht de bron waaruit deze afkomstig is.

![&#x200B; B2B de Structuur van Source &#x200B;](../images/data-types/b2b-source.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `sourceID` | String | Een unieke id voor de bronrecord. |
| `sourceInstanceID` | String | De instantie- of organisatie-id van de brongegevens. |
| `sourceKey` | String | Een unieke id die bestaat uit de `sourceId` , `sourceInstanceId` en `sourceType` en die in de volgende indeling samen wordt aaneengeschakeld: `[sourceID]@[sourceInstanceID].[sourceType]` .<br><br> sommige bronschakelaars zoals Marketo voegen deze waarde automatisch voor bepaalde herkenningstekens samen. Andere moeten manueel worden samengevoegd gebruikend de [&#x200B; functie van de Prep van Gegevens `concat` &#x200B;](../../data-prep/functions.md#string), bijvoorbeeld: `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | String | De naam van het platform dat de brongegevens levert. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
