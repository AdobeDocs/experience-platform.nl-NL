---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM-systeem;ervaringsgegevensmodel;Experience Data Model;Experience Data Model;Data Model;Schema Register;Ad-hoc;Ad-hoc;Ad-hoc;Ad-hoc;Ad-hoc;Zelfstudie;Lesbestand;Lesbestand;Maken;Schema;Schema
solution: Experience Platform
title: Een ad-hocschema maken
description: In specifieke omstandigheden, kan het noodzakelijk zijn om een schema van de Gegevens van de Ervaring van het Model (XDM) met gebieden tot stand te brengen die voor gebruik slechts door één enkele dataset worden genoemd. Dit wordt bedoeld als "ad-hoc"schema. Ad-hocschema's worden gebruikt in diverse werkstromen voor gegevensinvoer voor Experience Platform, met inbegrip van het opnemen van CSV-bestanden en het creëren van bepaalde soorten bronverbindingen.
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 1%

---


# Een ad-hocschema maken

In specifieke omstandigheden, kan het noodzakelijk zijn om een [!DNL Experience Data Model] (XDM) schema met gebieden tot stand te brengen die namespaced voor gebruik slechts door één enkele dataset zijn. Dit wordt bedoeld als &quot;ad-hoc&quot;schema. Ad-hocschema&#39;s worden gebruikt in diverse werkstromen voor gegevensinvoer voor [!DNL Experience Platform], met inbegrip van het opnemen van CSV-bestanden en het creëren van bepaalde soorten bronverbindingen.

Dit document bevat algemene stappen voor het maken van een ad-hocschema met de [Schemaregistratie-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Het is bedoeld om samen met andere [!DNL Experience Platform] zelfstudies te worden gebruikt die het creëren van een ad hoc schema als deel van hun werkschema vereisen. Elk van die documenten verstrekt gedetailleerde informatie over hoe te om een ad-hocschema voor zijn specifiek gebruiksgeval behoorlijk te vormen.

## Aan de slag

Deze zelfstudie vereist een goed begrip van [!DNL Experience Data Model] (XDM) Systeem. Lees de volgende XDM-documentatie voordat u deze zelfstudie start:

- [XDM-systeemoverzicht](../home.md): Een overzicht op hoog niveau van XDM en zijn implementatie in  [!DNL Experience Platform].
- [Basisbeginselen van de schemacompositie](../schema/composition.md): Een overzicht van de basiscomponenten van schema&#39;s XDM.

Voordat u deze zelfstudie start, raadpleegt u de [ontwikkelaarshandleiding](../api/getting-started.md) voor belangrijke informatie die u moet weten om de [!DNL Schema Registry]-API te kunnen aanroepen. Dit omvat uw `{TENANT_ID}`, het concept &quot;containers&quot;, en de vereiste kopballen voor het maken van verzoeken (met speciale aandacht voor de Accept kopbal en zijn mogelijke waarden).

## Een ad-hocklasse maken

Het gegevensgedrag van een schema XDM wordt bepaald door zijn onderliggende klasse. De eerste stap bij het maken van een ad-hocschema is het maken van een klasse op basis van het gedrag `adhoc`. Dit wordt gedaan door een verzoek van de POST aan het `/tenant/classes` eindpunt te doen.

**API-indeling**

```http
POST /tenant/classes
```

**Verzoek**

Met de volgende aanvraag wordt een nieuwe XDM-klasse gemaakt, geconfigureerd door de kenmerken die in de payload worden opgegeven. Door een `$ref` bezit te leveren die aan `https://ns.adobe.com/xdm/data/adhoc` in `allOf` serie wordt geplaatst, erft deze klasse het `adhoc` gedrag. Het verzoek definieert ook een `_adhoc`-object, dat de aangepaste velden voor de klasse bevat.

>[!NOTE]
>
>De aangepaste velden die worden gedefinieerd onder `_adhoc`, variëren afhankelijk van het gebruikte hoofdlettergebruik van het ad-hocschema. Raadpleeg de specifieke workflow in de juiste zelfstudie voor vereiste aangepaste velden op basis van het gebruiksgeval.

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

Een succesvolle reactie keert de details van de nieuwe klasse terug, die de naam van `properties._adhoc` met een GUID vervangt die een systeem-geproduceerde, read-only uniek herkenningsteken voor de klasse is. Het `meta:datasetNamespace` attribuut wordt ook automatisch geproduceerd en inbegrepen in de reactie.

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

Zodra u een ad-hoc klasse hebt gecreeerd, kunt u een nieuw schema tot stand brengen dat die klasse door een POST verzoek aan het `/tenant/schemas` eindpunt uit te voeren uitvoert.

**API-indeling**

```http
POST /tenant/schemas
```

**Verzoek**

Het volgende verzoek leidt tot een nieuw schema, dat een verwijzing (`$ref`) aan `$id` van de eerder gecreeerde ad hoc klasse in zijn lading verstrekt.

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

Een succesvolle reactie keert de details van het onlangs gecreeerd schema, met inbegrip van zijn systeem-geproduceerde, read-only `$id` terug.

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
>Deze stap is optioneel. Als u niet wenst om de gebiedsstructuur van uw ad hoc schema te inspecteren, kunt u aan [volgende stappen](#next-steps) sectie aan het eind van dit leerprogramma overslaan.

Nadat u het ad-hocschema hebt gemaakt, kunt u een opzoekverzoek (GET) indienen om het schema in het uitgebreide formulier weer te geven. Dit wordt gedaan door de aangewezen Accept- kopbal in het verzoek van de GET te gebruiken, zoals hieronder aangetoond.

**API-indeling**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` van het ad-hocschema dat u wilt openen. |

**Verzoek**

In het volgende verzoek wordt de header Accept `application/vnd.adobe.xed-full+json; version=1` gebruikt, die de uitgebreide vorm van het schema retourneert. Merk op dat wanneer het terugwinnen van een specifiek middel van [!DNL Schema Registry], de Accept van het verzoek kopbal belangrijke versie van de middel in kwestie moet omvatten.

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

Een succesvol antwoord retourneert de details van het schema, inclusief alle geneste velden onder `properties`.

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

Door deze zelfstudie te volgen, hebt u een nieuw ad-hocschema gemaakt. Als u naar dit document bent gebracht als onderdeel van een andere zelfstudie, kunt u nu `$id` van uw ad-hocschema gebruiken om de workflow volgens de instructies te voltooien.

Raadpleeg de [handleiding voor ontwikkelaars](../api/getting-started.md) voor meer informatie over het werken met de [!DNL Schema Registry]-API.