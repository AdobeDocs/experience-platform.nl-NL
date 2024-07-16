---
title: Advertising Pod Details Reporting Data Type
description: Meer informatie over het gegevenstype Advertising Pod Details Reporting Experience Data Model (XDM).
exl-id: 5164520f-8c48-4eb0-a0b0-66dc10b68356
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# [!UICONTROL Advertising Pod Details Reporting] gegevenstype

[!UICONTROL Advertising Pod Details Reporting] is een standaard XDM-gegevenstype (Experience Data Model). Hiermee definieert u een reeks of groep advertenties die normaal gesproken achtereenvolgens worden afgespeeld tijdens inhoudeinden. Gebruik het gegevenstype [!UICONTROL Advertising Pod Details Reporting] om details vast te leggen, zoals de id van het advertentie-einde, een vriendelijke naam voor het advertentieeinde, de index van advertenties binnen het einde en de verschuiving van het advertentierak binnen de tijdlijn van de inhoud in seconden.

![ een diagram van de Details die van de Pod van Advertising gegevenstype melden.](../images/data-types/advertising-pod-details-information.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|----------------------------|------------------------|-----------|-------------------------------------------------------|
| [!UICONTROL Ad Break ID] | `ID` | string | De id van het advertentieeinde. |
| [!UICONTROL Pod Friendly Name] | `friendlyName` | string | De eenvoudig te begrijpen naam van het advertentiepalk. |
| [!UICONTROL Ad In Pod Position] | `index` | integer | De index van de advertentie binnen het bovenliggende element en het begin van het einde. |
| [!UICONTROL Pod Offset] | `offset` | integer | **Vereiste** de compensatie van de advertentieonderbreking binnen de inhoud, in seconden. |

{style="table-layout:auto"}

Voor meer details op de gebiedsgroep, verwijs naar de [ openbare bewaarplaats XDM ](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json)
