---
keywords: Experience Platform;thuis;populaire onderwerpen;de vraagdienst;api gids;verbindingsparameters;de dienst van de vraag;
solution: Experience Platform
title: API-eindpunt voor verbindingsparameters
topic-legacy: connection parameters
description: U kunt uw verbindingsparameters voor het gebruiken van de interactieve dienst terugwinnen door een verzoek van de GET aan het /connection_parameters eindpunt te doen.
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# Het eindpunt van de verbindingsparameters

## Voorbeeld-API-aanroep

In de volgende sectie wordt u door de API-aanroep geleid die u kunt maken met de [!DNL Query Service] API. De aanroep omvat de algemene API-indeling, een voorbeeldaanvraag met de vereiste headers en een voorbeeldreactie.

### Verbindingsparameters aanvragen

U kunt uw verbindingsparameters terugwinnen door een verzoek van de GET aan `/connection_parameters` eindpunt. Voor meer informatie over clients die gebruikmaken van verbindingsparameters voor verbinding via de interactieve service, raadpleegt u de documentatie over [Query Service-clients](../clients/overview.md).

**API-indeling**

```http
GET /connection_parameters
```

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/connection_parameters
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 met de verbindingsparameters.

```json
{
    "username": "{USERNAME}",
    "dbName": "prod:all",
    "host": "{HOSTNAME}",
    "version": 1,
    "port": 80,
    "token": "{TOKEN}",
    "compressedToken": "{COMPRESSED_TOKEN}",
    "websocketHost": "{WEBSOCKET_HOSTNAME}"
}
```
