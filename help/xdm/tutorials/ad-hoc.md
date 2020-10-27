---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;ad-hoc;ad hoc;adhoc;Ad-hoc;Ad hoc;Adhoc;tutorial;Tutorial;create;Create;schema;Schema
solution: Experience Platform
title: Een ad-hocschema maken
description: In specifieke omstandigheden, kan het noodzakelijk zijn om een schema van de Gegevens van de Ervaring van het Model (XDM) met gebieden tot stand te brengen die voor gebruik slechts door één enkele dataset worden genoemd. Dit wordt bedoeld als "ad-hoc"schema. Ad-hocschema's worden gebruikt in diverse werkstromen voor gegevensinvoer voor Experience Platform, met inbegrip van het opnemen van CSV-bestanden en het creëren van bepaalde soorten bronverbindingen.
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 097fe219e0d64090de758f388ba98e6024db2201
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 1%

---


# Een ad-hocschema maken

In specifieke omstandigheden, kan het noodzakelijk zijn om een [!DNL Experience Data Model] (XDM) schema met gebieden tot stand te brengen die namespaced voor gebruik slechts door één enkele dataset zijn. Dit wordt bedoeld als &quot;ad-hoc&quot;schema. Ad-hocschema&#39;s worden gebruikt in diverse werkstromen voor het opnemen van gegevens, [!DNL Experience Platform]zoals het opnemen van CSV-bestanden en het maken van bepaalde soorten bronverbindingen.

Dit document bevat algemene stappen voor het maken van een ad-hocschema met behulp van de [Schemaregistratie-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Het is bedoeld voor gebruik in combinatie met andere [!DNL Experience Platform] zelfstudies waarvoor een ad-hocschema moet worden gemaakt als onderdeel van de workflow. Elk van die documenten verstrekt gedetailleerde informatie over hoe te om een ad-hocschema voor zijn specifiek gebruiksgeval behoorlijk te vormen.

## Aan de slag

Deze zelfstudie vereist een goed begrip van [!DNL Experience Data Model] (XDM) System. Lees de volgende XDM-documentatie voordat u deze zelfstudie start:

- [XDM-systeemoverzicht](../home.md): Een overzicht op hoog niveau van XDM en zijn implementatie in [!DNL Experience Platform].
- [Basisbeginselen van de schemacompositie](../schema/composition.md): Een overzicht van de basiscomponenten van schema&#39;s XDM.

Voordat u deze zelfstudie start, moet u eerst de [ontwikkelaarsgids](../api/getting-started.md) raadplegen voor belangrijke informatie die u moet weten om oproepen naar de [!DNL Schema Registry] API te kunnen uitvoeren. Dit omvat uw `{TENANT_ID}`, het concept &quot;containers&quot;, en de vereiste kopballen voor het maken van verzoeken (met speciale aandacht voor de Accept kopbal en zijn mogelijke waarden).

## Een ad-hocklasse maken

Het gegevensgedrag van een schema XDM wordt bepaald door zijn onderliggende klasse. De eerste stap bij het maken van een ad-hocschema is het maken van een klasse op basis van het `adhoc` gedrag. Dit wordt gedaan door een verzoek van de POST aan het `/tenant/classes` eindpunt te doen.

**API-indeling**

```http
POST /tenant/classes
```

**Verzoek**

Met de volgende aanvraag wordt een nieuwe XDM-klasse gemaakt, geconfigureerd door de kenmerken die in de payload worden opgegeven. Door een `$ref` eigenschap op te geven die is ingesteld op `https://ns.adobe.com/xdm/data/adhoc` in de `allOf` array, overerft deze klasse het `adhoc` gedrag. De aanvraag definieert ook een `_adhoc` object dat de aangepaste velden voor de klasse bevat.

>[!NOTE]
>
>De aangepaste velden die onder `_adhoc` deze sectie worden gedefinieerd, variëren afhankelijk van het gebruikte hoofdlettergebruik van het ad-hocschema. Raadpleeg de specifieke workflow in de juiste zelfstudie voor vereiste aangepaste velden op basis van het gebruiksgeval.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `$ref` | Het gegevensgedrag voor de nieuwe klasse. Voor ad-hocklassen moet deze waarde worden ingesteld op `https://ns.adobe.com/xdm/data/adhoc`. |
| `properties._adhoc` | Een object dat de aangepaste velden voor de klasse bevat, uitgedrukt als sleutel-waardeparen van veldnamen en gegevenstypen. |

**Antwoord**

Een succesvolle reactie keert de details van de nieuwe klasse terug, die de naam van het `properties._adhoc` voorwerp met een GUID vervangt die een systeem-geproduceerde, read-only uniek herkenningsteken voor de klasse is. Het `meta:datasetNamespace` kenmerk wordt ook automatisch gegenereerd en opgenomen in de reactie.

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
    "imsOrg": "{IMS_ORG}",
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

## Een ad-hocschema maken

Zodra u een ad-hocklasse hebt gecreeerd, kunt u een nieuw schema tot stand brengen dat die klasse uitvoert door een POST tot een verzoek aan het `/tenant/schemas` eindpunt te richten.

**API-indeling**

```http
POST /tenant/schemas
```

**Verzoek**

Met de volgende aanvraag wordt een nieuw schema gemaakt dat een verwijzing (`$ref`) bevat naar de eerder gemaakte ad-hocklasse in de payload `$id` van die klasse.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

**Antwoord**

Een geslaagde reactie retourneert de details van het nieuwe schema, inclusief de door het systeem gegenereerde, alleen-lezen `$id`.

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
    "imsOrg": "{IMS_ORG}",
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
>Deze stap is optioneel. Als u de veldstructuur van uw ad-hocschema niet wilt inspecteren, kunt u de sectie [Volgende stappen](#next-steps) aan het einde van deze zelfstudie overslaan.

Nadat u het ad-hocschema hebt gemaakt, kunt u een opzoekverzoek (GET) indienen om het schema in het uitgebreide formulier weer te geven. Dit wordt gedaan door de aangewezen Accept- kopbal in het verzoek van de GET te gebruiken, zoals hieronder aangetoond.

**API-indeling**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` het ad-hocschema waartoe u toegang wilt hebben. |

**Verzoek**

In het volgende verzoek wordt de header Accept gebruikt `application/vnd.adobe.xed-full+json; version=1`, die de uitgebreide vorm van het schema retourneert. Merk op dat wanneer het terugwinnen van een specifiek middel van het [!DNL Schema Registry], de Accept kopbal van het verzoek belangrijke versie van de betrokken bron moet omvatten.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

Een geslaagde reactie retourneert de details van het schema, inclusief alle geneste velden onder `properties`.

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
    "imsOrg": "{IMS_ORG}",
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

Door deze zelfstudie te volgen, hebt u een nieuw ad-hocschema gemaakt. Als u naar dit document bent overgebracht als onderdeel van een andere zelfstudie, kunt u nu de instructies van uw ad-hocschema gebruiken om de workflow te voltooien. `$id`

Raadpleeg voor meer informatie over het werken met de [!DNL Schema Registry] API de handleiding voor [ontwikkelaars](../api/getting-started.md).