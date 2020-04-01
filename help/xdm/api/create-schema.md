---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een schema maken
topic: developer guide
translation-type: tm+mt
source-git-commit: 162316c3b908ffa87d8df4dff72e26ba237993db

---


# Een schema maken

Een schema kan als blauwdruk voor de gegevens worden beschouwd u in het Platform van de Ervaring wilt opnemen. Elk schema bestaat uit een klasse en nul of meer mixen. Met andere woorden, u moet geen mixin toevoegen om een schema te bepalen, maar in de meeste gevallen zal minstens één mixin worden gebruikt.

Het proces van de schemacompositie begint door een klasse toe te wijzen. De klasse definieert de belangrijkste gedragsaspecten van de gegevens (record- of tijdreeks) en de minimale velden die vereist zijn om de gegevens te beschrijven die worden ingevoerd.

**API-indeling**

```http
POST /tenant/schemas
```

**Verzoek**

De aanvraag moet een `allOf` attribuut bevatten dat naar de klasse `$id` van verwijst. Dit attribuut bepaalt de &quot;basisklasse&quot;die het schema zal uitvoeren. In dit voorbeeld is de basisklasse een klasse &quot;Eigenschapinformatie&quot; die eerder is gemaakt.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `allOf > $ref` | De `$id` waarde van de klasse het nieuwe schema zal uitvoeren. |

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 (Gemaakt) en een payload die de details bevat van het nieuwe schema, inclusief het schema `$id`, `meta:altId`en `version`. Deze waarden zijn alleen-lezen en worden toegewezen door het schemaregister.

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
    "imsOrg": "{IMS_ORG}",
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

Het uitvoeren van een GET verzoek om van alle schema&#39;s in de huurderscontainer een lijst te maken zou nu het schema van de Informatie van het Bezit omvatten, of u kunt een raadpleging (KRIJGEN) verzoek uitvoeren gebruikend URL-Gecodeerde `$id` URI om het nieuwe schema direct te bekijken. Vergeet niet de header Accepteren op te nemen `version` in alle opzoekverzoeken.
