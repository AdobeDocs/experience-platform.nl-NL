---
keywords: Experience Platform;thuis;populaire onderwerpen;de stroomdienst;
title: (Bèta) creeer een Looppas van de Stroom voor Ingestie op bestelling gebruikend de Dienst API van de Stroom
description: In deze zelfstudie worden de stappen beschreven voor het maken van een flow die op aanvraag wordt uitgevoerd voor opname met behulp van de Flow Service API
exl-id: a7b20cd1-bb52-4b0a-aad0-796929555e4a
source-git-commit: 659f99a47b533bba2a6084bc8e235df2a29a6386
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 0%

---

# (Beta) Creeer een stroom die voor op bestelling opnemen loopt gebruikend [!DNL Flow Service] API

>[!IMPORTANT]
>
>Inname op aanvraag vindt momenteel plaats in bèta en uw organisatie heeft er wellicht nog geen toegang toe. De functionaliteit die in deze documentatie wordt beschreven, kan worden gewijzigd.

De looppas van de stroom vertegenwoordigt een geval van stroomuitvoering. Bijvoorbeeld, als een stroom om uur bij 9:00 AM, 10:00 AM, en 11:00 AM gepland is te lopen, dan zou u drie instanties van een stroomlooppas hebben. De looppas van de stroom is specifiek voor uw bepaalde organisatie.

Op bestelling kunt u een stroom maken die tegen een gegeven gegevensstroom wordt uitgevoerd. Dit staat uw gebruikers toe om een stroomlooppas tot stand te brengen, die op bepaalde parameters wordt gebaseerd en een opnamecyclus, zonder de diensttekenen tot stand te brengen.

In deze zelfstudie worden de stappen beschreven voor het gebruik van opname op aanvraag en het maken van een flowuitvoering met behulp van de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

>[!NOTE]
>
>Als u een flowuitvoering wilt maken, moet u eerst over de flow-id van een gegevensstroom beschikken die voor eenmalige invoer is gepland.

Voor deze zelfstudie hebt u een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Sandboxen](../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../landing/api-guide.md).

## Een doorloop maken voor een op tabellen gebaseerde bron

Om een stroom voor een op lijst-gebaseerde bron tot stand te brengen, doe een verzoek van de POST aan [!DNL Flow Service] API terwijl het verstrekken van identiteitskaart van de stroom u de looppas wilt tot stand brengen tegen, evenals waarden voor begintijd, eindtijd, en deltakolom.

>[!TIP]
>
>Op tabel gebaseerde bronnen bevatten de volgende broncategorieën: reclame, analyses, toestemming en voorkeuren, CRM&#39;s, succes van de klant, database, marketingautomatisering, betalingen en protocollen.

**API-indeling**

```http
POST /runs/
```

**Verzoek**

Met de volgende aanvraag wordt een flowuitvoering voor de flow-id gemaakt `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

>[!NOTE]
>
>U hoeft alleen de `deltaColumn` bij het maken van de eerste flowuitvoering. Daarna, `deltaColumn` wordt als onderdeel van `copy` transformatie in de stroom en zal als bron van waarheid worden behandeld. Alle pogingen om de `deltaColumn` De waarde door de parameters van de stroomlooppas zal in een fout resulteren.

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
| `params.windowStartTime` | Een geheel getal dat de begintijd definieert van het venster waarin gegevens moeten worden opgehaald. De waarde wordt uitgedrukt in unieke tijd. |
| `params.windowEndTime` | Een geheel getal dat de eindtijd definieert van het venster waarin gegevens moeten worden opgehaald. De waarde wordt uitgedrukt in unieke tijd. |
| `params.deltaColumn` | De deltakolom wordt vereist om de gegevens te verdelen en nieuw opgenomen gegevens van historische gegevens te scheiden. |
| `params.deltaColumn.name` | De naam van de deltakolom. |

**Antwoord**

Een succesvolle reactie keert de details van de pas gecreëerde stroomlooppas, met inbegrip van zijn unieke looppas terug `id`.

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "createdAt": 1651587212543,
    "updatedAt": 1651587223839,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "imsOrgId": "{ORGANIZATION_ID}",
    "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
    "params": {
        "windowStartTime": "1651584991",
        "windowEndTime": "16515859567",
        "deltaColumn": {
            "name": "DOB"
        }
    },
    "etag": "\"1100c53e-0000-0200-0000-627138980000\"",
    "metrics": {
        "statusSummary": {
            "status": "scheduled"
        }
    },
    "activities": []
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `id` | De id van de nieuwe flow-run. Zie de handleiding op [ophalen, stroomspecificaties](../api/collect/database-nosql.md#specs) voor meer informatie over op tabel-gebaseerde runtime specificaties. |
| `createdAt` | De unieke tijdstempel die aangeeft wanneer de flowuitvoering is gemaakt. |
| `updatedAt` | De unieke tijdstempel die aangeeft wanneer de flowuitvoering voor het laatst is bijgewerkt. |
| `createdBy` | De organisatie-id van de gebruiker die de flow heeft gemaakt. |
| `updatedBy` | De organisatie-id van de gebruiker die de flowuitvoering voor het laatst heeft bijgewerkt. |
| `createdClient` | De toepassingsclient die de flow heeft gemaakt. |
| `updatedClient` | De toepassingsclient die de flowuitvoering voor het laatst heeft bijgewerkt. |
| `sandboxId` | De id van de sandbox die de flowuitvoering bevat. |
| `sandboxName` | De naam van de sandbox die de uitgevoerde flow bevat. |
| `imsOrgId` | De organisatie-id. |
| `flowId` | De id van de flow waarop de flow wordt uitgevoerd. |
| `params.windowStartTime` | Een geheel getal dat de begintijd definieert van het venster waarin gegevens moeten worden opgehaald. De waarde wordt uitgedrukt in unieke tijd. |
| `params.windowEndTime` | Een geheel getal dat de eindtijd definieert van het venster waarin gegevens moeten worden opgehaald. De waarde wordt uitgedrukt in unieke tijd. |
| `params.deltaColumn` | De deltakolom wordt vereist om de gegevens te verdelen en nieuw opgenomen gegevens van historische gegevens te scheiden. **Opmerking**: De `deltaColumn` is alleen nodig bij het maken van uw eerste flowuitvoering. |
| `params.deltaColumn.name` | De naam van de deltakolom. |
| `etag` | De middelversie van de stroomlooppas. |
| `metrics` | This property displays a status summary for the flow run. |

## Een doorloop maken voor een op een bestand gebaseerde bron

Om een stroom voor een op dossier-gebaseerde bron tot stand te brengen, doe een verzoek van de POST aan [!DNL Flow Service] API terwijl het verstrekken van identiteitskaart van de stroom u de looppas tegen en waarden voor begintijd en eindtijd wilt tot stand brengen.

>[!TIP]
>
>Bestandsbronnen omvatten alle bronnen voor cloudopslag.

**API-indeling**

```http
POST /runs/
```

**Verzoek**

Met de volgende aanvraag wordt een flowuitvoering voor de flow-id gemaakt `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

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
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567"
      }
  }'
```

| Parameter | Beschrijving |
| --- | --- |
| `flowId` | De id van de flow waarop de flow wordt uitgevoerd. |
| `params.windowStartTime` | Een geheel getal dat de begintijd definieert van het venster waarin gegevens moeten worden opgehaald. De waarde wordt uitgedrukt in unieke tijd. |
| `params.windowEndTime` | Een geheel getal dat de eindtijd definieert van het venster waarin gegevens moeten worden opgehaald. De waarde wordt uitgedrukt in unieke tijd. |

**Antwoord**

Een succesvolle reactie keert de details van de pas gecreëerde stroomlooppas, met inbegrip van zijn unieke looppas terug `id`.


```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "createdAt": 1651587212543,
    "updatedAt": 1651587223839,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "imsOrgId": "{ORGANIZATION_ID}",
    "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
    "params": {
        "windowStartTime": "1651584991",
        "windowEndTime": "16515859567"
    },
    "etag": "\"1100c53e-0000-0200-0000-627138980000\"",
    "metrics": {
        "statusSummary": {
            "status": "scheduled"
        }
    },
    "activities": []
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `id` | De id van de nieuwe flow-run. Zie de handleiding op [ophalen, stroomspecificaties](../api/collect/cloud-storage.md#specs) voor meer informatie over op dossier-gebaseerde looppasspecificaties. |
| `createdAt` | De unieke tijdstempel die aangeeft wanneer de flowuitvoering is gemaakt. |
| `updatedAt` | De unieke tijdstempel die aangeeft wanneer de flowuitvoering voor het laatst is bijgewerkt. |
| `createdBy` | De organisatie-id van de gebruiker die de flow heeft gemaakt. |
| `updatedBy` | De organisatie-id van de gebruiker die de flowuitvoering voor het laatst heeft bijgewerkt. |
| `createdClient` | De toepassingsclient die de flow heeft gemaakt. |
| `updatedClient` | De toepassingsclient die de flowuitvoering voor het laatst heeft bijgewerkt. |
| `sandboxId` | De id van de sandbox die de flowuitvoering bevat. |
| `sandboxName` | De naam van de sandbox die de uitgevoerde flow bevat. |
| `imsOrgId` | De organisatie-id. |
| `flowId` | De id van de flow waarop de flow wordt uitgevoerd. |
| `params.windowStartTime` | Een geheel getal dat de begintijd definieert van het venster waarin gegevens moeten worden opgehaald. De waarde wordt uitgedrukt in unieke tijd. |
| `params.windowEndTime` | Een geheel getal dat de eindtijd definieert van het venster waarin gegevens moeten worden opgehaald. De waarde wordt uitgedrukt in unieke tijd. |
| `etag` | De middelversie van de stroomlooppas. |
| `metrics` | This property displays a status summary for the flow run. |


## De stroomuitvoering controleren

Zodra uw stroomlooppas is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over stroomlooppas, voltooiingsstatus, en fouten te zien. Raadpleeg de zelfstudie voor informatie over het controleren van de stroombewerkingen met de API [gegevens controleren in de API ](./monitor.md). Om uw stroomlooppas te controleren gebruikend Platform UI, zie de gids op [gegevens van bronnen controleren met behulp van het dashboard voor bewaking](../../../dataflows/ui/monitor-sources.md).
