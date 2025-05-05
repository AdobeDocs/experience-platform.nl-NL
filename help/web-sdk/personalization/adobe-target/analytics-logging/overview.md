---
title: Adobe Analytics for Target (A4T) Aanmelden bij Experience Platform Web SDK
description: Leer hoe te om de inzameling van Adobe Analytics voor Doel (A4T) gegevens te controleren gebruikend het Web SDK van Experience Platform.
seo-title: Adobe Analytics for Target (A4T) Logging in the Experience Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t;logging;analytics;sdk;web sdk;
exl-id: f1c90ccd-48a9-4668-b2ac-eacd5bec0b91
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Aanmelden bij Adobe Analytics for Target (A4T) via Experience Platform Web SDK

Als u Adobe Target gebruikt voor personalisatie, kunt u kiezen welk systeem u wilt gebruiken voor het meten van de prestaties. Elk [ activiteit van het Doel ](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html?lang=nl-NL) staat u toe om tussen Doel te selecteren rapporterend en Adobe Analytics rapporterend.

Als u Analytics-rapporten gebruikt, moet Adobe Target het volgende aan Analytics meedelen:

* Welke Adobe Target-activiteit uw bezoekers hebben ingevoerd
* Welke ervaring ze hebben gezien
* Welke conversie is bereikt

Adobe Experience Platform Web SDK steunt twee types van het registreren van Analytics voor Analytics voor het gebruiksgevallen van het Doel (A4T):

| Logmethode | Beschrijving |
| --- | --- |
| Logboekregistratie voor analyse op de server | Alle Analytics-resultaten die via de Edge Network worden verzonden, worden aangevuld met Target-gegevens aan de serverzijde, zonder dat u het detectieproces hoeft te doorlopen. |
| Logboekregistratie voor clientanalyse | Het gegeven van het doel is teruggekeerd op de cliëntkant, toestaand u om gegevens aan Analytics manueel te verhogen en te verzenden gebruikend de [ Invoeging API van Gegevens ](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html?lang=nl-NL). |

De registrerenmethode wordt bepaald door of u Adobe Analytics hebt toegelaten op uw gevormde [ datastream ](../../../../datastreams/overview.md):

![ Logging van de methodebeslissingsstroom ](../assets/analytics-logging.png)

## Volgende stappen

Dit document verstrekte een korte inleiding aan de verschillende registrerenmethodes voor gegevens A4T in het Web SDK. Raadpleeg de volgende documentatie voor meer informatie over elk van deze methoden:

* [Logboekregistratie op de server voor A4T-gegevens in Experience Platform Web SDK](./server-side.md)
* [Logboekregistratie op de client voor A4T-gegevens in de Experience Platform Web SDK](./client-side.md)
