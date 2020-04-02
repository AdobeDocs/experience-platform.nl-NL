---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Voorvertoningen
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# Handleiding voor ontwikkelaars voorvertoningen

intro

- Een nieuwe voorvertoning maken
- De resultaten van een specifieke voorvertoning ophalen
- Een specifieke voorvertoning annuleren of verwijderen

## Aan de slag

De API-eindpunten die in deze handleiding worden gebruikt, maken deel uit van de segmentatie-API. Lees de ontwikkelaarsgids voor [segmentatie voordat u verdergaat](./getting-started.md).

In het bijzonder, omvat de [begonnen sectie](./getting-started.md#getting-started) van de de ontwikkelaarsgids van de Segmentatie verbindingen aan verwante onderwerpen, een gids aan het lezen van de steekproefAPI vraag in het document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welke API van het Platform van de Ervaring met succes te maken.

## Een nieuwe voorvertoning maken

U kunt een nieuwe voorproef tot stand brengen door een POST- verzoek aan het `/preview` eindpunt te maken.

**API-indeling**

```http
POST /preview
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
  "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
  "predicateType": "pql/text",
  "predicateModel": "_xdm.context.profile",
  "graphType": "pdg"
}
 '
```

hoofdinformatie

**Antwoord**

Een succesvol antwoord retourneert HTTP-status 201 (Gemaakt) met details van de zojuist gemaakte voorvertoning.

```json
{
  "state": "NEW",
  "previewQueryId": "e890068b-f5ca-4a8f-a6b5-af87ff0caac3",
  "previewQueryStatus": "NEW",
  "previewId": "MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow",
  "previewExecutionId": 0
}
```

response info, x-location bestaat niet.

## De resultaten van een specifieke voorvertoning ophalen

U kunt gedetailleerde informatie over een specifieke voorproef terugwinnen door een GET verzoek aan het `/preview` eindpunt te doen en de `id` waarde van de voorproef in de verzoekweg te verstrekken.

**API-indeling**

```http
GET /preview/{PREVIEW_ID}
```

- `{PREVIEW_ID}`: De `id` waarde van de voorvertoning die u wilt ophalen.

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 met gedetailleerde informatie over de opgegeven voorvertoning.

```json
{
  "state": "RESULT_READY",
  "page": {
    "offset": 0,
    "size": 0
  },
  "results": [],
  "link": {
    "nextPage": ""
  },
  "previewSampledResultsCount": 0
}
```

## Een specifieke voorvertoning annuleren of verwijderen

U kunt een specifieke voorproef schrappen door een verzoek van de SCHRAPPING aan het `/preview` eindpunt te doen en door de `id` waarde van de voorproef in de verzoekweg te verstrekken.

**API-indeling**

```http
DELETE /preview/{PREVIEW_ID}
```

- `{PREVIEW_ID}` De `id` waarde van de voorvertoning die u wilt verwijderen.

**Verzoek**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie retourneert HTTP status 200 met het volgende bericht:

```json
{
  "status": true,
  "message": "KILLED"
}
```

## Volgende stappen
