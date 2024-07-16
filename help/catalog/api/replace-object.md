---
keywords: Experience Platform;home;populaire onderwerpen;catalogus;api;een object vervangen
solution: Experience Platform
title: Een catalogusobject vervangen
description: U kunt de inhoud van een voorwerp van de Catalogus beschrijven gebruikend een verzoek van de PUT, waar het volledige middel met de verzoeklading wordt vervangen.
exl-id: cd98d13c-5261-4bff-b5db-af5f06d093c9
source-git-commit: 2d6167ee7aaa0b79514be6e532e61602ae5cc640
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# Een catalogusobject vervangen

U kunt de inhoud van een [!DNL Catalog] -object overschrijven met behulp van een verzoek om PUT, waarbij de volledige bron wordt vervangen door de payload van de aanvraag.

>[!NOTE]
>
>Als u slechts een paar specifieke gebieden binnen een voorwerp [!DNL Catalog] moet bijwerken, kan het gebruiken van een verzoek van de PATCH efficiënter zijn.

**API formaat**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type [!DNL Catalog] -object dat moet worden vervangen. Geldige objecten zijn: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
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
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    }'
```

**Reactie**

Een geslaagde reactie retourneert een array die de id van het overschreven object bevat. Deze id moet overeenkomen met de id die in de aanvraag voor PUT is verzonden. Wanneer u een GET-verzoek voor dit object uitvoert, wordt nu aangegeven dat de gegevens zijn vervangen door de gegevens die zijn opgegeven in de payload van het vorige verzoek om PUT.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
