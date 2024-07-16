---
title: Specifieke velden toevoegen aan een schema met de API voor het schemaregister
description: Leer hoe u afzonderlijke velden van reeds bestaande veldgroepen toevoegt aan een XDM-schema (Experience Data Model) met behulp van de Schemaregistratie-API.
exl-id: 696cce2b-bbde-416a-9f52-12ab4da9c2c6
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---

# Specifieke velden aan een schema toevoegen met de API voor het schemaregister

De schema&#39;s van het Gegevensmodel van de ervaring (XDM) zijn samengesteld uit een basisklasse, met extra gebieden inbegrepen door het gebruik van standaardgebiedsgroepen die door Adobe en de groepen van het douanegebied worden bepaald door uw organisatie.

Wanneer u een schema samenstelt, wilt u wellicht bepaalde velden uit een bepaalde veldgroep gebruiken, terwijl u andere wilt uitsluiten van dezelfde groep die u niet nodig hebt. Deze zelfstudie laat zien hoe u afzonderlijke velden van een veldgroep kunt toevoegen aan een schema met behulp van de API voor schemaregistratie.

>[!NOTE]
>
>Voor informatie over hoe te om individuele schemagebieden in Adobe Experience Platform toe te voegen en te verwijderen UI, zie de gids op [ op gebied-gebaseerde werkschema&#39;s ](../ui/field-based-workflows.md) (momenteel in bèta).

## Vereisten

Dit leerprogramma impliceert het maken van vraag aan de [ Registratie API van het Schema ](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Alvorens te beginnen, te herzien gelieve de [ ontwikkelaarsgids ](../api/getting-started.md) voor belangrijke informatie die u moet kennen om met succes vraag aan API, met inbegrip van uw `{TENANT_ID}`, het concept containers, en de vereiste kopballen te maken om verzoeken te doen.

## Het veld `meta:refProperty`

Voor elk schema wordt naar de klasse- en veldgroepen die de structuur ervan vormen verwezen onder de array `allOf` . Elke component wordt vertegenwoordigd als een object dat een eigenschap `$ref` bevat die naar de URI van de component `$id` verwijst.

De volgende JSON vertegenwoordigt een vereenvoudigd schema dat één enkele klasse (`experienceevent`) en gebiedsgroep (`experienceevent-all`) gebruikt:

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all"
    }
  ]
}
```

Voor elk object in de array `allOf` dat verwijst naar een veldgroep, kunt u een verwant `meta:refProperty` -veld toevoegen om op te geven welke velden in de groep moeten worden opgenomen in het schema.

>[!NOTE]
>
>Elk veld wordt opgegeven met een JSON-aanwijzertekenreeks die het pad vertegenwoordigt naar het veld binnen de desbetreffende veldgroep. De tekenreeks moet beginnen met een slash (`/`) en mag geen naamruimten van het type `properties` bevatten. Bijvoorbeeld: `/_experience/campaign/message/id` .

Wanneer `meta:refProperty` wordt opgenomen als een tekenreeks, kan het verwijzen naar één veld in een groep. Andere velden van dezelfde groep kunnen worden opgenomen door dezelfde `$ref` -waarde te gebruiken in een ander object met een andere `meta:refProperty` -waarde.

```json
{
  "title": "My Sample Schema",
  "description": "An example schema that uses the XDM ExperienceEvent class.",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": "/_experience/campaign/message/id"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": "/_experience/campaign/message/size"
    }
  ]
}
```

U kunt `meta:refProperty` ook als een array opgeven, zodat u meerdere velden kunt opgeven die vanuit een bepaalde groep in één `allOf` -lijstitem moeten worden opgenomen:

```json
{
  "title": "My Sample Schema",
  "description": "An example schema that uses the XDM ExperienceEvent class.",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ]
}
```

## Velden toevoegen met behulp van een PUT

U kunt een verzoek van de PUT gebruiken om een volledig schema te herschrijven en de gebieden te vormen u onder `allOf` wilt omvatten.

**API formaat**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | De `meta:altId` of URL-gecodeerde `$id` van het schema dat u wilt herschrijven. |

**Verzoek**

Met de volgende aanvraag worden de specifieke velden bijgewerkt die zijn opgenomen in de veldgroep onder de array `allOf` .

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "title": "My Sample Schema",
        "description": "My Sample Description",
        "type": "object",
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
          },
          {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
            "meta:refProperty": [
              "/_experience/campaign/message/id",
              "/_experience/campaign/message/size",
              "/_experience/campaign/message/variant"
            ]
          }
        ]
      }'
```

**Reactie**

Een succesvolle reactie keert de details van het bijgewerkte schema terug.

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ],
  "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
  "meta:abstract": false,
  "meta:extensible": false,
  "meta:extends": [
      "https://ns.adobe.com/xdm/context/experienceevent",
      "https://ns.adobe.com/xdm/data/time-series"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{ORG_ID}",
  "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
  "version": "1.0",
  "meta:resourceType": "schemas",
  "meta:registryMetadata": {
      "repo:createDate": 1552088461236,
      "repo:lastModifiedDate": 1552088470592,
      "xdm:createdClientId": "{CREATED_CLIENT}",
      "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

>[!NOTE]
>
>Voor meer gedetailleerde informatie over de verzoeken van de PUT om schema&#39;s, verwijs naar de [ gids van het schemaeindpunt ](../api/schemas.md#put).

## Velden toevoegen met een PATCH-bewerking

U kunt een PATCH-verzoek gebruiken om afzonderlijke velden aan een schema toe te voegen zonder andere velden te overschrijven. Het schema-register ondersteunt alle standaard JSON-patchbewerkingen, inclusief `add` , `remove` en `replace` . Voor meer informatie over Reparatie JSON, zie de [ API fundamentals gids ](../../landing/api-fundamentals.md#json-patch).

**API formaat**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | De `meta:altId` of URL-gecodeerde `$id` van het schema dat u wilt herschrijven. |

**Verzoek**

Met de volgende aanvraag wordt een nieuw object toegevoegd aan de array `allOf` van het schema en worden velden opgegeven die moeten worden toegevoegd.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "op": "add",
          "path": "/allOf/-",
          "value":  {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
            "meta:refProperty": [
              "/_experience/campaign/message/id",
              "/_experience/campaign/message/size",
              "/_experience/campaign/message/variant"
            ]
          }
        }
      ]'
```

**Reactie**

Een succesvolle reactie keert de details van het bijgewerkte schema terug.

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ],
  "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
  "meta:abstract": false,
  "meta:extensible": false,
  "meta:extends": [
      "https://ns.adobe.com/xdm/context/experienceevent",
      "https://ns.adobe.com/xdm/data/time-series"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{ORG_ID}",
  "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
  "version": "1.0",
  "meta:resourceType": "schemas",
  "meta:registryMetadata": {
      "repo:createDate": 1552088461236,
      "repo:lastModifiedDate": 1552088470592,
      "xdm:createdClientId": "{CREATED_CLIENT}",
      "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

>[!NOTE]
>
>Voor meer gedetailleerde informatie over PATCH verzoeken om schema&#39;s, verwijs naar de [ gids van het schemaeindpunt ](../api/schemas.md#patch).

## Volgende stappen

Deze gids besprak hoe te om API vraag te gebruiken om individuele gebieden van een bestaande gebiedsgroep aan een schema toe te voegen. Voor details op hoe te om gelijkaardige op gebied-gebaseerde taken in het Platform UI uit te voeren, zie de gids op [ op gebied-gebaseerde werkschema&#39;s ](../ui/field-based-workflows.md).

Voor meer informatie over de mogelijkheden van de Registratie API van het Schema, verwijs naar het [ API overzicht ](../api/overview.md) voor een volledige lijst van eindpunten en processen.
