---
keywords: Experience Platform;home;populaire onderwerpen;gegevensverzameling;starten;web-SDK
solution: Experience Platform
title: Overzicht Real-time Customer Data Platform-verbindingen
topic-legacy: overview
description: Meer informatie over de verschillende technologieën die u nodig hebt om gegevens te verzamelen over de ervaringen van klanten in Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 0a01dd2b0d8a1039178e3593475f9a87639ccdcd
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 3%

---

# Overzicht van Real-time Customer Data Platform-verbindingen

De Verbindingen van Real-time Customer Data Platform (RTCDP) verstrekt een reeks technologieën die u toestaan om klantenervaringsgegevens van cliënt-zijbronnen te verzamelen, en het te verzenden naar het Netwerk van de Rand van Adobe Experience Platform waar het kan worden verrijkt, worden getransformeerd, en aan Adobe of niet-Adobe bestemmingen in seconden worden verdeeld.

RTCDP-verbindingen worden ondersteund voor de volgende clientbronnen:

* Webtoepassingen
* Systeemeigen mobiele toepassingen
* OTT-toepassingen (Over-the-top)

RTCDP-verbindingen richten zich op de ontdekkingsmogelijkheden en toegankelijkheid van ingesloten gegevenssets, die het volgende omvatten:

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [Tags](../tags/home.md)
* [DataStreams](../edge/datastreams/overview.md)
* [Gebeurtenis doorsturen](../tags/ui/event-forwarding/overview.md)
* [Adobe Experience Platform Web SDK](../edge/home.md)
* [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/)
* [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=en)
* [Experience Data Model (XDM)](../xdm/home.md)
* [Adobe Experience Platform Identity Service](../identity-service/home.md)

Deze gids verstrekt een inleiding op hoog niveau RTCDP Verbindingen en hoe het werkt om gegevens naar de producten van Adobe Experience Cloud en niet-Adobe toepassingen door het Netwerk van de Rand van het Platform te verzenden.

## Tags, Web SDK en Mobile SDK

De SDK van het Web SDK van het Platform en van het Platform Mobiele SDK doen ineenstorten en alle het productbibliotheken van Adobe in één enkele ontwikkelingskit voor Web en mobiele platforms respectievelijk comprimeren. Deze kunnen worden geïmplementeerd met onbewerkte code of met [tags](../tags/home.md) via de gebruikersinterface voor gegevensverzameling.

Het samenpersen van deze bibliotheken versnelt gegevensinzameling en consolideert verrichtingen in één enkele stroom van cliënt-zijapparaten aan het Netwerk van de Rand van het Platform.

![Tags, Web SDK, Mobile SDK](./images/home/tags-sdks.png)

## Platform Edge Network en gegevensstreams {#edge}

Platform Edge Network is een wereldwijd gedistribueerd, snel en betrouwbaar netwerk van servers die gegevens op enorme schaal kunnen ontvangen en verwerken. Met tags kunt u [gegevensstromen](../edge/datastreams/overview.md) voor producten zoals Adobe Target, Adobe Audience Manager en Adobe Analytics, waarmee u deze producten aan de serverzijde kunt activeren zonder de clientcode te wijzigen.

![DataStreams en Adobe-oplossingen](./images/home/adobe-solutions.png)

>[!NOTE]
>
>Voor een inleiding op hoog niveau aan het Netwerk van de Rand van het Platform, verwijs naar het volgende [interactieve productrondreis](https://adobe-ideacloud.forgedx.com/adobe-adobe-edge-collection/adobe-experience-edge/public/mx?SUID=hgb1a48ICSCpbM6MzBYHbxnsh9DgjUy1).

## Gebeurtenis doorsturen

[Gebeurtenis doorsturen](../tags/ui/event-forwarding/overview.md) kan in om het even welke gegevensstroom van het Experience Platform tikken, die u toestaat om, gegevens te transformeren te verrijken en te verzenden naar om het even welke niet-Adobe bestemming met extreme lage latentie en zonder enige dercode aan het cliëntapparaat toe te voegen.

![Gebeurtenis doorsturen](./images/home/event-forwarding.png)

>[!NOTE]
>
>Het door:sturen van gebeurtenissen is een betaalde eigenschap die slechts als deel van het aanbieden van de Verbindingen van Real-time Customer Data Platform inbegrepen is.

## Volgende stappen

Dit document verstrekte een overzicht op hoog niveau van hoe de Verbindingen RTCDP werken om het proces te automatiseren om uw verzamelde gegevens van de klantenervaring naar de producten van de Adobe en derdebestemmingen te verzenden.

![Gegevensverzamelingskader](./images/home/collection.png)

Raadpleeg voor meer informatie over de algemene workflow voor het verzenden van gebeurtenisgegevens via het Edge-netwerk de [end-to-end overzicht](./e2e.md).
