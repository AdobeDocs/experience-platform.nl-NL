---
keywords: Experience Platform;home;populaire onderwerpen;flowservice;
title: Creeer een Looppas van de Stroom voor On-Demand Ingestie die de Dienst API van de Stroom gebruikt
description: Leer hoe te om een stroom tot stand te brengen die voor opname op bestelling gebruikend de Dienst API van de Stroom wordt uitgevoerd
exl-id: a7b20cd1-bb52-4b0a-aad0-796929555e4a
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 0%

---

# Een stroom maken die wordt uitgevoerd voor opname op aanvraag met de API [!DNL Flow Service]

De looppas van de stroom vertegenwoordigt een geval van stroomuitvoering. Bijvoorbeeld, als een stroom wordt gepland om te lopen bij 9 :00 AM, 10 :00 AM, en 11 :00 AM, dan zou u drie instanties van een stroomlooppas hebben. De looppas van de stroom is specifiek voor uw bepaalde organisatie.

Op bestelling kunt u een stroom maken die tegen een gegeven gegevensstroom wordt uitgevoerd. Dit staat uw gebruikers toe om een stroomlooppas tot stand te brengen, die op bepaalde parameters wordt gebaseerd en een opnamecyclus, zonder de diensttekenen tot stand te brengen. Ondersteuning voor inname op aanvraag is alleen beschikbaar voor batchbronnen.

Dit leerprogramma behandelt de stappen op hoe te om op bestelling ingestie te gebruiken en een stroom tot stand te brengen die [[!DNL Flow Service]  API &#x200B;](https://www.adobe.io/experience-platform-apis/references/flow-service/) gebruikt.

>[!TIP]
>
>Als u een flowuitvoering opnieuw uitvoert, worden alleen bestanden met tijdstempels verwerkt die binnen het bereik van de oorspronkelijke uitvoering vallen.

## Aan de slag

>[!NOTE]
>
>Als u een flowuitvoering wilt maken, moet u eerst over de flow-id van een gegevensstroom beschikken die voor eenmalige invoer is gepland.

Voor deze zelfstudie hebt u een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [&#x200B; Bronnen &#x200B;](../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [&#x200B; Sandboxen &#x200B;](../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [&#x200B; begonnen wordt met Experience Platform APIs &#x200B;](../../../landing/api-guide.md).

## Een doorloop maken die wordt uitgevoerd voor een op tabellen gebaseerde bron

Als u een stroom voor een op een tabel gebaseerde bron wilt maken, dient u een POST-aanvraag in bij de [!DNL Flow Service] API en geeft u de id op van de flow waarop u de run wilt maken, evenals waarden voor begintijd, eindtijd en delta-kolom.

>[!TIP]
>
>De op lijst-gebaseerde bronnen omvatten de volgende broncategorieën: reclame, analyses, toestemming en voorkeur, CRMs, klantensucces, gegevensbestand, marketing automatisering, betalingen, en protocollen.

**API formaat**

```http
POST /runs/
```

**Verzoek**

Met de volgende aanvraag wordt een flowuitvoering voor de flow-id `3abea21c-7e36-4be1-bec1-d3bad0e3e0de` gemaakt.

>[!NOTE]
>
>U hoeft de `deltaColumn` alleen op te geven wanneer u de eerste flowuitvoering maakt. Hierna wordt `deltaColumn` als onderdeel van `copy` -transformatie in de flow gerepareerd en wordt het als de bron van de waarheid beschouwd. Als u probeert de waarde `deltaColumn` te wijzigen via de parameters van de flowuitvoering, treedt er een fout op.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
      "params": {
          "startTime": "1663735590",
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567",
          "deltaColumn": {
              "name": "DOB"
          }
      }
  }'
```

| Parameter | Beschrijving |
| --- | --- |
| `flowId` | De id van de flow waarop de flow wordt uitgevoerd. |
| `params.startTime` | De geplande tijd van wanneer de de stroomlooppas op bestelling zal beginnen. Deze waarde wordt uitgedrukt in unieke tijd. |
| `params.windowStartTime` | De vroegste datum en tijd waarop de gegevens worden opgehaald. Deze waarde wordt uitgedrukt in unieke tijd. |
| `params.windowEndTime` | De datum en tijd waarop de gegevens worden opgehaald tot. Deze waarde wordt uitgedrukt in unieke tijd. |
| `params.deltaColumn` | De deltakolom wordt vereist om de gegevens te verdelen en nieuw opgenomen gegevens van historische gegevens te scheiden. **Nota**: `deltaColumn` is slechts nodig wanneer het creëren van uw eerste stroomlooppas. |
| `params.deltaColumn.name` | De naam van de deltakolom. |

**Reactie**

Een geslaagde reactie retourneert de details van de nieuw gemaakte flow, inclusief de unieke run `id` .

```json
{
    "items": [
        {
            "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
            "etag": "\"1100c53e-0000-0200-0000-627138980000\""
        }
    ]
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `id` | De id van de nieuwe flow-run. Zie de gids bij [&#x200B; het terugwinnen van stroomspecificaties &#x200B;](../api/collect/database-nosql.md#specs) voor meer informatie over op lijst-gebaseerde looppas specificaties. |
| `etag` | De middelversie van de stroomlooppas. |

<!-- 
| `createdAt` | The unix timestamp that designates when the flow run was created. |
| `updatedAt` | The unix timestamp that designates when the flow run was last updated. |
| `createdBy` | The organization ID of the user who created the flow run. |
| `updatedBy` | The organization ID of the user who last updated the flow run. |
| `createdClient` | The application client that created the flow run. |
| `updatedClient` | The application client that last updated the flow run. |
| `sandboxId` | The ID of the sandbox that contains the flow run. |
| `sandboxName` | The name of the sandbox that contains the flow run. |
| `imsOrgId` | The organization ID. |
| `flowId` | The ID of the flow in which the flow run is created against. |
| `params.windowStartTime` | An integer that defines the start time of the window during which data is to be pulled. The value is represented in unix time. |
| `params.windowEndTime` | An integer that defines the end time of the window during which data is to be pulled. The value is represented in unix time. |
| `params.deltaColumn` | The delta column is required to partition the data and separate newly ingested data from historic data. **Note**: The `deltaColumn` is only needed when creating your firs flow run. |
| `params.deltaColumn.name` | The name of the delta column. |
| `etag` | The resource version of the flow run. |
| `metrics` | This property displays a status summary for the flow run. | -->

## Een doorloop maken voor een op een bestand gebaseerde bron

Als u een stroom voor een op een bestand gebaseerde bron wilt maken, dient u een POST-aanvraag in bij de [!DNL Flow Service] API en geeft u de id op van de flow waarop u de runtime en waarden voor de begintijd en eindtijd wilt maken.

>[!TIP]
>
>Bestandsbronnen omvatten alle bronnen voor cloudopslag.

**API formaat**

```http
POST /runs/
```

**Verzoek**

Met de volgende aanvraag wordt een flowuitvoering voor de flow-id `3abea21c-7e36-4be1-bec1-d3bad0e3e0de` gemaakt.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
      "params": {
          "startTime": "1663735590",
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567"
      }
  }'
```

| Parameter | Beschrijving |
| --- | --- |
| `flowId` | De id van de flow waarop de flow wordt uitgevoerd. |
| `params.startTime` | De geplande tijd van wanneer de de stroomlooppas op bestelling zal beginnen. Deze waarde wordt uitgedrukt in unieke tijd. |
| `params.windowStartTime` | De vroegste datum en tijd waarop de gegevens worden opgehaald. Deze waarde wordt uitgedrukt in unieke tijd. |
| `params.windowEndTime` | De datum en tijd waarop de gegevens worden opgehaald tot. Deze waarde wordt uitgedrukt in unieke tijd. |

**Reactie**

Een geslaagde reactie retourneert de details van de nieuw gemaakte flow, inclusief de unieke run `id` .


```json
{
    "items": [
        {
            "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
            "etag": "\"1100c53e-0000-0200-0000-627138980000\""
        }
    ]
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `id` | De id van de nieuwe flow-run. Zie de gids bij [&#x200B; het terugwinnen van stroomspecificaties &#x200B;](../api/collect/database-nosql.md#specs) voor meer informatie over op lijst-gebaseerde looppas specificaties. |
| `etag` | De middelversie van de stroomlooppas. |

## De stroomuitvoering controleren

Zodra uw stroomlooppas is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over stroomlooppas, voltooiingsstatus, en fouten te zien. Om uw stroomlooppas te controleren die API gebruiken, zie het leerprogramma op [&#x200B; controledataflows in API &#x200B;](./monitor.md). Om uw stroomlooppas te controleren die Experience Platform UI gebruiken, zie de gids op [&#x200B; gegevensstroom controlemogelijkheden gebruikend het controledashboard &#x200B;](../../../dataflows/ui/monitor-sources.md).
