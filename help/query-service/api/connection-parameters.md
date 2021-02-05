---
keywords: Experience Platform;thuis;populaire onderwerpen;de vraagdienst;api gids;verbindingsparameters;de dienst van de vraag;
solution: Experience Platform
title: API-eindpunt voor verbindingsparameters
topic: connection parameters
description: U kunt uw verbindingsparameters voor het gebruiken van de interactieve dienst terugwinnen door een verzoek van de GET aan het /connection_parameters eindpunt te doen.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---


# Het eindpunt van de verbindingsparameters

## Voorbeeld-API-aanroepen

Nu u begrijpt welke kopballen aan gebruik, bent u bereid beginnen het richten vraag aan [!DNL Query Service] API. De volgende secties lopen door de diverse API vraag u kan maken gebruikend [!DNL Query Service] API. Elke vraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen toont, en een steekproefreactie.

### Verbindingsparameters aanvragen

U kunt uw verbindingsparameters terugwinnen door een verzoek van de GET aan het `/connection_parameters` eindpunt te doen. Voor meer informatie over cliënten die verbindingsparameters gebruiken om via de interactieve dienst te verbinden, gelieve de documentatie op [de cliënten van de Dienst van de Vraag](../clients/overview.md) te lezen.

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
