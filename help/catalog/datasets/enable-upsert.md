---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API;gegevensset inschakelen
title: Een gegevensset voor profielupdates inschakelen met behulp van API's
type: Tutorial
description: In deze zelfstudie wordt uitgelegd hoe u Adobe Experience Platform API's kunt gebruiken om een gegevensset met "upsert"-mogelijkheden in te schakelen om updates uit te voeren naar gegevens in het realtime profiel van klanten.
source-git-commit: 3b34cf37182ae98545651a7b54f586df7d811f34
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 0%

---


# Een dataset voor profielupdates inschakelen met behulp van API&#39;s

Deze zelfstudie behandelt het proces waarbij een dataset met &quot;upsert&quot;mogelijkheden wordt toegelaten om updates aan gegevens van het Profiel van de Klant in real time te maken. Dit omvat stappen voor het creëren van een nieuwe dataset en het vormen van een bestaande dataset.

## Aan de slag

Deze zelfstudie vereist een goed begrip van verschillende Adobe Experience Platform-services die betrokken zijn bij het beheer van voor profielen geschikte gegevenssets. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor deze verwante DNL-services voor Platforms:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [[!DNL Catalog Service]](../../catalog/home.md): Een RESTful API die u toestaat om datasets tot stand te brengen en hen te vormen voor  [!DNL Real-time Customer Profile] en  [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Platform] klantenervaring worden georganiseerd.
- [Inname in batch](../../ingestion/batch-ingestion/overview.md)

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan de Platform APIs te maken.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u [!DNL Platform] API&#39;s wilt aanroepen, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen [!DNL Experience Platform], zoals hieronder wordt getoond:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra `Content-Type` kopbal. De correcte waarde voor deze kopbal wordt getoond in de steekproefverzoeken waar nodig.

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Voor alle aanvragen voor [!DNL Platform] API&#39;s is een `x-sandbox-name`-header vereist die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt. Raadpleeg de documentatie [sandbox-overzicht](../../sandboxes/home.md) voor meer informatie over sandboxen in [!DNL Platform].

## Een gegevensset maken die is ingeschakeld voor profielupdates

Wanneer het creëren van een nieuwe dataset, kunt u die dataset voor Profiel toelaten en updatemogelijkheden op het tijdstip van verwezenlijking toelaten.

>[!NOTE]
>
>Om een nieuwe profiel-Toegelaten dataset tot stand te brengen, moet u identiteitskaart van een bestaand schema kennen XDM dat voor Profiel wordt toegelaten. Voor informatie over hoe te om een profiel-Toegelaten schema te onderzoeken of tot stand te brengen, zie het leerprogramma [creërend een schema gebruikend de Registratie API](../../xdm/tutorials/create-schema-api.md) van het Schema.

Om een dataset tot stand te brengen die voor Profiel en updates wordt toegelaten, gebruik een verzoek van de POST aan het `/dataSets` eindpunt.

**API-indeling**

```http
POST /dataSets
```

**Verzoek**

Door `unifiedProfile` onder `tags` in het verzoeklichaam op te nemen, zal de dataset voor [!DNL Profile] op verwezenlijking worden toegelaten. Binnen de `unifiedProfile` serie, zal het toevoegen `isUpsert:true` de capaciteit voor de dataset toevoegen om updates te steunen.

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
        "schemaRef" : {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
          "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "tags" : {
          "unifiedProfile": [
            "enabled:true",
            "isUpsert:true"
          ]
        }
      }'
```

| Eigenschap | Beschrijving |
|---|---|
| `schemaRef.id` | Identiteitskaart van [!DNL Profile]-Toegelaten schema waarop de dataset zal worden gebaseerd. |
| `{TENANT_ID}` | De naamruimte in de [!DNL Schema Registry] die bronnen bevat die bij uw IMS-organisatie horen. Zie de [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) sectie van de [!DNL Schema Registry] ontwikkelaarsgids voor meer informatie. |

**Antwoord**

Een succesvolle reactie toont een serie die identiteitskaart van de pas gecreëerde dataset in de vorm van `"@/dataSets/{DATASET_ID}"` bevat.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Een bestaande gegevensset configureren {#configure-an-existing-dataset}

De volgende stappen behandelen hoe te om een bestaande profiel-Toegelaten dataset voor update (&quot;upsert&quot;) functionaliteit te vormen.

>[!NOTE]
>
>Om een bestaande profiel-Toegelaten dataset voor &quot;upsert&quot;te vormen, moet u eerst de dataset voor Profiel onbruikbaar maken en dan het re-toelaten naast de `isUpsert` markering. Als de bestaande dataset niet voor Profiel wordt toegelaten, kunt u aan de stappen voor [het toelaten van de dataset voor Profiel en upsert](#enable-the-dataset) direct te werk gaan. Als u onzeker bent, tonen de volgende stappen u hoe te om te controleren als de dataset reeds wordt toegelaten.

### Controleren of de gegevensset is ingeschakeld voor profiel

Met de [!DNL Catalog] API kunt u een bestaande dataset inspecteren om te bepalen of het voor gebruik in [!DNL Real-time Customer Profile] wordt toegelaten. De volgende vraag wint de details van een dataset door identiteitskaart terug

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
        "name": "{DATASET_NAME}",
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
            ],
            "unifiedProfile": [
                "enabled:true"
            ]
        },
        "lastBatchId": "{BATCH_ID}",
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
        "viewId": "{VIEW_ID}",
        "status": "enabled",
        "transforms": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/transforms",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "{SCHEMA}",
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

Onder het `tags` bezit, kunt u zien dat `unifiedProfile` met de waarde `enabled:true` aanwezig is. Daarom [!DNL Real-time Customer Profile] wordt toegelaten voor deze dataset.

### De gegevensset voor profiel uitschakelen

Als u een voor profiel ingeschakelde gegevensset voor updates wilt configureren, moet u eerst de tag `unifiedProfile` uitschakelen en deze vervolgens naast de tag `isUpsert` weer inschakelen. Dit wordt gedaan gebruikend twee verzoeken van PATCH, één om onbruikbaar te maken en één om re-toe te laten.

>[!WARNING]
>
>Gegevens die in de gegevensset worden opgenomen terwijl deze is uitgeschakeld, worden niet opgenomen in de profielopslag. Het wordt aanbevolen geen gegevens in de gegevensset in te voeren totdat deze opnieuw is ingeschakeld voor Profiel.

**API-indeling**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parameter | Beschrijving |
|---|---|
| `{DATASET_ID}` | De id van een gegevensset die u wilt bijwerken. |

**Verzoek**

De eerste hoofdtekst van de PATCH-aanvraag bevat de instelling `path` tot `unifiedProfile` van `value` op `enabled:false` om de tag uit te schakelen.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "replace", "path": "/tags/unifiedProfile", "value": ["enabled:false"] },
      ]'
```

**De**
ResponsA succesvolle aanvraag van de PATCH keert HTTP Status 200 (O.K.) en een serie terug die identiteitskaart van de bijgewerkte dataset bevatten. Deze id moet overeenkomen met de id die in de aanvraag voor PATCH is verzonden. De tag `unifiedProfile` is nu uitgeschakeld.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

### De dataset voor Profiel en Bijvoegen inschakelen {#enable-the-dataset}

Een bestaande dataset kan voor de updates van het Profiel en van attributen worden toegelaten gebruikend één enkel verzoek van PATCH.

**API-indeling**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parameter | Beschrijving |
|---|---|
| `{DATASET_ID}` | De id van een gegevensset die u wilt bijwerken. |

**Verzoek**

De aanvraaginstantie bevat een `path` tot `unifiedProfile` die `value` zodanig instelt dat de `enabled`- en `isUpsert`-tags worden opgenomen, beide ingesteld op `true`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/tags/unifiedProfile", "value": ["enabled:true","isUpsert:true"] },
      ]'
```

**De**
ResponsA succesvolle aanvraag van de PATCH keert HTTP Status 200 (O.K.) en een serie terug die identiteitskaart van de bijgewerkte dataset bevatten. Deze id moet overeenkomen met de id die in de aanvraag voor PATCH is verzonden. De tag `unifiedProfile` is nu ingeschakeld en geconfigureerd voor kenmerkupdates.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Volgende stappen

De gegevensset Profiel en Upsert-ingeschakeld kunnen nu worden gebruikt door batch- en streaming ingeslipworkflows om updates uit te voeren voor profielgegevens. Om meer over het opnemen van gegevens in Adobe Experience Platform te leren, gelieve te beginnen door [gegeven te lezen overzicht](../../ingestion/home.md).
