---
keywords: Experience Platform;home;populaire onderwerpen;catalogus;api;een object vervangen
solution: Experience Platform
title: Een catalogusobject vervangen
topic-legacy: developer guide
description: U kunt de inhoud van een voorwerp van de Catalogus beschrijven gebruikend een verzoek van de PUT, waar het volledige middel met de verzoeklading wordt vervangen.
exl-id: cd98d13c-5261-4bff-b5db-af5f06d093c9
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# Een catalogusobject vervangen

U kunt de inhoud van een [!DNL Catalog] object dat gebruikmaakt van een verzoek om PUT, waarbij de volledige bron wordt vervangen door de lading van het verzoek.

>[!NOTE]
>
>Als u slechts een paar specifieke gebieden binnen a moet bijwerken [!DNL Catalog] -object, is het gebruik van een PATCH-verzoek wellicht efficiënter.

**API-indeling**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type van [!DNL Catalog] te vervangen object. Geldige objecten zijn: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | De id van het specifieke object dat u wilt bijwerken. |

**Verzoek**

Het volgende verzoek beschrijft een dataset met de waarden die in de nuttige lading worden verstrekt.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
