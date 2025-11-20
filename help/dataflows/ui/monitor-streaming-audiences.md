---
title: Volwassenen voor streaming monitoren
description: Leer hoe u het dashboard voor bewaking gebruikt om het publiek te controleren dat met behulp van streaming segmentatie is geëvalueerd
hide: true
hidefromtoc: true
source-git-commit: 6fe0a36a8f2ac2cb954935ee8fe64432442b6e84
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# Volwassenen voor streaming monitoren

intro blurb

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [ Dataflows ](../home.md): Dataflows vertegenwoordigen gegevensbanen die informatie over Experience Platform overbrengen. Zij worden gevormd over diverse diensten om de beweging van gegevens van bronschakelaars aan doeldatasets, evenals aan de Dienst van de Identiteit, het Profiel van de Klant in real time, en Doelen te vergemakkelijken.
* [ de Dienst van de Segmentatie ](../../segmentation/home.md):
* [ Capaciteiten ](../../landing/license-usage-and-guardrails/capacity.md): In Experience Platform, laten de capaciteiten u weten als uw organisatie om het even welk van uw gidsen heeft overschreden en geeft u informatie over hoe te om deze kwesties te bevestigen.

## Metrische gegevens voor streaming publiek controleren {#streaming-audience-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_audience_evaluation_rate"
>title="Evaluatiepercentage"
>abstract="Deze metrische waarde vertegenwoordigt het aantal records dat per seconde wordt geëvalueerd."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_audience_p95_latency"
>title="P95-inlaatlatentie"
>abstract="Deze maatstaf meet de latentie van het 95ste percentiel van een gebeurtenis die in Adobe Experience Platform aankomt aan succesvolle evaluatie in het publiek."
>text="Learn more in documentation"

De volgende lijst verstrekt meer gedetailleerde informatie over de metriek die voor het stromen publiek worden gebruikt.

| Metrisch | Beschrijving | Afmetingen |
| ------ | ----------- | ---------- |
| Evaluatiepercentage | Het aantal verwerkte publieksevaluaties per seconde. | Sandbox, gegevensset |
| P95-inlaatlatentie | De 95e percentiele latentie van de succesvolle gebeurtenis die in het publiek aankomt. | Sandbox, gegevensset |
| Ontvangen records | Het totale aantal records dat tijdens het geselecteerde tijdvenster van streamingopname voor streamingsegmentatie is ontvangen. | Gegevensset |
| Gedownloade records | Het totale aantal verslagen dat **** met succes het stromen segmentatie tijdens het geselecteerde tijdvenster evalueerde. | Gegevensset |
| Records mislukt | Het totale aantal verslagen dat **** evaluatie in het stromen segmentatie wegens fouten tijdens het geselecteerde tijdvenster ontbrak. | Dataset, Flow-uitvoering |
| Records overgeslagen | Het totale aantalverslagen die **** evaluatie in het stromen segmentatie wegens fouten tijdens het geselecteerde tijdvenster overgeslagen. | Dataset, Flow-uitvoering |
| Profielen gekwalificeerd | Het aantal profielen dat tijdens het geselecteerde tijdvenster voor het publiek is gekwalificeerd. | Sandbox, publiek |
| Profielen gediskwalificeerd | Het aantal profielen dat tijdens het geselecteerde tijdvenster van het publiek is uitgesloten. | Sandbox, publiek |

{style="table-layout:auto"}

## Het monitoringdashboard gebruiken voor streaming publiek {#monitoring-dashboard}

Ga naar de gebruikersinterface van Experience Platform en selecteer **[!UICONTROL Monitoring]** in de linkernavigatie om het dashboard voor controle van streaming publiek te openen. Selecteer vervolgens **[!UICONTROL Streaming end-to-end]** .

AFBEELDING

Boven aan het dashboard bevindt zich de **[!UICONTROL Audiences]** -kaart. Dit toont informatie over het **tarief van de Evaluatie** voor het publiek.