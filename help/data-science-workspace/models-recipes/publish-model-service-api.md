---
keywords: Experience Platform;publiceer een model;Data Science Workspace;populaire onderwerpen;sensei machine learning api
solution: Experience Platform
title: Publish a Model as a Service Using Sensei Machine Learning API
type: Tutorial
description: Deze zelfstudie behandelt het publiceren van een model als service met de API voor leren van Sensei Machine.
exl-id: f78b1220-0595-492d-9f8b-c3a312f17253
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '1541'
ht-degree: 0%

---

# Publish a model as a service using the [!DNL Sensei Machine Learning API]

>[!NOTE]
>
>Data Science Workspace kan niet meer worden aangeschaft.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

Deze zelfstudie behandelt het proces om een model als dienst te publiceren gebruikend [[!DNL Sensei Machine Learning API] &#x200B;](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/).

## Aan de slag

Deze zelfstudie vereist een goed begrip van Adobe Experience Platform Data Science Workspace. Alvorens met dit leerprogramma te beginnen, te herzien gelieve het [&#x200B; overzicht van Workspace van de Wetenschap van Gegevens &#x200B;](../home.md) voor een inleiding op hoog niveau aan de dienst.

Om samen met dit leerprogramma te volgen, moet u een bestaande Motor van ML, Instantie van XML, en Experiment hebben. Voor stappen op hoe te om deze in API tot stand te brengen, zie het leerprogramma bij [&#x200B; het invoeren van een verpakt recept &#x200B;](./import-packaged-recipe-api.md).

Tot slot alvorens dit leerprogramma te beginnen, te herzien gelieve [&#x200B; begonnen wordt &#x200B;](../api/getting-started.md) sectie van de ontwikkelaarsgids voor belangrijke informatie die u moet kennen om vraag aan [!DNL Sensei Machine Learning] API met succes te maken, met inbegrip van de vereiste kopballen die door dit leerprogramma worden gebruikt:

- `{ACCESS_TOKEN}`
- `{ORG_ID}`
- `{API_KEY}`

Alle POST, PUT, en PATCH verzoeken vereisen een extra kopbal:

- Inhoudstype: application/json

### Belangrijkste voorwaarden

In de volgende tabel wordt een aantal gangbare terminologie beschreven die in deze zelfstudie wordt gebruikt:

| Term | Definitie |
| --- | --- |
| **het Leren van de Machine Instantie (de Instantie van XML)** | Een instantie van een [!DNL Sensei] -engine voor een bepaalde huurder, die specifieke gegevens, parameters en [!DNL Sensei] -code bevat. |
| **Experiment** | Een overkoepelende entiteit voor het houden van de looppas van de trainingsExperiment, het scoren Experimentloops, of allebei. |
| **Gepland Experiment** | Een term die de automatisering van de looppas van het opleidings of het schatten van Experiment beschrijft, die door een user-defined programma wordt geregeld. |
| **Experimentele Looppas** | Een specifiek geval van opleiding of het scoren van Experimenten. Meerdere experimentatieroutes van een bepaalde expert kunnen verschillen in waarden voor gegevenssets die worden gebruikt voor training of scoring. |
| **Geleid Model** | Een model voor machinaal leren dat is gemaakt door het experimenteren en het ontwerpen van functies voordat een gevalideerd, geëvalueerd en voltooid model wordt gevonden. |
| **Gepubliceerd Model** | Een voltooid en versioned model kwam na opleiding, bevestiging, en evaluatie aan. |
| **het Leren van de Machine Dienst (de Dienst van ML)** | Een Instantie van XML die als Dienst wordt opgesteld om op bestelling verzoeken om opleiding en het scoren te steunen gebruikend een API eindpunt. Een dienst van ML kan ook worden tot stand gebracht gebruikend bestaande getrainde Runnen van de Experiment. |

## Creeer de Dienst van ML met een bestaande de looppas van de trainings Experimenteer en geplande scoring

Wanneer u een de looppas van de trainingsExperiment als Dienst van ML publiceert, kunt u het scoren plannen door details voor het scoren in werking te stellen Experiment de lading van een verzoek van de POST. Dit resulteert in de oprichting van een geplande entiteit voor het maken van scores door een expert.

**API formaat**

```http
POST /mlServices
```

**Verzoek**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}'
  -H 'Content-Type: application/json'
  -d '{
        "name": "Service name",
        "description": "Service description",
        "trainingExperimentId": "c4155146-b38f-4a8b-86d8-1de3838c8d87",
        "trainingExperimentRunId": "5c5af39c73fcec153117eed1",
        "scoringDataSetId": "5c5af39c73fcec153117eed1",
        "scoringTimeframe": "20000",
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `mlInstanceId` | De bestaande die Instantie van XML identificatie, de opleidingUitvoer van de Experiment wordt gebruikt om de Dienst van ML tot stand te brengen zou aan dit bepaalde Instantie van XML moeten beantwoorden. |
| `trainingExperimentId` | Identificatie van het experiment overeenkomstig de identificatie van het XML-exemplaar. |
| `trainingExperimentRunId` | Een bepaalde opleiding van de Experimentlooppas die voor het publiceren van de Dienst van ML moet worden gebruikt. |
| `scoringDataSetId` | Identificatie die verwijst naar de specifieke gegevensset die moet worden gebruikt voor geplande scoring-experimentuitvoeren. |
| `scoringTimeframe` | Een geheel getal dat minuten vertegenwoordigt voor het filteren van gegevens die moeten worden gebruikt voor het scoren van experimentele runtime. De waarde `10080` betekent bijvoorbeeld dat gegevens uit de afgelopen 10080 minuten of 168 uur worden gebruikt voor elke geplande score die wordt uitgevoerd door een expert. De waarde `0` filtert geen gegevens, alle gegevens in de gegevensset worden gebruikt voor scoring. |
| `scoringSchedule` | Bevat details betreffende geplande het scoren van de Runnen van de Experiment. |
| `scoringSchedule.startTime` | Datumtijd die aangeeft wanneer de scoring moet worden gestart. |
| `scoringSchedule.endTime` | Datumtijd die aangeeft wanneer de scoring moet worden gestart. |
| `scoringSchedule.cron` | Waarde voor uitsnijden die het interval aangeeft tussen het uitvoeren van het experiment. |

**Reactie**

Een geslaagde reactie retourneert de details van de zojuist gemaakte ML-service, inclusief de unieke `id` en de `scoringExperimentId` voor de bijbehorende studie.


```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingExperimentRunId": "string",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-03-13T00:00",
    "endTime": "2019-03-14T00:00",
    "cron": "30 * * * *"
  },
  "created": "2019-04-08T14:45:25.981Z",
  "updated": "2019-04-08T14:45:25.981Z"
}
```

## Het creëren van een Dienst van XML van een bestaand Instantie van XML

Afhankelijk van uw specifiek gebruiksgeval en vereisten, is het creëren van een Dienst van ML met een Instantie van ML flexibel in termen van het plannen van opleiding en het scoren van de Runs van de Experiment. In deze zelfstudie worden de specifieke gevallen besproken waarin:

- [U hebt geen geplande training nodig, maar u hebt wel een geplande scoring nodig.](#ml-service-with-scheduled-experiment-for-scoring)
- [Voor zowel training als scoring hebt u geplande experimentatieroutes nodig.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

Merk op dat de Dienst van XML kan worden gecreeerd gebruikend een Instantie van XML zonder enige opleiding of het scoren Experimenten te plannen. Met dergelijke ML Services worden gewone Experimententiteiten en één enkele Experimentrun voor training en scoring gemaakt.

### ML Service met gepland experiment voor scoring {#ml-service-with-scheduled-experiment-for-scoring}

U kunt de Dienst van ML tot stand brengen door een Instantie van XML met geplande Runnen van de Experiment voor het scoring te publiceren, die tot een gewone Experimententiteit voor opleiding zal leiden. Er wordt een serie trainingsexperimenten gegenereerd die wordt gebruikt voor alle geplande evaluatiereacties voor scores. Zorg ervoor dat u beschikt over de vereiste `mlInstanceId` , `trainingDataSetId` en `scoringDataSetId` voor het maken van de XML-service en dat deze bestaan en geldige waarden zijn.

**API formaat**

```http
POST /mlServices
```

**Verzoek**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "Service name",
        "description": "Service description",
        "mlInstanceId": "c4155146-b38f-4a8b-86d8-1de3838c8d87",
        "trainingDataSetId": "5c5af39c73fcec153117eed1",
        "trainingTimeframe": "10000",
        "scoringDataSetId": "5c5af39c73fcec153117eed1",
        "scoringTimeframe": "20000",
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| JSON-toets | Beschrijving |
| --- | --- |
| `mlInstanceId` | De bestaande die Instantie van XML identificatie, die de Instantie van XML vertegenwoordigt wordt gebruikt om de Dienst van ML tot stand te brengen. |
| `trainingDataSetId` | Identificatie die verwijst naar de specifieke gegevensverzameling die moet worden gebruikt voor opleidingsexperimenten. |
| `trainingTimeframe` | Een geheel getal dat minuten vertegenwoordigt voor het filteren van gegevens die moeten worden gebruikt voor trainingsexperimenten. De waarde `"10080"` betekent bijvoorbeeld dat gegevens uit de afgelopen 10080 minuten of 168 uur worden gebruikt voor de uitvoering van het trainingsexperiment. De waarde `"0"` filtert geen gegevens, alle gegevens in de gegevensset worden gebruikt voor training. |
| `scoringDataSetId` | Identificatie die verwijst naar de specifieke gegevensset die moet worden gebruikt voor geplande scoring-experimentuitvoeren. |
| `scoringTimeframe` | Een geheel getal dat minuten vertegenwoordigt voor het filteren van gegevens die moeten worden gebruikt voor het scoren van experimentele runtime. De waarde `"10080"` betekent bijvoorbeeld dat gegevens uit de afgelopen 10080 minuten of 168 uur worden gebruikt voor elke geplande score die wordt uitgevoerd door een expert. De waarde `"0"` filtert geen gegevens, alle gegevens in de gegevensset worden gebruikt voor scoring. |
| `scoringSchedule` | Bevat details betreffende geplande het scoren van de Runnen van de Experiment. |
| `scoringSchedule.startTime` | Datumtijd die aangeeft wanneer de scoring moet worden gestart. |
| `scoringSchedule.endTime` | Datumtijd die aangeeft wanneer de scoring moet worden gestart. |
| `scoringSchedule.cron` | Waarde voor uitsnijden die het interval aangeeft tussen het uitvoeren van het experiment. |

**Reactie**

Een succesvolle reactie keert de details van de pas gecreëerde Dienst van ML terug. Hieronder vallen de unieke `id` van de service en de `trainingExperimentId` en `scoringExperimentId` voor de overeenkomende experimenten met training en scoring.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T08:58:10.956Z"
}
```

### ML Service met geplande experimenten voor training en scoring {#ml-service-with-scheduled-experiments-for-training-and-scoring}

Om een bestaande Instantie van XML als Dienst van ML met geplande opleiding en het scoren de Loppen van de Experimenten te publiceren, moet u zowel opleidings als het scoren programma&#39;s verstrekken. Wanneer een Dienst van ML van deze configuratie wordt gecreeerd, worden de geplande entiteiten van de Experiment voor zowel opleiding als het scoren ook gecreeerd. Opleiding- en scoringprogramma&#39;s hoeven niet hetzelfde te zijn. Tijdens het uitvoeren van een scoring wordt het meest recente trainingsmodel dat door de geplande trainingsexperimentatierouts is gemaakt, opgehaald en gebruikt voor de geplande scoring.

**API formaat**

```http
POST /mlServices
```

**Verzoek**

```SHELL
curl -X POST 'https://platform.adobe.io/data/sensei/mlServices' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "string",
        "description": "string",
        "mlInstanceId": "string",
        "trainingDataSetId": "string",
        "trainingTimeframe": "string",
        "scoringDataSetId": "string",
        "scoringTimeframe": "string",
        "trainingSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        },
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| JSON-toets | Beschrijving |
| --- | --- |
| `mlInstanceId` | De bestaande die Instantie van XML identificatie, die de Instantie van XML vertegenwoordigt wordt gebruikt om de Dienst van ML tot stand te brengen. |
| `trainingDataSetId` | Identificatie die verwijst naar de specifieke gegevensverzameling die moet worden gebruikt voor opleidingsexperimenten. |
| `trainingTimeframe` | Een geheel getal dat minuten vertegenwoordigt voor het filteren van gegevens die moeten worden gebruikt voor trainingsexperimenten. De waarde `"10080"` betekent bijvoorbeeld dat gegevens uit de afgelopen 10080 minuten of 168 uur worden gebruikt voor de uitvoering van het trainingsexperiment. De waarde `"0"` filtert geen gegevens, alle gegevens in de gegevensset worden gebruikt voor training. |
| `scoringDataSetId` | Identificatie die verwijst naar de specifieke gegevensset die moet worden gebruikt voor geplande scoring-experimentuitvoeren. |
| `scoringTimeframe` | Een geheel getal dat minuten vertegenwoordigt voor het filteren van gegevens die moeten worden gebruikt voor het scoren van experimentele runtime. De waarde `"10080"` betekent bijvoorbeeld dat gegevens uit de afgelopen 10080 minuten of 168 uur worden gebruikt voor elke geplande score die wordt uitgevoerd door een expert. De waarde `"0"` filtert geen gegevens, alle gegevens in de gegevensset worden gebruikt voor scoring. |
| `trainingSchedule` | Bevat details betreffende de geplande looppas van het trainingsexperiment. |
| `scoringSchedule` | Bevat details betreffende geplande het scoren van de Runnen van de Experiment. |
| `scoringSchedule.startTime` | Datumtijd die aangeeft wanneer de scoring moet worden gestart. |
| `scoringSchedule.endTime` | Datumtijd die aangeeft wanneer de scoring moet worden gestart. |
| `scoringSchedule.cron` | Waarde voor uitsnijden die het interval aangeeft tussen het uitvoeren van het experiment. |

**Reactie**

Een succesvolle reactie keert de details van de pas gecreëerde Dienst van ML terug. Dit omvat de unieke `id` van de service en de `trainingExperimentId` en `scoringExperimentId` van de overeenkomende experimenten met training en scoring. In het onderstaande voorbeeldantwoord geven de aanwezigheid van `trainingSchedule` en `scoringSchedule` de suggestie dat de entiteiten Experiment voor training en scoring geplande experimenten zijn.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",,
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T08:58:10.956Z"
}
```

## Zoek op de Dienst van ML {#retrieving-ml-services}

U kunt een bestaande ML-service opzoeken door een `GET` -aanvraag in te dienen bij `/mlServices` en de unieke `id` van de ML-service in het pad op te geven.

**API formaat**

```http
GET /mlServices/{SERVICE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SERVICE_ID}` | De unieke `id` van de XML-service die u opzoekt. |

**Verzoek**

```SHELL
curl -X GET 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie keert de details van de Dienst van ML terug.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-05-13T23:46:03.478Z",
  "updated": "2019-05-13T23:46:03.478Z"
}
```

>[!NOTE]
>
>Het terugwinnen van de verschillende Diensten van ML kan een reactie met meer of minder sleutel-waarde paren terugkeren. De bovengenoemde reactie is een vertegenwoordiging van de Dienst van a [&#x200B; ML met zowel geplande opleiding als het scoren van de Runnen van de Experiment &#x200B;](#ml-service-with-scheduled-experiments-for-training-and-scoring).


## Training of scores plannen

Als u scoring en training wilt plannen voor een ML Service die al is gepubliceerd, kunt u dit doen door de bestaande ML Service bij te werken met een `PUT` request on `/mlServices` .

**API formaat**

```http
PUT /mlServices/{SERVICE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SERVICE_ID}` | De unieke `id` van de XML-service die u bijwerkt. |

**Verzoek**

In het volgende verzoek worden training en scoring voor een bestaande XML-service gepland door de toetsen `trainingSchedule` en `scoringSchedule` toe te voegen met hun respectievelijke toetsen `startTime` , `endTime` en `cron` .

```SHELL
curl -X PUT 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "string",
        "description": "string",
        "mlInstanceId": "string",
        "trainingExperimentId": "string",
        "trainingDataSetId": "string",
        "trainingTimeframe": "integer",
        "scoringExperimentId": "string",
        "scoringDataSetId": "string",
        "scoringTimeframe": "integer",
        "trainingSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-11T00:00",
          "cron": "20 * * * *"
        },
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-11T00:00",
          "cron": "20 * * * *"
        }
      }'
```

>[!WARNING]
>
>Probeer de `startTime` niet te wijzigen voor bestaande geplande training- en scoring-taken. Als de `startTime` moet worden gewijzigd, kunt u hetzelfde model publiceren en opleidings- en scoretaken opnieuw plannen.

**Reactie**

Een succesvolle reactie keert de details van de bijgewerkte Dienst van ML terug.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-11T00:00",
    "cron": "20 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-11T00:00",
    "cron": "20 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T09:43:55.563Z"
}
```
