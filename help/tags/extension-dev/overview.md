---
title: Overzicht van de ontwikkeling van extensies
description: Meer informatie over de primaire componenten van verschillende typen tagextensies en het ontwikkelingsproces van extensies in Adobe Experience Platform.
exl-id: b72df3df-f206-488d-a690-0f086973c5b6
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 2%

---

# Overzicht van de ontwikkeling van extensies

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Een van de belangrijkste doelstellingen van tags in Adobe Experience Platform is het creëren van een open ecosysteem waar ingenieurs buiten de Adobe extra functies op hun websites en mobiele toepassingen kunnen blootstellen. Dit wordt gedaan door markeringsuitbreidingen. Nadat een extensie op een eigenschap tag is geïnstalleerd, wordt de functionaliteit van die extensie beschikbaar voor gebruik door alle gebruikers van de eigenschap.

In dit document worden de primaire componenten van een extensie beschreven en vindt u koppelingen naar verdere documentatie die u helpen bij het ontwikkelen van extensies.

## Extensiestructuur

Een extensie bestaat uit een map met bestanden. Specifiek, bestaat een uitbreiding uit een manifestdossier, bibliotheekmodules, en meningen.

### Manifest-bestand

Een manifestbestand ([`extension.json`](./manifest.md)) moet in de hoofdmap van de map staan. In dit bestand wordt de samenstelling van de extensie beschreven en wordt aangegeven waar bepaalde bestanden zich in de map bevinden. Het manifest werkt gelijkaardig aan a [`package.json`](https://docs.npmjs.com/files/package.json) bestand in een [npm](https://www.npmjs.com/) project.

### Bibliotheekmodules

Bibliotheekmodules zijn de bestanden die de verschillende [componenten](#components) dat een extensie bevat (met andere woorden de logica die moet worden uitgestraald in de runtimebibliotheek van de tag). De inhoud van elk bibliotheekmodulebestand moet overeenkomen met de [CommonJS module standard](https://nodejs.org/api/modules.html#modules-commonjs-modules).

Bijvoorbeeld, als u een actietype genoemd &quot;verzend baken&quot;bouwt, moet u een dossier hebben dat de logica bevat die het baken verzendt. Als u JavaScript gebruikt, kan het bestand worden aangeroepen `sendBeacon.js`. De inhoud van dit bestand wordt weergegeven in de runtimebibliotheek van de tag.

U kunt bibliotheekmodulebestanden op elke gewenste locatie in de extensiemap plaatsen, op voorwaarde dat u hun locaties in `extension.json`.

### Weergaven

Een weergave is een HTML-bestand dat in een [`iframe` element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) binnen de markeringstoepassing, specifiek door Platform UI en de UI van de Inzameling van Gegevens. De weergave moet een script bevatten dat door de extensie wordt aangeboden en moet een kleine API bevatten om te kunnen communiceren met de toepassing.

Het belangrijkste meningsdossier voor om het even welke uitbreiding is zijn configuratie. Zie de sectie over [extensieconfiguraties](#configuration) voor meer informatie .

Er gelden geen beperkingen ten aanzien van de bibliotheken die in uw weergaven worden gebruikt. Met andere woorden, u kunt jQuery, Onderstreping, Reageren, Angular, Bootstrap of andere gebruiken. Het wordt echter nog steeds aangeraden om uw extensie er net zo uit te laten zien als de interface.

U wordt aangeraden alle weergavegerelateerde bestanden (HTML, CSS, JavaScript) in één submap te plaatsen die is gescheiden van de bibliotheekmodulebestanden. In `extension.json`kunt u beschrijven waar deze submap voor de weergave zich bevindt. Het platform zal dan deze subdirectory (en slechts deze subdirectory) van zijn Webservers dienen.

## Bibliotheekcomponenten {#components}

Elke extensie definieert een reeks functies. Deze functies worden geïmplementeerd door in een [bibliotheek](../ui/publishing/libraries.md) die wordt geïmplementeerd op uw website of app. Bibliotheken zijn een verzameling afzonderlijke componenten, waaronder voorwaarden, handelingen, gegevenselementen en meer. Elke bibliotheekcomponent is een stuk herbruikbare code (verstrekt door een uitbreiding) die binnen markeringstruntime wordt uitgegeven.

Afhankelijk van het feit of u een webextensie of een randextensie ontwikkelt, verschillen de beschikbare typen componenten en de gebruikte toepassingen. Raadpleeg de onderstaande subsecties voor een overzicht van de componenten die beschikbaar zijn voor elk extensietype.

### Componenten voor webextensies {#web}

In webextensies worden regels geactiveerd via gebeurtenissen, die vervolgens specifieke acties kunnen uitvoeren als aan een bepaalde set voorwaarden wordt voldaan. Zie het overzicht op [modulestroom in Webuitbreidingen](./web/flow.md) voor meer informatie .

Naast de [kernmodules](./web/core.md) die door Adobe worden verstrekt, kunt u de volgende bibliotheekcomponenten in uw Webuitbreidingen bepalen:

* [Gebeurtenissen](./web/event-types.md)
* [Voorwaarden](./web/condition-types.md)
* [Acties](./web/action-types.md)
* [Gegevenselementen](./web/data-element-types.md)
* [Gedeelde modules](./web/shared.md)

>[!NOTE]
>
>Voor meer informatie over de vereiste indeling voor het implementeren van bibliotheekcomponenten in webextensies raadpleegt u de [overzicht van moduleopmaak](./web/format.md).

### Componenten voor randextensies {#edge}

In randuitbreidingen worden de regels geactiveerd door voorwaardencontroles, die vervolgens specifieke acties uitvoeren als die controles slagen. Zie het overzicht op de [edge extension flow](./edge/flow.md) voor meer informatie .

U kunt de volgende bibliotheekcomponenten in uw randuitbreidingen bepalen:

* [Voorwaarden](./edge/condition-types.md)
* [Acties](./edge/action-types.md)
* [Gegevenselementen](./edge/data-element-types.md)

>[!NOTE]
>
>Zie voor meer informatie over de vereiste indeling voor het implementeren van bibliotheekmodules in edge extensions de [overzicht van moduleopmaak](./edge/format.md).

## Extensieconfiguratie {#configuration}

De configuratie van een extensie verwijst naar de manier waarop algemene instellingen van een gebruiker worden verzameld. De configuratie bestaat uit een weergavecomponent die instellingen in de runtimebibliotheek van de tag als een onbewerkt object exporteert en uitgeeft.

Neem bijvoorbeeld een extensie die de gebruiker toestaat een baken te verzenden met de actie &quot;Send Beacon&quot; en die het baken altijd een account-id moet bevatten. In plaats van gebruikers elke keer om een account-id te vragen wanneer zij een actie &quot;Send Beacon&quot; configureren, moet de extensie eenmaal om de account-id vragen vanuit de configuratieweergave van de extensie. Telkens wanneer een baken moet worden verzonden, kan de actie &quot;Send Beacon&quot;rekeningsidentiteitskaart van de uitbreidingsconfiguratie trekken en het toevoegen aan het baken.

Wanneer gebruikers een uitbreiding aan een bezit in UI installeren, worden zij getoond de mening van de uitbreidingsconfiguratie, die zij moeten voltooien om de installatie te voltooien.

Raadpleeg de handleiding voor meer informatie [extensieconfiguraties](./configuration.md).

## Extensies verzenden

Nadat u de extensie hebt gemaakt, kunt u deze verzenden voor een lijst in de extensiecatalogus in Platform. Zie de [overzicht van het verzendproces voor extensies](./submit/overview.md) voor meer informatie .
