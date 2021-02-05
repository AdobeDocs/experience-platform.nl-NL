---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API;gegevensset inschakelen
title: Een gegevensset voor profiel- en identiteitsservice configureren met behulp van API's
topic: tutorial
type: Tutorial
description: Deze zelfstudie laat u zien hoe u een gegevensset inschakelt voor gebruik met Real-time Customer Profile and Identity Service met Adobe Experience Platform API's.
translation-type: tm+mt
source-git-commit: cad9c690be986961aea2969ef0ade975f33a8ee5
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 0%

---


# Een gegevensset configureren voor [!DNL Profile] en [!DNL Identity Service] met behulp van API&#39;s

Deze zelfstudie behandelt het proces waarbij een gegevensset wordt ingeschakeld voor gebruik in [!DNL Real-time Customer Profile] en [!DNL Identity Service], en omvat de volgende stappen:

1. Schakel een gegevensset in voor gebruik in [!DNL Real-time Customer Profile] met behulp van een van de volgende twee opties:
   - [Een nieuwe gegevensset maken](#create-a-dataset-enabled-for-profile-and-identity)
   - [Een bestaande gegevensset configureren](#configure-an-existing-dataset)
1. [Gegevens in de dataset opnemen](#ingest-data-into-the-dataset)
1. [Gegevens bevestigen die door het Profiel van de Klant in real time worden opgenomen](#confirm-data-ingest-by-real-time-customer-profile)
1. [Gegevens die door Identity Service worden ingevoerd bevestigen](#confirm-data-ingest-by-identity-service)

## Aan de slag

Deze zelfstudie vereist een goed begrip van de verschillende Adobe Experience Platform-services die betrokken zijn bij het beheer van gegevenssets die geschikt zijn voor [!DNL Profile]. Lees vóór het begin van deze zelfstudie de documentatie voor deze verwante [!DNL Platform]-services:

- [[!DNL Real-time Customer Profile]](../home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [[!DNL Identity Service]](../../identity-service/home.md): Hiermee wordt  [!DNL Real-time Customer Profile] door het overbruggen van identiteiten mogelijk van verschillende gegevensbronnen waarin gegevens worden opgenomen  [!DNL Platform].
- [[!DNL Catalog Service]](../../catalog/home.md): Een RESTful API die u toestaat om datasets tot stand te brengen en hen te vormen voor  [!DNL Real-time Customer Profile] en  [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Platform] klantenervaring worden georganiseerd.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan de Platform APIs te maken.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u [!DNL Platform] API&#39;s wilt aanroepen, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen [!DNL Experience Platform], zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt. Raadpleeg de documentatie [sandbox-overzicht](../../sandboxes/home.md) voor meer informatie over sandboxen in [!DNL Platform].

- x-sandbox-name: `{SANDBOX_NAME}`

## Maak een gegevensset die is ingeschakeld voor [!DNL Profile] en [!DNL Identity] {#create-a-dataset-enabled-for-profile-and-identity}

U kunt een dataset voor [!DNL Real-time Customer Profile] en [!DNL Identity Service] onmiddellijk op verwezenlijking of op om het even welk punt toelaten nadat de dataset is gecreeerd. Als u een dataset zou willen toelaten die reeds is gecreeerd, volg de stappen voor [het vormen van een bestaande dataset](#configure-an-existing-dataset) later in dit document wordt gevonden. Om een nieuwe dataset tot stand te brengen, moet u identiteitskaart van een bestaand schema kennen XDM dat voor het Profiel van de Klant in real time wordt toegelaten. Voor informatie over hoe te om een profiel-Toegelaten schema te onderzoeken of tot stand te brengen, zie het leerprogramma [creërend een schema gebruikend de Registratie API](../../xdm/tutorials/create-schema-api.md) van het Schema. De volgende vraag aan [!DNL Catalog] API laat een dataset voor [!DNL Profile] en [!DNL Identity Service] toe.

**API-indeling**

```http
POST /dataSets
```

**Verzoek**

Door `unifiedProfile` en `unifiedIdentity` onder `tags` in het verzoeklichaam op te nemen, zal de dataset onmiddellijk voor [!DNL Profile] en [!DNL Identity Service], respectievelijk worden toegelaten. De waarden van deze tags moeten een array zijn met de tekenreeks `"enabled:true"`.

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
| `schemaRef.id` | Identiteitskaart van [!DNL Profile]-Toegelaten schema waarop de dataset zal worden gebaseerd. |
| `{TENANT_ID}` | De naamruimte in de [!DNL Schema Registry] die bronnen bevat die bij uw IMS-organisatie horen. Zie de [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) sectie van de [!DNL Schema Registry] ontwikkelaarsgids voor meer informatie. |

**Antwoord**

Een succesvolle reactie toont een serie die identiteitskaart van de pas gecreëerde dataset in de vorm van `"@/dataSets/{DATASET_ID}"` bevat. Nadat u een gegevensset hebt gemaakt en ingeschakeld, gaat u verder met de stappen voor het uploaden van gegevens](#upload-data-to-the-dataset).[

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Een bestaande gegevensset {#configure-an-existing-dataset} configureren

In de volgende stappen wordt beschreven hoe u een eerder gemaakte dataset voor [!DNL Real-time Customer Profile] en [!DNL Identity Service] kunt inschakelen. Als u reeds een profiel-Toegelaten dataset hebt gecreeerd, gelieve te werk te gaan aan de stappen voor [het opnemen van gegevens](#ingest-data-into-the-dataset).

### Controleren of de gegevensset {#check-if-the-dataset-is-enabled} is ingeschakeld

Met de [!DNL Catalog] API kunt u een bestaande dataset inspecteren om te bepalen of het voor gebruik in [!DNL Real-time Customer Profile] en [!DNL Identity Service] wordt toegelaten. De volgende vraag wint de details van een dataset door identiteitskaart terug

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

Onder de eigenschap `tags` ziet u dat `unifiedProfile` en `unifiedIdentity` beide aanwezig zijn met de waarde `enabled:true`. Daarom worden [!DNL Real-time Customer Profile] en [!DNL Identity Service] toegelaten voor deze dataset, respectievelijk.

### Gegevensset {#enable-the-dataset} inschakelen

Als de bestaande dataset niet voor [!DNL Profile] of [!DNL Identity Service] is toegelaten, kunt u het toelaten door een verzoek van de PATCH te doen gebruikend dataset identiteitskaart

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

De aanvraaginstantie bevat een eigenschap `tags`, die twee subeigenschappen bevat: `"unifiedProfile"` en `"unifiedIdentity"`. De waarden van deze subeigenschappen zijn arrays die de tekenreeks `"enabled:true"` bevatten.

**De**
ResponsA succesvolle aanvraag van de PATCH keert HTTP Status 200 (O.K.) en een serie terug die identiteitskaart van de bijgewerkte dataset bevatten. Deze id moet overeenkomen met de id die in de aanvraag voor PATCH is verzonden. De `"unifiedProfile"` en `"unifiedIdentity"` markeringen zijn nu toegevoegd en de dataset wordt toegelaten voor gebruik door de diensten van het Profiel en van de Identiteit.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Gegevens in de gegevensset opnemen {#ingest-data-into-the-dataset}

Zowel [!DNL Real-time Customer Profile] als [!DNL Identity Service] verbruiken XDM gegevens aangezien het in een dataset wordt opgenomen. Voor instructies over hoe te om gegevens in een dataset te uploaden, verwijs naar de zelfstudie over [het creëren van een dataset gebruikend APIs](../../catalog/datasets/create.md). Wanneer het plannen van welke gegevens naar uw [!DNL Profile]-Toegelaten dataset te verzenden, overweeg de volgende beste praktijken:

- Neem alle gegevens op die u als criteria voor het publiekssegment wilt gebruiken.
- Neem zoveel id&#39;s op als u uit uw profielgegevens kunt opvragen om uw identiteitsgrafiek te maximaliseren. Hierdoor kan [!DNL Identity Service] identiteiten op effectievere wijze aan verschillende gegevenssets koppelen.

## Gegevens die worden ingevoerd door [!DNL Real-time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile} bevestigen

Bij het voor het eerst uploaden van gegevens naar een nieuwe gegevensset of als onderdeel van een proces waarbij een nieuwe ETL of gegevensbron betrokken is, wordt aanbevolen de gegevens zorgvuldig te controleren om te controleren of deze op de verwachte wijze zijn geüpload. Met de API [!DNL Real-time Customer Profile] Access kunt u batchgegevens ophalen terwijl deze in een gegevensset worden geladen. Als u geen van de entiteiten kunt terugwinnen u verwacht, kan uw dataset niet voor [!DNL Real-time Customer Profile] worden toegelaten. Na het bevestigen dat uw dataset is toegelaten, zorg ervoor dat uw brongegevensformaat en herkenningstekens uw verwachtingen steunen. Voor gedetailleerde instructies over hoe te om [!DNL Real-time Customer Profile] API te gebruiken om tot [!DNL Profile] gegevens toegang te hebben, te volgen gelieve [de gids van het eindpunt van entiteiten](../api/entities.md), die ook als &quot;[!DNL Profile Access] API wordt bekend&quot;.

## Gegevens die worden ingevoerd door identiteitsservice {#confirm-data-ingest-by-identity-service} bevestigen

Elk opgenomen gegevensfragment dat meer dan één identiteit bevat, maakt een koppeling in uw persoonlijke identiteitsgrafiek. Voor meer informatie over identiteitsgrafieken en toegang tot identiteitsgegevens, gelieve te beginnen door [Overzicht van de Dienst van de Identiteit](../../identity-service/home.md) te lezen.