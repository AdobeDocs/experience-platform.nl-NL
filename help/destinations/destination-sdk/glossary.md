---
solution: Experience Platform
title: Adobe Experience Platform Destination SDK glossary
description: Begrijp belangrijke terminologie wanneer het ontwerpen van een bestemming gebruikend Experience Platform Destination SDK.
exl-id: d65f390a-a980-49b8-9570-840f03534553
source-git-commit: 20427c4c8826905a77fac04d055d523b12a6f739
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 1%

---

# [!DNL Adobe Experience Platform] Destination SDK-woordenlijst

Zie deze verklarende woordenlijst voor definities van termen die in Destination SDK worden gebruikt. Voor andere [!DNL Adobe Experience Platform] termijnen, zie de [ verklarende woordenlijst van Experience Platform ](/help/landing/glossary.md).

## A {#a}

**Samenvoegingsbeleid**: Wanneer het vormen hoe de gegevens naar uw in real time het stromen bestemming zouden moeten worden uitgevoerd, kunt u bepalen hoe de profielgegevens alvorens worden verzonden naar uw bestemmingsplatform worden bijeengevoegd. Dit helpt gegevenslevering te optimaliseren door gegevensverslagen te groeperen die op specifieke criteria worden gebaseerd, de frequentie van API vraag te verminderen, en algemene efficiency te verbeteren. Het verschillende beleid kan worden gevormd om aan diverse bestemmingsvereisten te voldoen, die ervoor zorgen dat het gegeven op de meest efficiënte manier wordt verpakt en geleverd. [Meer informatie](/help/destinations/destination-sdk/functionality/destination-configuration/aggregation-policy.md).

**de meta-gegevensconfiguratie van het publiek**: Een configuratie van publieksmeta-gegevens verwijst naar de gestructureerde opstelling en de parameters die binnen [!DNL Adobe Experience Platform] worden bepaald die de programmatic verwezenlijking, het bijwerken, en de schrapping van publiekssegmenten in een gespecificeerde bestemming toelaten. Deze configuratie gebruikt publieksmeta-gegevensmalplaatjes om zich aan de specificaties van marketing API van het bestemmingsplatform te richten. Lees meer over de [ configuratie van publieksmeta-gegevens ](/help/destinations/destination-sdk/functionality/audience-metadata-management.md) en [ beschikbare macro&#39;s ](/help/destinations/destination-sdk/functionality/audience-metadata-management.md#macros).

## D {#d}

**eindpunt van de Configuratie van de Bestemming**: Een eindpunt van de bestemmingsconfiguratie in [!DNL Adobe Experience Platform], specifiek het `/authoring/destinations` API eindpunt, leidt tot, wint, werkt bij, en schrapt configuraties voor bestemmingen. Deze configuraties bepalen hoe gegevens van [!DNL Adobe Experience Platform] worden geleverd aan diverse externe systemen of bestemmingen, zoals marketingplatforms, cloudopslagservices of andere eindpunten voor gegevensverwerking. Lees meer over [ beschikbare configuratieopties ](/help/destinations/destination-sdk/functionality/configuration-options.md#destination-configuration) en bekijk de [ verwijzingsdocumentatie ](/help/destinations/destination-sdk/authoring-api/destination-configuration/create-destination-configuration.md).

**instantie van de Bestemming**: Een specifieke opstelling van een bestemmingsconfiguratie in [!DNL Adobe Experience Platform], die door Experience Platform UI wordt gecreeerd en wordt geleid. Het omvat alle noodzakelijke parameters en geloofsbrieven voor het verbinden van en het verzenden van gegevens naar de bestemming. Na het vestigen van de verbinding aan uw bestemming, kunt u bestemmingsidentiteitskaart krijgen wanneer [ doorbladerend een verbinding met uw bestemming ](/help/destinations/ui/destination-details-page.md).

![ beeld UI hoe te om identiteitskaart van de bestemmingsinstantie ](/help/destinations/destination-sdk/assets/testing-api/get-destination-instance-id.png) te krijgen

## P {#p}

**[!DNL Pebble]template**: een [!DNL Pebble] -sjabloon transformeert gegevens die zijn geëxporteerd van [!DNL Adobe Experience Platform] naar de indeling die is vereist voor het doelplatform. Hierbij wordt de sjabloontaal [!DNL Pebble] gebruikt, die dynamische gegevenstransformatie mogelijk maakt via functies zoals `filter` , `for` , `if` en `set` . [!DNL Adobe Experience Platform] bevat extra aangepaste functies zoals `addedSegments` en `removedSegments` . Deze malplaatjes helpen gegevenselementen, zoals timestamps en publiekslidmaatschappen formatteren, om aan de specificaties van de bestemming te voldoen. Leer meer [ hier ](/help/destinations/destination-sdk/functionality/destination-server/message-format.md) en [ hier ](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md).

**Privé bestemming**: De integratie van de Douane die door individuele [!DNL Adobe Experience Platform] klanten wordt gecreeerd. Deze zijn op specifieke bedrijfsbehoeften toegesneden en zijn slechts toegankelijk binnen de organisatie van de klant, die flexibiliteit in de configuraties van de gegevensuitvoer aanbieden. Privédoelen zijn alleen beschikbaar voor [!DNL Real-Time CDP] Ultimate-klanten. [Meer informatie](/help/destinations/destination-sdk/overview.md#productized-custom-integrations).

**Openbare bestemming**: Een openbaar beschikbare integratie in de [!DNL Adobe Experience Platform] catalogus. Deze bestemmingen worden gestandaardiseerd, van branding voorzien, en klantenopstelling vereenvoudigen door pre-gevormde parameters te verstrekken. Ze zijn toegankelijk voor alle klanten die [!DNL Adobe Experience Platform] gebruiken. [Meer informatie](/help/destinations/destination-sdk/overview.md#productized-custom-integrations).

## S {#s}

**Zelfbediening documentatiesjabloon**: Het zelfbedienings documentatiesjabloon verstrekt een gestructureerd formaat dat u kunt gebruiken om uw bestemming te documenteren. Het omvat secties voor een overzicht, gebruiksgevallen, eerste vereisten, gesteunde identiteiten, publiek, de uitvoertypes, en frequentie, evenals stappen voor het verbinden met de bestemming, het activeren van publiek, en kaartattributen. Gebruik dit malplaatje om uitvoerige en verenigbare documentatie te verzekeren, die klanten toestaan om snel aan de slag te gaan gebruikend uw bestemming en de verstrekte gebruiksgevallen te begrijpen. Lees meer over [ hoe te om uw bestemming ](/help/destinations/destination-sdk/docs-framework/documentation-instructions.md) te documenteren, [ download het recentste malplaatje van de zelfdienstdocumentatie ](/help/destinations/destination-sdk/assets/docs-framework/yourdestination-template.zip), en [ mening hoe het ](/help/destinations/destination-sdk/docs-framework/self-service-template.md) teruggeeft.

## T {#t}

**specs van het Malplaatje en het malplaatjestrategieën**: Sjabloonspecs zijn configuraties die worden gebruikt om de verzoeken van HTTP te formatteren die van [!DNL Adobe Experience Platform] naar een bestemming worden verzonden. Ze transformeren profielkenmerkvelden van het XDM-schema naar een indeling die door het doelplatform wordt ondersteund. Met behulp van een sjabloontaal die lijkt op [!DNL Jinja], zijn deze specificaties geschikt voor dynamische gegevenstransformaties op basis van specifieke regels en invoergegevens. [Meer info](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md).

**het Testen API**: Gebruik Testen API om uw bestemmingsconfiguraties te bevestigen alvorens een het publiceren verzoek voor te leggen. Het verstrekt hulpmiddelen om steekproefprofielen te produceren en de gegevensstroom te testen, die ervoor zorgen dat de configuratie de vereisten van de bestemming aanpast. De API ondersteunt zowel streaming als op bestanden gebaseerde (batch-) doelen en biedt een manier om gegevens te simuleren en mogelijke problemen in het installatieproces op te lossen. Lees meer over het testen API voor [ het stromen ](/help/destinations/destination-sdk/testing-api/streaming-destinations/streaming-destination-testing-overview.md) en [ op dossier-gebaseerde bestemmingen ](/help/destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md).

**het malplaatje van de Transformatie**: Een transformatiemalplaatje past gegevensformaat van het schema van Adobe XDM aan het verwachte formaat van de bestemming aan. [Meer info](/help/destinations/destination-sdk/functionality/destination-server/message-format.md).
