---
keywords: Experience Platform;ontwikkelaarshandleiding;eindpunt;Data Science Workspace;populaire onderwerpen;mlservices;sensei machine learning api
solution: Experience Platform
title: XMLServices API-eindpunt
topic: Developer guide
description: Een dienst MLService is een gepubliceerd opgeleid model dat uw organisatie van de capaciteit voorziet om tot eerder ontwikkelde modellen toegang te hebben en te hergebruiken. Een belangrijk kenmerk van MLServices is de mogelijkheid om training en scoring op een geplande basis te automatiseren. De geplande trainingslooppas kan helpen de efficiency en nauwkeurigheid van een model handhaven, terwijl de geplande scoring looppas kan ervoor zorgen dat de nieuwe inzichten constant worden geproduceerd.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 0%

---


# MLServices-eindpunt

Een dienst MLService is een gepubliceerd opgeleid model dat uw organisatie van de capaciteit voorziet om tot eerder ontwikkelde modellen toegang te hebben en te hergebruiken. Een belangrijk kenmerk van MLServices is de mogelijkheid om training en scoring op een geplande basis te automatiseren. De geplande trainingslooppas kan helpen de efficiency en nauwkeurigheid van een model handhaven, terwijl de geplande scoring looppas kan ervoor zorgen dat de nieuwe inzichten constant worden geproduceerd.

Geautomatiseerde trainings- en scoreschema&#39;s worden gedefinieerd met een begintijdstempel, een eindtijdstempel en een frequentie die wordt weergegeven als een [uitsnijdexpressie](https://en.wikipedia.org/wiki/Cron). Planningen kunnen worden gedefinieerd wanneer [een MLService](#create-an-mlservice) wordt gemaakt of door [een bestaande MLService](#update-an-mlservice) wordt bijgewerkt.

## Een MLService {#create-an-mlservice} maken

U kunt een dienst tot stand brengen MLService door een verzoek van de POST en een lading uit te voeren die een naam voor de dienst en een geldige identiteitskaart MLInstance verstrekt. De MLInstance die wordt gebruikt om een dienst te creëren MLService wordt vereist geen bestaande trainingsexperimenten te hebben maar u kunt verkiezen om de dienst MLService met een bestaand opgeleid model tot stand te brengen door overeenkomstige Deskundige identiteitskaart en opleidingsuitloopidentiteitskaart te verstrekken.

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
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "trainingDataSetId": "5ee3cd7f2d34011913c56941",
        "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
        "trainingExperimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
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

Een succesvolle reactie keert een lading terug die de details van de pas gecreëerde dienst MLService met inbegrip van zijn uniek herkenningsteken (`id`), Experiment ID voor opleiding (`trainingExperimentId`), Experiment ID voor het scoring (`scoringExperimentId`), en input opleidings dataset ID (`trainingDataSetId`) bevat.

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
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

## Een lijst met MLServices {#retrieve-a-list-of-mlservices} ophalen

U kunt een lijst van diensten terugwinnen MLServices door één enkel verzoek van de GET uit te voeren. Om filterresultaten te helpen, kunt u vraagparameters in de verzoekweg specificeren. Voor een lijst van beschikbare vragen, verwijs naar de bijlage sectie over [vraagparameters voor activa herwinning](./appendix.md#query).

**API-indeling**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parameter | Beschrijving |
| --- | --- |
| `{QUERY_PARAMETER}` | Één van [beschikbare vraagparameters](./appendix.md#query) die aan filterresultaten wordt gebruikt. |
| `{VALUE}` | De waarde voor de voorafgaande vraagparameter. |

**Verzoek**

Het volgende verzoek bevat een vraag en wint een lijst van diensten terug MLS die zelfde identiteitskaart MLInstance (`{MLINSTANCE_ID}`) delen.

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert een lijst van diensten MLServices en hun details met inbegrip van hun MLService ID (`{MLSERVICE_ID}`), Experiment ID voor opleiding (`{TRAINING_ID}`), Experiment ID voor het scoring (`{SCORING_ID}`), en input opleiding dataset ID (`{DATASET_ID}`) terug.

```json
{
    "children": [
        {
            "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
            "name": "A service created in UI",
            "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
            "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
            "trainingDataSetId": "5ee3cd7f2d34011913c56941",
            "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda,deleted==false",
        "count": 1
    }
}
```

## Een specifieke MLService {#retrieve-a-specific-mlservice} ophalen

U kunt de details van een specifiek Experiment terugwinnen door een verzoek van de GET uit te voeren dat gewenste identiteitskaart MLService in de verzoekweg omvat.

**API-indeling**

```http
GET /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`: Een geldige MLService-id.

**Verzoek**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert een lading terug die de details van de gevraagde MLService bevat.

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z"
}
```

## Een MLService {#update-an-mlservice} bijwerken

U kunt een bestaande dienst bijwerken MLService door zijn eigenschappen door een verzoek van de PUT te beschrijven dat identiteitskaart van doelMLService in de verzoekweg omvat en een nuttige lading te verstrekken JSON die bijgewerkte eigenschappen bevat.

>[!TIP]
>
>Om het succes van dit verzoek van de PUT te verzekeren, wordt gesuggereerd dat eerst u een verzoek van de GET aan [wint de dienst MLS door ID](#retrieve-a-specific-mlservice) terug. Pas vervolgens het geretourneerde JSON-object aan en werk dit bij en pas het gehele gewijzigde JSON-object toe als de payload voor het verzoek om PUT.

**API-indeling**

```http
PUT /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`: Een geldige MLService-id.

**Verzoek**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
        "trainingDataSetId": "5ee3cd7f2d34011913c56941",
        "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
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
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
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

U kunt één enkele dienst schrappen MLService door een verzoek van de DELETE uit te voeren dat identiteitskaart van doelMLService in de verzoekweg omvat.

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
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
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

U kunt alle diensten schrappen MLServices die tot een bepaalde instantie behoren door een verzoek van de DELETE uit te voeren die een identiteitskaart MLInstance als vraagparameter specificeert.

**API-indeling**

```http
DELETE /mlServices?mlInstanceId={MLINSTANCE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MLINSTANCE_ID}` | Een geldige MLInstance ID. |

**Verzoek**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices?mlInstanceId=46986c8f-7739-4376-8509-0178bdf32cda \
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
