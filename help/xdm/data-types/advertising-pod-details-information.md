---
title: Gegevenstype advertentiepod Details
description: Meer informatie over het gegevenstype XDM (Advertising Pod Details Information Experience Data Model).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# [!UICONTROL Advertising Pod Details Information] gegevenstype

[!UICONTROL Advertising Pod Details Information] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM). Hiermee definieert u een reeks of groep advertenties die normaal gesproken achtereenvolgens worden afgespeeld tijdens inhoudeinden. Gebruik de [!UICONTROL Advertising Pod Details Information] gegevenstype voor het vastleggen van details, zoals de id van het advertentie-einde, een vriendelijke naam voor het advertentieeinde, de index van advertenties binnen het einde en de verschuiving van het advertentiespoor binnen de tijdlijn van de inhoud in seconden.

![Een diagram van het gegevenstype Informatie over advertentiepod.](../images/data-types/advertising-pod-details-information.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|----------------------------|------------------------|-----------|-------------------------------------------------------|
| [!UICONTROL Ad Break ID] | `ID` | string | De id van het advertentieeinde. |
| [!UICONTROL Pod Friendly Name] | `friendlyName` | string | De eenvoudig te begrijpen naam van het advertentiepalk. |
| [!UICONTROL Ad In Pod Position] | `index` | integer | De index van de advertentie binnen het bovenliggende element en het begin van het einde. |
| [!UICONTROL Pod Offset] | `offset` | integer | **Vereist** De verschuiving van het advertentieeinde binnen de inhoud, in seconden. |

{style="table-layout:auto"}

Voor meer informatie over de veldgroep raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json)
