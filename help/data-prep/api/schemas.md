---
keywords: Experience Platform;thuis;populaire onderwerpen;gegevens prep;api gids;schema's;
solution: Experience Platform
title: Schemas API Endpoint
topic: schema's
description: 'U kunt het `/schema''s'' eindpunt in Adobe Experience Platform API gebruiken om schema''s voor gebruik met Mapper in Platform programmatically terug te winnen, tot stand te brengen en bij te werken. '
translation-type: tm+mt
source-git-commit: 435d27f7187074c78209948c0e57b610b63d2055
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---



# Schemas, eindpunt

Schema&#39;s kunnen met Mapper worden gebruikt om ervoor te zorgen dat de gegevens die u in Adobe Experience Platform hebt ingevoerd overeenkomen met wat u wilt opnemen. U kunt het `/schemas` eindpunt gebruiken programmatically om douaneschema&#39;s voor gebruik met Mapper in Platform tot stand te brengen, te maken en te krijgen.

>[!NOTE]
>
>Schema&#39;s die met dit eindpunt worden gemaakt, worden uitsluitend gebruikt met Mapper- en toewijzingssets. Als u schema&#39;s wilt maken die toegankelijk zijn voor andere services van Platforms, leest u de [Handleiding voor ontwikkelaars van het schema Registry](../../xdm/api/schemas.md).

## Alle schema&#39;s ophalen

U kunt een lijst van alle beschikbare schema&#39;s van de Toewijzing voor uw IMS Organisatie terugwinnen door een verzoek van de GET aan het `/schemas` eindpunt te doen.

**API-indeling**

Het `/schemas` eindpunt steunt verscheidene vraagparameters om u te helpen uw resultaten filtreren. Hoewel de meeste van deze parameters optioneel zijn, wordt het gebruik ervan sterk aanbevolen om de kostbare overhead te helpen verminderen. Nochtans, moet u zowel `start` als `limit` parameters als deel van uw verzoek omvatten. U kunt meerdere parameters opnemen, gescheiden door ampersands (`&`).

```http
GET /schemas?limit={LIMIT}&start={START}
GET /schemas?limit={LIMIT}&start={START}&name={NAME}
GET /schemas?limit={LIMIT}&start={START}&orderBy={ORDER_BY}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{LIMIT}` | **Vereist**. Geeft het aantal geretourneerde schema&#39;s aan. |
| `{START}` | **Vereist**. Hiermee bepaalt u de verschuiving van de resultatenpagina&#39;s. Als u de eerste pagina met resultaten wilt ophalen, stelt u de waarde in op `start=0`. |
| `{NAME}` | Hiermee filtert u het schema op basis van de naam. |
| `{ORDER_BY}` | Hiermee sorteert u de volgorde van de resultaten. De ondersteunde velden zijn `modifiedDate` en `createdDate`. U kunt de eigenschap voorvullen met `+` of `-` om deze te sorteren in oplopende of aflopende volgorde. |

**Verzoek**

Met het volgende verzoek worden de laatste twee gemaakte schema&#39;s voor uw IMS-organisatie opgehaald.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas&start=0&limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

De volgende reactie keert status 200 van HTTP met een lijst van de gevraagde schema&#39;s terug.

>[!NOTE]
>
>De volgende reactie is afgebroken voor de ruimte.

```json
{
    "data": [
        {
            "id": "823ac494f35e4e84bcb2f061378fcca6",
            "version": 0,
            "jsonSchema": {
                "title": "Sample schema",
                "type": "object",
                "properties": {
                    "_id": {
                        "title": "Identifier",
                        "description": "A unique identifier for the record.",
                        "type": "string",
                        "format": "uri-reference",
                        "meta:xdmField": "@id",
                        "meta:xdmType": "string"
                    },
                    "city": {
                        "title": "City",
                        "description": "The name of the city.",
                        "type": "string",
                        "meta:xdmField": "xdm:city",
                        "meta:xdmType": "string"
                    }
                }
            },
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc",
                "contentType": "1.0"
            }
        },
        {
            "id": "0f868d3a1b804fb0abf738306290ae79",
            "version": 0,
            "jsonSchema": {
                "title": "Sample schema 2",
                "type": "object",
                "properties": {
                    "_id": {
                        "title": "Identifier",
                        "description": "A unique identifier for the record.",
                        "type": "string",
                        "format": "uri-reference",
                        "meta:xdmField": "@id",
                        "meta:xdmType": "string"
                    },
                    "city": {
                        "title": "City",
                        "description": "The name of the city.",
                        "type": "string",
                        "meta:xdmField": "xdm:city",
                        "meta:xdmType": "string"
                    }
                }
            },
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/0f868d3a1b804fb0abf738306290ae79",
                "contentType": "1.0"
            }
        }
    ],
    "_page": {
        "count": 2,
        "limit": 2
    }
}
```

## Een schema maken

U kunt een schema tot stand brengen om tegen te bevestigen door een verzoek van de POST aan het `/schemas` eindpunt te doen. Er zijn drie manieren om een schema te maken: het verzenden van een [JSON Schema](https://json-schema.org/), gebruikend steekproefgegevens, of het van verwijzingen voorzien van een bestaand schema XDM.

```http
POST /schemas
```

### Een JSON-schema gebruiken

**Verzoek**

Met het volgende verzoek kunt u een schema maken door een [JSON-schema](https://json-schema.org/) te verzenden.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met informatie over uw onlangs gecreeerd schema terug.

```json
{
    "id": "6daffabf14b1425292add3719afc8fab",
    "version": 0,
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}
```

### Voorbeeldgegevens gebruiken

**Verzoek**

Met het volgende verzoek kunt u een schema maken met behulp van voorbeeldgegevens die u eerder hebt geüpload.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "sampleId": "45439a93d48d47d098d26e0f0840cc02"  
 }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `sampleId` | De id van de voorbeeldgegevens waarvan u het schema baseert. |

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met informatie over uw onlangs gecreeerd schema terug.

```json
{
    "id": "b2ee78bd55ac45f781a93fb8b90d99b2",
    "version": 0,
    "jsonSchema": {
        "title": "SampleSchema:45439a93d48d47d098d26e0f0840cc02",
        "type": "object",
        "properties": {
            "gender": {
                "title": "gender",
                "type": "string"
            },
            "last_name": {
                "title": "last_name",
                "type": "string"
            },
            "id": {
                "title": "id",
                "type": "string"
            },
            "ip_address": {
                "title": "ip_address",
                "type": "string"
            },
            "first_name": {
                "title": "first_name",
                "type": "string"
            },
            "email": {
                "title": "email",
                "type": "string"
            }
        }
    },
    "sampleId": "45439a93d48d47d098d26e0f0840cc02"
}
```

### Verwijs naar een XDM-schema

**Verzoek**

Met het volgende verzoek kunt u een schema maken door naar een bestaand XDM-schema te verwijzen.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "name": "outputSchema1",
     "schemaRef": {
         "id": "https://ns.adobe.com/{TENANT_ID}/schemas/0d555890502224d187b619f23c35c8d1",
         "contentType": "application/vnd.adobe.xed-full+json;version=1"
     }  
 }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `name` | De naam van het schema dat u wilt maken. |
| `schemaRef.id` | De id van het schema waarnaar u verwijst. |
| `schemaRef.contentType` | Bepaalt het reactieformaat van het referenced schema. Meer informatie dit gebied kan in [schema de ontwikkelaarsgids](../../xdm/api/schemas.md#lookup) worden gevonden |

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met informatie over uw onlangs gecreeerd schema terug.

>[!NOTE]
>
>De volgende reactie is afgebroken voor de ruimte.

```json
{
    "id": "4b64daa51b774cb2ac21b61d80125ed0",
    "version": 0,
    "name": "schemaName",
    "jsonSchema": "{\"id\":null,\"schema\":null,\"_refId\":null,\"title\":\"SimpleUser\",...,\"imsOrg\":\"{IMS_ORG}\",\"$id\":\"https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96\"}",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96",
        "contentType": "application/vnd.adobe.xed+json;version=1.0"
    }
}
```

## Schema maken met bestandsupload

U kunt een schema maken door een JSON-bestand te uploaden waaruit het kan worden omgezet.

**API-indeling**

```http
POST /schemas/upload
```

**Verzoek**

Met de volgende aanvraag kunt u een schema maken op basis van een geüpload JSON-bestand.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas/upload \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: multipart/form-data' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -F 'file=@{PATH_TO_FILE}.json'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met informatie over uw onlangs gecreeerd schema terug.

```json
{
    "id": "292add3716daffabf14b14259afc8fab",
    "version": 0,
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}
```

## Een specifiek schema ophalen

U kunt informatie over een specifiek schema terugwinnen door een verzoek van de GET aan het `/schemas` eindpunt te doen en identiteitskaart van het schema te verstrekken u wenst om in de verzoekweg terug te winnen.

**API-indeling**

```http
GET /schemas/{SCHEMA_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{SCHEMA_ID}` | De id van het schema dat u opzoekt. |

**Verzoek**

Het volgende verzoek wint informatie over het gespecificeerde schema terug.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas/0f868d3a1b804fb0abf738306290ae79 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met informatie over het gespecificeerde schema terug.

```json
{
    "id": "0f868d3a1b804fb0abf738306290ae79",
    "version": 0,
    "jsonSchema": {
        "title": "Sample schema",
        "description": "Sample description",
        "type": "object",
        "properties": {
            "_id": {
                "title": "Identifier",
                "description": "A unique identifier for the record.",
                "type": "string",
                "format": "uri-reference",
                "meta:xdmField": "@id",
                "meta:xdmType": "string"
            },
            "personalEmail": {
                "title": "Personal Email",
                "description": "A personal email address.",
                "type": "object",
                "properties": {
                    "primary": {
                        "title": "Primary",
                        "description": "Primary email indicator.\n\nA Profile can have only one `primary` email address at a given point of time.\n",
                        "type": "boolean",
                        "meta:xdmField": "xdm:primary",
                        "meta:xdmType": "boolean"
                    },
                    "address": {
                        "title": "Address",
                        "description": "The technical address, e.g 'name@domain.com' as commonly defined in RFC2822 and subsequent standards.",
                        "type": "string",
                        "format": "email",
                        "meta:xdmField": "xdm:address",
                        "meta:xdmType": "string"
                    }
                },
                "meta:xdmField": "xdm:personalEmail",
                "meta:referencedFrom": "https://ns.adobe.com/xdm/context/emailaddress",
                "meta:xdmType": "object"
            }
        },
        "imsOrg": "6A29340459CA8D350A49413A@AdobeOrg",
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc"
    },
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc",
        "contentType": "1.0"
    }
}
```
