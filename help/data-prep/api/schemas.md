---
keywords: Experience Platform;home;populaire onderwerpen;gegevens prep;api-gids;schema's;
solution: Experience Platform
title: Schemas API Endpoint
description: U kunt het `/schema's' eindpunt in Adobe Experience Platform API gebruiken om schema's voor gebruik met Mapper in Experience Platform programmatically terug te winnen, tot stand te brengen en bij te werken.
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 1%

---



# Schemas, eindpunt

Schema&#39;s kunnen met Mapper worden gebruikt om ervoor te zorgen dat de gegevens die u in Adobe Experience Platform hebt ingevoerd overeenkomen met wat u wilt opnemen. U kunt het `/schemas` eindpunt gebruiken om, douaneschema&#39;s programmatically tot stand te brengen voor gebruik met Mapper in Experience Platform.

>[!NOTE]
>
>Schema&#39;s die met dit eindpunt worden gemaakt, worden uitsluitend gebruikt met Mapper- en toewijzingssets. Om schema&#39;s tot stand te brengen die door andere diensten van Experience Platform toegankelijk zijn, te lezen gelieve de [ de ontwikkelaarsgids van de Registratie van het Schema ](../../xdm/api/schemas.md).

## Alle schema&#39;s ophalen

U kunt een lijst van alle beschikbare schema&#39;s van de Apper voor uw organisatie terugwinnen door een GET verzoek aan het `/schemas` eindpunt te doen.

**API formaat**

Het `/schemas` eindpunt steunt verscheidene vraagparameters om u te helpen uw resultaten filtreren. Hoewel de meeste van deze parameters optioneel zijn, wordt het gebruik ervan sterk aanbevolen om de kostbare overhead te helpen verminderen. U moet echter zowel de parameters `start` als `limit` opnemen als onderdeel van uw aanvraag. De veelvoudige parameters kunnen worden omvat, die door ampersands (`&`) worden gescheiden.

```http
GET /schemas?limit={LIMIT}&start={START}
GET /schemas?limit={LIMIT}&start={START}&name={NAME}
GET /schemas?limit={LIMIT}&start={START}&orderBy={ORDER_BY}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{LIMIT}` | **Vereiste**. Geeft het aantal geretourneerde schema&#39;s aan. |
| `{START}` | **Vereiste**. Hiermee bepaalt u de verschuiving van de resultatenpagina&#39;s. Als u de eerste pagina met resultaten wilt ophalen, stelt u de waarde in op `start=0` . |
| `{NAME}` | Hiermee filtert u het schema op basis van de naam. |
| `{ORDER_BY}` | Sorteert de volgorde van de resultaten. De ondersteunde velden zijn `modifiedDate` en `createdDate` . U kunt de eigenschap voorvullen met `+` of `-` om deze in oplopende of aflopende volgorde te sorteren. |

**Verzoek**

Het volgende verzoek wint de laatste twee gecreeerde schema&#39;s voor uw organisatie terug.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas&start=0&limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

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

U kunt een schema tot stand brengen om tegen te bevestigen door een POST- verzoek aan het `/schemas` eindpunt te doen. Er zijn drie manieren om een schema tot stand te brengen: het verzenden van het Schema van a [ JSON ](https://json-schema.org/), gebruikend steekproefgegevens, of het van verwijzingen voorzien van een bestaand schema XDM.

```http
POST /schemas
```

### Een JSON-schema gebruiken

**Verzoek**

Het volgende verzoek laat u een schema tot stand brengen door a [ Schema JSON ](https://json-schema.org/) te verzenden.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

**Reactie**

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

**Reactie**

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `schemaRef.contentType` | Bepaalt het reactieformaat van het referenced schema. Meer informatie dit gebied kan in de [ gids van de schemaontwikkelaar van de schemacontrole ](../../xdm/api/schemas.md#lookup) worden gevonden |

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met informatie over uw onlangs gecreeerd schema terug.

>[!NOTE]
>
>De volgende reactie is afgebroken voor de ruimte.

```json
{
    "id": "4b64daa51b774cb2ac21b61d80125ed0",
    "version": 0,
    "name": "schemaName",
    "jsonSchema": "{\"id\":null,\"schema\":null,\"_refId\":null,\"title\":\"SimpleUser\",...,\"imsOrg\":\"{ORG_ID}\",\"$id\":\"https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96\"}",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96",
        "contentType": "application/vnd.adobe.xed+json;version=1.0"
    }
}
```

## Schema maken met bestandsupload

U kunt een schema maken door een JSON-bestand te uploaden waaruit het kan worden omgezet.

**API formaat**

```http
POST /schemas/upload
```

**Verzoek**

Met de volgende aanvraag kunt u een schema maken van een geüpload JSON-bestand.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas/upload \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: multipart/form-data' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -F 'file=@{PATH_TO_FILE}.json'
```

**Reactie**

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

U kunt informatie over een specifiek schema terugwinnen door een GET- verzoek aan het `/schemas` eindpunt te doen en identiteitskaart van het schema te verstrekken u in de verzoekweg wenst terug te winnen.

**API formaat**

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

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
