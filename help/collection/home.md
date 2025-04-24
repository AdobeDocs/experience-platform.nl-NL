---
keywords: Experience Platform;home;populaire onderwerpen;gegevensverzameling;starten;web-SDK
solution: Experience Platform
title: Overzicht van gegevensverzameling
description: Meer informatie over de verschillende technologieën die u nodig hebt om gegevens te verzamelen over de ervaringen van klanten in Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 2%

---

# Overzicht van gegevensverzameling

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens van klanten-side bronnen kunt verzamelen en deze naar Adobe Experience Platform Edge Network kunt sturen waar ze kunnen worden verrijkt, getransformeerd en in enkele seconden naar Adobe- of niet-Adobe-bestemmingen kunnen worden gedistribueerd.

Gegevensverzameling wordt ondersteund voor de volgende clientbronnen:

* Webtoepassingen
* Systeemeigen mobiele toepassingen
* OTT-toepassingen (Over-the-top)

De inzameling van gegevens concentreert zich op de ontdekkingsbaarheid en de toegankelijkheid van ingebedde datasets, die het volgende omvatten:

* [ Adobe Experience Platform Edge Network ](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [Tags](../tags/home.md)
* [Gegevensstromen](../datastreams/overview.md)
* [Gebeurtenis doorsturen](../tags/ui/event-forwarding/overview.md)
* [Adobe Experience Platform Web SDK](../web-sdk/home.md)
* [ Adobe Experience Platform Mobile SDK ](https://developer.adobe.com/client-sdks/documentation/)
* [ Edge Network API ](https://developer.adobe.com/data-collection-apis/docs/api/)
* [ Adobe Experience Platform Debugger ](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=en)
* [Experience Platform Assurance](../assurance/home.md)


Deze gids verstrekt een inleiding op hoog niveau aan gegevensinzameling en hoe het werkt om gegevens naar de producten van Adobe Experience Cloud en niet-Adobe toepassingen door Experience Platform Edge Network te verzenden.

## Tags, Web SDK en Mobile SDK

De Experience Platform Web SDK en Experience Platform Mobile SDK vouwen en comprimeren alle Adobe-productbibliotheken in één ontwikkelingskit voor respectievelijk web- en mobiele platforms. Deze kunnen worden uitgevoerd gebruikend ruwe code of gebruikend [ markeringen ](../tags/home.md) door de Inzameling UI van Gegevens of UI UI UI van Adobe Experience Platform.

Als u deze bibliotheken comprimeert, wordt de gegevensverzameling versneld en worden bewerkingen in één stream geconsolideerd, van client-side apparaten tot de Experience Platform Edge Network.

![ Markeringen, Web SDK, Mobiele SDK ](./images/home/tags-sdks.png)

## Experience Platform Edge Network en gegevensstromen {#edge}

Experience Platform Edge Network is een wereldwijd gedistribueerd, snel en betrouwbaar netwerk van servers die gegevens op enorme schaal kunnen ontvangen en verwerken. Gebruikend markeringen, kunt u opstelling [ gegevensstromen ](../datastreams/overview.md) voor producten zoals Adobe Target, Adobe Audience Manager, en Adobe Analytics, die u toestaan om deze producten op de serverzijde te activeren zonder cliënt-zijcode te veranderen.

Bovendien zijn gegevensstromen geïntegreerd met verscheidene mogelijkheden van Experience Platform die helpen ervoor zorgen dat om het even welke gevoelige gegevens u verzendt correct met betrekking tot organisatiebeleid en wettelijke verordeningen wordt behandeld. Zie de sectie over [ behandelend gevoelige gegevens ](../datastreams/overview.md#sensitive) in de documentatie van gegevensstromen voor meer informatie.

![ Datastreams en de oplossingen van Adobe ](./images/home/adobe-solutions.png)

## Gebeurtenis doorsturen

[ Gebeurtenis die ](../tags/ui/event-forwarding/overview.md) door:sturen kan in om het even welke gegevensstroom van Experience Platform tikken, die u toestaat om, gegevens aan om het even welke niet bestemming van Adobe met extreme lage latentie te transformeren te verrijken en te verzenden en zonder enige derdecode aan het cliëntapparaat toe te voegen.

![ Gebeurtenis door:sturen ](./images/home/event-forwarding.png)

>[!NOTE]
>
>Het door:sturen van gebeurtenissen is een betaalde eigenschap die als deel van het aanbod van de Verbindingen van Adobe Real-Time Customer Data Platform, Prime, of Ultimate inbegrepen is.

## Volgende stappen

Dit document biedt een overzicht op hoog niveau van de manier waarop gegevensverzameling werkt om het proces te automatiseren waarbij de verzamelde gegevens voor de klantervaring naar Adobe-producten en andere bestemmingen worden gestuurd.

![ Kader van de inzameling van Gegevens ](./images/home/collection.png)

Voor meer informatie over het algemene werkschema betrokken bij het verzenden van gebeurtenisgegevens door Edge Network, verwijs naar het [ overzicht van begin tot eind ](./e2e.md).
