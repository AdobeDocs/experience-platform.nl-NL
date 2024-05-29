---
title: createMediaSession
description: Leer hoe u Web SDK configureert om mediasessies automatisch te beheren
source-git-commit: 83d3de67e7680369dc890f58b16d9668058e221c
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 1%

---


# `createMediaSession`

De `createMediaSession` bevel maakt deel uit van SDK van het Web `streamingMedia` component. Met deze component kunt u gegevens verzamelen die betrekking hebben op mediasessies op uw website. Zie de `streamingMedia` [documentatie](configure/streamingmedia.md) om te leren hoe te om deze component te vormen.

De verzamelde gegevens kunnen informatie over media playbacks, pauzes, voltooiing, en andere verwante gebeurtenissen omvatten. Nadat de gegevens zijn verzameld, kunt u deze naar [Adobe Analytics para medios de streaming](https://experienceleague.adobe.com/en/docs/media-analytics/using/media-overview), om metriek samen te voegen. Deze functie biedt een uitgebreide oplossing voor het bijhouden en begrijpen van het gedrag van het mediaconsumptie op uw website.

U kunt mediasessies maken in Web SDK op twee manieren:

* [Automatisch bijgehouden mediasessies](#automatic) staat SDK van het Web toe om de verzending van media te beheren pingelt gebeurtenissen aan [Adobe Analytics para medios de streaming](https://experienceleague.adobe.com/en/docs/media-analytics/using/media-overview). De frequentie van deze pingelt wordt bepaald door de configuratiemontages van [streamingMedia](configure/streamingmedia.md) component.
* [Handmatig bijgehouden mediasessies](#manual) geeft u meer controle over het verzenden van zitting pingelt gebeurtenissen aan [Adobe Analytics para medios de streaming](https://experienceleague.adobe.com/en/docs/media-analytics/using/media-overview). Bovendien kunt u de `sessionID` voor mediasessies.

## Een automatisch bijgehouden mediasessie maken {#automatic}

Als u een mediasessie automatisch wilt laten bijhouden, roept u de `createMediaSession` met de hieronder beschreven opties:

```javascript
    alloy("createMediaSession", {
        playerId: "movie-test",
        getPlayerDetails: () => {
            return {
                playhead: document.getElementById("movie-test").currentTime,
                qoeDataDetails: {
                    bitrate: 1000,
                    startupTime: 1000,
                    fps: 30,
                    droppedFrames: 10
                }
            };
        },
        xdm: {
            eventType: "media.sessionStart",
            mediaCollection: {
                sessionDetails: {
                    ...
                }
            }
        }
    });
```

| Eigenschap | Type | Vereist | Beschrijving |
|---------|----------|---------|---------|
| `playerId` | String | Ja | De speler-id, een unieke id die de mediasessie vertegenwoordigt. |
| `getPlayerDetails` | Functie | Ja | Een functie die de spelerdetails terugkeert. Deze callback functie zal door het Web SDK vóór elke media gebeurtenis voor worden geroepen `playerId` verstrekt. |
| `xdm.eventType ` | Object | Nee | Het type media-gebeurtenis. Indien niet opgegeven, wordt deze automatisch ingesteld op `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | Object | Ja | Het object session details. De `sessionDetails` -object moet de eigenschappen van de sessiedetails bevatten. Zie de [Schema voor mediagroep](../../xdm/data-types/media-collection-details.md) documentatie voor meer informatie. |


## Een handmatig bijgehouden mediasessie maken {#manual}

Als u een mediasessie handmatig wilt bijhouden, roept u de `createMediaSession` met de hieronder beschreven opties:

```javascript
const sessionPromise = alloy("createMediaSession", {
    xdm: {
        eventType: "media.sessionStart",
        mediaCollection: {
            playhead: 0,
            sessionDetails: {
                ...
            },
            qoeDataDetails: {
                bitrate: 1000,
                startupTime: 1000,
                fps: 30,
                droppedFrames: 10
            }
        }
    }
});
```

| Eigenschap | Type | Vereist | Beschrijving |
|---------|----------|---------|---------|
| `xdm.eventType` | Object | Nee | Het type media-gebeurtenis. Indien niet opgegeven, wordt deze automatisch ingesteld op `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | Object | Ja | Het object session details. De `sessionDetails` -object moet de eigenschappen van de sessiedetails bevatten. Zie de [Schema voor mediagroep](../../xdm/data-types/media-collection-details.md) documentatie voor meer informatie. |
| `xdm.mediaCollection.playhead` | Geheel | Ja | De huidige afspeelkop. |
| `xdm.mediaCollection.qoeDataDetails` | Object | Nee | De kwaliteit van ervaringsgegevens. Zie de [Schema voor mediagroep](../../xdm/data-types/media-collection-details.md) documentatie voor meer informatie. |
