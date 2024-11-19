---
keywords: Experience Platform;startpagina;populaire onderwerpen
solution: Experience Platform
title: Overzicht van beheer, privacy en beveiliging
description: Adobe Experience Platform biedt verschillende services en tools waarmee u uw verzamelde ervaringsgegevens op een betrouwbare manier kunt beheren, zodat u aan uw bedrijfspraktijken, wettelijke verplichtingen en ontwikkelingsproces kunt voldoen.
feature: Data Governance,Privacy
exl-id: 1ab5a436-c5dd-4e7a-aba1-549f0613f224
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 2%

---

# Bestuur, privacy en beveiliging in Adobe Experience Platform

Met Adobe Experience Platform kunt u uw gegevens invoeren, analyseren, optimaliseren en in actie brengen om de ervaringen van klanten aanzienlijk te verbeteren. Deze gegevens zijn enorm, complex en ongelooflijk waardevol. Afhankelijk van de aard van uw gegevensverrichtingen, de wettelijke jurisdicties uw bedrijf onder, en uw organisatiebeleid betreffende gegevensgebruik werkt, moet u zorgvuldig de inzameling en het gebruik van de gegevens van de klantenervaring controleren en controleren om uw bedrijfsbelangen te beschermen.

Experience Platform biedt verschillende services en tools waarmee u uw verzamelde ervaringsgegevens op een betrouwbare manier kunt beheren om te voldoen aan uw bedrijfspraktijken, wettelijke verplichtingen en ontwikkelingsprocessen. In de volgende secties wordt een inleiding gegeven op elk van deze diensten, samen met koppelingen naar documentatie voor meer informatie.

De diensten kunnen in drie domeinen worden gecategoriseerd:

* [Datagovernance](#governance)
* [Privacy](#privacy)
* [Beveiliging](#security)

## Datagovernance {#governance}

Het beheer van gegevens is een essentieel begrip dat met elke mogelijkheid in Experience Platform wordt verweven. Het beheer van gegevens vertegenwoordigt uw vermogen om uw gegevens door zijn reis door Platform te controleren en te begrijpen. Dit omvat het handhaven van gegevenskwaliteit, gegevenslijn, gegevens het catalogiseren, en meer.

### Adobe Experience Platform Data Governance {#data-governance}

Als platformservice kunt u met Adobe Experience Platform Data Governance klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op het gebruik van gegevens worden nageleefd. Het speelt een belangrijke rol binnen Experience Platform op diverse niveaus, met inbegrip van het etiketteren van het gegevensgebruik, het beleid van het gegevensgebruik, beleidshandhaving, en gegevenslijn.

Zie het [ overzicht van het Beleid van Gegevens ](../../data-governance/home.md) voor meer informatie.

### Catalogus en gegevenssets {#catalog}

Catalogusservice is het systeem voor het opnemen van gegevens voor de locatie en de verbinding binnen het platform. Terwijl alle gegevens die in Experience Platform worden opgenomen in het meer van Gegevens als dossiers en folders worden opgeslagen, houdt de Catalogus de meta-gegevens en de beschrijving van die dossiers en folders voor raadpleging en controledoeleinden.

De catalogus organiseert ingebedde gegevens in datasets, met elke dataset die meta-gegevens bevat die kunnen worden gebruikt om de gegevens te etiketteren en te categoriseren het bevat.

Zie het [ overzicht van de Dienst van de Catalogus ](../../catalog/home.md) voor meer informatie over de dienst. Leren hoe te om datasets in Experience Platform te beheren, zie het [ overzicht van datasets ](../../catalog/datasets/overview.md).

## Privacy {#privacy}

Privacy is een essentieel probleem voor uw bedrijf, wetgevers en uw klanten. Aangezien de persoonlijke gegevens die van uw klanten worden verzameld de kern van bijna alle werkschema&#39;s van het Experience Platform vormen, verleent het Platform de diensten om deze initiatieven te steunen.

### Adobe Experience Platform Privacy Service {#privacy-service}

Wettelijke privacyregels zoals de Algemene Verordening van de Europese Unie inzake gegevensbescherming (GDPR) en de California Consumer Privacy Act (CCPA) verlenen burgers binnen hun rechtsgebied het recht om toegang te krijgen tot en de persoonsgegevens te verwijderen die u van hen verzamelt en opslaat.

Adobe Experience Platform Privacy Service biedt een RESTful-API en -gebruikersinterface waarmee u deze aanvragen kunt beheren. Met Privacy Service kunt u verzoeken indienen om toegang te krijgen tot of persoonlijke klantgegevens te verwijderen uit Adobe Experience Cloud-toepassingen, waardoor u gemakkelijker kunt voldoen aan wettelijke en organisatorische privacyregels.

Zie het [ overzicht van de Privacy Service ](../../privacy-service/home.md) voor meer informatie.

### Conceptverwerking {#consent}

Veel wettelijke privacyverordeningen hebben vereisten ingevoerd voor actieve en specifieke toestemming op het gebied van gegevensverzameling, personalisatie en andere gevallen van marketinggebruik. Om aan deze vereisten te voldoen, staat het Experience Platform u toe om toestemmingsinformatie in individuele klantenprofielen te vangen en die voorkeur te gebruiken als bepalende factor in hoe de gegevens van elke klant in stroomafwaartse workflows van het Platform worden gebruikt.

Leren hoe te om klantentoestemming en voorkeursgegevens te verwerken gebruikend de norm van de Adobe, zie het overzicht over [ toestemmingsverwerking in Experience Platform ](./consent/adobe/overview.md).

Voor informatie over hoe de gegevens van de de toestemmingen van de procesklant in overeenstemming met IAB Transparantie en het Kader van de Toestemming (TCF) 2.0, het overzicht over [ IAB TCF 2.0 steun in Platform ](./consent/iab/overview.md) zien.

## Beveiliging {#security}

De integriteit en veiligheid van uw gegevens zijn onmisbaar voor uw bedrijf, en dit risico vereist industrie-leidende veiligheidsmogelijkheden. Om deze uitdaging het hoofd te bieden, biedt Platform verschillende tools om uw gegevensbewerkingen beter te beveiligen.

### Gegevenscodering

Alle gegevens van het Platform worden gecodeerd in doorvoer en in rust. Zie het document over [ gegevensencryptie in Platform ](./encryption.md) voor meer informatie.

### Toegangsbeheer {#access-control}

Experience Platform gebruikt de Adobe Admin Console om op rol-gebaseerde toegangscontrole aan diverse mogelijkheden van het Platform te verstrekken. Deze functionaliteit gebruikt productprofielen in Admin Console, die gebruikers met toestemmingen en zandbakken verbinden.

Zie het [ overzicht van de toegangscontrole ](../../access-control/home.md) voor meer informatie.

### Sandboxes {#sandboxes}

Experience Platform is ontworpen om toepassingen voor digitale beleving wereldwijd te verrijken. Bedrijven voeren vaak meerdere digitale-ervaringstoepassingen parallel uit en moeten rekening houden met de ontwikkeling, het testen en de implementatie van deze toepassingen en tegelijk de operationele compatibiliteit garanderen.

Om aan de behoefte aan ontwikkelingsflexibiliteit te voldoen, verstrekt het Experience Platform zandbakken die één enkele instantie van het Platform in afzonderlijke virtuele milieu&#39;s verdelen om u te helpen uw digitale ervaringstoepassingen ontwikkelen die op uw eigen ontwikkelingscyclus worden gebaseerd.

Zie het [sandboxoverzicht](../../sandboxes/home.md) voor meer informatie.

## Volgende stappen

In dit document wordt een overzicht gegeven van de verschillende platformservices en -instrumenten die betrokken zijn bij gegevensbeheer, privacy en beveiliging. Raadpleeg de documentatie in deze handleiding voor meer informatie over deze mogelijkheden.
