---
title: mediaCollection
description: Vorm SDK van het Web om gegevens te verzamelen met betrekking tot media gebruik op uw Web-eigenschappen.
source-git-commit: 1d1bb754769defd122faaa2160e06671bf02c974
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# `streamingMedia`

De `streamingMedia` kunt u gegevens verzamelen die betrekking hebben op mediasessies op uw website.

De verzamelde gegevens kunnen informatie over media playbacks, pauzes, voltooiing, en andere verwante gebeurtenissen omvatten. Nadat deze gegevens zijn verzameld, kunt u deze naar Adobe Experience Platform en/of Adobe Analytics verzenden om rapporten te genereren. Deze functie biedt een uitgebreide oplossing voor het bijhouden en begrijpen van het gedrag van het mediaconsumptie op uw website.

## Vereisten {#prerequisites}

Als u de opdracht `streamingMedia` component van Web SDK, moet u aan de volgende voorwaarden voldoen:

* Zorg ervoor dat u toegang hebt tot Adobe Experience Platform en/of Adobe Analytics.
* U moet Web SDK versie 2.20.0 of later gebruiken. Zie de [Overzicht van de installatie van Web SDK](../../install/overview.md) voor informatie over het installeren van de nieuwste versie.
* De optie **[[!UICONTROL Media Analytics]](../../../datastreams/configure.md#advanced-options)** voor de gegevensstroom die u gebruikt.
* Zorg ervoor dat het schema dat door uw gegevensstroom wordt gebruikt de het schemagebieden van de Inzameling van Media omvat.
* Vorm de Streaming eigenschap van Media in de configuratie van SDK van het Web, zoals aangetoond in deze pagina, of door [tagextensie](#tag-extension) of via de [JavaScript-bibliotheek](#library).

## Streaming media configureren met de webSDK-tagextensie {#tag-extension}

Voer de onderstaande stappen uit om streamingmedia te configureren in de SDK-tagextensie van Web.

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Navigeren naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] kaart.
1. Vorm **[!UICONTROL Streaming Media]** instellingen zoals beschreven in het dialoogvenster [Web SDK-pagina voor configuratie van tags](../../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#media-collection).

## Streaming media configureren met de Web SDK JavaScript-bibliotheek {#library}

Gebruik de eigenschappen die hieronder worden beschreven om streamingmedia in Web SDK te configureren.

Wanneer u de `configure` gebruiken, voegt u de opdracht `streamingMedia` object.

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
| `channel` | String | Ja | De naam van het kanaal waar de het stromen media inzameling voorkomt. Voorbeeld: `Video channel`. |
| `playerName` | String | Ja | De naam van de mediaspeler. |
| `appVersion` | String | Nee | De versie van de mediaspeler. |
| `mainPingInterval` | Geheel | Nee | Frequentie van pings voor belangrijkste inhoud, in seconden. De standaardwaarde is `10`. Waarden kunnen variëren van `10` tot `50` seconden.  Als er geen waarde is opgegeven, wordt de standaardwaarde gebruikt bij het gebruik [automatisch bijgehouden sessies](../createmediasession.md#automatic). |
| `adPingInterval` | Geheel | Nee | Frequentie van pingelt voor advertentie-inhoud, in seconden. De standaardwaarde is `10`. Waarden kunnen variëren van `1` tot `10` seconden. Als er geen waarde is opgegeven, wordt de standaardwaarde gebruikt bij het gebruik [automatisch bijgehouden sessies](../createmediasession.md#automatic). |
