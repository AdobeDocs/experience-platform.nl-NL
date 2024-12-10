---
title: Uitgebreid gegevenstype contactgegevens
description: Leer over het Uitgebreide gegevenstype van de Gegevens van de Ervaring van het Contact Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 4ac9b3d7-acc8-4a82-b34f-ec63a8bf12e0
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# [!UICONTROL Extended Contact Detail] gegevenstype

[!UICONTROL Extended Contact Detail] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat de informatie van een uitgebreid contact beschrijft. Dit gegevenstype wordt gecreeerd volgens de specificaties van Versie 5 van HL7 FHIR.

![ Uitgebreide het gegevenstype van het Detail van het Contact structuur ](../../../images/healthcare/data-types/extended-contact-detail.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Address] | `address` | [[!UICONTROL Address]](../data-types/address.md) | Het adres van de contactpersoon. |
| [!UICONTROL Name] | `name` | Array van [[!UICONTROL Human Name]](../data-types/human-name.md) | De naam/namen van de persoon/personen aan wie een contactpersoon moet worden toegewezen. |
| [!UICONTROL Organization] | `organization` | [[!UICONTROL Reference]](../data-types/reference.md) | De organisatie die de contactdetails behandelt/controleert. |
| [!UICONTROL Period] | `period` | [[!UICONTROL Period]](../data-types/period.md) | De periode dat het contact voor gebruik is of geldig was. |
| [!UICONTROL Purpose] | `purpose` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Het type contact. |
| [!UICONTROL Telecom] | `telecom` | Array van [[!UICONTROL Contact Point]](../data-types/contact-point.md) | De contactgegevens. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/extendedcontactdetail.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/extendedcontactdetail.schema.json)
