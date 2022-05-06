---
keywords: Experience Platform;home;populaire onderwerpen;catalogus;objectzoekopdracht;api
solution: Experience Platform
title: Een catalogusobject opzoeken
topic-legacy: developer guide
description: Als u de unieke id voor een specifiek catalogusobject kent, kunt u een verzoek uitvoeren om de details van dat object weer te geven.
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Een catalogusobject opzoeken

Als u de unieke id voor een specifieke id kent [!DNL Catalog] kunt u een GET-verzoek uitvoeren om de details van dat object weer te geven.

>[!NOTE]
>
>Bij het weergeven van specifieke objecten is het nog steeds raadzaam [filteren op eigenschappen](filter-data.md) en retourneert alleen de eigenschappen waarin u geïnteresseerd bent.

**API-indeling**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type van [!DNL Catalog] op te halen object. Geldige objecten zijn: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | De id van het specifieke object dat u wilt ophalen. |

**Verzoek**

Het volgende verzoek wint een dataset door zijn identiteitskaart terug, die zijn terugkeert `name`, `description`, `state`, `tags`, en `files` eigenschappen.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvol antwoord keert de gespecificeerde dataset met slechts gevraagde terug `properties` in het lichaam.

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
>Eigenschappen waarvan de waarden vooraf zijn ingesteld op `@` Hiermee worden verwante objecten weergegeven. Zie het aanhangsel over [weergeven, verwante objecten](appendix.md#view-interrelated-objects) voor stappen voor het weergeven van de details van deze objecten.
