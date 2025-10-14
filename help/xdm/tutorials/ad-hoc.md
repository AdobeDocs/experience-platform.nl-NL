---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM-systeem;ervaringsgegevensmodel;Experience Data Model;Experience Data Model;Data Model;Schema Register;Ad-hoc;Ad-hoc;Ad-hoc;Ad-hoc;Ad-hoc;Zelfstudie;Lesbestand;Lesbestand;Maken;Schema;Schema
solution: Experience Platform
title: Een ad-hocschema maken
description: In specifieke omstandigheden, kan het noodzakelijk zijn om een schema van de Gegevens van de Ervaring van het Model (XDM) met gebieden tot stand te brengen die voor gebruik slechts door één enkele dataset worden genoemd. Dit wordt bedoeld als "ad-hoc"schema. Ad-hocschema's worden gebruikt in diverse werkstromen voor gegevensinvoer voor Experience Platform, met inbegrip van het opnemen van CSV-bestanden en het creëren van bepaalde soorten bronverbindingen.
type: Tutorial
exl-id: bef01000-909a-4594-8cf4-b9dbe0b358d5
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 1%

---

# Een ad-hocschema maken

In specifieke omstandigheden, kan het noodzakelijk zijn om een [!DNL Experience Data Model] (XDM) schema met gebieden tot stand te brengen die namespaced voor gebruik slechts door één enkele dataset zijn. Dit wordt bedoeld als &quot;ad-hoc&quot;schema. Ad-hocschema&#39;s worden gebruikt in verschillende gegevensinvoerworkflows voor [!DNL Experience Platform] , waaronder het opnemen van CSV-bestanden en het maken van bepaalde soorten bronverbindingen.

Dit document verstrekt algemene stappen voor het creëren van een ad hoc schema gebruikend de [&#x200B; Registratie API van het Schema &#x200B;](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Het is bedoeld voor gebruik in combinatie met andere zelfstudies van [!DNL Experience Platform] waarvoor een ad-hocschema moet worden gemaakt als onderdeel van de workflow. Elk van die documenten verstrekt gedetailleerde informatie over hoe te om een ad-hocschema voor zijn specifiek gebruiksgeval behoorlijk te vormen.

## Aan de slag

Deze zelfstudie vereist een goed begrip van [!DNL Experience Data Model] (XDM) Systeem. Lees de volgende XDM-documentatie voordat u deze zelfstudie start:

- [&#x200B; XDM Overzicht van het Systeem &#x200B;](../home.md): Een overzicht op hoog niveau van XDM en zijn implementatie in [!DNL Experience Platform].
- [&#x200B; Grondbeginselen van schemacompositie &#x200B;](../schema/composition.md): Een overzicht van de basiscomponenten van schema&#39;s XDM.

Alvorens dit leerprogramma te beginnen, te herzien gelieve de [&#x200B; ontwikkelaarsgids &#x200B;](../api/getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan [!DNL Schema Registry] API met succes te maken. Dit omvat uw `{TENANT_ID}`, het concept &quot;containers&quot;, en de vereiste kopballen voor het maken van verzoeken (met speciale aandacht voor de Accept kopbal en zijn mogelijke waarden).

## Een ad-hocklasse maken

Het gegevensgedrag van een schema XDM wordt bepaald door zijn onderliggende klasse. De eerste stap bij het maken van een ad-hocschema is het maken van een klasse op basis van het `adhoc` -gedrag. Dit wordt gedaan door een verzoek van de POST aan het `/tenant/classes` eindpunt te doen.

**API formaat**

```http
POST /tenant/classes
```

**Verzoek**

Met de volgende aanvraag wordt een nieuwe XDM-klasse gemaakt, geconfigureerd door de kenmerken die in de payload worden opgegeven. Door een eigenschap `$ref` op te geven die is ingesteld op `https://ns.adobe.com/xdm/data/adhoc` in de array `allOf` , overerft deze klasse het gedrag `adhoc` . De aanvraag definieert ook een `_adhoc` -object dat de aangepaste velden voor de klasse bevat.

>[!NOTE]
>
>De aangepaste velden die onder `_adhoc` worden gedefinieerd, variëren afhankelijk van het gebruikte hoofdlettergebruik van het ad-hocschema. Raadpleeg de specifieke workflow in de juiste zelfstudie voor vereiste aangepaste velden op basis van het gebruiksgeval.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"New ad-hoc class",
        "description": "New ad-hoc class description",
        "type":"object",
        "allOf": [
          {
            "$ref":"https://ns.adobe.com/xdm/data/adhoc"
          },
          {
            "properties": {
              "_adhoc": {
                "type":"object",
                "properties": {
                  "field1": {
                    "type":"string"
                  },
                  "field2": {
                    "type":"string"
                  }
                }
              }
            }
          }
        ]
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `$ref` | Het gegevensgedrag voor de nieuwe klasse. Voor ad-hocklassen moet deze waarde worden ingesteld op `https://ns.adobe.com/xdm/data/adhoc` . |
| `properties._adhoc` | Een object dat de aangepaste velden voor de klasse bevat, uitgedrukt als sleutel-waardeparen van veldnamen en gegevenstypen. |

{style="table-layout:auto"}

**Reactie**

Een succesvolle reactie keert de details van de nieuwe klasse terug, die de naam van het `properties._adhoc` voorwerp met een GUID vervangt die systeem-geproduceerde, read-only unieke herkenningsteken voor de klasse is. Het kenmerk `meta:datasetNamespace` wordt ook automatisch gegenereerd en opgenomen in de reactie.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:altId": "_{TENANT_ID}.classes.6395cbd58812a6d64c4e5344f7b9120f",
    "meta:resourceType": "classes",
    "version": "1.0",
    "title": "New Class",
    "description": "New class description",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/data/adhoc"
        },
        {
            "properties": {
                "_6395cbd58812a6d64c4e5344f7b9120f": {
                    "type": "object",
                    "properties": {
                        "field1": {
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "field2": {
                            "type": "string",
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:extends": [
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "imsOrg": "{ORG_ID}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557527784822,
        "repo:lastModifiedDate": 1557527784822,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "Jggrlh4PQdZUvDUhQHXKx38iTQo="
    }
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `$id` | Een URI die fungeert als de alleen-lezen; door het systeem gegenereerde unieke id voor de nieuwe ad-hocklasse. Deze waarde wordt gebruikt in de volgende stap voor het maken van een ad-hocschema. |

{style="table-layout:auto"}

## Een ad-hocschema maken

Nadat u een ad-hocklasse hebt gemaakt, kunt u een nieuw schema maken dat die klasse implementeert door een POST aan te vragen bij het `/tenant/schemas` -eindpunt.

**API formaat**

```http
POST /tenant/schemas
```

**Verzoek**

Met de volgende aanvraag wordt een nieuw schema gemaakt, waarbij een verwijzing (`$ref`) naar de `$id` van de eerder gemaakte ad-hocklasse in de payload wordt opgegeven.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"New Schema",
        "description": "New schema description.",
        "type":"object",
        "allOf": [
          {
            "$ref":"https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f"
          }
        ]
      }'
```

**Reactie**

Een succesvol antwoord retourneert de details van het nieuwe schema, inclusief de door het systeem gegenereerde, alleen-lezen `$id` .

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d",
    "meta:altId": "_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "New Schema",
    "description": "New schema description.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f"
        }
    ],
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557528570542,
        "repo:lastModifiedDate": 1557528570542,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "Jggrlh4PQdZUvDUhQHXKx38iTQo="
    }
}
```

## Het volledige ad-hocschema weergeven

>[!NOTE]
>
>Deze stap is optioneel. Als u niet wenst om de gebiedsstructuur van uw ad hoc schema te inspecteren, kunt u aan de [&#x200B; volgende stappen &#x200B;](#next-steps) sectie aan het eind van dit leerprogramma overslaan.

Nadat u het ad-hocschema hebt gemaakt, kunt u een opzoekverzoek (GET) indienen om het schema in het uitgebreide formulier weer te geven. Dit wordt gedaan door de aangewezen Accept- kopbal in het verzoek van de GET te gebruiken, zoals hieronder aangetoond.

**API formaat**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` van het ad-hocschema waartoe u toegang wilt hebben. |

{style="table-layout:auto"}

**Verzoek**

In de volgende aanvraag wordt de header Accepteren `application/vnd.adobe.xed-full+json; version=1` gebruikt, die de uitgebreide vorm van het schema retourneert. Merk op dat wanneer het terugwinnen van een specifieke middel van [!DNL Schema Registry], de Accept kopbal van het verzoek belangrijke versie van de betrokken bron moet omvatten.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Reactie**

Een succesvol antwoord retourneert de details van het schema, inclusief alle geneste velden onder `properties` .

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d",
    "meta:altId": "_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "New Schema",
    "description": "New schema description.",
    "type": "object",
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:xdmType": "object",
    "properties": {
        "_6395cbd58812a6d64c4e5344f7b9120f": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "field1": {
                    "type": "string",
                    "meta:xdmType": "string"
                },
                "field2": {
                    "type": "string",
                    "meta:xdmType": "string"
                }
            }
        }
    },
    "meta:registryMetadata": {
        "repo:createdDate": 1557528570542,
        "repo:lastModifiedDate": 1557528570542,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "bTogM1ON2LO/F7rlcc1iOWmNVy0="
    }
}
```

## Volgende stappen {#next-steps}

Door deze zelfstudie te volgen, hebt u een nieuw ad-hocschema gemaakt. Als u naar dit document bent overgebracht als onderdeel van een andere zelfstudie, kunt u nu de `$id` van uw ad-hocschema gebruiken om de workflow volgens de aanwijzingen te voltooien.

Voor meer informatie bij het werken met [!DNL Schema Registry] API, gelieve te verwijzen naar de [&#x200B; ontwikkelaarsgids &#x200B;](../api/getting-started.md).
