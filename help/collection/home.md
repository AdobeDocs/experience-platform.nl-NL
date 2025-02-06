---
keywords: Experience Platform;home;populaire onderwerpen;gegevensverzameling;starten;web-SDK
solution: Experience Platform
title: Overzicht van gegevensverzameling
description: Meer informatie over de verschillende technologieën die u nodig hebt om gegevens te verzamelen over de ervaringen van klanten in Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: b8332686043311c4dd3afeff12300fbd2827498c
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 3%

---

# Overzicht van gegevensverzameling

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens van de klantenervaring van client-side bronnen kunt verzamelen en deze naar de Adobe Experience Platform-Edge Network kunt verzenden waar deze in seconden kan worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe doelen.

Gegevensverzameling wordt ondersteund voor de volgende clientbronnen:

* Webtoepassingen
* Systeemeigen mobiele toepassingen
* OTT-toepassingen (Over-the-top)

De inzameling van gegevens concentreert zich op de ontdekkingsbaarheid en de toegankelijkheid van ingebedde datasets, die het volgende omvatten:

* [ Edge Network van Adobe Experience Platform ](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [Tags](../tags/home.md)
* [Gegevensstromen](../datastreams/overview.md)
* [Gebeurtenis doorsturen](../tags/ui/event-forwarding/overview.md)
* [Adobe Experience Platform Web SDK](../web-sdk/home.md)
* [ Adobe Experience Platform Mobile SDK ](https://developer.adobe.com/client-sdks/documentation/)
* [Edge Network Server API](../server-api/overview.md)
* [ Adobe Experience Platform Debugger ](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=en)
* [Experience Platform Assurance](../assurance/home.md)


Deze gids verstrekt een inleiding op hoog niveau aan gegevensinzameling en hoe het werkt om gegevens naar de producten van Adobe Experience Cloud en niet-Adobe toepassingen door de Edge Network van het Platform te verzenden.

## Tags, Web SDK en Mobile SDK

Het Platform Web SDK en Platform Mobile SDK vouwen en comprimeren alle bibliotheken van het Adobe product in één enkele ontwikkelingskit voor respectievelijk Web en Mobiele platforms. Deze kunnen worden uitgevoerd gebruikend ruwe code of gebruikend [ markeringen ](../tags/home.md) door de Inzameling UI van Gegevens of UI UI UI van Adobe Experience Platform.

Het samenpersen van deze bibliotheken versnelt gegevensinzameling en consolideert verrichtingen in één enkele stroom van cliënt-zijapparaten aan de Edge Network van het Platform.

![ Markeringen, Web SDK, Mobiele SDK ](./images/home/tags-sdks.png)

## Platform Edge Network en gegevensstromen {#edge}

De Edge Network van het platform is een globaal verdeeld, snel, en betrouwbaar netwerk van servers die gegevens kunnen ontvangen en verwerken op enorme schaal. Gebruikend markeringen, kunt u opstelling [ gegevensstromen ](../datastreams/overview.md) voor producten zoals Adobe Target, Adobe Audience Manager, en Adobe Analytics, die u toestaan om deze producten op de serverzijde te activeren zonder cliënt-zijcode te veranderen.

Bovendien zijn de gegevensstromen geïntegreerd met verscheidene mogelijkheden van het Platform die helpen ervoor zorgen dat om het even welke gevoelige gegevens u verzendt correct met betrekking tot organisatiebeleid en wettelijke verordeningen wordt behandeld. Zie de sectie over [ behandelend gevoelige gegevens ](../datastreams/overview.md#sensitive) in de documentatie van gegevensstromen voor meer informatie.

![ Datastreams en de oplossingen van de Adobe ](./images/home/adobe-solutions.png)

## Gebeurtenis doorsturen

[ Gebeurtenis door:sturen ](../tags/ui/event-forwarding/overview.md) kan in om het even welke gegevensstroom van het Experience Platform tikken, toestaand u om, gegevens aan om het even welke niet Adobe bestemming met extreme lage latentie te transformeren en te verzenden en zonder enige derdecode aan het cliëntapparaat toe te voegen.

![ Gebeurtenis door:sturen ](./images/home/event-forwarding.png)

>[!NOTE]
>
>Het door:sturen van gebeurtenissen is een betaalde eigenschap die als deel van het aanbod van de Verbindingen van Adobe Real-time Customer Data Platform, Prime, of Ultimate inbegrepen is.

## Volgende stappen

Dit document verstrekte een overzicht op hoog niveau van hoe de gegevensinzameling werkt om het proces te automatiseren om uw verzamelde gegevens van de klantenervaring naar de producten van de Adobe en derdebestemmingen te verzenden.

![ Kader van de inzameling van Gegevens ](./images/home/collection.png)

Voor meer informatie over het algemene werkschema betrokken bij het verzenden van gebeurtenisgegevens door de Edge Network, verwijs naar het [ overzicht van begin tot eind ](./e2e.md).
