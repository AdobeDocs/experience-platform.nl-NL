---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een gegevenstype maken
topic: developer guide
translation-type: tm+mt
source-git-commit: b0d8c8ee4df11d601d8feb122c70a9cd5d7d5b77

---


# Een gegevenstype maken

Wanneer er gemeenschappelijke gegevensstructuren zijn die uw organisatie op veelvoudige manieren wenst te gebruiken, kunt u wensen om een gegevenstype te bepalen. De types van gegevens staan voor het verenigbare gebruik van multi-gebiedsstructuren, met meer flexibiliteit dan mengen toe omdat zij overal in een schema kunnen worden omvat door hen als `type` van een gebied toe te voegen.

Met andere woorden, met gegevenstypen kunt u één keer een objecthiërarchie definiëren en er in een veld op dezelfde manier naar verwijzen als elk ander scalair type.

**API-indeling**

```http
POST /tenant/datatypes
```

**Verzoek**

Voor het definiëren van een gegevenstype zijn geen velden `meta:extends` `meta:intendedToExtend` of velden nodig. Velden hoeven ook niet te zijn genest om conflicten te voorkomen.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Construction",
        "description":"Information related to the property construction",
        "type":"object",
        "properties": {
          "yearBuilt": {
            "type":"integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type":"string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "freeStanding",
              "mall",
              "shoppingCenter"
            ],
            "meta:enum": {
              "freeStanding": "Free Standing Building",
              "mall": "Mall Space",
              "shoppingCentre": "Shopping Center"
            }
          }
        } 
      }'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 (Gemaakt) en een payload die de details bevat van het nieuwe gegevenstype, inclusief de instructies `$id`, `meta:altId`en `version`. Deze drie waarden zijn read-only en door de Registratie van het Schema toegewezen.

```JSON
{
    "title": "Property Construction",
    "description": "Information related to the property construction",
    "type": "object",
    "properties": {
        "yearBuilt": {
            "type": "integer",
            "title": "Year Built",
            "description": "The year the property was constructed.",
            "meta:xdmType": "int"
        },
        "constructionType": {
            "type": "string",
            "title": "Construction Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
                "freeStanding",
                "mall",
                "shoppingCenter"
            ],
            "meta:enum": {
                "freeStanding": "Free Standing Building",
                "mall": "Mall Space",
                "shoppingCentre": "Shopping Center"
            },
            "meta:xdmType": "string"
        }
    },
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.datatypes.24c643f618647344606222c494bd0102",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102",
    "version": "1.0",
    "meta:resourceType": "datatypes",
    "meta:registryMetadata": {
        "repo:createDate": 1552087079285,
        "repo:lastModifiedDate": 1552087079285,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

Het uitvoeren van een GET verzoek om van alle gegevenstypes in de huurderscontainer een lijst te maken zou nu het gegevenstype van de Bouw van het Bezit omvatten. U kunt ook een opzoekaanvraag (GET) uitvoeren met de URL-gecodeerde `$id` URI om het nieuwe gegevenstype direct weer te geven. Zorg ervoor dat u de code opneemt `version` in de koptekst Accepteren voor een opzoekverzoek.
