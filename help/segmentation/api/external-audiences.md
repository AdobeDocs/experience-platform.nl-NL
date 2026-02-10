---
title: API-eindpunt voor extern publiek
description: Leer hoe u de API voor extern publiek kunt gebruiken om uw externe publiek te maken, bij te werken, te activeren en te verwijderen uit Adobe Experience Platform.
exl-id: eaa83933-d301-48cb-8a4d-dfeba059bae1
source-git-commit: ff58324446f28cbdca369ecbb58d8261614ae684
workflow-type: tm+mt
source-wordcount: '2340'
ht-degree: 1%

---

# Eindpunt voor extern publiek

Met externe doelgroepen kunt u profielgegevens van externe bronnen uploaden naar Adobe Experience Platform. U kunt het `/external-audience` eindpunt in de Segmentation Service API gebruiken om een extern publiek aan Experience Platform op te nemen, details te bekijken en uw externe publiek bij te werken, evenals uw externe publiek te schrappen.

## Guardrails

Vanaf de release van maart worden de volgende instructies afgedwongen wanneer het eindpunt van het externe publiek wordt gebruikt:

| Guardrail | Limiet | Type limiet | Beschrijving |
| --------- | ----- | ---------- | ----------- |
| Aantal uitgangen van het publiek per dag | 100 | Door het systeem afgedwongen geleiding | Het maximumaantal kijkcijfers dat per dag mag worden ingenomen. Deze grens zoals bij a per **zandbak** niveau. |
| Aantal ingesties per publiek | 10 | Door het systeem afgedwongen geleiding | Het aantal berichten dat op een bepaald publiek kan worden uitgevoerd. |
| Grootte extern publiek | 10 GB | Prestatiegerichting | De aanbevolen totale grootte van het externe publiek is 10 GB. |

## Aan de slag

>[!IMPORTANT]
>
>De eindpunten in deze handleiding worden voorafgegaan door `/core/ais` , in tegenstelling tot `/core/ups` .

om Experience Platform APIs te gebruiken, moet u het [&#x200B; authentificatieleerprogramma &#x200B;](https://www.adobe.com/go/platform-api-authentication-en) hebben voltooid. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in Experience Platform API-aanroepen, zoals hieronder wordt getoond:

- Autorisatie: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Experience Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie bij het werken met zandbakken in [!DNL Experience Platform], zie de [&#x200B; documentatie van het zandbakenoverzicht &#x200B;](../../sandboxes/home.md).

## Extern publiek maken {#create-audience}

U kunt een extern publiek maken door een POST-aanvraag in te dienen bij het eindpunt van `/external-audience/` .

**API formaat**

```http
POST /external-audience/
```

**Verzoek**

+++ Een voorbeeldverzoek om een extern publiek te maken.

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "params": {
                "path": "activation/sample-source/example.csv",
                "type": "file",
                "sourceType": "Cloud Storage",
                "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            }
        },
        "ttlInDays": "40",
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }'
```

| Eigenschap | Type | Beschrijving |
| -------- | ---- | ----------- |
| `name` | String | De naam voor het externe publiek. |
| `description` | String | Een optionele beschrijving voor het externe publiek. |
| `customAudienceId` | String | Een optionele id voor uw externe publiek. |
| `fields` | Array van objecten | De lijst met velden en hun gegevenstypen. Wanneer u de lijst met velden maakt, kunt u de volgende items toevoegen: <ul><li>`name`: **Vereiste** de naam van het gebied dat deel van de externe publieksspecificatie uitmaakt.</li><li>`type`: **Vereiste** het type van gegevens dat in het gebied gaat. Tot de ondersteunde waarden behoren `string`, `number`, `long`, `integer`, `date` (`2025-05-13`), `datetime` (`2025-05-23T20:19:00+00:00`) en `boolean` .</li><li>`identityNs`: **Vereist voor identiteitsgebied** namespace die door het identiteitsgebied wordt gebruikt. Tot de ondersteunde waarden behoren alle geldige naamruimten, zoals `ECID` of `email` .</li><li>`labels`: *Facultatieve* een serie van toegangsbeheeretiketten voor het gebied. Meer informatie over de beschikbare etiketten van de toegangscontrole kan in de [&#x200B; verklarende woordenlijst van de de etiketten van het gegevensgebruik &#x200B;](/help/data-governance/labels/reference.md) worden gevonden. </li></ul> |
| `sourceSpec` | Object | Een object dat de informatie bevat waar het externe publiek zich bevindt. Wanneer het gebruiken van dit voorwerp, moet u **&#x200B;**&#x200B;de volgende informatie omvatten: <ul><li>`path`: **Vereist**: De plaats van het externe publiek of de omslag die het externe publiek binnen de bron bevat. De dossierweg **kan** geen ruimten bevatten. Als het pad bijvoorbeeld `activation/sample-source/Example CSV File.csv` is, stelt u het pad in op `activation/sample-source/ExampleCSVFile.csv` . U kunt de weg aan uw bron binnen de **gegevens van Source** kolom van de dataflows sectie vinden.</li><li>`type`: **Vereist** het type van het voorwerp u uit de bron terugwint. Deze waarde kan `file` of `folder` zijn.</li><li>`sourceType`: *Facultatieve* het type van bron u van terugwint. Momenteel is de enige ondersteunde waarde `Cloud Storage` .</li><li>`cloudType`: **Vereiste** het type van wolkenopslag, die van het brontype wordt gebaseerd. Tot de ondersteunde waarden behoren `S3`, `DLZ`, `GCS`, `Azure` en `SFTP` .</li><li>`baseConnectionId`: De id van de basisverbinding en wordt geleverd door uw bronprovider. Deze waarde wordt **vereist** als het gebruiken van een `cloudType` waarde van `S3`, `GCS`, of `SFTP`. Anders, te hoeven u **niet** om deze parameter te omvatten. Voor meer informatie, te lezen gelieve het [&#x200B; overzicht van bronschakelaars &#x200B;](../../sources/home.md).</li></ul> |
| `ttlInDays` | Geheel | De gegevensvervaldatum voor het externe publiek, in dagen. Deze waarde kan van 1 tot 90 worden geplaatst. De gegevensvervaldatum wordt standaard ingesteld op 30 dagen. |
| `audienceType` | String | Het publiekstype voor het externe publiek. Momenteel wordt alleen `people` ondersteund. |
| `originName` | String | **Vereiste** de oorsprong van het publiek. Dit geeft aan waar het publiek vandaan komt. Gebruik `CUSTOM_UPLOAD` voor externe doelgroepen. |
| `namespace` | String | De naamruimte voor het publiek. Deze waarde wordt standaard ingesteld op `CustomerAudienceUpload` . |
| `labels` | Array van tekenreeksen | De labels van het toegangsbeheer die op het externe publiek van toepassing zijn. Meer informatie over de beschikbare etiketten van de toegangscontrole kan in de [&#x200B; verklarende woordenlijst van de de etiketten van het gegevensgebruik &#x200B;](/help/data-governance/labels/reference.md) worden gevonden. |
| `tags` | Array van tekenreeksen | De tags die u wilt toepassen op het externe publiek. Meer informatie over markeringen kan in [&#x200B; worden gevonden het leiden de gids van markeringen &#x200B;](/help/administrative-tags/ui/managing-tags.md). |

+++

**Reactie**

Een geslaagde reactie retourneert HTTP-status 202 met details van het nieuwe externe publiek.

+++ Een voorbeeldreactie bij het maken van een extern publiek.

```json
{
    "operationId": "df8cd82f-a214-4b72-b549-d6ee23f1ff1a",
    "operationDetails": {
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "Email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "params": {
                "path": "activation/sample-source/example.csv",
                "type": "file",
                "sourceType": "Cloud Storage",
                "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            }
        },
        "ttlInDays": 40,
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }   
}
```

| Eigenschap | Type | Beschrijving |
| -------- | ---- | ----------- |
| `operationId` | String | De id van de bewerking. U kunt deze id vervolgens gebruiken om de status van het maken van de doelgroep op te halen. |
| `operationDetails` | Object | Een object dat de details bevat van het verzoek dat u hebt verzonden om het externe publiek te maken. |
| `name` | String | De naam voor het externe publiek. |
| `description` | String | De beschrijving voor het externe publiek. |
| `fields` | Array van objecten | De lijst met velden en hun gegevenstypen. Deze array bepaalt welke velden u nodig hebt in uw externe publiek. |
| `sourceSpec` | Object | Een object dat de informatie bevat waar het externe publiek zich bevindt. |
| `ttlInDays` | Geheel | De gegevensvervaldatum voor het externe publiek, in dagen. Deze waarde kan van 1 tot 90 worden geplaatst. De gegevensvervaldatum wordt standaard ingesteld op 30 dagen. |
| `audienceType` | String | Het publiekstype voor het externe publiek. |
| `originName` | String | **Vereiste** de oorsprong van het publiek. Dit geeft aan waar het publiek vandaan komt. |
| `namespace` | String | De naamruimte voor het publiek. |
| `labels` | Array van tekenreeksen | De labels van het toegangsbeheer die op het externe publiek van toepassing zijn. Meer informatie over de beschikbare etiketten van de toegangscontrole kan in de [&#x200B; verklarende woordenlijst van de de etiketten van het gegevensgebruik &#x200B;](/help/data-governance/labels/reference.md) worden gevonden. |


+++

## Status van het maken van een publiek ophalen {#retrieve-status}

U kunt de status van uw externe publieksinzending ophalen door een GET-aanvraag in te dienen bij het `/external-audiences/operations` -eindpunt en de id op te geven van de bewerking die u hebt ontvangen van de reactie van het externe publiek maken.

**API formaat**

```http
GET /external-audiences/operations/{OPERATION_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{OPERATION_ID}` | De `id` -waarde van de bewerking die u wilt ophalen. |

**Verzoek**

+++ Een voorbeeldverzoek om de de verrichtingsstatus van een extern publiek terug te winnen.

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/operations/df8cd82f-a214-4b72-b549-d6ee23f1ff1a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met details van de de taakstatus van het externe publiek terug.

+++ Een voorbeeldreactie wanneer u de taakstatus van een extern publiek ophaalt.

```json
{
    "operationId": "df8cd82f-a214-4b72-b549-d6ee23f1ff1a",
    "status": "SUCCESS",
    "operationDetails": {
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "Email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "params": {
                "path": "activation/sample-source/example.csv",
                "type": "file",
                "sourceType": "Cloud Storage",
                "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            }
        },
        "ttlInDays": 40,
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    },
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "createdBy": "{USER_ID}",
    "createdAt": 1749324248,
    "updatedBy": "{USER_ID}",
    "updatedAt": 1749624273
}
```

| Eigenschap | Type | Beschrijving |
| -------- | ---- | ----------- |
| `operationId` | String | De id van de bewerking die u ophaalt. |
| `status` | String | De status van de operatie. Dit kan een van de volgende waarden zijn: `SUCCESS`, `FAILED`, `PROCESSING` . |
| `operationDetails` | Object | Een object dat details van het publiek bevat. |
| `audienceId` | String | De id van het externe publiek dat door de bewerking wordt verzonden. |
| `createdBy` | String | De id van de gebruiker die het externe publiek heeft gemaakt. |
| `createdAt` | Lange tijdstempel | De tijdstempel, in seconden, wanneer het verzoek om het externe publiek te maken is verzonden. |
| `updatedBy` | String | De id van de gebruiker die het publiek voor het laatst heeft bijgewerkt. |
| `updatedAt` | Lange tijdstempel | De tijdstempel, in seconden, toen het publiek voor het laatst werd bijgewerkt. |

+++

## Een extern publiek bijwerken {#update-audience}

>[!NOTE]
>
>Om het volgende eindpunt te gebruiken, moet u `audienceId` van uw extern publiek hebben. U kunt `audienceId` van een succesvolle vraag aan het `GET /external-audiences/operations/{OPERATION_ID}` eindpunt krijgen.

U kunt velden van uw externe publiek bijwerken door een PATCH-aanvraag in te dienen bij het `/external-audience` -eindpunt en de id van het publiek op te geven in het aanvraagpad.

Wanneer u dit eindpunt gebruikt, kunt u de volgende velden bijwerken:

- Beschrijving van het publiek
- Toegangsbeheerlabels op veldniveau
- Toegangsbeheerlabels op het niveau van het publiek
- Vervaldatum van de gegevens van het publiek

Het bijwerken van het gebied gebruikend dit eindpunt **vervangt** de inhoud van het gebied u vroeg.

**API formaat**

```http
PATCH /external-audience/{AUDIENCE_ID}
```

**Verzoek**

+++ Een voorbeeldverzoek om de beschrijving van het externe publiek bij te werken.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab\
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "description": "New sample description"
 }'
```

| Eigenschap | Type | Beschrijving |
| -------- | ---- | ----------- |
| `description` | String | De bijgewerkte beschrijving voor het externe publiek. |

Bovendien kunt u de volgende parameters bijwerken:

| Eigenschap | Type | Beschrijving |
| -------- | ---- | ----------- |
| `labels` | Array | Een array met de bijgewerkte lijst met toegangslabels voor het publiek. Meer informatie over de beschikbare etiketten van de toegangscontrole kan in de [&#x200B; verklarende woordenlijst van de de etiketten van het gegevensgebruik &#x200B;](/help/data-governance/labels/reference.md) worden gevonden. |
| `fields` | Array van objecten | Een array met de velden en de bijbehorende labels voor het externe publiek. Alleen de velden die in het PATCH-verzoek worden vermeld, worden bijgewerkt. Meer informatie over de beschikbare etiketten van de toegangscontrole kan in de [&#x200B; verklarende woordenlijst van de de etiketten van het gegevensgebruik &#x200B;](/help/data-governance/labels/reference.md) worden gevonden. |
| `ttlInDays` | Geheel | De gegevensvervaldatum voor het externe publiek, in dagen. Deze waarde kan van 1 tot 90 worden geplaatst. |

+++

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 met details van het bijgewerkte externe publiek.

+++ Een voorbeeldreactie bij het bijwerken van de beschrijving van het externe publiek.

```json
{
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceName": "Sample external audience",
    "description": "New sample description",
    "fields": [
        {
            "name": "ppid",
            "type": "string",
            "identityNs": "Email"
        },
        {
            "name": "list_id",
            "type": "string",
            "labels": ["core/C2", "custom/deep"]
        },
        {
            "name": "delete",
            "type": "number"
        },
        {
            "name": "process_consent",
            "type": "string"
        }
    ],
    "sourceSpec": {
        "path": "activation/sample-source/example.csv",
        "type": "file",
        "sourceType": "Cloud Storage",
        "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
        },
    "ttlInDays": 40,
    "labels": ["core/C1"],
    "audienceType": "people",
    "originName": "CUSTOM_UPLOAD",
    "createdBy": "{USER_ID}",
    "createdAt": 1749324248,
    "updatedBy": "{USER_ID}",
    "updatedAt": 1749624273
}
```

+++

## Beginnen met publiek starten {#start-audience-ingestion}

>[!IMPORTANT]
>
>U zult **&#x200B;**&#x200B;niet een nieuwe opname voor het externe publiek kunnen beginnen als een vorige publieksinname reeds lopend is.

>[!NOTE]
>
>Om het volgende eindpunt te gebruiken, moet u `audienceId` van uw extern publiek hebben. U kunt `audienceId` van een succesvolle vraag aan het `GET /external-audiences/operations/{OPERATION_ID}` eindpunt krijgen.

U kunt een publieksopname beginnen door een POST- verzoek aan het volgende eindpunt te doen terwijl het verstrekken van publiekidentiteitskaart

**API formaat**

```http
POST /external-audience/{AUDIENCE_ID}/runs
```

**Verzoek**

De volgende aanvraag activeert een opname die voor het externe publiek wordt uitgevoerd.

+++ Een voorbeeldaanvraag om een opname voor het publiek te starten.

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/runs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "dataFilterStartTime": 764245635
 }' 
```

| Eigenschap | Type | Beschrijving |
| -------- | ---- | ----------- |
| `dataFilterStartTime` | Tijdstempel tijdperk | **Vereiste** de waaier die de beginnende tijd specificeren om te bepalen welke dossiers zullen worden verwerkt. Dit betekent dat de geselecteerde dossiers **na** de gespecificeerde tijd zullen zijn. |
| `dataFilterEndTime` | Tijdstempel tijdperk | Het bereik dat de eindtijd opgeeft die de flow moet gebruiken om te selecteren welke bestanden worden verwerkt. Dit betekent dat de geselecteerde dossiers **vóór** de gespecificeerde tijd zullen zijn. |

+++

**Reactie**

Een geslaagde reactie retourneert HTTP status 200 met details over de opname run.

+++ Een voorbeeldreactie bij het starten van de opname van het publiek.

```json
{
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
    "differentialIngestion": true,
    "dataFilterStartTime": 764245635,
    "dataFilterEndTime": 4565657575,
    "createdAt": 4565657575,
    "createdBy:" "{USER_ID}"
}
```

| Eigenschap | Type | Beschrijving |
| -------- | ---- | ----------- |
| `audienceName` | String | De naam van het publiek waarvoor u een opname start. |
| `audienceId` | String | De id van het publiek. |
| `runId` | String | De id van de opname die u hebt gestart. |
| `differentialIngestion` | Boolean | Een veld dat bepaalt of de opname een gedeeltelijke opname is op basis van het verschil sinds de laatste opname of een volledige opname van het publiek. |
| `dataFilterStartTime` | Tijdstempel tijdperk | Het bereik dat de begintijd opgeeft waarop de stroom wordt uitgevoerd om te selecteren welke bestanden zijn verwerkt. |
| `dataFilterEndTime` | Tijdstempel tijdperk | Het bereik dat de eindtijd opgeeft waarop de stroom wordt uitgevoerd om te selecteren welke bestanden zijn verwerkt. |
| `createdAt` | Lange tijdstempel | De tijdstempel, in seconden, wanneer het verzoek om het externe publiek te maken is verzonden. |
| `createdBy` | String | De id van de gebruiker die het externe publiek heeft gemaakt. |

+++

## Specifieke inspraakstatus van het publiek ophalen {#retrieve-ingestion-status}

>[!NOTE]
>
>Als u het volgende eindpunt wilt gebruiken, moet u zowel de `audienceId` van uw externe publiek als de `runId` van de id van de invoeringsuitvoering hebben. U kunt `audienceId` van een succesvolle vraag aan het `GET /external-audiences/operations/{OPERATION_ID}` eindpunt en uw `runId` van een vorige succesvolle vraag van het `POST /external-audience/{AUDIENCE_ID}/runs` eindpunt krijgen.

U kunt de status van een publieksinvoer terugwinnen door een GET- verzoek aan het volgende eindpunt te doen terwijl het verstrekken van zowel het publiek als looppas IDs.

**API formaat**

```http
GET /external-audience/{AUDIENCE_ID}/runs/{RUN_ID}
```

**Verzoek**

Het volgende verzoek wint de innamestatus voor het externe publiek terug.

+++ Een voorbeeldverzoek om de inspraakstatus van het externe publiek op te halen.

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/runs/fb342311-725d-4b48-ab7d-c6105fbc2b8b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met details van de externe publieksinvoer terug.

+++ Een voorbeeldreactie bij het ophalen van de opname van het externe publiek.

```json
{
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
    "status": "SUCCESS",
    "differentialIngestion": true,
    "dataFilterStartTime": 764245635,
    "dataFilterEndTime": 3456788568,
    "createdAt": 1749324248,
    "createdBy": "{USER_ID}",
    "details": [
        {
            "stage": "DATASET_INGEST",
            "status": "SUCCESS",
            "flowRunId": "{FLOW_RUN_ID}"
        },
        {
            "stage": "PROFILE_STORE_INGEST",
            "status": "SUCCESS",
            "flowRunId": "{FLOW_RUN_ID}"
        }
    ]
}
```

| Eigenschap | Type | Beschrijving |
| -------- | ---- | ----------- |
| `audienceName` | String | De naam van het publiek. |
| `audienceId` | String | De id van het publiek. |
| `runId` | String | De id van de inlogrun. |
| `status` | String | De status van de opname. Mogelijke statussen zijn `SUCCESS` en `FAILED` . |
| `differentialIngestion` | Boolean | Een veld dat bepaalt of de opname een gedeeltelijke opname is op basis van het verschil sinds de laatste opname of een volledige opname van het publiek. |
| `dataFilterStartTime` | Tijdstempel tijdperk | Het bereik dat de begintijd opgeeft waarop de stroom wordt uitgevoerd om te selecteren welke bestanden zijn verwerkt. |
| `dataFilterEndTime` | Tijdstempel tijdperk | Het bereik dat de eindtijd opgeeft waarop de stroom wordt uitgevoerd om te selecteren welke bestanden zijn verwerkt. |
| `createdAt` | Lange tijdstempel | De tijdstempel, in seconden, wanneer het verzoek om het externe publiek te maken is verzonden. |
| `createdBy` | String | De id van de gebruiker die het externe publiek heeft gemaakt. |
| `details` | Array van objecten | Een object dat de details van de invoerbewerking bevat. <ul><li>`stage`: Het werkgebied van de opname. Dit kan `DATASET_INGEST` of `PROFILE_STORE_INGEST` zijn, die de opname van het gegevensmeer en de profielopname vertegenwoordigen.</li><li>`status`: De status van de opname in het werkgebied. Mogelijke statussen zijn `SUCCESS` en `FAILED` .</li><li>`flowRunId`: De id van de invoerstroom van het werkgebied.</li></ul> |

+++

## Voer publieksinvoer weergeven {#list-ingestion-runs}

>[!NOTE]
>
>Om het volgende eindpunt te gebruiken, moet u `audienceId` van uw extern publiek hebben. U kunt `audienceId` van een succesvolle vraag aan het `GET /external-audiences/operations/{OPERATION_ID}` eindpunt krijgen.

U kunt alle ingestitielooppas voor het geselecteerde externe publiek terugwinnen door een verzoek van GET aan het volgende eindpunt te doen terwijl het verstrekken van publiekID. De veelvoudige parameters kunnen worden omvat, die door ampersands (`&`) worden gescheiden.

**API formaat**

<!-- The following endpoint supports several query parameters to help filter your results. While these parameters are optional, their use is strongly recommended to help focus your results. -->

```http
GET /external-audience/{AUDIENCE_ID}/runs
```

<!-- **Query parameters**

+++ A list of available query parameters. 

| Parameter | Description | Example |
| --------- | ----------- | ------- |
| `limit` | The maximum number of items returned in the response. This value can range from 1 to 40. By default, the limit is set to 20. | `limit=30` |
| `sortBy` | The order in which the returned items are sorted. You can sort by either `name` or by `createdAt`. Additionally, you can add a `-` sign to sort by **descending** order instead of **ascending** order. By default, the items are sorted by `createdAt` in descending order. | `sortBy=name` |
| `property` | A filter to determine which audience ingestion runs are displayed. You can filter on the following properties: <ul><li>`name`: Lets you filter by the audience name. If using this property, you can compare by using `=`, `!=`, `=contains`, or `!=contains`. </li><li>`createdAt`: Lets you filter by the ingestion time. If using this property, you can compare by using `>=` or `<=`.</li><li>`status`: Lets you filter by the ingestion run's status. If using this property, you can compare by using `=`, `!=`, `=contains`, or `!=contains`. </li></ul>  | `property=createdAt<1683669114845`<br/>`property=name=demo_audience`<br/>`property=status=SUCCESS` |

+++ -->

**Verzoek**

Het volgende verzoek wint alle ingestitielooppas voor het externe publiek terug.

+++ Een steekproefverzoek om een lijst van publieksinname looppas te krijgen.

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/runs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met een lijst van ingestitielooppas voor het gespecificeerde externe publiek terug.

+++ Een voorbeeldreactie wanneer u een lijst van de publieksinname terugwint looppas.

```json
{
    "runs": [
        {
            "audienceName": "Sample external audience",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
            "status": "SUCCESS",
            "differentialIngestion": true,
            "dataFilterStartTime": 764245635,
            "dataFilterEndTime": 3456788568,
            "createdAt": 1785678909,
            "createdBy": "{USER_NAME}"
        },
        {
            "audienceName": "Sample external audience 2",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "runId": "406e38e4-fbd5-43e1-8d0c-01ccb3f9ad10",
            "status": "SUCCESS",
            "differentialIngestion": true,
            "dataFilterStartTime": 764245635,
            "dataFilterEndTime": 3456788568,
            "createdAt": 1749324248,
            "createdBy": "{USER_ID}"
        }
    ]
}
```

<!-- ,
    "_page": {
        "limit": 20,
        "count": 2,
        "totalCount": 2
    }
    
| `_page` | Object | An object that contains the pagination information about the list of results. |
     -->

| Eigenschap | Type | Beschrijving |
| -------- | ---- | ----------- |
| `runs` | Object | Een voorwerp dat de lijst van ingestie looppas bevat die tot het publiek behoort. Meer informatie over dit voorwerp kan in [&#x200B; worden gevonden wint sectie van de inspraakstatus &#x200B;](#retrieve-ingestion-status) terug. |

+++

## Een extern publiek verwijderen {#delete-audience}

>[!NOTE]
>
>Om het volgende eindpunt te gebruiken, moet u `audienceId` van uw extern publiek hebben. U kunt `audienceId` van een succesvolle vraag aan het `GET /external-audiences/operations/{OPERATION_ID}` eindpunt krijgen.

U kunt een extern publiek schrappen door een verzoek van DELETE aan het volgende eindpunt te doen terwijl het verstrekken van publiekID.

**API formaat**

```http
DELETE /external-audience/{AUDIENCE_ID}
```

**Verzoek**

Met het volgende verzoek verwijdert u het opgegeven externe publiek.

+++ Een voorbeeldverzoek om het externe publiek te verwijderen.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een geslaagde reactie retourneert HTTP status 204 met een lege response body.

## Volgende stappen {#next-steps}

Na het lezen van deze handleiding hebt u nu een beter inzicht in hoe u uw externe publiek kunt maken, beheren en verwijderen met de Experience Platform API&#39;s. Leren hoe te om extern publiek met Experience Platform UI te gebruiken, te lezen gelieve de [&#x200B; Poortdocumentatie van het Poort van het Publiek &#x200B;](../ui/audience-portal.md).

## Bijlage {#appendix}

In de volgende sectie worden de beschikbare foutcodes weergegeven wanneer de externe publiek-API wordt gebruikt.

| Platformfoutcode | Statuscode | Bericht | Beschrijving |
| ------------------- | ----------- | ------- | ----------- |
| 100910-400 | 400 | `BAD_REQUEST` | Er is een ongeldig verzoek opgetreden als gevolg van een fout tijdens het valideren van de aanvragen. |
| 100911-400 | 400 | `BAD_REQUEST` | Er is een ongeldig token opgegeven. |
| 100920-401 | 401 | `UNAUTHORIZED` | Er ontbreekt een koptekst. |
| 100921-401 | 401 | `UNAUTHORIZED` | Er is een ongeldige `imsOrgId` opgegeven. |
| 100922-401 | 401 | `UNAUTHORIZED` | U bent niet bevoegd om de API&#39;s voor externe doelgroepen te gebruiken. |
| 100940-404 | 404 | `NOT_FOUND` | Het gewenste publiek is niet gevonden. |
| 100950-409 | 409 | `DUPLICATE_RESOURCE` | Het publiek bestaat al. |
| 100960-422 | 422 | `UNPROCESSABLE_ENTITY` | De aanvraagstructuur is geldig, maar kan niet worden verwerkt vanwege logische of semantische fouten. |
| 100970-500 | 500 | `INTERNAL_SERVER_ERROR` | Er is een probleem opgetreden bij het verwerken van het verzoek in het systeem. |
| 100970-502 | 502 | `BAD_GATEWAY` | Er zijn kwesties met betrekking tot afhankelijkheid in de stroomafwaartse richting. |
