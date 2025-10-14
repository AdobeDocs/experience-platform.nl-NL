---
title: Logboekregistratie op de server voor A4T-gegevens in Experience Platform Web SDK
description: Leer hoe te om server-zijregistreren voor Adobe Analytics voor Doel (A4T) toe te laten gebruikend het Web SDK van Experience Platform.
seo-title: Server-side logging for A4T data in Experience Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;target;web;sdk;platform;logging;
exl-id: 26c25f58-e43c-4147-8595-69ea85af561f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# Logboekregistratie op de server voor A4T-gegevens in Experience Platform Web SDK

Met de Adobe Experience Platform Web SDK kunt u Adobe Analytics for Target (A4T)-functionaliteit implementeren in Experience Platform Edge Network. Wanneer de server-kant registreren wordt toegelaten, worden alle Analytics die door Edge Network worden verzonden uitgebreid met de details van het Doel op de server, zonder het moeten door het raakstitching proces gaan.

Logboekregistratie op de server voor Analytics wordt ingeschakeld wanneer Analytics is ingeschakeld in de configuratie van de gegevensstroom:

![&#x200B; toegelaten de gegevensstroomconfiguratie van Analytics &#x200B;](../assets/enable-analytics-datastream.png)

Het volgende diagram toont hoe de gegevens door het systeem stromen wanneer de server-kant het Registreren van Analytics wordt toegelaten:

![&#x200B; server-kant registrerenstroom &#x200B;](../assets/analytics-server-side-logging.png)

## Volgende stappen

Deze gids behandelde server-zijregistreren voor A4T gegevens in het Web SDK. Zie de gids op [&#x200B; cliënt-kant registreren &#x200B;](./client-side.md) voor meer informatie over hoe te om A4T gegevens op de cliëntkant te behandelen.
