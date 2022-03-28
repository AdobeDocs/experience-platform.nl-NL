---
keywords: Experience Platform;huis;populaire onderwerpen;dataset;Dataset;creeer een dataset;creeer dataset;laat dataset toe
solution: Experience Platform
title: Een gegevensset maken in de API
topic-legacy: developer guide
description: In dit document wordt beschreven hoe u een gegevenssetobject maakt in de API voor catalogusservice.
exl-id: f3e5de7f-1781-4898-ac42-063eb51e661a
source-git-commit: 75426b1ddc16af39eb6c423027fac7d4d0e21c6a
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Een gegevensset maken in de API

Om een dataset tot stand te brengen gebruikend [!DNL Catalog] API, u moet de `$id` waarde van de [!DNL Experience Data Model] (XDM) schema waarop de dataset zal worden gebaseerd. Zodra u schema identiteitskaart hebt, kunt u een dataset tot stand brengen door een verzoek van de POST aan het `/datasets` in de [!DNL Catalog] API.

>[!NOTE]
>
>In dit document wordt alleen beschreven hoe u een gegevenssetobject maakt in [!DNL Catalog]. Voor volledige stappen op om, te creëren bevolken en te controleren een dataset, gelieve te verwijzen naar het volgende [zelfstudie](../datasets/create.md).

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
    }
}'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van de gegevensset die moet worden gemaakt. |
| `schemaRef.id` | De URI `$id` waarde voor het XDM schema de dataset zal worden gebaseerd op. |
| `schemaRef.contentType` | Geeft de indeling en versie van het schema aan. Zie de sectie over [schemaversie](../../xdm/api/getting-started.md#versioning) in de XDM API-handleiding voor meer informatie. |

>[!NOTE]
>
>In dit voorbeeld wordt het [Apache Parquet](https://parquet.apache.org/docs/) bestandsindeling voor `containerFormat` eigenschap. Een voorbeeld met de JSON-bestandsindeling vindt u in het dialoogvenster [handleiding voor het ontwikkelen van batch-inhoud](../../ingestion/batch-ingestion/api-overview.md).

**Antwoord**

Een geslaagde reactie retourneert HTTP Status 201 (Gemaakt) en een reactieobject dat bestaat uit een array met de id van de nieuwe dataset in de indeling `"@/datasets/{DATASET_ID}"`. De dataset ID is een read-only, systeem-geproduceerde koord dat wordt gebruikt om de dataset in API vraag van verwijzingen te voorzien.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
