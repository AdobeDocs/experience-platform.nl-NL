---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;replace;Replace;put;PUT
solution: Experience Platform
title: Een bron vervangen
description: De Registratie van het Schema staat u toe om een volledige middel door een verrichting van de PUT te vervangen. Deze verrichting herschrijft hoofdzakelijk het middel, daarom moet het verzoeklichaam alle gebieden omvatten die zouden worden vereist wanneer het creëren van een nieuwe middel gebruikend een verzoek van de POST.
topic: developer guide
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# Een bron vervangen

Met [!DNL Schema Registry] deze optie kunt u een volledige bron vervangen door een PUT-bewerking. Deze verrichting herschrijft hoofdzakelijk het middel, daarom moet het verzoeklichaam alle gebieden omvatten die zouden worden vereist wanneer het creëren van een nieuwe middel gebruikend een verzoek van de POST.

Deze methode is vooral handig als u veel informatie in de bron tegelijk wilt bijwerken.

>[!NOTE]
>
>Als u slechts een deel van een middel wilt bijwerken in plaats van het volledig te vervangen, zie het document bij het [bijwerken van een middel gebruikend een verrichting](update-resource.md)van de PATCH.

**API-indeling**

Een verzoek van de PUT kan slechts tegen middelen worden uitgevoerd die u in de huurderscontainer bepaalt.

```http
PUT /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parameter | Beschrijving |
| --- | --- |
| `{RESOURCE_TYPE}` | Het type bron dat vanuit de [!DNL Schema Library]bron moet worden bijgewerkt. Geldige typen zijn `datatypes`, `mixins`, `schemas`en `classes`. |
| `{RESOURCE_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` van de bron. |

**Verzoek**

Dit voorbeeldverzoek vervangt het datatype van de Bouw van het Bezit dat in een vorig voorbeeld werd gecreeerd. De aanvraaginstantie ziet er ongeveer hetzelfde uit als de POST die wordt gebruikt om het gegevenstype te maken, behalve dat het nu een bijgewerkte set velden bevat met nieuwe waarden die vervangen wat eerder is gedefinieerd.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.datatypes.24c643f618647344606222c494bd0102 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Construction",
        "description":"Information related to the construction of the property.",
        "type":"object",
        "properties": {
          "dateOpened": {
            "type":"string",
            "format": "date",
            "title": "Date Opened",
            "description": "The date the property was first opened."
          },
          "propertyType": {
            "type":"string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "standAlone",
              "highRise",
              "stripMall"
            ],
            "meta:enum": {
              "standAlone": "Stand-Alone Building",
              "highRise": "High Rise Building",
              "stripMall": "Strip Mall"
            }
          },
          "constructionCompany": {
            "type": "string",
            "title": "Construction Company",
            "description": "Name of the construction company that completed the construction of the property."
          },
          "totalSquareFootage": {
            "type": "integer",
            "title": "Total Square Footage",
            "description": "Total square footage of the property."
          }
        } 
      }'
```

**Antwoord**

Een succesvol antwoord geeft de details van het gegevenstype terug, die de bijgewerkte gebieden en de waarden tonen zoals die in het verzoek worden verstrekt.

```JSON
{
    "title": "Property Construction",
    "description": "Information related to the construction of the property.",
    "type": "object",
    "properties": {
        "dateOpened": {
            "type": "string",
            "format": "date",
            "title": "Date Opened",
            "description": "The date the property was first opened.",
            "meta:xdmType": "date"
        },
        "propertyType": {
            "type": "string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
                "standAlone",
                "highRise",
                "stripMall"
            ],
            "meta:enum": {
                "standAlone": "Stand-Alone Building",
                "highRise": "High Rise Building",
                "stripMall": "Strip Mall"
            },
            "meta:xdmType": "string"
        },
        "constructionCompany": {
            "type": "string",
            "title": "Construction Company",
            "description": "Name of the construction company that completed the construction of the property.",
            "meta:xdmType": "string"
        },
        "totalSquareFootage": {
            "type": "integer",
            "title": "Total Square Footage",
            "description": "Total square footage of the property.",
            "meta:xdmType": "int"
        }
    },
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.datatypes.24c643f618647344606222c494bd0102",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102",
    "version": "1.2",
    "meta:resourceType": "datatypes",
    "meta:registryMetadata": {
        "repo:createDate": 1552087079285,
        "repo:lastModifiedDate": 1552090569013,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```
