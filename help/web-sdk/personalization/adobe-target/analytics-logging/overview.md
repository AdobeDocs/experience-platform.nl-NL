---
title: Adobe Analytics for Target (A4T)-aanmelding in de Platform Web SDK
description: Leer hoe te om de inzameling van Adobe Analytics voor Doel (A4T) gegevens te controleren gebruikend het Web SDK van het Experience Platform.
seo-title: Adobe Analytics for Target (A4T) Logging in the Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t;logging;analytics;sdk;web sdk;
exl-id: f1c90ccd-48a9-4668-b2ac-eacd5bec0b91
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# Aanmelden bij Adobe Analytics for Target (A4T) via de Platform Web SDK

Als u Adobe Target gebruikt voor personalisatie, kunt u kiezen welk systeem u wilt gebruiken voor het meten van de prestaties. Elk [ activiteit van het Doel ](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) staat u toe om tussen Doel te selecteren rapporterend en Adobe Analytics rapporterend.

Als u Analytics-rapporten gebruikt, moet Adobe Target het volgende aan Analytics meedelen:

* Welke Adobe Target-activiteit uw bezoekers hebben ingevoerd
* Welke ervaring ze hebben gezien
* Welke conversie is bereikt

De SDK van het Web van Adobe Experience Platform steunt twee soorten het registreren van Analytics voor Analytics voor het gebruiksgevallen van het Doel (A4T):

| Logmethode | Beschrijving |
| --- | --- |
| Logboekregistratie voor analyse op de server | Alle Analytics-resultaten die via de Edge Network worden verzonden, worden aangevuld met Target-gegevens aan de serverzijde, zonder dat het raakstitchproces hoeft te worden doorlopen. |
| Logboekregistratie voor clientanalyse | Het gegeven van het doel is teruggekeerd op de cliëntkant, toestaand u om gegevens aan Analytics manueel te verhogen en te verzenden gebruikend de [ Invoeging API van Gegevens ](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html). |

De registrerenmethode wordt bepaald door of u Adobe Analytics hebt toegelaten op uw gevormde [ datastream ](../../../../datastreams/overview.md):

![ Logging van de methodebeslissingsstroom ](../assets/analytics-logging.png)

## Volgende stappen

Dit document verstrekte een korte inleiding aan de verschillende registrerenmethodes voor gegevens A4T in het Web SDK. Raadpleeg de volgende documentatie voor meer informatie over elk van deze methoden:

* [Server-kant registreren voor A4T gegevens in het Web SDK van het Platform](./server-side.md)
* [Logboekregistratie aan de clientzijde voor A4T-gegevens in de Platform Web SDK](./client-side.md)
