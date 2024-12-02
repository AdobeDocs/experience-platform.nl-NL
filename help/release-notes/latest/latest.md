---
title: Aanvullende informatie voor Adobe Experience Platform, november 2024
description: Aanvullende informatie voor Adobe Experience platform, november 2024.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 3f43e120225bcca640cc46ebdce1e4d61100ad45
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 98%

---

# Aanvullende informatie voor Adobe Experience Platform

>[!TIP]
>
>De nieuwe [ AI Hulp productdocumentatie ](../../ai-assistant/landing.md) is nu beschikbaar. Gebruik deze pagina als een hub voor alle aan AI-assistent gerelateerde bronnen.

**Releasedatum: woensdag 26 november 2024**

Updates van bestaande functies en documentatie in Adobe Experience Platform:

- [AI-assistent](#ai-assistant)
- [Bestemmingen](#destinations)
- [Query-service](#query-service)
- [Sandboxes](#sandboxes)
- [Documentatie-updates](#documentation-updates)
   - [Interactieve API-documentatie voor Experience Platform](#interactive-experience-platform-api-documentation)
   - [Nieuwe inhoudstabel voor Experience League](#new-table-of-contents-on-experience-league)
   - [Nieuwe landingspagina van AI-assistent](#new-ai-assistant-landing-page)

## AI-assistent {#ai-assistant}

AI-assistent in Adobe Experience Platform is een gesprekservaring waarmee u uw workflows in Adobe-applicaties kunt versnellen. Met AI-assistent krijgt u meer inzicht in productkennis, kunt u problemen oplossen of informatie doorzoeken en operationele inzichten verkrijgen. AI-assistent biedt ondersteuning voor Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer en Customer Journey Analytics.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| [!BADGE Alpha]{type=Informative} Significante veranderingen en prognose voor de groei van de doelgroep bewaken | Gebruik AI-assistent om significante wijzigingen te controleren en groeiprognoses voor uw doelgroep en datasetformaten te zien. U kunt deze informatie vervolgens gebruiken om de integriteit van uw doelgroepgegevens te waarborgen en toekomstgerichte projecties te bieden om besluitvorming op basis van gegevens te ondersteunen. Lees voor meer informatie de handleiding over [controle van significante veranderingen en het voorspellen van de groei van de doelgroep](../../ai-assistant/new-features/audience-forecasting.md). |
| [!BADGE Alpha]{type=Informative} Inschatting natuurlijke taal | Gebruik de mogelijkheden voor inschatting van de natuurlijke taal van de AI-assistent om de omvang van doelgroepen te schatten en de geneigdheid van doelgroepen te voorspellen op basis van eenvoudige gespreksvragen. Lees voor meer informatie de handleiding over [inschatting van de natuurlijke taal door van AI-assistent gebruiken](../../ai-assistant/new-features/natural-language.md). |

{style="table-layout:auto"}

## Bestemmingen {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte bestemmingen** {#new-updated-destinations}

| Bestemming | Beschrijving |
| --- | --- |
| [Magnite Streaming Real-Time](/help/destinations/catalog/advertising/magnite-streaming.md) | Exporteer doelgroepen voor activering, targeting of onderdrukking in het Magnite Streaming-platform. Houd er rekening mee dat u voor correcte export van doelgroepen naar Magnite zowel de realtime- als de batchbestemmingen moet gebruiken. |
| [Magnite Streaming-batch](/help/destinations/catalog/advertising/magnite-batch.md) | Exporteer doelgroepen voor activering, targeting of onderdrukking in het Magnite Streaming-platform. Houd er rekening mee dat u voor correcte export van doelgroepen naar Magnite zowel de realtime- als de batchbestemmingen moet gebruiken. |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functie | Beschrijving |
| --- | --- |
| [Profielkenmerken in real time opzoeken in Edge](/help/destinations/ui/activate-edge-profile-lookup.md) | Leer hoe u in real time profielkenmerken in kunt opzoeken in Edge om personalisatie-eraringen te bieden of besluitvormingsregels te informeren via downstreamtoepassingen, met behulp van de API voor aangepaste personalisatiebestemming en Edge Network. |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [overzicht van bestemmingen](../../destinations/home.md).

## Query-service {#query-service}

Voer query&#39;s uit op gegevens in het Adobe Experience Platform-data lake met behulp van standaard SQL met Query Service. Combineer naadloos datasets en genereer nieuwe op basis van de queryresultaten om rapportage, datawetenschapworkflows of opname in het realtimeklantprofiel mogelijk te maken. U kunt bijvoorbeeld de gegevens van de klantentransactie samenvoegen met de gedragsgegevens om hoogwaardige doelgroepen te identificeren voor gerichte marketingcampagnes.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Dater Distiller Authorization-API | Beheer en forceer IP-gebaseerde toegangsbeperkingen voor Query Service-sandboxes om de gegevensbeveiliging te verbeteren en naleving van het organisatiebeleid te garanderen. Raadpleeg de [Data Distiller Authorization API-handleiding](../../query-service/auth-api/overview.md) voor meer informatie over de belangrijkste functies en mogelijkheden, of de [OpenAPI-documentatie](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/) voor uitgebreide informatie, waaronder eindpuntdetails, parameterlijsten, aanvraag-/reactievoorbeelden en testmogelijkheden. |

Voor meer informatie over [!DNL Query Service] raadpleegt u het [[!DNL Query Service] overzicht](../../query-service/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform is ontworpen om digitale ervaringstoepassingen wereldwijd te verrijken. Bedrijven gebruiken vaak meerdere digitale ervaringstoepassingen parallel en moeten de ontwikkeling, het testen en de implementatie van deze toepassingen verzorgen en tegelijkertijd de operationele naleving waarborgen. Om aan deze behoefte te voldoen, biedt Experience Platform sandboxes die één Platform-instantie opsplitsen in afzonderlijke virtuele omgevingen, zodat digitale ervaringstoepassingen kunnen worden ontwikkeld en verder ontwikkeld.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Pakket delen in de sandboxtool-API | Gebruik twee nieuwe API-eindpunten, [`/handshake`](../../sandboxes/sandbox-tooling-api/packages.md#org-linking) en [`/transfers`](../../sandboxes/sandbox-tooling-api/packages.md#transfer-packages), voor het delen van pakketten tussen organisaties, zoals goedkeuring van aanvragen, zichtbaarheid van pakketten en het importeren van pakketten, met behulp van de sandboxtool-API. |

Voor meer informatie over sandboxes raadpleegt u het [overzicht van sandboxes](../../sandboxes/home.md).

## Documentatie-updates {#documentation-updates}

### Interactieve API-documentatie voor Experience Platform {#interactive-api-documentation}

De [Experience Platform API-documentatie](https://developer.adobe.com/experience-platform-apis/) is nu volledig interactief, zodat u API&#39;s rechtstreeks op de API-referentiedocumentatiepagina kunt verifiëren en verkennen. U kunt nu naar de gewenste API-referentiedocumentatiepagina gaan, uw API-verificatiegegevens maken of ophalen, deze in het blok **[!UICONTROL Try it]** plakken en de oproep uitvoeren. Alles op één pagina. [Meer informatie](/help/landing/api-authentication.md#get-credentials-functionality) over de nieuwe functionaliteit.

### Nieuwe inhoudstabel voor Experience League {#new-table-of-contents-on-experience-league}

De inhoudsopgave op de documentatiepagina&#39;s van Experience League is verbeterd voor een betere ervaring voor lezers, inclusief een trefwoordfilter om de exacte pagina te vinden die u nodig hebt, de mogelijkheid om alle pagina&#39;s uit te vouwen en meer. <br> ![Nieuwe inhoudsopgave-ervaring met trefwoordfilter en de mogelijkheid om alle pagina&#39;s uit te vouwen.](../2024/assets/november/new-toc-experience.gif "Nieuwe inhoudsopgave-ervaring met trefwoordfilter en de mogelijkheid om alle pagina&#39;s uit te vouwen."){width="250" align="center" zoomable="yes"}

### Nieuwe landingspagina van AI-assistent {#new-ai-assistant-landing-page}

Gebruik de nieuwe pagina met [AI-assistent-productdocumentatie](../../ai-assistant/landing.md) als centrale plek voor alles over AI-assistent. Raadpleeg de productdocumentatie voor videotutorials, technische documentatie, gebruiksscenario&#39;s en koppelingen naar blogberichten over AI-assistent.