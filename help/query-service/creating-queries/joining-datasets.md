---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Gegevenssets samenvoegen
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

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
WHERE _ACP_YEAR=2018 
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

![Afbeelding](../images/queries/joining-datasets/select-operating-systems.png)