---
keywords: Experience Platform;een model publiceren;Data Science Workspace;populaire onderwerpen;sensei machine learning api
solution: Experience Platform
title: Een model publiceren als een service met de API voor leren door Sensei Machine
topic-legacy: tutorial
type: Tutorial
description: In deze zelfstudie wordt beschreven hoe u een model publiceert als service met de API voor leren van Sensei Machine.
exl-id: f78b1220-0595-492d-9f8b-c3a312f17253
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 0%

---

# Een model publiceren als een service met de [!DNL Sensei Machine Learning API]

Deze zelfstudie behandelt het proces voor het publiceren van een model als service met behulp van de [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml).

## Aan de slag

Deze zelfstudie vereist een goed begrip van de Adobe Experience Platform Data Science Workspace. Lees voordat u met deze zelfstudie begint de [Overzicht van de Data Science Workspace](../home.md) voor een introductie op hoog niveau van de dienst.

Om samen met dit leerprogramma te volgen, moet u een bestaande Motor van ML, Instantie van XML, en Experiment hebben. Raadpleeg de zelfstudie voor meer informatie over het maken van deze bestanden in de API [een verpakt recept importeren](./import-packaged-recipe-api.md).

Voordat u met deze zelfstudie begint, moet u eerst de [aan de slag](../api/getting-started.md) van de ontwikkelaarsgids voor belangrijke informatie die u moet kennen om met succes vraag aan te maken [!DNL Sensei Machine Learning] API, inclusief de vereiste kopteksten die in deze zelfstudie worden gebruikt:

- `{ACCESS_TOKEN}`
- `{ORG_ID}`
- `{API_KEY}`

Alle POST, PUT, en PATCH verzoeken vereisen een extra kopbal:

- Inhoudstype: application/json

### Belangrijkste voorwaarden

In de volgende tabel wordt een aantal gangbare terminologie beschreven die in deze zelfstudie wordt gebruikt:

| Term | Definitie |
| --- | --- |
| **Machine Learning Instance (XML-instantie)** | Een instantie van een [!DNL Sensei] Motor voor een bepaalde huurder, die specifieke gegevens, parameters bevat, en [!DNL Sensei] code. |
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
| `mlInstanceId` | De bestaande Instantie van XML identificatie, de opleiding de Looppas van de Experiment die wordt gebruikt om de Dienst van ML tot stand te brengen zou aan dit bepaalde Instantie van XML moeten beantwoorden. |
| `trainingExperimentId` | Identificatie van het experiment overeenkomstig de identificatie van het XML-exemplaar. |
| `trainingExperimentRunId` | Een bepaalde opleiding van de Experimentlooppas die voor het publiceren van de Dienst van ML moet worden gebruikt. |
| `scoringDataSetId` | Identificatie die verwijst naar de specifieke gegevensset die moet worden gebruikt voor geplande scoring-experimentuitvoeren. |
| `scoringTimeframe` | Een geheel getal dat minuten vertegenwoordigt voor het filteren van gegevens die moeten worden gebruikt voor het scoren van experimentele runtime. Bijvoorbeeld een waarde van `10080` betekent dat gegevens uit de afgelopen 10080 minuten of 168 uur worden gebruikt voor elke geplande scoring Experimentrun. De waarde van `0` zullen geen gegevens filtreren, worden alle gegevens binnen de dataset gebruikt voor het scoren. |
| `scoringSchedule` | Bevat details betreffende geplande het scoren van de Runnen van de Experiment. |
| `scoringSchedule.startTime` | Datumtijd die aangeeft wanneer de scoring moet worden gestart. |
| `scoringSchedule.endTime` | Datumtijd die aangeeft wanneer de scoring moet worden gestart. |
| `scoringSchedule.cron` | Waarde voor uitsnijden die het interval aangeeft tussen het uitvoeren van het experiment. |

**Antwoord**

Een succesvolle reactie keert de details van de pas gecreëerde Dienst van ML, met inbegrip van zijn unieke terug `id` en de `scoringExperimentId` voor de bijbehorende studie.


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

U kunt de Dienst van ML tot stand brengen door een Instantie van XML met geplande Runnen van de Experiment voor het scoring te publiceren, die tot een gewone Experimententiteit voor opleiding zal leiden. Er wordt een serie trainingsexperimenten gegenereerd die wordt gebruikt voor alle geplande evaluatiereacties voor scores. Zorg ervoor dat u beschikt over de `mlInstanceId`, `trainingDataSetId`, en `scoringDataSetId` vereist voor de verwezenlijking van de Dienst van ML, en dat zij bestaan en geldige waarden zijn.

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
| `trainingTimeframe` | Een geheel getal dat minuten vertegenwoordigt voor het filteren van gegevens die moeten worden gebruikt voor trainingsexperimenten. Bijvoorbeeld een waarde van `"10080"` betekent dat gegevens uit de afgelopen 10080 minuten of 168 uur zullen worden gebruikt voor de opleiding die wordt uitgevoerd door een expert. De waarde van `"0"` geen gegevens filteren, worden alle gegevens in de gegevensset gebruikt voor training. |
| `scoringDataSetId` | Identificatie die verwijst naar de specifieke gegevensset die moet worden gebruikt voor geplande scoring-experimentuitvoeren. |
| `scoringTimeframe` | Een geheel getal dat minuten vertegenwoordigt voor het filteren van gegevens die moeten worden gebruikt voor het scoren van experimentele runtime. Bijvoorbeeld een waarde van `"10080"` betekent dat gegevens uit de afgelopen 10080 minuten of 168 uur worden gebruikt voor elke geplande scoring Experimentrun. De waarde van `"0"` zullen geen gegevens filtreren, worden alle gegevens binnen de dataset gebruikt voor het scoren. |
| `scoringSchedule` | Bevat details betreffende geplande het scoren van de Runnen van de Experiment. |
| `scoringSchedule.startTime` | Datumtijd die aangeeft wanneer de scoring moet worden gestart. |
| `scoringSchedule.endTime` | Datumtijd die aangeeft wanneer de scoring moet worden gestart. |
| `scoringSchedule.cron` | Waarde voor uitsnijden die het interval aangeeft tussen het uitvoeren van het experiment. |

**Antwoord**

Een succesvolle reactie keert de details van de pas gecreëerde Dienst van ML terug. Dit omvat het unieke van de dienst `id`en de `trainingExperimentId` en `scoringExperimentId` voor de overeenkomstige experimenten met opleiding en scoring.

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

**API-indeling**

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
| `trainingTimeframe` | Een geheel getal dat minuten vertegenwoordigt voor het filteren van gegevens die moeten worden gebruikt voor trainingsexperimenten. Bijvoorbeeld een waarde van `"10080"` betekent dat gegevens uit de afgelopen 10080 minuten of 168 uur zullen worden gebruikt voor de opleiding die wordt uitgevoerd door een expert. De waarde van `"0"` geen gegevens filteren, worden alle gegevens in de gegevensset gebruikt voor training. |
| `scoringDataSetId` | Identificatie die verwijst naar de specifieke gegevensset die moet worden gebruikt voor geplande scoring-experimentuitvoeren. |
| `scoringTimeframe` | Een geheel getal dat minuten vertegenwoordigt voor het filteren van gegevens die moeten worden gebruikt voor het scoren van experimentele runtime. Bijvoorbeeld een waarde van `"10080"` betekent dat gegevens uit de afgelopen 10080 minuten of 168 uur worden gebruikt voor elke geplande scoring Experimentrun. De waarde van `"0"` zullen geen gegevens filtreren, worden alle gegevens binnen de dataset gebruikt voor het scoren. |
| `trainingSchedule` | Bevat details betreffende de geplande looppas van het trainingsexperiment. |
| `scoringSchedule` | Bevat details betreffende geplande het scoren van de Runnen van de Experiment. |
| `scoringSchedule.startTime` | Datumtijd die aangeeft wanneer de scoring moet worden gestart. |
| `scoringSchedule.endTime` | Datumtijd die aangeeft wanneer de scoring moet worden gestart. |
| `scoringSchedule.cron` | Waarde voor uitsnijden die het interval aangeeft tussen het uitvoeren van het experiment. |

**Antwoord**

Een succesvolle reactie keert de details van de pas gecreëerde Dienst van ML terug. Dit omvat het unieke van de dienst `id`en de `trainingExperimentId` en `scoringExperimentId` van de overeenkomstige opleiding- en studieprogramma-experimenten. In het onderstaande voorbeeldantwoord wordt de aanwezigheid van `trainingSchedule` en `scoringSchedule` stelt voor dat de experimenten voor opleiding en scoring gepland zijn als experimenten.

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

U kunt omhoog een bestaande Dienst van ML kijken door een `GET` verzoek om `/mlServices` en de unieke `id` van de dienst van ML in de weg.

**API-indeling**

```http
GET /mlServices/{SERVICE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SERVICE_ID}` | De unieke `id` van de dienst van ML u omhoog kijkt. |

**Verzoek**

```SHELL
curl -X GET 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
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
>Het terugwinnen van de verschillende Diensten van ML kan een reactie met meer of minder sleutel-waarde paren terugkeren. Het bovenstaande antwoord is een weergave van een [ML-service met zowel geplande trainings- als scoring-experimentbanen](#ml-service-with-scheduled-experiments-for-training-and-scoring).


## Training of scores plannen

Als u scoring en training wilt plannen voor een ML-service die al is gepubliceerd, kunt u dit doen door de bestaande ML-service bij te werken met een `PUT` verzoek op `/mlServices`.

**API-indeling**

```http
PUT /mlServices/{SERVICE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SERVICE_ID}` | De unieke `id` van de dienst van ML u bijwerkt. |

**Verzoek**

De volgende verzoekprogramma&#39;s opleiding en het scoren voor een bestaande Dienst van ML door toe te voegen `trainingSchedule` en `scoringSchedule` toetsen met hun respectievelijke `startTime`, `endTime`, en `cron` toetsen.

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
>Probeer niet de opdracht `startTime` over bestaande geplande opleidings- en scoretaken. Als de `startTime` moet worden gewijzigd, kunt u overwegen hetzelfde model te publiceren en opleidings- en scoretaken opnieuw te plannen.

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
