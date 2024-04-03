---
title: Gegevenstype van verzameling advertentiepod Details
description: Leer meer over het gegevenstype van het XDM-gegevensmodel (Experience Data Model) voor verzamelingen in advertentiepod.
source-git-commit: a604dc8b541784ace8aedef42030e5bd8b646c28
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 2%

---

# [!UICONTROL Advertising Pod Details] Gegevenstype verzameling

[!UICONTROL Advertising Pod Details] De inzameling is een standaardgegevenstype van de Gegevens van de Ervaring Model (XDM). Hiermee definieert u een reeks of groep advertenties die normaal gesproken achtereenvolgens worden afgespeeld tijdens inhoudeinden. Gebruik de [!UICONTROL Advertising Pod Details] Het gegevenstype van een verzameling voor het vastleggen van details, zoals de id van het advertentie-einde, een vriendelijke naam voor het advertentiespoor, de index van advertenties binnen het einde en de verschuiving van het advertentiespoor binnen de tijdlijn van de inhoud in seconden.

![Een diagram van het gegevenstype Informatie over verzameling van gegevens over advertentiepod.](../images/data-types/advertising-pod-details-collection.png)

| Weergavenaam | Eigenschap | Gegevenstype | Vereist | Beschrijving |
|-----------------------------------------|-----------------|-----------|--------------------------------------------------------------------|
| [!UICONTROL Ad In Pod Position] | `index` | integer | Ja | De index van de advertentie binnen het bovenliggende element en het begin van het einde. |
| [!UICONTROL Pod Friendly Name] | `friendlyName` | string | Nee | De eenvoudig te begrijpen naam van het advertentiepalk. |
| [!UICONTROL Pod Offset] | `offset` | integer | Ja | De verschuiving van het advertentieeinde binnen de inhoud, in seconden. |
