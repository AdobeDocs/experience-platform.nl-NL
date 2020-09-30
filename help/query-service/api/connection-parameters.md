---
keywords: Experience Platform;home;popular topics;query service;api guide;connection parameters;Query service;
solution: Experience Platform
title: Handleiding voor ontwikkelaars van Query Service
topic: connection parameters
description: U kunt uw verbindingsparameters voor het gebruiken van de interactieve dienst terugwinnen door een verzoek van de GET aan het /connection_parameters eindpunt te doen.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Verbindingsparameters

## Voorbeeld-API-aanroepen

Nu u begrijpt welke kopballen aan gebruik, bent u bereid beginnen het voeren van vraag aan [!DNL Query Service] API. De volgende secties lopen door diverse API vraag u kunt maken gebruikend [!DNL Query Service] API. Elke vraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen toont, en een steekproefreactie.

### Verbindingsparameters aanvragen voor de interactieve service

U kunt uw verbindingsparameters voor het gebruiken van de [interactieve dienst](../creating-queries/writing-queries.md) terugwinnen door een verzoek van de GET aan het `/connection_parameters` eindpunt te doen. Voor meer informatie over cliënten die verbindingsparameters gebruiken om via de interactieve dienst te verbinden, gelieve de documentatie op de cliënten [van de Dienst van de](../clients/overview.md)Vraag te lezen.

**API-indeling**

```http
GET /connection_parameters
```

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/connection_parameters
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
