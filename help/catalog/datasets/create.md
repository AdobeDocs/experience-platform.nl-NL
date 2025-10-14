---
keywords: Experience Platform;home;populaire onderwerpen;dataset;Dataset;maak een dataset;maak een dataset
solution: Experience Platform
title: Een gegevensset maken met API's
description: Dit document bevat algemene stappen voor het maken van een gegevensset met Adobe Experience Platform API's en het vullen van de gegevensset met behulp van een bestand.
exl-id: 3a5f48cf-ad05-4b9e-be1d-ff213a26a477
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1302'
ht-degree: 0%

---

# Een gegevensset maken met behulp van API&#39;s

Dit document bevat algemene stappen voor het maken van een gegevensset met Adobe Experience Platform API&#39;s en het vullen van de gegevensset met behulp van een bestand.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [&#x200B; Inname van de Partij &#x200B;](../../ingestion/batch-ingestion/overview.md): [!DNL Experience Platform] staat u toe om gegevens als partijdossiers in te voeren.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Het gestandaardiseerde framework waarmee [!DNL Experience Platform] gegevens voor de klantervaring indeelt.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één [!DNL Experience Platform] -instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om aanroepen naar de API&#39;s van [!DNL Experience Platform] te kunnen uitvoeren.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [&#x200B; hoe te om voorbeeld API vraag &#x200B;](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan [!DNL Experience Platform] APIs te maken, moet u het [&#x200B; authentificatieleerprogramma &#x200B;](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Experience Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over zandbakken in [!DNL Experience Platform], zie de [&#x200B; documentatie van het zandbakoverzicht &#x200B;](../../sandboxes/home.md).

Voor alle aanvragen die een payload (POST, PUT, PATCH) bevatten, is een extra `Content-Type: application/json` -header vereist. Voor JSON+PATCH-aanvragen moet de waarde `Content-Type` `application/json-patch+json` zijn.

## Tutorial

Om een dataset tot stand te brengen, moet een schema eerst worden bepaald. Een schema is een reeks regels helpen gegevens vertegenwoordigen. Naast het beschrijven van de structuur van gegevens, verstrekken de schema&#39;s beperkingen en verwachtingen die kunnen worden toegepast en worden gebruikt om gegevens te bevestigen aangezien het tussen systemen wordt bewogen.

Deze standaarddefinities maken het mogelijk dat gegevens consistent worden geïnterpreteerd, ongeacht de oorsprong, en verwijderen de noodzaak van vertaling in verschillende toepassingen. Voor meer informatie over het samenstellen van schema&#39;s, zie de gids op de [&#x200B; grondbeginselen van schemacompositie &#x200B;](../../xdm/schema/composition.md)

## Een gegevenssetschema opzoeken

Dit leerprogramma begint waar het [&#128279;](../../xdm/tutorials/create-schema-api.md) eind van het leerprogramma van de Registratie van het 0&rbrace; Schema API, makend gebruik van het schema van Leden Loyalty dat tijdens dat leerprogramma wordt gecreeerd.

Als u de zelfstudie van [!DNL Schema Registry] niet hebt voltooid, begint u daar en gaat u verder met deze zelfstudie over de gegevensset nadat u het vereiste schema hebt samengesteld.

De volgende aanroep kan worden gebruikt om het schema Loyalty-leden te bekijken dat u tijdens de API-zelfstudie [!DNL Schema Registry] hebt gemaakt:

**API formaat**

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

**Reactie**

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

**API formaat**

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
| `schemaRef.id` | De URI `$id`-waarde voor het XDM-schema waarop de gegevensset wordt gebaseerd. |
| `schemaRef.contentType` | Geeft de indeling en versie van het schema aan. Zie de sectie over [&#x200B; schema versioning &#x200B;](../../xdm/api/getting-started.md#versioning) in de gids XDM API voor meer informatie. |

>[!NOTE]
>
>Dit leerprogramma gebruikt het [&#128279;](https://parquet.apache.org/docs/) dossierformaat van het Pakket van 0&rbrace; Apache &lbrace;voor al zijn voorbeelden.  Een voorbeeld dat het JSON dossierformaat gebruikt kan in de [&#x200B; gids van de de partijontwikkelaar van de batch ingestitie &#x200B;](../../ingestion/batch-ingestion/api-overview.md) worden gevonden

**Reactie**

Een geslaagde reactie retourneert HTTP Status 201 (Gemaakt) en een reactieobject dat bestaat uit een array met de id van de nieuwe dataset in de indeling `"@/datasets/{DATASET_ID}"` . De dataset ID is een read-only, systeem-geproduceerde koord dat wordt gebruikt om de dataset in API vraag van verwijzingen te voorzien.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```

## Een batch maken

Alvorens u gegevens aan een dataset kunt toevoegen, moet u een partij tot stand brengen die met de dataset verbonden is. De batch wordt vervolgens gebruikt voor uploaden.

**API formaat**

```HTTP
POST /batches
```

**Verzoek**

De aanvraaginstantie bevat een veld &quot;datasetId&quot;, waarvan de waarde de `{DATASET_ID}` is die in de vorige stap is gegenereerd.

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

**Reactie**

Een geslaagde reactie retourneert HTTP Status 201 (Gemaakt) en een reactieobject. Het reactieobject bestaat uit een array met de id van de nieuwe batch in de indeling `"@/batches/{BATCH_ID}"` . De batch-id is een alleen-lezen, door het systeem gegenereerde tekenreeks die wordt gebruikt om naar de batch te verwijzen in API-aanroepen.

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

**API formaat**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{BATCH_ID}` | De `id` van de batch waarnaar u uploadt. |
| `{DATASET_ID}` | De `id` van de dataset waarin de partij zal worden voortgeduurd. |
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

**Reactie**

Een bestand dat is geüpload, retourneert een lege responstekst en HTTP Status 200 (OK).

## Signaalbatchverwerking

Nadat u al uw gegevensbestanden naar de batch hebt geüpload, kunt u de batch voor voltooiing signaleren. Als u een signaal afgeeft, maakt de service [!DNL Catalog] `DataSetFile` -items voor de geüploade bestanden en koppelt deze aan de eerder gegenereerde batch. De batch [!DNL Catalog] is gemarkeerd als succesvol, waardoor stroomafwaartse stromen worden geactiveerd die vervolgens aan de nu beschikbare gegevens kunnen werken.

**API formaat**

```HTTP
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parameter | Beschrijving |
| --- | --- |
| `{BATCH_ID}` | De `id` van de batch die u markeert als voltooid. |

**Verzoek**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c?action=COMPLETE" \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Reactie**

Een met succes voltooide partij keert een lege reactiekarakter en de Status 200 van HTTP terug (OK).

## Inname van monitor

Afhankelijk van de grootte van de gegevens, nemen de partijen variërende tijdsduur om in te nemen. U kunt de status van een batch controleren door de id van een batch toe te voegen aan een `GET /batches` aanvraag.

**API formaat**

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

**Reactie**

Een positieve reactie retourneert een object waarvan het kenmerk `status` de waarde `success` bevat:

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

Een negatieve reactie retourneert een object met de waarde `"failed"` in het `"status"` -kenmerk en bevat eventuele relevante foutberichten:

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

De gedetailleerde stappen voor het werken met de Toegang API van Gegevens kunnen in de [&#x200B; de ontwikkelaarsgids van de Toegang van Gegevens &#x200B;](../../data-access/home.md) worden gevonden.

## Het schema van de gegevensset bijwerken

U kunt velden toevoegen en aanvullende gegevens invoeren in gegevenssets die u hebt gemaakt. Hiervoor moet u eerst het schema bijwerken door extra eigenschappen toe te voegen die de nieuwe gegevens definiëren. Dit kan worden gedaan gebruikend de verrichtingen van PATCH en/of van PUT om het bestaande schema bij te werken.

Voor meer informatie over het bijwerken van schema&#39;s, zie de [&#x200B; Gids van de Ontwikkelaar van de Registratie API van het Schema &#x200B;](../../xdm/api/getting-started.md).

Nadat u het schema hebt bijgewerkt, kunt u de stappen in deze zelfstudie opnieuw volgen om nieuwe gegevens in te voeren die voldoen aan het herziene schema.

Het is belangrijk om te herinneren dat de schemaevolutie zuiver additief is, betekenend kunt u geen het breken verandering in een schema introduceren zodra het aan de registratie is bewaard en voor gegevensopname gebruikt. Meer over beste praktijken leren voor het samenstellen van schema voor gebruik met Adobe Experience Platform, zie de gids op de [&#x200B; grondbeginselen van schemacompositie &#x200B;](../../xdm/schema/composition.md).
