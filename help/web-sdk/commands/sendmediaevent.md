---
title: sendMediaEvent
description: Leer hoe te om het sendMediaEvent bevel te gebruiken om media zittingen in Web SDK te volgen.
source-git-commit: 83d3de67e7680369dc890f58b16d9668058e221c
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 0%

---


# `sendMediaEvent`

De `sendMediaEvent` bevel maakt deel uit van SDK van het Web `streamingMedia` component. Met deze component kunt u gegevens verzamelen die betrekking hebben op mediasessies op uw website. Zie de `streamingMedia` [documentatie](configure/streamingmedia.md) om te leren hoe te om deze component te vormen.

Gebruik de `sendMediaEvent` gebruiken om het afspelen van media, pauzes, voltooiing, updates van de spelerstatus en andere verwante gebeurtenissen bij te houden.

De SDK van het Web kan media gebeurtenissen behandelen die op het type van media zitting het volgen worden gebaseerd:

* **Gebeurtenisafhandeling voor automatisch bijgehouden sessies**. In deze modus hoeft u het `sessionID` aan de media-gebeurtenis of de waarde van de afspeelkop. De SDK van het Web zal dit voor u behandelen, die op speleridentiteitskaart wordt gebaseerd en verstrekt `getPlayerDetails` callback functie verstrekt wanneer het beginnen van de media zitting.
* **Gebeurtenisafhandeling voor handmatig bijgehouden sessies**. In deze modus moet u de opdracht `sessionID` aan de media-gebeurtenis toe, samen met de waarde van de afspeelkop (geheel getal). Indien nodig kunt u ook de gegevens over de kwaliteit van de ervaring doorgeven.

## Media-gebeurtenissen op type afhandelen {#handle-by-type}

Selecteer de tabbladen hieronder om voorbeelden weer te geven van gebeurtenistype afhandeling voor elk gebeurtenistype en elke methode voor het bijhouden van sessies (automatisch of handmatig).


### Afspelen {#play}

De `media.play` Het gebeurtenistype wordt gebruikt om te volgen wanneer media playback begint. Deze gebeurtenis moet worden verzonden wanneer de afspeelstatus van de speler verandert in een andere status. Andere toestanden waarvan de speler overgaat op &#39;afspelen&#39; zijn &#39;buffering&#39;, het hervatten van &#39;gepauzeerd&#39;, het herstellen van een fout of het automatisch afspelen van de speler.

>[!BEGINTABS]

>[!TAB Automatische sessietracering]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.play"
    }
});
```

>[!TAB Handmatige sessietracering]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.play",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Pauzeren {#pause}

De `media.pauseStart` Het gebeurtenistype wordt gebruikt om te volgen wanneer een media playback wordt gepauzeerd. Deze gebeurtenis moet worden verzonden wanneer de gebruiker op **[!UICONTROL Pause]**. Er is geen type hervattingsgebeurtenis. Een samenvatting wordt afgeleid wanneer u een verzendt `media.play` gebeurtenis na een `media.pauseStart`.

>[!BEGINTABS]

>[!TAB Automatische sessietracering]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.pauseStart"
    }
});
```

>[!TAB Handmatige sessietracering]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.pauseStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Fout {#error}

De `media.error` Het gebeurtenistype wordt gebruikt om te volgen wanneer een fout tijdens media playback voorkomt. Deze gebeurtenis moet worden verzonden wanneer een fout optreedt.

>[!BEGINTABS]

>[!TAB Automatische sessietracering]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.error",
        mediaCollection: {
            errorDetails: {
                name: "network-error",
                source: "player"
            }
        }
    }
});
```

>[!TAB Handmatige sessietracering]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.error",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                errorDetails: {
                    name: "network-error",
                    source: "player"
                }
            }
        }
    });
});
```

>[!ENDTABS]


### Begin van einde toevoegen {#ad-break-start}

De `media.adBreakStart` Het gebeurtenistype wordt gebruikt om te volgen wanneer een advertentie-einde begint. Deze gebeurtenis moet worden verzonden wanneer een advertentie-einde begint.

>[!BEGINTABS]

>[!TAB Automatische sessietracering]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adBreakStart",
        mediaCollection: {
            advertisingPodDetails: {
                friendlyName: "Mid-roll",
                offset: 0,
                index: 1
            }
        }
    }
});
```

>[!TAB Handmatige sessietracering]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adBreakStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                advertisingPodDetails: {
                    friendlyName: "Mid-roll",
                    offset: 0,
                    index: 1
                }
            }
        }
    });
});
```

>[!ENDTABS]


### Einde van advertentie voltooid {#ad-break-complete}

De `media.adBreakComplete` Het gebeurtenistype wordt gebruikt om te volgen wanneer een afbreking van de advertentie voltooit. Deze gebeurtenis moet worden verzonden wanneer een advertentie-einde is voltooid.

>[!BEGINTABS]

>[!TAB Automatische sessietracering]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adBreakComplete"
    }
});
```

>[!TAB Handmatige sessietracering]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adBreakComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Begin advertentie {#ad-start}

De `media.adStart` Het gebeurtenistype wordt gebruikt om te volgen wanneer een advertentie begint. Deze gebeurtenis moet worden verzonden wanneer een advertentie wordt gestart.

>[!BEGINTABS]

>[!TAB Automatische sessietracering]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adStart",
        mediaCollection: {
            advertisingDetails: {
                friendlyName: "Ad 1",
                name: "/uri-reference/001",
                length: 10,
                advertiser: "Adobe Marketing",
                campaignID: "Adobe Analytics",
                creativeID: "creativeID",
                creativeURL: "https://creativeurl.com",
                placementID: "placementID",
                siteID: "siteID",
                podPosition: 11,
                playerName: "HTML5 player"
            },
            customMetadata: [{
                    name: "myCustomValue3",
                    value: "c3"
                },
                {
                    name: "myCustomValue2",
                    value: "c2"
                },
                {
                    name: "myCustomValue1",
                    value: "c1"
                }
            ]
        }
    }
});
```

>[!TAB Handmatige sessietracering]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
        eventType: "media.adStart",
        mediaCollection: {
            playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
            sessionID,
            advertisingDetails: {
              friendlyName: "Ad 1",
              name: "/uri-reference/001",
              length: 10,
              advertiser: "Adobe Marketing",
              campaignID: "Adobe Analytics",
              creativeID: "creativeID",
              creativeURL: "https://creativeurl.com",
              placementID: "placementID",
              siteID: "siteID",
              podPosition: 11,
              playerName: "HTML5 player"
            },
            customMetadata: [
              {
                name: "myCustomValue3",
                value: "c3"
              },
              {
                name: "myCustomValue2",
                value: "c2"
              },
              {
                name: "myCustomValue1",
                value: "c1"
              }]
        }
        }
    });
});
```

>[!ENDTABS]


### Toevoegen voltooid {#ad-complete}

De `media.adComplete` Het gebeurtenistype wordt gebruikt om te volgen wanneer een advertentie voltooit. Deze gebeurtenis moet worden verzonden wanneer een advertentie is voltooid.

>[!BEGINTABS]

>[!TAB Automatische sessietracering]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adComplete"
    }
});
```

>[!TAB Handmatige sessietracering]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Overslaan van advertentie {#ad-skip}

De `media.adSkip` gebeurtenistype wordt gebruikt om bij te houden wanneer een advertentie wordt overgeslagen. Deze gebeurtenis moet worden verzonden wanneer een advertentie wordt overgeslagen.

>[!BEGINTABS]

>[!TAB Automatische sessietracering]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adSkip"
    }
});
```

>[!TAB Handmatige sessietracering]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adSkip",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Begin hoofdstuk {#chapter-start}

De `media.chapterStart` Het gebeurtenistype wordt gebruikt om te volgen wanneer een hoofdstuk begint. Deze gebeurtenis moet worden verzonden wanneer een hoofdstuk begint.

>[!BEGINTABS]

>[!TAB Automatische sessietracering]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterStart",
        mediaCollection: {
            chapterDetails: {
                friendlyName: "Chapter 1",
                position: 1,
                length: 10,
                index: 1,
                offset: 0
            },
            customMetadata: [{
                    name: "myCustomValue3",
                    value: "c3"
                },
                {
                    name: "myCustomValue2",
                    value: "c2"
                },
                {
                    name: "myCustomValue1",
                    value: "c1"
                }
            ]
        }
    }
});
```

>[!TAB Handmatige sessietracering]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                chapterDetails: {
                    friendlyName: "Chapter 1",
                    position: 1,
                    length: 10,
                    index: 1,
                    offset: 0
                },
                customMetadata: [{
                        name: "myCustomValue3",
                        value: "c3"
                    },
                    {
                        name: "myCustomValue2",
                        value: "c2"
                    },
                    {
                        name: "myCustomValue1",
                        value: "c1"
                    }
                ]
            }
        }
    });
});
```

>[!ENDTABS]


### Hoofdstuk voltooid {#chapter-complete}

De `media.chapterComplete` Het gebeurtenistype wordt gebruikt om te volgen wanneer een hoofdstuk voltooit. Deze gebeurtenis moet worden verzonden wanneer een hoofdstuk is voltooid.

>[!BEGINTABS]

>[!TAB Automatische sessietracering]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterComplete"
    }
});
```

>[!TAB Handmatige sessietracering]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Hoofdstukoverslaan {#chapter-skip}

De `media.chapterSkip` Het gebeurtenistype wordt gebruikt om te volgen wanneer een hoofdstuk wordt overgeslagen. Deze gebeurtenis moet worden verzonden wanneer een hoofdstuk wordt overgeslagen.

>[!BEGINTABS]

>[!TAB Automatische sessietracering]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterSkip"
    }
});
```

>[!TAB Handmatige sessietracering]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterSkip",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Begin buffer {#buffer-start}

De `media.bufferStart` gebeurtenistype wordt gebruikt om bij te houden wanneer het bufferen begint. Deze gebeurtenis moet worden verzonden wanneer het bufferen begint. Er is `bufferResume` gebeurtenistype. A `bufferResume` wordt afgeleid wanneer u een afspeelgebeurtenis verzendt na `bufferStart`.

>[!BEGINTABS]

>[!TAB Automatische sessietracering]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.bufferStart"
    }
});
```

>[!TAB Handmatige sessietracering]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.bufferStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Wijziging van bitsnelheid {#bitrate-change}

De `media.bitrateChange` Het gebeurtenistype wordt gebruikt om te volgen wanneer de bitsnelheid verandert. Deze gebeurtenis moet worden verzonden wanneer de bitsnelheid verandert.

>[!BEGINTABS]

>[!TAB Automatische sessietracering]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.bitrateChange",
        mediaCollection: {
            qoeDataDetails: {
                framesPerSecond: 1,
                bitrate: 35000,
                droppedFrames: 30,
                timeToStart: 1364
            }
        }
    }
});
```

>[!TAB Handmatige sessietracering]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.bitrateChange",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                qoeDataDetails: {
                    bitrate: 35000,
                    droppedFrames: 30,
                    timeToStart: 1364
                }
            }
        }
    });
});
```

>[!ENDTABS]


### Statusupdates {#state-updates}

De `media.stateUpdate` Het gebeurtenistype wordt gebruikt om bij te houden wanneer de spelerstatus verandert. Deze gebeurtenis moet worden verzonden wanneer de status van de speler verandert.

>[!BEGINTABS]

>[!TAB Automatische sessietracering]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.stateUpdate",
        mediaCollection: {
            statesStart: [{
                    name: "mute"
                },
                {
                    name: "pictureInPicture"
                }
            ],
            statesEnd: [{
                name: "fullScreen"
            }]
        }
    }
});
```

>[!TAB Handmatige sessietracering]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.stateUpdate",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                statesStart: [{
                        name: "mute"
                    },
                    {
                        name: "pictureInPicture"
                    }
                ],
                statesEnd: [{
                    name: "fullScreen"
                }]
            }
        }
    });
});
```

>[!ENDTABS]


### Einde sessie {#session-end}

De `media.sessionEnd` Het gebeurtenistype wordt gebruikt om de achtergrond van Media Analytics op de hoogte te brengen om de sessie onmiddellijk te sluiten wanneer de gebruiker zijn weergave van de inhoud heeft beëindigd en het onwaarschijnlijk is dat deze zal terugkeren.

Als u geen `sessionEnd` -gebeurtenis, wordt een verlaten sessie beëindigd nadat gedurende 10 minuten geen gebeurtenissen zijn ontvangen of wanneer er gedurende 30 minuten geen beweging van de afspeelkop plaatsvindt. De sessie wordt automatisch verwijderd.

>[!BEGINTABS]

>[!TAB Automatische sessietracering]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.sessionEnd"
    }
});
```

>[!TAB Handmatige sessietracering]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.sessionEnd",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Sessie voltooid {#session-complete}

De `media.sessionComplete` gebeurtenistype wordt gebruikt om te volgen wanneer een mediasessie is voltooid. Deze gebeurtenis moet worden verzonden wanneer het einde van de hoofdinhoud is bereikt.

>[!BEGINTABS]

>[!TAB Automatische sessietracering]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.sessionComplete"
    }
});
```

>[!TAB Handmatige sessietracering]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.sessionComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]



