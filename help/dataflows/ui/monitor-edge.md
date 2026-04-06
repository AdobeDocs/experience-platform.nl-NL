---
title: Segmentatie rand monitor
description: Leer hoe u het dashboard voor bewaking gebruikt om de doorvoer van de segmentatie van randen te observeren.
exl-id: 7abba7e8-1f2d-4a21-a93f-8bda7aa4d849
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# Segmentatie rand monitor

U kunt het controledashboard in Adobe Experience Platform UI gebruiken om controle in real time van randsegmentatie binnen uw organisatie uit te voeren. Met deze functie hebt u toegang tot meer transparantie in de doorvoer van uw randgegevens.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [&#x200B; Gegevensstromen &#x200B;](../../datastreams/overview.md): De stromen van gegevensstromen laten u Experience Platform Edge Network met uw dataset verbinden.
* [&#x200B; Capaciteiten &#x200B;](../../landing/license-usage-and-guardrails/capacity.md): In Experience Platform, laten de capaciteiten u weten als uw organisatie om het even welk van uw gidsen heeft overschreden en geeft u informatie over hoe te om deze kwesties te bevestigen.
* [&#x200B; de segmentatie van Edge &#x200B;](../../segmentation/methods/edge-segmentation.md): De segmentatie van Edge is de capaciteit om segmentdefinities in Adobe Experience Platform onmiddellijk [&#x200B; op de rand &#x200B;](../../landing/edge-and-hub-comparison.md) te evalueren, toelatend de zelfde pagina en volgende het gebruikscase van de paginaletterdheid.

## Toegang {#access}

Selecteer **[!UICONTROL Monitoring]** in de sectie **[!UICONTROL Data management]** , gevolgd door **[!UICONTROL Edge]** om het dashboard voor segmentatie van randen te openen.

![&#x200B; de methode om tot het dashboard van de segmentatie van de monitorrand toegang te hebben wordt benadrukt.](/help/dataflows/assets/ui/monitor-edge/access.png)

Het dashboard voor bewaking wordt weergegeven. Dit toont controlemetriek voor de productie van het randstromen, een grafiek die het tarief van de rand het stromen productie, en een gegevensstroommening toont. Deze metriek kan door de dienst, door rand, en door datum worden gefiltreerd.

![&#x200B; de het filtreren opties binnen het controledashboard worden benadrukt.](/help/dataflows/assets/ui/monitor-edge/filtering.png)

>[!NOTE]
>
>U kunt de mening slechts **zien DataStream als u** selecteert.[!UICONTROL Edge segmentation throughput]

Als u door de dienst filtreert, kunt u kiezen welke dienst u de productieinformatie over wilt bekijken. Dit omvat de diensten zoals de segmentatie van Edge, de inzameling van Gegevens, Doel, Adobe Journey Optimizer, Offer Decisioning, Douane gepersonaliseerde bestemmingen, Gebeurtenis door:sturen, Adobe Analytics, en Adobe Audience Manager.

Als u filtert op rand, kunt u kiezen over welke rand u informatie wilt bekijken. Tot de ondersteunde randen behoren US East Coast, US West Coast, Europe, India, Singapore, Australië, Japan en Zwitserland. U kunt meerdere randen tegelijk selecteren om weer te geven.

Als u filtert op datum, kunt u de tijdschaal kiezen om uw gebeurtenissen te filteren. Deze termijn kan worden ingesteld op 30 dagen. U kunt ook een van de volgende vooraf geconfigureerde tijdschalen gebruiken: [!UICONTROL Last 6 hours], [!UICONTROL Last 12 hours], [!UICONTROL Last 24 hours], [!UICONTROL Last 7 days] en [!UICONTROL Last 30 days] .

## Metrische gegevens voor Edge-doorvoer controleren

De metrieklijst verstrekt informatie specifiek voor de geselecteerde de randproductie van de dienst. U kunt naar de volgende lijst voor meer details over elke kolom verwijzen.

| Metrisch | Beschrijving |
| ------ | ----------- |
| Ontvangen verzoeken | Het aantal aanvragen dat door de geselecteerde randen binnen de tijdlijn wordt ontvangen. |
| Maximale doorvoer | Het hoogste percentage aanvragen dat door de geselecteerde randen binnen de tijdlijn wordt ontvangen. |

{style="table-layout:auto"}

## Grafiek controleren voor de doorvoer van de randsegmentatie

In de monitoringgrafiek worden de records per seconde weergegeven die de geselecteerde randen binnen de toegewezen tijdlijn hebben ontvangen, in vergelijking met de maximaal toegestane capaciteit.

![&#x200B; de grafiek van de randsegmentatieproductie wordt getoond.](/help/dataflows/assets/ui/monitor-edge/edge-segmentation-throughput.png)

## DataStream-weergave

>[!NOTE]
>
>De gegevensstroommening is **slechts** beschikbaar als u voor de segmentatieproductie van Edge filtreert.

In de sectie voor de gegevensstroomweergave wordt een lijst weergegeven met de meest recente gegevensstromen die door de randen van de sandbox zijn doorgegeven.

![&#x200B; de gegevensstroommening wordt getoond, tonend informatie over de vermelde gegevensstromen.](/help/dataflows/assets/ui/monitor-edge/datastream-view.png)

| Veld | Beschrijving |
| ----- | ----------- |
| Naam gegevensstroom | De naam van de gegevensstroom. |
| Gegevenssets | De naam van datasets tot de gegevensstroom behoort. |
| Service ingeschakeld | De namen van de diensten de gegevensstroom wordt toegelaten voor. |
| Verzoeken | Het aantal verzoeken dat door de datastream is overgegaan. |
| Maximale doorvoer | Het hoogste tarief van verzoeken die door de datastream overgingen. |
