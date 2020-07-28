---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Meerdere objecten opzoeken
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# Meerdere objecten opzoeken

Als u meerdere specifieke objecten wilt weergeven in plaats van één aanvraag per object te maken, [!DNL Catalog] biedt u een eenvoudige sneltoets voor het aanvragen van meerdere objecten van hetzelfde type. U kunt één aanvraag voor GET gebruiken om meerdere specifieke objecten te retourneren door een lijst met id&#39;s met komma&#39;s als scheidingsteken op te nemen.

>[!NOTE]
>
>Zelfs wanneer het verzoeken van om specifieke [!DNL Catalog] voorwerpen, is het nog beste praktijken om parameter te `properties` vragen om slechts de eigenschappen terug te keren u wenst.

**API-indeling**

```http
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| `{OBJECT_TYPE}` | Het type [!DNL Catalog] object dat moet worden opgehaald. Geldige objecten zijn: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{ID}` | Een id voor een van de specifieke objecten die u wilt ophalen. |

**Verzoek**

Het volgende verzoek omvat een komma-gescheiden lijst van dataset IDs evenals een komma-gescheiden lijst van eigenschappen die voor elke dataset moeten zijn teruggekeerd.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5bde21511dd27b0000d24e95,5bda3a4228babc0000126377,5bceaa4c26c115000039b24b,5bb276b03a14440000971552,5ba9452f7de80400007fc52a?properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert een lijst van de gespecificeerde datasets terug, die slechts de gevraagde eigenschappen (`name`, `description`, en `files`) voor elk bevatten.

>[!NOTE]
>
>Als een geretourneerd object niet meer van de gevraagde eigenschappen bevat die door de `properties` query worden aangegeven, retourneert het antwoord alleen de gevraagde eigenschappen die het wel bevat, zoals weergegeven in ***`Sample Dataset 3`*** en ***`Sample Dataset 4`*** hieronder.

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
