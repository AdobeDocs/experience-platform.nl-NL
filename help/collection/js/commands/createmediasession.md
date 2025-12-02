---
title: createMediaSession
description: Leer hoe u Web SDK configureert om mediasessies automatisch te beheren
exl-id: abcb26f6-7249-4235-99eb-e4b9aeecff3e
source-git-commit: 60447ef6f881bf2a34f5502f2259328bf73d08c0
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 1%

---

# `createMediaSession`

De opdracht `createMediaSession` maakt deel uit van de Web SDK `streamingMedia` -component. Met deze component kunt u gegevens verzamelen die betrekking hebben op mediasessies op uw website. Zie `streamingMedia` [&#x200B; documentatie &#x200B;](configure/streamingmedia.md) leren hoe te om deze component te vormen.

De verzamelde gegevens kunnen informatie over media playbacks, pauzes, voltooiing, en andere verwante gebeurtenissen omvatten. Zodra verzameld, kunt u deze gegevens naar [&#x200B; Analytics van Adobe voor het Streamen Media &#x200B;](https://experienceleague.adobe.com/en/docs/media-analytics/using/media-overview) verzenden, om metriek samen te voegen. Deze functie biedt een uitgebreide oplossing voor het bijhouden en begrijpen van het gedrag van het mediaconsumptie op uw website.

U kunt mediasessies op twee manieren maken in Web SDK:

* **automatisch-gevolgd media zittingen** staan SDK van het Web toe om de verzending van media te beheren pingelen gebeurtenissen aan [&#x200B; Analytics van Adobe voor het stromen Media &#x200B;](https://experienceleague.adobe.com/en/docs/media-analytics/using/media-overview). De frequentie van deze pingelt wordt bepaald door de configuratiemontages van de [&#x200B; streamingMedia &#x200B;](configure/streamingmedia.md) component.
* **manueel-geleide media zittingen** geven u meer controle over de verzending van zitting pingelt gebeurtenissen aan [&#x200B; Analytics van Adobe voor het stromen Media &#x200B;](https://experienceleague.adobe.com/en/docs/media-analytics/using/media-overview). Bovendien kunt u de `sessionID` voor mediasessies opslaan.

## Een automatisch bijgehouden mediasessie maken {#automatic}

Als u een mediasessie automatisch wilt laten volgen, roept u de methode `createMediaSession` aan met de opties die hieronder worden beschreven:

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
| `getPlayerDetails` | Functie | Ja | Een functie die de spelerdetails terugkeert. Deze callback functie zal door het Web SDK vóór elke media gebeurtenis voor `playerId` worden geroepen verstrekte. |
| `xdm.eventType` | Object | Nee | Het type media-gebeurtenis. Indien niet opgegeven, wordt dit veld automatisch ingesteld op `media.sessionStart` . |
| `xdm.mediaCollection.sessionDetails` | Object | Ja | Bevat eigenschappen voor sessiedetails. Zie [&#x200B; schema van de Inzameling van Media &#x200B;](/help/xdm/data-types/media-collection-details.md) voor meer informatie. |

## Een handmatig bijgehouden mediasessie maken {#manual}

Als u een mediasessie handmatig wilt volgen, roept u de methode `createMediaSession` aan met de opties die hieronder worden beschreven:

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
| `xdm.eventType` | Object | Nee | Het type media-gebeurtenis. Indien niet opgegeven, wordt deze automatisch ingesteld op `media.sessionStart` . |
| `xdm.mediaCollection.sessionDetails` | Object | Ja | Bevat eigenschappen voor sessiedetails. Zie [&#x200B; schema van de Inzameling van Media &#x200B;](/help/xdm/data-types/media-collection-details.md) voor meer informatie. |
| `xdm.mediaCollection.playhead` | Geheel | Ja | De huidige afspeelkop. |
| `xdm.mediaCollection.qoeDataDetails` | Object | Nee | De kwaliteit van ervaringsgegevens. Zie het [&#x200B; schema van de Inzameling van Media &#x200B;](/help/xdm/data-types/media-collection-details.md) documentatie voor meer informatie. |

## Een mediasessie maken met de Web SDK-tagextensie

De de markeringsuitbreiding van SDK van het Web gelijkwaardig aan dit bevel is het [**[!UICONTROL Session start]**](/help/tags/extensions/client/web-sdk/actions/send-media-event.md#session-start) gebeurtenistype binnen de &quot;[!UICONTROL Send media event]&quot;actie.
