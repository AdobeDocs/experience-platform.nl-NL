---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;Experience gegevensmodel;Experience Data Model;Gegevensmodel;Gegevensmodel;Schema register;Schema Register;Schema;Schema;schema's;Schema's;Maken
solution: Experience Platform
title: Schemas API Endpoint
description: Het /schemas eindpunt in de Registratie API van het Schema staat u toe om schema's XDM binnen uw ervaringstoepassing programmatically te beheren.
topic-legacy: developer guide
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1454'
ht-degree: 0%

---

# Schemas, eindpunt

Een schema kan worden beschouwd als de blauwdruk voor de gegevens die u in Adobe Experience Platform wilt invoeren. Elk schema bestaat uit een klasse en nul of meer groepen schemavelden. De `/schemas` in de [!DNL Schema Registry] Met API kunt u schema&#39;s programmatisch beheren binnen uw ervaringstoepassing.

## Aan de slag

Het API-eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van het [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Controleer voordat je doorgaat de [gids Aan de slag](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan lezing de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om met succes vraag aan om het even welk Experience Platform API te maken.

## Een lijst met schema&#39;s ophalen {#list}

U kunt alle schema&#39;s weergeven onder de `global` of `tenant` container door een GET-aanvraag in te dienen bij `/global/schemas` of `/tenant/schemas`, respectievelijk.

>[!NOTE]
>
>Bij het vermelden van bronnen, beperkt het resultaat van de Registratie van het Schema aan 300 punten. Om middelen voorbij deze grens terug te keren, moet u het pagineren parameters gebruiken. Men adviseert ook dat u extra vraagparameters gebruikt om resultaten te filtreren en het aantal teruggekeerde middelen te verminderen. Zie de sectie over [queryparameters](./appendix.md#query) voor meer informatie.

**API-indeling**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CONTAINER_ID}` | De container waarin de schema&#39;s zijn ondergebracht die u wilt ophalen: `global` voor door Adobe gemaakte schema&#39;s of `tenant` voor schema&#39;s die eigendom zijn van uw organisatie. |
| `{QUERY_PARAMS}` | Optionele queryparameters om resultaten te filteren op. Zie de [bijgevoegd document](./appendix.md#query) voor een lijst met beschikbare parameters. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

Het volgende verzoek wint een lijst van schema&#39;s van terug `tenant` container gebruiken `orderby` query-parameter om de resultaten op hun te sorteren `title` kenmerk.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

De responsindeling is afhankelijk van `Accept` in de aanvraag verzonden. Het volgende `Accept` Kopteksten zijn beschikbaar voor aanbiedingsschema&#39;s:

| `Accept` header | Beschrijving |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Retourneert een korte samenvatting van elke bron. Dit is de aanbevolen koptekst voor aanbiedingsbronnen. (Limiet: 300) |
| `application/vnd.adobe.xed+json` | Retourneert het volledige JSON-schema voor elke bron, met het origineel `$ref` en `allOf` opgenomen. (Limiet: 300) |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

In bovengenoemd verzoek werd gebruikgemaakt van de `application/vnd.adobe.xed-id+json` `Accept` header, daarom bevat de reactie alleen de `title`, `$id`, `meta:altId`, en `version` kenmerken voor elk schema. Het andere gebruiken `Accept` header (`application/vnd.adobe.xed+json`) retourneert alle kenmerken van elk schema. Selecteer de juiste `Accept` afhankelijk van de informatie die u in uw reactie nodig hebt.

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
| `{CONTAINER_ID}` | De container waarin het schema is opgeslagen dat u wilt ophalen: `global` voor een door Adobe gemaakt schema of `tenant` voor een schema dat eigendom is van uw organisatie. |
| `{SCHEMA_ID}` | De `meta:altId` of URL-gecodeerd `$id` van het schema dat u wilt opzoeken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

Het volgende verzoek wint een schema terug dat door zijn wordt gespecificeerd `meta:altId` waarde in het pad.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

De responsindeling is afhankelijk van `Accept` in de aanvraag verzonden. Alle opzoekverzoeken vereisen een `version` worden opgenomen in de `Accept` header. Het volgende `Accept` Kopteksten zijn beschikbaar:

| `Accept` header | Beschrijving |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Onbewerkt met `$ref` en `allOf`, heeft titels en beschrijvingen. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` en `allOf` heeft titels en beschrijvingen. |
| `application/vnd.adobe.xed-notext+json; version=1` | Onbewerkt met `$ref` en `allOf`, geen titels of beschrijvingen. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` en `allOf` opgelost, geen titels of beschrijvingen. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` en `allOf` opgelost, beschrijving inbegrepen. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een succesvolle reactie keert de details van het schema terug. De geretourneerde velden zijn afhankelijk van de `Accept` in de aanvraag verzonden. Experimenteer met andere `Accept` Kopteksten om de reacties te vergelijken en te bepalen welke kopbal het beste voor uw gebruiksgeval is.

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
  "imsOrg": "{ORG_ID}",
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
>De voorbeeldaanroep hieronder is slechts een basislijnvoorbeeld van hoe u een schema in de API maakt, met de minimale compositievereisten van een klasse en geen veldgroepen. Voor volledige stappen over hoe te om een schema in API tot stand te brengen, met inbegrip van hoe te om gebieden toe te wijzen die gebiedsgroepen en gegevenstypes gebruiken, zie [zelfstudie over het maken van schema&#39;s](../tutorials/create-schema-api.md).

**API-indeling**

```http
POST /tenant/schemas
```

**Verzoek**

Het verzoek moet een `allOf` kenmerk dat verwijst naar het `$id` van een klasse. Dit attribuut bepaalt de &quot;basisklasse&quot;die het schema zal uitvoeren. In dit voorbeeld is de basisklasse een klasse &quot;Eigenschapinformatie&quot; die eerder is gemaakt.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `allOf` | Een array van objecten, waarbij elk object verwijst naar een klasse of veldgroep waarvan de velden door het schema worden geïmplementeerd. Elk object bevat één eigenschap (`$ref`) waarvan de waarde de `$id` van de klasse of de gebiedsgroep zal het nieuwe schema uitvoeren. Er moet één klasse worden opgegeven, met nul of meer extra veldgroepen. In het bovenstaande voorbeeld wordt het ene object in het dialoogvenster `allOf` array is de klasse van het schema. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 (Gemaakt) en een payload die de details bevat van het nieuwe schema, inclusief de `$id`, `meta:altId`, en `version`. Deze waarden zijn alleen-lezen en worden toegewezen door de [!DNL Schema Registry].

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
    "imsOrg": "{ORG_ID}",
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

Een GET-aanvraag uitvoeren op [lijst alle schema&#39;s](#list) in de huurderscontainer zou nu het nieuwe schema omvatten. U kunt een [opzoekverzoek (GET)](#lookup) URL-gecodeerd gebruiken `$id` URI om het nieuwe schema direct te bekijken.

Als u aanvullende velden aan een schema wilt toevoegen, kunt u een [PATCH-bewerking](#patch) om veldgroepen toe te voegen aan de schema&#39;s `allOf` en `meta:extends` arrays.

## Een schema bijwerken {#put}

U kunt een volledig schema door een verrichting van de PUT vervangen, hoofdzakelijk herschrijvend het middel. Wanneer het bijwerken van een schema door een verzoek van de PUT, moet het lichaam alle gebieden omvatten die wanneer zouden worden vereist [een nieuw schema maken](#create) in een verzoek van de POST.

>[!NOTE]
>
>Als u slechts een deel van een schema wilt bijwerken in plaats van het volledig te vervangen, zie de sectie op [het bijwerken van een gedeelte van een schema](#patch).

**API-indeling**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | De `meta:altId` of URL-gecodeerd `$id` van het schema dat u opnieuw wilt schrijven. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

Het volgende verzoek vervangt een bestaand schema, veranderend zijn `title`, `description`, en `allOf` kenmerken.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

## Een gedeelte van een schema bijwerken {#patch}

U kunt een gedeelte van een schema bijwerken door een verzoek van PATCH te gebruiken. De [!DNL Schema Registry] ondersteunt alle standaard JSON-patchbewerkingen, inclusief `add`, `remove`, en `replace`. Voor meer informatie over JSON Patch raadpleegt u de [Handleiding voor API-basisbeginselen](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Als u een volledige bron wilt vervangen door nieuwe waarden in plaats van afzonderlijke velden bij te werken, raadpleegt u de sectie over [het vervangen van een schema gebruikend een verrichting van de PUT](#put).

Een van de meest gangbare PATCH-bewerkingen bestaat uit het toevoegen van eerder gedefinieerde veldgroepen aan een schema, zoals in het onderstaande voorbeeld wordt getoond.

**API-indeling**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | URL-gecodeerd `$id` URI of `meta:altId` van het schema dat u wilt bijwerken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

In de onderstaande voorbeeldaanvraag wordt een nieuwe veldgroep aan een schema toegevoegd door de naam van die veldgroep toe te voegen `$id` waarde voor beide `meta:extends` en `allOf` arrays.

De aanvraaginstantie heeft de vorm van een array, waarbij elk vermeld object een specifieke wijziging in een afzonderlijk veld vertegenwoordigt. Elk object bevat de uit te voeren bewerking (`op`), welk veld de bewerking moet worden uitgevoerd (`path`) en welke informatie in die operatie moet worden opgenomen (`value`).

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

De reactie toont aan dat beide bewerkingen met succes zijn uitgevoerd. De veldgroep `$id` is toegevoegd aan de `meta:extends` array en een verwijzing (`$ref`) aan de veldgroep `$id` wordt nu weergegeven in het dialoogvenster `allOf` array.

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
    "imsOrg": "{ORG_ID}",
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

Om aan een schema deel te nemen [Klantprofiel in realtime](../../profile/home.md), moet u een `union` tag toevoegen aan schema&#39;s `meta:immutableTags` array. U kunt dit bereiken door een PATCH-verzoek voor het desbetreffende schema in te dienen.

>[!IMPORTANT]
>
>Onveranderbare tags zijn tags die zijn bedoeld om te worden ingesteld, maar die nooit worden verwijderd.

**API-indeling**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | URL-gecodeerd `$id` URI of `meta:altId` van het schema dat u wilt inschakelen. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

De onderstaande voorbeeldaanvraag voegt een `meta:immutableTags` array naar een bestaand schema, waarbij de array een enkele tekenreekswaarde krijgt van `union` om deze in te schakelen voor gebruik in Profiel.

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Een succesvol antwoord keert de details van het bijgewerkte schema terug, die tonen dat `meta:immutableTags` array is toegevoegd.

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
    "imsOrg": "{ORG_ID}",
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

U kunt nu de samenvoeging voor de klasse van dit schema bekijken om te bevestigen dat de gebieden van het schema worden vertegenwoordigd. Zie de [Punthandleiding voor vakbonden](./unions.md) voor meer informatie .

## Schema verwijderen {#delete}

Het kan soms noodzakelijk zijn om een schema uit de Registratie van het Schema te verwijderen. Dit wordt gedaan door een verzoek van de DELETE met schema identiteitskaart uit te voeren die in de weg wordt verstrekt.

**API-indeling**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | URL-gecodeerd `$id` URI of `meta:altId` van het schema dat u wilt verwijderen. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst.

U kunt de schrapping bevestigen door een raadpleging (GET) verzoek aan het schema te proberen. U moet een `Accept` header in the request, but should receive an HTTP status 404 (Not Found) because the schema has been removed from the Schema Registry.
