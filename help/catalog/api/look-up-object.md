---
keywords: Experience Platform;home;populaire onderwerpen;catalogus;objectzoekopdracht;api
solution: Experience Platform
title: Een catalogusobject opzoeken
topic: developer guide
description: 'Als u de unieke id voor een specifiek catalogusobject kent, kunt u een verzoek uitvoeren om de details van dat object weer te geven. '
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# Een catalogusobject opzoeken

Als u de unieke id voor een specifiek [!DNL Catalog]-object kent, kunt u een verzoek tot GET uitvoeren om de details van dat object weer te geven.

>[!NOTE]
>
>Wanneer het bekijken van specifieke voorwerpen, is het nog beste praktijken om [filter door eigenschappen ](filter-data.md) te filteren en slechts de eigenschappen terug te keren u in geinteresseerd bent.

**API-indeling**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type object dat moet worden opgehaald. [!DNL Catalog] Geldige objecten zijn: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | De id van het specifieke object dat u wilt ophalen. |

**Verzoek**

Met het volgende verzoek wordt een gegevensset opgehaald op basis van de id en worden de eigenschappen `name`, `description`, `state`, `tags` en `files` geretourneerd.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert de gespecificeerde dataset met slechts gevraagde `properties` in het lichaam terug.

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

>[!NOTE]
>
>Eigenschappen waarvan de waarden worden voorgefixeerd met `@` vertegenwoordigen onderling verwante objecten. Zie de sectie in de bijlage over [het weergeven van onderling verwante objecten](appendix.md#view-interrelated-objects) voor stappen over het weergeven van de details van deze objecten.
