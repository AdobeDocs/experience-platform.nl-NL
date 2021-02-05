---
keywords: Experience Platform;home;populaire onderwerpen;filter;Filter;filtergegevens;Filter gegevens
solution: Experience Platform
title: Catalogusobjecten weergeven
topic: developer guide
description: U kunt een lijst van alle beschikbare voorwerpen van een specifiek type door één enkele API vraag terugwinnen, met beste praktijken die filters omvatten die de grootte van de reactie beperken.
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Catalogusobjecten weergeven

U kunt een lijst van alle beschikbare voorwerpen van een specifiek type door één enkele API vraag terugwinnen, met beste praktijken die filters omvatten die de grootte van de reactie beperken.

**API-indeling**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type object dat moet worden vermeld. [!DNL Catalog] Geldige objecten zijn: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{FILTER}` | Een queryparameter die wordt gebruikt om de resultaten te filteren die in de reactie worden geretourneerd. De veelvoudige parameters worden gescheiden door ampersands (`&`). Zie de gids op [het filtreren gegevens van de Catalogus](filter-data.md) voor meer informatie. |

**Verzoek**

Het steekproefverzoek wint hieronder een lijst van datasets, met een `limit` filter terug die de reactie op vijf resultaten vermindert, en een `properties` filter dat de eigenschappen beperkt die voor elke dataset worden getoond.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert een lijst van [!DNL Catalog] voorwerpen in de vorm van sleutel-waarde paren terug, die door de vraagparameters worden gefiltreerd die in het verzoek worden verstrekt. Voor elk zeer belangrijk-waardepaar, vertegenwoordigt de sleutel een uniek herkenningsteken voor het [!DNL Catalog] voorwerp in kwestie, die dan in een andere vraag aan [mening kan worden gebruikt dat specifiek voorwerp](look-up-object.md) voor meer details.

>[!NOTE]
>
>Als een geretourneerd object geen van de gevraagde eigenschappen bevat die door de query `properties` worden aangegeven, retourneert het antwoord alleen de gevraagde eigenschappen die het wel bevat, zoals hieronder in ***`Sample Dataset 3`*** en ***`Sample Dataset 4`*** wordt getoond.

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
