---
title: sendMediaEvent
description: Leer hoe u de opdracht sendMediaEvent gebruikt om mediasessies in Web SDK bij te houden.
exl-id: a38626fd-4810-40a0-8893-e98136634fac
source-git-commit: 364b9adc406f732ea5ba450730397c4ce1bf03cf
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---

# `sendMediaEvent`

De opdracht `sendMediaEvent` maakt deel uit van de Web SDK `streamingMedia` -component. Met deze component kunt u gegevens verzamelen die betrekking hebben op mediasessies op uw website. Zie `streamingMedia` [ documentatie ](configure/streamingmedia.md) leren hoe te om deze component te vormen.

Gebruik de opdracht `sendMediaEvent` om het afspelen van media, pauzes, voltooiing, updates van de spelerstatus en andere gerelateerde gebeurtenissen bij te houden.

Web SDK kan media-gebeurtenissen afhandelen op basis van het type mediasessie bijhouden:

* **Gebeurtenis behandeling voor automatisch-gevolgde zittingen**. In deze modus hoeft u de waarde `sessionID` niet door te geven aan de media-gebeurtenis of aan de afspeelkop. De SDK van het Web zal dit voor u behandelen, die op speleridentiteitskaart wordt gebaseerd die en de `getPlayerDetails` callback functie wordt verstrekt wanneer het beginnen van de media zitting.
* **Gebeurtenis behandeling voor manueel-gevolgde zittingen**. In deze modus moet u de waarde `sessionID` aan de media-gebeurtenis doorgeven, samen met de waarde van de afspeelkop (geheel getal). Indien nodig kunt u ook de gegevens over de kwaliteit van de ervaring doorgeven.

## Media-gebeurtenissen op type afhandelen {#handle-by-type}

Selecteer de tabbladen hieronder om voorbeelden weer te geven van gebeurtenistype afhandeling voor elk gebeurtenistype en elke methode voor het bijhouden van sessies (automatisch of handmatig).

### Afspelen {#play}

Het gebeurtenistype `media.play` wordt gebruikt om te volgen wanneer het afspelen van media begint. Deze gebeurtenis moet worden verzonden wanneer de afspeelstatus van de speler verandert in een andere status. Andere toestanden waarvan de speler overgaat op &#39;afspelen&#39; zijn &#39;buffering&#39;, het hervatten van &#39;gepauzeerd&#39;, het herstellen van een fout of het automatisch afspelen van de speler.

>[!BEGINTABS]

>[!TAB  Automatische zitting het volgen ]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.play"
    }
});
```

>[!TAB  Handmatige zitting het volgen ]

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

Het gebeurtenistype `media.pauseStart` wordt gebruikt om bij te houden wanneer het afspelen van media is gepauzeerd. Deze gebeurtenis moet worden verzonden wanneer de gebruiker op **[!UICONTROL Pause]** drukt. Er is geen type hervattingsgebeurtenis. Er wordt een resume gegenereerd wanneer u een `media.play` -gebeurtenis na een `media.pauseStart` verzendt.

>[!BEGINTABS]

>[!TAB  Automatische zitting het volgen ]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.pauseStart"
    }
});
```

>[!TAB  Handmatige zitting het volgen ]

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

Het gebeurtenistype `media.error` wordt gebruikt om bij te houden wanneer een fout optreedt tijdens het afspelen van media. Deze gebeurtenis moet worden verzonden wanneer een fout optreedt.

>[!BEGINTABS]

>[!TAB  Automatische zitting het volgen ]

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

>[!TAB  Handmatige zitting het volgen ]

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

Het gebeurtenistype `media.adBreakStart` wordt gebruikt om te volgen wanneer een advertentie-einde begint. Deze gebeurtenis moet worden verzonden wanneer een advertentie-einde begint.

>[!BEGINTABS]

>[!TAB  Automatische zitting het volgen ]

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

>[!TAB  Handmatige zitting het volgen ]

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

Het gebeurtenistype `media.adBreakComplete` wordt gebruikt om bij te houden wanneer een advertentie-einde is voltooid. Deze gebeurtenis moet worden verzonden wanneer een advertentie-einde is voltooid.

>[!BEGINTABS]

>[!TAB  Automatische zitting het volgen ]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adBreakComplete"
    }
});
```

>[!TAB  Handmatige zitting het volgen ]

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

Het gebeurtenistype `media.adStart` wordt gebruikt om te volgen wanneer een advertentie begint. Deze gebeurtenis moet worden verzonden wanneer een advertentie wordt gestart.

>[!BEGINTABS]

>[!TAB  Automatische zitting het volgen ]

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

>[!TAB  Handmatige zitting het volgen ]

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

Het gebeurtenistype `media.adComplete` wordt gebruikt om te volgen wanneer een advertentie is voltooid. Deze gebeurtenis moet worden verzonden wanneer een advertentie is voltooid.

>[!BEGINTABS]

>[!TAB  Automatische zitting het volgen ]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adComplete"
    }
});
```

>[!TAB  Handmatige zitting het volgen ]

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

Het gebeurtenistype `media.adSkip` wordt gebruikt om te volgen wanneer een advertentie wordt overgeslagen. Deze gebeurtenis moet worden verzonden wanneer een advertentie wordt overgeslagen.

>[!BEGINTABS]

>[!TAB  Automatische zitting het volgen ]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adSkip"
    }
});
```

>[!TAB  Handmatige zitting het volgen ]

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

Het gebeurtenistype `media.chapterStart` wordt gebruikt om te volgen wanneer een hoofdstuk begint. Deze gebeurtenis moet worden verzonden wanneer een hoofdstuk begint.

>[!BEGINTABS]

>[!TAB  Automatische zitting het volgen ]

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

>[!TAB  Handmatige zitting het volgen ]

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

Het gebeurtenistype `media.chapterComplete` wordt gebruikt om te volgen wanneer een hoofdstuk voltooit. Deze gebeurtenis moet worden verzonden wanneer een hoofdstuk is voltooid.

>[!BEGINTABS]

>[!TAB  Automatische zitting het volgen ]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterComplete"
    }
});
```

>[!TAB  Handmatige zitting het volgen ]

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

Het gebeurtenistype `media.chapterSkip` wordt gebruikt om bij te houden wanneer een hoofdstuk wordt overgeslagen. Deze gebeurtenis moet worden verzonden wanneer een hoofdstuk wordt overgeslagen.

>[!BEGINTABS]

>[!TAB  Automatische zitting het volgen ]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterSkip"
    }
});
```

>[!TAB  Handmatige zitting het volgen ]

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

Het gebeurtenistype `media.bufferStart` wordt gebruikt om bij te houden wanneer het bufferen begint. Deze gebeurtenis moet worden verzonden wanneer het bufferen begint. Er is geen gebeurtenistype `bufferResume` . Een `bufferResume` wordt afgeleid wanneer u een afspeelgebeurtenis verzendt na `bufferStart` .

>[!BEGINTABS]

>[!TAB  Automatische zitting het volgen ]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.bufferStart"
    }
});
```

>[!TAB  Handmatige zitting het volgen ]

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

Het gebeurtenistype `media.bitrateChange` wordt gebruikt om te volgen wanneer de bitsnelheid verandert. Deze gebeurtenis moet worden verzonden wanneer de bitsnelheid verandert.

>[!BEGINTABS]

>[!TAB  Automatische zitting het volgen ]

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

>[!TAB  Handmatige zitting het volgen ]

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

Het gebeurtenistype `media.statesUpdate` wordt gebruikt om te volgen wanneer de spelerstatus verandert. Deze gebeurtenis moet worden verzonden wanneer de status van de speler verandert.

>[!BEGINTABS]

>[!TAB  Automatische zitting het volgen ]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.statesUpdate",
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

>[!TAB  Handmatige zitting het volgen ]

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

Het gebeurtenistype `media.sessionEnd` wordt gebruikt om de achtergrond van Media Analytics op de hoogte te brengen om de sessie onmiddellijk te sluiten wanneer de gebruiker de weergave van de inhoud heeft beëindigd en deze waarschijnlijk niet meer zal terugkeren.

Als u geen `sessionEnd` -gebeurtenis verzendt, wordt een verlaten sessie beëindigd nadat gedurende 10 minuten geen gebeurtenissen zijn ontvangen of wanneer gedurende 30 minuten geen beweging van de afspeelkop plaatsvindt. De sessie wordt automatisch verwijderd.

>[!BEGINTABS]

>[!TAB  Automatische zitting het volgen ]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.sessionEnd"
    }
});
```

>[!TAB  Handmatige zitting het volgen ]

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

Het gebeurtenistype `media.sessionComplete` wordt gebruikt om te volgen wanneer een mediasessie is voltooid. Deze gebeurtenis moet worden verzonden wanneer het einde van de hoofdinhoud is bereikt.

>[!BEGINTABS]

>[!TAB  Automatische zitting het volgen ]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.sessionComplete"
    }
});
```

>[!TAB  Handmatige zitting het volgen ]

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

## Media-gebeurtenis verzenden met de Web SDK-tagextensie

De Web SDK-tagextensie die equivalent is aan deze opdracht, is de [**[!UICONTROL Send media event]**](/help/tags/extensions/client/web-sdk/actions/send-media-event.md) -handeling.
