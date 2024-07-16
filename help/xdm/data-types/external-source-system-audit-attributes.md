---
title: Gegevenstype externe Source System Audit Attributes
description: Meer informatie over het gegevenstype External Source System Audit Attributes Experience Data Model (XDM).
exl-id: ebdd8707-9675-4232-a5b7-4e4a481d706a
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# [!UICONTROL External Source System Audit Attributes] gegevenstype

[!UICONTROL External Source System Audit Attributes] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat controledetails over een extern bronsysteem vangt.

![](../images/data-types/external-source-system-audit-attributes.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `externalKey` | [[!UICONTROL B2B Source]](./b2b-source.md) | Een samengestelde id voor de bron die voor controle wordt gebruikt. |
| `createdBy` | String | De naam van de gebruiker die deze record heeft gemaakt. |
| `createdDate` | DateTime | De datum waarop deze record is gemaakt. |
| `externalID` | String | Externe unieke id voor de bron. Deze waarde wordt gebruikt om indien nodig te identificeren en te dedupliceren. |
| `lastActivityDate` | DateTime | De laatste activiteitsdatum voor het bronsysteem. |
| `lastReferencedDate` | DateTime | De laatste datum waarnaar wordt verwezen voor het bronsysteem. |
| `lastUpdatedBy` | String | De naam van de persoon die deze record het laatst heeft bijgewerkt. |
| `lastUpdatedDate` | DateTime | De laatste bijgewerkte datum voor het bronsysteem. |
| `lastViewedDate` | DateTime | De laatst bekeken datum voor het bronsysteem. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.schema.json)
