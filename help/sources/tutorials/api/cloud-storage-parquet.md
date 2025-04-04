---
keywords: Experience Platform;home;populaire onderwerpen;gegevensbronverbinding
solution: Experience Platform
title: Bovenliggende gegevens uit een Cloud Storage-systeem van derden verzamelen met behulp van de Flow Service API
type: Tutorial
description: Deze zelfstudie gebruikt de Flow Service API om u door de stappen te laten lopen om Apache Parquet-gegevens van een extern cloudopslagsysteem in te voeren.
exl-id: fb1b19d6-16bb-4a5f-9e81-f537bac95041
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 0%

---

# Bovenliggende gegevens uit een extern cloudopslagsysteem verzamelen met de API [!DNL Flow Service]

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de [!DNL Flow Service] API om u door de stappen te laten lopen om Parquet-gegevens van een extern cloudopslagsysteem in te voeren.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [ Bronnen ](../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
- [ Sandboxen ](../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om Parquet-gegevens van een externe cloudopslag met de API [!DNL Flow Service] correct te kunnen invoeren.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan [!DNL Experience Platform] APIs te maken, moet u het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Alle bronnen in [!DNL Experience Platform], inclusief bronnen die tot [!DNL Flow Service] behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Experience Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

- `x-sandbox-name: {SANDBOX_NAME}`

Alle verzoeken die een lading (POST, PUT, PATCH) bevatten vereisen een extra media typekopbal:

- `Content-Type: application/json`

## Verbinding maken

Als u Parket-gegevens wilt opnemen met [!DNL Experience Platform] API&#39;s, moet u beschikken over een geldige verbinding voor de externe cloudopslagbron waartoe u toegang hebt. Als u nog geen verbinding hebt voor de opslag waarmee u wilt werken, kunt u een verbinding maken via de volgende zelfstudies:

- [Amazon S3](./create/cloud-storage/s3.md)
- [Azure Blob](./create/cloud-storage/blob.md)
- [Azure Data Lake Storage Gen2](./create/cloud-storage/adls-gen2.md)
- [Google Cloud Store](./create/cloud-storage/google.md)
- [SFTP](./create/cloud-storage/sftp.md)

Haal de unieke id (`$id`) van de verbinding op en sla deze op. Ga vervolgens verder met de volgende stap van deze zelfstudie.

## Doelschema maken

Als u de brongegevens in [!DNL Experience Platform] wilt gebruiken, moet u ook een doelschema maken om de brongegevens naar wens te structureren. Het doelschema wordt vervolgens gebruikt om een [!DNL Experience Platform] dataset te maken waarin de brongegevens zich bevinden.

Als u het gebruikersinterface in [!DNL Experience Platform] liever zou gebruiken, verstrekt het [ leerprogramma van de Redacteur van het Schema ](../../../xdm/tutorials/create-schema-ui.md) geleidelijke instructies voor het uitvoeren van gelijkaardige acties in de Redacteur van het Schema.

**API formaat**

```http
POST /schemaregistry/tenant/schemas
```

**Verzoek**

Met de volgende voorbeeldaanvraag wordt een XDM-schema gemaakt dat de klasse XDM [!DNL Individual Profile] uitbreidt.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
    "type": "object",
    "title": "Sample Demo Profile XDM {{$guid}}",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-subscriptions"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
        }
    ],
    "meta:containerId": "tenant",
    "meta:resourceType": "schemas",
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/profile"
}'
```

**Reactie**

Een succesvolle reactie keert details van het pas gecreëerde schema met inbegrip van zijn uniek herkenningsteken (`$id`) terug. Deze id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80",
    "meta:altId": "_{TENANT_ID}.schemas.e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Sample Demo Profile XDM 8d96a964-aad8-43c5-a73a-c8b9b1ccbfb1",
    "type": "object",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-subscriptions",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/context/profile-subscriptions",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/context/profile-subscriptions",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1584673864341,
        "repo:lastModifiedDate": 1584673864341,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{MODIFIED_USER_ID}",
        "eTag": "fa704f80da907c8f0f66f453ffcac3e52958687edbf55d71231dc5e1522193c4"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Een bronverbinding maken {#source}

Als een doel-XDM-schema is gemaakt, kan nu een bronverbinding worden gemaakt met een POST-aanvraag voor de [!DNL Flow Service] API. Een bronverbinding bestaat uit een verbinding voor API, een indeling van brongegevens en een verwijzing naar het doel-XDM-schema dat in de vorige stap is opgehaald.

**API formaat**

```http
POST /sourceConnections
```

**Verzoek**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Source Connection S3 {{$guid}}",
        "baseConnectionId": "5831c52c-c261-4945-b1c5-2cc261d945b2",
        "connectionSpec": {
            "id": "ecadc60c-7455-4d87-84dc-2a0e293d997b",
            "version": 1
        },
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80",
                "id": "",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "path": "partners-demo/samples",
            "recursive": "true"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `baseConnectionId` | De verbinding voor de API die uw cloudopslag vertegenwoordigt. |
| `data.schema.id` | (`$id`) als het doel xdm- schema in de vorige stap wordt teruggewonnen. |
| `params.path` | Het pad van het bronbestand. |

**Reactie**

Een succesvolle reactie keert het unieke herkenningsteken (`id`) van de pas gecreëerde bronverbinding terug. Sla deze waarde op zoals deze in latere stappen is vereist voor het maken van een doelverbinding.

```json
{
    "id": "73bc8911-505a-4e46-bc89-11505a6e466f",
    "etag": "\"c4004435-0000-0200-0000-5e7437d90000\""
}
```

## Een databaseverbinding maken

Als u externe gegevens in [!DNL Experience Platform] wilt opnemen, moet eerst een [!DNL Experience Platform] gegevenssetbasisverbinding worden verkregen.

Om een verbinding van de datasetbasis tot stand te brengen, volg de stappen die in het [ worden geschetst verbindingsleerprogramma van de datasetbasis ](./create-dataset-base-connection.md).

Ga na de stappen die in de ontwikkelaarsgids worden geschetst verder tot u een verbinding van de datasetbasis hebt gecreeerd. Verkrijg en sla het unieke herkenningsteken (`$id`) op en ga verder om het als identiteitskaart van de basisverbinding in de volgende stap te gebruiken om een doelverbinding tot stand te brengen.

## Een doelgegevensset maken

Een doeldataset kan worden gecreeerd door een POST- verzoek aan de [ Dienst API van de Catalogus uit te voeren ](https://www.adobe.io/experience-platform-apis/references/catalog/), verstrekkend identiteitskaart van het doelschema binnen de nuttige lading.

**API formaat**

```http
POST /catalog/dataSets
```

**Verzoek**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Leads Dataset {{$guid}}",
        "schemaRef": {
            "id": ""https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80"",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `schemaRef.id` | De id van uw doel-XDM-schema. |

**Reactie**

Een geslaagde reactie retourneert een array met de id van de nieuwe dataset in de indeling `"@/datasets/{DATASET_ID}"` . De dataset ID is een read-only, systeem-geproduceerde koord dat wordt gebruikt om de dataset in API vraag van verwijzingen te voorzien. Sla identiteitskaart van de doeldataset zoals het in recentere stappen wordt vereist om een doelverbinding en een dataflow tot stand te brengen.

```json
[
    "@/dataSets/5e7439b1ad55a618ad4c5102"
]
```

## Een doelverbinding maken {#target}

U hebt nu de unieke herkenningstekens voor een gegevenssetbasisverbinding, een doelschema, en een doeldataset. Met behulp van deze id&#39;s kunt u een doelverbinding maken met de [!DNL Flow Service] API om de gegevensset op te geven die de binnenkomende brongegevens zal bevatten.

**API formaat**

```http
POST /targetConnections
```

**Verzoek**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "baseConnectionId": "291257e3-c560-4e07-9257-e3c5606e07d1",
        "connectionSpec": {
            "id":"c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "name": "Target Connection {{$guid}}",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": ""https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80"",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5e7439b1ad55a618ad4c5102"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `baseConnectionId` | De id van de gegevenssetbasisverbinding. |
| `data.schema.id` | The `$id` of the target XDM schema. |
| `params.dataSetId` | De id van de doeldataset. |
| `connectionSpec.id` | De verbindingsspecificatie-id voor uw cloudopslag. |

**Reactie**

Een succesvolle reactie keert het unieke herkenningsteken van de nieuwe doelverbinding (`id`) terug. Sla deze waarde op zoals deze in latere stappen wordt vereist.

```json
{
    "id": "9b3abc95-f2e9-47c1-babc-95f2e927c1ec",
    "etag": "\"7501936b-0000-0200-0000-5e743bcc0000\""
}
```

## Een gegevensstroom maken

De laatste stap in de richting van het opnemen van Parquet-gegevens van een externe cloudopslag is het maken van een dataflow. Momenteel zijn de volgende vereiste waarden voorbereid:

- [Source-verbinding-id](#source)
- [Doel-verbindings-id](#target)

Een dataflow is verantwoordelijk voor het plannen en verzamelen van gegevens uit een bron. U kunt een gegevensstroom tot stand brengen door een POST- verzoek uit te voeren terwijl het verstrekken van de eerder vermelde waarden binnen de lading.

**API formaat**

```http
POST /flows
```

**Verzoek**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Demo Parquet Ingestion Flow {{$guid}}",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "73bc8911-505a-4e46-bc89-11505a6e466f"
        ],
        "targetConnectionIds": [
            "9b3abc95-f2e9-47c1-babc-95f2e927c1ec"
        ],
        "scheduleParams": {
            "startTime": {{$timestamp}},
            "frequency": "minute",
            "interval": 1000,
            "backfill": true
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `sourceConnectionIds` | De bronverbindings-id die in een eerdere stap is opgehaald. |
| `targetConnectionIds` | De doel verbindings ID die in een vroegere stap wordt teruggewonnen. |

**Reactie**

Een succesvolle reactie keert identiteitskaart (`id`) van nieuw gecreeerd dataflow terug.

```json
{
    "id": "89ff50ef-b082-426e-bf50-efb082d26e78",
    "etag": "\"890070b8-0000-0200-0000-5e743c040000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een bronschakelaar gecreeerd om de gegevens van het Pakket van uw systeem van de derdecloudopslag op een geplande basis te verzamelen. Binnenkomende gegevens kunnen nu worden gebruikt door [!DNL Experience Platform] -services, zoals [!DNL Real-Time Customer Profile] en [!DNL Data Science Workspace] . Raadpleeg de volgende documenten voor meer informatie:

- [Overzicht van het realtime klantprofiel](../../../profile/home.md)
- [Overzicht van Data Science Workspace](../../../data-science-workspace/home.md)
