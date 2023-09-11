---
keywords: Experience Platform;home;populaire onderwerpen;gegevensverzameling;starten;web-SDK
solution: Experience Platform
title: Overzicht van gegevensverzameling
description: Meer informatie over de verschillende technologieën die u nodig hebt om gegevens te verzamelen over de ervaringen van klanten in Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 139d6a6632532b392fdf8d69c5c59d1fd779a6d1
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 3%

---

# Overzicht van gegevensverzameling

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens van de klantenervaring van client-side bronnen kunt verzamelen en deze naar het Adobe Experience Platform Edge Network kunt verzenden, waar het in seconden kan worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe doelen.

Gegevensverzameling wordt ondersteund voor de volgende clientbronnen:

* Webtoepassingen
* Systeemeigen mobiele toepassingen
* OTT-toepassingen (Over-the-top)

De inzameling van gegevens concentreert zich op de ontdekkingsbaarheid en de toegankelijkheid van ingebedde datasets, die het volgende omvatten:

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [Tags](../tags/home.md)
* [Gegevensstromen](../datastreams/overview.md)
* [Gebeurtenis doorsturen](../tags/ui/event-forwarding/overview.md)
* [Adobe Experience Platform Web SDK](../edge/home.md)
* [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)
* [Edge Network Server API](../server-api/overview.md)
* [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=en)
* [Experience Platform Assurance](../assurance/home.md)


Deze gids verstrekt een inleiding op hoog niveau aan gegevensinzameling en hoe het werkt om gegevens naar de producten van Adobe Experience Cloud en niet-Adobe toepassingen door het Netwerk van de Rand van het Platform te verzenden.

## Tags, Web SDK en Mobile SDK

De Platform Web SDK en Platform Mobile SDK doen ineenstorten en comprimeren alle bibliotheken van het product van de Adobe in één enkele ontwikkelingskit voor Web en mobiele platforms respectievelijk. Deze kunnen worden geïmplementeerd met onbewerkte code of met [tags](../tags/home.md) via de gebruikersinterface voor gegevensverzameling of de gebruikersinterface van Adobe Experience Platform.

Het samenpersen van deze bibliotheken versnelt gegevensinzameling en consolideert verrichtingen in één enkele stroom van cliënt-zijapparaten aan het Netwerk van de Rand van het Platform.

![Tags, Web SDK, Mobile SDK](./images/home/tags-sdks.png)

## Platform Edge Network en gegevensstreams {#edge}

Platform Edge Network is een wereldwijd gedistribueerd, snel en betrouwbaar netwerk van servers die gegevens op enorme schaal kunnen ontvangen en verwerken. Met tags kunt u [datastreams](../datastreams/overview.md) voor producten zoals Adobe Target, Adobe Audience Manager en Adobe Analytics, waarmee u deze producten aan de serverzijde kunt activeren zonder de clientcode te wijzigen.

Bovendien zijn de gegevensstromen geïntegreerd met verscheidene mogelijkheden van het Platform die helpen ervoor zorgen dat om het even welke gevoelige gegevens u verzendt correct met betrekking tot organisatiebeleid en wettelijke verordeningen wordt behandeld. Zie de sectie over [verwerking van gevoelige gegevens](../datastreams/overview.md#sensitive) in de documentatie van gegevensstromen voor meer informatie.

![Gegevensstromen en Adobe oplossingen](./images/home/adobe-solutions.png)

>[!NOTE]
>
>Voor een inleiding op hoog niveau aan het Netwerk van de Rand van het Platform, verwijs naar het volgende [interactieve productrondreis](https://adobe-ideacloud.forgedx.com/adobe-adobe-edge-collection/adobe-experience-edge/public/mx?SUID=hgb1a48ICSCpbM6MzBYHbxnsh9DgjUy1).

## Gebeurtenis doorsturen

[Gebeurtenis doorsturen](../tags/ui/event-forwarding/overview.md) kan in om het even welke gegevensstroom van het Experience Platform tikken, die u toestaat om, gegevens te transformeren te verrijken en te verzenden naar om het even welke niet Adobe bestemming met extreme lage latentie en zonder enige dercode aan het cliëntapparaat toe te voegen.

![Gebeurtenis doorsturen](./images/home/event-forwarding.png)

>[!NOTE]
>
>Het door:sturen van gebeurtenissen is een betaalde eigenschap die als deel van het de Verbindingen van Adobe Real-time Customer Data Platform, eerste, of Ultimate dienstenaanbod inbegrepen is.

## Volgende stappen

Dit document verstrekte een overzicht op hoog niveau van hoe de gegevensinzameling werkt om het proces te automatiseren om uw verzamelde gegevens van de klantenervaring naar de producten van de Adobe en derdebestemmingen te verzenden.

![Gegevensverzamelingskader](./images/home/collection.png)

Raadpleeg voor meer informatie over de algemene workflow voor het verzenden van gebeurtenisgegevens via het Edge-netwerk de [end-to-end overzicht](./e2e.md).
