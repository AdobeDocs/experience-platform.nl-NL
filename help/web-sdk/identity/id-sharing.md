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

Een kledingbedrijf wil de ervaring van hun klanten personaliseren die op hun belangen wordt gebaseerd, en de verpersoonlijking nauwkeurig houden in een mobiele toepassing die ook WebViews laadt. Met de functie voor het delen van mobiele-web-id&#39;s kunnen ze ervoor zorgen dat de meest nauwkeurige aanbiedingen aan klanten worden getoond, met dezelfde bezoeker-id in de app en mobiele webinhoud, door de [!DNL ECID] door te geven aan de mobiele URL.

### Zorg voor consistente personalisatie in verschillende domeinen

Een detailhandelaar met veelvoudige online winkels wil de winkelervaring over hun domeinen personaliseren, die op klantenbelangen wordt gebaseerd. Gebruikend de het delen eigenschap van identiteitskaart van SDK van het Web dwars-domein, kan de detailhandelaar nauwkeurige aanbiedingen leveren die op klantenbelangen, over elk van hun domeinen worden gebaseerd.

### De rapportage van bezoekersactiviteiten verbeteren

Een technologieverkoper wil zijn bezoekersactiviteit rapporteren met informatie over wanneer zijn bezoekers van de mobiele toepassing naar hun mobiele website of naar hun andere domeinen verhuizen. Gebruikend de het delen eigenschap van identiteitskaart van SDK van het Web dwars-domein, kan het marketing team bezoekers over hun Webeigenschappen nauwkeurig volgen en activiteitenrapporten produceren.

## Vereisten {#prerequisites}

Gebruik [!DNL Web SDK] versie 2.11.0 of hoger als u id&#39;s van mobiele naar webapparaten en andere domeinen wilt delen.

Voor mobiele implementaties van de Edge Network, wordt deze eigenschap gesteund in de [&#x200B; Identiteit voor Edge Network &#x200B;](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) uitbreiding die met versie 1.1.0 (iOS en Android) begint.

Deze functie is ook compatibel met [!DNL VisitorAPI.js] versie 1.7.0 of hoger.

## Id&#39;s delen via mobiele apparaten {#mobile-to-web}

Gebruik `getUrlVariables` API van de [&#x200B; Identiteit voor Edge Network &#x200B;](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables) uitbreiding om de herkenningstekens als vraagparameters terug te winnen en hen aan uw URL vast te maken wanneer het openen [!DNL webViews].

Er is geen aanvullende configuratie vereist voor de Web SDK om `ECID` -waarden in de queryreeks te accepteren.

De parameter van het vraagkoord omvat:

* `MCID`: De Experience Cloud-id (`ECID`)
* `MCORGID`: Het Experience Cloud `orgID` dat moet overeenkomen met de `orgID` die is geconfigureerd in de [!DNL Web SDK] .
* `TS`: een tijdstempelparameter die niet ouder dan vijf minuten mag zijn.


Bij het delen van een id van mobiel naar web wordt de parameter `adobe_mc` gebruikt. Wanneer de parameter `adobe_mc` aanwezig en geldig is, wordt `ECID` van het vraagkoord automatisch toegevoegd aan de identiteitskaart in het eerste verzoek aan de Edge Network wordt gemaakt die. Alle volgende Edge Network-interacties gebruiken die `ECID` .

Voor meer informatie over hoe te om bezoekers IDs van een mobiele app tot een WebView over te gaan, zie de documentatie over [&#x200B; behandelend WebViews &#x200B;](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html?lang=nl-NL#implementation).

## Id&#39;s delen naar andere domeinen implementeren {#cross-domain-sharing}

Zie het bevel [`appendIdentityToUrl`](../commands/appendidentitytourl.md) voor implementatieinstructies die zowel de de marktextensie van SDK van het Web als de bibliotheek van SDK van het Web gebruiken JavaScript.
