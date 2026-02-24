---
title: Overzicht van geavanceerd gegevenslevenscyclusbeheer
description: Met Advanced Data Lifecycle Management kunt u de levenscyclus van uw gegevens beheren door verouderde of onjuiste gegevens bij te werken of te wissen.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: fc71e61fd33fe216f8cd326b9df048958c07077a
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---

# Advanced Data Lifecycle Management in Adobe Experience Platform

Adobe Experience Platform biedt een robuuste set hulpmiddelen voor het beheer van grote, gecompliceerde gegevensbewerkingen om de ervaringen van de consument te kunnen indelen. Aangezien het gegeven in tijd in het systeem wordt opgenomen, wordt het steeds belangrijker om uw gegevensopslag te beheren zodat de gegevens zoals verwacht worden gebruikt, wordt bijgewerkt wanneer de onjuiste gegevens moeten verbeteren, en wordt geschrapt wanneer het organisatorische beleid het noodzakelijk acht.

Deze activiteiten kunnen worden uitgevoerd gebruikend de [[!UICONTROL Data Lifecycle] werkruimte UI &#x200B;](#ui) of [&#x200B; Hygiene API van Gegevens &#x200B;](#api). Wanneer een gegevenslevenscyclusbaan uitvoert, verstrekt het systeem transparantie updates bij elke stap van proces. Zie de sectie op [&#x200B; chronologie en transparantie &#x200B;](#timelines-and-transparency) voor meer informatie over hoe elk baantype in het systeem wordt vertegenwoordigd.

>[!NOTE]
>
>Het geavanceerde Beheer van de Levenscyclus van Gegevens steunt datasetschrappingen door het [&#x200B; eindpunt van de gegevenssetvervalsing &#x200B;](./api/dataset-expiration.md) en identiteitskaart schrappingen (rij-vlakke gegevens) gebruikend primaire identiteiten via het [&#x200B; werkordeeindpunt &#x200B;](./api/workorder.md). U kunt [&#x200B; datasetvervalingen &#x200B;](./ui/dataset-expiration.md) en [&#x200B; verslagschrappingen &#x200B;](./ui/record-delete.md) door Experience Platform UI ook beheren. Raadpleeg de gekoppelde documentatie voor meer informatie. Merk op dat de Levenscyclus van Gegevens geen partijschrapping steunt.

## [!UICONTROL Data Lifecycle] UI-werkruimte {#ui}

Met de werkruimte van [!UICONTROL Data Lifecycle] in de gebruikersinterface van Experience Platform kunt u bewerkingen tijdens de gegevenslevenscyclus configureren en plannen, zodat u zeker weet dat uw records op de verwachte manier worden onderhouden.

Voor gedetailleerde stappen bij het beheren van de taken van de gegevenslevenscyclus in UI, zie de [&#x200B; gids UI van de gegevenslevenscyclus &#x200B;](./ui/overview.md).

## API voor gegevenshygiëne {#api}

De gebruikersinterface van [!UICONTROL Data Lifecycle] is gebaseerd op de API voor gegevenshygiëne, waarvan de eindpunten direct beschikbaar zijn voor u als u uw activiteiten tijdens de levenscyclus van gegevens liever wilt automatiseren. Zie de [&#x200B; gids van de Hygiëne API van Gegevens &#x200B;](./api/overview.md) voor meer informatie.

## Tijdlijnen en transparantie {#timelines-and-transparency}

[&#x200B; schrapt het Verslag &#x200B;](./ui/record-delete.md) en de verzoeken van de datasetvervalsing elk hun eigen verwerkingschronologie hebben en transparantie updates op zeer belangrijke punten in hun respectieve werkschema&#39;s verstrekken.

>[!TIP]
>
>Om uw huidig gebruik tegen quotagrenzen te controleren, zie de [&#x200B; gids van de de verwijzingsverwijzing van de Quota &#x200B;](./api/quota.md).\
>Voor betitelingsregels, maandelijkse kappen, de chronologie van SLA, en uitzondering behandelend beleid, zie het [&#x200B; Verslag schrapt (UI) &#x200B;](./ui/record-delete.md#quotas) en [&#x200B; Werkorder (API) &#x200B;](./api/workorder.md#quotas) documentatie.

Het volgende vindt plaats wanneer het verzoek van de a [&#x200B; datasetvervaldatum &#x200B;](./ui/dataset-expiration.md) wordt gecreeerd:

| Stadium | Tijd na geplande vervaldatum | Beschrijving |
| --- | --- | --- |
| Verzoek is ingediend | 0 uur | Een gegevensbeheerder of privacyanalist dient een verzoek in om een dataset op een bepaald tijdstip te laten verlopen. Het verzoek is zichtbaar in [!UICONTROL Data Lifecycle UI] nadat het is ingediend en blijft in behandeling tot de geplande vervaltijd, waarna het verzoek zal uitvoeren. |
| Dataset wordt verwijderd uit datumpigment | 1 uur | De dataset wordt gelaten vallen van de [&#x200B; pagina van de datasetinventaris &#x200B;](../catalog/datasets/user-guide.md) in UI. De gegevens in het datumpeer worden slechts zachte geschrapt, en zullen zo tot het eind van het proces blijven, waarna het hard zal worden geschrapt. |
| Gegevensset wordt verwijderd uit profielservice | 3 uur | Vanaf dit punt, zullen de verrichtingen met inbegrip van partij en het stromen segmentatie, voorproef of raming, de uitvoer, en entiteittoegang niet meer gegevens van deze dataset lezen. De gegevens binnen de profielservice worden alleen op de elektronische manier verwijderd en blijven geldig tot het einde van het proces, waarna de gegevens worden verwijderd. |
| Aantal profielen en publiek bijgewerkt | 48 uur | Zodra alle beïnvloede profielen worden bijgewerkt, worden alle verwante [&#x200B; publiek &#x200B;](../segmentation/home.md) bijgewerkt om op hun nieuwe grootte te wijzen. Afhankelijk van de dataset die werd verwijderd en de attributen die u op segmenteert, kon de grootte van elk publiek wegens de schrapping stijgen of verminderen. Op dit punt worden om het even welke resulterende veranderingen in algemene profieltellingen weerspiegeld in [&#x200B; dashboard widgets &#x200B;](../dashboards/guides/profiles.md#profile-count-trend) en andere rapporten. |
| Reizen en bestemmingen bijgewerkt | 50 uur | [&#x200B; de Reizen &#x200B;](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html?lang=nl-NL), [&#x200B; campagnes &#x200B;](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html?lang=nl-NL), en [&#x200B; bestemmingen &#x200B;](../destinations/home.md) worden bijgewerkt volgens veranderingen in verwante segmenten. |
| Harde verwijdering voltooid | 15 dagen | Alle gegevens met betrekking tot de dataset zijn hard geschrapt van de gegevens meer en profieldienst. De [&#x200B; status van de baan van de gegevenslevenscyclus &#x200B;](./ui/browse.md#view-details) die de dataset schrapte wordt bijgewerkt om dit te weerspiegelen. |

{style="table-layout:auto"}

## Volgende stappen

Dit document biedt een overzicht van de mogelijkheden van de Experience Platform-levenscyclus van gegevens. Om begonnen te worden het maken van verzoeken van de gegevenshygiëne in UI, verwijs naar de [&#x200B; gids UI &#x200B;](./ui/overview.md). Leren hoe te om de banen van de Levenscyclus van Gegevens te creëren programmatically, naar de [&#x200B; gids van de Hygiëne API van Gegevens &#x200B;](./api/overview.md) verwijzen
