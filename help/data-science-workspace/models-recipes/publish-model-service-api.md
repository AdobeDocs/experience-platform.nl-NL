---
keywords: Experience Platform;een model publiceren;Data Science Workspace;populaire onderwerpen;sensei machine learning api
solution: Experience Platform
title: Een model publiceren als een service met de API voor leren van Sensei-machines
topic: tutorial
type: Tutorial
description: Deze zelfstudie behandelt het publiceren van een model als service met behulp van de API voor leren van Sensei-machines.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 0%

---


# Een model publiceren als een service met [!DNL Sensei Machine Learning API]

Deze zelfstudie behandelt het proces waarbij een model als service wordt gepubliceerd met de [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml).

## Aan de slag

Deze zelfstudie vereist een goed begrip van de Adobe Experience Platform Data Science Workspace. Voordat u met deze zelfstudie begint, bekijkt u het [Overzicht van de Data Science Workspace](../home.md) voor een introductie op hoog niveau van de service.

Om samen met dit leerprogramma te volgen, moet u een bestaande Motor van ML, Instantie van XML, en Experiment hebben. Raadpleeg de zelfstudie over het importeren van een verpakt recept](./import-packaged-recipe-api.md) voor meer informatie over het maken van deze recept in de API.[

Tot slot alvorens deze zelfstudie te beginnen, te herzien [aan de slag ](../api/getting-started.md) sectie van de ontwikkelaarsgids voor belangrijke informatie die u moet kennen om met succes vraag aan [!DNL Sensei Machine Learning] API te maken, met inbegrip van de vereiste kopballen die door dit leerprogramma worden gebruikt:

- `{ACCESS_TOKEN}`
- `{IMS_ORG}`
- `{API_KEY}`

Alle POST, PUT, en PATCH verzoeken vereisen een extra kopbal:

- Inhoudstype: application/json

### Belangrijkste voorwaarden

In de volgende tabel wordt een aantal gangbare terminologie beschreven die in deze zelfstudie wordt gebruikt:

| Term | Definitie |
--- | ---
| **Machine Learning Instance (XML-instantie)** | Een instantie van een [!DNL Sensei] Motor voor een bepaalde huurder, die specifieke gegevens, parameters, en [!DNL Sensei] code bevat. |
| **Experimenteer** | Een overkoepelende entiteit voor het houden van de looppas van de trainingsExperiment, het scoren Experimentloops, of allebei. |
| **Gepland experiment** | Een term die de automatisering van de looppas van het opleidings of het schatten van Experiment beschrijft, die door een user-defined programma wordt geregeld. |
| **Experimenteer uitvoeren** | Een specifiek geval van opleiding of het scoren van Experimenten. Meerdere experimentatieroutes van een bepaalde expert kunnen verschillen in waarden voor gegevenssets die worden gebruikt voor training of scoring. |
| **Gevolgd model** | Een model voor machinaal leren dat is gemaakt door het experimenteren en het ontwerpen van functies voordat een gevalideerd, geëvalueerd en voltooid model wordt gevonden. |
| **Gepubliceerd model** | Een voltooid en versioned model kwam na opleiding, bevestiging, en evaluatie aan. |
| **Machine Learning Service (ML Service)** | Een Instantie van XML die als Dienst wordt opgesteld om op bestelling verzoeken om opleiding en het scoren te steunen gebruikend een API eindpunt. Een dienst van ML kan ook worden tot stand gebracht gebruikend bestaande opgeleide Runnen van de Experiment. |

## Creeer de Dienst van ML met een bestaande de looppas van de trainings Experimenteer en geplande scoring

Wanneer u een de looppas van de trainingsExperiment als Dienst van ML publiceert, kunt u het scoren plannen door details voor het scoren in werking te stellen Experiment de lading van een verzoek van de POST. Dit resulteert in de oprichting van een geplande entiteit voor het maken van scores door een expert.

**API-indeling**

```http
POST /mlServices
```

**Verzoek**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}'
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
--- | ---
| `mlInstanceId` | De bestaande die Instantie van XML identificatie, de opleidingUitvoer van de Experiment wordt gebruikt om de Dienst van ML tot stand te brengen zou aan dit bepaalde Instantie van XML moeten beantwoorden. |
| `trainingExperimentId` | Identificatie van het experiment overeenkomstig de identificatie van het XML-exemplaar. |
| `trainingExperimentRunId` | Een bepaalde opleiding van de Experimentlooppas die voor het publiceren van de Dienst van ML moet worden gebruikt. |
| `scoringDataSetId` | Identificatie die verwijst naar de specifieke gegevensset die moet worden gebruikt voor geplande scoring-experimentuitvoeren. |
| `scoringTimeframe` | Een geheel getal dat minuten vertegenwoordigt voor het filteren van gegevens die moeten worden gebruikt voor het scoren van experimentele runtime. Een waarde van `10080` betekent bijvoorbeeld dat gegevens uit de afgelopen 10080 minuten of 168 uur worden gebruikt voor elke geplande proefrun met scoring. Een waarde van `0` zal geen gegevens filteren, alle gegevens binnen de dataset wordt gebruikt voor het scoren. |
| `scoringSchedule` | Bevat details betreffende geplande het scoren van de Runnen van de Experiment. |
| `scoringSchedule.startTime` | Datumtijd die aangeeft wanneer de scoring moet worden gestart. |
| `scoringSchedule.endTime` | Datumtijd die aangeeft wanneer de scoring moet worden gestart. |
| `scoringSchedule.cron` | Waarde voor uitsnijden die het interval aangeeft tussen het uitvoeren van het experiment. |

**Antwoord**

Een geslaagde reactie retourneert de details van de zojuist gemaakte ML-service, inclusief de unieke `id` en `scoringExperimentId` voor de bijbehorende studie.


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

U kunt de Dienst van ML tot stand brengen door een Instantie van XML met geplande Runnen van de Experiment voor het scoring te publiceren, die tot een gewone Experimententiteit voor opleiding zal leiden. Er wordt een serie trainingsexperimenten gegenereerd die wordt gebruikt voor alle geplande evaluatiereacties voor scores. Zorg ervoor dat de `mlInstanceId`, `trainingDataSetId` en `scoringDataSetId` vereist zijn voor het maken van de ML-service en dat deze bestaan en geldige waarden zijn.

**API-indeling**

```http
POST /mlServices
```

**Verzoek**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
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
| `scoringTimeframe` | Een geheel getal dat minuten vertegenwoordigt voor het filteren van gegevens die moeten worden gebruikt voor het scoren van experimentele runtime. Een waarde van `"10080"` betekent bijvoorbeeld dat gegevens uit de afgelopen 10080 minuten of 168 uur worden gebruikt voor elke geplande proefrun met scoring. Een waarde van `"0"` zal geen gegevens filteren, alle gegevens binnen de dataset wordt gebruikt voor het scoren. |
| `scoringSchedule` | Bevat details betreffende geplande het scoren van de Runnen van de Experiment. |
| `scoringSchedule.startTime` | Datumtijd die aangeeft wanneer de scoring moet worden gestart. |
| `scoringSchedule.endTime` | Datumtijd die aangeeft wanneer de scoring moet worden gestart. |
| `scoringSchedule.cron` | Waarde voor uitsnijden die het interval aangeeft tussen het uitvoeren van het experiment. |

**Antwoord**

Een succesvolle reactie keert de details van de pas gecreëerde Dienst van ML terug. Dit omvat de unieke `id` van de service, evenals de `trainingExperimentId` en `scoringExperimentId` voor de bijbehorende experimenten met training en scoring.

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

### ML Service met geplande experimenten voor training en scores {#ml-service-with-scheduled-experiments-for-training-and-scoring}

Om een bestaande Instantie van XML als Dienst van ML met geplande opleiding en het scoren de Loppen van de Experimenten te publiceren, moet u zowel opleidings als het scoren programma&#39;s verstrekken. Wanneer een Dienst van ML van deze configuratie wordt gecreeerd, worden de geplande entiteiten van de Experiment voor zowel opleiding als het scoren ook gecreeerd. Opleiding- en scoringprogramma&#39;s hoeven niet hetzelfde te zijn. Tijdens het uitvoeren van een scoring wordt het meest recente trainingsmodel dat door de geplande trainingsexperimentatierouts is gemaakt, opgehaald en gebruikt voor de geplande scoring.

**API-indeling**

```http
POST /mlServices
```

**Verzoek**

```SHELL
curl -X POST 'https://platform-int.adobe.io/data/sensei/mlServices' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
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
| `scoringTimeframe` | Een geheel getal dat minuten vertegenwoordigt voor het filteren van gegevens die moeten worden gebruikt voor het scoren van experimentele runtime. Een waarde van `"10080"` betekent bijvoorbeeld dat gegevens uit de afgelopen 10080 minuten of 168 uur worden gebruikt voor elke geplande proefrun met scoring. Een waarde van `"0"` zal geen gegevens filteren, alle gegevens binnen de dataset wordt gebruikt voor het scoren. |
| `trainingSchedule` | Bevat details betreffende de geplande looppas van het trainingsexperiment. |
| `scoringSchedule` | Bevat details betreffende geplande het scoren van de Runnen van de Experiment. |
| `scoringSchedule.startTime` | Datumtijd die aangeeft wanneer de scoring moet worden gestart. |
| `scoringSchedule.endTime` | Datumtijd die aangeeft wanneer de scoring moet worden gestart. |
| `scoringSchedule.cron` | Waarde voor uitsnijden die het interval aangeeft tussen het uitvoeren van het experiment. |

**Antwoord**

Een succesvolle reactie keert de details van de pas gecreëerde Dienst van ML terug. Hieronder vallen de unieke `id` van de service, evenals de `trainingExperimentId` en `scoringExperimentId` van de bijbehorende training- en scoring-experimenten. In het onderstaande voorbeeldantwoord suggereert de aanwezigheid van `trainingSchedule` en `scoringSchedule` dat de Experimententiteiten voor training en scoring geplande experimenten zijn.

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

## Zoek de Dienst {#retrieving-ml-services} van ML

U kunt een bestaande Dienst van ML opzoeken door `GET` verzoek aan `/mlServices` te doen en unieke `id` van de Dienst van ML in de weg te verstrekken.

**API-indeling**

```http
GET /mlServices/{SERVICE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SERVICE_ID}` | De unieke `id` van de ML-service die u opzoekt. |

**Verzoek**

```SHELL
curl -X GET 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

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
>Het terugwinnen van de verschillende Diensten van ML kan een reactie met meer of minder sleutel-waarde paren terugkeren. Het bovenstaande antwoord is een voorstelling van een [ML-service met zowel geplande training als het scoren van Experimentloops](#ml-service-with-scheduled-experiments-for-training-and-scoring).


## Training of scores plannen

Als u scoring en training wilt plannen voor een ML-service die al is gepubliceerd, kunt u dit doen door de bestaande ML-service bij te werken met een `PUT`-verzoek op `/mlServices`.

**API-indeling**

```http
PUT /mlServices/{SERVICE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SERVICE_ID}` | De unieke `id` van de XML-service die u bijwerkt. |

**Verzoek**

De volgende aanvraag plant training en scoring voor een bestaande ML-service door de toetsen `trainingSchedule` en `scoringSchedule` met hun respectievelijke toetsen `startTime`, `endTime` en `cron` toe te voegen.

```SHELL
curl -X PUT 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
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
>Probeer niet de `startTime` te wijzigen voor bestaande geplande training en scoring-taken. Als de `startTime` moet worden gewijzigd, kunt u overwegen hetzelfde model te publiceren en opleidings- en scoring-taken opnieuw te plannen.

**Antwoord**

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
