---
keywords: Experience Platform;home;populaire onderwerpen;query-service;Query-service;ExperienceEvent-query;ExperienceEvent-query;Experience Event-query;
title: Een roll-uprapport voor een specifieke bezoeker weergeven
description: In het volgende document worden voorbeelden gegeven van query's voor Experience Events in Adobe Experience Platform Query Service.
exl-id: 1348503f-65c1-41f9-b111-1284a49449a1
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# Een roll-uprapport voor een specifieke bezoeker weergeven

Dit document verstrekt een SQL voorbeeld om gegevens van veelvoudige analytische eigenschappen voor een specifieke gebruiker samen te voegen en die gegevens samen in één rapport te zien. Met Adobe Experience Platform Query Service kunt u query&#39;s schrijven die [!DNL Experience Events] gebruiken om verschillende gebruiksgevallen vast te leggen. De Gebeurtenissen van de ervaring worden vertegenwoordigd door de klasse ExperienceEvent van het Gegevensmodel van de Ervaring (XDM), die een onveranderlijke en niet-geaggregeerde momentopname van het systeem vangt wanneer een gebruiker met een website of de dienst interactie aangaat. De Gebeurtenissen van de ervaring kunnen zelfs voor tijd-domeinanalyse worden gebruikt. Zie [&#x200B; volgende stappen sectie &#x200B;](#next-steps) voor meer gebruiksgevallen die [!DNL Experience Events] impliceren om bezoekersrapporten te produceren.

Meer informatie over XDM en [!DNL Experience Events] kan in het [[!DNL XDM System]  overzicht &#x200B;](../../xdm/home.md) worden gevonden. Door de Dienst van de Vraag met [!DNL Experience Events] te combineren, kunt u gedragstendensen onder uw gebruikers effectief volgen. Het volgende document bevat voorbeelden van query&#39;s die [!DNL Experience Events] betreffen.

## Doelstelling

In het volgende SQL-voorbeeld ziet u hoe u een geaggregeerd rapport van verschillende analysewaarden voor een opgegeven gebruiker kunt weergeven.

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
|----------------------------------+-----------+-------+-------+-------+--------------
457C3510571E5930-69AA721C4CBF9339 |     706.0 | 83.0  |  7.0  | 38.0  |          22
```

## Volgende stappen {#next-steps}

Door dit document te lezen, hebt u een beter inzicht in hoe te om de Dienst van de Vraag met [!DNL Experience Events] te gebruiken om een samengevouwen rapport van analysewaarden voor een gespecificeerde gebruiker te bekijken.

Raadpleeg de volgende gebruiksgevallen voor meer informatie over andere gebruikte gevallen die door bezoekers worden gebruikt:

- [Hiermee wordt een lijst met bezoekers opgehaald die is ingedeeld op aantal paginaweergaven.](./visitors-by-number-of-page-views.md)
- [De vorige sessies van een bezoeker weergeven.](./list-visitor-sessions.md)
- [Maak een verouderd rapport van gebeurtenissen per dag.](./trended-report-of-events.md)
