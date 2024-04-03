---
title: Advertentiepod Details Rapportering Gegevenstype
description: Meer informatie over het gegevenstype Rapportage Experience Data Model (XDM) van de advertentiepod.
source-git-commit: b6b916c76d1b2babb673d419ab69ae414dd42f20
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# [!UICONTROL Advertising Pod Details Reporting] gegevenstype

[!UICONTROL Advertising Pod Details Reporting] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM). Hiermee definieert u een reeks of groep advertenties die normaal gesproken achtereenvolgens worden afgespeeld tijdens inhoudeinden. Gebruik de [!UICONTROL Advertising Pod Details Reporting] gegevenstype voor het vastleggen van details, zoals de id van het advertentie-einde, een vriendelijke naam voor het advertentieeinde, de index van advertenties binnen het einde en de verschuiving van het advertentiespoor binnen de tijdlijn van de inhoud in seconden.

![Een diagram van het gegevenstype Rapportage van gegevens van de advertentiepod.](../images/data-types/advertising-pod-details-information.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|----------------------------|------------------------|-----------|-------------------------------------------------------|
| [!UICONTROL Ad Break ID] | `ID` | string | De id van het advertentieeinde. |
| [!UICONTROL Pod Friendly Name] | `friendlyName` | string | De eenvoudig te begrijpen naam van het advertentiepalk. |
| [!UICONTROL Ad In Pod Position] | `index` | integer | De index van de advertentie binnen het bovenliggende element en het begin van het einde. |
| [!UICONTROL Pod Offset] | `offset` | integer | **Vereist** De verschuiving van het advertentieeinde binnen de inhoud, in seconden. |

{style="table-layout:auto"}

Voor meer informatie over de veldgroep raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json)
