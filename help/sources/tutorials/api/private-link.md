---
title: Ondersteuning voor persoonlijke koppelingen voor bronnen in de API
description: Meer informatie over het maken en gebruiken van persoonlijke koppelingen voor Adobe Experience Platform Sources
badge: Beta
hide: true
hidefromtoc: true
exl-id: 9b7fc1be-5f42-4e29-b552-0b0423a40aa1
source-git-commit: 45a50800f74a6a072e4246b11d338b0c134856e0
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 0%

---

# Ondersteuning voor persoonlijke koppelingen voor bronnen in de API

>[!AVAILABILITY]
>
>Deze functie is in Beperkte Beschikbaarheid en wordt momenteel slechts gesteund door de volgende bronnen:
>
>* [[!DNL Azure Blob]](../../connectors/cloud-storage/blob.md)
>* [[!DNL Azure Data Lake Gen2]](../../connectors/cloud-storage/adls-gen2.md)
>* [[!DNL Azure File Storage]](../../connectors/cloud-storage/azure-file-storage.md)
>* [[!DNL Snowflake]](../../connectors/databases/snowflake.md)

Met de functie Private Link kunt u persoonlijke eindpunten maken waarmee uw Adobe Experience Platform-bronnen verbinding kunnen maken. Sluit veilig uw bronnen aan een virtueel netwerk aan gebruikend privé IP adressen, die de behoefte aan openbare IPs elimineren en uw aanvalsoppervlakte verminderen. Vereenvoudig uw netwerkopstelling door de behoefte aan complexe firewall of de configuraties van de Vertaling van het Adres van het Netwerk te verwijderen, terwijl het verzekeren van gegevensverkeer slechts de goedgekeurde diensten bereikt.

Lees deze gids om te leren hoe u APIs kunt gebruiken om een privé eindpunt tot stand te brengen en te gebruiken.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [ Bronnen ](../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [ Sandboxes ](../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele [!DNL Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../landing/api-guide.md).

## Een privé-eindpunt maken {#create-private-endpoint}

Maak een POST-verzoek aan `/privateEndpoints` om een privé-eindpunt te maken.

**API formaat**

```http
POST /privateEndpoints
```

**Verzoek**

Het volgende verzoek leidt tot een privé eindpunt:

+++Selecteren om aanvraagvoorbeeld weer te geven

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Private Endpoint",
      "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [],
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
    }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van uw privé eindpunt. |
| `subscriptionId` | De id die is gekoppeld aan uw [!DNL Azure] -abonnement. Voor meer informatie, lees de [!DNL Azure] gids op [ het terugwinnen van uw abonnement en huurder IDs van  [!DNL Azure Portal] ](https://learn.microsoft.com/en-us/azure/azure-portal/get-subscription-tenant-id). |
| `resourceGroupName` | De naam van de bronnengroep op [!DNL Azure] . Een resourcegroep bevat gerelateerde bronnen voor een [!DNL Azure] -oplossing. Voor meer informatie, lees de [!DNL Azure] gids over [ het leiden middelgroepen ](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal). |
| `resourceName` | De naam van uw bron. In [!DNL Azure] verwijst een bron naar instanties zoals virtuele machines, webapps en databases. Voor meer informatie, lees de [!DNL Azure] gids op [ die de  [!DNL Azure]  middelmanager ](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview) begrijpt. |
| `fqdns` | De volledig gekwalificeerde domeinnamen voor uw bron. Deze eigenschap is alleen vereist bij gebruik van de [!DNL Snowflake] -bron. |
| `connectionSpec.id` | De verbindingsspecificatie-id van de bron die u gebruikt. |
| `connectionSpec.version` | De versie van de verbindingsspecificatie-id die u gebruikt. |

+++

**Reactie**

Een geslaagde reactie retourneert het volgende:

+++Selecteren om reactievoorbeeld weer te geven

```json
{
  "id": "2c7f6574-299a-4832-aec5-886e875872e2",
  "name": "ACME Private Endpoint",
  "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
  "resourceGroupName": "acme-sources-experience-platform",
  "resourceName": "acmeexperienceplatform",
  "fqdns": [],
  "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
  },
  "state": "Pending"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `id` | Identiteitskaart van uw onlangs gecreeerd privé eindpunt. |
| `name` | De naam van uw privé eindpunt. |
| `subscriptionId` | De id die is gekoppeld aan uw [!DNL Azure] -abonnement. Voor meer informatie, lees de [!DNL Azure] gids op [ het terugwinnen van uw abonnement en huurder IDs van  [!DNL Azure Portal] ](https://learn.microsoft.com/en-us/azure/azure-portal/get-subscription-tenant-id). |
| `resourceGroupName` | De naam van de bronnengroep op [!DNL Azure] . Een resourcegroep bevat gerelateerde bronnen voor een [!DNL Azure] -oplossing. Voor meer informatie, lees de [!DNL Azure] gids over [ het leiden middelgroepen ](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal). |
| `resourceName` | De naam van uw bron. In [!DNL Azure] verwijst een bron naar instanties zoals virtuele machines, webapps en databases. Voor meer informatie, lees de [!DNL Azure] gids op [ die de  [!DNL Azure]  middelmanager ](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview) begrijpt. |
| `fqdns` | De volledig gekwalificeerde domeinnamen voor uw bron. Deze eigenschap is alleen vereist bij gebruik van de [!DNL Snowflake] -bron. |
| `connectionSpec.id` | De verbindingsspecificatie-id van de bron die u gebruikt. |
| `connectionSpec.version` | De versie van de verbindingsspecificatie-id die u gebruikt. |
| `state` | De huidige staat van uw privé eindpunt. Geldige statussen zijn: <ul><li>`Pending`</li><li>`Failed`</li><li>`Approved`</li><li>`Rejected`</li></ul> |

+++

## Een lijst met persoonlijke eindpunten ophalen {#retrieve-private-endpoints}

Als u een lijst met persoonlijke eindpunten van een bepaalde sandbox in uw organisatie wilt ophalen, vraagt u GET om `/privateEndpoints` .

**API formaat**

```http
GET /privateEndpoints
```

**Verzoek**

Het volgende verzoek wint een lijst van alle privé eindpunten terug die in uw organisatie bestaan.

+++Selecteren om aanvraagvoorbeeld weer te geven

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Reactie**

Een succesvolle reactie keert een lijst van privé eindpunten in uw organisatie terug.

+++Selecteren om reactievoorbeeld weer te geven

```json
{
  "items": [
       {
      "id": "ac9eb695-0d1a-42d4-bc45-0842aeaa1eff",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
      "resourceGroupName": "acme-noid-experience-platform",
      "resourceName": "acmeprivatelinking",
      "fqdns": [
         
      ],
      "state": "Approved",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    },
          {
      "id": "4c9eb695-0d1a-42d4-bc45-0842aeaa1efr",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [
         
      ],
      "state": "Pending",
      "connectionSpec": {
        "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
        "version": "1.0"
      }
    } 
  ]
}
```

+++

## Hiermee wordt een lijst met persoonlijke eindpunten voor een bepaalde bron opgehaald {#retrieve-private-endpoints-by-source}

Als u een lijst wilt ophalen met persoonlijke eindpunten die overeenkomen met een specifieke bron, vraagt u GET het `/privateEndpoints` -eindpunt aan en geeft u de `connectionSpec.id` -bron op.

**API formaat**

```http
GET /privateEndpoints?property=connectionSpec.id=={CONNECTION_SPEC_ID}
```

| Query-parameter | Beschrijving |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | De verbindingsspecificatie-id van de bron waarnaar u persoonlijke eindpunten wilt zoeken. |

**Verzoek**

Met het volgende verzoek wordt een lijst opgehaald van alle persoonlijke eindpunten die overeenkomen met de bron met de verbindingsspecificatie-id: `4c10e202-c428-4796-9208-5f1f5732b1cf` .

+++Selecteren om aanvraagvoorbeeld weer te geven

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints?property=connectionSpec.id==4c10e202-c428-4796-9208-5f1f5732b1cf' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Reactie**

Een succesvol antwoord retourneert een lijst met alle persoonlijke eindpunten die overeenkomen met de bron met de verbindingsspecificatie-id: `4c10e202-c428-4796-9208-5f1f5732b1cf` .

+++Selecteren om reactievoorbeeld weer te geven

```json
{
  "items": [
       {
      "id": "ac9eb695-0d1a-42d4-bc45-0842aeaa1eff",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
      "resourceGroupName": "acme-noid-experience-platform",
      "resourceName": "acmeprivatelinkhg",
      "fqdns": [
         
      ],
      "state": "Approved",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    },
    {
      "id": "4c9eb695-0d1a-42d4-bc45-0842aeaa1efr",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [
         
      ],
      "state": "Pending",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    } 
  ]
}
```

+++

## Een privé eindpunt ophalen {#retrieve-specific-private-endpoint}

Om een specifiek privé eindpunt terug te winnen, doe een verzoek van GET aan `/privateEndpoints` en verstrek identiteitskaart van het privé eindpunt dat u wilt terugwinnen.

**API formaat**

```http
GET /privateEndpoints/{PRIVATE_ENDPOINT_ID}
```

| Query-parameter | Beschrijving |
| --- | --- |
| `{PRIVATE_ENDPOINT_ID}` | Identiteitskaart van het privé eindpunt dat u wilt terugwinnen. |

**Verzoek**

Het volgende verzoek wint het privé eindpunt met identiteitskaart terug:`2c5699b0-b9b6-486f-8877-ee5e21fe9a9d`.

+++Selecteren om aanvraagvoorbeeld weer te geven

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/2c5699b0-b9b6-486f-8877-ee5e21fe9a9d' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Reactie**

Een geslaagde reactie retourneert het persoonlijke eindpunt met de id: `2c5699b0-b9b6-486f-8877-ee5e21fe9a9d`

+++Selecteren om reactievoorbeeld weer te geven

```json
{
  "items": [
       {
      "id": "2c5699b0-b9b6-486f-8877-ee5e21fe9a9d",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-noid-experience-platform",
      "resourceName": "acmeprivatelinkhg",
      "fqdns": [
         
      ],
      "state": "Approved",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    }
  ]
}
```

+++

## Een privéeindpunt oplossen {#resolve-private-endpoint}

**API formaat**

```http
GET /privateEndpoints?op=autoResolve
```

**Verzoek**

+++Selecteren om aanvraagvoorbeeld weer te geven

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints?op=autoResolve' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "usePrivateLink": true,
              "connectionString": "{CONNECTION_STRING}"
          }
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

+++

**Reactie**

+++Selecteren om reactievoorbeeld weer te geven

```json
{
  "items": [
        {
      "id": "4c9eb695-0d1a-42d4-bc45-0842aeaa1efr",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [
         
      ],
      "state": "Pending",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      } 
    }
  ]
}
```

+++

## [!DNL Interactive Authoring] inschakelen {#enable-interactive-authoring}

>[!IMPORTANT]
>
>U moet [!DNL Interactive Authoring] inschakelen voordat u een flow maakt of bijwerkt en voordat u een verbinding maakt, bijwerkt of verkent.

[!DNL Interactive Authoring] wordt gebruikt voor functies zoals het verkennen van een verbinding of account en het voorvertonen van gegevens. Als u [!DNL Interactive Authoring] wilt inschakelen, moet u een POST-aanvraag indienen bij `/privateEndpoints/interactiveAuthoring` en `enable` opgeven als een operator in de queryparameters.

**API formaat**

```http
POST /privateEndpoints/interactiveAuthoring?op=enable
```

| Query-parameter | Beschrijving |
| --- | --- |
| `op` | De bewerking die u wilt uitvoeren. Als u [!DNL Interactive Authoring] wilt inschakelen, stelt u de `op` waarde in op `enable` . |

**Verzoek**

Het volgende verzoek laat [!DNL Interactive Authoring] voor uw privé eindpunt toe en plaatst TTL aan 60 minuten.

+++Selecteren om aanvraagvoorbeeld weer te geven

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/interactiveAuthoring?op=enable' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "autoTerminationMinutes": 60
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `autoTerminationMinutes` | De [!DNL Interactive Authoring] TTL (time-to-live) in minuten. [!DNL Interactive Authoring] wordt gebruikt voor functies zoals het verkennen van een verbinding of account en het voorvertonen van gegevens. U kunt een maximum TTL van 120 minuten plaatsen. De standaard TTL is 60 minuten. |

+++

**Reactie**

Een geslaagde reactie retourneert HTTP-status 202 (geaccepteerd).

## [!DNL Interactive Authoring] status ophalen {#retrieve-interactive-authoring-status}

Als u de huidige status van [!DNL Interactive Authoring] voor uw persoonlijke eindpunt wilt weergeven, vraagt u GET om `/privateEndpoints/interactiveAuthoring` .

**API formaat**

```http
GET /privateEndpoints/interactiveAuthoring
```

**Verzoek**

Met de volgende aanvraag wordt de status van [!DNL Interactive Authoring] opgehaald:

+++Selecteren om aanvraagvoorbeeld weer te geven

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/interactiveAuthoring' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Reactie**

+++Selecteren om reactievoorbeeld weer te geven

```json
{
    "status": "Disabled"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `status` | De status van [!DNL Interactive Authoring] . Geldige waarden zijn: `disabled` , `enabling` , `enabled` . |

+++

## Persoonlijk eindpunt verwijderen {#delete-private-endpoint}

Om uw privé eindpunt te schrappen, doe een DELETE verzoek aan `/privateEndpoints` en verstrek identiteitskaart van het eindpunt dat u wilt schrappen.

**API formaat**

```http
DELETE /privateEndpoints/{PRIVATE_ENDPOINT_ID}
```

| Query-parameter | Beschrijving |
| --- | --- |
| `{PRIVATE_ENDPOINT_ID}` | Identiteitskaart van het privé eindpunt dat u wilt schrappen. |

**Verzoek**

Het volgende verzoek verwijdert het persoonlijke eindpunt met de id: `02a74b31-a566-4a86-9cea-309b101a7f24` .

+++Selecteren om aanvraagvoorbeeld weer te geven

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/02a74b31-a566-4a86-9cea-309b101a7f24' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 (Voltooid). U kunt de verwijdering controleren door een GET-aanvraag in te dienen en aan `/privateEndpoints` een verwijderde id op te geven als een queryparameter.

## Flow Service {#flow-service}

Lees de volgende secties voor informatie over hoe u privé eindpunten samen met [[!DNL Flow Service]  API ](https://developer.adobe.com/experience-platform-apis/references/flow-service/) kunt gebruiken.

### Verbinding maken met een privé-eindpunt {#create-base-connection}

Als u een verbinding wilt maken met een privéeindpunt in Experience Platform, vraagt u een POST-aanvraag naar het `/connections` -eindpunt van de [!DNL Flow Service] API.

**API formaat**

```http
POST /connections/
```

**Verzoek**

Het volgende verzoek leidt tot een voor authentiek verklaarde basisverbinding voor [!DNL Snowflake], terwijl ook het gebruiken van een privé eindpunt.

+++Selecteren om aanvraagvoorbeeld weer te geven

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection",
      "description": "A base connection for a Snowflake source that uses a private link.",
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "connectionString": "{CONNECTION_STRING}",
              "usePrivateLink" : true
          }
      },
      "connectionSpec": {
          "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van uw basisverbinding. |
| `description` | (Optioneel) Een beschrijving met aanvullende informatie over de verbinding. |
| `auth.specName` | De verificatie die wordt gebruikt om uw bron te verbinden met Experience Platform. |
| `auth.params.connectionString` | De [!DNL Snowflake] verbindingstekenreeks. Voor meer informatie, lees de [[!DNL Snowflake]  API authentificatiegids ](../api/create/databases/snowflake.md). |
| `auth.params.usePrivateLink` | Een booleaanse waarde die bepaalt of u een privé eindpunt gebruikt of niet. Stel deze waarde in op `true` als u een privé-eindpunt gebruikt. |
| `connectionSpec.id` | De verbindingsspecificatie-id van [!DNL Snowflake] . |
| `connectionSpec.version` | De versie van uw [!DNL Snowflake] connection spec ID. |

+++

**Reactie**

Een geslaagde reactie retourneert de zojuist gegenereerde basis verbindings-id en -tag.

+++Selecteren om reactievoorbeeld weer te geven

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

+++

### Hiermee worden verbindingen opgehaald die zijn gekoppeld aan een bepaald privéeindpunt {#retrieve-connections-by-endpoint}

Om verbindingen terug te winnen verbonden aan een bepaald privé eindpunt, doe een verzoek van GET aan het `/connections` eindpunt en verstrek identiteitskaart van het privé eindpunt als vraagparameter.

**API formaat**

```http
GET /connections?property=auth.params.privateEndpointId=={PRIVATE_ENDPOINT_ID}
```

| Query-parameter | Beschrijving |
| --- | --- |
| {PRIVATE_ENDPOINT_ID} | Identiteitskaart van het privé eindpunt verbonden aan de verbindingen die u wilt terugwinnen. |

**Verzoek**

Het volgende verzoek wint bestaande verbindingen terug die aan privé eindpunt met identiteitskaart worden gebonden: `02a74b31-a566-4a86-9cea-309b101a7f24`.

+++Selecteren om aanvraagvoorbeeld weer te geven

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections?property=auth.params.privateEndpointId==02a74b31-a566-4a86-9cea-309b101a7f24' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Reactie**

Een succesvolle reactie keert een lijst van verbindingen terug die aan het gevraagde privé eindpunt worden gebonden.

+++Selecteren om reactievoorbeeld weer te geven

```json
{
  "items": [
    {
      "id": "42a27b1f-8e3f-48ce-8c29-7e474b29a015",
      "createdAt": 1729154379292,
      "updatedAt": 1729154382031,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme-e2e",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true,
          "privateEndpointId": "02a74b31-a566-4a86-9cea-309b101a7f24"
        }
      },
      "version": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "etag": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    },
    {
      "id": "6350311a-664c-4b08-aad4-4065781aac81",
      "createdAt": 1718199941102,
      "updatedAt": 1718199945147,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme demo",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true,
          "privateEndpointId": "02a74b31-a566-4a86-9cea-309b101a7f24"
        }
      },
      "version": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "etag": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    }
  ],
  "_links": {
     
  }
}
```

+++

### Verbindingen ophalen die zijn gekoppeld aan een willekeurig particulier eindpunt {#retrieve-connections}

Als u verbindingen wilt ophalen die aan een willekeurig particulier eindpunt zijn gekoppeld, moet u een GET-aanvraag indienen bij het `/connections` -eindpunt en `property=auth.params.usePrivateLink==true` opgeven als een queryparameter.

**API formaat**

```http
GET /connections?property=auth.params.usePrivateLink==true
```

**Verzoek**

Het volgende verzoek wint alle verbindingen in uw organisatie terug die privé eindpunten gebruiken.

+++Selecteren om aanvraagvoorbeeld weer te geven

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections?property=auth.params.usePrivateLink==true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Reactie**

Een geslaagde reactie retourneert alle verbindingen die aan persoonlijke eindpunten zijn gekoppeld.

+++Selecteren om reactievoorbeeld weer te geven

```json
{
  "items": [
    {
      "id": "42a27b1f-8e3f-48ce-8c29-7e474b29a015",
      "createdAt": 1729154379292,
      "updatedAt": 1729154382031,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme-e2e",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true,
          "privateEndpointId": "02a74b31-a566-4a86-9cea-309b101a7f24"
        }
      },
      "version": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "etag": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    },
    {
      "id": "6350311a-664c-4b08-aad4-4065781aac81",
      "createdAt": 1718199941102,
      "updatedAt": 1718199945147,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme demo",
      "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true
        }
      },
      "version": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "etag": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    }
  ],
  "_links": {
     
  }
}
```

+++

## Bijlage

Lees deze sectie voor meer informatie met [!DNL Azure] persoonlijke koppelingen in de API.

### Uw [!DNL Snowflake] -account configureren voor verbinding met persoonlijke koppelingen

U moet de volgende stappen uitvoeren om de [!DNL Snowflake] -bron te kunnen gebruiken met persoonlijke koppelingen.

Eerst, moet u een steunkaartje in [!DNL Snowflake] opheffen en om **identiteitskaart van het eindpuntdienstmiddel** van het [!DNL Azure] gebied van uw [!DNL Snowflake] rekening verzoeken. Voer de onderstaande stappen uit om een [!DNL Snowflake] -ticket op te halen:

1. Navigeer aan [[!DNL Snowflake]  UI ](https://app.snowflake.com) en teken binnen met uw e-mailrekening. Tijdens deze stap moet u controleren of uw e-mail is geverifieerd in de profielinstellingen.
2. Selecteer uw **gebruikersmenu** en selecteer dan **steun** om tot [!DNL Snowflake] steun toegang te hebben.
3. Selecteer **[!DNL + Support Case]** als u een draagtas wilt maken. Vul vervolgens het formulier in met relevante gegevens en voeg de benodigde bestanden bij.
4. Als u klaar bent, verzendt u de kwestie.

De eindpuntmiddel identiteitskaart wordt geformatteerd als volgt:

```shell
subscriptions/{SUBSCRIPTION_ID}/resourceGroups/az{REGION}-privatelink/providers/microsoft.network/privatelinkservices/sf-pvlinksvc-az{REGION}
```

+++Selecteren om voorbeeld weer te geven

```shell
/subscriptions/4575fb04-6859-4781-8948-7f3a92dc06a3/resourceGroups/azwestus2-privatelink/providers/microsoft.network/privatelinkservices/sf-pvlinksvc-azwestus2
```

+++

| Parameter | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `{SUBSCRIPTION_ID}` | De unieke id die uw [!DNL Azure] -abonnement aangeeft. | `a1b2c3d4-5678-90ab-cdef-1234567890ab` |
| `{REGION}` | Het [!DNL Azure] gebied van uw [!DNL Snowflake] account. | `azwestus2` |

### Haal de configuratiegegevens van uw persoonlijke koppeling op

Als u de configuratiegegevens van uw persoonlijke koppeling wilt ophalen, moet u de volgende opdracht uitvoeren in [!DNL Snowflake] :

```sql
USE ROLE accountadmin;
SELECT key, value::varchar
FROM TABLE(FLATTEN(input => PARSE_JSON(SYSTEM$GET_PRIVATELINK_CONFIG())));
```

Vervolgens haalt u waarden op voor de volgende eigenschappen:

* `privatelink-account-url`
* `regionless-privatelink-account-url`
* `privatelink_ocsp-url`

Nadat u de waarden hebt opgehaald, kunt u de volgende aanroep uitvoeren om een persoonlijke koppeling voor [!DNL Snowflake] te maken.

**Verzoek**

Met de volgende aanvraag wordt een privéeindpunt voor [!DNL Snowflake] gemaakt:

>[!BEGINTABS]

>[!TAB  Malplaatje ]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "{ENDPOINT_NAME}",
    "subscriptionId": "{AZURE_SUBSCRIPTION_ID}",
    "resourceGroupName": "{RESOURCE_GROUP_NAME}",
    "resourceName": "{SNOWFLAKE_ENDPOINT_SERVICE_NAME}",
    "fqdns": [
      "{PRIVATELINK_ACCOUNT_URL}",
      "{REGIONLESS_PRIVATELINK_ACCOUNT_URL}",
      "{PRIVATELINK_OCSP_URL}"
    ],
    "connectionSpec": {
      "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
      "version": "1.0"
    }
  }'
```

>[!TAB  Voorbeeld ]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "TEST_Snowflake_PE",
    "subscriptionId": "4575fb04-6859-4781-8948-7f3a92dc06a3",
    "resourceGroupName": "azwestus2-privatelink",
    "resourceName": "sf-pvlinksvc-azwestus2",
    "fqdns": [
      "hf06619.west-us-2.privatelink.snowflakecomputing.com",
      "adobe-segmentationdbint.privatelink.snowflakecomputing.com",
      "ocsp.hf06619.west-us-2.privatelink.snowflakecomputing.com"
    ],
    "connectionSpec": {
      "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
      "version": "1.0"
    }
  }'
```


>[!ENDTABS]

### Een privé-eindpunt goedkeuren voor [!DNL Azure Blob] en [!DNL Azure Data Lake Gen2]

Als u een aanvraag voor een privéeindpunt voor de bronnen [!DNL Azure Blob] en [!DNL Azure Data Lake Gen2] wilt goedkeuren, meldt u zich aan bij de map [!DNL Azure Portal] . Selecteer in de linkernavigatie **[!DNL Data storage]** , ga naar de tab **[!DNL Security + networking]** en kies **[!DNL Networking]** . Selecteer vervolgens **[!DNL Private endpoints]** om een lijst weer te geven met persoonlijke eindpunten die zijn gekoppeld aan uw account en de huidige verbindingsstatussen. Als u een aanvraag in behandeling wilt goedkeuren, selecteert u het gewenste eindpunt en klikt u op **[!DNL Approve]** .

![ het Azure portaal met een lijst van hangende privé eindpunten.](../../images/tutorials/private-links/azure.png)
