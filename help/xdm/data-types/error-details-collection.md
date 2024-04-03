---
title: Foutdetails Gegevenstype verzameling
description: Meer informatie over het gegevenstype Error Details Collection Data Model (XDM).
source-git-commit: 899c656a7295896b291ac5c80df873711bc6f149
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# [!UICONTROL Error Details] Gegevenstype verzameling

[!UICONTROL Error Details] Verzameling is een standaard XDM-gegevenstype (Experience Data Model) waarmee de details van fouten worden beschreven. Gebruik de [!UICONTROL Error Details] Het gegevenstype van de inzameling om details voor de foutenbron en identificatie te vangen. De fout-id identificeert de fout en de bron van de fout geeft aan of deze afkomstig is van de speler of van een externe bron.

![Een diagram van het gegevenstype Error Details.](../images/data-types/error-details-collection.png)

| Weergavenaam | Eigenschap | Gegevenstype | Vereist | Beschrijving |
|----------------------------|--------------|-----------|----------|-----------------------------------------------|
| [!UICONTROL Error ID] | `name` | string | Nee | De fout-id. |
| [!UICONTROL Error Source] | `source` | string | Nee | De foutenbron. Opsomming: &quot;player&quot;, &quot;external&quot; met respectieve betekenissen. |

{style="table-layout:auto"}
