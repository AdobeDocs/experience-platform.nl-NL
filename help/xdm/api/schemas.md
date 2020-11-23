---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;schema;Schema;schemas;Schemas;create
solution: Experience Platform
title: Een schema maken
description: Het /schemas eindpunt in de Registratie API van het Schema staat u toe om schema's XDM binnen uw ervaringstoepassing programmatically te beheren.
topic: developer guide
translation-type: tm+mt
source-git-commit: 0b55f18eabcf1d7c5c233234c59eb074b2670b93
workflow-type: tm+mt
source-wordcount: '1386'
ht-degree: 0%

---


# Schemas, eindpunt

Een schema kan worden beschouwd als de blauwdruk voor de gegevens die u in Adobe Experience Platform wilt opnemen. Elk schema bestaat uit een klasse en nul of meer mixen. Het `/schemas` eindpunt in [!DNL Schema Registry] API staat u toe om schema&#39;s binnen uw ervaringstoepassing programmatically te beheren.

## Aan de slag

Het API-eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Lees voordat u verdergaat de gids [Aan de](./getting-started.md) slag voor koppelingen naar gerelateerde documentatie, een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document en belangrijke informatie over vereiste headers die nodig zijn om aanroepen naar elke Experience Platform-API te kunnen uitvoeren.

## Een lijst met schema&#39;s ophalen {#list}

U kunt alle schema&#39;s onder de `global` container of de `tenant` container weergeven door een GET-aanvraag in te dienen bij `/global/schemas` of `/tenant/schemas`.

>[!NOTE]
>
>Bij het vermelden van bronnen, beperkt het resultaat van de Registratie van het Schema aan 300 punten. Om middelen voorbij deze grens terug te keren, moet u het pagineren parameters gebruiken. Men adviseert ook dat u extra vraagparameters gebruikt om resultaten te filtreren en het aantal teruggekeerde middelen te verminderen. Zie de sectie over [vraagparameters](./appendix.md#query) in het bijlage document voor meer informatie.

**API-indeling**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CONTAINER_ID}` | De container waarin de schema&#39;s zijn ondergebracht die u wilt ophalen: `global` voor schema&#39;s die met Adobe zijn gemaakt of `tenant` voor schema&#39;s die eigendom zijn van uw organisatie. |
| `{QUERY_PARAMS}` | Optionele queryparameters om resultaten te filteren op. Zie het [bijlage document](./appendix.md#query) voor een lijst van beschikbare parameters. |

**Verzoek**

Het volgende verzoek wint een lijst van schema&#39;s van de `tenant` container terug, gebruikend een `orderby` vraagparameter om de resultaten door hun `title` attribuut te sorteren.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

De antwoordindeling is afhankelijk van de `Accept` header die in de aanvraag wordt verzonden. De volgende `Accept` kopteksten zijn beschikbaar voor aanbiedingsschema&#39;s:

| `Accept` header | Beschrijving |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Retourneert een korte samenvatting van elke bron. Dit is de aanbevolen koptekst voor aanbiedingsbronnen. (Limiet: 300) |
| `application/vnd.adobe.xed+json` | Retourneert het volledige JSON-schema voor elke bron, met origineel `$ref` en `allOf` ingesloten. (Limiet: 300) |

**Antwoord**

In het bovenstaande verzoek werd de `application/vnd.adobe.xed-id+json` header gebruikt. Daarom bevat het antwoord alleen de kenmerken `Accept` , `title`, `$id`en `meta:altId``version` voor elk schema. Als u de andere `Accept` header (`application/vnd.adobe.xed+json`) gebruikt, worden alle kenmerken van elk schema geretourneerd. Selecteer de juiste `Accept` koptekst, afhankelijk van de informatie die u in uw reactie nodig hebt.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/0238be93d3e7a06aec5e0655955901ec",
      "meta:altId": "_{TENANT_ID}.schemas.0238be93d3e7a06aec5e0655955901ec",
      "version": "1.4",
      "title": "Hotels"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/0ef4ce0d390f0809fad490802f53d30b",
      "meta:altId": "_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b",
      "version": "1.0",
      "title": "Loyalty Members"
    }
  ],
  "_page": {
        "orderby": "title",
        "next": null,
        "count": 2
    },
    "_links": {
        "next": null,
        "global_schemas": {
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas"
        }
    }
}
```

## Een schema opzoeken {#lookup}

U kunt een specifiek schema opzoeken door een verzoek van de GET te doen dat identiteitskaart van het schema in de weg omvat.

**API-indeling**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CONTAINER_ID}` | De container waarin het schema is opgeslagen dat u wilt ophalen: `global` voor een Adobe-gecreeerd schema of `tenant` voor een schema dat door uw organisatie wordt bezeten. |
| `{SCHEMA_ID}` | De `meta:altId` URL of URL-gecodeerde `$id` van het schema dat u wilt opzoeken. |

**Verzoek**

Met het volgende verzoek wordt een schema opgehaald dat door de `meta:altId` waarde ervan in het pad wordt opgegeven.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

De antwoordindeling is afhankelijk van de `Accept` header die in de aanvraag wordt verzonden. Alle opzoekverzoeken vereisen een `version` item dat in de `Accept` koptekst moet worden opgenomen. The following `Accept` headers are available:

| `Accept` header | Beschrijving |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Ruwe met `$ref` en `allOf`, heeft titels en beschrijvingen. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` en `allOf` opgelost, heeft titels en beschrijvingen. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Onbewerkt met `$ref` en `allOf`, geen titels of beschrijvingen. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` en `allOf` opgelost, geen titels of beschrijvingen. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` en `allOf` opgelost, beschrijving inbegrepen. |

**Antwoord**

Een succesvolle reactie keert de details van het schema terug. Welke velden worden geretourneerd, is afhankelijk van de `Accept` header die in de aanvraag wordt verzonden. Experimenteer met verschillende `Accept` kopteksten om de reacties te vergelijken en te bepalen welke kopbal het beste voor uw gebruiksgeval is.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/20af3f1d4b175f27ba59529d1b51a0c79fc25df454117c80",
  "meta:altId": "_{TENANT_ID}.schemas.20af3f1d4b175f27ba59529d1b51a0c79fc25df454117c80",
  "meta:resourceType": "schemas",
  "version": "1.1",
  "title": "Example schema",
  "type": "object",
  "description": "An example schema created within the tenant container.",
  "allOf": [
      {
          "$ref": "https://ns.adobe.com/xdm/context/profile",
          "type": "object",
          "meta:xdmType": "object"
      },
      {
          "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/443fe51457047d958f4a97853e64e0eca93ef34d7990583b",
          "type": "object",
          "meta:xdmType": "object"
      }
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
      "https://ns.adobe.com/{TENANT_ID}/mixins/443fe51457047d958f4a97853e64e0eca93ef34d7990583b",
      "https://ns.adobe.com/xdm/common/auditable",
      "https://ns.adobe.com/xdm/data/record",
      "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
      "repo:createdDate": 1602872911226,
      "repo:lastModifiedDate": 1603381419889,
      "xdm:createdClientId": "{CLIENT_ID}",
      "xdm:lastModifiedClientId": "{CLIENT_ID}",
      "xdm:createdUserId": "{USER_ID}",
      "xdm:lastModifiedUserId": "{USER_ID}",
      "eTag": "84b4da79b7445a4bf1c59269e718065effddb983c492f48e223d49c049c6d589",
      "meta:globalLibVersion": "1.15.4"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Een schema maken {#create}

Het proces van de schemacompositie begint door een klasse toe te wijzen. De klasse definieert de belangrijkste gedragsaspecten van de gegevens (record- of tijdreeks) en de minimale velden die vereist zijn om de gegevens te beschrijven die worden ingevoerd.

>[!NOTE]
>
>De voorbeeldvraag hieronder is slechts een basislijnvoorbeeld van hoe te om een schema in API, met de minimale samenstellingsvereisten van een klasse en geen mengen tot stand te brengen. Voor volledige stappen op hoe te om een schema in API tot stand te brengen, met inbegrip van hoe te om gebieden toe te wijzen gebruikend mengen en gegevenstypes, zie de [schemaverwezenlijking zelfstudie](../tutorials/create-schema-api.md).

**API-indeling**

```http
POST /tenant/schemas
```

**Verzoek**

De aanvraag moet een `allOf` attribuut bevatten dat naar de klasse `$id` van verwijst. Dit attribuut bepaalt de &quot;basisklasse&quot;die het schema zal uitvoeren. In dit voorbeeld is de basisklasse een klasse &quot;Eigenschapinformatie&quot; die eerder is gemaakt.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Information",
        "description": "Property-related information.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590" 
          } 
        ]
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `allOf` | Een array van objecten, waarbij elk object verwijst naar een klasse of combinatie waarvan het schema velden implementeert. Elk object bevat één eigenschap (`$ref`) waarvan de waarde de waarde vertegenwoordigt `$id` van de klasse of de mix in het nieuwe schema wordt geïmplementeerd. Er moet één klasse worden aangeboden met nul of meer extra mengsels. In het bovenstaande voorbeeld is het ene object in de `allOf` array de klasse van het schema. |

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 (Gemaakt) en een payload die de details bevat van het nieuwe schema, inclusief het schema `$id`, `meta:altId`en `version`. Deze waarden zijn alleen-lezen en worden toegewezen door de [!DNL Schema Registry]operator.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088461236,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

Het uitvoeren van een verzoek van de GET om van alle schema&#39;s [in de huurderscontainer een lijst te](#list) maken zou nu het nieuwe schema omvatten. U kunt een [opzoekverzoek](#lookup) (GET) uitvoeren gebruikend URL-Gecodeerde `$id` URI om het nieuwe schema direct te bekijken.

Als u aanvullende velden aan een schema wilt toevoegen, kunt u een [PATCH-bewerking](#patch) uitvoeren om mixins toe te voegen aan de `allOf` en `meta:extends` arrays van het schema.

## Een schema bijwerken {#put}

U kunt een volledig schema door een verrichting van de PUT vervangen, hoofdzakelijk herschrijvend het middel. Wanneer het bijwerken van een schema door een verzoek van de PUT, moet het lichaam alle gebieden omvatten die wanneer het [creëren van een nieuw schema](#create) in een verzoek van de POST worden vereist.

>[!NOTE]
>
>Als u slechts een deel van een schema wilt bijwerken in plaats van het volledig te vervangen, zie de sectie bij het [bijwerken van een gedeelte van een schema](#patch).

**API-indeling**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | De `meta:altId` URL of URL-gecodeerde `$id` van het schema dat u wilt herschrijven. |

**Verzoek**

Het volgende verzoek vervangt een bestaand schema, veranderend zijn `title`, `description`, en `allOf` attributen.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Commercial Property Information",
        "description": "Information related to commercial properties.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7" 
          } 
        ]
      }'
```

**Antwoord**

Een succesvolle reactie keert de details van het bijgewerkte schema terug.

```JSON
{
    "title":"Commercial Property Information",
    "description": "Information related to commercial properties.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
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

## Een gedeelte van een schema bijwerken {#patch}

U kunt een gedeelte van een schema bijwerken door een verzoek van PATCH te gebruiken. De [!DNL Schema Registry] functie ondersteunt alle standaard JSON-patchbewerkingen, inclusief `add`, `remove`en `replace`. Zie de handleiding [voor](../../landing/api-fundamentals.md#json-patch)API-basisbeginselen voor meer informatie over JSON Patch.

>[!NOTE]
>
>Als u een volledige bron wilt vervangen door nieuwe waarden in plaats van afzonderlijke velden bij te werken, raadpleegt u de sectie over het [vervangen van een schema met behulp van een PUT-bewerking](#put).

Één van de gemeenschappelijkste verrichtingen van de PATCH impliceert het toevoegen van eerder bepaalde mengelingen aan een schema, zoals aangetoond in het hieronder voorbeeld.

**API-indeling**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` het schema dat u wilt bijwerken. |

**Verzoek**

In de onderstaande voorbeeldaanvraag wordt een nieuwe mix toegevoegd aan een schema door de `$id` waarde van die mix toe te voegen aan zowel de `meta:extends` als de `allOf` arrays.

De aanvraaginstantie heeft de vorm van een array, waarbij elk vermeld object een specifieke wijziging in een afzonderlijk veld vertegenwoordigt. Elk object bevat de uit te voeren bewerking (`op`), in welk veld de bewerking moet worden uitgevoerd (`path`) en welke informatie in die bewerking moet worden opgenomen (`value`).

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { 
          "op": "add",
          "path": "/meta:extends/-",
          "value":  "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        },
        {
          "op": "add",
          "path": "/allOf/-",
          "value":  {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
          }
        }
      ]'
```

**Antwoord**

De reactie toont aan dat beide bewerkingen met succes zijn uitgevoerd. De mix `$id` is toegevoegd aan de `meta:extends` array en er wordt`$ref`nu een verwijzing ( `$id` ) naar de mix in de `allOf` array weergegeven.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088649634,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Een schema inschakelen voor gebruik in realtime klantprofiel {#union}

Als een schema aan het Profiel [van de Klant in](../../profile/home.md)real time moet deelnemen, moet u een `union` markering aan de `meta:immutableTags` serie van het schema toevoegen. U kunt dit bereiken door een PATCH-verzoek voor het desbetreffende schema in te dienen.

>[!IMPORTANT]
>
>Onveranderbare tags zijn tags die zijn bedoeld om te worden ingesteld, maar die nooit worden verwijderd.

**API-indeling**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` het schema dat u wilt inschakelen. |

**Verzoek**

In de onderstaande voorbeeldaanvraag wordt een `meta:immutableTags` `union` array toegevoegd aan een bestaand schema, zodat de array een enkele tekenreekswaarde heeft om deze in te schakelen voor gebruik in Profiel.

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "add",
          "path": "/meta:immutableTags",
          "value": ["union"]
        }
      ]'
```

**Antwoord**

Een succesvol antwoord keert de details van het bijgewerkte schema terug, die tonen dat de `meta:immutableTags` serie is toegevoegd.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088649634,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    },
    "meta:immutableTags": [
      "union"
    ]
}
```

U kunt nu de samenvoeging voor de klasse van dit schema bekijken om te bevestigen dat de gebieden van het schema worden vertegenwoordigd. Zie de gids [van het](./unions.md) vakbondseindpunt voor meer informatie.

## Schema verwijderen {#delete}

Het kan soms noodzakelijk zijn om een schema uit de Registratie van het Schema te verwijderen. Dit wordt gedaan door een verzoek van de DELETE met schema identiteitskaart uit te voeren die in de weg wordt verstrekt.

**API-indeling**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` het schema dat u wilt verwijderen. |

**Verzoek**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst.

U kunt de schrapping bevestigen door een raadpleging (GET) verzoek aan het schema te proberen. U zult een `Accept` kopbal in het verzoek moeten omvatten, maar zou een status 404 van HTTP (niet Gevonden) moeten ontvangen omdat het schema uit de Registratie van het Schema is verwijderd.