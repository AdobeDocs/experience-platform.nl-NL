---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een gegevensset maken
topic: developer guide
translation-type: tm+mt
source-git-commit: 6d24637dc6cc282f98288b6416e4a3b7cebe42ea

---


# Een gegevensset maken

Om een dataset tot stand te brengen die de Catalogus API gebruikt, moet u de `$id` waarde van het schema van de Gegevens van de Ervaring kennen het Model (XDM) waarop de dataset zal worden gebaseerd. Zodra u schema identiteitskaart hebt, kunt u een dataset tot stand brengen door een POST- verzoek aan het `/datasets` eindpunt in de Catalogus API te doen.

>[!NOTE] Dit document behandelt slechts hoe te om een datasetvoorwerp in Catalog tot stand te brengen. Voor volledige stappen op om, te creëren bevolken en te controleren een dataset, gelieve te verwijzen naar het volgende [leerprogramma](../datasets/create.md).

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

>[!NOTE] In dit voorbeeld wordt de bestandsindeling [parket](https://parquet.apache.org/documentation/latest/) voor de `containerFormat` eigenschap gebruikt. Een voorbeeld dat de JSON-bestandsindeling gebruikt, vindt u in de ontwikkelaarshandleiding voor [batchinvoer](../../ingestion/batch-ingestion/api-overview.md).

**Antwoord**

Een geslaagde reactie retourneert HTTP Status 201 (Gemaakt) en een reactieobject dat bestaat uit een array met de id van de nieuwe dataset in de indeling `"@/datasets/{DATASET_ID}"`. De dataset ID is een read-only, systeem-geproduceerde koord dat wordt gebruikt om de dataset in API vraag van verwijzingen te voorzien.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
