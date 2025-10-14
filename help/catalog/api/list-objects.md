---
keywords: Experience Platform;home;populaire onderwerpen;filter;Filter;filtergegevens;Filter gegevens
solution: Experience Platform
title: Catalogusobjecten weergeven
description: U kunt een lijst van alle beschikbare voorwerpen van een specifiek type door één enkele API vraag terugwinnen, met beste praktijken die filters omvatten die de grootte van de reactie beperken.
exl-id: 2c65e2bc-4ddd-445a-a52d-6ceb1153ccea
source-git-commit: 409d052c119814a1cf6b79ff4448d1100b18e199
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# Catalogusobjecten weergeven

U kunt een lijst van alle beschikbare voorwerpen van een specifiek type door één enkele API vraag terugwinnen, met beste praktijken die filters omvatten die de grootte van de reactie beperken.

**API formaat**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type [!DNL Catalog] -object dat moet worden vermeld. Geldige objecten zijn: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{FILTER}` | Een queryparameter die wordt gebruikt om de resultaten te filteren die in de reactie worden geretourneerd. De veelvoudige parameters worden gescheiden door ampersands (`&`). Zie de gids bij [&#x200B; het filtreren gegevens van de Catalogus &#x200B;](filter-data.md) voor meer informatie. |

**Verzoek**

In de voorbeeldaanvraag hieronder wordt een lijst met gegevenssets opgehaald, met een filter `limit` waarmee de respons op vijf resultaten wordt verminderd, en een filter `properties` waarmee de eigenschappen die voor elke gegevensset worden weergegeven, worden beperkt.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert een lijst met [!DNL Catalog] -objecten in de vorm van sleutel-waardeparen, gefilterd op basis van de queryparameters die in de aanvraag zijn opgegeven. Voor elk zeer belangrijk-waardepaar, vertegenwoordigt de sleutel een uniek herkenningsteken voor het [!DNL Catalog] voorwerp in kwestie, dat dan in een andere vraag aan [&#x200B; kan worden gebruikt mening dat specifiek voorwerp &#x200B;](look-up-object.md) voor meer details.

>[!NOTE]
>
>Als een geretourneerd object geen van de gevraagde eigenschappen bevat die door de `properties` -query worden aangegeven, retourneert het antwoord alleen de gevraagde eigenschappen die het wel bevat, zoals hieronder in ***`Sample Dataset 3`*** en ***`Sample Dataset 4`*** wordt getoond.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bb276b03a14440000971552"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    },
    "5bda3a4228babc0000126377": {
        "name": "Sample Dataset 4",
        "files": "@/dataSetFiles?dataSetId=5bda3a4228babc0000126377"
    },
    "5bde21511dd27b0000d24e95": {
        "name": "Sample Dataset 5",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bde21511dd27b0000d24e95"
    }
}
```
