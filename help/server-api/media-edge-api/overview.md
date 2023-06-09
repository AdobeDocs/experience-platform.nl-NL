---
keywords: Experience Platform;mediarand;populaire onderwerpen;datumbereik
solution: Experience Platform
title: Media Edge-API's
description: Overzicht van de mediarand-API's.
exl-id: null
source-git-commit: f040ba6d1403da4212fe279e32316bac995905b2
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 2%

---


# Overzicht van de Media Edge API

Media Edge-API&#39;s zijn gebaseerd op de Adobe Experience Platform (AEP) en leveren gegevens voor het bijhouden van mediagebeurtenissen in het kader van [XDM-schema&#39;s](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=en#:~:text=Experience%20Data%20Model%20(XDM)%2C,the%20power%20of%20digital%20experiences). Voor klanten van Media Analytics, maakt dit de volgende eigenschappen beschikbaar:

* Met [Customer Journey Analytics (CJA)](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=en), kunnen klanten bijna real-time, korrelige details van duur krijgen, beginnen, en einden om voor media metriek te evalueren en te combineren. Klanten die vanuit Adobe Analytics migreren, beschikken over alle rapporteringsgegevens in CJA.

* Met [Adobe Real-time Customer Data Platform (CDP)](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=nl)klanten kunnen hun realtime profielen verrijken met gegevens over mediaverbruik.

* Met [Adobe Journey Optimizer (AJO)](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=en), kunnen klanten omnichannel campagnes optimaliseren en reizen automatiseren met signalen van mediaconsumptie.


## Gegevensstromen voor het bijhouden van media optimaliseren

Beide [Media-verzameling](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-overview.html?lang=en&amp;media-tracking-data-flows) API&#39;s en Media Edge API&#39;s bieden mediatrackinggegevens als RESTful-services. Maar het gebruik van de Media Edge-service heeft de volgende voordelen:

* Het is de eenvoudigste manier om XDM-schema&#39;s in uw gegevensstroom op te nemen.

* De vraag van een media speler richt rechtstreeks aan [Ervaar Edge Platform Network](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=en).

* Mediagebeurtenissen worden het meest efficiënt bijgehouden.

In de volgende tabel worden de beste Adobe API-service voor verschillende gevallen van mediaverlichting weergegeven:

| Gebruiksscenario | Platform | API-service |
| -------- | ------ | ---------- |
| CJA | AEP | Mediarand |
| CDP + CJA | AEP | Mediarand |
| Analyse + CJA | AEP | Mediarand |
| Verouderde analyse | N.v.t. | Media-verzameling |

>[!NOTE]
>
> De dienst van API van de Inzameling van Media voor Analtyics ontvangt nog XDM gegevens, maar is niet geoptimaliseerd voor het in zoverre dat de dienst van de Rand van Media is. Afhankelijk van de gegevens die van de Speler van Media worden verzonden, kunnen sommige Analytics-slechts gegevens ook door de dienst van de Rand van Media worden verpletterd API.

In de volgende afbeelding ziet u de gegevensstromen voor de twee API-services:


![Gegevensstromen van mediaveralyse](../assets/edge-api-dataflow.png)


Raadpleeg de documentatie Aan de slag voor meer informatie over het gebruik van Media Edge API&#39;s.

Voor meer informatie over het werken met de Rand van het Platform, zie [Media Analytics installeren met Experience Platform Edge](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/implementation-edge.html?lang=en).




