---
keywords: Experience Platform;home;populaire onderwerpen;query-service;Query-service;ExperienceEvent-query;ExperienceEvent-query;Experience Event-query;
title: De paginaweergaven van een gebruiker weergeven
description: Leer hoe te vragen schrijven die de Gebeurtenissen van de Ervaring gebruiken om een lijst van de laatste 100 pagina's tot stand te brengen die een gespecificeerde gebruiker heeft gebruikt.
exl-id: d831910d-d3a4-4a5a-b897-b09f0546dab0
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# De paginaweergaven van een gebruiker weergeven

Dit document bevat een voorbeeld van de SQL-code die vereist is om de paginaweergaven weer te geven van een opgegeven gebruiker. Met Adobe Experience Platform Query Service kunt u query&#39;s schrijven die [!DNL Experience Events] gebruiken om verschillende gebruiksgevallen vast te leggen. De Gebeurtenissen van de ervaring worden vertegenwoordigd door de klasse ExperienceEvent van het Gegevensmodel van de Ervaring (XDM), die een onveranderlijke en niet-geaggregeerde momentopname van het systeem vangt wanneer een gebruiker met een website of de dienst interactie aangaat. De Gebeurtenissen van de ervaring kunnen zelfs voor tijd-domeinanalyse worden gebruikt. Zie [ volgende stappen sectie ](#next-steps) voor meer gebruiksgevallen die [!DNL Experience Events] impliceren om bezoekersrapporten te produceren.

Meer informatie over XDM en [!DNL Experience Events] kan in het [[!DNL XDM System]  overzicht ](../../xdm/home.md) worden gevonden. Door de Dienst van de Vraag met [!DNL Experience Events] te combineren, kunt u gedragstendensen onder uw gebruikers effectief volgen. Het volgende document bevat voorbeelden van query&#39;s die [!DNL Experience Events] betreffen.

## Doelstelling

In het volgende voorbeeld worden de laatste 100 pagina&#39;s weergegeven die een opgegeven gebruiker heeft weergegeven.

```sql
SELECT 
timestamp, 
web.webReferrer.type as referrerType, 
web.webReferrer.URL as referrer, 
web.webPageDetails.name as pageName, 
_experience.analytics.event1to100.event1.value as A, 
_experience.analytics.event1to100.event2.value as B, 
_experience.analytics.event1to100.event3.value as C, 
web.webPageDetails.pageviews.value as pageViews
FROM your_analytics_table 
WHERE endUserIds._experience.aaid.id = '457C3510571E5930-69AA721C4CBF9339' 
ORDER BY timestamp 
LIMIT 100;
```

De resultaten van deze query zijn hieronder te zien.

```console
      timestamp       |  referrerType  |                            referrer                                |                 pageName            |  A  |  B  |  C  | pageViews
|----------------------+----------------+--------------------------------------------------------------------+-------------------------------------+-----+-----+-----+--------------
2019-11-08 17:15:28.0 | typed_bookmark |                                                                    |                                     |     |     |     |
2019-11-08 17:53:05.0 | social         | http://www.reddit.com                                              | Home                                |     |     |     |          1.0
2019-11-08 17:53:45.0 | typed_bookmark |                                                                    | Kids                                |     |     |     |          1.0
2019-11-08 19:22:34.0 | typed_bookmark |                                                                    |                                     |     |     |     |          
2019-11-08 20:01:12.0 | search_engine  | http://www.google.com/search?ie=UTF-8&q=laundry parkas&cid=sem:115 | Home                                |     |     |     |          1.0 
2019-11-08 20:01:57.0 | typed_bookmark |                                                                    | Kids                                |     |     |     |          1.0
2019-11-08 20:03:36.0 | typed_bookmark |                                                                    | Search Results                      | 1.0 |     |     |          1.0
2019-11-08 20:04:30.0 | typed_bookmark |                                                                    | Product Details: Pemmican Power Bar |     |     |     |          1.0
2019-11-08 20:05:27.0 | typed_bookmark |                                                                    | Shopping Cart: Cart Details         |     |     |     |          1.0
2019-11-08 20:06:07.0 | typed_bookmark |                                                                    | Shopping Cart: Shipping Information |     |     |     |          1.0
2019-11-08 20:07:02.0 | typed_bookmark |                                                                    | Shopping Cart: Billing Information  |     |     | 1.0 |          1.0
2019-11-08 20:07:52.0 | typed_bookmark |                                                                    | Shopping Cart: Order Review         |     |     |     |          1.0
2019-11-08 20:08:45.0 | typed_bookmark |                                                                    | Order Confirmation                  |     |     |     |          1.0
2019-11-08 20:09:24.0 | typed_bookmark |                                                                    | Home                                |     |     |     |          1.0
2019-11-08 20:10:03.0 | typed_bookmark |                                                                    | Editorial Page: Camping Essentials  |     |     |     |          1.0
2019-11-08 20:11:01.0 | typed_bookmark |                                                                    | Account Registration|Form           |     |     |     |          1.0
2019-11-08 20:11:38.0 | typed_bookmark |                                                                    | Seasonal Sale                       |     |     |     |          1.0
2019-11-08 20:12:10.0 | typed_bookmark |                                                                    | Blog: Iris Sagan                    |     |     |     |          1.0
2019-11-08 20:13:09.0 | typed_bookmark |                                                                    | Product Details: UltraTech Socks    |     |     |     |          1.0
2019-11-08 20:14:05.0 | typed_bookmark |                                                                    | Seasonal Sale                       |     |     |     |          1.0
```

## Volgende stappen {#next-steps}

Door dit document te lezen, hebt u een beter inzicht in hoe u de Query-service met [!DNL Experience Events] kunt gebruiken om de paginaweergaven als een opgegeven gebruiker weer te geven.

Raadpleeg de volgende gebruiksgevallen voor meer informatie over andere gebruikte gevallen die door bezoekers worden gebruikt:

- [Hiermee wordt een lijst met bezoekers opgehaald die is ingedeeld op aantal paginaweergaven.](./visitors-by-number-of-page-views.md)
- [Een roll-uprapport van een bezoeker weergeven.](./roll-up-report-of-a-visitor.md)
- [Maak een verouderd rapport van gebeurtenissen per dag.](./trended-report-of-events.md)
