---
keywords: Experience Platform;home;populaire onderwerpen;queryservice;Query-service;ExperienceEvent-query;ExperienceEvent-query;ExperienceEvent-query;
title: Een roll-uprapport voor een specifieke bezoeker weergeven
description: In het volgende document worden voorbeelden gegeven van query's voor Experience Events in Adobe Experience Platform Query Service.
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# Een roll-uprapport voor een specifieke bezoeker weergeven

Dit document verstrekt een SQL voorbeeld om gegevens van veelvoudige analytische eigenschappen voor een specifieke gebruiker samen te voegen en die gegevens samen in één rapport te zien. Met Adobe Experience Platform Query Service kunt u query&#39;s schrijven die worden gebruikt [!DNL Experience Events] om verschillende gebruiksgevallen vast te leggen. De Gebeurtenissen van de ervaring worden vertegenwoordigd door de klasse ExperienceEvent van het Gegevensmodel van de Ervaring (XDM), die een onveranderlijke en niet-geaggregeerde momentopname van het systeem vangt wanneer een gebruiker met een website of de dienst interactie aangaat. De Gebeurtenissen van de ervaring kunnen zelfs voor tijd-domeinanalyse worden gebruikt. Zie de [sectie Volgende stappen](#next-steps) voor meer gebruik: [!DNL Experience Events] om bezoekersrapporten te genereren.

Meer informatie over XDM en [!DNL Experience Events] kunt u vinden in het dialoogvenster [[!DNL XDM System] overzicht](../../xdm/home.md). Door de Dienst van de Vraag met te combineren [!DNL Experience Events], kunt u gedragstrends onder uw gebruikers effectief volgen. Het volgende document bevat voorbeelden van query&#39;s die betrekking hebben op [!DNL Experience Events].

## Doelstelling

In het volgende SQL-voorbeeld ziet u hoe u een geaggregeerd rapport van verschillende analysewaarden voor een opgegeven gebruiker bekijkt.

```sql
SELECT 
endUserIds._experience.aaid.id, 
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
WHERE endUserIds._experience.aaid.id = '457C3510571E5930-69AA721C4CBF9339' 
GROUP BY endUserIds._experience.aaid.id
ORDER BY pageViews DESC;
```

De resultaten van de query worden weergegeven in de onderstaande tabel.

```console
               id                 | pageViews |   A   |   B   |   C   | viewedParkas
----------------------------------+-----------+-------+-------+-------+--------------
457C3510571E5930-69AA721C4CBF9339 |     706.0 | 83.0  |  7.0  | 38.0  |          22
```

## Volgende stappen {#next-steps}

Door dit document te lezen, hebt u een beter inzicht in hoe te om de Dienst van de Vraag met te gebruiken [!DNL Experience Events] om een geaggregeerd rapport weer te geven van analysewaarden voor een opgegeven gebruiker.

Raadpleeg de volgende gebruiksgevallen voor meer informatie over andere gebruikte gevallen die door bezoekers worden gebruikt:

- [Hiermee haalt u een lijst met bezoekers op, ingedeeld op basis van het aantal paginaweergaven.](./visitors-by-number-of-page-views.md)
- [De vorige sessies van een bezoeker weergeven.](./list-visitor-sessions.md)
- [Maak een verouderd rapport van gebeurtenissen per dag.](./trended-report-of-events.md)
