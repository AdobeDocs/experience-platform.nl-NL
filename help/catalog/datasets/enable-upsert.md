---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API;gegevensset inschakelen
title: Een gegevensset voor profielupdates inschakelen met behulp van API's
type: Tutorial
description: In deze zelfstudie wordt uitgelegd hoe u Adobe Experience Platform API's kunt gebruiken om een gegevensset met "upsert"-mogelijkheden in te schakelen om updates uit te voeren naar gegevens in het realtime profiel van klanten.
exl-id: fc89bc0a-40c9-4079-8bfc-62ec4da4d16a
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 0%

---

# Een dataset voor profielupdates inschakelen met behulp van API&#39;s

Deze zelfstudie behandelt het proces waarbij een dataset met &quot;upsert&quot;mogelijkheden wordt toegelaten om updates aan gegevens van het Profiel van de Klant in real time te maken. Dit omvat stappen voor het creëren van een nieuwe dataset en het vormen van een bestaande dataset.

>[!NOTE]
>
>De workflow die in deze zelfstudie wordt beschreven, werkt alleen voor batchopname. Voor het stromen opnemen upserts, gelieve te verwijzen naar de gids bij [ verzendend gedeeltelijke rijupdates naar het Profiel van de Klant in real time gebruikend Prep van Gegevens ](../../data-prep/upserts.md).

## Aan de slag

Deze zelfstudie vereist een goed begrip van verschillende Adobe Experience Platform-services die betrokken zijn bij het beheer van voor profielen geschikte gegevenssets. Lees vóór het starten van deze zelfstudie de documentatie voor deze verwante [!DNL Platform] services:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
- [[!DNL Catalog Service]](../../catalog/home.md): Een RESTful-API waarmee u gegevenssets kunt maken en configureren voor [!DNL Real-Time Customer Profile] en [!DNL Identity Service] .
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde framework waarmee [!DNL Platform] gegevens voor de klantervaring indeelt.
- [ Inname van de Partij ](../../ingestion/batch-ingestion/overview.md): De Ingestie API van de Partij staat u toe om gegevens in Experience Platform als partijdossiers in te voeren.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan Platform APIs te maken.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan [!DNL Platform] APIs te maken, moet u het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra `Content-Type` kopbal. De correcte waarde voor deze kopbal wordt getoond in de steekproefverzoeken waar nodig.

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Platform] API&#39;s vereisen een `x-sandbox-name` -header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt. Voor meer informatie over zandbakken in [!DNL Platform], zie de [ documentatie van het zandbakoverzicht ](../../sandboxes/home.md).

## Een gegevensset maken die is ingeschakeld voor profielupdates

Wanneer het creëren van een nieuwe dataset, kunt u die dataset voor Profiel toelaten en updatemogelijkheden op het tijdstip van verwezenlijking toelaten.

>[!NOTE]
>
>Om een nieuwe profiel-Toegelaten dataset tot stand te brengen, moet u identiteitskaart van een bestaand schema kennen XDM dat voor Profiel wordt toegelaten. Voor informatie over hoe te omhoog kijken of een profiel-Toegelaten schema tot stand brengen, zie het leerprogramma op [ creërend een schema gebruikend de Registratie API van het Schema ](../../xdm/tutorials/create-schema-api.md).

Om een dataset tot stand te brengen die voor Profiel en updates wordt toegelaten, gebruik een verzoek van de POST aan het `/dataSets` eindpunt.

**API formaat**

```http
POST /dataSets
```

**Verzoek**

Door zowel de `unifiedIdentity` als de `unifiedProfile` under `tags` in de hoofdtekst van de aanvraag op te nemen, wordt de gegevensset ingeschakeld voor [!DNL Profile] bij het maken. Als u `isUpsert:true` toevoegt binnen de array `unifiedProfile` , kan de dataset updates ondersteunen.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Sample dataset",
        "description: "A sample dataset with a sample description.",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "tags": {
            "unifiedIdentity": [
                "enabled: true"
            ],
            "unifiedProfile": [
                "enabled: true",
                "isUpsert: true"
            ]
        }
      }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `schemaRef.id` | De id van het schema waarvoor [!DNL Profile] is ingeschakeld en waarop de gegevensset wordt gebaseerd. |
| `{TENANT_ID}` | De naamruimte in de [!DNL Schema Registry] die bronnen bevat die tot uw organisatie behoren. Zie [ TENANT_ID ](../../xdm/api/getting-started.md#know-your-tenant-id) sectie van de [!DNL Schema Registry] ontwikkelaarsgids voor meer informatie. |

**Reactie**

Een succesvol antwoord toont een serie die identiteitskaart van de pas gecreëerde dataset in de vorm van `"@/dataSets/{DATASET_ID}"` bevat.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Een bestaande gegevensset configureren {#configure-an-existing-dataset}

De volgende stappen behandelen hoe te om een bestaande profiel-Toegelaten dataset voor updatefunctionaliteit (upsert) te vormen.

>[!NOTE]
>
>Om een bestaande profiel-Toegelaten dataset voor upsert te vormen, moet u eerst de dataset voor Profiel onbruikbaar maken en dan het naast de `isUpsert` markering re-toelaten. Als de bestaande dataset niet voor Profiel wordt toegelaten, kunt u rechtstreeks aan de stappen voor [ te werk gaan toelatend de dataset voor Profiel en ](#enable-the-dataset) te steunen. Als u onzeker bent, tonen de volgende stappen u hoe te om te controleren als de dataset reeds wordt toegelaten.

### Controleren of de gegevensset is ingeschakeld voor profiel

Met de API van [!DNL Catalog] kunt u een bestaande dataset inspecteren om te bepalen of deze is ingeschakeld voor gebruik in [!DNL Real-Time Customer Profile] . De volgende vraag wint de details van een dataset door identiteitskaart terug

**API formaat**

```http
GET /dataSets/{DATASET_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{DATASET_ID}` | De id van een gegevensset die u wilt inspecteren. |

**Verzoek**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "{DATASET_NAME}",
        "imsOrg": "{ORG_ID}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ],
            "unifiedProfile": [
                "enabled:true"
            ]
        },
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "{VIEW_ID}",
        "files": "@/dataSetFiles?dataSetId=5b020a27e7040801dedbf46e",
        "schema": "{SCHEMA}",
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

Onder de eigenschap `tags` ziet u dat `unifiedProfile` aanwezig is met de waarde `enabled:true` . Daarom is [!DNL Real-Time Customer Profile] ingeschakeld voor deze gegevensset.

### De gegevensset voor profiel uitschakelen

Als u een voor profiel geschikte gegevensset wilt configureren voor updates, moet u eerst de tags `unifiedProfile` en `unifiedIdentity` uitschakelen en deze vervolgens weer inschakelen naast de tag `isUpsert` . Dit wordt gedaan gebruikend twee verzoeken van PATCH, één om onbruikbaar te maken en één om re-toe te laten.

>[!WARNING]
>
>Gegevens die in de gegevensset worden opgenomen terwijl deze is uitgeschakeld, worden niet opgenomen in de profielopslag. U zou moeten vermijden het opnemen van gegevens in de dataset tot het voor Profiel opnieuw is toegelaten.

**API formaat**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{DATASET_ID}` | De id van de gegevensset die u wilt bijwerken. |

**Verzoek**

De eerste hoofdtekst van de PATCH-aanvraag bevat een lus `path` to `unifiedProfile` en een lus `path` to `unifiedIdentity` , waarbij de waarde `value` op `enabled:false` voor beide paden wordt ingesteld om de tags uit te schakelen.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { 
            "op": "replace", 
            "path": "/tags/unifiedProfile", 
            "value": ["enabled:false"] 
        },
        {
            "op": "replace",
            "path": "/tags/unifiedIdentity",
            "value": ["enabled:false"]
        }
      ]'
```

**Reactie**

Een succesvol PATCH verzoek keert de Status 200 van HTTP (O.K.) en een serie terug die identiteitskaart van de bijgewerkte dataset bevatten. Deze id moet overeenkomen met de id die in de aanvraag voor PATCH is verzonden. De tags `unifiedProfile` en `unifiedIdentity` zijn nu uitgeschakeld.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

### De dataset voor Profiel en Bijvoegen inschakelen {#enable-the-dataset}

Een bestaande dataset kan voor de updates van het Profiel en van attributen worden toegelaten gebruikend één enkel verzoek van PATCH.

>[!IMPORTANT]
>
>Wanneer het toelaten van uw dataset voor Profiel, gelieve te verzekeren het schema de dataset met wordt geassocieerd is **ook** profiel-toegelaten. Als het schema niet profiel-toegelaten is, zal de dataset **niet** als profiel-toegelaten binnen Platform UI verschijnen.

**API formaat**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{DATASET_ID}` | De id van een gegevensset die u wilt bijwerken. |

**Verzoek**

De hoofdtekst van de aanvraag bevat een `path` tot `unifiedProfile` instelling van `value` om de tags `enabled` en `isUpsert` op te nemen, beide ingesteld op `true` en een `path` tot `unifiedIdentity` instelling van `value` om de tag `enabled` op te nemen die is ingesteld op `true` .

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { 
            "op": "add", 
            "path": "/tags/unifiedProfile", 
            "value": [
                "enabled:true",
                "isUpsert:true"
            ] 
        },
        {
            "op": "add",
            "path": "/tags/unifiedIdentity",
            "value": [
                "enabled:true"
            ]
        }
      ]'
```

**Reactie**

Een succesvol PATCH verzoek keert de Status 200 van HTTP (O.K.) en een serie terug die identiteitskaart van de bijgewerkte dataset bevatten. Deze id moet overeenkomen met de id die in de aanvraag voor PATCH is verzonden. De tag `unifiedProfile` en de tag `unifiedIdentity` zijn nu ingeschakeld en geconfigureerd voor kenmerkupdates.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Volgende stappen

De gegevensset Profiel en Upsert-ingeschakeld kunnen nu worden gebruikt door workflows voor het invoeren van batches om updates van profielgegevens te maken. Om meer over het opnemen van gegevens in Adobe Experience Platform te leren, gelieve te beginnen door het [ overzicht van de gegevensinvoer te lezen ](../../ingestion/home.md).
