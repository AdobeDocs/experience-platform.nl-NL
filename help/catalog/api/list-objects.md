---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Objecten weergeven
topic: developer guide
translation-type: tm+mt
source-git-commit: 71c73a3899ccdd1c024a811b36c411915a3b14be

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
| `{OBJECT_TYPE}` | Het type Catalog-object dat moet worden weergegeven. Geldige objecten zijn: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
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

Een succesvolle reactie keert een lijst van de voorwerpen van de Catalogus in de vorm van sleutel-waarde paren terug, die door de vraagparameters worden gefiltreerd die in het verzoek worden verstrekt. Voor elk sleutel-waardepaar, vertegenwoordigt de sleutel een uniek herkenningsteken voor het voorwerp van de Catalogus in kwestie, dat dan in een andere vraag kan worden gebruikt om dat specifieke voorwerp [voor meer details te](look-up-object.md) bekijken.

>[!NOTE] Als een teruggekeerd voorwerp één of meerdere gevraagde eigenschappen niet bevat die door de `properties` vraag worden vermeld, keert de reactie slechts de gevraagde eigenschappen terug die het omvat, zoals aangetoond in &quot;Gegevensset 3 van de Steekproef&quot;en &quot;Dataset 4 van de Steekproef hieronder.

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
