---
title: Gegevenstype verzameling Advertising Pod Details
description: Meer informatie over het gegevenstype Advertising Pod Details Collection Experience Data Model (XDM).
exl-id: 401c393f-aeda-4ecd-89f4-458833190ced
source-git-commit: 9350cfc299c20bd63a2a559c177b3af02739e5b9
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# [!UICONTROL Advertising Pod Details] Gegevenstype verzameling

[!UICONTROL Advertising Pod Details] Verzameling is een standaard XDM-gegevenstype (Experience Data Model). Hiermee definieert u een reeks of groep advertenties die normaal gesproken achtereenvolgens worden afgespeeld tijdens inhoudeinden. Gebruik het gegevenstype [!UICONTROL Advertising Pod Details] Verzameling om details vast te leggen, zoals de id van het advertentie-einde, een vriendelijke naam voor het advertentieeinde, de index van advertenties binnen het einde en de verschuiving van het advertentierak binnen de tijdlijn van de inhoud in seconden.

![&#x200B; een diagram van het de gegevenstype van de Inzameling van de Informatie van de Peul van Advertising.](../images/data-types/advertising-pod-details-collection.png)

| Weergavenaam | Eigenschap | Gegevenstype | Vereist | Beschrijving |
|-----------------------------------------|-----------------|-----------|----------|---------------------------------------------------------|
| [!UICONTROL Ad In Pod Position] | `index` | integer | Ja | De index van de advertentie binnen het bovenliggende element en het begin van het einde. |
| [!UICONTROL Pod Friendly Name] | `friendlyName` | string | Nee | De eenvoudig te begrijpen naam van het advertentiepalk. |
| [!UICONTROL Pod Offset] | `offset` | integer | Ja | De verschuiving van het advertentieeinde binnen de inhoud, in seconden. |

{style="table-layout:auto"}
