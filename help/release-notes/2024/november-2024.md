---
title: Opmerkingen bij de release van Adobe Experience Platform november 2024
description: In de release van november 2024 staat een opmerking voor Adobe Experience Platform.
exl-id: e3969f8b-70b2-40f8-bb9b-5be6e3d8f722
source-git-commit: f71fc1d4ad51af52046caeee289546e05967d5bd
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 29%

---

# Aanvullende informatie voor Adobe Experience Platform

>[!TIP]
>
>De nieuwe [ AI Hulp productdocumentatie ](../../ai-assistant/landing.md) is nu beschikbaar. Gebruik deze pagina als een hub voor alle aan AI Assistant gerelateerde bronnen.

**Releasedatum: woensdag 26 november 2024**

Updates van bestaande functies en documentatie in Adobe Experience Platform:

- [AI-assistent](#ai-assistant)
- [Bestemmingen](#destinations)
- [Query-service](#query-service)
- [Sandboxes](#sandboxes)
- [Documentatie-updates](#documentation-updates)
   - [Interactieve API-documentatie voor Experience Platform](#interactive-experience-platform-api-documentation)
   - [Nieuwe inhoudsopgave op Experience League](#new-table-of-contents-on-experience-league)
   - [Nieuwe bestemmingspagina van AI Assistant](#new-ai-assistant-landing-page)

## AI-assistent {#ai-assistant}

AI-assistent in Adobe Experience Platform is een gesprekservaring waarmee u uw workflows in Adobe-applicaties kunt versnellen. Met AI-assistent krijgt u meer inzicht in productkennis, kunt u problemen oplossen of informatie doorzoeken en operationele inzichten verkrijgen. AI-assistent biedt ondersteuning voor Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer en Customer Journey Analytics.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| [!BADGE  Alpha ] {type=Informative} Monitor significante veranderingen en voorspelde publieksgroei | Gebruik AI Assistant om significante wijzigingen te controleren en groeiprognoses voor uw publiek en gegevenssetformaten te maken. U kunt deze informatie dan gebruiken om de integriteit van uw publieksgegevens te verzekeren en toekomstgerichte prognoses aan te bieden om gegeven-geïnformeerde besluitvorming te steunen. Voor meer informatie, lees de gids over [ controle significante veranderingen en het voorspellen van publieksgroei ](../../ai-assistant/new-features/audience-forecasting.md). |
| [!BADGE  Alpha ] {type=Informatieve} Natuurlijke taalschatting | Gebruik de mogelijkheden voor het schatten van de natuurlijke taal van AI Assistant om publieksgrootten te ramen en publiekseigenschappen te voorspellen op basis van eenvoudige, conversationele vragen. Voor meer informatie, lees de gids op [ gebruikend natuurlijke taalschatting met AI Medewerker ](../../ai-assistant/new-features/natural-language.md). |

{style="table-layout:auto"}

## Bestemmingen {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte bestemmingen** {#new-updated-destinations}

| Bestemming | Beschrijving |
| --- | --- |
| [ Magnite die in real time stromen ](/help/destinations/catalog/advertising/magnite-streaming.md) | Exporteer soorten publiek voor activering, activering of onderdrukking in het Magnite Streaming-platform. Merk op dat voor publiek om correct naar Magnite worden uitgevoerd, u zowel de real time als de partijbestemmingen moet gebruiken. |
| [ Magnite die Batch stroomt ](/help/destinations/catalog/advertising/magnite-batch.md) | Exporteer soorten publiek voor activering, activering of onderdrukking in het Magnite Streaming-platform. Merk op dat voor publiek om correct naar Magnite worden uitgevoerd, u zowel de real time als de partijbestemmingen moet gebruiken. |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functie | Beschrijving |
| --- | --- |
| [ kijkt omhoog profielattributen in real time op de rand ](/help/destinations/ui/activate-edge-profile-lookup.md) | Leer hoe u Edge-profielkenmerken in real-time kunt opzoeken om verpersoonlijkingservaringen te bieden of besluitvormingsregels te informeren via downstreamtoepassingen, met behulp van de API voor aangepaste Personalization-doelen en -Edge Network. |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [overzicht van bestemmingen](../../destinations/home.md).

## Query-service {#query-service}

De gegevens van de vraag in het de gegevensmeer van Adobe Experience Platform gebruikend standaardSQL met de Dienst van de Vraag. Combineer naadloos datasets en produceer nieuwe degenen van uw vraagresultaten aan macht rapportering, laat de werkschema&#39;s van de gegevenswetenschap toe, of vergemakkelijkt opname in het Profiel van de Klant in real time. Bijvoorbeeld, kunt u de gegevens van de klantentransactie met gedragsgegevens samenvoegen om hoog-waardepubliek voor gerichte marketing campagnes te identificeren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Distiller-API voor gegevensverificatie | Beheer en handhaaf op IP-Gebaseerde toegangsbeperkingen voor de zanddozen van de Dienst van de Vraag, om gegevensveiligheid te verbeteren en naleving van organisatiebeleid te verzekeren. Verwijs naar de [ Vergunning API van Distiller van Gegevens gids ](../../query-service/auth-api/overview.md) voor meer informatie over zijn zeer belangrijke eigenschappen en mogelijkheden, of de [ documentatie OpenAPI ](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/) voor uitvoerige informatie met inbegrip van eindpuntdetails, parameterlijsten, verzoek/antwoordvoorbeelden, en testende mogelijkheden. |

Voor meer informatie over [!DNL Query Service], gelieve te zien het [[!DNL Query Service]  overzicht ](../../query-service/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform is ontworpen om digitale ervaringstoepassingen wereldwijd te verrijken. Bedrijven gebruiken vaak meerdere digitale ervaringstoepassingen parallel en moeten de ontwikkeling, het testen en de implementatie van deze toepassingen verzorgen en tegelijkertijd de operationele naleving waarborgen. Om aan deze behoefte te voldoen, biedt Experience Platform sandboxes die één Platform-instantie opsplitsen in afzonderlijke virtuele omgevingen, zodat digitale ervaringstoepassingen kunnen worden ontwikkeld en verder ontwikkeld.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Delen van pakketten met de API voor gereedschappen van de sandbox | Gebruik twee nieuwe API-eindpunten [`/handshake`](../../sandboxes/sandbox-tooling-api/packages.md#org-linking) en [`/transfers`](../../sandboxes/sandbox-tooling-api/packages.md#transfer-packages) om het delen van pakketten tussen organisaties, zoals goedkeuringen aanvragen, zichtbaarheid van pakketten en importpakketten, af te handelen met behulp van de API voor gereedschappen voor de sandbox. |

Voor meer informatie over sandboxes, raadpleegt u het [ overzicht van sandboxes](../../sandboxes/home.md).

## Documentatie-updates {#documentation-updates}

### Interactieve API-documentatie voor Experience Platform {#interactive-api-documentation}

De [ Experience Platform API documentatie ](https://developer.adobe.com/experience-platform-apis/) is nu volledig interactief, toestaand u om APIs op de pagina van de API verwijzingsdocumentatie voor authentiek te verklaren en te onderzoeken. U kunt nu naar de gewenste pagina met API-referentiedocumentatie gaan, uw API-verificatiereferenties maken of ophalen, deze in het **[!UICONTROL Try it]** -blok plakken en de aanroep uitvoeren. Alles op één pagina. [ las meer ](/help/landing/api-authentication.md#get-credentials-functionality) over de functionaliteit.

### Nieuwe inhoudsopgave op Experience League {#new-table-of-contents-on-experience-league}

De inhoudsopgave op documentatiepagina&#39;s van het Experience League is verbeterd en biedt lezers nu een verbeterde ervaring, waaronder een trefwoordfilter waarmee u precies de gewenste pagina kunt vinden, waarmee u alle pagina&#39;s kunt uitvouwen en nog veel meer. <br> ![ de Nieuwe ervaring van de inhoudstafel met inbegrip van sleutelwoordfilter en capaciteit om alle pagina&#39;s uit te breiden.](../2024/assets/november/new-toc-experience.gif " Nieuwe de ervaring van de inhoudstafel met inbegrip van sleutelwoordfilter en capaciteit om alle pagina&#39;s uit te breiden."){width="250" align="center" zoomable="yes"}

### Nieuwe bestemmingspagina van AI Assistant {#new-ai-assistant-landing-page}

Gebruik de nieuwe [ AI Hulp pagina van het productdocumentatie ](../../ai-assistant/landing.md) als hub voor alle dingen AI Medewerker. Raadpleeg de productdocumentatie voor videozelfstudies, technische documentatie, gebruiksgevallen en koppelingen naar blogberichten over AI Assistant.
