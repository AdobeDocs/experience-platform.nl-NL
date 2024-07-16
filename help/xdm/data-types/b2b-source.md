---
title: B2B Source-gegevenstype
description: Leer meer over het B2B Source Experience Data Model (XDM) gegevenstype.
exl-id: 01b7d41c-1ab6-4cbc-b9b3-77b6af69faf3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# [!UICONTROL B2B Source] gegevenstype

[!UICONTROL B2B Source] is een standaardgegevenstype van de Gegevens van de Ervaring (XDM) dat een samengesteld herkenningsteken voor een entiteit B2B (zoals een [ rekening ](../classes/b2b/business-account.md), een [ kans ](../classes/b2b/business-opportunity.md), of a [ campagne ](../classes/b2b/business-campaign.md)) vertegenwoordigt.

Wanneer u alleen op op tekenreeks gebaseerde id&#39;s vertrouwt, kan er sprake zijn van overlappingen tussen id&#39;s op meerdere systemen (een mogelijkheid kan bijvoorbeeld worden gegeven aan een tekenreeks-id op één CRM-systeem, maar die id kan verwijzen naar een totaal andere mogelijkheid). Dit kan in gegevensconflicten resulteren wanneer het samenvoegen van gegevens in [ Real-Time Profiel van de Klant ](../../profile/home.md).

Met het gegevenstype [!UICONTROL B2B Source] kunt u de oorspronkelijke tekenreeks-id van een entiteit gebruiken en deze combineren met bronspecifieke contextuele informatie om ervoor te zorgen dat deze volledig uniek blijft in het platformsysteem, ongeacht de bron waaruit deze afkomstig is.

![ B2B de Structuur van Source ](../images/data-types/b2b-source.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `sourceID` | String | Een unieke id voor de bronrecord. |
| `sourceInstanceID` | String | De instantie- of organisatie-id van de brongegevens. |
| `sourceKey` | String | Een unieke id die bestaat uit de `sourceId` , `sourceInstanceId` en `sourceType` en die in de volgende indeling samen wordt aaneengeschakeld: `[sourceID]@[sourceInstanceID].[sourceType]` .<br><br> sommige bronschakelaars zoals Marketo voegen deze waarde automatisch voor bepaalde herkenningstekens samen. Andere moeten manueel worden samengevoegd gebruikend de [ functie van de Prep van Gegevens `concat` ](../../data-prep/functions.md#string), bijvoorbeeld: `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | String | De naam van het platform dat de brongegevens levert. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
