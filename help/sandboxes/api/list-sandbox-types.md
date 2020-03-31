---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Ondersteunde sandboxtypen weergeven
topic: developer guide
translation-type: tm+mt
source-git-commit: b4741cdfd065bbaed7f2feeafe8619191e4b8f6c

---


# Ondersteunde sandboxtypen weergeven

U kunt een lijst van gesteunde zandbaktypes voor uw organisatie terugwinnen door een GET verzoek aan het `/sandboxTypes` eindpunt te doen.

**API-indeling**

```http
GET /sandboxTypes
```

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxTypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert een lijst met sandboxtypen die worden ondersteund voor uw organisatie.

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
