---
keywords: Experience Platform;home;populaire onderwerpen;queryservice;Query-service;ExperienceEvent-query;ExperienceEvent-query;ExperienceEvent-query;
title: Een trendrapport van gebeurtenissen maken
description: Leer hoe te om vragen te schrijven die de Gebeurtenissen van de Ervaring gebruiken om een trended rapport van gebeurtenissen over een gespecificeerde datumwaaier, gegroepeerd door datum tot stand te brengen.
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---

# Een vernieuwd rapport van gebeurtenissen maken

Dit document bevat een voorbeeld van de SQL-code die nodig is om een trended-rapport van gebeurtenissen overdag over een bepaald datumbereik te maken. Met Adobe Experience Platform Query Service kunt u query&#39;s schrijven die worden gebruikt [!DNL Experience Events] om verschillende gebruiksgevallen vast te leggen. De Gebeurtenissen van de ervaring worden vertegenwoordigd door de klasse ExperienceEvent van het Gegevensmodel van de Ervaring (XDM), die een onveranderlijke en niet-geaggregeerde momentopname van het systeem vangt wanneer een gebruiker met een website of de dienst interactie aangaat. De Gebeurtenissen van de ervaring kunnen zelfs voor tijd-domeinanalyse worden gebruikt. Zie de [sectie Volgende stappen](#next-steps) voor meer gebruik: [!DNL Experience Events] om bezoekersrapporten te genereren.

De rapporten geven u toegang tot uw gegevens van het Platform om de strategische bedrijfsinzichten van uw organisatie te profiteren. Met deze rapporten, kunt u uw gegevens van het Platform op een verscheidenheid van manieren onderzoeken, zeer belangrijke metriek in gemakkelijk-aan-begrijpen formaten tonen, en de resulterende inzichten delen.

Meer informatie over XDM en [!DNL Experience Events] kunt u vinden in het dialoogvenster [[!DNL XDM System] overzicht](../../xdm/home.md). Door de Dienst van de Vraag met te combineren [!DNL Experience Events], kunt u gedragstrends onder uw gebruikers effectief volgen. Het volgende document bevat voorbeelden van query&#39;s die betrekking hebben op [!DNL Experience Events].

## Doelstellingen

In het volgende voorbeeld wordt een trended-rapport gemaakt van gebeurtenissen over een opgegeven datumbereik, gegroepeerd op datum. In dit SQL-voorbeeld worden diverse analysewaarden samengevat als `A`, `B`, en `C`en geeft vervolgens een overzicht van het aantal keren dat parka&#39;s in de loop van een maand zijn bekeken.

De tijdstempelkolom in [!DNL Experience Event] datasets heeft de UTC-indeling. In het voorbeeld wordt het `from_utc_timestamp()` om de tijdstempel te transformeren van UTC naar EDT en gebruikt vervolgens de `date_format()` gebruiken om de datum te isoleren van de rest van de tijdstempel.

```sql
SELECT 
date_format( from_utc_timestamp(timestamp, 'EDT') , 'yyyy-MM-dd') as Day,
SUM(web.webPageDetails.pageviews.value) as pageViews,
SUM(_experience.analytics.event1to100.event1.value) as A,
SUM(_experience.analytics.event1to100.event2.value) as B,
SUM(_experience.analytics.event1to100.event3.value) as C,
SUM(
    CASE 
    WHEN _experience.analytics.customDimensions.evars.evar1 = 'parkas' 
    THEN 1 
    ELSE 0 
    END) as viewedParkas
FROM your_analytics_table 
WHERE TIMESTAMP >= to_timestamp('2019-03-01') AND TIMESTAMP <= to_timestamp('2019-03-31')
GROUP BY Day 
ORDER BY Day ASC, pageViews DESC;
```

De resultaten van deze query zijn hieronder te zien.

```console
     Day     | pageViews |   A    |   B   |    C    | viewedParkas
-------------+-----------+--------+-------+---------+--------------
 2019-03-01  |   55317.0 | 8503.0 | 804.0 | 1578.0  |           73
 2019-03-02  |   55302.0 | 8600.0 | 854.0 | 1528.0  |           86
 2019-03-03  |   54613.0 | 8162.0 | 795.0 | 1568.0  |          100
 2019-03-04  |   54501.0 | 8479.0 | 832.0 | 1509.0  |          100
 2019-03-05  |   54941.0 | 8603.0 | 816.0 | 1514.0  |           73
 2019-03-06  |   54817.0 | 8434.0 | 855.0 | 1538.0  |           76
 2019-03-07  |   55201.0 | 8604.0 | 843.0 | 1517.0  |           64
 2019-03-08  |   55020.0 | 8490.0 | 849.0 | 1536.0  |           99
 2019-03-09  |   43186.0 | 6736.0 | 643.0 | 1150.0  |           52
 2019-03-10  |   48471.0 | 7542.0 | 772.0 | 1272.0  |           70
 2019-03-11  |   56307.0 | 8721.0 | 818.0 | 1571.0  |           81
 2019-03-12  |   55374.0 | 8653.0 | 843.0 | 1501.0  |           59
 2019-03-13  |   55046.0 | 8509.0 | 887.0 | 1556.0  |           65
 2019-03-14  |   55518.0 | 8551.0 | 848.0 | 1516.0  |           77
 2019-03-15  |   55329.0 | 8575.0 | 818.0 | 1607.0  |           96
 2019-03-16  |   55030.0 | 8651.0 | 815.0 | 1542.0  |           66
 2019-03-17  |   55143.0 | 8435.0 | 774.0 | 1572.0  |           65
 2019-03-18  |   54065.0 | 8211.0 | 816.0 | 1574.0  |          111
 2019-03-19  |   55097.0 | 8395.0 | 771.0 | 1498.0  |           86
 2019-03-20  |   55198.0 | 8472.0 | 863.0 | 1583.0  |           82
 2019-03-21  |   54978.0 | 8490.0 | 820.0 | 1580.0  |           83
 2019-03-22  |   55464.0 | 8561.0 | 820.0 | 1559.0  |           83
 2019-03-23  |   55384.0 | 8482.0 | 800.0 | 1139.0  |           82
 2019-03-24  |   55295.0 | 8594.0 | 841.0 | 1382.0  |           78
 2019-03-25  |   42069.0 | 6365.0 | 606.0 | 1509.0  |           62
 2019-03-26  |   49724.0 | 7629.0 | 724.0 | 1553.0  |           44
 2019-03-27  |   55111.0 | 8524.0 | 804.0 | 1524.0  |           94
 2019-03-28  |   55030.0 | 8439.0 | 822.0 | 1554.0  |           73
 2019-03-29  |   55281.0 | 8601.0 | 854.0 | 1580.0  |           73
 2019-03-30  |   55162.0 | 8538.0 | 846.0 | 1534.0  |           79
 2019-03-31  |   55437.0 | 8486.0 | 807.0 | 1649.0  |           68
 (31 rows)
```

## Volgende stappen {#next-steps}

Door dit document te lezen, hebt u een beter inzicht in hoe te om de Dienst van de Vraag met te gebruiken [!DNL Experience Events] om gedragstrends onder uw gebruikers effectief te volgen.

Informatie over andere op bezoekers gebaseerde gebruiksgevallen die [!DNL Experience Events], lees de volgende documenten:

- [Hiermee haalt u een lijst met bezoekers op, ingedeeld op basis van het aantal paginaweergaven.](./visitors-by-number-of-page-views.md)
- [De vorige sessies van een bezoeker weergeven.](./list-visitor-sessions.md)
- [Een roll-uprapport van een bezoeker weergeven.](./roll-up-report-of-a-visitor.md)
