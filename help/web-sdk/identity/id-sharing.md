---
title: Id's delen via mobiel naar web en verschillende domeinen
description: Leer hoe u id's van bezoekers van mobiele naar webeigenschappen en in verschillende domeinen kunt behouden
keywords: Identiteit;mobiel;id;delen;domein;cross-domain;sdk;platform;
exl-id: b9bb236f-52cf-4615-96d8-1137d957de8c
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# Id&#39;s delen via mobiel naar web en verschillende domeinen

## Overzicht

De Adobe Experience Platform Web SDK ondersteunt mogelijkheden voor het delen van bezoekersidentificaties, waarmee klanten een betere persoonlijke ervaring kunnen bieden, tussen mobiele apps en mobiele webinhoud, en in verschillende domeinen.

## Gebruiksscenario’s {#use-cases}

### Lever consistente personalisatie tussen mobiele apps en mobiele websites

Een kledingbedrijf wil de ervaring van hun klanten personaliseren die op hun belangen wordt gebaseerd, en de verpersoonlijking nauwkeurig houden in een mobiele toepassing die ook WebViews laadt. Met de functie voor het delen van mobiele tot webid kunnen ze ervoor zorgen dat de meest nauwkeurige aanbiedingen aan klanten worden gepresenteerd met dezelfde bezoeker-id in de app en mobiele webinhoud door te geven [!DNL ECID] naar de URL van het mobiele web.

### Zorg voor consistente personalisatie in verschillende domeinen

Een detailhandelaar met veelvoudige online winkels wil de winkelervaring over hun domeinen personaliseren, die op klantenbelangen wordt gebaseerd. Gebruikend de het delen eigenschap van identiteitskaart van SDK van het Web dwars-domein, kan de detailhandelaar nauwkeurige aanbiedingen leveren die op klantenbelangen, over elk van hun domeinen worden gebaseerd.

### De rapportage van bezoekersactiviteiten verbeteren

Een technologieverkoper wil zijn bezoekersactiviteit rapporteren met informatie over wanneer zijn bezoekers van de mobiele toepassing naar hun mobiele website of naar hun andere domeinen verhuizen. Gebruikend de het delen eigenschap van identiteitskaart van SDK van het Web dwars-domein, kan het marketing team bezoekers over hun Webeigenschappen nauwkeurig volgen en activiteitenrapporten produceren.

## Vereisten {#prerequisites}

Als u de id&#39;s van mobiel naar web en tussen domeinen wilt delen, moet u [!DNL Web SDK] versie 2.11.0 of hoger.

Voor mobiele Edge Network-implementaties wordt deze functie ondersteund in het dialoogvenster [Identiteit voor Edge Network](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) extensie die begint met versie 1.1.0 (iOS en Android).

Deze functie is ook compatibel met [!DNL VisitorAPI.js] versie 1.7.0 of hoger.

## Id&#39;s delen via mobiele apparaten {#mobile-to-web}

Gebruik de `getUrlVariables` API van de [Identiteit voor Edge Network](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables) extensie om de id&#39;s op te halen als queryparameters en deze aan uw URL te koppelen bij het openen van de URL [!DNL webViews].

Geen extra configuratie wordt vereist voor Web SDK om goed te keuren `ECID` waarden in de queryreeks.

De parameter van het vraagkoord omvat:

* `MCID`: De Experience Cloud-id (`ECID`)
* `MCORGID`: Het Experience Cloud `orgID` dat moet overeenkomen met `orgID` geconfigureerd in het dialoogvenster [!DNL Web SDK].
* `TS`: Een tijdstempelparameter die niet ouder dan vijf minuten mag zijn.


Bij het delen van een mobiele id naar een web wordt gebruikgemaakt van de `adobe_mc` parameter. Wanneer de `adobe_mc` parameter aanwezig en geldig is, `ECID` van het vraagkoord wordt automatisch toegevoegd aan de identiteitskaart in het eerste verzoek dat aan het Netwerk van de Rand wordt gemaakt. Alle volgende Edge Network-interacties gebruiken `ECID`.

Raadpleeg de documentatie voor meer informatie over het doorgeven van gebruikers-id&#39;s van een mobiele app aan een WebView [webweergaven verwerken](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation).

## Id&#39;s delen naar andere domeinen implementeren {#cross-domain-sharing}

Zie de [`appendIdentityToUrl`](../commands/appendidentitytourl.md) bevel voor implementatieinstructies die zowel de de markeringsuitbreiding van SDK van het Web als de bibliotheek van JavaScript van SDK van het Web gebruiken.
