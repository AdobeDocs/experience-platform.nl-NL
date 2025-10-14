---
title: Een Source Connection en Dataflow voor Chatlio maken met de Flow Service API
description: Leer hoe u Adobe Experience Platform met Chatlio kunt verbinden met behulp van de Flow Service API.
badge: Beta
exl-id: 867b8096-0841-4462-9888-e60c97c2115e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1396'
ht-degree: 0%

---

# Een bronverbinding en gegevensstroom maken voor [!DNL Chatlio] met de Flow Service API

>[!NOTE]
>
>De bron [!DNL Chatlio] is in bèta. Gelieve te lezen het [&#x200B; overzicht van bronnen &#x200B;](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

Het volgende leerprogramma begeleidt u door de stappen om een bronverbinding en een dataflow tot stand te brengen [[!DNL Chatlio] &#x200B;](https://chatlio.com/) gebeurtenisgegevens aan Adobe Experience Platform te brengen gebruikend [[!DNL Flow Service]  API &#x200B;](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag {#getting-started}

Deze handleiding vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [&#x200B; Bronnen &#x200B;](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [&#x200B; Sandboxes &#x200B;](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

## Verbinding maken met Experience Platform via de [!DNL Flow Service] API[!DNL Chatlio] {#connect-platform-to-flow-api}

In het volgende voorbeeld worden de stappen beschreven die u moet uitvoeren om een bronverbinding en een gegevensstroom te maken om uw [!DNL Chatlio] gebeurtenisgegevens naar Experience Platform te brengen.

### Een bronverbinding maken {#source-connection}

Maak een bronverbinding door een POST-aanvraag in te dienen bij de [!DNL Flow Service] API en de verbindingsspecificatie-id van uw bron, details zoals naam en beschrijving en de indeling van uw gegevens op te geven.

**API formaat**

```https
POST /sourceConnections
```

**Verzoek**

Met de volgende aanvraag wordt een bronverbinding gemaakt voor [!DNL Chatlio] :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Source Connection for Chatlio.",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "description": "Streaming Source Connection for Chatlio.",
      "connectionSpec": {
          "id": "073127a3-26e3-496c-9d94-9f48fb93fba8",
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
| `data.format` | De indeling van de [!DNL Chatlio] -gegevens die u wilt invoeren. Momenteel is de enige ondersteunde gegevensindeling `json` . |

**Reactie**

Een succesvolle reactie keert het unieke herkenningsteken (`id`) van de pas gecreëerde bronverbinding terug. Deze id is in een latere stap vereist om een gegevensstroom te maken.

```json
{
    "id": "7689a40d-43eb-4f74-a3f1-092a55884f6c",
    "etag": "\"01013ed0-0000-0200-0000-63f314d00000\""
}
```

### Een doel-XDM-schema maken {#target-schema}

Als u de brongegevens in Experience Platform wilt gebruiken, moet u een doelschema maken om de brongegevens naar wens te structureren. Het doelschema wordt dan gebruikt om een dataset van Experience Platform tot stand te brengen waarin de brongegevens bevat zijn.

Een doelXDM schema kan worden gecreeerd door een POST- verzoek aan de [&#x200B; Registratie API van het Schema &#x200B;](https://developer.adobe.com/experience-platform-apis/references/schema-registry/) uit te voeren.

Voor gedetailleerde stappen op hoe te om een doelXDM schema tot stand te brengen, zie het leerprogramma op [&#x200B; creërend een schema gebruikend API &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html?lang=nl-NL#create).

### Een doelgegevensset maken {#target-dataset}

Een doeldataset kan worden gecreeerd door een POST- verzoek aan de [&#x200B; Dienst API van de Catalogus uit te voeren &#x200B;](https://developer.adobe.com/experience-platform-apis/references/catalog/), verstrekkend identiteitskaart van het doelschema binnen de nuttige lading.

Voor gedetailleerde stappen op hoe te om een doeldataset tot stand te brengen, zie het leerprogramma op [&#x200B; het creëren van een dataset gebruikend API &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html?lang=nl-NL).

### Een doelverbinding maken {#target-connection}

Een doelverbinding vertegenwoordigt de verbinding met de bestemming waar de ingesloten gegevens moeten worden opgeslagen. Om een doelverbinding tot stand te brengen, moet u vaste identiteitskaart van de verbindingsspecificatie verstrekken die aan het gegevens meer beantwoordt. Deze id is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c` .

U hebt nu de unieke herkenningstekens een doelschema een doeldataset en identiteitskaart van de verbindingsspecificatie aan het gegevensmeer. Met behulp van deze id&#39;s kunt u een doelverbinding maken met de [!DNL Flow Service] API om de gegevensset op te geven die de binnenkomende brongegevens zal bevatten.

**API formaat**

```https
POST /targetConnections
```

**Verzoek**

Met de volgende aanvraag wordt een doelverbinding voor [!DNL Chatlio] gemaakt:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Target Connection for a Chatlio.",
      "description": "Streaming Target Connection for a Chatlio.",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "json",
          "schema": {
              "id": "https://ns.adobe.com/extconndev/schemas/49cecec83dd1a8da1aef4a96c67c06654e8c337a0a3b4262",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "63ef7df781f14a1bd02a7e49"
      }
  }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `name` | De naam van de doelverbinding. Zorg ervoor dat de naam van uw doelverbinding beschrijvend is aangezien u dit kunt gebruiken om informatie over uw doelverbinding op te zoeken. |
| `description` | Een optionele waarde die u kunt opnemen voor meer informatie over de doelverbinding. |
| `connectionSpec.id` | De id van de verbindingsspecificatie die correspondeert met data Lake. Deze vaste id is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c` . |
| `data.format` | De indeling van de [!DNL Chatlio] -gegevens die u wilt invoeren. |
| `params.dataSetId` | De doel dataset ID die in een vorige stap wordt teruggewonnen. |

**Reactie**

Een succesvolle reactie keert het unieke herkenningsteken van de nieuwe doelverbinding (`id`) terug. Deze id is vereist in latere stappen.

```json
{
    "id": "f7be8ab6-e5ea-4405-83b9-200cdfb2a9e5",
    "etag": "\"7f0072bc-0000-0200-0000-63f314a50000\""
}
```

### Een toewijzing maken {#mapping}

Opdat de brongegevens in een doeldataset moeten worden opgenomen, moet het eerst aan het doelschema worden in kaart gebracht dat de doeldataset zich aan houdt. Dit wordt bereikt door een POST- verzoek aan [[!DNL Data Prep]  API &#x200B;](https://www.adobe.io/experience-platform-apis/references/data-prep/) met gegevenstoewijzingen uit te voeren die binnen de verzoeklading worden bepaald.

**API formaat**

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
            "destinationXdmPath": "_extconndev.slackchannel_ID",
            "sourceAttribute": "slackChannelId",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.slackchannel_name",
            "sourceAttribute": "slackChannelName",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.UUID",
            "sourceAttribute": "visitor.UUID",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.chatlio_email",
            "sourceAttribute": "visitor.email",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.message",
            "sourceAttribute": "message",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.channel_ID",
            "sourceAttribute": "channelId",
            "identity": false,
            "version": 0
        }
    ]
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `outputSchema.schemaRef.id` | Identiteitskaart van het [&#x200B; doelXDM- schema &#x200B;](#target-schema) in een vroegere stap wordt geproduceerd. |
| `mappings.sourceType` | Het bronkenmerktype dat wordt toegewezen. |
| `mappings.source` | Het bronkenmerk dat moet worden toegewezen aan een XDM-doelpad. |
| `mappings.destination` | Het doel-XDM-pad waaraan het bronkenmerk wordt toegewezen. |

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde afbeelding met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze waarde is in een latere stap vereist om een gegevensstroom te maken.

```json
{
    "id": "4b7188aad69c44529a5e674ab5d3568b",
    "version": 0,
    "createdDate": 1676875099546,
    "modifiedDate": 1676875099546,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### Een flow maken {#flow}

De laatste stap naar het verzenden van gegevens van [!DNL Chatlio] naar Experience Platform is het maken van een gegevensstroom. Momenteel zijn de volgende vereiste waarden voorbereid:

* [Source-verbinding-id](#source-connection)
* [Doel-verbindings-id](#target-connection)
* [Toewijzing-id](#mapping)

Een dataflow is verantwoordelijk voor het plannen en verzamelen van gegevens uit een bron. U kunt een gegevensstroom tot stand brengen door een POST- verzoek uit te voeren terwijl het verstrekken van de eerder vermelde waarden binnen de lading.

**API formaat**

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
      "name": "Streaming Dataflow for Chatlio",
      "description": "Streaming Dataflow for Chatlio",
      "flowSpec": {
          "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "7689a40d-43eb-4f74-a3f1-092a55884f6c"
      ],
      "targetConnectionIds": [
          "f7be8ab6-e5ea-4405-83b9-200cdfb2a9e5"
      ],
      "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "4b7188aad69c44529a5e674ab5d3568b",
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
| `flowSpec.id` | De flow specification-id die is vereist om een gegevensstroom te maken. Deze vaste id is: `e77fde5a-22a8-11ed-861d-0242ac120002` . |
| `flowSpec.version` | De corresponderende versie van de specificatie-id voor de stroom. Deze waarde is standaard ingesteld op `1.0` . |
| `sourceConnectionIds` | [&#x200B; bron verbindingsidentiteitskaart &#x200B;](#source-connection) die in een vroegere stap wordt geproduceerd. |
| `targetConnectionIds` | De [&#x200B; identiteitskaart van de doelverbinding &#x200B;](#target-connection) die in een vroegere stap wordt geproduceerd. |
| `transformations` | Deze eigenschap bevat de verschillende transformaties die op de gegevens moeten worden toegepast. Dit bezit wordt vereist wanneer het brengen van niet-XDM-Volgzame gegevens aan Experience Platform. |
| `transformations.name` | De naam die aan de transformatie is toegewezen. |
| `transformations.params.mappingId` | [&#x200B; afbeelding identiteitskaart &#x200B;](#mapping) die in een vroegere stap wordt geproduceerd. |
| `transformations.params.mappingVersion` | De corresponderende versie van de toewijzing-id. Deze waarde is standaard ingesteld op `0` . |

**Reactie**

Een succesvolle reactie keert identiteitskaart (`id`) van nieuw gecreeerd dataflow terug. Met deze id kunt u uw gegevensstroom controleren, bijwerken of verwijderen.

```json
{
    "id": "d947e6a9-ea53-42c4-985c-c9379265491f",
    "etag": "\"9b01c840-0000-0200-0000-63f3163e0000\""
}
```

### Uw URL voor het streamingeindpunt ophalen {#get-streaming-endpoint}

Met uw gemaakte gegevensstroom, kunt u uw het stromen eindpunt URL nu terugwinnen. U gebruikt dit eindpunt-URL om uw bron te abonneren op een webhaak, zodat uw bron kan communiceren met Experience Platform.

Om uw het stromen eindpunt URL terug te winnen, doe een GET verzoek aan het `/flows` eindpunt en verstrek identiteitskaart van uw gegevensstroom.

**API formaat**

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

**Reactie**

Een geslaagde reactie retourneert informatie over de gegevensstroom, inclusief de URL van het eindpunt, gemarkeerd als `inletUrl` . Verwijs naar de [&#x200B; pagina van Webhaak van de Opstelling &#x200B;](../../../ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint-url) om de vereiste waarde te verkrijgen.

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
            "name": "Streaming Dataflow for Chatlio",
            "description": "Streaming Dataflow for Chatlio",
            "flowSpec": {
                "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"9b012541-0000-0200-0000-63f316430000\"",
            "etag": "\"9b012541-0000-0200-0000-63f316430000\"",
            "sourceConnectionIds": [
                "7689a40d-43eb-4f74-a3f1-092a55884f6c"
            ],
            "targetConnectionIds": [
                "f7be8ab6-e5ea-4405-83b9-200cdfb2a9e5"
            ],
            "inheritedAttributes": {
                "properties": {
                    "isSourceFlow": true
                },
                "sourceConnections": [
                    {
                        "id": "7689a40d-43eb-4f74-a3f1-092a55884f6c",
                        "connectionSpec": {
                            "id": "073127a3-26e3-496c-9d94-9f48fb93fba8",
                            "version": "1.0"
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "f7be8ab6-e5ea-4405-83b9-200cdfb2a9e5",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "options": {
                "inletUrl": "https://dcs.adobedc.net/collection/e71b6a6cd7270388674f8ab68ee438da58ba4434dea63cc547ee21547275923c"
            },
            "transformations": [
                {
                    "name": "Mapping",
                    "params": {
                        "mappingId": "4b7188aad69c44529a5e674ab5d3568b",
                        "mappingVersion": 0
                    }
                }
            ],
            "runs": "/runs?property=flowId==d947e6a9-ea53-42c4-985c-c9379265491f",
            "providerRefId": "bfac26f5-9256-438c-b1a0-e07a7dc675f6",
            "lastOperation": {
                "started": 0,
                "updated": 0,
                "operation": "enable"
            }
        }
    ]
}
```

## Bijlage {#appendix}

In de volgende sectie vindt u informatie over de stappen die u kunt uitvoeren om uw gegevensstroom te controleren, bij te werken en te verwijderen.

### Uw gegevensstroom controleren {#monitor-dataflow}

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over stroomlooppas, voltooiingsstatus, en fouten te zien. Voor volledige API voorbeelden, lees de gids op [&#x200B; controlerend uw brongegevens gebruikend API &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html?lang=nl-NL).

### Uw gegevensstroom bijwerken {#update-dataflow}

Werk de details van uw gegevensstroom bij, zoals zijn naam en beschrijving, evenals zijn looppas programma en bijbehorende kaartreeksen door een PATCH- verzoek aan het `/flows` eindpunt van [!DNL Flow Service] API te doen, terwijl het verstrekken van identiteitskaart van uw gegevensstroom. Wanneer u een PATCH-aanvraag indient, moet u de unieke `etag` gegevens van uw gegevensstroom opgeven in de `If-Match` -header. Voor volledige API voorbeelden, lees de gids bij [&#x200B; het bijwerken bronnen dataflows gebruikend API &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html?lang=nl-NL)

### Uw account bijwerken {#update-account}

Werk de naam, beschrijving en gegevens van uw bronaccount bij door een PATCH-aanvraag uit te voeren naar de [!DNL Flow Service] API en uw basis-verbindings-id op te geven als een queryparameter. Wanneer u een PATCH-aanvraag indient, moet u de unieke `etag` naam van uw bronaccount opgeven in de header van `If-Match` . Voor volledige API voorbeelden, lees de gids bij [&#x200B; het bijwerken van uw bronrekening gebruikend API &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html?lang=nl-NL).

### Uw gegevensstroom verwijderen {#delete-dataflow}

Verwijder uw gegevensstroom door een DELETE-aanvraag uit te voeren naar de [!DNL Flow Service] API terwijl u de id opgeeft van de gegevensstroom die u wilt verwijderen als onderdeel van de queryparameter. Voor volledige API voorbeelden, lees de gids op [&#x200B; schrappend uw dataflows gebruikend API &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html?lang=nl-NL).

### Uw account verwijderen {#delete-account}

Verwijder uw account door een DELETE-aanvraag uit te voeren naar de [!DNL Flow Service] API terwijl u de basis-verbindings-id opgeeft van het account dat u wilt verwijderen. Voor volledige API voorbeelden, lees de gids bij [&#x200B; het schrappen van uw bronrekening gebruikend API &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html?lang=nl-NL).
