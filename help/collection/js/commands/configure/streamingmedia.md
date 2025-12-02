---
title: streamingMedia
description: Configureer de Web SDK om gegevens te verzamelen die betrekking hebben op mediagebruik op uw wegeigenschappen.
exl-id: f7733619-d35e-43eb-ac90-052717310c39
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 1%

---

# `streamingMedia`

Met de component `streamingMedia` kunt u gegevens verzamelen die betrekking hebben op mediasessies op uw website.

De verzamelde gegevens kunnen informatie over media playbacks, pauzes, voltooiing, en andere verwante gebeurtenissen omvatten. Nadat deze gegevens zijn verzameld, kunt u deze naar Adobe Experience Platform of Adobe Analytics verzenden om rapporten te genereren. Deze functie biedt een uitgebreide oplossing voor het bijhouden en begrijpen van het gedrag van het mediaconsumptie op uw website.

## Vereisten

Als u de `streamingMedia` -component van de Web SDK wilt gebruiken, moet u aan de volgende voorwaarden voldoen:

* Zorg ervoor dat je toegang hebt tot Adobe Experience Platform of Adobe Analytics.
* U moet Web SDK versie 2.20.0 of later gebruiken. Zie het [ de installatieoverzicht van SDK van het Web ](../../install/overview.md) leren hoe te om de recentste versie te installeren.
* Schakel de optie **[[!UICONTROL Media Analytics]](/help/datastreams/configure.md#advanced-options)** in voor de gegevensstroom die u gebruikt.
* Zorg ervoor dat het schema dat door uw gegevensstroom wordt gebruikt de het schemagebieden van de Inzameling van Media omvat.
* Configureer de functie Streaming Media in de Web SDK, zoals weergegeven op deze pagina.

Voeg het object `configure` toe wanneer u de opdracht `streamingMedia` aanroept.

```js
alloy("configure", {
    streamingMedia: {
        channel: "Video channel",
        playerName: "Example player",
        appVersion: "Media Analytics with Web SDK 2.20.0",
        mainPingInterval: 10,
        adPingInterval: 10
    }
});
```

| Eigenschap | Type | Vereist | Beschrijving |
| --- | --- | --- | --- |
| **`channel`** | String | Ja | De naam van het kanaal waar de het stromen media inzameling voorkomt. Voorbeeld: `Video channel` . |
| **`playerName`** | String | Ja | De naam van de mediaspeler. |
| **`appVersion`** | String | Nee | De versie van de mediaspeler. |
| **`mainPingInterval`** | Geheel | Nee | Frequentie van pings voor belangrijkste inhoud, in seconden. De standaardwaarde is `10` . Waarden kunnen variëren van `10` tot `50` seconden.  Als geen waarde wordt gespecificeerd, wordt de standaardwaarde gebruikt wanneer het gebruiken van [ automatisch-gevolgde zittingen ](../createmediasession.md#automatic). |
| **`adPingInterval`** | Geheel | Nee | Frequentie van pingelt voor advertentie-inhoud, in seconden. De standaardwaarde is `10` . Waarden kunnen variëren van `1` tot `10` seconden. Als geen waarde wordt gespecificeerd, wordt de standaardwaarde gebruikt wanneer het gebruiken van [ automatisch-gevolgde zittingen ](../createmediasession.md#automatic). |

## Configuratie van streaming media met gebruik van de webtag SDK

Deze montages kunnen in de de markeringsuitbreiding van SDK van het Web worden gevormd gebruikend [ het stromen media configuratiemontages ](/help/tags/extensions/client/web-sdk/configure/streaming-media.md).
