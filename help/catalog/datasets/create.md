---
keywords: Experience Platform;huis;populaire onderwerpen;dataset;Dataset;creeer een dataset;creeer dataset
solution: Experience Platform
title: Een gegevensset maken met API's
description: Dit document bevat algemene stappen voor het maken van een gegevensset met Adobe Experience Platform API's en het vullen van de gegevensset met behulp van een bestand.
exl-id: 3a5f48cf-ad05-4b9e-be1d-ff213a26a477
source-git-commit: e2f16f532b98e6948ffd7f331e630137b3972f0f
workflow-type: tm+mt
source-wordcount: '1303'
ht-degree: 0%

---

# Een gegevensset maken met behulp van API&#39;s

Dit document bevat algemene stappen voor het maken van een gegevensset met Adobe Experience Platform API&#39;s en het vullen van de gegevensset met behulp van een bestand.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Inname in batch](../../ingestion/batch-ingestion/overview.md): [!DNL Experience Platform] kunt u gegevens invoeren als batchbestanden.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan te maken [!DNL Platform] API&#39;s.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] gids voor probleemoplossing.

### Waarden verzamelen voor vereiste koppen

Om vraag te maken aan [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in alle [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over sandboxen in [!DNL Platform], zie de [overzichtsdocumentatie van sandbox](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra `Content-Type: application/json` header. Voor JSON+PATCH-aanvragen `Content-Type` moeten `application/json-patch+json`.

## Tutorial

Om een dataset tot stand te brengen, moet een schema eerst worden bepaald. Een schema is een reeks regels helpen gegevens vertegenwoordigen. Naast het beschrijven van de structuur van gegevens, verstrekken de schema&#39;s beperkingen en verwachtingen die kunnen worden toegepast en worden gebruikt om gegevens te bevestigen aangezien het tussen systemen wordt bewogen.

Deze standaarddefinities maken het mogelijk dat gegevens consistent worden geïnterpreteerd, ongeacht de oorsprong, en verwijderen de noodzaak van vertaling in verschillende toepassingen. Zie de handleiding over de [grondbeginselen van de schemacompositie](../../xdm/schema/composition.md)

## Een gegevenssetschema opzoeken

Deze zelfstudie begint waar de [Zelfstudie Schema Registry API](../../xdm/tutorials/create-schema-api.md) eindigt, die gebruik maken van het schema van Leden Loyalty tijdens die zelfstudie wordt gecreeerd.

Als u de [!DNL Schema Registry] een zelfstudie: start daar en ga verder met deze zelfstudie voor de gegevensset, maar pas nadat u het vereiste schema hebt samengesteld.

De volgende vraag kan worden gebruikt om het schema van Leden van de Loyalty te bekijken u tijdens creeerde [!DNL Schema Registry] API-zelfstudie:

**API-indeling**

```HTTP
GET /tenant/schemas/{schema meta:altId or URL encoded $id URI}
```

**Verzoek**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

De indeling van het reactieobject is afhankelijk van de header Accepteren die in de aanvraag wordt verzonden. Afzonderlijke eigenschappen in deze reactie zijn geminimaliseerd voor ruimte.

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "properties": {
        "repositoryCreatedBy": {},
        "repositoryLastModifiedBy": {},
        "createdByBatchID": {},
        "modifiedByBatchID": {},
        "_repo": {},
        "identityMap": {},
        "_id": {},
        "timeSeriesEvents": {},
        "person": {},
        "homeAddress": {},
        "personalEmail": {},
        "homePhone": {},
        "mobilePhone": {},
        "faxPhone": {},
        "_{TENANT_ID}": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "loyalty": {
                    "title": "Loyalty",
                    "description": "Loyalty Info",
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/49b594dabe6bec545c8a6d1a0991a4dd",
                    "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier.",
                            "meta:xdmType": "string"
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "loyaltyPoints": {
                            "title": "Loyalty Points",
                            "type": "integer",
                            "description": "Loyalty points total.",
                            "meta:xdmType": "int"
                        },
                        "memberSince": {
                            "title": "Member Since",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined the Loyalty Program.",
                            "meta:xdmType": "date-time"
                        }
                    }
                }
            }
        }
    },
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.4",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551843052271,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Een gegevensset maken

Met het schema van de Leden van de Loyalty op zijn plaats, kunt u een dataset nu tot stand brengen die verwijzingen het schema.

**API-indeling**

```HTTP
POST /dataSets
```

**Verzoek**

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
| `schemaRef.id` | De URI `$id` waarde voor het XDM schema de dataset zal worden gebaseerd op. |
| `schemaRef.contentType` | Geeft de indeling en versie van het schema aan. Zie de sectie over [schemaversie](../../xdm/api/getting-started.md#versioning) in de XDM API-handleiding voor meer informatie. |

>[!NOTE]
>
>Deze zelfstudie gebruikt de [Apache Parquet](https://parquet.apache.org/docs/) bestandsindeling voor alle voorbeelden. Een voorbeeld met de JSON-bestandsindeling vindt u in het dialoogvenster [handleiding voor het ontwikkelen van batch-inhoud](../../ingestion/batch-ingestion/api-overview.md)

**Antwoord**

Een geslaagde reactie retourneert HTTP Status 201 (Gemaakt) en een reactieobject dat bestaat uit een array met de id van de nieuwe dataset in de indeling `"@/datasets/{DATASET_ID}"`. De dataset ID is een read-only, systeem-geproduceerde koord dat wordt gebruikt om de dataset in API vraag van verwijzingen te voorzien.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```

## Een batch maken

Alvorens u gegevens aan een dataset kunt toevoegen, moet u een partij tot stand brengen die met de dataset verbonden is. De batch wordt vervolgens gebruikt voor uploaden.

**API-indeling**

```HTTP
POST /batches
```

**Verzoek**

De aanvraaginstantie bevat een veld &quot;datasetId&quot;, waarvan de waarde `{DATASET_ID}` gegenereerd in de vorige stap.

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP Status 201 (Gemaakt) en een reactieobject. Het reactieobject bestaat uit een array met de id van de nieuwe batch in de indeling `"@/batches/{BATCH_ID}"`. De batch-id is een alleen-lezen, door het systeem gegenereerde tekenreeks die wordt gebruikt om naar de batch te verwijzen in API-aanroepen.

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{ORG_ID}",
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

## Bestanden uploaden naar een batch

Nadat u een nieuwe batch hebt gemaakt om te uploaden, kunt u nu bestanden uploaden naar de specifieke dataset. Het is belangrijk om te herinneren dat wanneer u de dataset bepaalde, u het dossierformaat als Parquet specificeerde. De bestanden die u uploadt, moeten daarom een dergelijke indeling hebben.

>[!NOTE]
>
>Het grootste ondersteunde bestand voor het uploaden van gegevens is 512 MB. Als uw gegevensbestand groter is dan dit, moet het in brokken worden gebroken die niet groter zijn dan 512 MB, één voor één moeten worden geupload. U kunt elk bestand in dezelfde batch uploaden door deze stap voor elk bestand te herhalen met dezelfde batch-id. Er is geen limiet aan het aantal als bestanden die u kunt uploaden als onderdeel van een batch.

**API-indeling**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{BATCH_ID}` | De `id` van de batch waarnaar u uploadt. |
| `{DATASET_ID}` | De `id` van de dataset zal de partij in worden voortgeduurd. |
| `{FILE_NAME}` | De naam van het bestand dat u uploadt. |

**Verzoek**

```SHELL
curl -X PUT 'https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c/datasets/5c8c3c555033b814b69f947f/files/loyaltyData.parquet' \
  -H 'content-type: application/octet-stream' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  --data-binary '@{FILE_PATH_AND_NAME}.parquet'
```

**Antwoord**

Een bestand dat is geüpload, retourneert een lege responstekst en HTTP Status 200 (OK).

## Signaalbatchverwerking

Nadat u al uw gegevensbestanden naar de batch hebt geüpload, kunt u de batch voor voltooiing signaleren. De signalerende voltooiing veroorzaakt de dienst om te creëren [!DNL Catalog] `DataSetFile` vermeldingen voor de geüploade bestanden en koppel deze aan de eerder gegenereerde batch. De [!DNL Catalog] batch is gemarkeerd als succesvol, waardoor stroomafwaartse stromen worden geactiveerd die vervolgens aan de nu beschikbare gegevens kunnen werken.

**API-indeling**

```HTTP
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parameter | Beschrijving |
| --- | --- |
| `{BATCH_ID}` | De `id` van de batch waaraan u een markering hebt toegevoegd, als voltooid. |

**Verzoek**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c?action=COMPLETE" \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Antwoord**

Een met succes voltooide partij keert een lege reactiekarakter en de Status 200 van HTTP terug (OK).

## Inname van monitor

Afhankelijk van de grootte van de gegevens, nemen de partijen variërende tijdsduur om in te nemen. U kunt de status van een batch controleren door een batch-id aan een batch toe te voegen `GET /batches` verzoek.

**API-indeling**

```HTTP
GET /batches/{BATCH_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{BATCH_ID}` | De `id` van de batch die u wilt controleren. |

**Verzoek**

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?batch=5d01230fc78a4e4f8c0c6b387b4b8d1c' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Antwoord**

Een positieve reactie retourneert een object met de bijbehorende `status` kenmerk met de waarde van `success`:

```JSON
{
    "5b7129a879323401ef2a6486": {
        "imsOrg": "{ORG_ID}",
        "created": 1534142888068,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1534142955152,
        "replay": {},
        "status": "success",
        "errors": [],
        "version": "1.0.3",
        "availableDates": {},
        "relatedObjects": [
            {
                "type": "batch",
                "id": "29285e08378f4a41827e7e70fb7cb8f0"
            }
        ],
        "metrics": {
            "startTime": 1534142943819,
            "endTime": 1534142951760,
            "recordsRead": 108,
            "recordsWritten": 108
        }
    }
}
```

Een negatief antwoord retourneert een object met de waarde `"failed"` in haar `"status"` en bevat relevante foutberichten:

```JSON
{
    "5b96ce65badcf701e51f075d": {
        "imsOrg": "{ORG_ID}",
        "status": "failed",
        "relatedObjects": [
            {
                "type": "batch",
                "id": "29285e08378f4a41827e7e70fb7cb8f0"
            }
        ],
        "replay": {},
        "availableDates": {},
        "metrics": {
            "startTime": 1536610322329,
            "endTime": 1536610438083,
            "recordsRead": 4004,
            "recordsWritten": 4004,
            "failureReason": "Job aborted due to stage failure: Task 0 in stage 1.0 failed 4 times,:"
        },
        "errors": [
            {
                "code": "0070000017",
                "description": "Unknown error occurred."
            },
            {
                "code": "unknown",
                "description": "Job aborted."
            }
        ],
        "created": 1536609893629,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1536610442814,
        "version": "1.0.5"
    }
}
```

>[!NOTE]
>
>Een aanbevolen pollinginterval is twee minuten.

## Gegevens uit de gegevensset lezen

Met de batch-id kunt u de API voor gegevenstoegang gebruiken om terug te lezen en alle bestanden te controleren die naar de batch zijn geüpload. De reactie retourneert een array die een lijst met bestands-id&#39;s bevat, die elk verwijzen naar een bestand in de batch.

U kunt de API voor gegevenstoegang ook gebruiken om de naam, grootte in bytes en een koppeling te retourneren om het bestand of de map te downloaden.

Gedetailleerde stappen voor het werken met de API voor gegevenstoegang vindt u in de [Handleiding voor ontwikkelaars van gegevenstoegang](../../data-access/home.md).

## Het schema van de gegevensset bijwerken

U kunt velden toevoegen en aanvullende gegevens invoeren in gegevenssets die u hebt gemaakt. Hiervoor moet u eerst het schema bijwerken door extra eigenschappen toe te voegen die de nieuwe gegevens definiëren. Dit kan worden gedaan gebruikend PATCH en/of PUT verrichtingen om het bestaande schema bij te werken.

Voor meer informatie over het bijwerken van schema&#39;s, zie [Handleiding voor ontwikkelaars van schema-register](../../xdm/api/getting-started.md).

Nadat u het schema hebt bijgewerkt, kunt u de stappen in deze zelfstudie opnieuw volgen om nieuwe gegevens in te voeren die voldoen aan het herziene schema.

Het is belangrijk om te herinneren dat de schemaevolutie zuiver additief is, betekenend kunt u geen het breken verandering in een schema introduceren zodra het aan de registratie is bewaard en voor gegevensopname gebruikt. Raadpleeg de handleiding op het tabblad [grondbeginselen van de schemacompositie](../../xdm/schema/composition.md).
