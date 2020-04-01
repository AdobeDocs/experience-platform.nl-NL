---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Een dataset voor profiel en identiteitsservice configureren met behulp van API's
topic: tutorial
translation-type: tm+mt
source-git-commit: 5aad9fa71051a58fe1c4678553f47077d81d23fc

---


# Een dataset voor profiel en identiteitsservice configureren met behulp van API&#39;s

Deze zelfstudie behandelt het proces om een dataset voor gebruik in het Profiel en de Dienst van de Identiteit van de Klant in real time toe te laten, die in de volgende stappen wordt uitgesplitst:

1. Laat een dataset voor gebruik in het Profiel van de Klant in real time toe, gebruikend één van twee opties:
   - [Een nieuwe gegevensset maken](#create-a-dataset-enabled-for-profile-and-identity)
   - [Een bestaande gegevensset configureren](#configure-an-existing-dataset)
1. [Gegevens in de dataset opnemen](#ingest-data-into-the-dataset)
1. [Gegevens bevestigen die door het Profiel van de Klant in real time worden opgenomen](#confirm-data-ingest-by-real-time-customer-profile)
1. [Gegevens die door Identity Service worden ingevoerd bevestigen](#confirm-data-ingest-by-identity-service)

## Aan de slag

Deze zelfstudie vereist een goed begrip van de verschillende services van het Adobe Experience Platform die betrokken zijn bij het beheer van voor profielen geschikte gegevenssets. Lees vóór het begin van deze zelfstudie de documentatie voor deze verwante platformservices:

- [Klantprofiel](../home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [Identiteitsservice](../../identity-service/home.md): Laat het Profiel van de Klant in real time toe door identiteiten van ongelijke gegevensbronnen te overbruggen die in Platform worden opgenomen.
- [Catalogusservice](../../catalog/home.md): Een RESTful API die u toestaat om datasets tot stand te brengen en hen voor de Dienst van het Profiel en van de Identiteit in real time te vormen.
- [XDM (Experience Data Model)](../../xdm/home.md): Het gestandaardiseerde kader waardoor Platform gegevens van de klantenervaring organiseert.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan Platform APIs te maken.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Platform van de Ervaring te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u de [authentificatieleerprogramma](../../tutorials/authentication.md)eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen van het Experience Platform, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

Alle bronnen in het ervaringsplatform zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt. Raadpleeg de documentatie bij het overzicht van de [sandbox voor meer informatie over sandboxen in Platform](../../sandboxes/home.md).

- x-sandbox-name: `{SANDBOX_NAME}`

## Een gegevensset maken die is ingeschakeld voor profiel en identiteit {#create-a-dataset-enabled-for-profile-and-identity}

U kunt een dataset voor het Profiel en de Dienst van de Identiteit van de Klant in real time onmiddellijk op verwezenlijking of op om het even welk punt toelaten nadat de dataset is gecreeerd. Als u een dataset zou willen toelaten die reeds is gecreeerd, volg de stappen voor het [vormen van een bestaande dataset](#configure-an-existing-dataset) die later in dit document wordt gevonden. Om een nieuwe dataset tot stand te brengen, moet u identiteitskaart van een bestaand schema kennen XDM dat voor het Profiel van de Klant in real time wordt toegelaten. Voor informatie over hoe te om een profiel-Toegelaten schema te onderzoeken of tot stand te brengen, zie de zelfstudie over het [creëren van een schema gebruikend de Registratie API](../../xdm/tutorials/create-schema-api.md)van het Schema. De volgende vraag aan Catalog API laat een dataset voor de Dienst van het Profiel en van de Identiteit toe.

**API-indeling**

```http
POST /dataSets
```

**Verzoek**

Door de gegevensset in de aanvraaginstantie op te nemen `unifiedProfile` en `unifiedIdentity` `tags` in te voeren, wordt de gegevensset onmiddellijk ingeschakeld voor respectievelijk profiel- en identiteitsdienst. De waarden van deze tags moeten een array met de tekenreeks zijn `"enabled:true"`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fileDescription" : {
    "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    },
    "fields":[],
    "schemaRef" : {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
        "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
    },
    "tags" : {
       "unifiedProfile": ["enabled:true"],
       "unifiedIdentity": ["enabled:true"]
    }
  }'
```

| Eigenschap | Beschrijving |
|---|---|
| `schemaRef.id` | Identiteitskaart van het profiel-Toegelaten schema waarop de dataset zal worden gebaseerd. |
| `{TENANT_ID}` | De naamruimte in het schemaregister die bronnen bevat die tot uw IMS-organisatie behoren. Zie de sectie [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) van de de ontwikkelaarsgids van de Registratie van het Schema voor meer informatie. |

**Antwoord**

Een succesvolle reactie toont een serie die identiteitskaart van de pas gecreëerde dataset in de vorm van `"@/dataSets/{DATASET_ID}"`bevat. Nadat u een gegevensset hebt gemaakt en ingeschakeld, gaat u verder met de stappen voor het [uploaden van gegevens](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Een bestaande gegevensset configureren {#configure-an-existing-dataset}

De volgende stappen betreffen hoe u een eerder gemaakte gegevensset kunt inschakelen voor realtime profiel en identiteitsservice van klanten. Als u reeds een profiel-Toegelaten dataset hebt gecreeerd, te werk te gaan aan de stappen voor het [opnemen van gegevens](#ingest-data-into-the-dataset).

### Controleren of de gegevensset is ingeschakeld {#check-if-the-dataset-is-enabled}

Met behulp van de Catalog-API kunt u een bestaande dataset inspecteren om te bepalen of deze is ingeschakeld voor gebruik in Real-time Customer Profile and Identity Service. De volgende vraag wint de details van een dataset door identiteitskaart terug

**API-indeling**

```http
GET /dataSets/{DATASET_ID}
```

| Parameter | Beschrijving |
|---|---|
| `{DATASET_ID}` | De id van een gegevensset die u wilt inspecteren. |

**Verzoek**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "Commission Program Events DataSet",
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
            ],
            "unifiedProfile": [
                "enabled:true"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ]
        },
        "lastBatchId": "6dcd9128a1c84e6aa5177641165e18e4",
        "lastBatchStatus": "success",
        "dule": {},
        "statsCache": {
            "startDate": null,
            "endDate": null
        },
        "namespace": "ACP",
        "state": "DRAFT",
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "5b020a27e7040801dedbf46f",
        "aspect": "production",
        "status": "enabled",
        "fileDescription": {
            "persisted": true,
            "containerFormat": "parquet",
            "format": "parquet"
        },
        "transforms": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/transforms",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "@/xdms/context/experienceevent",
        "schemaMetadata": {
            "primaryKey": [],
            "delta": [],
            "dule": [],
            "gdpr": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

Onder de `tags` eigenschap kunt u zien dat `unifiedProfile` en beide aanwezig `unifiedIdentity` zijn met de waarde `enabled:true`. Daarom worden het profiel en de Identiteitsdienst van de Klant in real time toegelaten voor deze dataset, respectievelijk.

### De gegevensset inschakelen {#enable-the-dataset}

Als de bestaande dataset niet voor de Dienst van het Profiel of van de Identiteit is toegelaten, kunt u het toelaten door een verzoek van de PATCH te maken gebruikend dataset identiteitskaart

**API-indeling**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parameter | Beschrijving |
|---|---|
| `{DATASET_ID}` | De id van een gegevensset die u wilt bijwerken. |

**Verzoek**

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags" : {
        "unifiedProfile": ["enabled:true"],
        "unifiedIdentity": ["enabled:true"]
    }
  }'
```

De aanvraaginstantie bevat een `tags` eigenschap die twee subeigenschappen bevat: `"unifiedProfile"` en `"unifiedIdentity"`. De waarden van deze subeigenschappen zijn arrays die de tekenreeks bevatten `"enabled:true"`.

**De vraag van de Reactie** Een succesvolle PATCH keert de Status 200 van HTTP (O.K.) en een serie terug die identiteitskaart van de bijgewerkte dataset bevatten. Deze id moet overeenkomen met de id die in de PATCH-aanvraag is verzonden. De `"unifiedProfile"` - en `"unifiedIdentity"` -tags zijn nu toegevoegd en de gegevensset is ingeschakeld voor gebruik door de services Profiel en Identiteit.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Gegevens in de dataset opnemen {#ingest-data-into-the-dataset}

Zowel in real time het Profiel van de Klant als de Dienst van de Identiteit verbruiken XDM gegevens aangezien het in een dataset wordt opgenomen. Voor instructies over hoe te om gegevens in een dataset te uploaden, verwijs naar de zelfstudie over het [creëren van een dataset gebruikend APIs](../../catalog/datasets/create.md). Wanneer het plannen van welke gegevens naar uw profiel-Toegelaten dataset te verzenden, overweeg de volgende beste praktijken:

- Neem alle gegevens op die u als criteria voor het publiekssegment wilt gebruiken.
- Neem zoveel id&#39;s op als u uit uw profielgegevens kunt opvragen om uw identiteitsgrafiek te maximaliseren. Dit staat de Dienst van de Identiteit toe om identiteiten over datasets effectiever te binden.

## Gegevens bevestigen die door het Profiel van de Klant in real time worden opgenomen {#confirm-data-ingest-by-real-time-customer-profile}

Bij het voor het eerst uploaden van gegevens naar een nieuwe gegevensset of als onderdeel van een proces waarbij een nieuwe ETL of gegevensbron betrokken is, wordt aanbevolen de gegevens zorgvuldig te controleren om te controleren of deze op de verwachte wijze zijn geüpload. Gebruikend de Toegang API van het Profiel van de Klant in real time, kunt u partijgegevens terugwinnen aangezien het in een dataset wordt geladen. Als u om het even welke entiteiten niet kunt terugwinnen u verwacht, kan uw dataset niet voor het Profiel van de Klant in real time worden toegelaten. Na het bevestigen dat uw dataset is toegelaten, zorg ervoor dat uw brongegevensformaat en herkenningstekens uw verwachtingen steunen. Voor gedetailleerde instructies voor het gebruik van de Real-Time Customer Profile API voor toegang tot profielgegevens, volgt u de [subhandleiding voor entiteiten, ook wel de &quot;Profile Access API&quot;](../api/entities.md)genoemd.

## Gegevens die door Identity Service worden ingevoerd bevestigen {#confirm-data-ingest-by-identity-service}

Elk opgenomen gegevensfragment dat meer dan één identiteit bevat, maakt een koppeling in uw persoonlijke identiteitsgrafiek. Voor meer informatie over identiteitsgrafieken en toegang tot identiteitsgegevens, gelieve te beginnen door het overzicht [van de Dienst van de](../../identity-service/home.md)Identiteit te lezen.