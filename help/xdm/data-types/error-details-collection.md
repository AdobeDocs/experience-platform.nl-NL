---
title: Foutdetails Gegevenstype verzameling
description: Meer informatie over het gegevenstype Error Details Collection Data Model (XDM).
exl-id: 54b03147-9bca-46af-86c8-90e42b4de26b
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# [!UICONTROL Error Details] Gegevenstype verzameling

[!UICONTROL Error Details] Verzameling is een standaard XDM-gegevenstype (Experience Data Model) waarmee de details van fouten worden beschreven. Gebruik het gegevenstype [!UICONTROL Error Details] Verzameling om details voor de bron en identificatie van de fout vast te leggen. De fout-id identificeert de fout en de bron van de fout geeft aan of deze afkomstig is van de speler of van een externe bron.

![ A diagram van het gegevenstype van de Informatie van de Details van de Fout.](../images/data-types/error-details-collection.png)

| Weergavenaam | Eigenschap | Gegevenstype | Vereist | Beschrijving |
|----------------------------|--------------|-----------|----------|-----------------------------------------------|
| [!UICONTROL Error ID] | `name` | string | Nee | De fout-id. |
| [!UICONTROL Error Source] | `source` | string | Nee | De foutenbron. Opsomming: &quot;player&quot;, &quot;external&quot; met respectieve betekenissen. |

{style="table-layout:auto"}
