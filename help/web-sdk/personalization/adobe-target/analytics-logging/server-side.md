---
title: Logboekregistratie op de server voor A4T-gegevens in Platform Web SDK
description: Leer hoe te om server-zijregistreren voor Adobe Analytics voor Doel (A4T) toe te laten gebruikend het Web SDK van het Experience Platform.
seo-title: Server-side logging for A4T data in Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;target;web;sdk;platform;logging;
exl-id: 26c25f58-e43c-4147-8595-69ea85af561f
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# Logboekregistratie op de server voor A4T-gegevens in Platform Web SDK

Met de Adobe Experience Platform Web SDK kunt u de functionaliteit Adobe Analytics for Target (A4T) implementeren op Platform Edge Network. Wanneer het server-zij registreren wordt toegelaten, worden alle Analytische die hits door de Edge Network worden verzonden uitgebreid met de details van het Doel op de server, zonder het moeten door het raakstitching proces gaan.

Logboekregistratie op de server voor Analytics wordt ingeschakeld wanneer Analytics is ingeschakeld in de configuratie van de gegevensstroom:

![ toegelaten de gegevensstroomconfiguratie van Analytics ](../assets/enable-analytics-datastream.png)

Het volgende diagram toont hoe de gegevens door het systeem stromen wanneer de server-kant het Registreren van Analytics wordt toegelaten:

![ server-kant registrerenstroom ](../assets/analytics-server-side-logging.png)

## Volgende stappen

Deze gids behandelde server-zijregistreren voor A4T gegevens in het Web SDK. Zie de gids op [ cliënt-kant registreren ](./client-side.md) voor meer informatie over hoe te om A4T gegevens op de cliëntkant te behandelen.
