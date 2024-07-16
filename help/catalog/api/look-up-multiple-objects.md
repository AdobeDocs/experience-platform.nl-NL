---
keywords: Experience Platform;home;populaire onderwerpen;catalogus;opzoeken van meerdere objecten;api
solution: Experience Platform
title: Meerdere catalogusobjecten opzoeken
description: Als u meerdere specifieke objecten wilt weergeven in plaats van één aanvraag per object te maken, biedt Catalog een eenvoudige sneltoets voor het aanvragen van meerdere objecten van hetzelfde type. U kunt één aanvraag voor GET gebruiken om meerdere specifieke objecten te retourneren door een lijst met id's met komma's als scheidingsteken op te nemen.
exl-id: b2329b32-6139-4557-aff3-a584e03b09f3
source-git-commit: 99837f7aa803f3f992dce2127089bff6279c7008
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Meerdere catalogusobjecten opzoeken

Als u meerdere specifieke objecten wilt weergeven in plaats van één aanvraag per object uit te voeren, biedt [!DNL Catalog] een eenvoudige sneltoets voor het aanvragen van meerdere objecten van hetzelfde type. U kunt één aanvraag voor GET gebruiken om meerdere specifieke objecten te retourneren door een lijst met id&#39;s met komma&#39;s als scheidingsteken op te nemen.

>[!NOTE]
>
>Zelfs wanneer u specifieke [!DNL Catalog] -objecten aanvraagt, is het nog steeds aan te raden om met de parameter query `properties` alleen de eigenschappen te retourneren die u nodig hebt.

**API formaat**

```http
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{OBJECT_TYPE}` | Het type [!DNL Catalog] -object dat moet worden opgehaald. Geldige objecten zijn: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{ID}` | Een id voor een van de specifieke objecten die u wilt ophalen. |

**Verzoek**

Het volgende verzoek omvat een komma-gescheiden lijst van dataset IDs evenals een komma-gescheiden lijst van eigenschappen die voor elke dataset moeten zijn teruggekeerd.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5bde21511dd27b0000d24e95,5bda3a4228babc0000126377,5bceaa4c26c115000039b24b,5bb276b03a14440000971552,5ba9452f7de80400007fc52a?properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert een lijst met de opgegeven datasets die alleen de gevraagde eigenschappen (`name`, `description` en `files`) voor elke set bevatten.

>[!NOTE]
>
>Als een geretourneerd object niet meer van de gevraagde eigenschappen bevat die door de query `properties` worden aangegeven, retourneert het antwoord alleen de gevraagde eigenschappen die het wel bevat, zoals hieronder in ***`Sample Dataset 3`*** en ***`Sample Dataset 4`*** wordt getoond.

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
