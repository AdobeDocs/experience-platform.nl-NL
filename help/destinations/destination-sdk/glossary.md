---
solution: Experience Platform
title: Woordenlijst Adobe Experience Platform Destination SDK
description: Begrijp belangrijke terminologie wanneer het ontwerpen van een bestemming gebruikend Destination SDK van het Experience Platform.
source-git-commit: 3dae91fbe46dc3e23c6ac0cfb10c25ac8473876a
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 0%

---


# Woordenlijst Adobe Experience Platform Destination SDK

Zie deze woordenlijst voor definities van termen die in Destination SDK worden gebruikt. Raadpleeg voor andere Adobe Experience Platform-termen de [Woordenlijst Experience Platform](/help/landing/glossary.md).

## A

**Samenvoegingsbeleid**: Wanneer het vormen hoe de gegevens naar uw in real time het stromen bestemming zouden moeten worden uitgevoerd, kunt u bepalen hoe de profielgegevens alvorens wordt verzonden naar uw bestemmingsplatform worden samengevoegd. Dit helpt gegevenslevering te optimaliseren door gegevensverslagen te groeperen die op specifieke criteria worden gebaseerd, de frequentie van API vraag te verminderen, en algemene efficiency te verbeteren. Het verschillende beleid kan worden gevormd om aan diverse bestemmingsvereisten te voldoen, die ervoor zorgen dat het gegeven op de meest efficiënte manier wordt verpakt en geleverd. [Meer informatie](/help/destinations/destination-sdk/functionality/destination-configuration/aggregation-policy.md).

**Configuratie van metagegevens voor publiek**: Een configuratie van publieksmeta-gegevens verwijst naar de gestructureerde opstelling en parameters die binnen Adobe Experience Platform worden bepaald die de programmatic verwezenlijking, het bijwerken, en de schrapping van publiekssegmenten in een gespecificeerde bestemming toelaten. Deze configuratie gebruikt publieksmeta-gegevensmalplaatjes om zich aan de specificaties van marketing API van het bestemmingsplatform te richten. Meer informatie over de [doelmetagegevensconfiguratie](/help/destinations/destination-sdk/functionality/audience-metadata-management.md) en [beschikbare macro&#39;s](/help/destinations/destination-sdk/functionality/audience-metadata-management.md#macros).

## D

**Het eindpunt van de bestemmingsconfiguratie**: Een eindpunt van de bestemmingsconfiguratie in Adobe Experience Platform, specifiek `/authoring/destinations` API eindpunt, wordt gebruikt om configuraties voor bestemmingen tot stand te brengen, terug te winnen, bij te werken en te schrappen. Deze configuraties bepalen hoe gegevens van Adobe Experience Platform worden geleverd aan verschillende externe systemen of bestemmingen, zoals marketingplatforms, cloudopslagservices of andere eindpunten voor gegevensverwerking. Meer informatie over [beschikbare configuratieopties](/help/destinations/destination-sdk/functionality/configuration-options.md#destination-configuration) en bekijk de [referentiedocumentatie](/help/destinations/destination-sdk/authoring-api/destination-configuration/create-destination-configuration.md).

**Bestemmingsinstantie**: Een specifieke opstelling van een bestemmingsconfiguratie in Adobe Experience Platform, die door het Experience Platform UI wordt gecreeerd en wordt geleid. Het omvat alle noodzakelijke parameters en geloofsbrieven voor het verbinden van en het verzenden van gegevens naar de bestemming. Na het vestigen van de verbinding aan uw bestemming kunt u bestemmingsidentiteitskaart krijgen wanneer [bladeren door een verbinding met uw bestemming](/help/destinations/ui/destination-details-page.md).

![UI-afbeelding voor het ophalen van bestemmings-ID](/help/destinations/destination-sdk/assets/testing-api/get-destination-instance-id.png)

## P

**[!DNL Pebble]template**: A [!DNL Pebble] sjabloon wordt gebruikt om uit Adobe Experience Platform geëxporteerde gegevens om te zetten in de indeling die door het doelplatform wordt vereist. Het gebruikt de [!DNL Pebble] sjabloontaal, waarmee dynamische gegevenstransformatie mogelijk is via functies zoals `filter`, `for`, `if`, en `set`. Adobe Experience Platform bevat extra aangepaste functies zoals `addedSegments` en `removedSegments`. Deze malplaatjes helpen gegevenselementen, zoals timestamps en publiekslidmaatschappen formatteren, om aan de specificaties van de bestemming te voldoen. Meer informatie [hier](/help/destinations/destination-sdk/functionality/destination-server/message-format.md) en [hier](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md).

**Privébestemming**: Aangepaste integratie gemaakt door individuele Adobe Experience Platform-klanten. Deze zijn op specifieke bedrijfsbehoeften toegesneden en zijn slechts toegankelijk binnen de organisatie van de klant, die flexibiliteit in de configuraties van de gegevensuitvoer aanbieden. Privébestemmingen zijn alleen beschikbaar voor Real-Time CDP Ultimate-klanten. [Meer informatie](/help/destinations/destination-sdk/overview.md#productized-custom-integrations).

**Openbare bestemming**: Een openbaar beschikbare integratie in de Adobe Experience Platform-catalogus. Deze bestemmingen worden gestandaardiseerd, van branding voorzien, en klantenopstelling vereenvoudigen door pre-gevormde parameters te verstrekken. Ze zijn toegankelijk voor alle klanten die Adobe Experience Platform gebruiken. [Meer informatie](/help/destinations/destination-sdk/overview.md#productized-custom-integrations).

## S

**Zelfbediening documentatiesjabloon**: De zelfbedieningsdocumentatiesjabloon biedt een gestructureerde indeling waarmee u uw doel kunt documenteren. Het omvat secties voor een overzicht, gebruiksgevallen, eerste vereisten, gesteunde identiteiten, publiek, de uitvoertypes, en frequentie, evenals stappen voor het verbinden met de bestemming, het activeren van publiek, en kaartattributen. Gebruik dit malplaatje om uitvoerige en verenigbare documentatie te verzekeren, die klanten toestaan om snel aan de slag te gaan gebruikend uw bestemming en de verstrekte gebruiksgevallen te begrijpen. Meer informatie over [het documenteren van uw bestemming](/help/destinations/destination-sdk/docs-framework/documentation-instructions.md), [download het recentste zelf-dienst documentatiesjabloon](/help/destinations/destination-sdk/assets/docs-framework/yourdestination-template.zip), en [bekijken hoe het rendert](/help/destinations/destination-sdk/docs-framework/self-service-template.md).

## T

**Sjabloonspecificaties en sjabloonstrategieën**: Sjabloonspecificaties zijn configuraties die worden gebruikt om HTTP-aanvragen op te maken die van Adobe Experience Platform naar een bestemming worden verzonden. Ze transformeren profielkenmerkvelden van het XDM-schema naar een indeling die door het doelplatform wordt ondersteund. Een sjabloontaal gebruiken die lijkt op [!DNL Jinja]Deze specificaties maken echter dynamische gegevenstransformaties mogelijk op basis van specifieke regels en invoergegevens. [Meer informatie](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md).

**Testen, API**: Met de API voor testen kunt u uw doelconfiguraties valideren voordat u een publicatieverzoek indient. Het verstrekt hulpmiddelen om steekproefprofielen te produceren en de gegevensstroom te testen, die ervoor zorgen dat de configuratie de vereisten van de bestemming aanpast. De API ondersteunt zowel streaming als op bestanden gebaseerde (batch-) doelen en biedt een manier om gegevens te simuleren en mogelijke problemen in het installatieproces op te lossen. Meer informatie over de test-API voor [streaming](/help/destinations/destination-sdk/testing-api/streaming-destinations/streaming-destination-testing-overview.md) en [bestandsgebaseerde doelen](/help/destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md).

**Transformatiesjabloon**: Een transformatiesjabloon past de gegevensindeling aan van het Adobe-XDM-schema naar de verwachte indeling van de bestemming. [Meer informatie](/help/destinations/destination-sdk/functionality/destination-server/message-format.md).