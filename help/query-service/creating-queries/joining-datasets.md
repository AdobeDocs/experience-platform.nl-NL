---
keywords: Experience Platform;home;popular topics;query service;Query service;joining datasets;joining dataset;
solution: Experience Platform
title: Gegevenssets samenvoegen
topic: queries
type: Tutorial
description: Het aansluiten van datasets staat u toe om gegevens van andere datasets in uw vraag te omvatten. In dit voorbeeld wordt een aangepaste gegevensset van het besturingssysteem gebruikt om de besturingssysteemid toe te wijzen aan de waarde van het besturingssysteem.
translation-type: tm+mt
source-git-commit: 37356db1666b0c800119b1e254940ad72550848a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 1%

---


# Gegevenssets samenvoegen

Het aansluiten van datasets staat u toe om gegevens van andere datasets in uw vraag te omvatten. In dit voorbeeld wordt een aangepaste gegevensset van het besturingssysteem gebruikt om de gegevens toe te wijzen `operatingsystemID` aan de `operatingsystem` waarde.

Gegevenssets:
- your_analytics_table
- custom_operating_system_lookup

Maak een `SELECT` instructie voor de bovenste 50 besturingssystemen op basis van het aantal paginaweergaven.

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE TIMESTAMP >= ('2018-01-01') AND TIMESTAMP <= ('2018-12-31')
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

![Image](../images/queries/joining-datasets/select-operating-systems.png)