---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Een model publiceren als service (API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# Een model publiceren als service (API)

## Vereisten

- Volg deze [zelfstudie](../../tutorials/authentication.md) voor toestemming om API-aanroepen te starten.
In de zelfstudie hebt u nu de volgende informatie:
   - `{ACCESS_TOKEN}`: Uw specifieke tokokenwaarde van de drager die na authentificatie wordt verstrekt.
   - `{IMS_ORG}`: Uw IMS org-referenties zijn gevonden in uw unieke integratie van het Adobe Experience Platform.
   - `{API_KEY}`: Uw specifieke API-sleutelwaarde is te vinden in uw unieke integratie van het Adobe Experience Platform.
- Deze zelfstudie vereist bestaande ML Engine, ML Instance, en Experimente entiteiten. Raadpleeg deze [zelfstudie](./import-packaged-recipe-api.md) over het maken van ML Engine, ML Instance of Experiment-entiteiten.
- Voor informatie over API eindpunten en verzoeken vermeld in deze zelfstudie, controleer de volledige [Sensei Machine Learning API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml).

## Belangrijkste voorwaarden

Enkele gangbare terminologie die in deze zelfstudie wordt gebruikt:

| Term | Definitie |
--- | ---
| **Machine Learning Instance (XML-instantie)** | De conceptuele entiteit die een Instantie van een Motor Sensei voor een bepaalde huurder is die uit specifieke gegevens, parameters, en code Sensei bestaat. |
| **Experimenteer** | Een overkoepelende entiteit voor het houden van de looppas van de trainingsExperiment, het scoren Experimentloops, of allebei. |
| **Gepland experiment** | Een term die de automatisering van de looppas van het opleidings of het schatten van Experiment beschrijft, die door een user-defined programma wordt geregeld. |
| **Experimenteer uitvoeren** | Een specifiek geval van opleiding of het scoren van Experimenten. Meerdere experimentatieroutes van een bepaalde expert kunnen verschillen in waarden voor gegevenssets die worden gebruikt voor training of scoring. |
| **Gevolgd model** | Een model voor machinaal leren dat is gemaakt door het experimenteren en het ontwerpen van functies voordat een gevalideerd, geëvalueerd en voltooid model wordt gevonden. |
| **Gepubliceerd model** | Een voltooid en versioned model kwam na opleiding, bevestiging, en evaluatie aan. |
| **Machine Learning Service (ML Service)** | Een Instantie van XML die als Dienst wordt opgesteld om op bestelling verzoek om opleiding en het scoren via een eindpunt te steunen. Merk op dat een Dienst van ML ook kan worden gecreeerd gebruikend bestaande getrainde proeflooppas. |


## API-workflow

Dit leerprogramma zal over het creëren van, het terugwinnen van, en het bijwerken van de Dienst van ML gaan.

## Het creëren van een Dienst van ML met een bestaande de looppas van de trainingsExperimenteer en geplande scoring

Wanneer u een trainingsproefrun publiceert als een XML-service, kunt u scoring plannen door details op te geven voor de scoring Experiment Run in `scoringSchedule` uw {JSON_PAYLOAD} . Dit resulteert in de oprichting van een geplande entiteit voor het maken van scores door een expert. Zorg ervoor dat u over de waarden `mlInstanceId`, `trainingExperimentId`, `trainingExperimentRunId`, `scoringDataSetId`en dat deze bestaan en geldige waarden zijn.

Voer een `POST` `/mlServices`aanvraag in om te beginnen. Hieronder ziet u een voorbeeldopdracht voor krullen:

**Verzoek**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -d '{JSON_PAYLOAD}'
```

- `{API_KEY}` : Uw specifieke API-sleutelwaarde is te vinden in uw unieke integratie van het Adobe Experience Platform.
- `{IMS_ORG}` :  De IMS-organisatie-id vindt u onder de integratiegegevens in de Adobe I/O-console.
- `{ACCESS_TOKEN}` : Uw specifieke tokokenwaarde van de drager die na authentificatie wordt verstrekt.
- `{JSON_PAYLOAD}` : Een voorbeeld van de JSON-payload-indeling vindt u hieronder:

```JSON
{
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingExperimentRunId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-03-13T00:00",
    "endTime": "2019-03-14T00:00",
    "cron": "30 * * * *"
  }
}
```

- `mlInstanceId` : De bestaande Instantie van XML identificatie, de opleiding de Looppas van de Experiment die wordt gebruikt om de Dienst van ML tot stand te brengen zou aan dit bepaalde Instantie van XML moeten beantwoorden.
- `trainingExperimentId` : Identificatie van het experiment overeenkomstig de identificatie van het XML-exemplaar.
- `trainingExperimentRunId` : Een bepaalde opleiding van de Experimentlooppas die voor het publiceren van de Dienst van ML moet worden gebruikt.
- `scoringDataSetId` : Identificatie die verwijst naar de specifieke gegevensset die moet worden gebruikt voor geplande scoring-experimentuitvoeren.
- `scoringTimeframe` : Een geheel getal dat minuten vertegenwoordigt voor het filteren van gegevens die moeten worden gebruikt voor het scoren van experimentele runtime. Voor elke geplande proefrun met scoring wordt bijvoorbeeld een waarde gebruikt van `"10080"` gemiddeldengegevens uit de afgelopen 10080 minuten of 168 uur. Merk op dat een waarde van `"0"` niet gegevens zal filtreren, alle gegevens binnen de dataset voor het scoren wordt gebruikt.
- `scoringSchedule` : Bevat details betreffende geplande het scoren van de Runnen van de Experiment.
- `startTime` : definitie.
- `endTime` : definitie.
- `cron` : definitie.

**Antwoord**

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

Uit het JSON-antwoord blijkt dat de sleutel `scoringExperimentId` met de corresponderende waarde ervan aangeeft dat er een nieuw studieprogramma is gemaakt, samen met het studieprogramma dat u in het `POST` verzoek hebt opgegeven. De `id` sleutel in de reactie identificeert uniek de Dienst van ML die werd gecreeerd.

## Het creëren van de Dienst van XML van een bestaand Instantie van XML

Afhankelijk van uw specifiek gebruiksgeval en vereisten, is het creëren van een Dienst van ML met een Instantie van ML flexibel in termen van het plannen van opleiding en het scoren van de Runs van de Experiment. In deze zelfstudie worden de specifieke gevallen besproken waarin:

- [U hebt geen geplande training nodig, maar u hebt wel een geplande scoring nodig.](#ml-service-with-scheduled-experiment-for-scoring)
- [Voor zowel training als scoring hebt u geplande experimentatieroutes nodig.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

Merk op dat de Dienst van XML kan worden gecreeerd gebruikend een Instantie van XML zonder enige opleiding of het scoren Experimenten te plannen. Met deze ML Service worden gewone Experimententiteiten en één enkele Experimentrun voor training en scoring gemaakt.

### ML Service met gepland experiment voor scoring

Het creëren van een Dienst van ML door een Instantie van XML met geplande Runnen van de Experimenten voor het scoren te publiceren zal in de verwezenlijking van een gewone Experimententiteit voor opleiding resulteren. De resulterende serie trainingsexperimenten die wordt gegenereerd, worden gebruikt voor alle geplande evaluatiemodellen. Zorg ervoor dat u de `mlInstanceId`, `trainingDataSetId`en `scoringDataSetId` vereiste waarden hebt voor het maken van de XML-service en dat deze bestaan en geldige waarden zijn.

Voer een `POST` `/mlServices`aanvraag in om te beginnen. Hieronder ziet u een voorbeeldopdracht voor krullen:

**Verzoek**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -d '{JSON_PAYLOAD}'
```

- `{API_KEY}` : Uw specifieke API-sleutelwaarde is te vinden in uw unieke integratie van het Adobe Experience Platform.
- `{IMS_ORG}` :  De IMS-organisatie-id vindt u onder de integratiegegevens in de Adobe I/O-console.
- `{ACCESS_TOKEN}` : Uw specifieke tokokenwaarde van de drager die na authentificatie wordt verstrekt.
- `{JSON_PAYLOAD}` : Een voorbeeld van de JSON-payload-indeling vindt u hieronder:

```JSON
{
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
}
```

| JSON-toets | Beschrijving |
| --- | --- |
| **`mlInstanceId`** | De bestaande die Instantie van XML identificatie, die de Instantie van XML vertegenwoordigt wordt gebruikt om de Dienst van ML tot stand te brengen. |
| **`trainingDataSetId`** | Identificatie die verwijst naar de specifieke gegevensverzameling die moet worden gebruikt voor opleidingsexperimenten. |
| **`trainingTimeframe`** | Een geheel getal dat minuten vertegenwoordigt voor het filteren van gegevens die moeten worden gebruikt voor trainingsexperimenten. Zo wordt een waarde van de `"10080"` gemiddelden in de afgelopen 10080 minuten of 168 uur gebruikt voor de uitvoering van het trainingsexperiment. Merk op dat een waarde van `"0"` zal geen gegevens filtreren, alle gegevens binnen de dataset voor opleiding wordt gebruikt. |
| **`scoringDataSetId`** | Identificatie die verwijst naar de specifieke gegevensset die moet worden gebruikt voor geplande scoring-experimentuitvoeren. |
| **`scoringTimeframe`** | Een geheel getal dat minuten vertegenwoordigt voor het filteren van gegevens die moeten worden gebruikt voor het scoren van experimentele runtime. Voor elke geplande proefrun met scoring wordt bijvoorbeeld een waarde gebruikt van `"10080"` gemiddeldengegevens uit de afgelopen 10080 minuten of 168 uur. Merk op dat een waarde van `"0"` niet gegevens zal filtreren, alle gegevens binnen de dataset voor het scoren wordt gebruikt. |
| **`scoringSchedule`** | Bevat details betreffende geplande het scoren van de Runnen van de Experiment. |

**Antwoord**

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

Uit het `JSON` antwoord, de sleutels `trainingExperimentId` en `scoringExperimentId` suggereert dat een nieuwe opleiding en het scoren van Deskundige entiteit voor deze Dienst van ML werd gecreeerd. De aanwezigheid van het `scoringSchedule` object verwijst naar details over het schema Experiment uitvoeren van scoring. De `id` sleutel in de reactie verwijst naar de Dienst van ML u enkel hebt gecreeerd.

### ML Service met geplande experimenten voor training en scoring

Om een bestaande Instantie van XML als Dienst van ML met geplande opleiding en het scoren de Loppen van de Experimenten te publiceren, moet u zowel opleidings als het scoren programma&#39;s verstrekken. Wanneer een Dienst van ML van deze configuratie wordt gecreeerd, worden de geplande entiteiten van de Experiment voor zowel opleiding als het scoren ook gecreeerd. Opleiding- en scoringprogramma&#39;s hoeven niet hetzelfde te zijn. Tijdens het uitvoeren van een scoring wordt het meest recente trainingsmodel dat door de geplande trainingsexperimentatierouts is gemaakt, opgehaald en gebruikt voor de geplande scoring.

Om de Dienst van ML tot stand te brengen, doe een `POST` verzoek aan `/mlServices` met het `{JSON_PAYLOAD}` vertegenwoordigen van het voorwerp van de Dienst van ML dat moet worden toegevoegd. Zorg ervoor dat de waarden `mlInstanceId`, `trainingDataSetId`en `scoringDataSetId` bestaan en geldig zijn.

**Verzoek**

```SHELL
curl -X POST "https://platform-int.adobe.io/data/sensei/mlServices" 
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
  -d "{JSON_PAYLOAD}"
```

- `{API_KEY}` : Uw specifieke API-sleutelwaarde is te vinden in uw unieke integratie van het Adobe Experience Platform.
- `{IMS_ORG}` :  De IMS-organisatie-id vindt u onder de integratiegegevens in de Adobe I/O-console.
- `{ACCESS_TOKEN}` : Uw specifieke tokokenwaarde van de drager die na authentificatie wordt verstrekt.
- `{JSON_PAYLOAD}` : Een voorbeeld van de JSON-payload-indeling vindt u hieronder:

```JSON
{
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
}
```

| JSON-toets | Beschrijving |
| --- | --- |
| **`mlInstanceId`** | De bestaande die Instantie van XML identificatie, die de Instantie van XML vertegenwoordigt wordt gebruikt om de Dienst van ML tot stand te brengen. |
| **`trainingDataSetId`** | Identificatie die verwijst naar de specifieke gegevensverzameling die moet worden gebruikt voor opleidingsexperimenten. |
| **`trainingTimeframe`** | Een geheel getal dat minuten vertegenwoordigt voor het filteren van gegevens die moeten worden gebruikt voor trainingsexperimenten. Zo wordt een waarde van de `"10080"` gemiddelden in de afgelopen 10080 minuten of 168 uur gebruikt voor de uitvoering van het trainingsexperiment. Merk op dat een waarde van `"0"` zal geen gegevens filtreren, alle gegevens binnen de dataset voor opleiding wordt gebruikt. |
| **`scoringDataSetId`** | Identificatie die verwijst naar de specifieke gegevensset die moet worden gebruikt voor geplande scoring-experimentuitvoeren. |
| **`scoringTimeframe`** | Een geheel getal dat minuten vertegenwoordigt voor het filteren van gegevens die moeten worden gebruikt voor het scoren van experimentele runtime. Voor elke geplande proefrun met scoring wordt bijvoorbeeld een waarde gebruikt van `"10080"` gemiddeldengegevens uit de afgelopen 10080 minuten of 168 uur. Merk op dat een waarde van `"0"` niet gegevens zal filtreren, alle gegevens binnen de dataset voor het scoren wordt gebruikt. |
| **`trainingSchedule`** | Bevat details betreffende de geplande looppas van het trainingsexperiment. |
| **`scoringSchedule`** | Bevat details betreffende geplande het scoren van de Runnen van de Experiment. |

**Antwoord**

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

De toevoeging van `trainingExperimentId` en `scoringExperimentId` in het responsorgaan suggereert de oprichting van experimentele entiteiten voor zowel opleiding als scoring. De aanwezigheid van `trainingSchedule` en `scoringSchedule` suggereert dat de hierboven genoemde experimentele entiteiten voor opleiding en scoring geplande experimenten zijn. De `id` sleutel in de reactie verwijst naar de Dienst van ML u enkel hebt gecreeerd.

## HTML-services ophalen

Om de bestaande Dienst van ML terug te winnen is zo eenvoudig zoals het doen van een `GET` verzoek aan `/mlServices` eindpunt. Zorg ervoor dat u de identificatie van de Dienst van ML voor de specifieke Dienst van ML hebt u probeert terug te winnen.

**Verzoek**

```SHELL
curl -X GET "https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}" 
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
```

- `{API_KEY}` : Uw specifieke API-sleutelwaarde is te vinden in uw unieke integratie van het Adobe Experience Platform.
- `{IMS_ORG}` :  De IMS-organisatie-id vindt u onder de integratiegegevens in de Adobe I/O-console.
- `{ACCESS_TOKEN}` : Uw specifieke tokokenwaarde van de drager die na authentificatie wordt verstrekt.

**Antwoord**

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

De reactie JSON vertegenwoordigt het voorwerp van de Dienst van ML. Dit voorwerp is gelijkwaardig aan de reactie voor wanneer de Dienst van ML wordt gecreeerd. Merk op dat het terugwinnen van verschillende Diensten van ML een reactie met meer of minder sleutel-waarde paren kan terugkeren. De bovenstaande reactie is een vertegenwoordiging van een Dienst van [ML met zowel geplande opleiding als het scoren van de Runnen van de Experiment](#ml-service-with-scheduled-experiments-for-training-and-scoring).


## Training of scores plannen

Veronderstel u scoring en opleiding op een Dienst van XML wilt plannen die reeds is gepubliceerd, kunt u dit doen door de bestaande Dienst van ML met een `PUT` verzoek op bij te werken `/mlServices`. Zorg ervoor dat u de servicdentificatie van ML hebt die u wilt bijwerken. Voor uw verwijzing, zou het [terugwinnen van de Dienst](#retrieving-ml-services) van XML u wilt bijwerken een nuttige eerste stap kunnen zijn.

**Verzoek**

```SHELL
curl -X PUT "https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}" 
  -H "Authorization: {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
  -d "{JSON_PAYLOAD}"
```

- `{SERVICE_ID}` : Unieke identificatie die verwijst naar de ML-service die u wilt bijwerken.
- `{API_KEY}` : Uw specifieke API-sleutelwaarde is te vinden in uw unieke integratie van het Adobe Experience Platform.
- `{IMS_ORG}` :  De IMS-organisatie-id vindt u onder de integratiegegevens in de Adobe I/O-console.
- `{ACCESS_TOKEN}` : Uw specifieke tokokenwaarde van de drager die na authentificatie wordt verstrekt.
- `{JSON_PAYLOAD}` : Een voorbeeld van de JSON-payload-indeling vindt u hieronder:

```JSON
{
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
}
```

U kunt training en scoring plannen door de `trainingSchedule` toets en de `scoringSchedule` toets met hun respectievelijke `startTime`, `endTime`en `cron` toetsen in te voegen.

>[!NOTE] dat de `PUT` verzoeken op `mlServices` u toestaan om de Diensten met bestaande geplande proeflooppas te wijzigen. Probeer **niet** de bestaande `startTime` geplande training- en scores-taken te wijzigen. Als u het model `startTime` moet wijzigen, kunt u hetzelfde model publiceren en opleidings- en scoretaken opnieuw plannen.

**Antwoord**

De reactie is de `{JSON_PAYLOAD}` maar met extra `id`, `created`en `updated` toetsen in het object.

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
