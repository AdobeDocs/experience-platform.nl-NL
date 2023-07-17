---
title: API-eindpunt voor soorten publiek
description: Gebruik het publiek eindpunt in de API van de Dienst van de Segmentatie van Adobe Experience Platform om, publiek voor uw organisatie programmatically tot stand te brengen te beheren en bij te werken.
exl-id: cb1a46e5-3294-4db2-ad46-c5e45f48df15
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '2124'
ht-degree: 0%

---

# Eind publiek

Een publiek is een verzameling personen die vergelijkbare gedragingen en/of kenmerken delen. Deze verzamelingen mensen kunnen worden gegenereerd met Adobe Experience Platform of met externe bronnen. U kunt de `/audiences` eindpunt in de Segmentatie API, die u toestaat om publiek programmatically terug te winnen, tot stand te brengen bij te werken en te schrappen.

## Aan de slag

De eindpunten die in deze handleiding worden gebruikt, maken deel uit van de [!DNL Adobe Experience Platform Segmentation Service] API. Controleer voordat je doorgaat de [gids Aan de slag](./getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van vereiste kopballen en hoe te om voorbeeld API vraag te lezen.

## Een lijst met soorten publiek ophalen {#list}

U kunt een lijst van alle soorten publiek voor uw organisatie terugwinnen door een verzoek van de GET aan te dienen `/audiences` eindpunt.

**API-indeling**

De `/audiences` het eindpunt steunt verscheidene vraagparameters helpen uw resultaten filtreren. Hoewel deze parameters optioneel zijn, wordt het gebruik ervan sterk aanbevolen om kostbare overhead te verminderen wanneer resources worden vermeld. Als u een vraag aan dit eindpunt zonder parameters maakt, zullen alle publiek beschikbaar voor uw organisatie worden teruggewonnen. U kunt meerdere parameters opnemen, gescheiden door ampersands (`&`).

```http
GET /audiences
GET /audiences?{QUERY_PARAMETERS}
```

De volgende vraagparameters kunnen worden gebruikt wanneer het terugwinnen van een lijst van publiek:

| Query-parameter | Beschrijving | Voorbeeld |
| --------------- | ----------- | ------- |
| `start` | Geeft de beginverschuiving voor het geretourneerde publiek aan. | `start=5` |
| `limit` | Hiermee geeft u het maximale aantal bezoekers op dat per pagina wordt geretourneerd. | `limit=10` |
| `sort` | Hiermee geeft u de volgorde op waarin de resultaten moeten worden gesorteerd. Dit is geschreven in de indeling `attributeName:[desc/asc]`. | `sort=updateTime:desc` |
| `property` | Een filter waarmee u een publiek kunt opgeven dat **exact** komt overeen met de waarde van een kenmerk. Dit is geschreven in de indeling `property=` | `property=audienceId==test-audience-id` |
| `name` | Een filter waarmee u een publiek kunt opgeven waarvan de namen **bevatten** de opgegeven waarde. Deze waarde is niet hoofdlettergevoelig. | `name=Sample` |
| `description` | Een filter waarmee u een publiek kunt opgeven waarvan de beschrijvingen **bevatten** de opgegeven waarde. Deze waarde is niet hoofdlettergevoelig. | `description=Test Description` |

**Verzoek**

Het volgende verzoek wint de laatste twee publiek terug dat in uw organisatie wordt gecreeerd.

+++A steekproefverzoek om een lijst van publiek terug te winnen.

```shell
curl -X GET https: //platform.adobe.io/data/core/ups/audiences?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwoord**

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
| `audienceId` | Beide | Als het publiek een publiek is dat door een Platform wordt gegenereerd, is dit dezelfde waarde als de `id`. Als het publiek extern wordt gegenereerd, wordt deze waarde door de client opgegeven. |
| `schema` | Beide | Het schema van de Gegevens van de Ervaring Model (XDM) van het publiek. |
| `imsOrgId` | Beide | De id van de organisatie waartoe het publiek behoort. |
| `sandbox` | Beide | Informatie over de sandbox waartoe het publiek behoort. Meer informatie over sandboxen vindt u in de [sandboxen, overzicht](../../sandboxes/home.md). |
| `name` | Beide | De naam van het publiek. |
| `description` | Beide | Een beschrijving van het publiek. |
| `expression` | Door Platform gegenereerd | De PQL-expressie (Profile Query Language) van het publiek. Meer informatie over PQL-expressies vindt u in het gedeelte [Hulplijn voor PQL-expressies](../pql/overview.md). |
| `mergePolicyId` | Door Platform gegenereerd | De id van het samenvoegbeleid waaraan het publiek is gekoppeld. Meer informatie over het samenvoegbeleid vindt u in het gedeelte [handleiding voor samenvoegbeleid](../../profile/api/merge-policies.md). |
| `evaluationInfo` | Door Platform gegenereerd | Toont hoe het publiek zal worden geëvalueerd. Mogelijke evaluatiemethoden zijn batch, synchronous (streaming) of continue (edge). Meer informatie over de evaluatiemethoden vindt u in de [segmentatieoverzicht](../home.md) |
| `dependents` | Beide | Een array met gebruikers-id&#39;s die afhankelijk zijn van het huidige publiek. Dit zou worden gebruikt als u een publiek creeert dat een segment van een segment is. |
| `dependencies` | Beide | Een array met publiek-id&#39;s waarvan het publiek afhankelijk is. Dit zou worden gebruikt als u een publiek creeert dat een segment van een segment is. |
| `type` | Beide | Een door het systeem gegenereerd veld dat weergeeft of het publiek door het Platform wordt gegenereerd of dat een extern gegenereerd publiek is. Mogelijke waarden zijn `SegmentDefinition` en `ExternalSegment`. A `SegmentDefinition` verwijst naar een publiek dat in Platform is gegenereerd, terwijl een `ExternalSegment` verwijst naar een publiek dat niet in Platform is gegenereerd. |
| `originName` | Beide | Een veld dat verwijst naar de naam van de oorsprong van het publiek. Voor publiek dat door Platforms wordt gegenereerd, wordt deze waarde `REAL_TIME_CUSTOMER_PROFILE`. Voor soorten publiek die worden gegenereerd in Audience Orchestration, wordt deze waarde `AUDIENCE_ORCHESTRATION`. Voor in Adobe Audience Manager gegenereerde soorten publiek wordt deze waarde `AUDIENCE_MANAGER`. Voor andere extern gegenereerde soorten publiek wordt deze waarde `CUSTOM_UPLOAD`. |
| `createdBy` | Beide | De id van de gebruiker die het publiek heeft gemaakt. |
| `labels` | Beide | Gegevensgebruik op objectniveau en op kenmerk gebaseerde toegangsbeheerlabels die relevant zijn voor het publiek. |
| `namespace` | Beide | De naamruimte waartoe het publiek behoort. Mogelijke waarden zijn `AAM`, `AAMSegments`, `AAMTraits`, en `AEPSegments`. |
| `linkedAudienceRef` | Beide | Een object dat id&#39;s bevat voor andere publiekgerelateerde systemen. |

+++

## Een nieuw publiek maken {#create}

U kunt een nieuw publiek tot stand brengen door een verzoek van de POST aan `/audiences` eindpunt.

**API-indeling**

```http
POST /audiences
```

**Verzoek**

>[!BEGINTABS]

>[!TAB Door Platforms gegenereerd publiek]

+++ Een voorbeeldverzoek voor het creëren van een Platform-geproduceerd publiek

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
| `type` | Een veld waarin wordt weergegeven of het publiek door Platforms wordt gegenereerd of dat een extern gegenereerd publiek is. Mogelijke waarden zijn `SegmentDefinition` en `ExternalSegment`. A `SegmentDefinition` verwijst naar een publiek dat in Platform is gegenereerd, terwijl een `ExternalSegment` verwijst naar een publiek dat niet in Platform is gegenereerd. |
| `expression` | De PQL-expressie (Profile Query Language) van het publiek. Meer informatie over PQL-expressies vindt u in het gedeelte [Hulplijn voor PQL-expressies](../pql/overview.md). |
| `schema` | Het schema van de Gegevens van de Ervaring Model (XDM) van het publiek. |
| `labels` | Gegevensgebruik op objectniveau en op kenmerk gebaseerde toegangsbeheerlabels die relevant zijn voor het publiek. |
| `ttlInDays` | Geeft de vervalwaarde van de gegevens voor het publiek aan, in dagen. |

+++

>[!TAB Extern gegenereerd publiek]

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
| `type` | Een veld waarin wordt weergegeven of het publiek door Platforms wordt gegenereerd of dat een extern gegenereerd publiek is. Mogelijke waarden zijn `SegmentDefinition` en `ExternalSegment`. A `SegmentDefinition` verwijst naar een publiek dat in Platform is gegenereerd, terwijl een `ExternalSegment` verwijst naar een publiek dat niet in Platform is gegenereerd. |
| `originName` | De naam van de oorsprong van het publiek. Voor extern gegenereerde soorten publiek is de standaardwaarde hiervan `CUSTOM_UPLOAD`. Andere ondersteunde waarden zijn `REAL_TIME_CUSTOMER_PROFILE`, `CUSTOM_UPLOAD`, `AUDIENCE_ORCHESTRATION`, en `AUDIENCE_MATCH`. |
| `lifecycleState` | Een optioneel veld dat de begintoestand bepaalt van het publiek dat u wilt maken. Tot de ondersteunde waarden behoren `draft`, `published`, en `inactive`. |
| `datasetId` | De id van de dataset waar de gegevens worden gevonden die het publiek omvatten. |
| `labels` | Gegevensgebruik op objectniveau en op kenmerk gebaseerde toegangsbeheerlabels die relevant zijn voor het publiek. |
| `audienceMeta` | Metagegevens die bij het extern gegenereerde publiek horen. |
| `linkedAudienceRef` | Een object dat id&#39;s bevat voor andere publieksgerelateerde systemen. Dit kan het volgende omvatten: <ul><li>`flowId`: Deze id wordt gebruikt om het publiek te verbinden met de dataflow die werd gebruikt om de publieksgegevens in te brengen. Meer informatie over de vereiste id&#39;s vindt u in de [een gegevensstroomhulplijn maken](../../sources/tutorials/api/collect/cloud-storage.md).</li><li>`aoWorkflowId`: Deze ID wordt gebruikt om het publiek met een verwante samenstelling van het Orchestration van het Publiek te verbinden.&lt;/li/> <li>`payloadFieldGroupRef`: Deze id wordt gebruikt om naar het schema van de Groep van het Gebied XDM te verwijzen dat de structuur van het publiek beschrijft. Meer informatie over de waarde van dit veld vindt u in het gedeelte [XDM-eindgebruikershandleiding voor veldgroep](../../xdm/api/field-groups.md).</li><li>`audienceFolderId`: Deze id wordt gebruikt om naar de map-id in Adobe Audience Manager voor het publiek te verwijzen. Meer informatie over deze API vindt u in de [Adobe Audience Manager API-handleiding](https://bank.demdex.com/portal/swagger/index.html#/Segment%20Folder%20API).</ul> |

+++

>[!ENDTABS]

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met informatie over uw pas gecreeerd publiek terug.

>[!BEGINTABS]

>[!TAB Door Platforms gegenereerd publiek]

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

>[!TAB Extern gegenereerd publiek]

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

U kunt gedetailleerde informatie over een specifiek publiek opzoeken door een verzoek van de GET aan het `/audiences` eindpunt en het verstrekken van identiteitskaart van het publiek u wenst om in de verzoekweg terug te winnen.

**API-indeling**

```http
GET /audiences/{AUDIENCE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- | 
| `{AUDIENCE_ID}` | De id van het publiek dat u probeert op te halen. Dit is het `id` veld, en is **niet** de `audienceId` veld. |

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

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met informatie over het gespecificeerde publiek terug. De reactie is anders, afhankelijk van of het publiek wordt gegenereerd met Adobe Experience Platform of externe bronnen.

>[!BEGINTABS]

>[!TAB Door Platforms gegenereerd publiek]

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

>[!TAB Extern gegenereerd publiek]

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

U kunt de velden van specifieke doelgroepen bijwerken door een PATCH-aanvraag in te dienen bij de `/audiences` en het verstrekken van identiteitskaart van het publiek u wenst om in de verzoekweg bij te werken.

**API-indeling**

```http
PATCH /audiences/{AUDIENCE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{AUDIENCE_ID}` | De id van het publiek dat u wilt bijwerken. Dit is het `id` veld, en is **niet** de `audienceId` veld. |

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
| `op` | Voor het bijwerken van soorten publiek is deze waarde altijd `add`. |
| `path` | Het pad van het veld dat u wilt bijwerken. |
| `value` | De waarde waaraan u het veld wilt bijwerken. |

+++

**Antwoord**

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

U kunt een specifiek publiek bijwerken (overschrijven) door een verzoek van de PUT aan het `/audiences` en het verstrekken van identiteitskaart van het publiek u wenst om in de verzoekweg bij te werken.

**API-indeling**

```http
PUT /audiences/{AUDIENCE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{AUDIENCE_ID}` | De id van het publiek dat u wilt bijwerken. Dit is het `id` veld, en is **niet** de `audienceId` veld. |

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
| `type` | Een door het systeem gegenereerd veld dat weergeeft of het publiek door het Platform wordt gegenereerd of dat een extern gegenereerd publiek is. Mogelijke waarden zijn `SegmentDefinition` en `ExternalSegment`. A `SegmentDefinition` verwijst naar een publiek dat in Platform is gegenereerd, terwijl een `ExternalSegment` verwijst naar een publiek dat niet in Platform is gegenereerd. |
| `lifecycleState` | De status van het publiek. Mogelijke waarden zijn `draft`, `published`, en `inactive`. `draft` vertegenwoordigt wanneer het publiek wordt gecreëerd; `published` wanneer het publiek wordt gepubliceerd, en `inactive` wanneer het publiek niet meer actief is. |
| `datasetId` | De id van de dataset die de publieksgegevens kunnen worden gevonden. |
| `labels` | Gegevensgebruik op objectniveau en op kenmerk gebaseerde toegangsbeheerlabels die relevant zijn voor het publiek. |

+++

**Antwoord**

Een geslaagde reactie retourneert HTTP status 200 met details over uw onlangs bijgewerkte publiek. Houd er rekening mee dat de details van uw publiek verschillen, afhankelijk van het publiek dat door een Platform wordt gegenereerd of een publiek dat extern wordt gegenereerd.

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

U kunt een specifiek publiek verwijderen door een DELETE-aanvraag in te dienen bij de `/audiences` eindpunt en het verstrekken van identiteitskaart van het publiek u wenst om in de verzoekweg te schrappen.

**API-indeling**

```http
DELETE /audiences/{AUDIENCE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{AUDIENCE_ID}` | De id van het publiek dat u wilt verwijderen. Dit is het `id` veld, en is **niet** de `audienceId` veld. |

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

**Antwoord**

Een succesvolle reactie retourneert HTTP status 204 zonder bericht.

## Meerdere soorten publiek ophalen {#bulk-get}

U kunt veelvoudige soorten publiek terugwinnen door een verzoek van de POST aan `/audiences/bulk-get` en het verstrekken van identiteitskaarts van het publiek u wenst terug te winnen.

**API-indeling**

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

**Antwoord**

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

## Meerdere soorten publiek bijwerken {#bulk-patch}

U kunt het profiel en het aantal records van meerdere soorten publiek bijwerken door een POST aan te vragen bij de `/audiences/bulk-patch-metric` en het verstrekken van identiteitskaarts van het publiek u wenst om bij te werken.

**API-indeling**

```http
POST /audiences/bulk-patch-metric
```

**Verzoek**

+++ Een voorbeeldverzoek om meerdere soorten publiek bij te werken.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences/bulk-patch-metric
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d ' {
    "jobId": "12345",
    "jobType": "AO",
    "resources": [
        {
            "audienceId": "QUFNVHJhaXRzX2V4dGVybmFsU2VnbWVudC1hdWRpZW5jZS1pZA_6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "namespace": "AAMTraits",
            "operations": [
                {
                    "op": "add",
                    "path": "/metrics/data",
                    "value": {
                        "totalProfiles": 11037
                    }
                },
            ]
        },
        {
            "audienceId": "QUFNVHJhaXRzX2V4dGVybmFsU2VnbWVudC1hdWRpZW5jZS1pZA_6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
            "namespace": "AAMTraits",
            "operations": [
                {
                    "op": "add",
                    "path": "/metrics/data",
                    "value": {
                        "totalProfiles": 523
                    }
                }
            ]
        }
    ]
    }
```

<table>
<thead>
<tr>
<th>Parameter</th>
<th>Beschrijving</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>jobId</code></td>
<td>De id van de taak die de update uitvoert.</td>
</tr>
<tr>
<td><code>jobType</code></td>
<td>Het type taak waarmee de update wordt uitgevoerd. Deze waarde kan <code>export</code> of <code>AO</code>.</td>
</tr>
<tr>
<td><code>audienceId</code></td>
<td>De id van het publiek dat u wilt bijwerken. Dit is het <code>audienceId</code> waarde, en <strong>niet</strong> de <code>id</code> waarde van het publiek.</td>
</tr>
<tr>
<td><code>namespace</code></td>
<td>De naamruimte voor het publiek dat u wilt bijwerken.</td>
</tr>
<tr>
<td><code>operations</code></td>
<td>Een object met de informatie die wordt gebruikt om het publiek bij te werken.</td>
</tr>
<tr>
<td><code>operations.op</code></td>
<td>De bewerking die voor de patch wordt gebruikt. Wanneer u meerdere soorten publiek bijwerkt, is deze waarde <strong>altijd</strong> <code>add</code>.</td>
</tr>
<tr>
<td><code>operations.path</code></td>
<td>Het pad van het veld dat moet worden bijgewerkt. Momenteel worden slechts twee paden ondersteund: <code>/metrics/data</code> wanneer u de <strong>profiel</strong> tellen en <code>/recordMetrics/data</code> wanneer u de <strong>opnemen</strong> aantal.</td>
</tr>
<tr>
<td><code>operations.value</code></td>
<td>
De waarde van het veld dat moet worden bijgewerkt. Wanneer u het aantal profielen bijwerkt, ziet deze waarde er als volgt uit: 
<pre>
{
    "totalProfiles": 123456
}
</pre>
Wanneer u de recordtelling bijwerkt, ziet deze waarde er als volgt uit: 
<pre>
{ "recordCount": } 123456 }
</pre>
</td>
</tr>
</tbody>
</table>

+++

**Antwoord**

Een succesvolle reactie retourneert HTTP-status 207 met details over het bijgewerkte publiek.

+++ Een voorbeeldreactie voor het bijwerken van meerdere soorten publiek.

```json
{
   "resources":[
      {
         "audienceId":"QUFNVHJhaXRzX2V4dGVybmFsU2VnbWVudC1hdWRpZW5jZS1pZA_6ed34f6f-fe21-4a30-934f-6ffe21fa3075",

         "namespace": "AAMTraits",
         "status":200
      },
      {
         "audienceId":"QUFNVHJhaXRzX2V4dGVybmFsU2VnbWVudC1vcmlnaW4tdGVzdDE_6ed34f6f-fe21-4a30-934f-6ffe21fa3075",

         "namespace": "AAMTraits",
         "status":200
      }
   ]
}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `status` | De status van het bijgewerkte publiek. Als de geretourneerde status 200 is, is het publiek bijgewerkt. Als het publiek niet kon worden bijgewerkt, zal een fout die verklaren waarom het publiek niet werd bijgewerkt terugkeren. |

+++

## Volgende stappen

Na het lezen van deze handleiding hebt u nu een beter inzicht in hoe u publiek kunt maken, beheren en verwijderen met de Adobe Experience Platform API. Voor meer informatie over publieksbeheer met behulp van de gebruikersinterface leest u de [segmenteringsUI-hulplijn](../ui/overview.md).
