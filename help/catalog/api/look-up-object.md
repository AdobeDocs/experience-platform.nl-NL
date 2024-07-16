---
keywords: Experience Platform;home;populaire onderwerpen;catalogus;objectzoekopdracht;api
solution: Experience Platform
title: Een catalogusobject opzoeken
description: Als u de unieke id voor een specifiek catalogusobject kent, kunt u een verzoek uitvoeren om de details van dat object weer te geven.
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
source-git-commit: 0331b6bbd22255cab92c93070dda1ffaed5bbbcb
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Een catalogusobject opzoeken

Als u de unieke id voor een specifiek [!DNL Catalog] -object kent, kunt u een GET-aanvraag uitvoeren om de details van dat object weer te geven.

>[!NOTE]
>
>Wanneer het bekijken van specifieke voorwerpen, is het nog beste praktijken aan [ filter door eigenschappen ](filter-data.md) en terugkeer slechts de eigenschappen u geinteresseerd bent in.

**API formaat**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type [!DNL Catalog] -object dat moet worden opgehaald. Geldige objecten zijn: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | De id van het specifieke object dat u wilt ophalen. |

**Verzoek**

Met de volgende aanvraag wordt een gegevensset opgehaald op basis van de id en worden de eigenschappen `name` , `description` , `tags` en `files` geretourneerd.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie keert de gespecificeerde dataset met slechts gevraagde `properties` in het lichaam terug.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset",
        "description": "Sample dataset containing important data.",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    }
}
```

>[!NOTE]
>
>Eigenschappen waarvan de waarden vooraf met `@` zijn ingesteld, vertegenwoordigen onderling verwante objecten. Zie de appendix sectie op [ het bekijken van onderling verwant voorwerpen ](appendix.md#view-interrelated-objects) voor stappen op hoe te om de details van deze voorwerpen te bekijken.
