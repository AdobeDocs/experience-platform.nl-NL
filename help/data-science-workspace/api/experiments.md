---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Experimenten
topic: Developer guide
translation-type: tm+mt
source-git-commit: 01cfbc86516a05df36714b8c91666983f7a1b0e8

---


# Experimenten

Modelontwikkeling en -training vinden plaats op het niveau van de experimenten, waarbij een experiment bestaat uit een MLInstance, trainingsrun en scoring run.

## Een experiment maken

U kunt een Experiment tot stand brengen door een POST- verzoek uit te voeren terwijl het verstrekken van een naam en een geldige identiteitskaart MLInstance in de verzoeklading.

>[!NOTE] In tegenstelling tot modeltraining in de UI, leidt het creëren van een Experiment door een expliciete API vraag niet automatisch tot en voert een trainingslooppas uit.

**API-indeling**

```http
POST /experiments
```

**Verzoek**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/experiments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
    -d '{
        "name": "a name for this Experiment",
        "mlInstanceId": "{MLINSTANCE_ID}"
    }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De gewenste naam voor het experiment. De trainingsrun die overeenkomt met dit experiment, neemt deze waarde over die in de gebruikersinterface moet worden weergegeven als de naam van de trainingsrun. |
| `mlInstanceId` | Een geldige MLInstance ID. |

**Antwoord**

Een geslaagde reactie retourneert een payload die de details bevat van het nieuwe experiment, inclusief de unieke id (`id`).

```json
{
    "id": "{EXPERIMENT_ID}",
    "name": "A name for this Experiment",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## Een training of scores maken en uitvoeren

U kunt trainings- of scoring-runtime maken door een POST-aanvraag uit te voeren en een geldige experimenteerid op te geven en de uitvoertaak op te geven. Er kunnen alleen scores worden gemaakt als het Experimentprogramma een bestaande en geslaagde training heeft. Met succes zal het creëren van een trainingslooppas de model opleidingsprocedure initialiseren en zijn succesvolle voltooiing zal een getraind model produceren. Het genereren van getrainde modellen vervangt alle eerder bestaande modellen, zodat een expert op elk moment slechts één getraind model kan gebruiken.

**API-indeling**

```http
POST /experiments/{EXPERIMENT_ID}/runs
```

| Parameter | Beschrijving |
| --- | --- |
| `{EXPERIMENT_ID}` | Een geldige experimentele id. |

**Verzoek**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
    -d '{
        "mode": "{TASK}"
    }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `{TASK}` | Geeft de taak van de uitvoering aan. Plaats deze waarde als of `train` voor opleiding, `score` voor het scoren, of `fp` voor eigenschappijpleiding. |

**Antwoord**

Een succesvolle reactie keert een lading terug die de details van de pas gecreëerde looppas met inbegrip van de geërfte standaardopleiding of het scoren parameters, en unieke identiteitskaart van de looppas (`{RUN_ID}`) bevat.

```json
{
    "id": "{RUN_ID}",
    "mode": "{TASK}",
    "experimentId": "{EXPERIMENT_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdBySchedule": false,
    "tasks": [
        {
            "name": "{TASK}",
            "parameters": [
                {
                    "key": "parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## Een lijst met experimenten ophalen

U kunt een lijst van Experimenten terugwinnen die tot een bepaalde instantie behoren door één enkel GET verzoek uit te voeren en geldige identiteitskaart MLInstance als vraagparameter te verstrekken. Voor een lijst van beschikbare vragen, verwijs naar de bijlage sectie over [vraagparameters voor activaherwinning](./appendix.md#query).


**API-indeling**

```http
GET /experiments
GET /experiments?property=mlInstanceId=={MLINSTANCE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{MLINSTANCE_ID}` | Geef een geldige MLInstance-id op om een lijst met experimenten op te halen die bij die specifieke MLInstance horen. |

**Verzoek**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments?property=mlInstanceId=={MLINSTANCE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert een lijst van Experimenten terug die zelfde MLInstance ID (`{MLINSTANCE_ID}`) delen.

```json
{
    "children": [
        {
            "id": "{EXPERIMENT_ID}",
            "name": "A name for this Experiment",
            "mlInstanceId": "{MLINSTANCE_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "{EXPERIMENT_ID}",
            "name": "Training Run 1",
            "mlInstanceId": "{MLINSTANCE_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "{EXPERIMENT_ID}",
            "name": "Training Run 2",
            "mlInstanceId": "{MLINSTANCE_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        }
    ],
    "_page": {
        "property": "deleted==false",
        "count": 3
    }
}
```

## Een specifiek experiment ophalen {#retrieve-specific}

U kunt de details van een specifieke Experiment terugwinnen door een GET verzoek uit te voeren dat gewenste identiteitskaart van de Experiment in de verzoekweg omvat.

**API-indeling**

```http
GET /experiments/{EXPERIMENT_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{EXPERIMENT_ID}` | Een geldige experimentele id. |

**Verzoek**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```


**Antwoord**

Een geslaagde reactie retourneert een payload die de details van het gewenste experiment bevat.

```json
{
    "id": "{EXPERIMENT_ID}",
    "name": "A name for this Experiment",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## Een lijst met experimentele tests ophalen

U kunt een lijst van opleiding of het scoren looppas terugwinnen die tot een bepaalde Experiment behoren door één enkele GET verzoek uit te voeren en een geldige Experimentidentiteitskaart te verstrekken. Om filterresultaten te helpen, kunt u vraagparameters in de verzoekweg specificeren. Voor een volledige lijst van beschikbare vraagparameters, zie de bijlage sectie over [vraagparameters voor activaherwinning](./appendix.md#query).

>[!NOTE] Wanneer het combineren van veelvoudige vraagparameters, moeten zij door ampersands (&amp;) worden gescheiden.

**API-indeling**

```http
GET /experiments/{EXPERIMENT_ID}/runs
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER}={VALUE}
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parameter | Beschrijving |
| --- | --- |
| `{EXPERIMENT_ID}` | Een geldige experimentele id. |
| `{QUERY_PARAMETER}` | Een van de [beschikbare queryparameters](./appendix.md#query) die wordt gebruikt om resultaten te filteren. |
| `{VALUE}` | De waarde voor de voorafgaande vraagparameter. |

**Verzoek**

Het volgende verzoek bevat een vraag en wint een lijst van trainingslooppas terug die tot één of andere Experiment behoren.

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs?property=mode==train \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert een payload die een lijst met uitvoeringen en alle details, inclusief de id van de experimentele uitvoering (`{RUN_ID}`), bevat.

```json
{
    "children": [
        {
            "id": "{RUN_ID}",
            "mode": "train",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "createdBySchedule": false
        }
    ],
    "_page": {
        "property": "mode==train,experimentId=={EXPERIMENT_ID},deleted==false",
        "totalCount": 1,
        "count": 1
    }
}
```

## Een experiment bijwerken

U kunt een bestaande Experiment bijwerken door de eigenschappen ervan te overschrijven via een PUT-aanvraag die de id van de doelexpert in het aanvraagpad bevat en een JSON-payload met bijgewerkte eigenschappen opgeeft.

>[!TIP] Om ervoor te zorgen dat deze PUT-aanvraag succesvol is, wordt u aangeraden eerst een GET-aanvraag uit te voeren om de Experiment op id [op te](#retrieve-specific)halen. Vervolgens past u het geretourneerde JSON-object aan en werkt u dit bij en past u het gehele gewijzigde JSON-object toe als de payload voor de PUT-aanvraag.

De volgende voorbeeld-API-aanroep werkt de naam van een expert bij terwijl deze in eerste instantie deze eigenschappen heeft:

```json
{
    "name": "A name for this Experiment",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "createdByService": false
}
```

**API-indeling**

```http
PUT /experiments/{EXPERIMENT_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{EXPERIMENT_ID}` | Een geldige experimentele id. |

**Verzoek**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiments.v1.json' \
    -d '{
        "name": "An upated name",
        "mlInstanceId": "{MLINSTANCE_ID}",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "createdByService": false
    }'
```

**Antwoord**

Een geslaagde reactie retourneert een lading die de bijgewerkte gegevens van de expert bevat.

```json
{
    "id": "{EXPERIMENT_ID}",
    "name": "An updated name",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "createdByService": false
}
```

## Een experiment verwijderen

U kunt één Experiment verwijderen door een DELETE-aanvraag uit te voeren die de id van de doelexpert in het aanvraagpad bevat.

**API-indeling**

```http
DELETE /experiments/{EXPERIMENT_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{EXPERIMENT_ID}` | Een geldige experimentele id. |

**Verzoek**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID} \
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
    "detail": "Experiment successfully deleted"
}
```

## Experimenten door MLInstance ID verwijderen

U kunt alle Experimenten schrappen die tot een bepaalde instantie behoren door een verzoek uit te voeren DELETE dat identiteitskaart MLInstance als vraagparameter omvat.

**API-indeling**

```http
DELETE /experiments?mlInstanceId={MLINSTANCE_ID}
```

| Parameter | Beschrijving |
| --- | ---|
| `{MLINSTANCE_ID}` | Een geldige MLInstance ID. |

**Verzoek**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments?mlInstanceId={MLINSTANCE_ID} \
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
    "detail": "Experiments successfully deleted"
}
```
