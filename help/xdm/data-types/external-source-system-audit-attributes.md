---
title: Kenmerken voor externe bronsysteemcontrole Gegevenstype
description: Dit document biedt een overzicht van het gegevenstype XDM (External Source System Audit Attributes Experience Data Model).
exl-id: ebdd8707-9675-4232-a5b7-4e4a481d706a
source-git-commit: a7e6ebfe09566e6e027b13efc95dda97ff8f0315
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 2%

---

# [!UICONTROL External Source System Audit Attributes] gegevenstype

[!UICONTROL External Source System Audit Attributes] is een standaardgegevenstype van de Gegevens van de Ervaring Model (XDM) dat controledetails over een extern bronsysteem vangt.

![](../images/data-types/external-source-system-audit-attributes.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `externalKey` | [[!UICONTROL B2B Source]](./b2b-source.md) | Een samengestelde id voor de bron die voor controle wordt gebruikt. |
| `createdBy` | Tekenreeks | De naam van de gebruiker die deze record heeft gemaakt. |
| `createdDate` | DateTime | De datum waarop deze record is gemaakt. |
| `externalID` | Tekenreeks | Externe unieke id voor de bron. Deze waarde wordt gebruikt om indien nodig te identificeren en te dedupliceren. |
| `lastActivityDate` | DateTime | De laatste activiteitsdatum voor het bronsysteem. |
| `lastReferencedDate` | DateTime | De laatste datum waarnaar wordt verwezen voor het bronsysteem. |
| `lastUpdatedBy` | Tekenreeks | De naam van de persoon die deze record het laatst heeft bijgewerkt. |
| `lastUpdatedDate` | DateTime | De laatste bijgewerkte datum voor het bronsysteem. |
| `lastViewedDate` | DateTime | De laatst bekeken datum voor het bronsysteem. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.schema.json)
