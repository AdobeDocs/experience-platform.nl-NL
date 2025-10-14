---
title: Gegevensstromen bijwerken met behulp van de Flow Service API
description: Leer hoe te om een gegevensstroom, met inbegrip van zijn naam, beschrijving, en programma, gebruikend de Dienst API van de Stroom.
exl-id: 367a3a9e-0980-4144-a669-e4cfa7a9c722
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 0%

---

# Dataflows bijwerken met behulp van de Flow Service API

Dit leerprogramma behandelt de stappen voor het bijwerken van een dataflow, met inbegrip van zijn basisinformatie, programma, en kaartreeksen die [[!DNL Flow Service]  API &#x200B;](https://www.adobe.io/experience-platform-apis/references/flow-service/) gebruiken.

>[!TIP]
>
>Uw bronverbinding en uw doelverbinding moeten aan één dataflow worden toegewezen. Werk de bron- en doelverbindingen niet afzonderlijk bij, omdat de wijzigingen niet in de bijbehorende gegevensstroom worden doorgevoerd. Als uw gebruiksgeval een update van uw bron en doelverbindingen vereist, dan moet u een nieuw paar bron en doelverbindingen, evenals een nieuwe dataflow tot stand brengen.

## Aan de slag

Voor deze zelfstudie hebt u een geldige stroom-id nodig. Als u geen geldige stroom identiteitskaart hebt, selecteer uw schakelaar van keus van het [&#x200B; overzicht van bronnen &#x200B;](../../home.md) en volg de stappen die vóór het proberen van dit leerprogramma worden geschetst.

Voor deze zelfstudie hebt u ook een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [&#x200B; Bronnen &#x200B;](../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [&#x200B; Sandboxes &#x200B;](../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [&#x200B; begonnen wordt met Experience Platform APIs &#x200B;](../../../landing/api-guide.md).

## Gegevens over gegevensstroom opzoeken

De eerste stap bij het bijwerken van uw gegevensstroom is gegevens terug te winnen die uw stroom ID gebruiken. U kunt de huidige details van een bestaande gegevensstroom bekijken door een GET- verzoek aan het `/flows` eindpunt te doen.

**API formaat**

```http
GET /flows/{FLOW_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{FLOW_ID}` | De unieke `id` -waarde voor de gegevensstroom die u wilt ophalen. |

**Verzoek**

Met het volgende verzoek wordt bijgewerkte informatie over uw flow-id opgehaald.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie keert de huidige details van uw gegevensstroom met inbegrip van zijn versie, programma, en uniek herkenningsteken (`id`) terug.

```json
{
    "items": [
        {
            "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
            "createdAt": 1612310475905,
            "updatedAt": 1614122324830,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Database dataflow using BigQuery",
            "description": "collecting test1.Mytable from Google BigQuery",
            "flowSpec": {
                "id": "14518937-270c-4525-bdec-c2ba7cce3860",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"5400d99c-0000-0200-0000-60358d540000\"",
            "etag": "\"5400d99c-0000-0200-0000-60358d540000\"",
            "sourceConnectionIds": [
                "b7581b59-c603-4df1-a689-d23d7ac440f3"
            ],
            "targetConnectionIds": [
                "320f119a-5ac1-4ab1-88ea-eb19e674ea2e"
            ],
            "inheritedAttributes": {
                "sourceConnections": [
                    {
                        "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
                        "connectionSpec": {
                            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
                            "version": "1.0"
                        },
                        "baseConnection": {
                            "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
                            "connectionSpec": {
                                "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
                                "version": "1.0"
                            }
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "320f119a-5ac1-4ab1-88ea-eb19e674ea2e",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "scheduleParams": {
                "startTime": "1612310466",
                "frequency": "week",
                "interval": "15",
                "backfill": "true"
            },
            "transformations": [
                {
                    "name": "Copy",
                    "params": {
                        "deltaColumn": {
                            "name": "Datefield",
                            "dateFormat": "YYYY-MM-DD",
                            "timezone": "UTC"
                        }
                    }
                },
                {
                    "name": "Mapping",
                    "params": {
                        "mappingId": "0b090130b58b4819afc78b6dc98b484d",
                        "mappingVersion": "0"
                    }
                }
            ],
            "runs": "/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c/runs",
            "lastOperation": {
                "started": 1614122316652,
                "updated": 1614122324830,
                "percentCompleted": 100.0,
                "status": {
                    "value": "completed",
                    "errors": []
                },
                "ops": [
                    {
                        "op": "replace",
                        "path": "/scheduleParams/frequency",
                        "value": "week"
                    }
                ],
                "operation": "update"
            },
            "lastRunDetails": {
                "id": "a10cc80b-fbea-4c6b-873e-d7fd32f4d12d",
                "state": "success",
                "startedAtUTC": 1613079975512,
                "completedAtUTC": 1613080027511
            }
        }
    ]
}
```

## Gegevensstroom bijwerken

Als u het schema, de naam en de beschrijving van uw gegevensstroom wilt bijwerken, moet u een PATCH-aanvraag voor de [!DNL Flow Service] -API uitvoeren en tegelijkertijd uw flow-id, -versie en het nieuwe schema opgeven dat u wilt gebruiken.

>[!IMPORTANT]
>
>De header `If-Match` is vereist wanneer een PATCH-aanvraag wordt ingediend. De waarde voor deze header is de unieke versie van de verbinding die u wilt bijwerken. De labelwaarde wordt bijgewerkt bij elke geslaagde update van een gegevensstroom.

**API formaat**

```http
PATCH /flows/{FLOW_ID}
```

**Verzoek**

De volgende aanvraag werkt uw schema voor de uitvoering van de flow bij, evenals de naam en beschrijving van uw gegevensstroom.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
            {
                "op": "replace",
                "path": "/scheduleParams/frequency",
                "value": "day"
            },
            {
                "op": "replace",
                "path": "/name",
                "value": "Database Dataflow Feb2021"
            },
            {
                "op": "replace",
                "path": "/description",
                "value": "Database dataflow for testing update API"
            }
        ]'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om dataflow bij te werken. Bewerkingen zijn: `add` , `replace` en `remove` . |
| `path` | Definieert het deel van de flow dat moet worden bijgewerkt. |
| `value` | De nieuwe waarde waarmee u de parameter wilt bijwerken. |

**Reactie**

Een geslaagde reactie retourneert uw flow-id en een bijgewerkt label. U kunt de update verifiëren door een GET-aanvraag in te dienen bij de [!DNL Flow Service] API en tegelijk uw flow-id op te geven.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Toewijzing bijwerken

U kunt de toewijzingenset van een bestaande gegevensstroom bijwerken door een PATCH-aanvraag in te dienen bij de [!DNL Flow Service] API en door bijgewerkte waarden voor de `mappingId` en `mappingVersion` op te geven.

**API formaat**

```http
PATCH /flows/{FLOW_ID}
```

**Verzoek**

Met de volgende aanvraag wordt de toewijzingenset van uw gegevensstroom bijgewerkt.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "50014cc8-0000-0200-0000-6036eb720000"' \
    -d '[
        {
            "op": "replace",
            "path": "/transformations/0",
            "value": {
                "name": "Mapping",
                "params": {
                    "mappingId": "c5f22f04e09f44498e528901546a83b1",
                    "mappingVersion": 2
                }
            }
        }
    ]'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om dataflow bij te werken. Bewerkingen zijn: `add` , `replace` en `remove` . |
| `path` | Definieert het deel van de flow dat moet worden bijgewerkt. In dit voorbeeld wordt `transformations` bijgewerkt. |
| `value.name` | De naam van de eigenschap die moet worden bijgewerkt. |
| `value.params.mappingId` | De nieuwe afbeeldings-id die moet worden gebruikt om de toewijzingsset van de gegevensstroom bij te werken. |
| `value.params.mappingVersion` | De nieuwe toewijzingsversie die is gekoppeld aan de bijgewerkte toewijzingsID. |

**Reactie**

Een geslaagde reactie retourneert uw flow-id en een bijgewerkt label. U kunt de update verifiëren door een GET-aanvraag in te dienen bij de [!DNL Flow Service] API en tegelijk uw flow-id op te geven.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"2c000802-0000-0200-0000-613976440000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de basisinformatie-, planning- en toewijzingssets van uw gegevensstroom bijgewerkt met behulp van de [!DNL Flow Service] API. Voor meer informatie bij het gebruiken van bronschakelaars, zie het [&#x200B; overzicht van bronnen &#x200B;](../../home.md).
