---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een object opzoeken
topic: developer guide
translation-type: tm+mt
source-git-commit: 4dcd174eda98fee1e8cf668819809bd061c6e8bb

---


# Een object opzoeken

Als u de unieke id voor een specifiek catalogusobject kent, kunt u een aanvraag GET uitvoeren om de details van dat object weer te geven.

>[!NOTE] Wanneer u specifieke objecten weergeeft, kunt u het beste alleen [filteren op eigenschappen](filter-data.md) en alleen de gewenste eigenschappen retourneren.

**API-indeling**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type Catalog-object dat moet worden opgehaald. Geldige objecten zijn: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | De id van het specifieke object dat u wilt ophalen. |

**Verzoek**

Het volgende verzoek wint een dataset door zijn identiteitskaart terug, terugkerend zijn `name`, `description`, `state`, `tags`, en `files` eigenschappen.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert de gespecificeerde dataset met slechts het gevraagde `properties` lichaam terug.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset",
        "description": "Sample dataset containing important data.",
        "state": "DRAFT",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    }
}
```

>[!NOTE] Eigenschappen waarvan de waarden worden voorafgegaan door `@` vertegenwoordigen onderling verwante objecten. Zie de sectie in de bijlage over het [weergeven van onderling verwante objecten](appendix.md#view-interrelated-objects) voor stappen over het weergeven van de details van deze objecten.
