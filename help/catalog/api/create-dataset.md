---
keywords: Experience Platform;huis;populaire onderwerpen;dataset;Dataset;creeer een dataset;creeer dataset;laat dataset toe
solution: Experience Platform
title: Een gegevensset maken in de API
topic: developer guide
description: In dit document wordt beschreven hoe u een gegevenssetobject maakt in de API voor catalogusservice.
exl-id: f3e5de7f-1781-4898-ac42-063eb51e661a
translation-type: tm+mt
source-git-commit: 727c9dbd87bacfd0094ca29157a2d0283c530969
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Een gegevensset maken in de API

Als u een gegevensset wilt maken met de [!DNL Catalog]-API, moet u de `$id`-waarde weten van het [!DNL Experience Data Model]-schema (XDM) waarop de gegevensset wordt gebaseerd. Zodra u schema identiteitskaart hebt, kunt u een dataset tot stand brengen door een verzoek van de POST aan het `/datasets` eindpunt in [!DNL Catalog] API te doen.

>[!NOTE]
>
>In dit document wordt alleen beschreven hoe u een gegevenssetobject maakt in [!DNL Catalog]. Raadpleeg de volgende [zelfstudie](../datasets/create.md) voor de volledige stappen voor het maken, vullen en controleren van een gegevensset.

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
| `schemaRef.id` | De URI `$id`-waarde voor het XDM-schema waarop de gegevensset wordt gebaseerd. |
| `schemaRef.contentType` | Geeft de indeling en versie van het schema aan. Zie de sectie over [schemaversie](../../xdm/api/getting-started.md#versioning) in de gids XDM API voor meer informatie. |

>[!NOTE]
>
>In dit voorbeeld wordt de bestandsindeling [Apache Parquet](https://parquet.apache.org/documentation/latest/) gebruikt voor de eigenschap `containerFormat`. Een voorbeeld dat de JSON-bestandsindeling gebruikt, vindt u in de handleiding [voor het ontwikkelen van batch-indelingen](../../ingestion/batch-ingestion/api-overview.md).

**Antwoord**

Een geslaagde reactie retourneert HTTP Status 201 (Gemaakt) en een reactieobject dat bestaat uit een array met de id van de nieuwe dataset in de notatie `"@/datasets/{DATASET_ID}"`. De dataset ID is een read-only, systeem-geproduceerde koord dat wordt gebruikt om de dataset in API vraag van verwijzingen te voorzien.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
