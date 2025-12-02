---
title: Overschrijving van gebeurtenissen afhandelen in Experience Platform
description: Leer hoe Adobe Experience Platform dubbel werk bij gebeurtenissen verwerkt
exl-id: ac8c3ee8-52cf-459c-b283-16ed32d2976d
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# Overschrijving van gebeurtenissen afhandelen in Adobe Experience Platform

Adobe Experience Platform is een sterk gedistribueerd systeem dat is ontworpen om de betrouwbaarheid te maximaliseren en tegelijk te schalen naar steeds grotere hoeveelheden gegevens.

Voor gegevensinzameling in real time, {de Gebeurtenissen van de Ervaring [ worden verzameld via Edge Network, van cliënt-zijbronnen, zoals SDK van het Web of ](/help/xdm/classes/experienceevent.md) Mobiele SDK [, en geleverd aan de verwerking en opslaglagen van Experience Platform. ](https://developer.adobe.com/client-sdks/home/) Deze lagen stellen oplossingen zoals Experience Platform samen, [ Real-Time CDP ](/help/rtcdp/home.md), [ Customer Journey Analytics ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html), en [ Adobe Journey Optimizer ](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html).

Om Ervaring-gebeurtenisverlies te minimaliseren, verwachten SDK&#39;s aan de clientzijde en de interne Experience Platform-leveringsservice een bevestiging dat een gebeurtenis correct is verzameld.

Als deze bevestiging niet wordt ontvangen, brengen de client-side SDK&#39;s of de interne Experience Platform-leveringsservice een nieuwe poging in en wordt de Experience Event opnieuw verzonden.

Dit is de beste manier om fouten van voorbijgaande aard te verwerken. De bijwerking is de mogelijkheid om dubbele gebeurtenissen in te voeren.

Om beter te begrijpen beste praktijken voor de behandeling van voorbijgaande mislukkingen, zie dit artikel op [ voorbijgaande fout behandeling ](https://learn.microsoft.com/en-us/azure/architecture/best-practices/transient-faults).

## Gebeurtenisduplicatiescenario&#39;s {#scenarios}

Dubbele gebeurtenissen kunnen in verschillende scenario&#39;s voorkomen, zoals, maar niet beperkt tot:

* Netwerkgerelateerde problemen tussen client-side SDK&#39;s en de [!DNL Edge Network] . Deze kwesties kunnen uit de mislukkingen van Internet Service Provider, mobiel signaalverlies, of andere netwerkmislukkingen voortkomen, aangezien de connectiviteit tussen de klant en Edge Network door openbaar Internet wordt gedaan.
* Interne Experience Platform-gebeurtenissen voor automatisch schalen Soms kunnen gegevens opnieuw in evenwicht worden gebracht vanwege de volatiliteit van de cloudinfrastructuur.

De Adobe Experience Platform-gegevensverzamelingslaag is ontworpen ter ondersteuning van verwerking &quot;minstens één keer&quot;. Daarom kan dubbel optreden in beperkte, zeldzame situaties.

Om meer over &quot;minstens één keer&quot;verwerking te leren, zie dit artikel op [ garanties van de berichtlevering ](https://docs.confluent.io/kafka/design/delivery-semantics.html).

## Opties voor deduplicatie van gebeurtenissen {#deduplication}

Voor bedrijfsscenario&#39;s die gevoelig zijn voor dubbele gebeurtenissen, gebruikt Experience Platform meerdere deduplicatiemethoden voor gebeurtenissen in de downstreamopslagsystemen, zoals de hieronder beschreven methoden.

* Real-Time CDP Profile store slaat gebeurtenissen over als er al een gebeurtenis met dezelfde `_id` in [!DNL Profile store] bestaat. Zie de documentatie op [ klasse XDM ExperienceEvent ](/help/xdm/classes/experienceevent.md) voor meer details.
* Customer Journey Analytics staat gebruikers toe om metrisch te vormen om waarden niet-herhalend slechts te tellen. Leren hoe te om dit te doen, zie de documentatie op [ metrische montages van de deduplicatiecomponent ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication.html?lang=en).
* De Dienst van de Vraag van Experience Platform steunt gegevensdeduplicatie wanneer het wordt vereist om een volledige rij uit een berekening te verwijderen of een specifieke reeks gebieden te negeren omdat slechts een deel van de gegevens in de rij dubbele informatie is. Zie de documentatie rond [ gegevensdeduplicatie in de Dienst van de Vraag ](/help/query-service/key-concepts/deduplication.md) voor meer informatie.

>[!NOTE]
>
>Als u problemen ondervindt met het dupliceren van gebeurtenissen buiten de hierboven vermelde gebruiksgevallen, neemt u contact op met uw Adobe-vertegenwoordiger en geeft u gedetailleerde informatie over uw gebruiksscenario.
