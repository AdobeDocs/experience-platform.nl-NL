---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API;gegevensset inschakelen
title: Een gegevensset voor profiel- en identiteitsservice inschakelen met behulp van API's
type: Tutorial
description: Deze zelfstudie laat u zien hoe u een gegevensset inschakelt voor gebruik met Real-time Customer Profile and Identity Service met Adobe Experience Platform API's.
exl-id: a115e126-6775-466d-ad7e-ee36b0b8b49c
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 0%

---

# Een gegevensset inschakelen voor [!DNL Profile] en [!DNL Identity Service] gebruiken, API&#39;s

Deze zelfstudie behandelt het proces waarbij een gegevensset wordt ingeschakeld voor gebruik in [!DNL Real-time Customer Profile] en [!DNL Identity Service], onderverdeeld in de volgende stappen:

1. Een gegevensset inschakelen voor gebruik in [!DNL Real-time Customer Profile]met een van de volgende twee opties:
   - [Een nieuwe gegevensset maken](#create-a-dataset-enabled-for-profile-and-identity)
   - [Een bestaande gegevensset configureren](#configure-an-existing-dataset)
1. [Gegevens in de dataset opnemen](#ingest-data-into-the-dataset)
1. [Gegevens bevestigen die door het Profiel van de Klant in real time worden opgenomen](#confirm-data-ingest-by-real-time-customer-profile)
1. [Gegevens die door Identity Service worden ingevoerd bevestigen](#confirm-data-ingest-by-identity-service)

## Aan de slag

Deze zelfstudie vereist een goed begrip van verschillende Adobe Experience Platform-services die betrokken zijn bij het beheer van voor profielen geschikte gegevenssets. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor deze verwante DNL-services voor Platforms:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [[!DNL Identity Service]](../../identity-service/home.md): Inschakelen [!DNL Real-time Customer Profile] door identiteiten te overbruggen van verschillende gegevensbronnen waarin [!DNL Platform].
- [[!DNL Catalog Service]](../../catalog/home.md): Een RESTful API die u toestaat om datasets tot stand te brengen en hen te vormen voor [!DNL Real-time Customer Profile] en [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Platform] organiseert de gegevens van de klantenervaring.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan de Platform APIs te maken.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] gids voor probleemoplossing.

### Waarden verzamelen voor vereiste koppen

Om vraag te maken aan [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in alle [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra `Content-Type` header. De correcte waarde voor deze kopbal wordt getoond in de steekproefverzoeken waar nodig.

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een `x-sandbox-name` header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt. Voor meer informatie over sandboxen in [!DNL Platform], zie de [overzichtsdocumentatie van sandbox](../../sandboxes/home.md).

## Een gegevensset maken die is ingeschakeld voor profiel en identiteit {#create-a-dataset-enabled-for-profile-and-identity}

U kunt een dataset voor het Profiel en de Dienst van de Identiteit van de Klant in real time onmiddellijk op verwezenlijking of op om het even welk punt toelaten nadat de dataset is gecreeerd. Als u een dataset zou willen toelaten die reeds is gecreeerd, volg de stappen voor [het vormen van een bestaande dataset](#configure-an-existing-dataset) gevonden verderop in dit document.

>[!NOTE]
>
>Om een nieuwe profiel-Toegelaten dataset tot stand te brengen, moet u identiteitskaart van een bestaand schema kennen XDM dat voor Profiel wordt toegelaten. Raadpleeg de zelfstudie voor informatie over het opzoeken of maken van een schema waarvoor profiel is ingeschakeld [het creëren van een schema gebruikend de Registratie API van het Schema](../../xdm/tutorials/create-schema-api.md).

Om een dataset tot stand te brengen die voor Profiel wordt toegelaten, kunt u een verzoek van de POST aan `/dataSets` eindpunt.

**API-indeling**

```http
POST /dataSets
```

**Verzoek**

Door `unifiedProfile` en `unifiedIdentity` krachtens `tags` in de aanvraaginstantie zal de gegevensset onmiddellijk worden ingeschakeld voor [!DNL Profile] en [!DNL Identity Service], respectievelijk. De waarden van deze tags moeten een array zijn die de tekenreeks bevat `"enabled:true"`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields":[],
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
| `schemaRef.id` | De id van de [!DNL Profile]- toegelaten schema waarop de dataset zal worden gebaseerd. |
| `{TENANT_ID}` | De naamruimte binnen de [!DNL Schema Registry] die bronnen van uw IMS-organisatie bevat. Zie de [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) van de [!DNL Schema Registry] ontwikkelaarsgids voor meer informatie. |

**Antwoord**

Een succesvolle reactie toont een serie die identiteitskaart van de pas gecreëerde dataset in de vorm van bevat `"@/dataSets/{DATASET_ID}"`. Nadat u een gegevensset hebt gemaakt en ingeschakeld, gaat u verder met de stappen voor [gegevens uploaden](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Een bestaande gegevensset configureren {#configure-an-existing-dataset}

De volgende stappen behandelen hoe te om een eerder gecreeerde dataset voor toe te laten [!DNL Real-time Customer Profile] en [!DNL Identity Service]. Als u reeds een profiel-Toegelaten dataset hebt gecreeerd, gelieve te werk te gaan aan de stappen voor [opnemen, gegevens](#ingest-data-into-the-dataset).

### Controleren of de gegevensset is ingeschakeld {#check-if-the-dataset-is-enabled}

Met de [!DNL Catalog] API, kunt u een bestaande dataset inspecteren om te bepalen of het voor gebruik binnen wordt toegelaten [!DNL Real-time Customer Profile] en [!DNL Identity Service]. De volgende vraag wint de details van een dataset door identiteitskaart terug

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

Onder de `tags` eigenschap, kunt u zien dat `unifiedProfile` en `unifiedIdentity` zijn beide aanwezig met de waarde `enabled:true`. Daarom [!DNL Real-time Customer Profile] en [!DNL Identity Service] zijn ingeschakeld voor deze gegevensset.

### De gegevensset inschakelen {#enable-the-dataset}

Als de bestaande gegevensset niet is ingeschakeld voor [!DNL Profile] of [!DNL Identity Service], kunt u het toelaten door een verzoek van de PATCH te maken gebruikend dataset identiteitskaart

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
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/tags/unifiedProfile", "value": ["enabled:true"] },
        { "op": "add", "path": "/tags/unifiedIdentity", "value": ["enabled:true"] } 
      ]'
```

De verzoekende instantie omvat een `path` tot twee typen tags, `unifiedProfile` en `unifiedIdentity`. De `value` van elk zijn arrays die de tekenreeks bevatten `enabled:true`.

**Antwoord**
Een succesvol PATCH verzoek keert de Status 200 van HTTP (O.K.) en een serie terug die identiteitskaart van de bijgewerkte dataset bevatten. Deze id moet overeenkomen met de id die in de aanvraag voor PATCH is verzonden. De `unifiedProfile` en `unifiedIdentity` Er zijn nu codes toegevoegd en de gegevensset is ingeschakeld voor gebruik door de services Profiel en Identiteit.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Gegevens in de dataset opnemen {#ingest-data-into-the-dataset}

Beide [!DNL Real-time Customer Profile] en [!DNL Identity Service] verbruikt XDM gegevens aangezien het in een dataset wordt opgenomen. Voor instructies over hoe te om gegevens in een dataset te uploaden, verwijs naar de zelfstudie op [maken van een gegevensset met behulp van API&#39;s](../../catalog/datasets/create.md). Wanneer u plant welke gegevens u naar uw [!DNL Profile]- toegelaten dataset, overweeg de volgende beste praktijken:

- Neem alle gegevens op die u als segmentatiecriteria wilt gebruiken.
- Neem zoveel id&#39;s op als u uit uw profielgegevens kunt opvragen om uw identiteitsgrafiek te maximaliseren. Dit maakt [!DNL Identity Service] om identiteiten over datasets effectiever te binden.

## Gegevens bevestigen die worden ingevoerd door [!DNL Real-time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

Bij het voor het eerst uploaden van gegevens naar een nieuwe gegevensset of als onderdeel van een proces waarbij een nieuwe ETL of gegevensbron betrokken is, wordt aanbevolen de gegevens zorgvuldig te controleren om te controleren of deze op de verwachte wijze zijn geüpload. Met de [!DNL Real-time Customer Profile] Toegang API, kunt u partijgegevens terugwinnen aangezien het in een dataset wordt geladen. Als u geen van de entiteiten kunt terugwinnen u verwacht, kan uw dataset niet worden toegelaten voor [!DNL Real-time Customer Profile]. Na het bevestigen dat uw dataset is toegelaten, zorg ervoor dat uw brongegevensformaat en herkenningstekens uw verwachtingen steunen. Voor gedetailleerde instructies over het gebruik van de [!DNL Real-time Customer Profile] API voor toegang [!DNL Profile] gegevens, raadpleeg de [eindgebruikershandleiding voor entiteiten](../../profile/api/entities.md), ook wel bekend als &quot;[!DNL Profile Access]&quot; API.

## Gegevens die door Identity Service worden ingevoerd bevestigen {#confirm-data-ingest-by-identity-service}

Elk opgenomen gegevensfragment dat meer dan één identiteit bevat, maakt een koppeling in uw persoonlijke identiteitsgrafiek. Voor meer informatie over identiteitsgrafieken en toegang tot identiteitsgegevens, gelieve te beginnen door te lezen [Overzicht van identiteitsservice](../../identity-service/home.md).
