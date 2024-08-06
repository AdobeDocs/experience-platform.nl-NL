---
keywords: Experience Platform;ontwikkelaarshandleiding;eindpunt;Data Science Workspace;populaire onderwerpen;mlservices;sensei machine learning-API
solution: Experience Platform
title: XMLServices-API-eindpunt
description: Een MLService is een gepubliceerd opgeleid model dat uw organisatie de mogelijkheid biedt om toegang te krijgen tot en gebruik te maken van eerder ontwikkelde modellen. Een belangrijk kenmerk van MLServices is de mogelijkheid om training en scores op een geplande basis te automatiseren. Gepland trainingsprogramma's kunnen de efficiëntie en nauwkeurigheid van een model helpen behouden, terwijl geplande scores ervoor kunnen zorgen dat er consistent nieuwe inzichten worden gegenereerd.
role: Developer
exl-id: cd236e0b-3bfc-4d37-83eb-432f6ad5c5b6
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---

# MLServices-eindpunt

>[!NOTE]
>
>Data Science Workspace kan niet meer worden aangeschaft.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

Een dienst MLService is een gepubliceerd opgeleid model dat uw organisatie van de capaciteit voorziet om tot eerder ontwikkelde modellen toegang te hebben en te hergebruiken. Een belangrijk kenmerk van MLServices is de mogelijkheid om training en scoring op een geplande basis te automatiseren. De geplande trainingslooppas kan helpen de efficiency en nauwkeurigheid van een model handhaven, terwijl de geplande scoring looppas kan ervoor zorgen dat de nieuwe inzichten constant worden geproduceerd.

De geautomatiseerde opleiding en het schrapen programma&#39;s worden bepaald met beginnende timestamp, het beëindigen timestamp, en een frequentie die als a [ wordt vertegenwoordigd cron uitdrukking ](https://en.wikipedia.org/wiki/Cron). De programma&#39;s kunnen worden bepaald wanneer [ creërend een MLService ](#create-an-mlservice) of toegepast door [ het bijwerken van een bestaande MLService ](#update-an-mlservice).

## Een MLService maken {#create-an-mlservice}

U kunt een dienst tot stand brengen MLService door een verzoek van de POST en een lading uit te voeren die een naam voor de dienst en een geldige identiteitskaart MLInstance verstrekt. De instantie die wordt gebruikt om een MLService te maken, hoeft geen bestaande trainingsexperimenten te hebben, maar u kunt ervoor kiezen om de MLService te maken met een bestaand getraind model door de bijbehorende id van de Experiment en de trainingsrun-id op te geven.

**API Formaat**

```http
POST /mlServices
```

**Verzoek**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/mlServices \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | De gewenste naam voor de MLService. De dienst die aan deze dienst MLSerft deze waarde om in UI van de Galerij van de Dienst als naam van de dienst te worden getoond. |
| `description` | Een optionele beschrijving voor de MLService. De service die overeenkomt met deze MLService, neemt deze waarde over die in de gebruikersinterface van de servicegalerie moet worden weergegeven als de beschrijving van de service. |
| `mlInstanceId` | Een geldige MLInstance ID. |
| `trainingDataSetId` | Een identiteitskaart van de opleidingsdataset die indien verstrekt de standaard dataset ID van MLInstance zal met voeten treden. Als MLInstance die wordt gebruikt om tot de dienst te leiden MLService geen trainingsdataset bepaalt, moet u een aangewezen identiteitskaart van de opleidingsdataset verstrekken. |
| `trainingExperimentId` | Een experimentele id die u desgewenst kunt opgeven. Als deze waarde niet wordt opgegeven, maakt het maken van de MLService ook een nieuwe Experiment met de standaardconfiguraties van de MLInstance. |
| `trainingExperimentRunId` | Een trainingsrun-id die u optioneel kunt opgeven. Als deze waarde niet wordt verstrekt, zal het creëren van MLService ook een trainingslooppas creëren en uitvoeren gebruikend de standaard trainingsparameters van MLInstance. |
| `trainingSchedule` | Een schema voor geautomatiseerde trainingen. Als dit bezit wordt bepaald, dan zal MLService automatisch trainingslooppas op een geplande basis uitvoeren. |
| `trainingSchedule.startTime` | Een tijdstempel waarvoor de geplande training wordt gestart. |
| `trainingSchedule.endTime` | Een tijdstempel waarvoor de geplande training wordt beëindigd. |
| `trainingSchedule.cron` | Een uitsnede die de frequentie van automatische trainingen bepaalt. |
| `scoringSchedule` | Een schema voor automatische scoring. Als dit bezit wordt bepaald, dan zal MLService automatisch het scoren looppas op een geplande basis uitvoeren. |
| `scoringSchedule.startTime` | Een tijdstempel waarvoor geplande scores worden uitgevoerd. |
| `scoringSchedule.endTime` | Een tijdstempel waarvan de geplande scores eindigen. |
| `scoringSchedule.cron` | Een uitsnijdexpressie die de frequentie van automatische scoring definieert. |

**Reactie**

Een succesvolle reactie keert een lading terug die de details van de pas gecreëerde dienst MLService met inbegrip van zijn uniek herkenningsteken (`id`), Experiment identiteitskaart voor opleiding (`trainingExperimentId`), Experiment identiteitskaart voor het scoring (`scoringExperimentId`), en identiteitskaart van de inputopleiding (`trainingDataSetId`) bevat.

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

## Een lijst met MLServices ophalen {#retrieve-a-list-of-mlservices}

U kunt een lijst van diensten terugwinnen MLServices door één enkel verzoek van de GET uit te voeren. Om filterresultaten te helpen, kunt u vraagparameters in de verzoekweg specificeren. Voor een lijst van beschikbare vragen, verwijs naar de appendix sectie op [ vraagparameters voor activaherwinning ](./appendix.md#query).

**API Formaat**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parameter | Beschrijving |
| --- | --- |
| `{QUERY_PARAMETER}` | Één van de [ beschikbare vraagparameters ](./appendix.md#query) die aan filterresultaten wordt gebruikt. |
| `{VALUE}` | De waarde voor de voorafgaande queryparameter. |

**Verzoek**

Het volgende verzoek bevat een vraag en wint een lijst van MLServices terug die zelfde ID MLInstance (`{MLINSTANCE_ID}`) delen.

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie keert een lijst van diensten MLServices en hun details met inbegrip van hun identiteitskaart MLService (`{MLSERVICE_ID}`), Experiment identiteitskaart voor opleiding (`{TRAINING_ID}`), Experiment ID voor het scoring (`{SCORING_ID}`), en input opleidings dataset identiteitskaart (`{DATASET_ID}`) terug.

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

## Een specifieke MLService ophalen {#retrieve-a-specific-mlservice}

U kunt de details van een specifieke Experiment terugwinnen door een verzoek van de GET uit te voeren dat gewenste identiteitskaart MLService in de verzoekweg omvat.

**API Formaat**

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie retourneert een lading die de details van de aangevraagde MLService bevat.

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

## Een MLService bijwerken {#update-an-mlservice}

U kunt een bestaande MLService bijwerken door zijn eigenschappen door een verzoek van de PUT te beschrijven dat identiteitskaart van doelMLService in de verzoekweg omvat en een lading JSON verstrekt die bijgewerkte eigenschappen bevat.

>[!TIP]
>
>om het succes van dit verzoek van de PUT te verzekeren, wordt gesuggereerd dat eerst u een GET verzoek uitvoert om [ MLService door identiteitskaart ](#retrieve-a-specific-mlservice) terug te winnen. Vervolgens past u het geretourneerde JSON-object aan en werkt u het bij en past u het gehele gewijzigde JSON-object toe als de payload voor het verzoek om PUT.

**API Formaat**

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

**Reactie**

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

**API Formaat**

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "MLService deletion was successful"
}
```

## MLServices verwijderen op basis van MLInstance ID

U kunt alle diensten schrappen MLServices die tot een bepaalde instantie behoren door een verzoek van de DELETE uit te voeren die een identiteitskaart MLInstance als vraagparameter specificeert.

**API Formaat**

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "MLServices deletion was successful"
}
```
