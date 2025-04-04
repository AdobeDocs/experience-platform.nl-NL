---
keywords: Experience Platform;home;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
solution: Experience Platform
title: Zelfbedieningsbronnen (Batch SDK) - Overzicht
description: Adobe Experience Platform Self-Serve Sources (Batch SDK) is een set configuratie-API's waarmee u een REST API-bron kunt integreren met behulp van de Flow Service API om uw gegevens naar Experience Platform te brengen.
exl-id: 5d5449ad-a1ba-402b-a281-0b2d8b704f32
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---

# Zelfbedieningsbronnen (Batch SDK) - overzicht

Adobe Experience Platform Self-Serve Sources (Batch SDK) is een kader dat u toestaat om een REST API-based bron aan de Experience Platform broncatalogus te integreren gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/). Self-Serve Sources (Batch SDK) beschikt over een set configuratie-API&#39;s om uw eigen bron te maken en uw batchgegevens naar Experience Platform te brengen.

Met Self-Serve Bronnen (Batch SDK) kunt u:

* Configureer en integreer een nieuwe bron met de API van [!DNL Flow Service] in de Experience Platform-catalogus.
* Definieer specificaties voor uw bron, inclusief informatie over ondersteunde verificatietypen en hoe brongegevens worden opgehaald.
* Maak gebruikersgerichte documentatie voor uw nieuwe bron.

De Self-Serve documentatie van Bronnen verstrekt instructies om, een REST API-Gebaseerde bronintegratie met Experience Platform te vormen te testen en vrij te geven, en uw bron te hebben deel van de alsmaar groeiende broncatalogus worden.

![ catalogus ](./assets/catalog.png)

## Bronnen begrijpen

Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens opnemen uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

Voor meer informatie over bronnen, en om een lijst van verschillende bronnen te zien die momenteel op Experience Platform worden gesteund, zie het [ overzicht van bronnen ](../home.md).

## Een bron maken

Via Self-Serve Sources kunt u uw eigen REST API-bron integreren en uw gegevens met [!DNL Flow Service] naar Experience Platform overbrengen. U kunt een bron integreren in de Experience Platform-broncatalogus door nieuwe verbindingsspecificaties te maken, te configureren en in te dienen via de [!DNL Flow Service] API.

Zie de gids bij [ het creëren van een nieuwe verbindingsspecificatie ](./api/api-overview.md) voor informatie over hoe te om een nieuwe bron aan Experience Platform te integreren.

## Uw bron documenteren

Zodra uw bron wordt gecreeerd, zie de [ documentatiegids ](./documentation/doc-overview.md) voor instructies op hoe te om uw bron door de [!DNL GitHub] Webinterface of door uw eigen tekstredacteur te documenteren.

## Proces op hoog niveau

Het stapsgewijze proces voor het configureren van uw bron in Experience Platform wordt hieronder beschreven:

* Lees de [ Zelf-Serve Bron (Partij SDK) API gids ](./api/api-overview.md).
   * Lees de [ begonnen gids ](./api/getting-started.md) worden.
   * Volg het leerprogramma op [ creërend een nieuwe verbindingsspecificatie ](./api/create.md).
   * Volg het leerprogramma bij [ het bijwerken van uw verbindingsspecificatie ](./api/update-connection-specs.md).
   * Volg het leerprogramma op [ toevoegend uw nieuwe identiteitskaart van de verbindingsspecificatie aan een stroomspecificatie ](./api/update-flow-specs.md)
   * [ legt uw nieuwe bron ](./api/submit.md) voor.
* Om een beter inzicht in de structuur en de eigenschappen van een verbindingsspecificatie te verkrijgen, lees de gids op [ configuratieopties voor Zelfbediening Bronnen (Partij SDK) ](./config/config.md).
   * Lees de gids op [ vormend uw authentificatiespecificaties ](./config/authspec.md) om een beter inzicht in de verschillende authentificatietypen te krijgen die u voor uw bron kunt gebruiken.
   * Lees de gids op [ vormend uw bronspecificaties ](./config/sourcespec.md) voor informatie over de verschillende pagineringstypes, het plannen van formaten, en douaneschema&#39;s die voor uw bron kunnen worden gevormd.
   * Lees de gids op [ vormend uw onderzoek specificaties ](./config/explorespec.md) voor informatie over hoe te om de parameters te bepalen die voor het onderzoeken van en het inspecteren van voorwerpen in uw bron worden vereist.
* Begin documenterend uw bron, lees het [ overzicht bij het creëren van documentatie voor Zelfbediening Bronnen ](./documentation/doc-overview.md)
   * U kunt dit [ bronAPI documentatiesjabloon ](./documentation/template.md) gebruiken om uw API documentatie te structureren.
   * U kunt dit [ bronUI documentatiemalplaatje ](./documentation/ui-template.md) gebruiken om uw documentatie te structureren UI.
   * Zie de gids op [ gebruikend de het Webinterface van GitHub ](./documentation/github.md) voor stappen op hoe te om documentatie tot stand te brengen die GitHub gebruikt.
   * Zie de gids op [ gebruikend een tekstredacteur ](./documentation/text-editor.md) voor stappen op hoe te om documentatie tot stand te brengen gebruikend uw lokale machine.
