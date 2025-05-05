---
title: Aan de slag met Extension Development
description: Ga aan de slag met het ontwikkelen van je eigen tag-extensies in Adobe Experience Platform.
exl-id: 3925b928-0180-4a4f-aaa6-42f342089560
source-git-commit: 077d3ac5a34f052ef6293927d67e3cc8afb27563
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 9%

---

# Aan de slag met extensieontwikkeling

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor dataverzameling in Adobe Experience Platform.  Als gevolg hiervan zijn er verschillende terminologiewijzigingen in de productdocumentatie doorgevoerd. Raadpleeg het volgende [ document ](../term-updates.md) voor een geconsolideerde referentie van de terminologiewijzigingen.

Om u in werking te stellen en uitbreidingen te bouwen, zullen wij het open-bronsteigereedschap gebruiken, dat door de ingenieurs van de Adobe wordt verstrekt om de noodzakelijke dossiers en dossierstructuur voor uw uitbreidingspakket tot stand te brengen, zodat alles u hebt verlaten om te doen is het waardevolle deel: eigenlijk schrijf de code.

## Vereisten

* Installeer [ Node.js ](https://nodejs.org/en/download/).

## Extensie instellen

Maak een map waarin uw extensiebestanden zich bevinden.

```shell
mkdir example && cd example
```

Deze handleiding gebruikt het basisgereedschap voor extensies om de initiële extensiestructuur samen te stellen, zodat ontwikkelaars snel kunnen beginnen met coderen. U kunt dit proces desgewenst handmatig uitvoeren zonder het basisgereedschap.

Voer het basisgereedschap uit.

```shell
npx @adobe/reactor-scaffold
```

In het basisgereedschap worden enkele initiële configuratieopties als volgt weergegeven:

* Weergavenaam - De zichtbare naam van de extensie
* Platform - Geeft aan of de extensie is ontwikkeld voor web, mobiel of edge
* Versie - De versie van de extensie
* Beschrijving - Een korte beschrijving van het doel van de extensie
* Auteur - De naam van de auteur van de extensie

>[!NOTE]
> Voor mobiele extensies worden verschillende vragen gesteld over de structuur van uw Android- en iOS-toepassingen.

Het basisgereedschap bevat vervolgens opties voor het bouwen van de extensiestructuur:

* [ de configuratiemening van de Uitbreiding ](./configuration.md): De mening, dossier van HTML, waardoor een uitbreiding globale montages van een gebruiker verzamelt.
* [ de types van Gebeurtenis ](./web/event-types.md): Bepaalt een activiteit voor observatie. U moet bijvoorbeeld weten wanneer een gebruiker snel schuift of wanneer een gebruiker interactie heeft gehad met een pagina-element. Gebeurtenissen kunnen vervolgens in regels worden gebruikt om handelingen uit te voeren.
* [ de types van Voorwaarde ](./web/condition-types.md): De types van Voorwaarde evalueren of iets waar of vals is.
Dit kan bijvoorbeeld worden geretourneerd als de browser van de gebruiker Chrome is, als de gebruiker een iPad gebruikt of als de gebruiker zich in een specifiek domein bevindt.
* [ types van Actie ](./web/action-types.md): De actie om uit te voeren wanneer een gebeurtenis voorkomt. U kunt bijvoorbeeld een analysebaken verzenden, een aanbod weergeven, een cookie opslaan of een ondersteuningschat openen.
* [ het elementtypes van Gegevens ](./web/data-element-types.md): Het type van gegevenselement wint een stuk van gegevens terug. Deze gegevens kunnen lokaal worden opgeslagen, in een cookie, in een DOM-element of op een aangepaste locatie.
* [ Gedeelde modules ](./web/shared.md) (Web slechts): Een gedeelde module is een mechanisme waardoor de uitbreidingen met andere uitbreidingen kunnen communiceren.
* [ Meningen ](./web/views.md): Elke gebeurtenis, voorwaarde, actie, of type van gegevenselement kan een mening verstrekken die een gebruiker toestaat om montages te leveren.
* Exchange URL (alleen voor web en edge): wanneer een extensie wordt gepubliceerd naar de openbare catalogus van de Adobe, geeft u hier de URL van de lijst op.
* Pad naar pictogram: een pad naar een pictogrambestand voor de extensie.

>[!NOTE]
>
>* De volgende looppas van het steigereedschap zal over de aanvankelijke configuratie overslaan.
>* Er kunnen meerdere gebeurtenissen, voorwaarden en handelingen worden toegevoegd.
>* Er kan slechts één configuratieweergave bestaan.

## Volgende stappen

* Volg het [ Overzicht van het Proces van de Verzending ](./submit/overview.md) en voorbereidingen om [&#128279;](./submit/upload-and-test.md#validate) te bevestigen en [&#128279;](./submit/upload-and-test.md#integration) uw uitbreiding voor het testen binnen het ecosysteem van de Markering te uploaden.
