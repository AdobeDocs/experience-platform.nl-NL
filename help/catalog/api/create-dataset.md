---
keywords: Experience Platform;huis;populaire onderwerpen;dataset;Dataset;creeer een dataset;creeer dataset;laat dataset toe
solution: Experience Platform
title: Een gegevensset maken in de API
description: In dit document wordt beschreven hoe u een gegevenssetobject maakt in de API voor catalogusservice.
exl-id: f3e5de7f-1781-4898-ac42-063eb51e661a
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# Een gegevensset maken in de API

Als u een gegevensset wilt maken met de [!DNL Catalog] API, moet u de `$id` -waarde weten van het [!DNL Experience Data Model] -schema (XDM) waarop de gegevensset wordt gebaseerd. Als u de schema-id hebt, kunt u een gegevensset maken door een aanvraag voor een POST in te dienen bij het eindpunt `/datasets` in de [!DNL Catalog] API.

>[!NOTE]
>
>In dit document wordt alleen beschreven hoe u een gegevenssetobject maakt in [!DNL Catalog] . Voor volledige stappen op om, een dataset tot stand te brengen te bevolken en te controleren, gelieve te verwijzen naar het volgende [ leerprogramma ](../datasets/create.md).

**API formaat**

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `schemaRef.contentType` | Geeft de indeling en versie van het schema aan. Zie de sectie over [ schema versioning ](../../xdm/api/getting-started.md#versioning) in de gids XDM API voor meer informatie. |

>[!NOTE]
>
>Dit voorbeeld gebruikt het [&#128279;](https://parquet.apache.org/docs/) dossierformaat van de Parket van 0&rbrace; Apache &lbrace;voor zijn `containerFormat` bezit.  Een voorbeeld dat het JSON dossierformaat gebruikt kan in de [ handleiding van de partijontwikkelaar ](../../ingestion/batch-ingestion/api-overview.md) worden gevonden.

**Reactie**

Een geslaagde reactie retourneert HTTP Status 201 (Gemaakt) en een reactieobject dat bestaat uit een array met de id van de nieuwe dataset in de indeling `"@/datasets/{DATASET_ID}"` . De dataset ID is een read-only, systeem-geproduceerde koord dat wordt gebruikt om de dataset in API vraag van verwijzingen te voorzien.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
