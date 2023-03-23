---
title: Aan de slag met Extension Development
description: Ga aan de slag met het ontwikkelen van je eigen tag-extensies in Adobe Experience Platform.
exl-id: 3925b928-0180-4a4f-aaa6-42f342089560
source-git-commit: 0a4883cff4f8e04dd0dd62a9e01435fa302a9e54
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---

# Aan de slag met de ontwikkeling van extensies

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Als u extensies wilt gaan maken en gebruiken, gebruikt u het opensource-steigereedschap dat door Adobe-technici wordt geleverd om de benodigde bestanden en bestandsstructuur voor uw extensiepakket te maken. U hoeft dus alleen maar het waardevolle deel te doen: schrijven de code.

## Vereisten

* Installeren [Node.js](https://nodejs.org/en/download/).

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
* Versie - De versie van de extensie
* Beschrijving - Een korte beschrijving van het doel van de extensie
* Auteur - De naam van de auteur van de extensie

Het basisgereedschap bevat vervolgens opties voor het bouwen van de extensiestructuur:

* [Weergave voor extensieconfiguratie](./configuration.md): De weergave, het HTML-bestand waarmee een extensie algemene instellingen van een gebruiker verzamelt.
* [Gebeurtenistypen](./web/event-types.md): Definieert een activiteit voor observatie. U moet bijvoorbeeld weten wanneer een gebruiker snel schuift of wanneer een gebruiker interactie heeft gehad met een pagina-element. Gebeurtenissen kunnen vervolgens in regels worden gebruikt om handelingen uit te voeren.
* [Type voorwaarde](./web/condition-types.md): Voorwaardetypen evalueren of iets waar of onwaar is.
Dit kan bijvoorbeeld worden geretourneerd als de browser van de gebruiker Chrome is, als de gebruiker een iPad gebruikt of als de gebruiker zich in een specifiek domein bevindt.
* [Typen handelingen](./web/action-types.md): De handeling die moet worden uitgevoerd wanneer een gebeurtenis plaatsvindt. U kunt bijvoorbeeld een analysebaken verzenden, een aanbod weergeven, een cookie opslaan of een ondersteuningschat openen.
* [Gegevenstelelementtypen](./web/data-element-types.md): Een gegevenstype van een gegevenselement wint een stuk gegevens terug. Deze gegevens kunnen lokaal worden opgeslagen, in een cookie, in een DOM-element of op een aangepaste locatie.
* [Gedeelde modules](./web/shared.md): Een gedeelde module is een mechanisme waarmee extensies kunnen communiceren met andere extensies.
* [Weergaven](./web/views.md): Elke gebeurtenis, voorwaarde, actie, of het type van gegevenselement kan een mening verstrekken die een gebruiker toestaat om montages te leveren.

>[!NOTE]
>
>* De volgende looppas van het steigereedschap zal over de aanvankelijke configuratie overslaan.
>* Er kunnen meerdere gebeurtenissen, voorwaarden en handelingen worden toegevoegd.
>* Er kan slechts één configuratieweergave bestaan.


## Volgende stappen

* Volg de [Overzicht verzendproces](./submit/overview.md) en zich voorbereiden op [validate](./submit/upload-and-test.md#validate) en [uploaden](./submit/upload-and-test.md#integration) uw extensie voor testen binnen het ecosysteem van de tag.
