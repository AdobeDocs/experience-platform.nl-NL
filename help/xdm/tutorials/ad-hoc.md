---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM-systeem;ervaringsgegevensmodel;Experience Data Model;Experience Data Model;Data Model;Schema Register;Ad-hoc;Ad-hoc;Ad-hoc;Ad-hoc;Ad-hoc;Zelfstudie;Lesbestand;Lesbestand;Maken;Schema;Schema
solution: Experience Platform
title: Een ad-hocschema maken
description: In specifieke omstandigheden, kan het noodzakelijk zijn om een schema van de Gegevens van de Ervaring van het Model (XDM) met gebieden tot stand te brengen die voor gebruik slechts door één enkele dataset worden genoemd. Dit wordt bedoeld als "ad-hoc"schema. Ad-hocschema's worden gebruikt in diverse werkstromen voor gegevensinvoer voor Experience Platform, met inbegrip van het opnemen van CSV-bestanden en het creëren van bepaalde soorten bronverbindingen.
topic-legacy: tutorial
type: Tutorial
exl-id: bef01000-909a-4594-8cf4-b9dbe0b358d5
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 1%

---

# Een ad-hocschema maken

In specifieke omstandigheden kan het nodig zijn een [!DNL Experience Data Model] (XDM) schema met gebieden die namespaced voor gebruik slechts door één enkele dataset zijn. Dit wordt bedoeld als &quot;ad-hoc&quot;schema. Ad-hocschema&#39;s worden gebruikt in verschillende workflows voor gegevensinvoer voor [!DNL Experience Platform], waaronder het opnemen van CSV-bestanden en het maken van bepaalde soorten bronverbindingen.

Dit document bevat algemene stappen voor het maken van een ad-hocschema met het [Schema-register-API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Het is bedoeld om samen met andere [!DNL Experience Platform] zelfstudies die het maken van een ad-hocschema als onderdeel van hun workflow vereisen. Elk van die documenten verstrekt gedetailleerde informatie over hoe te om een ad-hocschema voor zijn specifiek gebruiksgeval behoorlijk te vormen.

## Aan de slag

Deze zelfstudie vereist een goed begrip van [!DNL Experience Data Model] (XDM) System. Lees de volgende XDM-documentatie voordat u deze zelfstudie start:

- [XDM System, overzicht](../home.md): Een overzicht op hoog niveau van XDM en zijn implementatie in [!DNL Experience Platform].
- [Basisbeginselen van de schemacompositie](../schema/composition.md): Een overzicht van de basiscomponenten van schema&#39;s XDM.

Lees voordat u deze zelfstudie start de [ontwikkelaarsgids](../api/getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan te maken [!DNL Schema Registry] API. Dit omvat uw `{TENANT_ID}`, het concept &quot;containers&quot; en de vereiste kopteksten voor het indienen van verzoeken (met speciale aandacht voor de Accept-koptekst en de mogelijke waarden ervan).

## Een ad-hocklasse maken

Het gegevensgedrag van een schema XDM wordt bepaald door zijn onderliggende klasse. De eerste stap bij het maken van een ad-hocschema bestaat uit het maken van een klasse op basis van het `adhoc` gedrag. Dit gebeurt door een verzoek van de POST aan `/tenant/classes` eindpunt.

**API-indeling**

```http
POST /tenant/classes
```

**Verzoek**

Met de volgende aanvraag wordt een nieuwe XDM-klasse gemaakt, geconfigureerd door de kenmerken die in de payload worden opgegeven. Door een `$ref` eigenschap ingesteld op `https://ns.adobe.com/xdm/data/adhoc` in de `allOf` array, deze klasse overerft de `adhoc` gedrag. In de aanvraag wordt ook een `_adhoc` object, dat de aangepaste velden voor de klasse bevat.

>[!NOTE]
>
>De aangepaste velden die zijn gedefinieerd onder `_adhoc` variëren afhankelijk van het gebruiksgeval van het ad-hocschema. Raadpleeg de specifieke workflow in de juiste zelfstudie voor vereiste aangepaste velden op basis van het gebruiksgeval.

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
| `$ref` | Het gegevensgedrag voor de nieuwe klasse. Voor ad-hocklassen moet deze waarde worden ingesteld op `https://ns.adobe.com/xdm/data/adhoc`. |
| `properties._adhoc` | Een object dat de aangepaste velden voor de klasse bevat, uitgedrukt als sleutel-waardeparen van veldnamen en gegevenstypen. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Als de reactie met succes is uitgevoerd, worden de details van de nieuwe klasse geretourneerd en wordt de naam `properties._adhoc` de naam van objecten met een GUID die een systeem-geproduceerde, read-only uniek herkenningsteken voor de klasse is. De `meta:datasetNamespace` wordt ook automatisch gegenereerd en opgenomen in de reactie.

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

{style=&quot;table-layout:auto&quot;}

## Een ad-hocschema maken

Wanneer u een ad-hocklasse hebt gemaakt, kunt u een nieuw schema maken dat die klasse implementeert door een POST aan te vragen bij de `/tenant/schemas` eindpunt.

**API-indeling**

```http
POST /tenant/schemas
```

**Verzoek**

Met het volgende verzoek maakt u een nieuw schema en geeft u een verwijzing op (`$ref`) aan de `$id` van de eerder gemaakte ad-hocklasse in de payload.

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

**Antwoord**

Een succesvolle reactie keert de details van het onlangs gecreëerde schema, met inbegrip van zijn systeem-geproduceerde, read-only terug `$id`.

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
>Deze stap is optioneel. Als u de veldstructuur van uw ad-hocschema niet wilt inspecteren, kunt u het volgende overslaan: [volgende stappen](#next-steps) aan het einde van deze zelfstudie.

Nadat u het ad-hocschema hebt gemaakt, kunt u een opzoekverzoek (GET) indienen om het schema in het uitgebreide formulier weer te geven. Dit wordt gedaan door de aangewezen Accept- kopbal in het verzoek van de GET te gebruiken, zoals hieronder aangetoond.

**API-indeling**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | URL-gecodeerd `$id` URI of `meta:altId` van het ad-hocschema waartoe u toegang wilt hebben. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

In het volgende verzoek wordt de header Accepteren gebruikt `application/vnd.adobe.xed-full+json; version=1`, die de uitgebreide vorm van het schema retourneert. Merk op dat wanneer het terugwinnen van een specifiek middel van [!DNL Schema Registry]In de Accept-header van het verzoek moet echter een belangrijke versie van de betreffende bron staan.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Door deze zelfstudie te volgen, hebt u een nieuw ad-hocschema gemaakt. Als u naar dit document bent gebracht als onderdeel van een andere zelfstudie, kunt u nu de opdracht `$id` van uw ad-hocschema om de workflow volgens de instructies te voltooien.

Voor meer informatie over het werken met de [!DNL Schema Registry] API, gelieve te verwijzen naar [ontwikkelaarsgids](../api/getting-started.md).
