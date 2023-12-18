---
title: B2B-brongegevenstype
description: Leer over het B2B-gegevenstype (Source Experience Data Model).
exl-id: 01b7d41c-1ab6-4cbc-b9b3-77b6af69faf3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# [!UICONTROL B2B Source] gegevenstype

[!UICONTROL B2B Source] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat een samengestelde herkenningsteken voor een entiteit B2B (zoals een [account](../classes/b2b/business-account.md), en [kans](../classes/b2b/business-opportunity.md)of een [campagne](../classes/b2b/business-campaign.md)).

Wanneer u alleen op op tekenreeks gebaseerde id&#39;s vertrouwt, kan er sprake zijn van overlappingen tussen id&#39;s op meerdere systemen (een mogelijkheid kan bijvoorbeeld worden gegeven aan een tekenreeks-id op één CRM-systeem, maar die id kan verwijzen naar een totaal andere mogelijkheid). Dit kan leiden tot gegevensconflicten bij het samenvoegen van gegevens in [Klantprofiel in realtime](../../profile/home.md).

De [!UICONTROL B2B Source] Met het gegevenstype kunt u de oorspronkelijke tekenreeks-id van een entiteit gebruiken en deze combineren met bronspecifieke contextafhankelijke informatie om ervoor te zorgen dat deze volledig uniek blijft in het platformsysteem, ongeacht de bron waaruit deze afkomstig is.

![B2B-bronstructuur](../images/data-types/b2b-source.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `sourceID` | String | Een unieke id voor de bronrecord. |
| `sourceInstanceID` | String | De instantie- of organisatie-id van de brongegevens. |
| `sourceKey` | String | Een unieke id die bestaat uit de `sourceId`, `sourceInstanceId`, en `sourceType` samengevoegd in de volgende indeling: `[sourceID]@[sourceInstanceID].[sourceType]`.<br><br>Sommige bronschakelaars zoals Marketo voegen deze waarde automatisch voor bepaalde herkenningstekens samen. Andere moeten handmatig worden samengevoegd met de [Gegevensprep `concat` function](../../data-prep/functions.md#string), bijvoorbeeld: `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | String | De naam van het platform dat de brongegevens levert. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
