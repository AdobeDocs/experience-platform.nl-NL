---
keywords: data governance rtcdp;rtcdp data governance;real time customer data profile data governance;privacy rtcdp;rtcdp privacy
title: Privacy in realtime gegevensprofiel van klanten
seo-title: Privacy in realtime gegevensprofiel van klanten
description: Met het realtime gegevensprofiel voor klanten kunt u het proces stroomlijnen waarbij uw gegevensbewerkingen in overeenstemming worden gehouden met privacyregels.
seo-description: Met het realtime gegevensprofiel voor klanten kunt u het proces stroomlijnen waarbij uw gegevensbewerkingen in overeenstemming worden gehouden met privacyregels.
translation-type: tm+mt
source-git-commit: 15323134f0c626cad2c4e90b3e1c0662cf7e57dd
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Privacy in real time CDP

[!DNL Real-time Customer Data Platform] (CDP in real time) helpt marketers gegevens van veelvoudige ondernemingssystemen samen te brengen, die hen toestaan om, hun klanten beter te identificeren te begrijpen en te betrekken. Adobe beschouwt de privacy van consumentengegevens als een fundamenteel ontwerpbeginsel en biedt verschillende controles om marketers te helpen de gegevensprivacy van hun klanten te beheren.

De meeste CDP-mogelijkheden in realtime worden aangestuurd door Adobe Experience Platform. Dit document biedt informatie over de verschillende technologieën voor privacyverbetering die worden ondersteund door Real-time CDP, met koppelingen naar [!DNL Experience Platform] documentatie voor meer informatie.

## [!DNL Privacy Service]

Met Adobe Experience Platform [!DNL Privacy Service] kunt u het proces stroomlijnen waarbij uw gegevensbewerkingen voldoen aan privacyregels zoals de [!DNL General Data Protection Regulation] (GDPR) en de [!DNL California Consumer Privacy Act] (CCPA). Aangezien CDP in real time [!DNL Experience Platform] mogelijkheden voor gegevensinzameling en opslag gebruikt, zouden de toegang en schrappingsverzoeken voor GDPR en CCPA binnen moeten worden beheerd [!DNL Platform]. Zie het overzichtsdocument [van de](../../privacy-service/home.md) Privacy Service voor een meer gedetailleerde inleiding van de dienst.

Er zijn twee methoden voor het indienen van individuele aanvragen voor GDPR- en CCPA-gegevens voor de toegang tot en het verwijderen van klantgegevens:

* Gebruik het [!DNL Privacy Service UI](https://gdprui.cloud.adobe.io/) om toegang tot en schrapping verzoeken binnen een visuele werkruimte tot stand te brengen en te controleren. Zie de zelfstudie [over de gebruikersinterface van de](../../privacy-service/ui/overview.md) Privacy Service voor stapsgewijze instructies.
* Gebruik [!DNL Privacy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) om toegang te beheren en verzoeken met RESTful API vraag te schrappen. Zie de API-zelfstudie voor [Privacy Service](../../privacy-service/api/getting-started.md) voor stapsgewijze instructies.

<!-- (Capability will not be available for November GA) 
## Opt-out capabilities

Real-time CDP provides two types of consumer opt-out capabilities:

1. **General opt-out**: (Waiting on info)
1. **Segment-level opt-out of sale**: Opt-out of sale requests are captured using the Profile Privacy mixin (see the section on "Handling opt-out requests" in the [Real-time Customer Profile overview](../../profile/home.md) for more information). Using this, you can exclude users who have opted out from a segment using boolean logic ("AND NOT") in the segment predicate.
-->

## Volgende stappen

Dit document verstrekte een korte inleiding aan de mogelijkheden van de Privacy van CDP in real time. Raadpleeg de documentatie bij de [Privacy Service](../../privacy-service/home.md)voor meer informatie over de beste praktijken en stappen voor het indienen van verzoeken om toegang/verwijdering.