---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Modellen
topic: Developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 1%

---


# Modellen

Een model is een geval van een machine het leren recept dat gebruikend historische gegevens en configuraties wordt opgeleid om voor een bedrijfs geval op te lossen.

## Een lijst met modellen ophalen

U kunt een lijst van Modeldetails terugwinnen die tot alle Modellen behoren door één enkel verzoek van de GET aan /models uit te voeren. Standaard wordt in deze lijst de volgorde van het oudste gemaakte model gewijzigd en worden de resultaten beperkt tot 25. U kunt verkiezen om resultaten te filtreren door sommige vraagparameters te specificeren. Voor een lijst van beschikbare vragen, verwijs naar de bijlage sectie over [vraagparameters voor activaherwinning](./appendix.md#query).

**API-indeling**

```http
GET /models
```

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/ \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert een payload die de details van uw modellen bevat, inclusief elke unieke id voor Modellen (`id`).

```json
{
    "children": [
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "A name for this Model",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "27c53796-bd6b-4u59-b51d-7296aa20er23",
            "name": "Model 2",
            "experimentId": "3cb25a2d-2cbd-4d34-a619-8ddae5259a5t",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for Model2",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "Model 3",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for Model3",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
    ],
    "_page": {
        "property": "deleted==false",
        "count": 3
    }
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `id` | De id die overeenkomt met het model. |
| `modelArtifactUri` | Een URI die aangeeft waar het model wordt opgeslagen. De URI eindigt met de `name` waarde voor het model. |
| `experimentId` | Een geldige experimentele id. |
| `experimentRunId` | Een geldige uitvoerings-id voor Experimenten. |

## Een specifiek model ophalen

U kunt een lijst ophalen met Modeldetails die bij een bepaald model horen door één aanvraag voor een GET uit te voeren en een geldige model-id op te geven in het aanvraagpad. Om filterresultaten te helpen, kunt u vraagparameters in de verzoekweg specificeren. Voor een lijst van beschikbare vragen, verwijs naar de bijlage sectie over [vraagparameters voor activaherwinning](./appendix.md#query).

**API-indeling**

```http
GET /models/{MODEL_ID}
GET /models/?property=experimentRunID=={EXPERIMENT_RUN_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MODEL_ID}` | De id van het opgeleide of gepubliceerde model. |
| `{EXPERIMENT_RUN_ID}` | De id van de experimentele uitvoering. |

**Verzoek**

Het volgende verzoek bevat een vraag en wint een lijst van opgeleide Modellen terug die zelfde experimentRunID ({EXPERIMENT_RUN_ID}) delen.

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/?property=experimentRunId==33408593-2871-4198-a812-6d1b7d939cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert een payload die de details van uw model bevat, inclusief de unieke id voor Modellen (`id`).

```json
{
    "children": [
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "A name for this Model",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       }
    ],
    "_page": {
        "property": "experimentRunId==33408593-2871-4198-a812-6d1b7d939cda,deleted==false",
        "count": 1
    }
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `id` | De id die overeenkomt met het model. |
| `modelArtifactUri` | Een URI die aangeeft waar het model wordt opgeslagen. De URI eindigt met de `name` waarde voor het model. |
| `experimentId` | Een geldige experimentele id. |
| `experimentRunId` | Een geldige uitvoerings-id voor Experimenten. |

## Een vooraf gegenereerd model registreren {#register-a-model}

U kunt een vooraf gegenereerd model registreren door een POST aan te vragen bij het `/models` eindpunt. Als u uw model wilt registreren, moeten de waarden van het `modelArtifact` bestand en de `model` eigenschap worden opgenomen in de hoofdtekst van de aanvraag.

**API-indeling**

```http
POST /models
```

**Verzoek**

De volgende POST bevat de benodigde `modelArtifact` bestand- en `model` eigenschapswaarden. Zie de onderstaande tabel voor meer informatie over deze waarden.

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/models \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -F 'modelArtifact=@/Users/yourname/Desktop/model.onnx' \
    -F 'model={
            "name": "Your Model - 0615-1342-45",
            "originType": "offline"
    }'
```

| Parameter | Beschrijving |
| --- | --- |
| `modelArtifact` | De locatie van het volledige modelartefact dat u wilt opnemen. |
| `model` | De formuliergegevens van het Modelobject dat moet worden gemaakt. |

**Antwoord**

Een geslaagde reactie retourneert een payload die de details van uw model bevat, inclusief de unieke id voor Modellen (`id`).

```json
{
  "id": "a28f151a-597a-4a7e-87e9-1c1dbc9c2af7",
  "name": "Your Model - 0615-1342-45",
  "originType": "offline",
  "modelArtifactUri": "http://storageblobml.blob.core.windows.net/prod-models/a28f151a-597a-4a7e-87e9-1c1dbc9c2af7",
  "created": "2020-06-15T20:55:41.520Z",
  "updated": "2020-06-15T20:55:41.520Z",
  "deprecated": false
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `id` | De id die overeenkomt met het model. |
| `modelArtifactUri` | Een URI die aangeeft waar het model wordt opgeslagen. De URI eindigt met de `id` waarde voor het model. |

## Model op id bijwerken

U kunt een bestaand Model bijwerken door zijn eigenschappen door een verzoek van de PUT te beschrijven dat identiteitskaart van het doelModel in de verzoekweg omvat en een nuttige lading te verstrekken JSON die bijgewerkte eigenschappen bevat.

>[!TIP]
>
>Om ervoor te zorgen dat deze PUT-aanvraag succesvol is, wordt u aangeraden eerst een GET-aanvraag uit te voeren om het model op id op te halen. Pas vervolgens het geretourneerde JSON-object aan en werk dit bij en pas het gehele gewijzigde JSON-object toe als de payload voor het verzoek om PUT.

**API-indeling**

```http
PUT /models/{MODEL_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MODEL_ID}` | De id van het opgeleide of gepubliceerde model. |

**Verzoek**

```shell
curl -X PUT \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -d '{
        "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
        "name": "A name for this Model",
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "description": "An updated description for this Model",
        "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "updated": "2019-01-02T00:00:00.000Z"
    }'
```

**Antwoord**

Een geslaagde reactie retourneert een lading die de bijgewerkte gegevens van de expert bevat.

```json
{
        "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
        "name": "A name for this Model",
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "description": "An updated description for this Model",
        "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "updated": "2019-01-02T00:00:00.000Z"
    }
```

## Model op id verwijderen

U kunt één enkel Model schrappen door een DELETE verzoek uit te voeren die identiteitskaart van het doelModel in de verzoekweg omvat.

**API-indeling**

```http
DELETE /models/{MODEL_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MODEL_ID}` | De id van het opgeleide of gepubliceerde model. |

**Verzoek**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert een lading terug die een status 200 bevat die de schrapping van het Model bevestigt.

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Model deletion was successful"
}
```

## Een nieuwe transcodering maken voor een model {#create-transcoded-model}

Transcodering is de directe digitaal-naar-digitale conversie van de ene codering naar de andere. U maakt een nieuwe transcodering voor een model door de nieuwe uitvoer op te geven `{MODEL_ID}` en een `targetFormat` uitvoerbestand op te geven.

**API-indeling**

```http
POST /models/{MODEL_ID}/transcodings
```

| Parameter | Beschrijving |
| --- | --- |
| `{MODEL_ID}` | De id van het opgeleide of gepubliceerde model. |

**Verzoek**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: text/plain' \
    -D '{
 "id": "491a3be5-1d32-4541-94d5-cd1cd07affb5",
 "modelId" : "15c53796-bd6b-4e09-b51d-7296aa20af71",
 "targetFormat": "CoreML",
 "created": "2019-12-16T19:59:08.360Z",
 "createdBy": {
    "userId": "FDD760CD5CD467380A495FE2@AdobeID"
 },
 "updated": "2019-12-19T18:37:43.696Z",
 "deleted": false,
}'
```

**Antwoord**

Een geslaagde reactie retourneert een payload die een JSON-object met de informatie van de transcodering bevat. Dit omvat het unieke herkenningsteken van transcoderingen (`id`) dat in het [terugwinnen van een specifiek getranscodeerd Model](#retrieve-transcoded-model)wordt gebruikt.

```json
{
  "id": "491a3be5-1d32-4541-94d5-cd1cd07affb5",
  "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
  "targetFormat": "CoreML",
  "created": "2020-06-12T22:01:55.886Z",
  "createdBy": {
    "userId": "FDD760CD5CD467380A495FE2@AdobeID"
  },
  "updated": "2020-06-12T22:01:55.886Z",
  "deleted": false
}
```

## Een lijst met transcoderingen ophalen voor een model {#retrieve-transcoded-model-list}

U kunt een lijst van transcoderingen terugwinnen die op een Model zijn uitgevoerd door een verzoek van de GET met uw `{MODEL_ID}`.

**API-indeling**

```http
GET /models/{MODEL_ID}/transcodings
```

| Parameter | Beschrijving |
| --- | --- |
| `{MODEL_ID}` | De id van het opgeleide of gepubliceerde model. |

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert een payload die een JSON-object bevat met een lijst van elke transcodering die op het Model is uitgevoerd. Elk getranscodeerd model ontvangt een unieke id (`id`).

```json
{
    "children": [
        {
            "id": "460aa5a1-e972-455d-b8dc-4bc6cd91edb6",
            "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "created": "2019-12-20T01:07:50.978Z",
            "createdBy": {
                "userId": "FDD760CD5CD467380A495FE2@AdobeID"
            },
            "updated": "2019-12-20T01:07:50.978Z",
            "deprecated": false
        },
        {
            "id": "bdb3e4c2-4702-4045-86b4-17ee40df91cc",
            "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "created": "2019-12-20T17:48:26.473Z",
            "createdBy": {
                "userId": "FDD760CD5CD467380A495FE2@AdobeID"
            },
            "updated": "2019-12-20T17:48:26.473Z",
            "deprecated": false
        }
    ],
    "_page": {
        "property": "modelId==15c53796-bd6b-4e09-b51d-7296aa20af71,deleted==false,deprecated==false",
        "count": 2
    }
}
```

## Een specifiek getranscodeerd model ophalen {#retrieve-transcoded-model}

U kunt een specifiek getranscodeerd Model terugwinnen door een verzoek van de GET met uw `{MODEL_ID}` en identiteitskaart van een getranscodeerd model uit te voeren.

**API-indeling**

```http
GET /models/{MODEL_ID}/transcodings/{TRANSCODING_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MODEL_ID}` | De unieke id van een getraind of gepubliceerd model. |
| `{TRANSCODING_ID}` | De unieke id van een getranscodeerd model. |

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings/460aa5a1-e972-455d-b8dc-4bc6cd91edb6 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert een payload die een JSON-object bevat met de gegevens van het getranscodeerde model.

```json
{
    "id": "460aa5a1-e972-455d-b8dc-4bc6cd91edb6",
    "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
    "created": "2019-12-20T01:07:50.978Z",
    "createdBy": {
        "userId": "FDD760CD5CD467380A495FE2@AdobeID"
    },
    "updated": "2019-12-20T01:07:50.978Z",
    "deprecated": false
}
```


