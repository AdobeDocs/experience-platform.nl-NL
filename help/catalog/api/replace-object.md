---
keywords: Experience Platform;home;populaire onderwerpen;catalogus;api;een object vervangen
solution: Experience Platform
title: Een catalogusobject vervangen
topic: developer guide
description: U kunt de inhoud van een voorwerp van de Catalogus beschrijven gebruikend een verzoek van de PUT, waar het volledige middel met de verzoeklading wordt vervangen.
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# Een catalogusobject vervangen

U kunt de inhoud van een [!DNL Catalog] voorwerp beschrijven gebruikend een verzoek van de PUT, waar het volledige middel met de verzoeklading wordt vervangen.

>[!NOTE]
>
>Als u slechts een paar specifieke gebieden binnen een [!DNL Catalog] voorwerp moet bijwerken, kan het gebruiken van een verzoek van de PATCH efficiënter zijn.

**API-indeling**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type van [!DNL Catalog] te vervangen voorwerp. Geldige objecten zijn: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | De id van het specifieke object dat u wilt bijwerken. |

**Verzoek**

Het volgende verzoek beschrijft een dataset met de waarden die in de nuttige lading worden verstrekt.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "New Dataset Name",
        "description": "New description for dataset",
        "state": "DRAFT",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    }'
```

**Antwoord**

Een geslaagde reactie retourneert een array met de id van het overschreven object. Deze id moet overeenkomen met de id die in de aanvraag voor PUT is verzonden. Wanneer u een GET-verzoek voor dit object uitvoert, wordt nu aangegeven dat de gegevens zijn vervangen door de gegevens die zijn opgegeven in de payload van het vorige verzoek om PUT.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
