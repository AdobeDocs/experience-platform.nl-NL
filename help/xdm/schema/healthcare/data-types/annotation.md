---
title: Gegevenstype aantekening
description: Leer over het gegevenstype van het gegevensmodel van de Ervaring van de Annotatie (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: f46b5fb6-d64a-4a37-91f6-b470599d9130
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# [!UICONTROL Annotation] gegevenstype

[!UICONTROL Annotation] is een standaard XDM-gegevenstype (Experience Data Model) dat een tekstknooppunt bevat met kenmerk aan de auteur. Dit gegevenstype wordt gecreeerd volgens de specificaties van Versie 5 van HL7 FHIR.

![&#x200B; structuur van het gegevenstype van de Annotatie &#x200B;](../../../images/healthcare/data-types/annotation.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Author Reference] | `authorReference` | [[!UICONTROL Reference]](../data-types/reference.md) | Een verwijzing naar de auteur. |
| [!UICONTROL Author] | `authorString` | String | De persoon die verantwoordelijk is voor de aantekening. |
| [!UICONTROL Text] | `text` | String | De inhoud van de aantekening. |
| [!UICONTROL Time] | `time` | DateTime | Toen de annotatie werd gemaakt. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.schema.json)
