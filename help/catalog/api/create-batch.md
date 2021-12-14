---
keywords: Experience Platform;home;populaire onderwerpen;batch maken;catalogusservice;api
solution: Experience Platform
title: Een batch maken in de API
topic-legacy: developer guide
description: U kunt een partij tot stand brengen door een verzoek van de POST aan het /batches eindpunt in de Catalogus API te doen.
exl-id: 1d2cbca9-1cd6-4b89-9b77-3687268bd849
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# Een batch maken

Opdat een dataset gegevens inneemt, moet het een partij hebben verbonden aan het. Met de `id` waarde van een bestaande dataset, kunt u een partij tot stand brengen door een verzoek van de POST aan de `/batches` in de [!DNL Catalog] API.

**API-indeling**

```HTTP
POST /batches
```

**Verzoek**

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `datasetId` | De `id` van de dataset zal de partij met worden geassocieerd. |

**Antwoord**

Een geslaagde reactie retourneert HTTP Status 201 (Gemaakt) en een reactieobject met details van de nieuwe batch, inclusief de nieuwe batch `id`, een alleen-lezen tekenreeks die door het systeem wordt gegenereerd.

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{IMS_ORG}",
    "updated": 1552694873602,
    "status": "loading",
    "created": 1552694873602,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "5c8c3c555033b814b69f947f"
        }
    ],
    "version": "1.0.0",
    "tags": {
        "acp_producer": [
            "{CREATED_CLIENT}"
        ],
        "acp_stagePath": [
            "{CREATED_CLIENT}/stage/5d01230fc78a4e4f8c0c6b387b4b8d1c"
        ],
        "use_plan_b_batch_status": [
            "false"
        ]
    },
    "createdUser": "{CREATED_BY}",
    "updatedUser": "{CREATED_BY}",
    "externalId": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "createdClient": "{CREATED_CLIENT}",
    "inputFormat": {
        "format": "parquet"
    }
}
```
