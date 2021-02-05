---
keywords: Experience Platform;home;populaire onderwerpen;lijstsandboxen
solution: Experience Platform
title: Ondersteunde sandboxtypen weergeven in de API
topic: developer guide
description: U kunt een lijst van gesteunde zandbaktypes voor uw organisatie terugwinnen door een verzoek van de GET aan het /sandboxTypes eindpunt te richten.
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 0%

---


# Ondersteunde sandboxtypen weergeven in de API

U kunt een lijst van gesteunde zandbaktypes voor uw organisatie terugwinnen door een verzoek van de GET tot het `/sandboxTypes` eindpunt te richten.

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
