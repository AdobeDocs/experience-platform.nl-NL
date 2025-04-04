---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API;gegevensset inschakelen
title: Een gegevensset voor profiel- en identiteitsservice inschakelen met behulp van API's
type: Tutorial
description: Deze zelfstudie laat u zien hoe u een gegevensset kunt inschakelen voor gebruik met Real-Time Customer Profile and Identity Service met Adobe Experience Platform API's.
exl-id: a115e126-6775-466d-ad7e-ee36b0b8b49c
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 0%

---

# Een gegevensset inschakelen voor [!DNL Profile] en [!DNL Identity Service] met behulp van API&#39;s

Deze zelfstudie behandelt het proces waarbij een gegevensset wordt ingeschakeld voor gebruik in [!DNL Real-Time Customer Profile] en [!DNL Identity Service] , en omvat de volgende stappen:

1. Schakel een gegevensset in voor gebruik in [!DNL Real-Time Customer Profile] met behulp van een van de volgende twee opties:
   - [Een nieuwe gegevensset maken](#create-a-dataset-enabled-for-profile-and-identity)
   - [Een bestaande gegevensset configureren](#configure-an-existing-dataset)
1. [ Samenvatting gegevens in de dataset ](#ingest-data-into-the-dataset)
1. [ Bevestig gegevens die door Real-Time Profiel van de Klant ](#confirm-data-ingest-by-real-time-customer-profile) worden opgenomen
1. [ Bevestig gegevens die door de Dienst van de Identiteit worden ingesloten ](#confirm-data-ingest-by-identity-service)

## Aan de slag

Deze zelfstudie vereist een goed begrip van verschillende Adobe Experience Platform-services die betrokken zijn bij het beheer van voor profielen geschikte gegevenssets. Lees vóór het starten van deze zelfstudie de documentatie voor deze verwante [!DNL Experience Platform] services:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
- [[!DNL Identity Service]](../../identity-service/home.md): schakelt [!DNL Real-Time Customer Profile] in door identiteiten te overbruggen van verschillende gegevensbronnen die in [!DNL Experience Platform] worden opgenomen.
- [[!DNL Catalog Service]](../../catalog/home.md): Een RESTful-API waarmee u gegevenssets kunt maken en configureren voor [!DNL Real-Time Customer Profile] en [!DNL Identity Service] .
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde framework waarmee [!DNL Experience Platform] gegevens voor de klantervaring indeelt.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan Experience Platform APIs te maken.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan [!DNL Experience Platform] APIs te maken, moet u het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Voor alle aanvragen die een payload (POST, PUT, PATCH) bevatten, is een extra `Content-Type` -header vereist. De correcte waarde voor deze kopbal wordt getoond in de steekproefverzoeken waar nodig.

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Experience Platform] API&#39;s vereisen een `x-sandbox-name` -header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt. Voor meer informatie over zandbakken in [!DNL Experience Platform], zie de [ documentatie van het zandbakoverzicht ](../../sandboxes/home.md).

## Een gegevensset maken die is ingeschakeld voor profiel en identiteit {#create-a-dataset-enabled-for-profile-and-identity}

U kunt een dataset voor het Profiel en de Dienst van de Identiteit van de Klant in real time onmiddellijk op verwezenlijking of op om het even welk punt toelaten nadat de dataset is gecreeerd. Als u een dataset zou willen toelaten die reeds is gecreeerd, de stappen voor [ vormend een bestaande dataset ](#configure-an-existing-dataset) volgen die later in dit document wordt gevonden.

>[!NOTE]
>
>Om een nieuwe profiel-Toegelaten dataset tot stand te brengen, moet u identiteitskaart van een bestaand schema kennen XDM dat voor Profiel wordt toegelaten. Voor informatie over hoe te omhoog kijken of een profiel-Toegelaten schema tot stand brengen, zie het leerprogramma op [ creërend een schema gebruikend de Registratie API van het Schema ](../../xdm/tutorials/create-schema-api.md).

Om een dataset tot stand te brengen die voor Profiel wordt toegelaten, kunt u een POST- verzoek aan het `/dataSets` eindpunt gebruiken.

**API formaat**

```http
POST /dataSets
```

**Verzoek**

Door `unifiedProfile` en `unifiedIdentity` under `tags` op te nemen in de hoofdtekst van de aanvraag, wordt de gegevensset direct ingeschakeld voor respectievelijk [!DNL Profile] en [!DNL Identity Service] . De waarden van deze tags moeten een array zijn met de tekenreeks `"enabled:true"` .

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
        "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
    },
    "tags": {
       "unifiedProfile": ["enabled:true"],
       "unifiedIdentity": ["enabled:true"]
    }
  }'
```

| Eigenschap | Beschrijving |
|---|---|
| `schemaRef.id` | De id van het schema waarvoor [!DNL Profile] is ingeschakeld en waarop de gegevensset wordt gebaseerd. |
| `{TENANT_ID}` | De naamruimte in de [!DNL Schema Registry] die bronnen bevat die tot uw organisatie behoren. Zie [ TENANT_ID ](../../xdm/api/getting-started.md#know-your-tenant-id) sectie van de [!DNL Schema Registry] ontwikkelaarsgids voor meer informatie. |

**Reactie**

Een succesvol antwoord toont een serie die identiteitskaart van de pas gecreëerde dataset in de vorm van `"@/dataSets/{DATASET_ID}"` bevat. Zodra u met succes een dataset hebt gecreeerd en toegelaten, te werk gaan aan de stappen voor [ het uploaden gegevens ](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Een bestaande gegevensset configureren {#configure-an-existing-dataset}

In de volgende stappen wordt beschreven hoe u een eerder gemaakte dataset voor [!DNL Real-Time Customer Profile] en [!DNL Identity Service] kunt inschakelen. Als u reeds een profiel-Toegelaten dataset hebt gecreeerd, te werk gaan aan de stappen voor [ het nemen van gegevens ](#ingest-data-into-the-dataset).

### Controleren of de gegevensset is ingeschakeld {#check-if-the-dataset-is-enabled}

Met de API [!DNL Catalog] kunt u een bestaande dataset inspecteren om te bepalen of deze is ingeschakeld voor gebruik in [!DNL Real-Time Customer Profile] en [!DNL Identity Service] . De volgende vraag wint de details van een dataset door identiteitskaart terug

**API formaat**

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "Commission Program Events DataSet",
        "imsOrg": "{ORG_ID}",
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
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "5b020a27e7040801dedbf46f",
        "files": "@/dataSetFiles?dataSetId=5b020a27e7040801dedbf46e",
        "schema": "@/xdms/context/experienceevent",
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

Onder de eigenschap `tags` ziet u dat `unifiedProfile` en `unifiedIdentity` beide aanwezig zijn met de waarde `enabled:true` . Daarom zijn [!DNL Real-Time Customer Profile] en [!DNL Identity Service] ingeschakeld voor deze gegevensset.

### De gegevensset inschakelen {#enable-the-dataset}

Als de bestaande dataset niet voor [!DNL Profile] of [!DNL Identity Service] is toegelaten, kunt u het toelaten door een PATCH- verzoek te maken gebruikend dataset identiteitskaart

**API formaat**

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
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/tags/unifiedProfile", "value": ["enabled:true"] },
        { "op": "add", "path": "/tags/unifiedIdentity", "value": ["enabled:true"] } 
      ]'
```

De hoofdtekst van de aanvraag bevat een `path` naar twee typen tags, `unifiedProfile` en `unifiedIdentity` . De `value` van elk zijn arrays die de tekenreeks `enabled:true` bevatten.

**Reactie**

Een geslaagde PATCH-aanvraag retourneert HTTP Status 200 (OK) en een array met de id van de bijgewerkte dataset. Deze id moet overeenkomen met de id die in de PATCH-aanvraag is verzonden. De tags `unifiedProfile` en `unifiedIdentity` zijn nu toegevoegd en de gegevensset is ingeschakeld voor gebruik door de services Profiel en Identiteit.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Gegevens in de dataset opnemen {#ingest-data-into-the-dataset}

Zowel [!DNL Real-Time Customer Profile] als [!DNL Identity Service] gebruiken XDM-gegevens terwijl deze in een gegevensset worden opgenomen. Voor instructies op hoe te om gegevens in een dataset te uploaden, verwijs naar het leerprogramma op [ creërend een dataset gebruikend APIs ](../../catalog/datasets/create.md). Houd bij het plannen van de gegevens die u naar de [!DNL Profile] -gegevensset wilt verzenden rekening met de volgende aanbevolen procedures:

- Neem alle gegevens op die u als segmentatiecriteria wilt gebruiken.
- Neem zoveel id&#39;s op als u uit uw profielgegevens kunt opvragen om uw identiteitsgrafiek te maximaliseren. Hierdoor kan [!DNL Identity Service] identiteiten op effectievere wijze aan verschillende gegevenssets koppelen.

## Gegevens die worden ingevoerd door [!DNL Real-Time Customer Profile] bevestigen {#confirm-data-ingest-by-real-time-customer-profile}

Bij het voor het eerst uploaden van gegevens naar een nieuwe gegevensset of als onderdeel van een proces waarbij een nieuwe ETL of gegevensbron betrokken is, wordt aanbevolen de gegevens zorgvuldig te controleren om te controleren of deze op de verwachte wijze zijn geüpload. Met de API voor toegang van [!DNL Real-Time Customer Profile] kunt u batchgegevens ophalen terwijl deze in een gegevensset worden geladen. Als u geen van de entiteiten kunt ophalen die u verwacht, is het mogelijk dat de gegevensset niet is ingeschakeld voor [!DNL Real-Time Customer Profile] . Na het bevestigen dat uw dataset is toegelaten, zorg ervoor dat uw brongegevensformaat en herkenningstekens uw verwachtingen steunen. Voor gedetailleerde instructies op hoe te om [!DNL Real-Time Customer Profile] API te gebruiken om tot [!DNL Profile] gegevens toegang te hebben, gelieve te verwijzen naar de [ gids van het entiteitseindpunt ](../../profile/api/entities.md), die ook als &quot;[!DNL Profile Access]&quot;API wordt bekend.

## Gegevens die door Identity Service worden ingevoerd bevestigen {#confirm-data-ingest-by-identity-service}

Elk opgenomen gegevensfragment dat meer dan één identiteit bevat, maakt een koppeling in uw persoonlijke identiteitsgrafiek. Voor meer informatie over identiteitsgrafieken en de gegevens van de toegangsidentiteit, gelieve te beginnen door het [ overzicht van de Dienst van de Identiteit ](../../identity-service/home.md) te lezen.
