---
title: Aan de slag met Extension Development
description: Ga aan de slag met het ontwikkelen van je eigen tag-extensies in Adobe Experience Platform.
exl-id: 3925b928-0180-4a4f-aaa6-42f342089560
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---

# Aan de slag met extensieontwikkeling

Als u extensies wilt gaan maken en gebruiken, gebruikt u het opensource-steigereedschap dat door Adobe-technici wordt geleverd om de benodigde bestanden en bestandsstructuur voor uw extensiepakket te maken. U hoeft dus alleen maar het waardevolle deel te doen: de code schrijven.

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

* [ de configuratiemening van de Uitbreiding ](./configuration.md): De mening, het dossier van HTML, waardoor een uitbreiding globale montages van een gebruiker verzamelt.
* [ de types van Gebeurtenis ](./web/event-types.md): Bepaalt een activiteit voor observatie. U moet bijvoorbeeld weten wanneer een gebruiker snel schuift of wanneer een gebruiker interactie heeft gehad met een pagina-element. Gebeurtenissen kunnen vervolgens in regels worden gebruikt om handelingen uit te voeren.
* [ de types van Voorwaarde ](./web/condition-types.md): De types van Voorwaarde evalueren of iets waar of vals is.
Dit kan bijvoorbeeld worden geretourneerd als de browser van de gebruiker Chrome is, als de gebruiker een iPad gebruikt of als de gebruiker zich in een specifiek domein bevindt.
* [ types van Actie ](./web/action-types.md): De actie om uit te voeren wanneer een gebeurtenis voorkomt. U kunt bijvoorbeeld een analysebaken verzenden, een aanbod weergeven, een cookie opslaan of een ondersteuningschat openen.
* [ het elementtypes van Gegevens ](./web/data-element-types.md): Het type van gegevenselement wint een stuk van gegevens terug. Deze gegevens kunnen lokaal worden opgeslagen, in een cookie, in een DOM-element of op een aangepaste locatie.
* [ Gedeelde modules ](./web/shared.md) (Web slechts): Een gedeelde module is een mechanisme waardoor de uitbreidingen met andere uitbreidingen kunnen communiceren.
* [ Meningen ](./web/views.md): Elke gebeurtenis, voorwaarde, actie, of type van gegevenselement kan een mening verstrekken die een gebruiker toestaat om montages te leveren.
* Exchange URL (alleen web en edge): wanneer een extensie wordt gepubliceerd naar een openbare catalogus in Adobe, geef hier de URL van de aanbieding op.
* Pad naar pictogram: een pad naar een pictogrambestand voor de extensie.

>[!NOTE]
>
>* De volgende looppas van het steigereedschap zal over de aanvankelijke configuratie overslaan.
>* Er kunnen meerdere gebeurtenissen, voorwaarden en handelingen worden toegevoegd.
>* Er kan slechts één configuratieweergave bestaan.

## Volgende stappen

* Volg het [ Overzicht van het Proces van de Verzending ](./submit/overview.md) en voorbereidingen om [ ](./submit/upload-and-test.md#validate) te bevestigen en [ ](./submit/upload-and-test.md#integration) uw uitbreiding voor het testen binnen het ecosysteem van de Markering te uploaden.
