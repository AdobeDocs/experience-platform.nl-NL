---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een sandbox bijwerken
topic: developer guide
translation-type: tm+mt
source-git-commit: 974e93b1c24493734848151b9be00758f6a84578

---


# Een sandbox bijwerken

U kunt een of meer velden in een sandbox bijwerken door een PATCH-aanvraag in te dienen die de sandbox in het aanvraagpad en de eigenschap bevat die moeten worden bijgewerkt in de aanvraaglading. `name`

>[!NOTE] Momenteel kan alleen de `title` eigenschap van een sandbox worden bijgewerkt.

**API-indeling**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SANDBOX_NAME}` | De `name` eigenschap van de sandbox die u wilt bijwerken. |

**Verzoek**

Met de volgende aanvraag wordt de `title` eigenschap van de sandbox met de naam &quot;dev-2&quot; bijgewerkt.

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
