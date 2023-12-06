---
solution: Experience Platform
title: Media Edge-API's
description: Overzicht van mediarand-API's
exl-id: 55c952de-caab-4301-acf2-f7b64cebbb1c
source-git-commit: 034498e662ed55112f22751d44cf3ecf75d38d61
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 1%

---

# Overzicht van de Media Edge API

Media Edge-API&#39;s zijn gebaseerd op de Adobe Experience Platform en bieden in het kader van [XDM-schema&#39;s](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html#:~:text=Experience%20Data%20Model%20(XDM)%2C,the%20power%20of%20digital%20experiences). Voor klanten van Media Analytics, maakt dit de volgende eigenschappen beschikbaar:

* Met [Adobe Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html), kunnen klanten bijna real-time, korrelige details van duur krijgen, beginnen, en houdt op om voor media metriek te evalueren en te combineren. Klanten die vanuit Adobe Analytics migreren, beschikken over alle statistische gegevens voor rapportage in Adobe Customer Journey Analytics.

* Met [Adobe Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=nl)klanten kunnen hun realtime profielen verrijken met gegevens over mediaverbruik.

* Met [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=nl), kunnen klanten omnichannel campagnes optimaliseren en reizen automatiseren met signalen van mediaconsumptie.


## Gegevensstromen voor het bijhouden van media optimaliseren

Beide [Media Collection-API&#39;s](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-overview.html#media-tracking-data-flows) en Media Edge-API&#39;s bieden mediatrackinggegevens als RESTful-services. Maar het gebruik van de Media Edge-service heeft de volgende voordelen:

* Het is de eenvoudigste manier om XDM-schema&#39;s in uw gegevensstroom op te nemen.

* De vraag van een media speler richt rechtstreeks aan [Experience Platform Edge Network](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html).

* Het volgt media gebeurtenissen efficiënt met een minimum van dwars-servervraag.

In de volgende tabel ziet u een mogelijke API-service voor Adobe voor verschillende gevallen van mediaverlichting:

| Gebruiksscenario | API-service |
| -------- | ----------- |
| Adobe Experience Platform-oplossing | Mediarand |
| REAL-TIME CDP + CUSTOMER JOURNEY ANALYTICS | Mediarand |
| Adobe Analytics + Adobe Experience Platform oplossing | Mediarand |
| Alleen Adobe Analytics (al gevolgd) | Media-verzameling |

>[!NOTE]
>
> De dienst van API van de Inzameling van Media voor Analtyics ontvangt nog XDM gegevens, maar is niet geoptimaliseerd voor het voor zover de dienst van de Rand van Media is. Afhankelijk van de gegevens die van de Speler van Media worden verzonden, kunnen sommige Analytics-slechts gegevens ook door de dienst van de Rand van Media worden verpletterd API.

In de volgende afbeelding ziet u de gegevensstromen voor de twee API-services:

![Gegevensstromen van mediaveralyse](../assets/edge-api-dataflow.png)

## Volgende stappen

* Raadpleeg voor meer informatie over het gebruik van Media Edge API&#39;s de [Aan de slag - documentatie](getting-started.md).

* Voor meer informatie over het werken met de Rand van het Platform, zie [Media Analytics installeren met Experience Platform Edge](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/implementation-edge.html).
