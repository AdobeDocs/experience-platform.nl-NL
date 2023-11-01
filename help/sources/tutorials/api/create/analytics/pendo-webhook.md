---
title: Creeer een Verbinding Bron en Dataflow voor Pendo gebruikend de Dienst API van de Stroom
description: Leer hoe u Adobe Experience Platform verbindt met Pendo met behulp van de Flow Service API.
badge: Beta
exl-id: 12b0295d-4b26-4eb7-a02a-a01d825d2a1e
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1455'
ht-degree: 0%

---

# Een bronverbinding en gegevensstroom maken voor [!DNL Pendo] de Flow Service API gebruiken

>[!NOTE]
>
>De [!DNL Pendo] De bron is in bèta. Lees de [overzicht van bronnen](../../../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

Het volgende leerprogramma begeleidt u door de stappen om een bronverbinding en een dataflow tot stand te brengen [[!DNL Pendo]](https://Pendo.com/) gebeurtenisgegevens naar Adobe Experience Platform met de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag {#getting-started}

Deze handleiding vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één platforminstantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## Verbinden [!DNL Pendo] naar Platform met de [!DNL Flow Service] API {#connect-platform-to-flow-api}

Hieronder worden de stappen beschreven die u moet uitvoeren om een bronverbinding en een gegevensstroom te maken om uw [!DNL Pendo] gebeurtenisgegevens naar Experience Platform.

### Een bronverbinding maken {#source-connection}

Maak een bronverbinding door een POST aan te vragen bij de [!DNL Flow Service] API, terwijl de verbindings specificatie-id van uw bron, details zoals naam en beschrijving, en het formaat van uw gegevens wordt verstrekt.

**API-indeling**

```https
POST /sourceConnections
```

**Verzoek**

Met de volgende aanvraag wordt een bronverbinding gemaakt voor [!DNL Pendo]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Source Connection for Pendo",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "description": "Streaming Source Connection for Pendo",
      "connectionSpec": {
          "id": "6ff5654f-19d5-427d-bd3e-c0ebc802389a",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      }
    }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van de bronverbinding. Zorg ervoor dat de naam van uw bronverbinding beschrijvend is aangezien u dit kunt gebruiken om informatie over uw bronverbinding op te zoeken. |
| `description` | Een optionele waarde die u kunt opnemen voor meer informatie over de bronverbinding. |
| `connectionSpec.id` | De verbindingsspecificatie-id die overeenkomt met uw bron. |
| `data.format` | Het formaat van de [!DNL Pendo] gegevens die u wilt invoeren. Momenteel is de enige ondersteunde gegevensindeling `json`. |

**Antwoord**

Een geslaagde reactie retourneert de unieke id (`id`) van de nieuwe bronverbinding. Deze id is in een latere stap vereist om een gegevensstroom te maken.

```json
{
    "id": "76b968ff-3ff0-4e98-98bb-f3205d4d370c",
    "etag": "\"0301c198-0000-0200-0000-63f32ba50000\""
}
```

### Een doel-XDM-schema maken {#target-schema}

Om de brongegevens in Platform te gebruiken, moet een doelschema worden gecreeerd om de brongegevens volgens uw behoeften te structureren. Het doelschema wordt dan gebruikt om een dataset van het Platform tot stand te brengen waarin de brongegevens bevat zijn.

Een doelXDM schema kan tot stand worden gebracht door een POST verzoek aan te voeren [Schema-register-API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

Voor gedetailleerde stappen op hoe te om een doelXDM schema tot stand te brengen, zie de zelfstudie op [een schema maken met de API](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html#create).

### Een doelgegevensset maken {#target-dataset}

Een doeldataset kan tot stand worden gebracht door een verzoek van de POST aan [Catalogusservice-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), op voorwaarde dat de id van het doelschema zich binnen de payload bevindt.

Voor gedetailleerde stappen op hoe te om een doeldataset tot stand te brengen, zie het leerprogramma op [een gegevensset maken met de API](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html).

### Een doelverbinding maken {#target-connection}

Een doelverbinding vertegenwoordigt de verbinding met de bestemming waar de ingesloten gegevens moeten worden opgeslagen. Om een doelverbinding tot stand te brengen, moet u vaste identiteitskaart van de verbindingsspecificatie verstrekken die aan het gegevens meer beantwoordt. Deze id is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

U hebt nu de unieke herkenningstekens een doelschema een doeldataset en identiteitskaart van de verbindingsspecificatie aan het gegevensmeer. Met deze id&#39;s kunt u een doelverbinding maken met de [!DNL Flow Service] API om de dataset te specificeren die de binnenkomende brongegevens zal bevatten.

**API-indeling**

```https
POST /targetConnections
```

**Verzoek**

Met de volgende aanvraag wordt een doelverbinding gemaakt voor [!DNL Pendo]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Target Connection for Pendo",
      "description": "Streaming Target Connection for Pendo",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "json",
          "schema": {
              "id": "https://ns.adobe.com/extconndev/schemas/b48de0b204046e65a4c50232e7946401946b4c519fd7c172",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "63dca52231a6031c07280614"
      }
  }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `name` | De naam van de doelverbinding. Zorg ervoor dat de naam van uw doelverbinding beschrijvend is aangezien u dit kunt gebruiken om informatie over uw doelverbinding op te zoeken. |
| `description` | Een optionele waarde die u kunt opnemen voor meer informatie over de doelverbinding. |
| `connectionSpec.id` | De id van de verbindingsspecificatie die correspondeert met data Lake. Deze vaste ID is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | Het formaat van de [!DNL Pendo] gegevens die u wilt invoeren. |
| `params.dataSetId` | De doel dataset ID die in een vorige stap wordt teruggewonnen. |

**Antwoord**

Een geslaagde reactie retourneert de unieke id van de nieuwe doelverbinding (`id`). Deze id is vereist in latere stappen.

```json
{
    "id": "c63978c1-df7e-4611-aa32-3657eab5704b",
    "etag": "\"7f0045f1-0000-0200-0000-63f32c9d0000\""
}
```

### Een toewijzing maken {#mapping}

Opdat de brongegevens in een doeldataset moeten worden opgenomen, moet het eerst aan het doelschema worden in kaart gebracht dat de doeldataset zich aan houdt. Dit wordt bereikt door een verzoek van de POST uit te voeren aan [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) met gegevenstoewijzingen die zijn gedefinieerd in de payload van het verzoek.

**API-indeling**

```http
POST /conversion/mappingSets
```

**Verzoek**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "outputSchema": {
          "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/945546112b746524bfd9f1264b26c2b7d8e7f5b7fadb953a",
              "contentType": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
    "mappings": [
        {
            "destinationXdmPath": "_extconndev.accountid",
            "sourceAttribute": "accountId",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.uniqueid",
            "sourceAttribute": "uniqueId",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.name1",
            "sourceAttribute": "properties.guideProperties.name",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.timestamp1",
            "sourceAttribute": "timestamp",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.visitorid",
            "sourceAttribute": "visitorId",
            "identity": false,
            "version": 0
        }
    ]
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `outputSchema.schemaRef.id` | De id van de [doel-XDM-schema](#target-schema) gegenereerd in een eerdere stap. |
| `mappings.sourceType` | Het bronkenmerktype dat wordt toegewezen. |
| `mappings.source` | Het bronkenmerk dat moet worden toegewezen aan een XDM-doelpad. |
| `mappings.destination` | Het doel-XDM-pad waaraan het bronkenmerk wordt toegewezen. |

**Antwoord**

Een geslaagde reactie retourneert details van de nieuwe toewijzing inclusief de unieke id (`id`). Deze waarde is in een latere stap vereist om een gegevensstroom te maken.

```json
{
    "id": "a126ae1a1d134c4b82bd00c2d01a039e",
    "version": 0,
    "createdDate": 1676881164541,
    "modifiedDate": 1676881164541,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### Een flow maken {#flow}

De laatste stap op weg naar het verzamelen van gegevens van [!DNL Pendo] aan Platform moet een gegevensstroom creëren. Momenteel zijn de volgende vereiste waarden voorbereid:

* [Bronverbinding-id](#source-connection)
* [Doel-verbindings-id](#target-connection)
* [Toewijzing-id](#mapping)

Een dataflow is verantwoordelijk voor het plannen en verzamelen van gegevens uit een bron. U kunt een gegevensstroom tot stand brengen door een verzoek van de POST uit te voeren terwijl het verstrekken van de eerder vermelde waarden binnen de lading.

**API-indeling**

```http
POST /flows
```

**Verzoek**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Dataflow for Pendo",
      "description": "Streaming Dataflow for Pendo",
      "flowSpec": {
          "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "339d60a5-9ff6-4eba-8197-e8887eeb3c08"
      ],
      "targetConnectionIds": [
          "df7c660e-3484-463b-b01a-1835e9b04ac9"
      ],
      "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "bae11501021646e58cecc1182451af22",
          "mappingVersion": 0
        }
      }
    ]
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van uw gegevensstroom. Zorg ervoor dat de naam van uw gegevensstroom beschrijvend is aangezien u dit kunt gebruiken om op informatie over uw gegevensstroom omhoog te kijken. |
| `description` | Een optionele waarde die u kunt opnemen voor meer informatie over uw gegevensstroom. |
| `flowSpec.id` | De flow specification-id die is vereist om een gegevensstroom te maken. Deze vaste ID is: `e77fde5a-22a8-11ed-861d-0242ac120002`. |
| `flowSpec.version` | De corresponderende versie van de specificatie-id voor de stroom. Deze waarde wordt standaard ingesteld op `1.0`. |
| `sourceConnectionIds` | De [bron-verbindings-id](#source-connection) gegenereerd in een eerdere stap. |
| `targetConnectionIds` | De [doel-verbindings-id](#target-connection) gegenereerd in een eerdere stap. |
| `transformations` | Deze eigenschap bevat de verschillende transformaties die op de gegevens moeten worden toegepast. Dit bezit wordt vereist wanneer het brengen van niet-XDM-Volgzame gegevens aan Platform. |
| `transformations.name` | De naam die aan de transformatie is toegewezen. |
| `transformations.params.mappingId` | De [toewijzing-id](#mapping) gegenereerd in een eerdere stap. |
| `transformations.params.mappingVersion` | De corresponderende versie van de toewijzing-id. Deze waarde wordt standaard ingesteld op `0`. |

**Antwoord**

Een geslaagde reactie retourneert de id (`id`) van de nieuwe gegevensstroom. Met deze id kunt u uw gegevensstroom controleren, bijwerken of verwijderen.

```json
{
    "id": "c341617b-e143-43d5-aff1-da02b3e028b6",
    "etag": "\"9c01173c-0000-0200-0000-63f32d7c0000\""
}
```

### Uw URL voor het streamingeindpunt ophalen {#get-streaming-url}

Met uw gemaakte gegevensstroom, kunt u uw het stromen eindpunt URL nu terugwinnen. U zult dit eindpunt URL gebruiken om uw bron aan een webhaak in te tekenen, toestaand uw bron om met Experience Platform te communiceren.

Om uw het stromen eindpunt URL terug te winnen, doe een verzoek van de GET aan `/flows` en geef de id van de gegevensstroom op.

**API-indeling**

```http
GET /flows/{FLOW_ID}
```

**Verzoek**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/4982698b-e6b3-48c2-8dcf-040e20121fd2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert informatie over uw gegevensstroom, met inbegrip van uw eindpunt URL terug, duidelijk als `inletUrl`. Zie de [Webhaak instellen](../../../ui/create/analytics/pendo-webhook.md#get-streaming-endpoint-url) pagina om de vereiste waarde te verkrijgen.

```json
{
    "items": [
        {
            "id": "d947e6a9-ea53-42c4-985c-c9379265491f",
            "createdAt": 1676875325841,
            "updatedAt": 1676875331938,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Streaming Dataflow for Pendo",
            "description": "Streaming Dataflow for Pendo",
            "flowSpec": {
                "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"9801a366-0000-0200-0000-63f2f92c0000\"",
            "etag": "\"9801a366-0000-0200-0000-63f2f92c0000\"",
            "sourceConnectionIds": [
                "339d60a5-9ff6-4eba-8197-e8887eeb3c08"
            ],
            "targetConnectionIds": [
                "df7c660e-3484-463b-b01a-1835e9b04ac9"
            ],
            "inheritedAttributes": {
                "properties": {
                    "isSourceFlow": true
                },
                "sourceConnections": [
                    {
                        "id": "339d60a5-9ff6-4eba-8197-e8887eeb3c08",
                        "connectionSpec": {
                            "id": "6ff5654f-19d5-427d-bd3e-c0ebc802389a",
                            "version": "1.0"
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "df7c660e-3484-463b-b01a-1835e9b04ac9",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "options": {
                "inletUrl": "https://dcs.adobedc.net/collection/e389c18dbc7f5de8b95df07b1b89d76ddd9b1e88d5423abc71b6ac9161491373"
            },
            "transformations": [
                {
                    "name": "Mapping",
                    "params": {
                        "mappingId": "bae11501021646e58cecc1182451af22",
                        "mappingVersion": 0
                    }
                }
            ],
            "runs": "/runs?property=flowId==4d90b316-1c9b-469d-935f-5a27d5deefdf",
            "providerRefId": "19d9fb14-9cb9-42a5-bb8b-23dc545e766a",
            "lastOperation": {
                "started": 0,
                "updated": 0,
                "operation": "enable"
            },
            "lastRunDetails": {
                "id": "d6972216-2332-41f6-8ed3-2ac82e6550b7",
                "state": "partialSuccess",
                "startedAtUTC": 1676862000000,
                "completedAtUTC": 1676867880000
            }
        }
    ]
}
```

## Bijlage {#appendix}

In de volgende sectie vindt u informatie over de stappen die u kunt uitvoeren om uw gegevensstroom te controleren, bij te werken en te verwijderen.

### Uw gegevensstroom controleren {#monitor-dataflow}

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over stroomlooppas, voltooiingsstatus, en fouten te zien. Lees de handleiding voor volledige API-voorbeelden op [de gegevensstroom van uw bronnen controleren met behulp van de API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### Uw gegevensstroom bijwerken {#update-dataflow}

Werk de details van uw dataflow, zoals zijn naam en beschrijving, evenals zijn looppas programma en bijbehorende kaartreeksen bij door een verzoek van de PATCH aan het `/flows` eindpunt van [!DNL Flow Service] API, terwijl het verstrekken van identiteitskaart van uw gegevensstroom. Wanneer u een PATCH-verzoek indient, moet u de unieke gegevens van uw gegevensstroom opgeven `etag` in de `If-Match` header. Lees de handleiding voor volledige API-voorbeelden op [bronnen bijwerken met behulp van de API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### Uw account bijwerken {#update-account}

Werk de naam, beschrijving en referenties van uw bronaccount bij door een PATCH-verzoek uit te voeren naar de [!DNL Flow Service] API terwijl het verstrekken van uw identiteitskaart van de basisverbinding als vraagparameter. Wanneer u een PATCH-aanvraag indient, moet u de unieke bronaccount opgeven `etag` in de `If-Match` header. Lees de handleiding voor volledige API-voorbeelden op [het bijwerken van uw bronrekening gebruikend API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### Uw gegevensstroom verwijderen {#delete-dataflow}

Verwijder de gegevensstroom door een DELETE-aanvraag uit te voeren naar de [!DNL Flow Service] API terwijl het verstrekken van identiteitskaart van dataflow wilt u als deel van de vraagparameter schrappen. Lees de handleiding voor volledige API-voorbeelden op [verwijderen, gegevensstromen met behulp van de API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### Uw account verwijderen {#delete-account}

Uw account verwijderen door een DELETE-verzoek uit te voeren aan de [!DNL Flow Service] API terwijl het verstrekken van de identiteitskaart van de basisverbinding van de rekening u wilt schrappen. Lees de handleiding voor volledige API-voorbeelden op [verwijderen van uw bronaccount met behulp van de API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).
