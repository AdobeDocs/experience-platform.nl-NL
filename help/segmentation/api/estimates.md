---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Schattingen
topic: developer guide
translation-type: tm+mt
source-git-commit: 16ebff522c5b08e4c100f5d2f972ef4db64656a7

---


# Schattingen

intro

- De resultaten van een specifieke geschatte taak ophalen

## Aan de slag

De API-eindpunten die in deze handleiding worden gebruikt, maken deel uit van de segmentatie-API. Lees de ontwikkelaarsgids voor [segmentatie voordat u verdergaat](./getting-started.md).

In het bijzonder, omvat de [begonnen sectie](./getting-started.md#getting-started) van de de ontwikkelaarsgids van de Segmentatie verbindingen aan verwante onderwerpen, een gids aan het lezen van de steekproefAPI vraag in het document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welke API van het Platform van de Ervaring met succes te maken.

## De resultaten van een specifieke geschatte taak ophalen

U kunt details van een specifieke ramingstaak terugwinnen door een GET verzoek aan het `/estimate` eindpunt te doen en de `id` waarde van de ramingstaak in de verzoekweg te verstrekken.

**API-indeling**

```http
GET /estimate/{PREVIEW_ID}
```

- `{PREVIEW_ID}`: De `id` waarde van de geschatte taak die u wilt ophalen.

**Verzoek**

Het volgende verzoek wint de resultaten van een specifieke ramingstaak terug.

//hebt een voorbeeld-id nodig

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/{PREVIEW_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie retourneert HTTP status 200 met details van de geschatte taak.

```json
{
  "estimatedSize": 0,
  "numRowsToRead": 1,
  "state": "RESULT_READY",
  "profilesReadSoFar": 1,
  "standardError": 0,
  "error": {
    "description": "",
    "traceback": ""
  },
  "profilesMatchedSoFar": 0,
  "totalRows": 1,
  "confidenceInterval": "95%",
  "_links": {
    "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
  }
}
```

## Volgende stappen

Nu u weet hoe u de geschatte resultaten van de baan kunt terugwinnen, kunt u beter