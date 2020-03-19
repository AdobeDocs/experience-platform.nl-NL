---
title: Privacy in realtime gegevensprofiel van klanten
seo-title: Privacy in realtime gegevensprofiel van klanten
description: Met het realtime gegevensprofiel voor klanten kunt u het proces stroomlijnen waarbij uw gegevensbewerkingen in overeenstemming worden gehouden met privacyregels.
seo-description: Met het realtime gegevensprofiel voor klanten kunt u het proces stroomlijnen waarbij uw gegevensbewerkingen in overeenstemming worden gehouden met privacyregels.
translation-type: tm+mt
source-git-commit: 5d3bedd97208d9eed3977a35e16a10f4864aedd9

---


# Privacy in real time CDP

Het Real-Time Customer Data Platform (Real-time CDP) helpt marketers gegevens van meerdere bedrijfssystemen samen te brengen, zodat ze hun klanten beter kunnen identificeren, begrijpen en betrekken. Adobe beschouwt de privacy van consumentengegevens als een fundamenteel ontwerpbeginsel en biedt verschillende besturingselementen om marketers te helpen de privacy van gegevens van hun klanten te beheren.

De meeste CDP-mogelijkheden in realtime worden aangestuurd door het Adobe Experience Platform. Dit document biedt informatie over de verschillende technologieën voor privacyverbetering die worden ondersteund door Real-time CDP, met koppelingen naar de documentatie van het Experience Platform voor meer informatie.

## Privacy Service

Met de Adobe Experience Platform Privacy Service kunt u het proces van het naleven van uw gegevensbewerkingen stroomlijnen met privacyregels, zoals de General Data Protection Regulation (GDPR) en de California Consumer Privacy Act (CCPA). Aangezien CDP in real time de mogelijkheden van het Platform van de Ervaring voor gegevensinzameling en opslag gebruikt, zouden de toegang en schrappingsverzoeken voor GDPR en CCPA binnen Platform moeten worden beheerd. Zie het overzichtsdocument [van de Dienst van de](https://www.adobe.io/apis/experiencecloud/gdpr/docs/alldocs.html#!api-specification/markdown/narrative/technical_overview/privacy_service_overview/privacy_service_overview.md) Privacy voor een meer gedetailleerde inleiding van de dienst.

Er zijn twee methoden voor het indienen van individuele aanvragen voor GDPR- en CCPA-gegevens voor de toegang tot en het verwijderen van klantgegevens:

* Gebruik de UI [van de Dienst van de](https://gdprui.cloud.adobe.io/) Privacy om toegang tot te creëren en te controleren en verzoeken binnen een visuele werkruimte te schrappen. Raadpleeg de zelfstudie [over de](https://www.adobe.io/apis/experiencecloud/gdpr/docs/alldocs.html#!api-specification/markdown/narrative/tutorials/privacy_service_tutorial/privacy_service_ui_tutorial.md) privacyservice voor stapsgewijze instructies.
* Gebruik de API [van de Dienst van de](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html) Privacy om toegang te beheren en verzoeken met RESTful API vraag te schrappen. Zie de API-zelfstudie [van de](https://www.adobe.io/apis/experiencecloud/gdpr/docs/alldocs.html#!api-specification/markdown/narrative/tutorials/privacy_service_tutorial/privacy_service_api_tutorial.md) privacyservice voor stapsgewijze instructies.

<!-- (Capability will not be available for November GA) 
## Opt-out capabilities

Real-time CDP provides two types of consumer opt-out capabilities:

1. **General opt-out**: (Waiting on info)
1. **Segment-level opt-out of sale**: Opt-out of sale requests are captured using the Profile Privacy mixin (see the section on "Handling opt-out requests" in the [Real-time Customer Profile overview](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md) for more information). Using this, you can exclude users who have opted out from a segment using boolean logic ("AND NOT") in the segment predicate.
-->

## Volgende stappen

Dit document verstrekte een korte inleiding aan de mogelijkheden van de Privacy van CDP in real time. Raadpleeg de documentatie [van de](https://www.adobe.io/apis/experiencecloud/gdpr/docs.html)privacydienst voor gedetailleerde informatie over de beste praktijken en stappen voor het verzenden van toegang-/verwijderverzoeken.