---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Objecten weergeven
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---


# Objecten weergeven

U kunt een lijst van alle beschikbare voorwerpen van een specifiek type door één enkele API vraag terugwinnen, met beste praktijken die filters omvatten die de grootte van de reactie beperken.

**API-indeling**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type [!DNL Catalog] object dat moet worden weergegeven. Geldige objecten zijn: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{FILTER}` | Een queryparameter die wordt gebruikt om de resultaten te filteren die in de reactie worden geretourneerd. Meerdere parameters worden gescheiden door ampersands (`&`). Zie de handleiding voor het [filteren van catalogusgegevens](filter-data.md) voor meer informatie. |

**Verzoek**

Het steekproefverzoek wint hieronder een lijst van datasets, met een `limit` filter terug die de reactie tot vijf resultaten vermindert, en een `properties` filter dat de eigenschappen beperkt die voor elke dataset worden getoond.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert een lijst met [!DNL Catalog] objecten in de vorm van sleutelwaardeparen, gefilterd door de queryparameters die in de aanvraag zijn opgegeven. Voor elk sleutel-waardepaar, vertegenwoordigt de sleutel een uniek herkenningsteken voor het [!DNL Catalog] voorwerp in kwestie, die dan in een andere vraag kan worden gebruikt om dat specifieke voorwerp [voor meer details te](look-up-object.md) bekijken.

>[!NOTE]
>
>Als een geretourneerd object geen van de gevraagde eigenschappen bevat die door de `properties` query worden aangegeven, retourneert het antwoord alleen de gevraagde eigenschappen die het wel bevat, zoals in ***`Sample Dataset 3`*** en ***`Sample Dataset 4`*** eronder.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bb276b03a14440000971552/views/5bb276b01250b012f9acc75b/files"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    },
    "5bda3a4228babc0000126377": {
        "name": "Sample Dataset 4",
        "files": "@/dataSets/5bda3a4228babc0000126377/views/5bda3a4228babc0000126378/files"
    },
    "5bde21511dd27b0000d24e95": {
        "name": "Sample Dataset 5",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bde21511dd27b0000d24e95/views/5bde21511dd27b0000d24e96/files"
    }
}
```
