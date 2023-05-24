---
title: Specifieke velden toevoegen aan een schema met de API voor het schemaregister
description: Leer hoe u afzonderlijke velden van reeds bestaande veldgroepen toevoegt aan een XDM-schema (Experience Data Model) met behulp van de Schemaregistratie-API.
exl-id: 696cce2b-bbde-416a-9f52-12ab4da9c2c6
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 1%

---

# Specifieke velden aan een schema toevoegen met de API voor het schemaregister

De schema&#39;s van het Gegevensmodel van de ervaring (XDM) zijn samengesteld uit een basisklasse, met extra gebieden inbegrepen door het gebruik van standaardgebiedsgroepen die door Adobe en de groepen van het douanegebied worden bepaald door uw organisatie.

Wanneer u een schema samenstelt, wilt u wellicht bepaalde velden uit een bepaalde veldgroep gebruiken, terwijl u andere wilt uitsluiten van dezelfde groep die u niet nodig hebt. Deze zelfstudie laat zien hoe u afzonderlijke velden van een veldgroep kunt toevoegen aan een schema met behulp van de API voor schemaregistratie.

>[!NOTE]
>
>Zie de handleiding voor informatie over het toevoegen en verwijderen van afzonderlijke schemavelden in de gebruikersinterface van Adobe Experience Platform [werkstromen op basis van velden](../ui/field-based-workflows.md) (momenteel in bèta).

## Vereisten

Dit leerprogramma impliceert het maken van vraag aan [Schema-register-API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Controleer voordat u begint de [ontwikkelaarsgids](../api/getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van uw `{TENANT_ID}`, het concept containers en de vereiste kopteksten voor het indienen van verzoeken.

## De `meta:refProperty` field

Voor een bepaald schema wordt onder het desbetreffende schema verwezen naar de klasse- en veldgroepen waaruit de structuur bestaat `allOf` array. Elke component wordt vertegenwoordigd als een object dat een `$ref` eigenschap die verwijst naar de URI van de component `$id`.

De volgende JSON vertegenwoordigt een vereenvoudigd schema dat één klasse gebruikt (`experienceevent`) en veldgroep (`experienceevent-all`):

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

Voor elk object in het dialoogvenster `allOf` array die verwijst naar een veldgroep, kunt u een item op hetzelfde niveau toevoegen `meta:refProperty` veld om aan te geven welke velden in de groep in het schema moeten worden opgenomen.

>[!NOTE]
>
>Elk veld wordt opgegeven met een JSON-aanwijzertekenreeks die het pad vertegenwoordigt naar het veld binnen de desbetreffende veldgroep. De tekenreeks moet beginnen met een slash (`/`) en mag geen `properties` naamruimten. Bijvoorbeeld: `/_experience/campaign/message/id`.

Indien opgenomen als een tekenreeks `meta:refProperty` kan verwijzen naar één veld in een groep. Andere velden van dezelfde groep kunnen worden opgenomen door dezelfde groep te gebruiken `$ref` waarde in een ander object met een andere waarde `meta:refProperty` waarde.

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

Alternatief, `meta:refProperty` kan worden opgegeven als een array, zodat u meerdere velden kunt opgeven die u wilt opnemen vanuit een bepaalde groep binnen één groep `allOf` lijstitem:

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

## Velden toevoegen met een PUT

U kunt een verzoek van de PUT gebruiken om een volledig schema te herschrijven en de gebieden te vormen u onder wilt omvatten `allOf`.

**API-indeling**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | De `meta:altId` of URL-gecodeerd `$id` van het schema dat u wilt herschrijven. |

**Verzoek**

Met het volgende verzoek worden de specifieke velden bijgewerkt die zijn opgenomen in de veldgroep onder de `allOf` array.

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

**Antwoord**

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
>Voor meer gedetailleerde informatie over de verzoeken van de PUT om schema&#39;s, verwijs naar [schema&#39;s eindpuntgids](../api/schemas.md#put).

## Velden toevoegen met een PATCH-bewerking

U kunt een PATCH-verzoek gebruiken om afzonderlijke velden aan een schema toe te voegen zonder andere velden te overschrijven. Het schemaregister ondersteunt alle standaard JSON-patchbewerkingen, inclusief `add`, `remove`, en `replace`. Voor meer informatie over JSON Patch raadpleegt u de [Handleiding voor API-basisbeginselen](../../landing/api-fundamentals.md#json-patch).

**API-indeling**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | De `meta:altId` of URL-gecodeerd `$id` van het schema dat u wilt herschrijven. |

**Verzoek**

Met de volgende aanvraag wordt een nieuw object toegevoegd aan het schema `allOf` array, velden opgeven die moeten worden toegevoegd.

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

**Antwoord**

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
>Voor meer gedetailleerde informatie over de verzoeken van PATCH om schema&#39;s, verwijs naar [schema&#39;s eindpuntgids](../api/schemas.md#patch).

## Volgende stappen

Deze gids besprak hoe te om API vraag te gebruiken om individuele gebieden van een bestaande gebiedsgroep aan een schema toe te voegen. Voor details over hoe te om gelijkaardige op gebied-gebaseerde taken in de UI van het Platform uit te voeren, zie de gids op [werkstromen op basis van velden](../ui/field-based-workflows.md).

Raadpleeg voor meer informatie over de mogelijkheden van de Schema Registry API de [API-overzicht](../api/overview.md) voor een volledige lijst van eindpunten en processen.
