---
title: B2B-brongegevenstype
description: Dit document biedt een overzicht van het gegevenstype B2B Source Experience Data Model (XDM).
exl-id: 01b7d41c-1ab6-4cbc-b9b3-77b6af69faf3
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 1%

---

# [!UICONTROL B2B Source] gegevenstype (bèta)

>[!IMPORTANT]
>
>Dit gegevenstype is beschikbaar als onderdeel van Real-time Customer Data Platform B2B Edition, dat momenteel in bèta wordt weergegeven. De documentatie en functionaliteit kunnen worden gewijzigd.

[!UICONTROL B2B Source] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat een samengestelde herkenningsteken voor een entiteit B2B (zoals een  [rekening](../classes/b2b/business-account.md), een  [kans](../classes/b2b/business-opportunity.md), of een  [campagne](../classes/b2b/business-campaign.md)) vertegenwoordigt.

Wanneer u alleen op op tekenreeks gebaseerde id&#39;s vertrouwt, kan er sprake zijn van overlappingen tussen id&#39;s op meerdere systemen (een mogelijkheid kan bijvoorbeeld worden gegeven aan een tekenreeks-id op één CRM-systeem, maar die id kan verwijzen naar een totaal andere mogelijkheid). Dit kan leiden tot gegevensconflicten bij het samenvoegen van gegevens in [Real-time klantprofiel](../../profile/home.md).

Met het gegevenstype [!UICONTROL B2B Source] kunt u de oorspronkelijke tekenreeks-id van een entiteit gebruiken en deze combineren met bronspecifieke contextuele informatie om ervoor te zorgen dat deze volledig uniek blijft in het Platform-systeem, ongeacht de bron waaruit de id afkomstig is.

![B2B-bronstructuur](../images/data-types/b2b-source.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `sourceID` | Tekenreeks | Een unieke id voor de bronrecord. |
| `sourceInstanceID` | Tekenreeks | De instantie- of organisatie-id van de brongegevens. |
| `sourceKey` | Tekenreeks | Een unieke id die bestaat uit de `sourceId`, `sourceInstanceId` en `sourceType`, en die in de volgende notatie samen wordt aaneengeschakeld: `[sourceID]@$[sourceInstanceID].[sourceType]`.<br><br>Sommige bronschakelaars zoals Marketo voegen deze waarde automatisch voor bepaalde herkenningstekens samen. Andere moeten handmatig worden samengevoegd met de functie [Data Prep `concat`](../../data-prep/functions.md#string), bijvoorbeeld: `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | Tekenreeks | De naam van het platform dat de brongegevens levert. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
