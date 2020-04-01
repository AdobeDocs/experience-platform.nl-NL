---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een gegevensset maken met behulp van API's
topic: datasets
translation-type: tm+mt
source-git-commit: 6d24637dc6cc282f98288b6416e4a3b7cebe42ea

---


# Een gegevensset maken met behulp van API&#39;s

Dit document bevat algemene stappen voor het maken van een gegevensset met behulp van API&#39;s van het Adobe Experience Platform en het vullen van de gegevensset met behulp van een bestand.

## Aan de slag

Voor deze handleiding is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [Inname](../../ingestion/batch-ingestion/overview.md)in batch: Met Experience Platform kunt u gegevens invoeren als batchbestanden.
* [XDM-systeem](../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
* [Sandboxen](../../sandboxes/home.md): Het ervaringsplatform biedt virtuele sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan Platform APIs te maken.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Platform van de Ervaring te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u de [authentificatieleerprogramma](../../tutorials/authentication.md)eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen van het Experience Platform, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in het ervaringsplatform zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Raadpleeg de documentatie bij het overzicht van de [sandbox voor meer informatie over sandboxen in Platform](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* Inhoudstype: application/json

## Zelfstudie

Om een dataset tot stand te brengen, moet een schema eerst worden bepaald. Een schema is een reeks regels helpen gegevens vertegenwoordigen. Naast het beschrijven van de structuur van gegevens, verstrekken de schema&#39;s beperkingen en verwachtingen die kunnen worden toegepast en worden gebruikt om gegevens te bevestigen aangezien het tussen systemen wordt bewogen.

Deze standaarddefinities maken het mogelijk dat gegevens consistent worden geïnterpreteerd, ongeacht de oorsprong, en verwijderen de noodzaak van vertaling in verschillende toepassingen. Voor meer informatie over het samenstellen van schema&#39;s, zie de gids over de [grondbeginselen van schemacompositie](../../xdm/schema/composition.md)

## Een gegevenssetschema opzoeken

Deze zelfstudie begint waar de zelfstudie over de API voor [schemaregistratie](../../xdm/tutorials/create-schema-api.md) eindigt, waarbij gebruik wordt gemaakt van het schema Loyalty-leden dat tijdens die zelfstudie is gemaakt.

Als u niet het leerprogramma van de Registratie van het Schema hebt voltooid, gelieve daar te beginnen en met dit datasetleerprogramma voort te zetten slechts zodra u het noodzakelijke schema hebt samengesteld.

De volgende vraag kan worden gebruikt om het schema van de Leden van de Loyalty te bekijken u tijdens het leerprogramma van de Registratie van het Schema API creeerde:

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
    "imsOrg": "{IMS_ORG}",
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

>[!NOTE] In deze zelfstudie wordt voor alle voorbeelden de bestandsindeling [parket](https://parquet.apache.org/documentation/latest/) gebruikt. Een voorbeeld dat de JSON-bestandsindeling gebruikt, vindt u in de handleiding voor ontwikkelaars van [batchinvoer](../../ingestion/batch-ingestion/api-overview.md)

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

Het aanvraaglichaam omvat een &quot;datasetId&quot;gebied, waarvan de waarde in de vorige stap wordt `{DATASET_ID}` geproduceerd.

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP Status 201 (Gemaakt) en een reactieobject dat details bevat van de nieuwe batch, inclusief een tekenreeks die door het systeem wordt gegenereerd `id`en die alleen-lezen is.

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

## Bestanden uploaden naar een batch

Nadat u een nieuwe batch hebt gemaakt om te uploaden, kunt u nu bestanden uploaden naar de specifieke dataset. Het is belangrijk om te herinneren dat wanneer u de dataset bepaalde, u het dossierformaat als parquet specificeerde. De bestanden die u uploadt, moeten daarom een dergelijke indeling hebben.

>[!NOTE] Het grootste ondersteunde bestand voor het uploaden van gegevens is 512 MB. Als uw gegevensbestand groter is dan dit, moet het in brokken worden gebroken die niet groter zijn dan 512 MB, één voor één moeten worden geupload. U kunt elk bestand in dezelfde batch uploaden door deze stap voor elk bestand te herhalen met dezelfde batch-id. Er is geen limiet aan het aantal als bestanden die u kunt uploaden als onderdeel van een batch.

**API-indeling**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{BATCH_ID}` | De `id` batch waarnaar u uploadt. |
| `{DATASET_ID}` | De `id` gegevensset waarin de batch wordt gecontinueerd. |
| `{FILE_NAME}` | De naam van het bestand dat u uploadt. |

**Verzoek**

```SHELL
curl -X PUT 'https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c/datasets/5c8c3c555033b814b69f947f/files/loyaltyData.parquet' \
  -H 'content-type: application/octet-stream' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  --data-binary '@{FILE_PATH_AND_NAME}.parquet'
```

**Antwoord**

Een bestand dat is geüpload, retourneert een lege responstekst en HTTP Status 200 (OK).

## Signaalbatchverwerking

Nadat u al uw gegevensbestanden naar de batch hebt geüpload, kunt u de batch voor voltooiing signaleren. Door het afgeven van de handtekening maakt de service catalogusitems voor de geüploade bestanden en koppelt u deze aan de eerder gegenereerde batch. `DataSetFile` De catalogusbatch is gemarkeerd als succesvol, waardoor stroomafwaartse stromen worden geactiveerd die vervolgens aan de nu beschikbare gegevens kunnen werken.

**API-indeling**

```HTTP
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parameter | Beschrijving |
| --- | --- |
| `{BATCH_ID}` | De `id` batch die u markeert is voltooid. |

**Verzoek**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c?action=COMPLETE" \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Antwoord**

Een met succes voltooide partij keert een lege reactiekarakter en de Status 200 van HTTP terug (OK).

## Inname van monitor

Afhankelijk van de grootte van de gegevens, nemen de partijen variërende tijdsduur om in te nemen. U kunt de status van een batch controleren door een `batch` aanvraagparameter met de id van de batch aan een `GET /batches` aanvraag toe te voegen. De API pollt de dataset voor de status van de partij van opname tot `status` in de reactie op voltooiing (&quot;succes&quot; of &quot;mislukking&quot;) wijst.

**API-indeling**

```HTTP
GET /batches?batch={BATCH_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{BATCH_ID}` | De hoeveelheid `id` van de batch die u wilt controleren. |

**Verzoek**

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?batch=5d01230fc78a4e4f8c0c6b387b4b8d1c' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Antwoord**

Een positieve reactie retourneert een object waarvan het `status` kenmerk de waarde bevat van `success`:

```JSON
{
    "5b7129a879323401ef2a6486": {
        "imsOrg": "{IMS_ORG}",
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

Een negatieve reactie retourneert een object met de waarde van `"failed"` in het `"status"` kenmerk en bevat eventuele relevante foutberichten:

```JSON
{
    "5b96ce65badcf701e51f075d": {
        "imsOrg": "{IMS_ORG}",
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

>[!NOTE] Een aanbevolen pollinginterval is twee minuten.

## Gegevens uit de gegevensset lezen

Met de batch-id kunt u de API voor gegevenstoegang gebruiken om terug te lezen en alle bestanden te controleren die naar de batch zijn geüpload. De reactie retourneert een array die een lijst met bestands-id&#39;s bevat, die elk verwijzen naar een bestand in de batch.

U kunt de API voor gegevenstoegang ook gebruiken om de naam, grootte in bytes en een koppeling te retourneren om het bestand of de map te downloaden.

Gedetailleerde stappen voor het werken met de API voor gegevenstoegang vindt u in de [handleiding](../../data-access/api.md)voor ontwikkelaars van gegevenstoegang.

## Het schema van de gegevensset bijwerken

U kunt velden toevoegen en aanvullende gegevens invoeren in gegevenssets die u hebt gemaakt. Hiervoor moet u eerst het schema bijwerken door extra eigenschappen toe te voegen die de nieuwe gegevens definiëren. Dit kan worden gedaan gebruikend PATCH en/of de verrichtingen van de PLAATS om het bestaande schema bij te werken.

Voor meer informatie over het bijwerken van schema&#39;s, zie de [Gids](../../xdm/api/getting-started.md)van de Ontwikkelaar van de Registratie van het Schema API.

Nadat u het schema hebt bijgewerkt, kunt u de stappen in deze zelfstudie opnieuw volgen om nieuwe gegevens in te voeren die voldoen aan het herziene schema.

Het is belangrijk om te herinneren dat de schemaevolutie zuiver additief is, betekenend kunt u geen het breken verandering in een schema introduceren zodra het aan de registratie is bewaard en voor gegevensopname gebruikt. Meer over beste praktijken voor het samenstellen van schema voor gebruik met het Platform van de Ervaring van Adobe leren, zie de gids over de [grondbeginselen van schemacompositie](../../xdm/schema/composition.md).