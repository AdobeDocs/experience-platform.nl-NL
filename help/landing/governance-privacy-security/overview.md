---
keywords: Experience Platform;startpagina;populaire onderwerpen
solution: Experience Platform
title: Overzicht van beheer, privacy en beveiliging
description: Adobe Experience Platform biedt verschillende services en tools waarmee u uw verzamelde ervaringsgegevens op een betrouwbare manier kunt beheren, zodat u aan uw bedrijfspraktijken, wettelijke verplichtingen en ontwikkelingsproces kunt voldoen.
feature: Data Governance,Privacy
exl-id: 1ab5a436-c5dd-4e7a-aba1-549f0613f224
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 2%

---

# Bestuur, privacy en beveiliging in Adobe Experience Platform

Met Adobe Experience Platform kunt u uw gegevens invoeren, analyseren, optimaliseren en in actie brengen om de ervaringen van klanten aanzienlijk te verbeteren. Deze gegevens zijn enorm, complex en ongelooflijk waardevol. Afhankelijk van de aard van uw gegevensverrichtingen, de wettelijke jurisdicties uw bedrijf onder, en uw organisatiebeleid betreffende gegevensgebruik werkt, moet u zorgvuldig de inzameling en het gebruik van de gegevens van de klantenervaring controleren en controleren om uw bedrijfsbelangen te beschermen.

Experience Platform biedt verschillende services en tools waarmee u uw verzamelde ervaringsgegevens op een betrouwbare manier kunt beheren, zodat u aan uw bedrijfspraktijken, wettelijke verplichtingen en ontwikkelingsprocessen kunt voldoen. In de volgende secties wordt een inleiding gegeven op elk van deze diensten, samen met koppelingen naar documentatie voor meer informatie.

De diensten kunnen in drie domeinen worden gecategoriseerd:

* [Datagovernance](#governance)
* [Privacy](#privacy)
* [Beveiliging](#security)

## Datagovernance {#governance}

Het beheer van gegevens is een essentieel concept dat met alle mogelijkheden in Experience Platform is verweven. Het beheer van gegevens is uw vermogen om uw gegevens te controleren en te begrijpen gedurende de reis door Experience Platform. Dit omvat het handhaven van gegevenskwaliteit, gegevenslijn, gegevens het catalogiseren, en meer.

### Adobe Experience Platform Data Governance {#data-governance}

Als Experience Platform-service kunt u met Adobe Experience Platform Data Governance klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik worden nageleefd. Het speelt een sleutelrol binnen Experience Platform op diverse niveaus, met inbegrip van het etiketteren van het gegevensgebruik, het beleid van het gegevensgebruik, beleidshandhaving, en gegevenslijn.

Zie het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](../../data-governance/home.md) voor meer informatie.

### Catalogus en gegevenssets {#catalog}

Catalogusservice is het systeem voor het vastleggen van de locatie van gegevens en de gegevensverbinding in Experience Platform. Terwijl alle gegevens die in Experience Platform worden opgenomen in het Datameer als dossiers en folders worden opgeslagen, houdt de Catalogus de meta-gegevens en de beschrijving van die dossiers en folders voor raadpleging en controledoeleinden.

De catalogus organiseert ingebedde gegevens in datasets, met elke dataset die meta-gegevens bevat die kunnen worden gebruikt om de gegevens te etiketteren en te categoriseren het bevat.

Zie het [&#x200B; overzicht van de Dienst van de Catalogus &#x200B;](../../catalog/home.md) voor meer informatie over de dienst. Leren hoe te om datasets in Experience Platform te beheren, zie het [&#x200B; overzicht van datasets &#x200B;](../../catalog/datasets/overview.md).

## Privacy {#privacy}

Privacy is een essentieel probleem voor uw bedrijf, wetgevers en uw klanten. Aangezien persoonlijke gegevens die van uw klanten worden verzameld de kern vormen van bijna alle Experience Platform-workflows, biedt Experience Platform services om deze initiatieven te ondersteunen.

### Adobe Experience Platform Privacy Service {#privacy-service}

Wettelijke privacyregels zoals de Algemene Verordening van de Europese Unie inzake gegevensbescherming (GDPR) en de California Consumer Privacy Act (CCPA) verlenen burgers binnen hun rechtsgebied het recht om toegang te krijgen tot en de persoonsgegevens te verwijderen die u van hen verzamelt en opslaat.

Adobe Experience Platform Privacy Service biedt een RESTful-API en -gebruikersinterface waarmee u deze aanvragen kunt beheren. Met Privacy Service kunt u verzoeken indienen om toegang te krijgen tot persoonlijke of persoonlijke klantgegevens of deze te verwijderen uit Adobe Experience Cloud-toepassingen. Zo kunt u de automatische naleving van wettelijke en organisatorische privacyregels vereenvoudigen.

Zie het [&#x200B; overzicht van Privacy Service &#x200B;](../../privacy-service/home.md) voor meer informatie.

### Conceptverwerking {#consent}

Veel wettelijke privacyverordeningen hebben vereisten ingevoerd voor actieve en specifieke toestemming op het gebied van gegevensverzameling, personalisatie en andere gevallen van marketinggebruik. Om aan deze vereisten te voldoen, staat Experience Platform u toe om toestemmingsinformatie in individuele klantenprofielen te vangen en die voorkeur te gebruiken als bepalende factor in hoe de gegevens van elke klant in stroomafwaartse workflows van Experience Platform worden gebruikt.

Leren hoe te om klantentoestemming en voorkeursgegevens te verwerken gebruikend de norm van Adobe, zie het overzicht over [&#x200B; toestemmingsverwerking in Experience Platform &#x200B;](./consent/adobe/overview.md).

Voor informatie over hoe de gegevens van de de toestemmingen van de procesklant in overeenstemming met IAB Transparantie en het Kader van de Toestemming (TCF) 2.0, het overzicht op [&#x200B; IAB TCF 2.0 steun in Experience Platform &#x200B;](./consent/iab/overview.md) zien.

## Beveiliging {#security}

De integriteit en veiligheid van uw gegevens zijn onmisbaar voor uw bedrijf, en dit risico vereist industrie-leidende veiligheidsmogelijkheden. Om deze uitdaging het hoofd te bieden, biedt Experience Platform verschillende tools om uw gegevensbewerkingen beter te beveiligen.

### Gegevenscodering

Alle Experience Platform-gegevens worden in doorvoer en in rust versleuteld. Zie het document over [&#x200B; gegevensencryptie in Experience Platform &#x200B;](./encryption.md) voor meer informatie.

### Toegangsbeheer {#access-control}

Experience Platform gebruikt de Adobe Admin Console om rolgebaseerde toegangscontrole aan diverse mogelijkheden van Experience Platform te verstrekken. Deze functionaliteit maakt gebruik van productprofielen in Admin Console, die gebruikers koppelen aan machtigingen en sandboxen.

Zie het [&#x200B; overzicht van de toegangscontrole &#x200B;](../../access-control/home.md) voor meer informatie.

### Sandboxes {#sandboxes}

Experience Platform is ontworpen om toepassingen voor digitale beleving wereldwijd te verrijken. Bedrijven voeren vaak meerdere digitale-ervaringstoepassingen parallel uit en moeten rekening houden met de ontwikkeling, het testen en de implementatie van deze toepassingen en tegelijk de operationele compatibiliteit garanderen.

Experience Platform biedt sandboxen die één Experience Platform-instantie in afzonderlijke virtuele omgevingen verdelen om aan de behoefte aan ontwikkelflexibiliteit te voldoen. Zo kunt u uw digitale-ervaringstoepassingen ontwikkelen op basis van uw eigen ontwikkelingscyclus.

Zie het [sandboxoverzicht](../../sandboxes/home.md) voor meer informatie.

## Volgende stappen

In dit document wordt een overzicht gegeven van de verschillende Experience Platform-services en -tools op het gebied van gegevensbeheer, privacy en beveiliging. Raadpleeg de documentatie in deze handleiding voor meer informatie over deze mogelijkheden.
