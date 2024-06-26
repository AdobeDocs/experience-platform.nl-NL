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
>De workflow die in deze zelfstudie wordt beschreven, werkt alleen voor batchopname. Raadpleeg de handleiding voor gestreamde opname-upserts [gedeeltelijke rijupdates verzenden naar Real-Time Klantprofiel met Data Prep](../../data-prep/upserts.md).

## Aan de slag

Deze zelfstudie vereist een goed begrip van verschillende Adobe Experience Platform-services die betrokken zijn bij het beheer van voor profielen geschikte gegevenssets. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor deze verwante onderwerpen [!DNL Platform] diensten:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
- [[!DNL Catalog Service]](../../catalog/home.md): Een RESTful API die u toestaat om datasets tot stand te brengen en hen te vormen voor [!DNL Real-Time Customer Profile] en [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waarbinnen [!DNL Platform] organiseert de gegevens van de klantenervaring.
- [Inname in batch](../../ingestion/batch-ingestion/overview.md): Met de API voor batchverwerking kunt u gegevens als batchbestanden in het Experience Platform invoeren.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan Platform APIs te maken.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] gids voor probleemoplossing.

### Waarden verzamelen voor vereiste koppen

Om vraag te maken aan [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in alle [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra `Content-Type` header. De correcte waarde voor deze kopbal wordt getoond in de steekproefverzoeken waar nodig.

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een `x-sandbox-name` header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt. Voor meer informatie over sandboxen in [!DNL Platform], zie de [overzichtsdocumentatie van sandbox](../../sandboxes/home.md).

## Een gegevensset maken die is ingeschakeld voor profielupdates

Wanneer het creëren van een nieuwe dataset, kunt u die dataset voor Profiel toelaten en updatemogelijkheden op het tijdstip van verwezenlijking toelaten.

>[!NOTE]
>
>Om een nieuwe profiel-Toegelaten dataset tot stand te brengen, moet u identiteitskaart van een bestaand schema kennen XDM dat voor Profiel wordt toegelaten. Raadpleeg de zelfstudie voor informatie over het opzoeken of maken van een schema waarvoor profiel is ingeschakeld [een schema maken met de API voor het schemaregister](../../xdm/tutorials/create-schema-api.md).

Om een dataset tot stand te brengen die voor Profiel en updates wordt toegelaten, gebruik een verzoek van de POST aan `/dataSets` eindpunt.

**API-indeling**

```http
POST /dataSets
```

**Verzoek**

Door zowel de `unifiedIdentity` en de `unifiedProfile` krachtens `tags` in de aanvraaginstantie zal de dataset worden toegelaten voor [!DNL Profile] bij het maken. Binnen de `unifiedProfile` array, toevoegen `isUpsert:true` zal de capaciteit voor de dataset toevoegen om updates te steunen.

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
| `schemaRef.id` | De id van de [!DNL Profile]- toegelaten schema waarop de dataset zal worden gebaseerd. |
| `{TENANT_ID}` | De naamruimte binnen de [!DNL Schema Registry] die bronnen van uw organisatie bevat. Zie de [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) van de [!DNL Schema Registry] ontwikkelaarsgids voor meer informatie. |

**Antwoord**

Een succesvolle reactie toont een serie die identiteitskaart van de pas gecreëerde dataset in de vorm van bevat `"@/dataSets/{DATASET_ID}"`.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Een bestaande gegevensset configureren {#configure-an-existing-dataset}

De volgende stappen behandelen hoe te om een bestaande profiel-Toegelaten dataset voor updatefunctionaliteit (upsert) te vormen.

>[!NOTE]
>
>Om een bestaande profiel-Toegelaten dataset voor upsert te vormen, moet u eerst de dataset voor Profiel onbruikbaar maken en dan het naast opnieuw toelaten `isUpsert` -tag. Als de bestaande dataset niet voor Profiel wordt toegelaten, kunt u rechtstreeks aan de stappen te werk gaan voor [het toelaten van de dataset voor Profiel en upsert](#enable-the-dataset). Als u onzeker bent, tonen de volgende stappen u hoe te om te controleren als de dataset reeds wordt toegelaten.

### Controleren of de gegevensset is ingeschakeld voor profiel

Met de [!DNL Catalog] API, kunt u een bestaande dataset inspecteren om te bepalen of het voor gebruik binnen wordt toegelaten [!DNL Real-Time Customer Profile]. De volgende vraag wint de details van een dataset door identiteitskaart terug

**API-indeling**

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

**Antwoord**

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

Onder de `tags` eigenschap, kunt u zien dat `unifiedProfile` is aanwezig met de waarde `enabled:true`. Daarom [!DNL Real-Time Customer Profile] wordt toegelaten voor deze dataset.

### De gegevensset voor profiel uitschakelen

Om een profiel-toegelaten dataset voor updates te vormen, moet u eerst onbruikbaar maken `unifiedProfile` en `unifiedIdentity` -tags en vervolgens weer inschakelen naast de `isUpsert` -tag. Dit wordt gedaan gebruikend twee verzoeken van PATCH, één om onbruikbaar te maken en één om re-toe te laten.

>[!WARNING]
>
>Gegevens die in de gegevensset worden opgenomen terwijl deze is uitgeschakeld, worden niet opgenomen in de profielopslag. U zou moeten vermijden het opnemen van gegevens in de dataset tot het voor Profiel opnieuw is toegelaten.

**API-indeling**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{DATASET_ID}` | De id van de gegevensset die u wilt bijwerken. |

**Verzoek**

De eerste instantie van de PATCH-aanvraag bevat een `path` tot `unifiedProfile` en `path` tot `unifiedIdentity`, de instelling `value` tot `enabled:false` voor beide paden om de tags uit te schakelen.

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

**Antwoord**

Een succesvol PATCH verzoek keert de Status 200 van HTTP (O.K.) en een serie terug die identiteitskaart van de bijgewerkte dataset bevatten. Deze id moet overeenkomen met de id die in de aanvraag voor PATCH is verzonden. De `unifiedProfile` en `unifiedIdentity` tags zijn nu uitgeschakeld.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

### De dataset voor Profiel en Bijvoegen inschakelen {#enable-the-dataset}

Een bestaande dataset kan voor de updates van het Profiel en van attributen worden toegelaten gebruikend één enkel verzoek van PATCH.

>[!IMPORTANT]
>
>Wanneer het toelaten van uw dataset voor Profiel, gelieve te verzekeren het schema de dataset met wordt geassocieerd **ook** Profiel ingeschakeld. Als het schema niet profiel-toegelaten is, zal de dataset **niet** worden weergegeven als profiel-ingeschakeld in de gebruikersinterface van het platform.

**API-indeling**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{DATASET_ID}` | De id van een gegevensset die u wilt bijwerken. |

**Verzoek**

De verzoekende instantie omvat een `path` tot `unifiedProfile` instellen `value` om de `enabled` en `isUpsert` tags, beide ingesteld op `true`en `path` tot `unifiedIdentity` instellen `value` om de `enabled` tag ingesteld op `true`.

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

**Antwoord**

Een succesvol PATCH verzoek keert de Status 200 van HTTP (O.K.) en een serie terug die identiteitskaart van de bijgewerkte dataset bevatten. Deze id moet overeenkomen met de id die in de aanvraag voor PATCH is verzonden. De `unifiedProfile` tag en `unifiedIdentity` tag is nu ingeschakeld en geconfigureerd voor kenmerkupdates.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Volgende stappen

De gegevensset Profiel en Upsert-ingeschakeld kunnen nu worden gebruikt door workflows voor het invoeren van batches om updates van profielgegevens te maken. Als u meer wilt weten over het opnemen van gegevens in Adobe Experience Platform, leest u eerst de [gegevensinvoer - overzicht](../../ingestion/home.md).
