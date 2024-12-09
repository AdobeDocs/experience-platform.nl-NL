---
title: Uitgebreid gegevenstype contactgegevens
description: Leer over het Uitgebreide gegevenstype van de Gegevens van de Ervaring van het Contact Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# [!UICONTROL Extended Contact Detail] gegevenstype

[!UICONTROL Extended Contact Detail] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat de informatie van een uitgebreid contact beschrijft. Dit gegevenstype wordt gecreeerd volgens de specificaties van Versie 5 van HL7 FHIR.

![ Uitgebreide het gegevenstype van het Detail van het Contact structuur ](../../images/data-types/healthcare/extended-contact-detail.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Address] | `address` | [[!UICONTROL Address]](../healthcare/address.md) | Het adres van de contactpersoon. |
| [!UICONTROL Name] | `name` | Array van [[!UICONTROL Human Name]](../healthcare/human-name.md) | De naam/namen van de persoon/personen aan wie een contactpersoon moet worden toegewezen. |
| [!UICONTROL Organization] | `organization` | [[!UICONTROL Reference]](../healthcare/reference.md) | De organisatie die de contactdetails behandelt/controleert. |
| [!UICONTROL Period] | `period` | [[!UICONTROL Period]](../healthcare/period.md) | De periode dat het contact voor gebruik is of geldig was. |
| [!UICONTROL Purpose] | `purpose` | [[!UICONTROL Codeable Concept]](../healthcare/codeable-concept.md) | Het type contact. |
| [!UICONTROL Telecom] | `telecom` | Array van [[!UICONTROL Contact Point]](../healthcare/contact-point.md) | De contactgegevens. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/extendedcontactdetail.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/extendedcontactdetail.schema.json)
