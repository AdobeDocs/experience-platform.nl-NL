---
title: Instellingen voor streamingmedia
description: Pas aan hoe de de markeringsuitbreiding van SDK van het Web het stromen media gegevens verzamelt.
exl-id: f486d729-b7ad-4720-8399-71495cb9c57e
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 1%

---

# Instellingen voor streamingmedia {#streaming-media}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_streamingmedia"
>title="Streaming media"
>abstract="Hiermee bepaalt u hoe streaming mediagegevens worden verzameld tijdens het afspelen van media."

Met de functie voor het verzamelen van media kunt u gegevens verzamelen die betrekking hebben op mediasessies, zoals het afspelen van media, pauzes, voltooide bewerkingen en andere gerelateerde gebeurtenissen. Nadat deze gegevens zijn verzameld, kunt u deze naar Adobe Experience Platform of Adobe Analytics verzenden om rapporten te genereren. Deze functie biedt een uitgebreide oplossing voor het bijhouden en begrijpen van het gedrag van het mediaconsumptie op uw website.

1. Login aan [&#x200B; experience.adobe.com &#x200B;](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Ga naar **[!UICONTROL Extensions]** en selecteer vervolgens **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Schuif omlaag naar de sectie **[!UICONTROL Streaming media]** .

![&#x200B; Beeld dat de montages van de media inzameling van de de markeringsuitbreiding van SDK van het Web in de markeringen UI toont &#x200B;](../assets/media-collection.png)

## Vereisten

Als u de streamingmediacomponent van de Web SDK wilt gebruiken, moet u aan de volgende voorwaarden voldoen:

* Zorg ervoor dat je toegang hebt tot Adobe Experience Platform of Adobe Analytics.
* Schakel de optie **[[!UICONTROL Media Analytics]](/help/datastreams/configure.md#advanced-options)** in voor de gegevensstroom die u gebruikt.
* Zorg ervoor dat het schema dat door uw gegevensstroom wordt gebruikt de het schemagebieden van de Inzameling van Media omvat.
* Configureer de functie Streaming Media in de Web SDK-tagextensie, zoals wordt weergegeven op deze pagina.

## [!UICONTROL Channel]

De naam van het kanaal waar de media inzameling voorkomt. Bijvoorbeeld `Video channel` . Elke tekenreekswaarde is geldig.

## [!UICONTROL Player Name]

De naam van de mediaspeler die door de eigenschap wordt gebruikt voor het afspelen van media.

## [!UICONTROL Application Version]

De versie van de mediaspeler die uw eigenschap gebruikt voor het afspelen van media.

## [!UICONTROL Main ping interval]

De frequentie van pings voor belangrijkste inhoud, in seconden. De standaardwaarde is `10` . Waarden kunnen variëren van `10` tot `50` seconden. Als geen waarde wordt gespecificeerd, wordt de standaardwaarde gebruikt wanneer het gebruiken van [&#x200B; automatisch-gevolgde zittingen &#x200B;](/help/collection/js/commands/createmediasession.md#automatic).

## [!UICONTROL Ad ping interval]

De frequentie van pingelt voor advertentie-inhoud, in seconden. De standaardwaarde is `10` . Waarden kunnen variëren van `1` tot `10` seconden. Als geen waarde wordt gespecificeerd, wordt de standaardwaarde gebruikt wanneer het gebruiken van [&#x200B; automatisch-gevolgde zittingen &#x200B;](/help/collection/js/commands/createmediasession.md#automatic).
