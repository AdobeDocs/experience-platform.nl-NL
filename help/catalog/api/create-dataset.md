---
keywords: Experience Platform;home;popular topics;dataset;Dataset;create a dataset;create dataset;enable dataset
solution: Experience Platform
title: Een gegevensset maken
topic: developer guide
description: In dit document wordt beschreven hoe u een gegevenssetobject maakt in Catalog.
translation-type: tm+mt
source-git-commit: bf99b08a1093a815687cc06372407949e170a0b3
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# Een gegevensset maken

Om een dataset tot stand te brengen gebruikend [!DNL Catalog] API, moet u de `$id` waarde van het schema [!DNL Experience Data Model] (XDM) kennen waarop de dataset zal worden gebaseerd. Zodra u schema identiteitskaart hebt, kunt u een dataset tot stand brengen door een verzoek van de POST aan het `/datasets` eindpunt in [!DNL Catalog] API te doen.

>[!NOTE]
>
>In dit document wordt alleen beschreven hoe u een gegevenssetobject maakt in [!DNL Catalog]. Voor volledige stappen op om, te creëren bevolken en te controleren een dataset, gelieve te verwijzen naar het volgende [leerprogramma](../datasets/create.md).

**API-indeling**

```HTTP
POST /dataSets
```

**Verzoek**

Het volgende verzoek leidt tot een dataset die verwijzingen een eerder bepaald schema.

```SHELL
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van de gegevensset die moet worden gemaakt. |
| `schemaRef.id` | De URI- `$id` waarde voor het XDM-schema waarop de gegevensset wordt gebaseerd. |

>[!NOTE]
>
>In dit voorbeeld wordt de bestandsindeling [parket](https://parquet.apache.org/documentation/latest/) voor de `containerFormat` eigenschap gebruikt. Een voorbeeld dat de JSON-bestandsindeling gebruikt, vindt u in de ontwikkelaarshandleiding voor [batchinvoer](../../ingestion/batch-ingestion/api-overview.md).

**Antwoord**

Een geslaagde reactie retourneert HTTP Status 201 (Gemaakt) en een reactieobject dat bestaat uit een array met de id van de nieuwe dataset in de indeling `"@/datasets/{DATASET_ID}"`. De dataset ID is een read-only, systeem-geproduceerde koord dat wordt gebruikt om de dataset in API vraag van verwijzingen te voorzien.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
