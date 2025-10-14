---
title: API-eindpunt voor soorten publiek
description: Gebruik het publiek eindpunt in de API van de Dienst van de Segmentatie van Adobe Experience Platform om, publiek voor uw organisatie programmatically tot stand te brengen te beheren en bij te werken.
role: Developer
exl-id: cb1a46e5-3294-4db2-ad46-c5e45f48df15
source-git-commit: 63fa87ac9777b3ac66d990dd4bfbd202f07b0eba
workflow-type: tm+mt
source-wordcount: '1592'
ht-degree: 0%

---

# Eind publiek

Een publiek is een verzameling personen die vergelijkbare gedragingen en/of kenmerken delen. Deze verzamelingen mensen kunnen worden gegenereerd met Adobe Experience Platform of met externe bronnen. U kunt het `/audiences` eindpunt in de Segmentatie API gebruiken, die u toestaat om publiek programmatically terug te winnen, tot stand te brengen bij te werken en te schrappen.

## Aan de slag

De eindpunten die in deze handleiding worden gebruikt, maken deel uit van de API van [!DNL Adobe Experience Platform Segmentation Service] . Alvorens verder te gaan, te herzien gelieve [&#x200B; begonnen gids &#x200B;](./getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van vereiste kopballen en hoe te om voorbeeld API vraag te lezen.

## Een lijst met soorten publiek ophalen {#list}

U kunt een lijst van alle soorten publiek voor uw organisatie terugwinnen door een GET- verzoek aan het `/audiences` eindpunt te doen.

**API formaat**

Het `/audiences` eindpunt steunt verscheidene vraagparameters helpen uw resultaten filtreren. Hoewel deze parameters optioneel zijn, wordt het gebruik ervan sterk aanbevolen om kostbare overhead te verminderen wanneer resources worden vermeld. Als u een vraag aan dit eindpunt zonder parameters maakt, zullen alle publiek beschikbaar voor uw organisatie worden teruggewonnen. De veelvoudige parameters kunnen worden omvat, die door ampersands (`&`) worden gescheiden.

```http
GET /audiences
GET /audiences?{QUERY_PARAMETERS}
```

>[!NOTE]
>
>Als u dit eindpunt zonder enige vraagparameters gebruikt, zal het inactieve publiek **niet** zijn teruggekeerd. Nochtans, als u dit eindpunt samen met de `property=audienceId` vraagparameter gebruikt, zal het inactieve publiek **&#x200B;**&#x200B;zijn teruggekeerd.

De volgende vraagparameters kunnen worden gebruikt wanneer het terugwinnen van een lijst van publiek:

| Query-parameter | Beschrijving | Voorbeeld |
| --------------- | ----------- | ------- |
| `start` | Geeft de beginverschuiving voor het geretourneerde publiek aan. | `start=5` |
| `limit` | Hiermee geeft u het maximale aantal bezoekers per pagina op. | `limit=10` |
| `sort` | Hiermee geeft u de volgorde op waarin de resultaten moeten worden gesorteerd. Dit wordt geschreven in de indeling `attributeName:[desc/asc]` . | `sort=updateTime:desc` |
| `property` | Een filter dat u toestaat om publiek te specificeren dat **precies** de waarde van een attribuut aanpast. Dit wordt geschreven in de indeling `property=` | `property=audienceId==test-audience-id` |
| `name` | Een filter dat u toestaat om publiek te specificeren de waarvan namen **&#x200B;**&#x200B;bevatten de verstrekte waarde. Deze waarde is niet hoofdlettergevoelig. | `name=Sample` |
| `description` | Een filter dat u toestaat om publiek te specificeren de waarvan beschrijvingen **&#x200B;**&#x200B;bevatten de verstrekte waarde. Deze waarde is niet hoofdlettergevoelig. | `description=Test Description` |
| `entityType` | Een filter waarmee u het type publiek kunt opgeven dat u zoekt. | `entityType=_xdm.context.account` |

**Verzoek**

Het volgende verzoek wint de laatste twee publiek terug dat in uw organisatie wordt gecreeerd.

+++Een voorbeeldverzoek om een lijst met soorten publiek op te halen.

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

+++Een voorbeeldreactie die de laatste twee gecreëerde soorten publiek bevat die tot uw organisatie behoren

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
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
      "totalPages": 21,
      "sortField": "name",
      "sort": "asc", 
      "pageSize": 5,
      "limit": 5,
      "start": "0",
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
| `sandbox` | Beide | Informatie over de sandbox waartoe het publiek behoort. Meer informatie over zandbakken kan in het [&#x200B; overzicht van zandbakken &#x200B;](../../sandboxes/home.md) worden gevonden. |
| `name` | Beide | De naam van het publiek. |
| `description` | Beide | Een beschrijving van het publiek. |
| `expression` | Door het platform gegenereerd | De Profile Query Language (PQL)-expressie van het publiek. Meer informatie over de uitdrukkingen van PQL kan in de [&#x200B; uitdrukkingengids van PQL &#x200B;](../pql/overview.md) worden gevonden. |
| `mergePolicyId` | Door het platform gegenereerd | De id van het samenvoegbeleid waaraan het publiek is gekoppeld. Meer informatie over fusiebeleid kan in de [&#x200B; gids van het samenvoegingsbeleid &#x200B;](../../profile/api/merge-policies.md) worden gevonden. |
| `evaluationInfo` | Door het platform gegenereerd | Toont hoe het publiek zal worden geëvalueerd. Mogelijke evaluatiemethoden zijn batch, synchronous (streaming) of continue (edge). Meer informatie over de evaluatiemethodes kan in het [&#x200B; segmentatieoverzicht &#x200B;](../home.md) worden gevonden |
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

U kunt een nieuw publiek tot stand brengen door een POST- verzoek aan het `/audiences` eindpunt te doen.

**API formaat**

```http
POST /audiences
```

**Verzoek**

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
        "profileInstanceId": "AEPSegments",
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
        ]
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- | 
| `name` | De naam van het publiek. |
| `description` | Een beschrijving van het publiek. |
| `type` | Een veld waarin wordt weergegeven of het publiek door het platform wordt gegenereerd of dat een extern gegenereerd publiek is. Mogelijke waarden zijn `SegmentDefinition` en `ExternalSegment` . Een `SegmentDefinition` verwijst naar een publiek dat is gegenereerd in Platform, terwijl een `ExternalSegment` verwijst naar een publiek dat niet is gegenereerd in Platform. |
| `expression` | De Profile Query Language (PQL)-expressie van het publiek. Meer informatie over de uitdrukkingen van PQL kan in de [&#x200B; uitdrukkingengids van PQL &#x200B;](../pql/overview.md) worden gevonden. |
| `schema` | Het schema van de Gegevens van de Ervaring Model (XDM) van het publiek. |
| `labels` | Gegevensgebruik op objectniveau en op kenmerk gebaseerde toegangsbeheerlabels die relevant zijn voor het publiek. |

+++

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met informatie over uw pas gecreeerd publiek terug.

+++Een voorbeeldreactie bij het maken van een publiek dat via een platform wordt gegenereerd.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
     "schema": {
      "name": "_xdm.context.profile"
    },
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

## Een bepaald publiek opzoeken {#get}

U kunt gedetailleerde informatie over een specifiek publiek opzoeken door een GET-aanvraag in te dienen bij het `/audiences` eindpunt en de id op te geven van het publiek dat u wilt ophalen in het aanvraagpad.

**API formaat**

```http
GET /audiences/{AUDIENCE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- | 
| `{AUDIENCE_ID}` | De id van het publiek dat u probeert op te halen. Gelieve te merken op dat dit het `id` gebied is, en **niet** het `audienceId` gebied is. |

**Verzoek**

+++Een voorbeeldverzoek om een publiek op te halen

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met informatie over het gespecificeerde publiek terug.

+++Een steekproefreactie wanneer het terugwinnen van een Platform-geproduceerd publiek.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
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

## Een publiek overschrijven {#put}

U kunt een specifiek publiek bijwerken (overschrijven) door een PUT-aanvraag in te dienen bij het `/audiences` -eindpunt en de id op te geven van het publiek dat u wilt bijwerken in het aanvraagpad.

**API formaat**

```http
PUT /audiences/{AUDIENCE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{AUDIENCE_ID}` | De id van het publiek dat u wilt bijwerken. Gelieve te merken op dat dit het `id` gebied is, en **niet** het `audienceId` gebied is. |

**Verzoek**

+++Een voorbeeldverzoek om een volledig publiek bij te werken.

```shell
curl -X PUT https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "audienceId": "test-platform-audience-id",
    "name": "New Platform audience",
    "namespace": "AEPSegments",
    "description": "Last 30 days",
    "type": "SegmentDefinition",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country=\"US\""
    }
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
| `type` | Een door het systeem gegenereerd veld dat weergeeft of het publiek door het platform wordt gegenereerd of dat een extern gegenereerd publiek is. Mogelijke waarden zijn `SegmentDefinition` en `ExternalSegment` . Een `SegmentDefinition` verwijst naar een publiek dat is gegenereerd in Experience Platform, terwijl een `ExternalSegment` verwijst naar een publiek dat niet is gegenereerd in Experience Platform. |
| `expression` | Een object dat de PQL-expressie van het publiek bevat. |
| `lifecycleState` | De status van het publiek. Mogelijke waarden zijn `draft` , `published` en `inactive` . `draft` vertegenwoordigt wanneer het publiek wordt gecreeerd, `published` wanneer het publiek wordt gepubliceerd, en `inactive` wanneer het publiek niet meer actief is. |
| `datasetId` | De id van de dataset die de publieksgegevens kunnen worden gevonden. |
| `labels` | Gegevensgebruik op objectniveau en op kenmerk gebaseerde toegangsbeheerlabels die relevant zijn voor het publiek. |

+++

**Reactie**

Een geslaagde reactie retourneert HTTP status 200 met details over uw onlangs bijgewerkte publiek. Houd er rekening mee dat de details van uw publiek verschillen, afhankelijk van het publiek dat via een Experience-Platform wordt gegenereerd of een publiek dat extern wordt gegenereerd.

+++Een voorbeeldreactie bij het bijwerken van een volledig publiek.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-platform-audience-id",
    "name": "New Experience Platform audience",
    "namespace": "AEPSegments",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "type": "SegmentDefinition",
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

## Een publiek bijwerken {#patch}

U kunt een specifiek publiek bijwerken door een PATCH-aanvraag in te dienen bij het `/audiences` -eindpunt en de id op te geven van het publiek dat u wilt bijwerken in het aanvraagpad.

**API formaat**

```http
PATCH /audiences/{AUDIENCE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{AUDIENCE_ID}` | De id van het publiek dat u wilt bijwerken. Gelieve te merken op dat dit het `id` gebied is, en **niet** het `audienceId` gebied is. |

**Verzoek**

+++ Een voorbeeldverzoek om een publiek bij te werken.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab5
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '[
    {
        "op": "add",
        "path": "/lifecycleState",
        "value": "inactive"
    }
 ]'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `op` | Het type uitgevoerde PATCH-bewerking. Voor dit eindpunt, is deze waarde **altijd** `/add`. |
| `path` | Het pad van het veld dat moet worden bijgewerkt. Systeem-geproduceerde gebieden, zoals `id`, `audienceId`, en `namespace` **kunnen niet** worden uitgegeven. |
| `value` | De nieuwe waarde die wordt toegewezen aan de eigenschap die is opgegeven in `path` . |

+++

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 met het bijgewerkte publiek.

+++Een voorbeeldreactie bij het patchen van een veld in een publiek.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab5",
    "audienceId": "test-platform-audience-id",
    "name": "New Experience Platform audience",
    "namespace": "AEPSegments",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "type": "SegmentDefinition",
    "lifecycleState": "inactive",
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

U kunt een specifiek publiek verwijderen door een DELETE-aanvraag in te dienen bij het `/audiences` -eindpunt en de id op te geven van het publiek dat u wilt verwijderen in het aanvraagpad.

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

U kunt meerdere soorten publiek ophalen door een POST-aanvraag in te dienen bij het `/audiences/bulk-get` -eindpunt en de id&#39;s op te geven van het publiek dat u wilt ophalen.

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

Na het lezen van deze handleiding hebt u nu een beter inzicht in hoe u publiek kunt maken, beheren en verwijderen met de Adobe Experience Platform API. Voor meer informatie over publieksbeheer die UI gebruiken, te lezen gelieve de [&#x200B; gids van de segmentatie UI &#x200B;](../ui/overview.md).
