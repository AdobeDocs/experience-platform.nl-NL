---
keywords: Experience Platform;home;populaire onderwerpen;update-sandbox
solution: Experience Platform
title: Een sandbox bijwerken in de API
topic: developer guide
description: U kunt een of meer velden in een sandbox bijwerken door een PATCH-aanvraag in te dienen die de naam van de sandbox bevat in het aanvraagpad en de eigenschap die moet worden bijgewerkt in de aanvraaglading.
translation-type: tm+mt
source-git-commit: 62ce5ac92d03a6e85589fc92e8d953f7fc1d8f31
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# Een sandbox in de API bijwerken

U kunt een of meer velden in een sandbox bijwerken door een PATCH-verzoek in te dienen dat de sandbox `name` bevat in het aanvraagpad en de eigenschap die moet worden bijgewerkt in de aanvraaglading.

>[!NOTE]
>
>Momenteel kan alleen de eigenschap `title` van een sandbox worden bijgewerkt.

**API-indeling**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SANDBOX_NAME}` | De eigenschap `name` van de sandbox die u wilt bijwerken. |

**Verzoek**

Met het volgende verzoek wordt de eigenschap `title` van de sandbox met de naam &quot;dev-2&quot; bijgewerkt.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "title": "Development B"
  }'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 (OK) met de details van de zojuist bijgewerkte sandbox.

```json
{
    "name": "dev-2",
    "title": "Development B",
    "state": "active",
    "type": "development",
    "region": "VA7"
}
```
