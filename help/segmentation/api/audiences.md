---
title: API-eindpunt voor soorten publiek
description: Gebruik het publiek eindpunt in de API van de Dienst van de Segmentatie van Adobe Experience Platform om, publiek voor uw organisatie programmatically tot stand te brengen te beheren en bij te werken.
role: Developer
exl-id: cb1a46e5-3294-4db2-ad46-c5e45f48df15
source-git-commit: 87b491339469e69653cad79b657bd1edfbca1de9
workflow-type: tm+mt
source-wordcount: '1879'
ht-degree: 0%

---

# Eind publiek

Een publiek is een verzameling personen die vergelijkbare gedragingen en/of kenmerken delen. Deze verzamelingen mensen kunnen worden gegenereerd met Adobe Experience Platform of met externe bronnen. U kunt het `/audiences` eindpunt in de Segmentatie API gebruiken, die u toestaat om publiek programmatically terug te winnen, tot stand te brengen bij te werken en te schrappen.

## Aan de slag

De eindpunten die in deze handleiding worden gebruikt, maken deel uit van de API van [!DNL Adobe Experience Platform Segmentation Service] . Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](./getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van vereiste kopballen en hoe te om voorbeeld API vraag te lezen.

## Een lijst met soorten publiek ophalen {#list}

U kunt een lijst van alle soorten publiek voor uw organisatie terugwinnen door een verzoek van de GET tot het `/audiences` eindpunt te richten.

**API formaat**

Het `/audiences` eindpunt steunt verscheidene vraagparameters helpen uw resultaten filtreren. Hoewel deze parameters optioneel zijn, wordt het gebruik ervan sterk aanbevolen om kostbare overhead te verminderen wanneer resources worden vermeld. Als u een vraag aan dit eindpunt zonder parameters maakt, zullen alle publiek beschikbaar voor uw organisatie worden teruggewonnen. De veelvoudige parameters kunnen worden omvat, die door ampersands (`&`) worden gescheiden.

```http
GET /audiences
GET /audiences?{QUERY_PARAMETERS}
```

De volgende vraagparameters kunnen worden gebruikt wanneer het terugwinnen van een lijst van publiek:

| Query-parameter | Beschrijving | Voorbeeld |
| --------------- | ----------- | ------- |
| `start` | Geeft de beginverschuiving voor het geretourneerde publiek aan. | `start=5` |
| `limit` | Hiermee geeft u het maximale aantal bezoekers per pagina op. | `limit=10` |
| `sort` | Hiermee geeft u de volgorde op waarin de resultaten moeten worden gesorteerd. Dit wordt geschreven in de indeling `attributeName:[desc/asc]` . | `sort=updateTime:desc` |
| `property` | Een filter dat u toestaat om publiek te specificeren dat **precies** de waarde van een attribuut aanpast. Dit wordt geschreven in de indeling `property=` | `property=audienceId==test-audience-id` |
| `name` | Een filter dat u toestaat om publiek te specificeren de waarvan namen **** bevatten de verstrekte waarde. Deze waarde is niet hoofdlettergevoelig. | `name=Sample` |
| `description` | Een filter dat u toestaat om publiek te specificeren de waarvan beschrijvingen **** bevatten de verstrekte waarde. Deze waarde is niet hoofdlettergevoelig. | `description=Test Description` |

**Verzoek**

Het volgende verzoek wint de laatste twee publiek terug dat in uw organisatie wordt gecreeerd.

+++A steekproefverzoek om een lijst van publiek terug te winnen.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 met een lijst van soorten publiek die in uw organisatie als JSON zijn gemaakt.

+++A steekproefreactie die de laatste twee gecreeerde publiek bevat dat tot uw organisatie behoort

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "People who ordered in the last 30 days",
            "description": "Last 30 days",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"US\""
            },
            "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "isSystem": false,
            "creationTime": 1650374572000,
            "updateEpoch": 1650374573,
            "updateTime": 1650374573000,
            "createEpoch": 1650374572,
            "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
            "dependents": [],
            "definedOn": [
                {
                    "meta: resourceType": "unions",
                    "meta: containerId": "tenant",
                    "$ref": "https: //ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "dependencies": [],
            "type": "SegmentDefinition",
            "originName": "REAL_TIME_CUSTOMER_PROFILE",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycleState": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        },
        {
            "id": "32a83b5d-a118-4bd6-b3cb-3aee2f4c30a1",
            "audienceId": "test-external-audience-id",
            "name": "externalSegment1",
            "namespace": "aam",
            "imsOrgId": "{ORG_ID}",
            "sandbox":{
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "isSystem": false,
            "description": "Last 30 days",
            "type": "ExternalSegment",
            "originName": "CUSTOM_UPLOAD",
            "lifecycleState": "published",
            "createdBy": "{CREATED_BY_ID}",
            "datasetId": "6254cf3c97f8e31b639fb14d",
            "labels":[
                "core/C1"
            ],
            "linkedAudienceRef": {
                "flowId": "4685ea90-d2b6-11ec-9d64-0242ac120002"
            },
            "creationTime": 1642745034000000,
            "updateEpoch": 1649926314,
            "updateTime": 1649926314000,
            "createEpoch": 1642745034
        }
    ],
    "_page":{
      "totalCount": 111,
      "pageSize": 2,
      "next": "1"
   },
   "_links":{
      "next":{
         "href":"@/audiences?start=1&limit=2&totalCount=111"
      }
   }
}
```

| Eigenschap | Type publiek | Beschrijving |
| -------- | ------------- | ----------- | 
| `id` | Beide | Een door het systeem gegenereerde alleen-lezen id voor het publiek. |
| `audienceId` | Beide | Als het publiek een publiek is dat via een platform wordt gegenereerd, heeft dit dezelfde waarde als de `id` . Als het publiek extern wordt gegenereerd, wordt deze waarde door de client opgegeven. |
| `schema` | Beide | Het schema van de Gegevens van de Ervaring Model (XDM) van het publiek. |
| `imsOrgId` | Beide | De id van de organisatie waartoe het publiek behoort. |
| `sandbox` | Beide | Informatie over de sandbox waartoe het publiek behoort. Meer informatie over zandbakken kan in het [ overzicht van zandbakken ](../../sandboxes/home.md) worden gevonden. |
| `name` | Beide | De naam van het publiek. |
| `description` | Beide | Een beschrijving van het publiek. |
| `expression` | Door het platform gegenereerd | De Profile Query Language (PQL)-expressie van het publiek. Meer informatie over de uitdrukkingen van PQL kan in de [ uitdrukkingengids van PQL ](../pql/overview.md) worden gevonden. |
| `mergePolicyId` | Door het platform gegenereerd | De id van het samenvoegbeleid waaraan het publiek is gekoppeld. Meer informatie over fusiebeleid kan in de [ gids van het samenvoegingsbeleid ](../../profile/api/merge-policies.md) worden gevonden. |
| `evaluationInfo` | Door het platform gegenereerd | Toont hoe het publiek zal worden geëvalueerd. Mogelijke evaluatiemethoden zijn batch, synchronous (streaming) of continue (edge). Meer informatie over de evaluatiemethodes kan in het [ segmentatieoverzicht ](../home.md) worden gevonden |
| `dependents` | Beide | Een array met gebruikers-id&#39;s die afhankelijk zijn van het huidige publiek. Dit zou worden gebruikt als u een publiek creeert dat een segment van een segment is. |
| `dependencies` | Beide | Een array met publiek-id&#39;s waarvan het publiek afhankelijk is. Dit zou worden gebruikt als u een publiek creeert dat een segment van een segment is. |
| `type` | Beide | Een door het systeem gegenereerd veld dat weergeeft of het publiek door het platform wordt gegenereerd of dat een extern gegenereerd publiek is. Mogelijke waarden zijn `SegmentDefinition` en `ExternalSegment` . Een `SegmentDefinition` verwijst naar een publiek dat is gegenereerd in Platform, terwijl een `ExternalSegment` verwijst naar een publiek dat niet is gegenereerd in Platform. |
| `originName` | Beide | Een veld dat verwijst naar de naam van de oorsprong van het publiek. Voor publiek dat door Platform wordt gegenereerd, is deze waarde `REAL_TIME_CUSTOMER_PROFILE` . Voor soorten publiek dat wordt gegenereerd in Audience Orchestration, is deze waarde `AUDIENCE_ORCHESTRATION` . Voor in Adobe Audience Manager gegenereerde soorten publiek is deze waarde `AUDIENCE_MANAGER` . Voor andere extern gegenereerde soorten publiek is deze waarde `CUSTOM_UPLOAD` . |
| `createdBy` | Beide | De id van de gebruiker die het publiek heeft gemaakt. |
| `labels` | Beide | Gegevensgebruik op objectniveau en op kenmerk gebaseerde toegangsbeheerlabels die relevant zijn voor het publiek. |
| `namespace` | Beide | De naamruimte waartoe het publiek behoort. Mogelijke waarden zijn `AAM` , `AAMSegments` , `AAMTraits` en `AEPSegments` . |
| `linkedAudienceRef` | Beide | Een object dat id&#39;s bevat voor andere publiekgerelateerde systemen. |

+++

## Een nieuw publiek maken {#create}

U kunt een nieuw publiek tot stand brengen door een verzoek van de POST aan het `/audiences` eindpunt te doen.

**API formaat**

```http
POST /audiences
```

**Verzoek**

>[!BEGINTABS]

>[!TAB  Platform-geproduceerde publiek ]

+++ Een voorbeeldverzoek om een door het platform gegenereerd publiek te maken

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
        "description": "Last 30 days",
        "type": "SegmentDefinition",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "workAddress.country = \"US\""
        },
        "schema": {
            "name": "_xdm.context.profile"
        },
        "labels": [
          "core/C1"
        ],
        "ttlInDays": 60
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- | 
| `name` | De naam van het publiek. |
| `description` | Een beschrijving van het publiek. |
| `type` | Een veld waarin wordt weergegeven of het publiek door het platform wordt gegenereerd of dat een extern gegenereerd publiek is. Mogelijke waarden zijn `SegmentDefinition` en `ExternalSegment` . Een `SegmentDefinition` verwijst naar een publiek dat is gegenereerd in Platform, terwijl een `ExternalSegment` verwijst naar een publiek dat niet is gegenereerd in Platform. |
| `expression` | De Profile Query Language (PQL)-expressie van het publiek. Meer informatie over de uitdrukkingen van PQL kan in de [ uitdrukkingengids van PQL ](../pql/overview.md) worden gevonden. |
| `schema` | Het schema van de Gegevens van de Ervaring Model (XDM) van het publiek. |
| `labels` | Gegevensgebruik op objectniveau en op kenmerk gebaseerde toegangsbeheerlabels die relevant zijn voor het publiek. |
| `ttlInDays` | Geeft de waarde aan voor de gegevensvervaldatum voor het publiek, in dagen. |

+++

>[!TAB  Extern geproduceerd publiek ]

+++ Een voorbeeldverzoek voor het maken van een extern gegenereerd publiek

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "audienceId":"test-external-audience-id",
        "name":"externalAudience",
        "namespace":"aam",
        "description":"Last 30 days",
        "type":"ExternalSegment",
        "originName":"CUSTOM_UPLOAD",
        "lifecycleState":"published",
        "datasetId":"6254cf3c97f8e31b639fb14d",
        "labels":[
            "core/C1"
        ],
        "linkedAudienceRef":{
            "flowId": "4685ea90-d2b6-11ec-9d64-0242ac120002"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- | 
| `audienceId` | Een door de gebruiker opgegeven id voor het publiek. |
| `name` | De naam van het publiek. |
| `namespace` | De naamruimte voor het publiek. |
| `description` | Een beschrijving van het publiek. |
| `type` | Een veld waarin wordt weergegeven of het publiek door het platform wordt gegenereerd of dat een extern gegenereerd publiek is. Mogelijke waarden zijn `SegmentDefinition` en `ExternalSegment` . Een `SegmentDefinition` verwijst naar een publiek dat is gegenereerd in Platform, terwijl een `ExternalSegment` verwijst naar een publiek dat niet is gegenereerd in Platform. |
| `originName` | De naam van de oorsprong van het publiek. Voor extern gegenereerde soorten publiek is de standaardwaarde `CUSTOM_UPLOAD` . Andere ondersteunde waarden zijn `REAL_TIME_CUSTOMER_PROFILE` , `CUSTOM_UPLOAD` , `AUDIENCE_ORCHESTRATION` en `AUDIENCE_MATCH` . |
| `lifecycleState` | Een optioneel veld dat de begintoestand bepaalt van het publiek dat u wilt maken. Tot de ondersteunde waarden behoren `draft` , `published` en `inactive` . |
| `datasetId` | De id van de dataset waar de gegevens worden gevonden die het publiek omvatten. |
| `labels` | Gegevensgebruik op objectniveau en op kenmerk gebaseerde toegangsbeheerlabels die relevant zijn voor het publiek. |
| `audienceMeta` | Metagegevens die bij het extern gegenereerde publiek horen. |
| `linkedAudienceRef` | Een object dat id&#39;s bevat voor andere publieksgerelateerde systemen. Dit kan het volgende omvatten: <ul><li>`flowId`: Deze id wordt gebruikt om het publiek te verbinden met de dataflow die werd gebruikt om de publieksgegevens te brengen. Meer informatie over vereiste IDs kan in [ worden gevonden leidt tot een dataflow gids ](../../sources/tutorials/api/collect/cloud-storage.md).</li><li>`aoWorkflowId`: Deze id wordt gebruikt om het publiek te verbinden met een verwante compositie van de Orchestratie van de Publiek.&lt;/li/> <li>`payloadFieldGroupRef`: Deze id wordt gebruikt om naar het schema van de Groep van het Gebied XDM te verwijzen dat de structuur van het publiek beschrijft. Meer informatie over de waarde van dit gebied kan in de [ XDM het eindpuntgids van de Groep van het Gebied ](../../xdm/api/field-groups.md) worden gevonden.</li><li>`audienceFolderId`: Deze id wordt gebruikt om naar de map-id in Adobe Audience Manager voor het publiek te verwijzen. Meer informatie over deze API kan in de [ Adobe Audience Manager API gids ](https://bank.demdex.com/portal/swagger/index.html#/Segment%20Folder%20API) worden gevonden.</ul> |

+++

>[!ENDTABS]

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met informatie over uw pas gecreeerd publiek terug.

>[!BEGINTABS]

>[!TAB  Platform-geproduceerde publiek ]

+++Een voorbeeldreactie bij het creëren van een Platform-geproduceerd publiek.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
     "schema": {
      "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem":false,     
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
    },
    "dataGovernancePolicy": {
      "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "originName": "REAL_TIME_CUSTOMER_PROFILE",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycleState": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

+++

>[!TAB  Extern geproduceerd publiek ]

+++Een voorbeeldreactie bij het maken van een extern gegenereerd publiek.

```json
{
   "id": "322f9f62-cd27-11ec-9d64-0242ac120002",
   "audienceId": "test-external-audience-id",
   "name": "externalAudience",
   "namespace": "aam",
   "imsOrgId": "{ORG_ID}",
   "sandbox":{
      "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
      "sandboxName": "prod",
      "type": "production",
      "default": true
   },
   "isSystem": false,
   "description": "Last 30 days",
   "type": "ExternalSegment",
   "originName": "CUSTOM_UPLOAD",
   "lifecycleState": "published",
   "createdBy": "{CREATED_BY_ID}",
   "datasetId": "6254cf3c97f8e31b639fb14d",
   "labels": [
      "core/C1"
   ],
   "linkedAudienceRef": {
      "flowId": "4685ea90-d2b6-11ec-9d64-0242ac120002"
   },
   "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
   "creationTime": 1650251290000,
   "updateEpoch": 1650251290,
   "updateTime": 1650251290000,
   "createEpoch": 1650251290
}
```

+++

## Een bepaald publiek opzoeken {#get}

U kunt gedetailleerde informatie over een specifiek publiek omhoog kijken door een verzoek van de GET tot het `/audiences` eindpunt te richten en identiteitskaart van het publiek te verstrekken u wenst om in de verzoekweg terug te winnen.

**API formaat**

```http
GET /audiences/{AUDIENCE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- | 
| `{AUDIENCE_ID}` | De id van het publiek dat u probeert op te halen. Gelieve te merken op dat dit het `id` gebied is, en **niet** het `audienceId` gebied is. |

**Verzoek**

+++Een voorbeeldverzoek om een publiek terug te winnen

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met informatie over het gespecificeerde publiek terug. De reactie is anders, afhankelijk van of het publiek wordt gegenereerd met Adobe Experience Platform of externe bronnen.

>[!BEGINTABS]

>[!TAB  Platform-geproduceerde publiek ]

+++A steekproefreactie wanneer het terugwinnen van een Platform-geproduceerd publiek.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem": false,
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycleState": "active",
    "labels": [
        "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

+++

>[!TAB  Extern geproduceerd publiek ]

+++Een voorbeeldreactie bij het ophalen van een extern gegenereerd publiek.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "test-external-audience-id",
    "name": "externalAudience",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem": false,
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycleState": "active",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "labels": [
        "core/C1"
    ],
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

+++

>[!ENDTABS]

## Een veld bijwerken voor een publiek {#update-field}

U kunt de gebieden van specifiek publiek bijwerken door een verzoek van PATCH aan het `/audiences` eindpunt te richten en identiteitskaart van het publiek te verstrekken u wenst om in de verzoekweg bij te werken.

**API formaat**

```http
PATCH /audiences/{AUDIENCE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{AUDIENCE_ID}` | De id van het publiek dat u wilt bijwerken. Gelieve te merken op dat dit het `id` gebied is, en **niet** het `audienceId` gebied is. |

**Verzoek**

+++Een voorbeeldverzoek om een gebied in een publiek bij te werken.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
     [
        {
            "op": "add",
            "path": "/expression",
            "value": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"CA\""
            }
        }
      ]'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `op` | Voor het bijwerken van soorten publiek is deze waarde altijd `add` . |
| `path` | Het pad van het veld dat u wilt bijwerken. |
| `value` | De waarde waaraan u het veld wilt bijwerken. |

+++

**Reactie**

Een geslaagde reactie geeft HTTP status 200 met informatie over uw onlangs bijgewerkte publiek terug.

+++A voorbeeldreactie wanneer het bijwerken van een gebied in een publiek.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"CA\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
    },
    "dataGovernancePolicy": {
      "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycleState": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

+++

## Een publiek bijwerken {#put}

U kunt een specifiek publiek bijwerken (overschrijven) door een verzoek van de PUT aan het `/audiences` eindpunt te richten en identiteitskaart van het publiek te verstrekken u wenst om in de verzoekweg bij te werken.

**API formaat**

```http
PUT /audiences/{AUDIENCE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{AUDIENCE_ID}` | De id van het publiek dat u wilt bijwerken. Gelieve te merken op dat dit het `id` gebied is, en **niet** het `audienceId` gebied is. |

**Verzoek**

+++A voorbeeldverzoek om een volledig publiek bij te werken.

```shell
curl -X PUT https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "audienceId": "test-external-audience-id",
    "name": "New external audience",
    "namespace": "aam",
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycleState": "published",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "labels": [
        "core/C1"
    ]
}' 
```

| Eigenschap | Beschrijving |
| -------- | ----------- | 
| `audienceId` | De id van het publiek. Voor extern gegenereerde soorten publiek kan deze waarde door de gebruiker worden opgegeven. |
| `name` | De naam van het publiek. |
| `namespace` | De naamruimte voor het publiek. |
| `description` | Een beschrijving van het publiek. |
| `type` | Een door het systeem gegenereerd veld dat weergeeft of het publiek door het platform wordt gegenereerd of dat een extern gegenereerd publiek is. Mogelijke waarden zijn `SegmentDefinition` en `ExternalSegment` . Een `SegmentDefinition` verwijst naar een publiek dat is gegenereerd in Platform, terwijl een `ExternalSegment` verwijst naar een publiek dat niet is gegenereerd in Platform. |
| `lifecycleState` | De status van het publiek. Mogelijke waarden zijn `draft` , `published` en `inactive` . `draft` vertegenwoordigt wanneer het publiek wordt gecreeerd, `published` wanneer het publiek wordt gepubliceerd, en `inactive` wanneer het publiek niet meer actief is. |
| `datasetId` | De id van de dataset die de publieksgegevens kunnen worden gevonden. |
| `labels` | Gegevensgebruik op objectniveau en op kenmerk gebaseerde toegangsbeheerlabels die relevant zijn voor het publiek. |

+++

**Reactie**

Een geslaagde reactie retourneert HTTP status 200 met details over uw onlangs bijgewerkte publiek. Houd er rekening mee dat de details van uw publiek verschillen, afhankelijk van het publiek dat door het platform wordt gegenereerd of een publiek dat extern wordt gegenereerd.

+++A voorbeeldreactie wanneer het bijwerken van een volledig publiek.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "New external audience",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycleState": "published",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

+++

## Een publiek verwijderen {#delete}

U kunt een specifiek publiek schrappen door een DELETE verzoek aan het `/audiences` eindpunt te doen en identiteitskaart van het publiek te verstrekken u wenst om in de verzoekweg te schrappen.

**API formaat**

```http
DELETE /audiences/{AUDIENCE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{AUDIENCE_ID}` | De id van het publiek dat u wilt verwijderen. Gelieve te merken op dat dit het `id` gebied is, en **niet** het `audienceId` gebied is. |

**Verzoek**

+++ Een voorbeeldverzoek om een publiek te verwijderen.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab5 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een geslaagde reactie retourneert HTTP status 204 zonder bericht.

## Meerdere soorten publiek ophalen {#bulk-get}

U kunt veelvoudige publiek terugwinnen door een verzoek van de POST aan het `/audiences/bulk-get` eindpunt te doen en identiteitskaarts van het publiek te verstrekken u wenst om terug te winnen.

**API formaat**

```http
POST /audiences/bulk-get
```

**Verzoek**

+++ Een voorbeeldverzoek om meerdere soorten publiek op te halen.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences/bulk-get
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d ' {
    "ids": [
        {
            "id": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd"
        },
        {
            "id": "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075"
        }
    ]
 }
```

+++

**Reactie**

Een succesvolle reactie retourneert HTTP-status 207 met informatie voor het gevraagde publiek.

+++ Een voorbeeldreactie bij het ophalen van meerdere soorten publiek.

```json
{
   "results":{
      "72c393ea-caed-441a-9eb6-5f66bb1bd6cd":{
         "id": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd",
         "audienceId": "72c393ea-caed-441a-9eb6-5f66bb1bd6cd",
         "schema": {
            "name": "_xdm.context.profile"
         },
         "ttlInDays": 30,
         "imsOrgId": "{ORG_ID}",
         "sandbox": {
            "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "sandboxName": "prod",
            "type": "production",
            "default": true
         },
         "name": "Sample audience",
         "expression": {
            "type": "pql",
            "format": "pql/text",
            "value": "_id = \"abc\""         
        },
         "mergePolicyId": "87c94d51-239c-4391-932c-29c2412100e5",
         "evaluationInfo": {
            "batch": {
               "enabled": false
            },
            "continuous": {
               "enabled": true
            },
            "synchronous": {
               "enabled": false
            }
         },
         "ansibleUiEnabled": false,
         "dataGovernancePolicy": {
            "excludeOptOut": true
         },
         "creationTime": 1623889553000000,
         "updateEpoch": 1674646369,
         "updateTime": 1674646369000,
         "createEpoch": 1623889552,
         "_etag": "\"61030ec7-0000-0200-0000-63d113610000\"",
         "dependents": [],
         "definedOn": [
            {
               "meta:resourceType": "unions",
               "meta:containerId": "tenant",
               "$ref": "https://ns.adobe.com/xdm/context/profile__union"
            }
         ],
         "dependencies": [],
         "type": "SegmentDefinition",
         "state": "enabled",
         "overridePerformanceWarnings": false,
         "lastModifiedBy": "{CREATED_ID}",
         "lifecycleState": "published",
         "namespace": "AEPSegments",
         "isSystem": false,
         "saveSegmentMembership": true,
         "originName": "REAL_TIME_CUSTOMER_PROFILE"
      },
      "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075":{
         "id": "QU9fLTEzOTgzNTE0MzY0NzY0NDg5NzkyOTkx_6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
         "name": "label test24764489707692",
         "namespace": "AO",
         "imsOrgId": "{ORG_ID}",
         "sandbox":{
            "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "sandboxName": "prod",
            "type": "production",
            "default": true
         },
         "type": "ExternalSegment",
         "lifecycleState": "published",
         "sourceId": "source-id",
         "createdBy": "{USER_ID}",
         "datasetId": "62bf31a105e9891b63525c92",
         "_etag": "\"3100da6d-0000-0200-0000-62bf31a10000\"",
         "creationTime": 1656697249000,
         "updateEpoch": 1656697249,
         "updateTime": 1656697249000,
         "createEpoch": 1656697249,
         "audienceId": "test-audience-id",
         "isSystem": false,
         "saveSegmentMembership": true,
         "linkedAudienceRef": {
            "aoWorkflowId": "62bf31858e87e34c8364befa"
         },
         "originName": "AUDIENCE_ORCHESTRATION"
      }
   }
}
```

+++


## Volgende stappen

Na het lezen van deze handleiding hebt u nu een beter inzicht in hoe u publiek kunt maken, beheren en verwijderen met de Adobe Experience Platform API. Voor meer informatie over publieksbeheer die UI gebruiken, te lezen gelieve de [ gids van de segmentatie UI ](../ui/overview.md).
