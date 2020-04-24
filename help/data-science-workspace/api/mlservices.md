---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Services
topic: Developer guide
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# MLServices

Een dienst MLService is een gepubliceerd opgeleid model dat uw organisatie van de capaciteit voorziet om tot eerder ontwikkelde modellen toegang te hebben en te hergebruiken. Een belangrijk kenmerk van MLServices is de mogelijkheid om training en scoring op een geplande basis te automatiseren. De geplande trainingslooppas kan helpen de efficiency en nauwkeurigheid van een model handhaven, terwijl de geplande scoring looppas kan ervoor zorgen dat de nieuwe inzichten constant worden geproduceerd.

Geautomatiseerde trainings- en scoreschema&#39;s worden gedefinieerd met een begintijdstempel, een eindtijdstempel en een frequentie die wordt weergegeven als een <a href="https://en.wikipedia.org/wiki/Cron" target="_blank">uitsnijdexpressie</a>. U kunt planningen definiëren wanneer u een MLService [](#create-an-mlservice) maakt of toepassen door een bestaande MLService [bij te werken](#update-an-mlservice).

## Een MLService maken {#create-an-mlservice}

U kunt een dienst tot stand brengen MLService door een POST- verzoek en een lading uit te voeren die een naam voor de dienst en een geldige identiteitskaart MLInstance verstrekt. De MLInstance die wordt gebruikt om een dienst te creëren MLService wordt vereist geen bestaande trainingsexperimenten te hebben maar u kunt verkiezen om de dienst MLService met een bestaand opgeleid model tot stand te brengen door overeenkomstige Deskundige identiteitskaart en opleidingsuitloopidentiteitskaart te verstrekken.

**API-indeling**

```http
POST /mlServices
```

**Verzoek**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/mlServices \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "{MLINSTANCE_ID}",
        "trainingDataSetId": "{DATASET_ID}",
        "trainingExperimentId": "{TRAINING_ID}",
        "trainingExperimentRunId": "{RUN_ID}",
        "trainingSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        },
        "scoringSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        }
    }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De gewenste naam voor de dienst MLService. De dienst die aan deze dienst MLSerft deze waarde die in de UI van de Galerij van de Dienst als naam van de dienst moet worden getoond. |
| `description` | Een optionele beschrijving voor de MLService. De dienst die aan deze dienst MLSerft deze waarde die in de UI van de Galerij van de Dienst als beschrijving van de dienst moet worden getoond. |
| `mlInstanceId` | Een geldige MLInstance ID. |
| `trainingDataSetId` | Een identiteitskaart van de opleidingsdataset die indien verstrekt de standaard dataset ID van MLInstance zal met voeten treden. Als MLInstance die wordt gebruikt om tot de dienst te leiden MLService geen trainingsdataset bepaalt, moet u een aangewezen identiteitskaart van de opleidingsdataset verstrekken. |
| `trainingExperimentId` | Een experimentele id die u desgewenst kunt opgeven. Als deze waarde niet wordt verstrekt, zal het creëren van de dienst MLService ook tot een nieuwe Experiment leiden gebruikend de standaardconfiguraties van MLInstance. |
| `trainingExperimentRunId` | Een trainingsrun-id die u optioneel kunt opgeven. Als deze waarde niet wordt verstrekt, zal het creëren van MLService ook een trainingslooppas creëren en uitvoeren gebruikend de standaard opleidingsparameters van MLInstance. |
| `trainingSchedule` | Een schema voor geautomatiseerde trainingen. Als dit bezit wordt bepaald, dan zal MLService automatisch trainingslooppas op een geplande basis uitvoeren. |
| `trainingSchedule.startTime` | Een tijdstempel waarvoor de geplande training wordt gestart. |
| `trainingSchedule.endTime` | Een tijdstempel waarvoor de geplande training wordt beëindigd. |
| `trainingSchedule.cron` | Een uitsnijdexpressie die de frequentie van automatische trainingen definieert. |
| `scoringSchedule` | Een schema voor automatische scoring. Als dit bezit wordt bepaald, dan zal MLService automatisch het scoren looppas op een geplande basis uitvoeren. |
| `scoringSchedule.startTime` | Een tijdstempel waarvoor de geplande scoring wordt uitgevoerd. |
| `scoringSchedule.endTime` | Een tijdstempel waarvoor de geplande scoring-runtime wordt beëindigd. |
| `scoringSchedule.cron` | Een uitsnijdexpressie die de frequentie van automatische scoring definieert. |

**Antwoord**

Een geslaagde reactie retourneert een lading die de details bevat van de nieuwe MLService, inclusief de unieke id (`id`), de experimentele id voor training (`trainingExperimentId`), de experimentele id voor scoring (`scoringExperimentId`) en de gegevensset-id voor invoertraining (`trainingDataSetId`).

```json
{
    "id": "{MLSERVICE_ID}",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "trainingExperimentId": "{TRAINING_ID}",
    "trainingDataSetId": "{DATASET_ID}",
    "scoringExperimentId": "{SCORING_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "trainingSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "scoringSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "updated": "2019-01-01T00:00:00.000Z"
}
```

## Een lijst met MLServices ophalen {#retrieve-a-list-of-mlservices}

U kunt een lijst van diensten terugwinnen MLServices door één enkel GET verzoek uit te voeren. Om filterresultaten te helpen, kunt u vraagparameters in de verzoekweg specificeren. Voor een lijst van beschikbare vragen, verwijs naar de bijlage sectie over [vraagparameters voor activaherwinning](./appendix.md#query).

**API-indeling**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parameter | Beschrijving |
| --- | --- |
| `{QUERY_PARAMETER}` | Een van de [beschikbare queryparameters](./appendix.md#query) die wordt gebruikt om resultaten te filteren. |
| `{VALUE}` | De waarde voor de voorafgaande vraagparameter. |

**Verzoek**

Het volgende verzoek bevat een vraag en wint een lijst van diensten terug MLS die zelfde identiteitskaart MLInstance (`{MLINSTANCE_ID}`) delen.

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId=={MLINSTANCE_ID}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert een lijst van diensten MLServices en hun details met inbegrip van hun MLService ID (`{MLSERVICE_ID}`), Experiment ID voor opleiding (`{TRAINING_ID}`), Experiment ID voor het scoren (`{SCORING_ID}`), en input opleidings dataset ID (`{DATASET_ID}`) terug.

```json
{
    "children": [
        {
            "id": "{MLSERVICE_ID}",
            "name": "A service created in UI",
            "mlInstanceId": "{MLINSTANCE_ID}",
            "trainingExperimentId": "{TRAINING_ID}",
            "trainingDataSetId": "{DATASET_ID}",
            "scoringExperimentId": "{SCORING_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "mlInstanceId=={MLINSTANCE_ID},deleted==false",
        "count": 1
    }
}
```

## Een specifieke MLService ophalen {#retrieve-a-specific-mlservice}

U kunt de details van een specifieke Experiment terugwinnen door een GET verzoek uit te voeren dat gewenste identiteitskaart MLService in de verzoekweg omvat.

**API-indeling**

```http
GET /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`: Een geldige MLService-id.

**Verzoek**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlServices/{MLSERVICE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert een lading terug die de details van de gevraagde MLService bevat.

```json
{
    "id": "{MLSERVICE_ID}",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "trainingExperimentId": "{TRAINING_ID}",
    "trainingDataSetId": "{DATASET_ID}",
    "scoringExperimentId": "{SCORING_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z"
}
```

## Een MLService bijwerken {#update-an-mlservice}

U kunt een bestaande dienst bijwerken MLService door zijn eigenschappen door een PUT verzoek te beschrijven die identiteitskaart van doelMLService in de verzoekweg omvat en een nuttige lading te verstrekken JSON die bijgewerkte eigenschappen bevat.

>[!TIP] Om ervoor te zorgen dat dit PUT-verzoek succesvol is, wordt u aangeraden eerst een GET-verzoek uit te voeren om de MLService via ID [op te](#retrieve-a-specific-mlservice)halen. Vervolgens past u het geretourneerde JSON-object aan en werkt u dit bij en past u het gehele gewijzigde JSON-object toe als de payload voor de PUT-aanvraag.

**API-indeling**

```http
PUT /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`: Een geldige MLService-id.

**Verzoek**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlServices/{MLSERVICE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "{MLINSTANCE_ID}",
        "trainingExperimentId": "{TRAINING_ID}",
        "trainingDataSetId": "{DATASET_ID}",
        "scoringExperimentId": "{SCORING_ID}",
        "trainingSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        },
        "scoringSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        }
    }'
```

**Antwoord**

Een succesvolle reactie keert een lading terug die de bijgewerkte details van MLService bevat.

```json
{
    "id": "{MLSERVICE_ID}",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "trainingExperimentId": "{TRAINING_ID}",
    "trainingDataSetId": "{DATASET_ID}",
    "scoringExperimentId": "{SCORING_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "trainingSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "scoringSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "updated": "2019-01-02T00:00:00.000Z"
}
```

## Een MLService verwijderen

U kunt één enkele dienst schrappen MLService door een verzoek uit te voeren DELETE dat identiteitskaart van doelMLService in de verzoekweg omvat.

**API-indeling**

```http
DELETE /mlServices/{MLSERVICE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MLSERVICE_ID}` | Een geldige MLService-id. |

**Verzoek**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices/{MLSERVICE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "MLService deletion was successful"
}
```

## MLServices verwijderen op MLInstance ID

U kunt alle diensten schrappen MLServices die tot een bepaalde MLInstance behoren door een verzoek uit te voeren DELETE dat een identiteitskaart MLInstance als vraagparameter specificeert.

**API-indeling**

```http
DELETE /mlServices?mlInstanceId={MLINSTANCE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MLSERVICE_ID}` | Een geldige MLService-id. |

**Verzoek**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices?mlInstanceId={MLINSTANCE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "MLServices deletion was successful"
}
```
