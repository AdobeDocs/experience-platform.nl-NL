---
title: Omgaan met duplicatie van gebeurtenissen in Experience Platform
description: Leer hoe Adobe Experience Platform dubbel werk bij gebeurtenissen verwerkt
exl-id: ac8c3ee8-52cf-459c-b283-16ed32d2976d
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# Overschrijving van gebeurtenissen afhandelen in Adobe Experience Platform

Adobe Experience Platform is een sterk gedistribueerd systeem dat is ontworpen om de betrouwbaarheid te maximaliseren en tegelijk te schalen naar steeds grotere hoeveelheden gegevens.

Voor gegevensinzameling in real time, {de Gebeurtenissen van de Ervaring ](../xdm/classes/experienceevent.md) worden verzameld via de [ Edge Network ](../web-sdk/home.md#edge-network), van cliënt-zijbronnen, zoals [ Web SDK ](../web-sdk/home.md) of [ Mobiele SDK ](https://developer.adobe.com/client-sdks/home/), en geleverd aan de verwerking van het Experience Platform en opslaglagen. [ Deze lagen stellen oplossingen zoals Experience Platform samen, [ Real-Time CDP ](../rtcdp/home.md), [ Customer Journey Analytics ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html), en [ Adobe Journey Optimizer ](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html).

Om het verlies van de Gebeurtenis van de Ervaring te minimaliseren, verwachten de cliënt-kant SDKs en de interne dienst van de levering van het Experience Platform een bevestiging dat een gebeurtenis met succes werd verzameld.

Als die bevestiging niet wordt ontvangen, teweegbrengen client-side SDKs of de interne dienst van de Levering van het Platform opnieuw, en de Gebeurtenis van de Ervaring wordt opnieuw verzonden.

Dit is de beste manier om fouten van voorbijgaande aard te verwerken. De bijwerking is de mogelijkheid om dubbele gebeurtenissen in te voeren.

Om beter te begrijpen beste praktijken voor de behandeling van voorbijgaande mislukkingen, zie dit artikel op [ voorbijgaande fout behandeling ](https://learn.microsoft.com/en-us/azure/architecture/best-practices/transient-faults).

## Gebeurtenisduplicatiescenario&#39;s {#scenarios}

Dubbele gebeurtenissen kunnen in verschillende scenario&#39;s voorkomen, zoals, maar niet beperkt tot:

* Netwerkgerelateerde problemen tussen client-side SDK&#39;s en de [!DNL Edge Network] . Deze kwesties kunnen uit de mislukkingen van Internet Service Provider, mobiel signaalverlies, of andere netwerkmislukkingen voortkomen, aangezien de connectiviteit tussen de klant en de Edge Network door openbaar Internet wordt gedaan.
* Gebeurtenissen voor automatisch schalen van interne Experience Platforms. Soms kunnen gegevens opnieuw in evenwicht worden gebracht vanwege de volatiliteit van de cloudinfrastructuur.

De Adobe Experience Platform-gegevensverzamelingslaag is ontworpen ter ondersteuning van verwerking &quot;minstens één keer&quot;. Daarom kan dubbel optreden in beperkte, zeldzame situaties.

Om meer over &quot;minstens één keer&quot;verwerking te leren, zie dit artikel op [ garanties van de berichtlevering ](https://docs.confluent.io/kafka/design/delivery-semantics.html).

## Opties voor deduplicatie van gebeurtenissen {#deduplication}

Voor bedrijfsscenario&#39;s die gevoelig zijn voor dubbele gebeurtenissen, gebruikt Experience Platform veelvoudige methodes van gebeurtenisdeduplicatie in zijn stroomafwaartse opslagsystemen, zoals hieronder beschreven.

* Real-Time CDP Profile store slaat gebeurtenissen over als er al een gebeurtenis met dezelfde `_id` in [!DNL Profile store] bestaat. Zie de documentatie op [ klasse XDM ExperienceEvent ](../xdm/classes/experienceevent.md) voor meer details.
* Customer Journey Analytics staat gebruikers toe om metrisch te vormen om waarden niet-herhalend slechts te tellen. Leren hoe te om dit te doen, zie de documentatie op [ metrische montages van de deduplicatiecomponent ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication.html?lang=en).
* De Dienst van de Vraag van het Experience Platform steunt gegevensdeduplicatie wanneer het wordt vereist om een volledige rij uit een berekening te verwijderen of een specifieke reeks gebieden te negeren omdat slechts een deel van de gegevens in de rij dubbele informatie is. Zie de documentatie rond [ gegevensdeduplicatie in de Dienst van de Vraag ](../query-service/key-concepts/deduplication.md) voor meer informatie.

>[!NOTE]
>
>Als u problemen ondervindt met het dupliceren van gebeurtenissen buiten de hierboven vermelde gebruiksgevallen, dient u contact op te nemen met uw Adobe en gedetailleerde informatie te verstrekken over uw gebruiksgeval.
