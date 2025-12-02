---
title: Id's delen via mobiel naar web en verschillende domeinen
description: Leer hoe u id's van bezoekers van mobiele naar webeigenschappen en in verschillende domeinen kunt behouden
keywords: Identiteit;mobiel;id;delen;domein;cross-domain;sdk;platform;
exl-id: b9bb236f-52cf-4615-96d8-1137d957de8c
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---

# Id&#39;s delen via mobiel naar web en verschillende domeinen

## Overzicht

De Adobe Experience Platform Web SDK ondersteunt mogelijkheden voor het delen van bezoekersidentificaties waarmee klanten een betere persoonlijke ervaring kunnen bieden, tussen mobiele apps en mobiele webinhoud, en in verschillende domeinen.

## Gebruiksscenario’s {#use-cases}

### Lever consistente personalisatie tussen mobiele apps en mobiele websites

Een kledingbedrijf wil de ervaring van hun klanten personaliseren die op hun belangen wordt gebaseerd, en de verpersoonlijking nauwkeurig houden in een mobiele toepassing die ook WebViews laadt. Met de functie voor het delen van mobiele-web-id&#39;s kunnen ze ervoor zorgen dat de meest nauwkeurige aanbiedingen aan klanten worden getoond, met dezelfde bezoeker-id in de app en mobiele webinhoud, door de [!DNL ECID] door te geven aan de mobiele URL.

### Zorg voor consistente personalisatie in verschillende domeinen

Een retailer met meerdere online winkels wil de verkoopervaring op hun verschillende domeinen personaliseren op basis van de belangen van de klant. Met de SDK-functie voor het delen van domeinoverschrijdende id&#39;s van het web kan de retailer op basis van de belangen van de klant nauwkeurige aanbiedingen op al hun domeinen aanbieden.

### De rapportage van bezoekersactiviteiten verbeteren

Een technologie die retailer wil verbeteren, wil de rapportage van bezoekersactiviteiten verbeteren met informatie over wanneer bezoekers van de mobiele toepassing naar hun mobiele website of naar hun andere domeinen gaan. Met de functie voor het delen van domeinoverschrijdende id&#39;s via Web SDK kan het marketingteam bezoekers nauwkeurig bijhouden op hun wegeigenschappen en activiteitenrapporten genereren.

## Vereisten {#prerequisites}

Gebruik [!DNL Web SDK] versie 2.11.0 of hoger als u id&#39;s van mobiele naar webapparaten en andere domeinen wilt delen.

Voor mobiele implementaties van Edge Network, wordt deze eigenschap gesteund in de [&#x200B; Identiteit voor Edge Network &#x200B;](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) uitbreiding die met versie 1.1.0 (iOS en Android) begint.

Deze functie is ook compatibel met [!DNL VisitorAPI.js] versie 1.7.0 of hoger.

## Id&#39;s delen via mobiele apparaten {#mobile-to-web}

Gebruik `getUrlVariables` API van de [&#x200B; Identiteit voor Edge Network &#x200B;](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables) uitbreiding om de herkenningstekens als vraagparameters terug te winnen en hen aan uw URL vast te maken wanneer het openen [!DNL webViews].

Er is geen aanvullende configuratie vereist voor de Web SDK om `ECID` -waarden in de queryreeks te accepteren.

De parameter van het vraagkoord omvat:

* `MCID`: De Experience Cloud-id (`ECID`)
* `MCORGID`: De Experience Cloud `orgID` die moet overeenkomen met de `orgID` die is geconfigureerd in de [!DNL Web SDK] .
* `TS`: een tijdstempelparameter die niet ouder dan vijf minuten mag zijn.


Bij het delen van een id van mobiel naar web wordt de parameter `adobe_mc` gebruikt. Wanneer de parameter `adobe_mc` aanwezig en geldig is, wordt `ECID` van de queryreeks automatisch toegevoegd aan de identiteitskaart in de eerste aanvraag die naar de Edge Network wordt uitgevoerd. Alle volgende Edge Network-interacties gebruiken die `ECID` .

Voor meer informatie over hoe te om bezoekers IDs van een mobiele app tot een WebView over te gaan, zie de documentatie over [&#x200B; behandelend WebViews &#x200B;](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html?lang=nl-NL#implementation).

## Id&#39;s delen naar andere domeinen implementeren {#cross-domain-sharing}

Zie de volgende verbindingen, afhankelijk van hoe u het Web SDK hebt gevormd:

* **de bibliotheek van JavaScript**: [`appendIdentityToUrl`](../../js/commands/appendidentitytourl.md) bevel
* **uitbreiding van de Markering**: [&#x200B; richt met identiteit &#x200B;](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md) actie
