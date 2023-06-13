---
keywords: Experience Platform;mediarand;populaire onderwerpen;datumbereik
solution: Experience Platform
title: Aan de slag met Media Edge-API's
description: Aan de slag met Media Edge-API's
exl-id: null
source-git-commit: 696ddd93d87601f9f6dedfd651ee12573dc4990a
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 1%

---


# Media Edge API aan de slag

Deze handleiding bevat instructies voor het tot stand brengen van succesvolle initiële interactie met de Media Edge API-service. Dit omvat het starten van een mediasessie en het volgen van gebeurtenissen die naar een Adobe Experience Platform-oplossing (AEP), zoals Customer Journey Analytics (CJA), worden verzonden. De dienst van Media Edge API wordt in werking gesteld met het eindpunt van het Begin van de Zitting. Nadat de sessie is gestart, kunnen een of meer van de volgende gebeurtenissen worden bijgehouden:

* play
* pingelen
* bitrateChange
* bufferStart
* pauseStart
* adBreakStart
* adStart
* adComplete
* adSkip
* adBreakComplete
* hoofdstukStart
* hoofdstukComplete
* hoofdstukSkip
* error
* sessionEnd
* sessionComplete
* statesUpdate

Elke gebeurtenis heeft zijn eigen eindpunt. Alle eindpunten van de mediarand-API zijn POST-methoden, met JSON-aanvraaginstanties voor gebeurtenisgegevens. Zie het Media Edge Swagger-bestand voor meer informatie over eindpunten, parameters en voorbeelden van de Media Edge API.

In deze handleiding ziet u hoe de volgende gebeurtenissen worden bijgehouden na het starten van de sessie:

* Begin buffer
* Afspelen
* Sessie voltooid

## De API implementeren

Naast kleine verschillen in het model en de geroepen wegen, is de Rand API van Media het zelfde als de Inzameling API van Media. De implementatiedetails van Media Collection blijven geldig voor Media Edge API, zoals die in de volgende documentatie wordt beschreven:

* [Het HTTP-aanvraagtype in de speler instellen](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-sed-pings.html?lang=en)
* [Pingsgebeurtenissen verzenden](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-sed-pings.html?lang=en)
* [Tijdslimiet](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-timeout.html?lang=en)
* [De volgorde van gebeurtenissen bepalen](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-ctrl-order.html?lang=en)

## Toestemming

Op dit moment vereisen de mediarand-API&#39;s geen machtigingskoppen in hun aanvragen.


## De sessie starten

Om de media zitting op de server te beginnen, gebruik het eindpunt van het Begin van de Zitting. Een geslaagde reactie omvat een `sessionId`, een vereiste parameter voor volgende gebeurtenisaanvragen.

Voordat u de aanvraag voor het starten van de sessie indient, hebt u het volgende nodig:

* De `datastreamId` is een vereiste parameter voor het verzoek van het Begin van de Zitting van de POST. Om een `datastreamId`, zie [Een gegevensstroom configureren](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en).

* Een JSON-object voor de payload van de aanvraag dat de minimaal vereiste gegevens bevat (zoals in de onderstaande voorbeeldaanvraag wordt getoond).

Wanneer u deze informatie hebt, geeft u de `datastreamId` in de volgende vraag:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/sessionStart?configId={datastream ID} \`

### Voorbeeld van aanvraag

In het volgende voorbeeld wordt een cURL-aanvraag voor het starten van een sessie getoond:

```
curl -i --request POST '{uri}/ee/va/v1/sessionStart?configId={dataStreamId}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
          "sessionDetails": {
            "name": "Media Analytics API Sample",
            "playerName": "sample-html5-api-player",
            "contentType": "VOD",
            "length": 60,
            "channel": "sample-channel",
            "appVersion": "va-api-1.0.0"
          },
          "playhead": 0
        }
      }
    }
  ]
}'
```

In het bovenstaande voorbeeldverzoek worden de `eventType` value contains the prefix `media` volgens de [Experience Data Model (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=nl) voor het opgeven van domeinen.

De datatypes-toewijzing voor `eventType` in het bovenstaande voorbeeld ziet het er als volgt uit :

| eventType | datatypen |
| -------- | ------ |
| mediaSessionStart | [sessionDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/sessiondetails.schema.md) |
| media.chapterStart | [hoofdstukDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/chapterdetails.schema.md) |
| media.adBreakStart | [advertentiePodDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/advertisingpoddetails.schema.md) |
| media.adStart | [adverterenDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/advertisingdetails.schema.md) |
| media.error | [errorDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/errordetails.schema.md) |
| media.statesUpdate | [statesStart](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmstatesstart): Array[playerStateData], [statesEnd](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmstatesend): Array[playerStateData] |
| media.sessionStart, media.chapterStart, media.adStart | [customMetadata](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmcustommetadata) |
| alles | [qoeDataDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/qoedatadetails.schema.md) |

### Voorbeeldreactie

Het volgende voorbeeld toont een succesvolle reactie voor het verzoek van het zittingsbegin:

```
HTTP/2 200
x-request-id: 99603f5c-95cf-49ad-9afb-0ba6c5867fd7
x-rate-limit-remaining: 599
vary: Origin
date: Tue, 07 Mar 2023 14:37:58 GMT
x-konductor: 23.3.2:367bc7dc
x-adobe-edge: IRL1;6
server: jag
content-type: application/json;charset=utf-8
strict-transport-security: max-age=31536000; includeSubDomains
cache-control: no-cache, no-store, max-age=0, no-transform
x-xss-protection: 1; mode=block
x-content-type-options: nosniff

{
    "requestId": "df14bca1-ba0f-4574-ae80-a4e24a960c00",
    "handle": [
        {
            "payload": [
                {
                    "sessionId": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333"
                }
            ],
            "type": "media-analytics:new-session",
            "eventIndex": 0
        },
        {
            "payload": [
                {
                    "key": "kndctr_6D9FE18C5536A5E90A4C98A6_AdobeOrg_cluster",
                    "value": "irl1",
                    "maxAge": 1800
                },
                {
                    "key": "kndctr_6D9FE18C5536A5E90A4C98A6_AdobeOrg_identity",
                    "value": "CiY1MTkxMDM4OTc1MzkwMTY4NTQ1NjAxNDg4OTgzODU5MTAzMDcyMVIPCKKt8KnsMBgBKgRJUkwx8AGirfCp7DA=",
                    "maxAge": 34128000
                }
            ],
            "type": "state:store"
        }
    ]
}
```

In het bovenstaande voorbeeldantwoord worden de `sessionId` wordt weergegeven zoals `af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333`. U gebruikt deze id in volgende verzoeken om gebeurtenissen als een vereiste parameter.

Voor meer informatie over de parameters en voorbeelden van het eindpunt van het Begin van de Zitting, zie het dossier van de Rand van Media.

Voor meer informatie over XDM media gegevensparameters, zie [Informatieschema voor mediagegevens](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmplayhead).


## Buffer Start-gebeurtenisaanvraag

De gebeurtenissignalen van het Begin van de buffer wanneer het bufferen op de media speler begint. Buffer Resume is geen gebeurtenis in de API-service. in plaats daarvan wordt het afgeleid wanneer een playbackgebeurtenis wordt verzonden na het Begin van de Buffer. Als u een aanvraag voor een bufferstartgebeurtenis wilt indienen, gebruikt u uw `sessionId` in de lading van een vraag aan het volgende eindpunt:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/bufferStart \`

### Voorbeeld van aanvraag

In het volgende voorbeeld wordt een BufferStart-cURL-aanvraag getoond:

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/bufferStart' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.bufferStart",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

In het bovenstaande voorbeeldverzoek is hetzelfde `sessionId` die in de vorige vraag is teruggekeerd wordt gebruikt als vereiste parameter in het verzoek van het Begin van de Buffer.

Voor meer informatie over de parameters en voorbeelden van het eindpunt van het Begin van de Buffer, zie het dossier van de Rand van Media.

De geslaagde reactie geeft de status 200 aan en bevat geen inhoud.

## Gebeurtenisverzoek afspelen

De gebeurtenis Play wordt verzonden wanneer de mediaspeler de afspeelstatus wijzigt in een andere status, zoals &quot;buffering&quot;, &quot;gepauzeerd&quot; of &quot;fout&quot;. Als u een verzoek voor een Play-gebeurtenis wilt uitvoeren, gebruikt u uw `sessionId` in de lading van een vraag aan het volgende eindpunt:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/play \`

### Voorbeeld van aanvraag

In het volgende voorbeeld wordt een Play cURL-aanvraag getoond:

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/play' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.play",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

De geslaagde reactie geeft de status 200 aan en bevat geen inhoud.

Zie het bestand Media Edge Swagger voor meer informatie over parameters en voorbeelden van het eindpunt Afspelen.

## Gebeurtenisaanvraag voor sessie voltooid

De gebeurtenis Session Complete wordt verzonden wanneer het einde van de hoofdinhoud is bereikt. Als u een aanvraag voor een volledige sessie wilt indienen, gebruikt u uw `sessionId` in de lading van een vraag aan het volgende eindpunt:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/sessionComplete \`

### Voorbeeld van aanvraag

In het volgende voorbeeld ziet u een Sessie CompleteURL-aanvraag:

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/sessionComplete' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionComplete",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

De geslaagde reactie geeft de status 200 aan en bevat geen inhoud.

## Antwoordcodes

In de volgende tabel worden de mogelijke responscodes weergegeven die het gevolg zijn van de verzoeken van de Media Edge API:

| Status | Beschrijving |
| ---------- | --------- |
| 200 | Sessie is gemaakt |
| 207 | Probleem met één van de diensten die met het Netwerk van de Rand van de Ervaring verbinden (zie meer in de het oplossen van problemen gids) |
| 400-niveau | Ongeldig verzoek |
| 500-niveau | Serverfout |

Raadpleeg de handleiding voor het oplossen van problemen in Media Edge voor meer informatie over het verwerken van fouten en mislukte responscodes.


