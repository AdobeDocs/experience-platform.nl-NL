---
title: Overzicht van configuratie-instellingen
description: Meer informatie over de beschikbare opties bij het configureren van de Web SDK-tagextensie.
exl-id: 03f7bc0a-05c9-48ae-ae57-478db6d18f52
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 1%

---

# Overzicht van configuratie-instellingen {#config-overview}

De Adobe Experience Platform Web SDK-tagextensie biedt verschillende opties die u kunt aanpassen. Deze configuratie-instellingen komen overeen met het gebruik van de opdracht [`configure`](/help/collection/js/commands/configure/overview.md) in de JavaScript-bibliotheek.

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Ga naar **[!UICONTROL Extensions]** en selecteer vervolgens **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.

## Aangepaste build-componenten

Als het optimaliseren van bouwstijlgrootte een prioriteit voor uw organisatie is, kunt u bepaalde eigenschappen onbruikbaar maken die u niet gebruikt om de bouwstijlgrootte van de uitbreiding te verminderen. Zie [ Aangepast bouwt componenten ](custom-build-components.md) voor meer informatie.

## SDK-instanties

De meeste implementaties hebben doorgaans één SDK-exemplaar nodig. Als uw organisatie echter meerdere instanties van Web SDK-tracking nodig heeft, kunt u de knop **[!UICONTROL Add instance]** gebruiken. De volgende overkoepelende secties zijn beschikbaar wanneer het vormen van elke de markeringsinstantie van SDK van het Web:

* [**[!UICONTROL SDK instance]**](general.md) : Algemene instellingen voor de instantie. Alle velden in deze sectie zijn vereist.
* [**[!UICONTROL Datastreams]**](datastreams.md): waar u de gegevens voor elke markeringsmilieu wilt gaan.
* [**[!UICONTROL Consent]**](consent.md): standaardinstellingen voor toestemming voor de extensie.
* [**[!UICONTROL Identity]**](identity.md): instellingen voor cookie- en bezoekersmigratie.
* [**[!UICONTROL Personalization]**](personalization.md): Pas de ervaring van de bezoeker op individueel niveau aan.
* [**[!UICONTROL Data collection]**](data-collection.md): neem op of laat weg wat automatisch wordt verzameld.
* [**[!UICONTROL Streaming media]**](streaming-media.md): instellingen die specifiek zijn voor het streamen van mediaverzamelingen.
* [**[!UICONTROL Datastream configuration overrides]**](configuration-overrides.md): wijzig configuratie-instellingen wanneer aan bepaalde voorwaarden wordt voldaan.
* [**[!UICONTROL Advanced settings]**](advanced-settings.md): geef het basispad voor de Edge Network op.
