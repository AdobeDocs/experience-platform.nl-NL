---
title: Gegevenstype gegevens fout
description: Meer informatie over het gegevenstype Error Details Information Experience Data Model (XDM).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# [!UICONTROL Error Details Information] gegevenstype

[!UICONTROL Error Details Information] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat foutendetails beschrijft. Gebruik de [!UICONTROL Error Details Information] gegevenstype om details voor de foutenbron en identificatie te vangen. De fout-id identificeert de fout en de bron van de fout geeft aan of deze afkomstig is van de speler of van een externe bron.

![Een diagram van het gegevenstype Error Details.](../images/data-types/error-details-information.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|----------------|----------------|-----------|----------------------------------------------|
| [!UICONTROL Error ID] | `name` | string | De fout-id. |
| [!UICONTROL Error Source] | `source` | string | De foutenbron. Opsomming: &quot;player&quot;, &quot;external&quot; met respectieve betekenissen. |

{style="table-layout:auto"}

Voor meer informatie over de veldgroep raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json)
