---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM-systeem;ervaringsgegevensmodel;Experience gegevensmodel;Experience Data Model;Gegevensmodel;Gegevensmodel;Schema register;Schema Register;Schema;Schema;Schema's;Schemas;create
solution: Experience Platform
title: Schemas API Endpoint
description: Het /schemas eindpunt in de Registratie API van het Schema staat u toe om schema's XDM binnen uw ervaringstoepassing programmatically te beheren.
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
source-git-commit: 491588dab1388755176b5e00f9d8ae3e49b7f856
workflow-type: tm+mt
source-wordcount: '2091'
ht-degree: 0%

---

# Schemas, eindpunt

Een schema kan worden beschouwd als de blauwdruk voor de gegevens die u in Adobe Experience Platform wilt invoeren. Elk schema bestaat uit een klasse en nul of meer groepen schemavelden. Met het eindpunt `/schemas` in de [!DNL Schema Registry] API kunt u schema&#39;s programmatisch beheren binnen uw ervaringstoepassing.

## Aan de slag

Het API eindpunt dat in deze gids wordt gebruikt maakt deel uit van [[!DNL Schema Registry]  API ](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welke Experience Platform API met succes te maken.

## Een lijst met schema&#39;s ophalen {#list}

U kunt alle schema&#39;s weergeven onder de container `global` of `tenant` door een GET-aanvraag in te dienen bij respectievelijk `/global/schemas` of `/tenant/schemas` .

>[!NOTE]
>
>Bij het vermelden van bronnen, beperkt het resultaat van de Registratie van het Schema aan 300 punten. Om middelen voorbij deze grens terug te keren, moet u het pagineren parameters gebruiken. Men adviseert ook dat u extra vraagparameters gebruikt om resultaten te filtreren en het aantal teruggekeerde middelen te verminderen. Zie de sectie over [ vraagparameters ](./appendix.md#query) in het bijlage document voor meer informatie.

**API formaat**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CONTAINER_ID}` | De container waarin de schema&#39;s zijn opgeslagen die u wilt ophalen: `global` voor door Adobe gemaakte schema&#39;s of `tenant` voor schema&#39;s die eigendom zijn van uw organisatie. |
| `{QUERY_PARAMS}` | Optionele queryparameters om resultaten te filteren op. Zie het [ bijlage document ](./appendix.md#query) voor een lijst van beschikbare parameters. |

{style="table-layout:auto"}

**Verzoek**

Met de volgende aanvraag wordt een lijst met schema&#39;s opgehaald uit de container `tenant` . Hierbij wordt een `orderby` query-parameter gebruikt om de resultaten op hun `title` -kenmerk te sorteren.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

De antwoordindeling is afhankelijk van de header `Accept` die in de aanvraag wordt verzonden. De volgende `Accept` kopteksten zijn beschikbaar voor aanbiedingsschema&#39;s:

| `Accept` header | Beschrijving |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Retourneert een korte samenvatting van elke bron. Dit is de aanbevolen koptekst voor aanbiedingsbronnen. (Limiet: 300) |
| `application/vnd.adobe.xed+json` | Retourneert het volledige JSON-schema voor elke bron, met origineel `$ref` en `allOf` inbegrepen. (Limiet: 300) |

{style="table-layout:auto"}

**Reactie**

In de bovenstaande aanvraag is de header `application/vnd.adobe.xed-id+json` `Accept` gebruikt en daarom bevat het antwoord alleen de kenmerken `title` , `$id` , `meta:altId` en `version` voor elk schema. Als u de andere `Accept` header (`application/vnd.adobe.xed+json` ) gebruikt, worden alle kenmerken van elk schema geretourneerd. Selecteer de juiste `Accept` header, afhankelijk van de informatie die u in uw reactie nodig hebt.

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

U kunt een specifiek schema opzoeken door een GET-aanvraag in te dienen die de schema-id in het pad bevat.

**API formaat**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CONTAINER_ID}` | De container waarin het schema is opgeslagen dat u wilt ophalen: `global` voor een Adobe-schema of `tenant` voor een schema dat eigendom is van uw organisatie. |
| `{SCHEMA_ID}` | De `meta:altId` of URL-gecodeerde `$id` van het schema dat u wilt opzoeken. |

{style="table-layout:auto"}

**Verzoek**

Met de volgende aanvraag wordt een schema opgehaald dat door de `meta:altId` -waarde in het pad wordt opgegeven.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

De antwoordindeling is afhankelijk van de header `Accept` die in de aanvraag wordt verzonden. Voor alle opzoekverzoeken moet een `version` worden opgenomen in de `Accept` -koptekst. De volgende `Accept` headers zijn beschikbaar:

| `Accept` header | Beschrijving |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Met `$ref` en `allOf` heeft Raw titels en beschrijvingen. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` en `allOf` resolve, heeft titels en beschrijvingen. |
| `application/vnd.adobe.xed-notext+json; version=1` | Onbewerkt met `$ref` en `allOf` , geen titels of beschrijvingen. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` en `allOf` opgelost, geen titels of beschrijvingen. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` en `allOf` opgelost, inclusief beschrijvingen. |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` en `allOf` resolve, heeft titels en beschrijvingen. Vervangen velden worden aangegeven met een `meta:status` -kenmerk van `deprecated` . |

{style="table-layout:auto"}

**Reactie**

Een succesvolle reactie keert de details van het schema terug. Welke velden worden geretourneerd, is afhankelijk van de header `Accept` die in de aanvraag wordt verzonden. Experimenteer met verschillende kopteksten van `Accept` om de reacties te vergelijken en te bepalen welke kopbal het beste voor uw gebruiksgeval is.

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

Voor instructies bij het creëren van een schema zonder klassen of gebiedsgroepen, die als relationeel schema worden bekend, zie [ een relationele schema ](#create-relational-schema) sectie creëren.

>[!NOTE]
>
>De voorbeeldaanroep hieronder is slechts een basislijnvoorbeeld van hoe u een schema in de API maakt, met de minimale compositievereisten van een klasse en geen veldgroepen. Voor volledige stappen op hoe te om een schema in API tot stand te brengen, met inbegrip van hoe te om gebieden toe te wijzen die gebiedsgroepen en gegevenstypes gebruiken, zie de [ zelfstudie van de schemaverwezenlijking ](../tutorials/create-schema-api.md).

**API formaat**

```http
POST /tenant/schemas
```

**Verzoek**

De aanvraag moet een `allOf` -kenmerk bevatten dat naar de `$id` van een klasse verwijst. Dit attribuut bepaalt de &quot;basisklasse&quot;die het schema zal uitvoeren. In dit voorbeeld is de basisklasse een klasse &quot;Eigenschapinformatie&quot; die eerder is gemaakt.

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
| `allOf` | Een array van objecten, waarbij elk object verwijst naar een klasse of veldgroep waarvan het schema velden implementeert. Elk object bevat één eigenschap (`$ref`) waarvan de waarde de `$id` vertegenwoordigt van de klasse of veldgroep die het nieuwe schema zal implementeren. Er moet één klasse worden opgegeven, met nul of meer extra veldgroepen. In het bovenstaande voorbeeld is het ene object in de array `allOf` de klasse van het schema. |

{style="table-layout:auto"}

**Reactie**

Een succesvol antwoord retourneert HTTP-status 201 (Gemaakt) en een lading die de details bevat van het nieuwe schema, inclusief `$id`, `meta:altId` en `version` . Deze waarden zijn alleen-lezen en worden toegewezen door de [!DNL Schema Registry] .

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

Het uitvoeren van een verzoek van GET aan [ lijst alle schema&#39;s ](#list) in de huurderscontainer zou nu het nieuwe schema omvatten. U kunt a [ raadpleging (GET) verzoek ](#lookup) uitvoeren gebruikend URL-Gecodeerde `$id` URI om het nieuwe schema direct te bekijken.

Om extra gebieden aan een schema toe te voegen, kunt u de verrichting van a [ PATCH ](#patch) uitvoeren om gebiedsgroepen aan de 2} en `allOf` series van het schema toe te voegen.`meta:extends`

## Een relationeel schema maken {#create-relational-schema}

>[!AVAILABILITY]
>
>Data Mirror en relationele schema&#39;s zijn beschikbaar aan Adobe Journey Optimizer **Geordende campagnes** vergunninghouders. Zij zijn ook beschikbaar als a **beperkte versie** voor de gebruikers van Customer Journey Analytics, afhankelijk van uw vergunning en eigenschapenactivering. Neem contact op met uw Adobe-vertegenwoordiger voor toegang.

Maak een relationeel schema door een POST-aanvraag in te dienen bij het eindpunt van `/schemas` . De relationele schema&#39;s slaan gestructureerde, relationele-stijlgegevens **zonder** klassen of gebiedsgroepen op. Definieer velden rechtstreeks in het schema en identificeer het schema als relationeel met behulp van een logische gedragstag.

>[!IMPORTANT]
>
>Stel `meta:extends` in op `"https://ns.adobe.com/xdm/data/adhoc-v2"` om een relationeel schema te maken. Dit is a **logisch gedragsherkenningsteken** (niet een fysiek gedrag of een klasse). **niet** verwijzingsklassen of gebiedsgroepen in `allOf`, en **** omvat geen klassen of gebiedsgroepen in `meta:extends`.

Maak eerst het schema met `POST /tenant/schemas` . Dan voeg de vereiste beschrijvers met [ toe Beschrijvers API (`POST /tenant/descriptors`) ](../api/descriptors.md):

- [ Primaire zeer belangrijke beschrijver ](../api/descriptors.md#primary-key-descriptor): Een primair-zeer belangrijk gebied moet op **wortel-niveau** zijn en **duidelijk zoals vereist**.
- [ beschrijver van de Versie ](../api/descriptors.md#version-descriptor): **Vereist** wanneer een primaire sleutel bestaat.
- [ beschrijver van de Verhouding ](../api/descriptors.md#relationship-descriptor): Facultatief, bepaalt toetreedt; kardinaliteit niet afgedwongen bij opname.
- [ de beschrijver van de tijdstempel ](../api/descriptors.md#timestamp-descriptor): Voor tijd-reeksen schema&#39;s, moet de primaire sleutel a **samengestelde** sleutel zijn die het timestamp gebied omvat.

>[!NOTE]
>
>In de Redacteur van het Schema UI, verschijnen de versiedescriptor en timestamp beschrijvers als &quot;[!UICONTROL Version identifier]&quot;en &quot;[!UICONTROL Timestamp identifier]&quot; respectievelijk.

>[!CAUTION]
>
>De relationele schema&#39;s zijn **niet compatibel met unieschema&#39;s**. Pas de tag `union` niet toe op `meta:immutableTags` wanneer u werkt met relationele schema&#39;s. Deze configuratie is geblokkeerd in de gebruikersinterface, maar wordt momenteel niet geblokkeerd door de API. Zie de [ gids van het vakbondseindpunt ](./unions.md) voor meer informatie over het gedrag van het unieschema.

**API formaat**

```http
POST /tenant/schemas
```

**Verzoek**

```shell
curl --request POST \
  --url https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
  "title": "marketing.customers",
  "type": "object",
  "description": "Schema of the Marketing Customers table.",
  "definitions": {
    "customFields": {
      "type": "object",
      "properties": {
        "customer_id": {
          "title": "Customer ID",
          "description": "Primary key of the customer table.",
          "type": "string",
          "minLength": 1
        },
        "name": {
          "title": "Name",
          "description": "Name of the customer.",
          "type": "string"
        },
        "email": {
          "title": "Email",
          "description": "Email of the customer.",
          "type": "string",
          "format": "email",
          "minLength": 1
        }
      },
      "required": ["customer_id"]
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields",
      "meta:xdmType": "object"
    }
  ],
  "meta:extends": ["https://ns.adobe.com/xdm/data/adhoc-v2"],
  "meta:behaviorType": "record"
}
'
```

### Hoofdtekst aanvragen

| Eigenschap | Type | Beschrijving |
| ------------------------------- | ------ | --------------------------------------------------------- |
| `title` | String | Naam van schema weergeven. |
| `description` | String | Korte uitleg van het doel van het schema. |
| `type` | String | Moet `"object"` zijn voor relationele schema&#39;s. |
| `definitions` | Object | Bevat de objecten op hoofdniveau die uw schemavelden definiëren. |
| `definitions.<name>.properties` | Object | Veldnamen en gegevenstypen |
| `allOf` | Array | Verwijst naar de objectdefinitie op hoofdniveau (bijvoorbeeld `#/definitions/marketing_customers` ). |
| `meta:extends` | Array | Moet `"https://ns.adobe.com/xdm/data/adhoc-v2"` bevatten om het schema als relationeel te identificeren. |
| `meta:behaviorType` | String | Instellen op `"record"` . Gebruik `"time-series"` alleen wanneer deze is ingeschakeld en van toepassing is. |

>[!IMPORTANT]
>
>De ontwikkeling van schema&#39;s voor relationele schema&#39;s volgt dezelfde additieve regels als standaardschema&#39;s. U kunt nieuwe velden toevoegen met een PATCH-aanvraag. Wijzigingen als het hernoemen of verwijderen van velden zijn alleen toegestaan als er geen gegevens in de gegevensset zijn opgenomen.

**Reactie**

Een succesvol verzoek keert **HTTP 201 (Gemaakt)** en het gecreeerde schema terug.

>[!NOTE]
>
>Relationele schema&#39;s nemen vooraf ingestelde velden (bijvoorbeeld id, tijdstempel of eventType) niet over. Definieer alle vereiste velden expliciet in uw schema.

**reactie van het Voorbeeld**

```json
{
  "$id": "https://ns.adobe.com/<TENANT_ID>/schemas/<SCHEMA_UUID>",
  "meta:altId": "_<SCHEMA_ALT_ID>",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "marketing.customers",
  "description": "Schema of the Marketing Customers table.",
  "type": "object",
  "definitions": {
    "marketing_customers": {
      "type": "object",
      "properties": {
        "customer_id": {
          "title": "Customer ID",
          "description": "Primary key of the customer table.",
          "type": "string",
          "minLength": 1
        },
        "name": {
          "title": "Name",
          "description": "Name of the customer.",
          "type": "string"
        },
        "email": {
          "title": "Email",
          "description": "Email of the customer.",
          "type": "string",
          "format": "email",
          "minLength": 1
        }
      },
      "required": ["customer_id"]
    }
  },
  "allOf": [
    { "$ref": "#/definitions/marketing_customers" }
  ],
  "meta:extends": ["https://ns.adobe.com/xdm/data/adhoc-v2"],
  "meta:behaviorType": "record",
  "meta:containerId": "tenant"
}
```

### Eigenschappen van het responslichaam

| Eigenschap | Type | Beschrijving |
| ------------------- | ------ | -------------------------- |
| `$id` | String | De unieke URL van het gemaakte schema. Gebruik in volgende API-aanroepen. |
| `meta:altId` | String | Een alternatieve id voor het schema. |
| `meta:resourceType` | String | Het middeltype (altijd `"schemas"`). |
| `version` | String | Een schemaversie die bij verwezenlijking wordt toegewezen. |
| `title` | String | De weergavenaam van het schema. |
| `description` | String | Een korte uitleg van het doel van het schema. |
| `type` | String | Het schematype. |
| `definitions` | Object | Hiermee definieert u herbruikbare objecten of veldgroepen die in het schema worden gebruikt. Dit omvat doorgaans de hoofdgegevensstructuur en wordt in de array `allOf` vermeld om de hoofdmap van het schema te definiëren. |
| `allOf` | Array | Geeft het hoofdobject van het schema op door naar een of meer definities te verwijzen (bijvoorbeeld `#/definitions/marketing_customers` ). |
| `meta:extends` | Array | Identificeert het schema als relationeel (`adhoc-v2`). |
| `meta:behaviorType` | String | Gedragstype (`record` of `time-series` , indien ingeschakeld). |
| `meta:containerId` | String | Container waarin het schema is opgeslagen (bijvoorbeeld `tenant`). |

Om gebieden aan een relationeel schema toe te voegen nadat het is gecreeerd, doe het verzoek van a [ PATCH ](#patch). Relationele schema&#39;s nemen of automatisch evolueren niet over. Structurele wijzigingen zoals het wijzigen van de naam of het verwijderen van velden zijn alleen toegestaan als er geen gegevens in de gegevensset zijn opgenomen. Zodra het gegeven bestaat, slechts **additieve veranderingen** (zoals het toevoegen van nieuwe gebieden) worden gesteund.

U kunt nieuwe velden op hoofdniveau toevoegen (binnen de basisdefinitie of basiscode `properties` ), maar u kunt het type van bestaande velden niet verwijderen, hernoemen of wijzigen.

>[!CAUTION]
>
>De evolutie van het schema wordt beperkt nadat een dataset gebruikend het schema wordt geïnitialiseerd. Namen en typen van velden vooraf zorgvuldig plannen, aangezien velden niet kunnen worden verwijderd of gewijzigd nadat gegevens zijn ingevoerd.

## Een schema bijwerken {#put}

U kunt een volledig schema door een verrichting van PUT vervangen, hoofdzakelijk herschrijvend het middel. Wanneer het bijwerken van een schema door een verzoek van PUT, moet het lichaam alle gebieden omvatten die zouden worden vereist wanneer [ creërend een nieuw schema ](#create) in een POST- verzoek.

>[!NOTE]
>
>Als u slechts een deel van een schema wilt bijwerken in plaats van het volledig te vervangen, zie de sectie op [ het bijwerken van een gedeelte van een schema ](#patch).

**API formaat**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | De `meta:altId` of URL-gecodeerde `$id` van het schema dat u opnieuw wilt schrijven. |

{style="table-layout:auto"}

**Verzoek**

De volgende aanvraag vervangt een bestaand schema door de kenmerken `title` , `description` en `allOf` ervan te wijzigen.

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

**Reactie**

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

U kunt een gedeelte van een schema bijwerken door een PATCH-verzoek te gebruiken. [!DNL Schema Registry] ondersteunt alle standaard JSON-patchbewerkingen, inclusief `add` , `remove` en `replace` . Voor meer informatie over Reparatie JSON, zie de [ API fundamentals gids ](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Als u een volledig middel met nieuwe waarden in plaats van het bijwerken van individuele gebieden wilt vervangen, zie de sectie op [ het vervangen van een schema gebruikend een verrichting van PUT ](#put).

Een van de meest voorkomende PATCH-bewerkingen bestaat uit het toevoegen van eerder gedefinieerde veldgroepen aan een schema, zoals in het onderstaande voorbeeld wordt getoond.

**API formaat**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` van het schema dat u wilt bijwerken. |

{style="table-layout:auto"}

**Verzoek**

In de onderstaande voorbeeldaanvraag wordt een nieuwe veldgroep toegevoegd aan een schema door de waarde `$id` van die veldgroep toe te voegen aan de arrays `meta:extends` en `allOf` .

De aanvraaginstantie heeft de vorm van een array, waarbij elk vermeld object een specifieke wijziging in een afzonderlijk veld vertegenwoordigt. Elk voorwerp omvat uit te voeren verrichting (`op`), welk gebied de verrichting zou moeten worden uitgevoerd (`path`), en welke informatie in die verrichting (`value`) zou moeten worden omvat.

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

**Reactie**

De reactie toont aan dat beide bewerkingen met succes zijn uitgevoerd. De veldgroep `$id` is toegevoegd aan de array `meta:extends` en een verwijzing ( `$ref` ) naar de veldgroep `$id` wordt nu weergegeven in de array `allOf` .

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

## Een schema inschakelen voor gebruik in realtime-klantprofiel {#union}

Opdat een schema om aan [ in real time Profiel van de Klant ](../../profile/home.md) deel te nemen, moet u a `union` markering aan de 3} serie van het schema {toevoegen. `meta:immutableTags` U kunt dit bereiken door een PATCH-aanvraag voor het desbetreffende schema in te dienen.

>[!IMPORTANT]
>
>Onveranderbare tags zijn tags die zijn bedoeld om te worden ingesteld, maar die nooit worden verwijderd.

**API formaat**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` van het schema dat u wilt inschakelen. |

{style="table-layout:auto"}

**Verzoek**

In de onderstaande voorbeeldaanvraag wordt een array `meta:immutableTags` toegevoegd aan een bestaand schema, zodat de array een enkele tekenreekswaarde `union` krijgt om deze in te schakelen voor gebruik in Profiel.

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

**Reactie**

Een succesvol antwoord retourneert de details van het bijgewerkte schema, waarbij wordt getoond dat de array `meta:immutableTags` is toegevoegd.

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

U kunt nu de samenvoeging voor de klasse van dit schema bekijken om te bevestigen dat de gebieden van het schema worden vertegenwoordigd. Zie de [ gids van het vakbondseindpunt ](./unions.md) voor meer informatie.

## Schema verwijderen {#delete}

Het kan soms noodzakelijk zijn om een schema uit de Registratie van het Schema te verwijderen. Dit wordt gedaan door een DELETE- verzoek met schema-identiteitskaart uit te voeren die in de weg wordt verstrekt.

**API formaat**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` van het schema dat u wilt verwijderen. |

{style="table-layout:auto"}

**Verzoek**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst.

U kunt de verwijdering bevestigen door een opzoekverzoek (GET) in te dienen bij het schema. U moet een header `Accept` in de aanvraag opnemen, maar u moet de HTTP-status 404 (Niet gevonden) ontvangen omdat het schema uit de schemaregistratie is verwijderd.
