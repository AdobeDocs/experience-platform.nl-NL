---
title: streamingMedia
description: Vorm SDK van het Web om gegevens te verzamelen met betrekking tot media gebruik op uw Web-eigenschappen.
exl-id: f7733619-d35e-43eb-ac90-052717310c39
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 1%

---

# `streamingMedia`

Met de component `streamingMedia` kunt u gegevens verzamelen die betrekking hebben op mediasessies op uw website.

De verzamelde gegevens kunnen informatie over media playbacks, pauzes, voltooiing, en andere verwante gebeurtenissen omvatten. Nadat deze gegevens zijn verzameld, kunt u deze naar Adobe Experience Platform en/of Adobe Analytics verzenden om rapporten te genereren. Deze functie biedt een uitgebreide oplossing voor het bijhouden en begrijpen van het gedrag van het mediaconsumptie op uw website.

## Vereisten {#prerequisites}

Als u de component `streamingMedia` van Web SDK wilt gebruiken, moet u aan de volgende voorwaarden voldoen:

* Zorg ervoor dat u toegang hebt tot Adobe Experience Platform en/of Adobe Analytics.
* U moet Web SDK versie 2.20.0 of later gebruiken. Zie het [ de installatieoverzicht van SDK van het Web ](../../install/overview.md) leren hoe te om de recentste versie te installeren.
* Schakel de optie **[[!UICONTROL Media Analytics]](../../../datastreams/configure.md#advanced-options)** in voor de gegevensstroom die u gebruikt.
* Zorg ervoor dat het schema dat door uw gegevensstroom wordt gebruikt de het schemagebieden van de Inzameling van Media omvat.
* Vorm de Streaming eigenschap van Media in de configuratie van SDK van het Web, zoals aangetoond in deze pagina, of door de [ markeringsuitbreiding ](#tag-extension) of door de [ bibliotheek van JavaScript ](#library).

## Streaming media configureren met de webSDK-tagextensie {#tag-extension}

Voer de onderstaande stappen uit om streamingmedia te configureren in de SDK-tagextensie van Web.

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Vorm de **[!UICONTROL Streaming Media]** montages zoals die in de [ pagina van de de de taguitbreiding van SDK van het Web ](../../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#media-collection) worden beschreven.

## Streaming media configureren met de Web SDK JavaScript-bibliotheek {#library}

Gebruik de eigenschappen die hieronder worden beschreven om streamingmedia in Web SDK te configureren.

Voeg het object `streamingMedia` toe wanneer u de opdracht `configure` aanroept.

```js
alloy("configure", {
    streamingMedia: {
        channel: "video channel",
        playerName: "test player",
        appVersion: "Media Analytics with Web SDK 2.20.0",
        mainPingInterval: 10,
        adPingInterval: 10
    }
});
```

| Eigenschap | Type | Vereist | Beschrijving |
|---------|----------|---------|---------|
| `channel` | String | Ja | De naam van het kanaal waar de het stromen media inzameling voorkomt. Voorbeeld: `Video channel` . |
| `playerName` | String | Ja | De naam van de mediaspeler. |
| `appVersion` | String | Nee | De versie van de mediaspeler. |
| `mainPingInterval` | Geheel | Nee | Frequentie van pings voor belangrijkste inhoud, in seconden. De standaardwaarde is `10` . Waarden kunnen variëren van `10` tot `50` seconden.  Als geen waarde wordt gespecificeerd, wordt de standaardwaarde gebruikt wanneer het gebruiken van [ automatisch-gevolgde zittingen ](../createmediasession.md#automatic). |
| `adPingInterval` | Geheel | Nee | Frequentie van pingelt voor advertentie-inhoud, in seconden. De standaardwaarde is `10` . Waarden kunnen variëren van `1` tot `10` seconden. Als geen waarde wordt gespecificeerd, wordt de standaardwaarde gebruikt wanneer het gebruiken van [ automatisch-gevolgde zittingen ](../createmediasession.md#automatic). |
