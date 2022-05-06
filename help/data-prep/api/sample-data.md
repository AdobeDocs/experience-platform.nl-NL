---
keywords: Experience Platform;thuis;populaire onderwerpen;gegevens prep;api gids;steekproefgegevens;
solution: Experience Platform
title: API-eindpunt voor voorbeeldgegevens
topic-legacy: sample data
description: 'U kunt het `-/steekproeven'' eindpunt in Adobe Experience Platform API gebruiken om kaartsteekproefgegevens programmatically terug te winnen, tot stand te brengen bij te werken en te bevestigen. '
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---


# Gegevenseindpunt van sample

Voorbeeldgegevens kunnen worden gebruikt bij het maken van een schema voor uw toewijzingsset. U kunt de `/samples` eindpunt in de Prep API van Gegevens om programmatically steekproefgegevens terug te winnen, tot stand te brengen en bij te werken.

## Voorbeeldgegevens weergeven

U kunt een lijst van alle gegevens van de toewijzingssteekproef voor uw IMS Organisatie terugwinnen door een verzoek van de GET aan te richten `/samples` eindpunt.

**API-indeling**

De `/samples` het eindpunt steunt verscheidene vraagparameters helpen uw resultaten filtreren. U moet op dit moment beide opties opnemen `start` en `limit` -parameters als onderdeel van uw verzoek.

```http
GET /samples?limit={LIMIT}&start={START}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{LIMIT}` | **Vereist**. Hiermee geeft u het aantal geretourneerde gegevens van het toewijzingsvoorbeeld op. |
| `{START}` | **Vereist**. Hiermee bepaalt u de verschuiving van de resultatenpagina&#39;s. Als u de eerste pagina met resultaten wilt ophalen, stelt u de waarde in op `start=0`. |

**Verzoek**

Met het volgende verzoek worden de laatste twee voorbeeldgegevens van de toewijzing binnen uw IMS-organisatie opgehaald.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples?limit=2&start=0 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 met informatie over de laatste twee objecten van de voorbeeldgegevens van de toewijzing.

```json
{
    "data": [
        {
            "id": "2a429a0057ce47109a4b3e2bc256d755",
            "version": 0,
            "createdDate": 1582250863000,
            "modifiedDate": 1582250863000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_xql_gateway",
            "sampleData": "{\"id\":\"\",\"first_name\":\"\",\"last_name\":\"\",\"email\":\"\",\"gender\":\"\",\"ip_address\":\"\"}",
            "sampleType": "JSON"
        },
        {
            "id": "0248bfb352214f908bdd6cf9c19447e1",
            "version": 0,
            "createdDate": 1582250892000,
            "modifiedDate": 1582250892000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_xql_gateway",
            "sampleData": "{\"id\":\"\",\"first_name\":\"\",\"last_name\":\"\",\"email\":\"\",\"gender\":\"\",\"ip_address\":\"\"}",
            "sampleType": "JSON"
        }
    ],
    "_page": {
        "count": 2,
        "limit": 2
    }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `sampleData` |  |
| `sampleType` |  |

## Voorbeeldgegevens maken

U kunt voorbeeldgegevens maken door een POST aan te vragen bij de `/samples` eindpunt.

```http
POST /samples
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/samples \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Smith\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 met informatie over de nieuwe voorbeeldgegevens.

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 0,
    "createdDate": 1615335404492,
    "modifiedDate": 1615335404492,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## Voorbeeldgegevens maken door een bestand te uploaden

U kunt voorbeeldgegevens maken met behulp van een bestand door een POST aan te vragen bij de `/samples/upload` eindpunt.

**API-indeling**

```http
POST /samples/upload
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/samples \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: multipart/form-data' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -F 'file=@{PATH_TO_FILE}.json'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 met informatie over de nieuwe voorbeeldgegevens.

```json
{
    "id": "1fb33209ed126bdcdc0b6c20bae49d8a",
    "version": 0,
    "createdDate": 1615335404492,
    "modifiedDate": 1615335404492,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## Een specifiek voorbeeldgegevensobject opzoeken

U kunt een specifiek voorwerp van steekproefgegevens opzoeken door zijn identiteitskaart in de weg van een verzoek van de GET aan te verstrekken `/samples` eindpunt.

**API-indeling**

```http
GET /samples/{SAMPLE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{SAMPLE_ID}` | De id van het voorbeeldgegevensobject dat u wilt ophalen. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 met informatie over het voorbeeldgegevensobject dat u wilt ophalen.

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 0,
    "createdDate": 1615335404000,
    "modifiedDate": 1615335404000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## Voorbeeldgegevens bijwerken

U kunt een specifiek voorbeeldgegevensobject bijwerken door de id ervan op te geven in het pad van een verzoek van de PUT aan de `/samples` eindpunt.

**API-indeling**

```http
PUT /samples/{SAMPLE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{SAMPLE_ID}` | De id van het voorbeeldgegevensobject dat u wilt bijwerken. |

**Verzoek**

Met het volgende verzoek worden de opgegeven voorbeeldgegevens bijgewerkt. Specifiek, werkt het de achternaam van &quot;Smith&quot;in &quot;Lee&quot;bij.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Lee\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 met informatie over de bijgewerkte voorbeeldgegevens.

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 1,
    "createdDate": 1615335404000,
    "modifiedDate": 1615337870375,
    "createdBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "modifiedBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Lee\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```
