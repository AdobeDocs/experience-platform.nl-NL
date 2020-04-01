---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een sandbox verwijderen
topic: developer guide
translation-type: tm+mt
source-git-commit: 974e93b1c24493734848151b9be00758f6a84578

---


# Een sandbox verwijderen

U kunt een sandbox verwijderen door een DELETE-aanvraag in te dienen die de sandbox&#39;s bevat `name` in het aanvraagpad.

>[!NOTE] Als u deze API-aanroep maakt, wordt de `status` eigenschap van de sandbox bijgewerkt naar &quot;verwijderd&quot; en gedeactiveerd. Met GET-aanvragen kunnen de details van de sandbox nog steeds worden opgehaald nadat deze zijn verwijderd.

**API-indeling**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SANDBOX_NAME}` | De `name` sandbox die u wilt verwijderen. |

**Verzoek**

Met het volgende verzoek wordt een sandbox met de naam &quot;dev-2&quot; verwijderd.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvol antwoord retourneert de bijgewerkte details van de sandbox, waarbij wordt getoond dat het `state` is &quot;verwijderd&quot;.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
