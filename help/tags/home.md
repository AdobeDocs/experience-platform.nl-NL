---
title: Overzicht van tags
description: Tags in Adobe Experience Platform zijn de volgende generatie mogelijkheden voor tagbeheer van Adobe. Met labels kunnen klanten eenvoudig alle analytische, marketing- en advertentietags implementeren en beheren die nodig zijn om relevante klantervaringen te stimuleren.
exl-id: 23d882a5-1ddd-404b-a7e9-3000f1804971
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 1%

---

# Overzicht van codes

Tags in Adobe Experience Platform (voorheen Adobe Experience Platform Launch genoemd) zijn de volgende generatie mogelijkheden voor tagbeheer van Adobe. Met labels kunnen klanten eenvoudig alle analytische, marketing- en advertentietags implementeren en beheren die nodig zijn om relevante klantervaringen te stimuleren.

De markeringen machtigen iedereen om hun eigen integratie te bouwen en te handhaven, genoemd *uitbreidingen*. Deze extensies zijn beschikbaar voor [!DNL Adobe Experience Cloud] -klanten in een app-store-ervaring, zodat ze hun tags snel kunnen installeren, configureren en implementeren.

Tags worden aan [!DNL Adobe Experience Cloud] klanten aangeboden als een opgenomen functie voor het toevoegen van waarden.

## Belangrijkste voordelen {#key-benefits}

* Snellere waardetijd.
* Betrouwbare gegevens via gecentraliseerde verzameling, organisatie en levering met gegevenselementen.
* Dringende ervaringen door de integratie van gegevens en marketing technologie die regel bouwt.

## Belangrijkste kenmerken {#key-features}

Gebruik de Help in het product in het rechterdeelvenster voor meer informatie over tags en om aanvullende beschikbare bronnen weer te geven.

![&#x200B; de eigenschappen van Markeringen in de Inzameling UI van Gegevens.](./images/ui/tags-overview/tags-properties.png)

### Extensies {#extensions}

Een extensie is een pakket code (JavaScript, HTML en CSS) dat de functionaliteit voor tags uitbreidt. Ontwikkel, beheer, en werk uw integratie bij gebruikend een vrijwel zelfbedienings interface. U kunt extensies beschouwen als apps waarmee u uw taken kunt uitvoeren.

### Extensiecatalogus {#extension-catalog}

Blader naar, configureer en implementeer marketing-/advertentiegereedschappen die zijn gemaakt en onderhouden door onafhankelijke softwareleveranciers.

### Regelbouwer {#rule-builder}

Creeer robuuste regels die veelvoudige gebeurtenissen combineren, die op de manier worden gesequenced u het gebruiken als/toen logica met voorwaarden en uitzonderingen bepaalt. De regels bieden opties voor:

* Gebeurtenissen
* Voorwaarden
* Uitzonderingen
* Acties

De regelbouwer bevat foutcontrole en syntaxismarkering in real time voor uw aangepaste code.

Wanneer aan de criteria in uw regels is voldaan en aan de voorwaarden is voldaan, worden de acties die u definieert op volgorde uitgevoerd.

### Gegevenselementen {#data-elements}

Verzamel, organiseer, en lever gegevens over Web-based marketing en reclametechnologie.

### Enterprise publishing {#enterprise-publishing}

Met het publicatieproces kunnen teams code naar pagina&#39;s publiceren. Verschillende personen kunnen een implementatie maken, deze goedkeuren en op uw pagina&#39;s publiceren.

* Wijzigingen in de code worden ingekapseld in de bibliotheken die u definieert.
* U geeft op waar en wanneer u de code wilt implementeren.
* Meerdere bibliotheken kunnen parallel door verschillende teams worden gebouwd.
* Onbeperkte ontwikkelomgevingen.
* Een bewust, op toestemming-gebaseerd proces om bibliotheken samen te voegen.

### API&#39;s openen {#open-apis}

Automatiseer implementaties van individuele technologieën of een groep technologieën.

* Tags beïnvloeden de Reactor-API.
* Implementaties kunnen worden geautomatiseerd via API&#39;s.
* Integreer de API&#39;s met uw eigen interne systemen.
* U kunt desgewenst uw eigen gebruikersinterface maken.

### Lichte, modulaire containertag {#modular-tag}

De inhoud van de container wordt geminiatuurd, inclusief de aangepaste code. Alles is modulair. Als u geen punt nodig hebt, is het niet inbegrepen in uw bibliotheek. Het resultaat is een snelle en compacte implementatie. Zie [&#x200B; Minificatie &#x200B;](./ui/publishing/builds.md).

## Overige hooglichten {#other-highlights}

Tags bieden diverse verbeteringen ten opzichte van vergelijkbare systemen, zoals:

* Geen gebruik van `document.write ()` waar Chrome dit niet toestaat.
* De regels van de Boven Pagina en van de Onderkant van de Pagina zijn gebundeld in de belangrijkste bibliotheek om onnodige vraag van HTTP te minimaliseren.
* Scripts voor aangepaste handelingen binnen een regel kunnen parallel worden geladen, maar worden opeenvolgend uitgevoerd.
* Als u de regels Boven en Onder aan pagina vermijdt, is de code meestal asynchroon, met een pad naar volledig asynchroon worden.
