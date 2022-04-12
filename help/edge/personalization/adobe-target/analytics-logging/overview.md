---
title: Adobe Analytics for Target (A4T) Aanmelden bij de Web SDK van het Platform
description: Leer hoe te om de inzameling van Adobe Analytics voor Doel (A4T) gegevens te controleren gebruikend het Web SDK van het Experience Platform.
seo-title: Adobe Analytics for Target (A4T) Logging in the Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t;logging;analytics;sdk;web sdk;
source-git-commit: a2214465001f90d19d88c0622c154e7a4ae3bb03
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---


# Aanmelden bij Adobe Analytics for Target (A4T) via de Web SDK van het Platform

Als u Adobe Target gebruikt voor personalisatie, kunt u kiezen welk systeem u wilt gebruiken voor het meten van de prestaties. Elk [Doelactiviteit](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) kunt u kiezen tussen Target-rapportage en Adobe Analytics-rapportage.

Als u Analytics-rapporten gebruikt, moet Adobe Target het volgende aan Analytics meedelen:

* Welke Adobe Target-activiteit uw bezoekers hebben ingevoerd
* Welke ervaring ze hebben gezien
* Welke conversie is bereikt

De SDK van het Web van Adobe Experience Platform steunt twee soorten het registreren van Analytics voor Analytics voor het gebruiksgevallen van het Doel (A4T):

| Logmethode | Beschrijving |
| --- | --- |
| Logboekregistratie voor analyse op de server | Alle Analytics-resultaten die via het Edge-netwerk worden verzonden, worden aangevuld met Target-gegevens aan de serverzijde, zonder dat u het hit-stitching-proces hoeft te doorlopen. |
| Logboekregistratie voor clientanalyse | De doelgegevens worden aan de clientzijde geretourneerd, zodat u gegevens handmatig kunt vergroten en naar Analytics kunt verzenden met de functie [API voor gegevensinvoer](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html). |

De registrerenmethode wordt bepaald door of u Adobe Analytics op uw gevormde hebt toegelaten [datastream](../../../fundamentals/datastreams.md):

![Beslissingsstroom voor de registratiemethode](../assets/analytics-logging.png)

## Volgende stappen

Dit document verstrekte een korte inleiding aan de verschillende registrerenmethodes voor gegevens A4T in het Web SDK. Raadpleeg de volgende documentatie voor meer informatie over elk van deze methoden:

* [Server-kant registreren voor A4T gegevens in het Web SDK van het Platform](./server-side.md)
* [Clientregistratie voor A4T-gegevens in de Web SDK van het Platform](./client-side.md)
