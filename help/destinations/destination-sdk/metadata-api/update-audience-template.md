---
description: Deze pagina illustreert de API-aanroep die wordt gebruikt om een publiekssjabloon bij te werken via Adobe Experience Platform Destination SDK.
title: Een publiekssjabloon bijwerken
exl-id: 8185a015-256d-46a7-af33-8475832fb6c1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# Een publiekssjabloon bijwerken

>[!IMPORTANT]
>
>**API eindpunt**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Deze pagina illustreert de API-aanvraag en lading die u kunt gebruiken om een publiekssjabloon bij te werken met behulp van het API-eindpunt `/authoring/audience-templates` .

Voor een gedetailleerde beschrijving van de mogelijkheden die u door dit eindpunt kunt vormen, zie [&#x200B; beheer van publieksmeta-gegevens &#x200B;](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Alle parameternamen en waarden die door Destination SDK worden gesteund zijn **gevoelig geval**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Aan de slag met API-bewerkingen voor publiekssjablonen {#get-started}

Alvorens verder te gaan, te herzien gelieve [&#x200B; begonnen gids &#x200B;](../getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings authoring en vereiste kopballen te verkrijgen.

## Een publiekssjabloon bijwerken {#create}

U kunt een [&#x200B; bestaand &#x200B;](create-audience-template.md) publiekssjabloon bijwerken door een `PUT` verzoek aan het `/authoring/audience-templates` eindpunt met de bijgewerkte nuttige lading te doen.

Om een bestaand publiekssjabloon en zijn overeenkomstige `{INSTANCE_ID}` te verkrijgen, zie het artikel over [&#x200B; het terugwinnen van een publiekssjabloon &#x200B;](retrieve-audience-template.md).

**API formaat**

```http
PUT /authoring/audience-templates/{INSTANCE_ID}
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{INSTANCE_ID}` | De id van de publiekssjabloon die u wilt bijwerken. Om een bestaand publiekssjabloon en zijn overeenkomstige `{INSTANCE_ID}` te verkrijgen, zie [&#x200B; een publiekssjabloon &#x200B;](retrieve-audience-template.md) terugwinnen. |

Het volgende verzoek werkt een bestaand malplaatje van publiekmeta-gegevens bij, dat door de parameters wordt gevormd die in de lading worden verstrekt.

+++verzoek

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/audience-templates/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
  "metadataTemplate": {
    "name": "Test Webhook Audience Template",
    "create": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/segments",
      "httpMethod": "POST",
      "headers": [
        {
          "value": "application/json",
          "header": "Content-Type"
        },
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "requestBody": {
        "json": {
          "name": "{{segment.name}}",
          "type": "segment",
          "metadata": {
            "org_id": "{{destination.imsOrgId}}",
            "sandbox": "{{destination.sandboxName}}",
            "destination_id": "{{destination.id}}",
            "destination_name": "{{destination.name}}",
            "segmentEnrichmentAttributes": "{% set columns = [] %}{% for atr in segmentEnrichmentAttributes %}{% set columns = columns|merge([atr.source]) %}{% endfor %}{{ columns | toJson }}"
          },
          "external_id": "{{segment.id}}"
        }
      },
      "responseFields": [
        {
          "value": "{{headers.X-Request-Id}}",
          "name": "externalAudienceId"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "update": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/segments/{{segment.alias}}",
      "httpMethod": "PUT",
      "headers": [
        {
          "value": "application/json",
          "header": "Content-Type"
        },
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "requestBody": {
        "json": {
          "name": "{{segment.name}}",
          "type": "segment",
          "metadata": {
            "org_id": "{{destination.imsOrgId}}",
            "sandbox": "{{destination.sandboxName}}",
            "destination_id": "{{destination.id}}",
            "destination_name": "{{destination.name}}",
            "segmentEnrichmentAttributes": "{% set columns = [] %}{% for atr in segmentEnrichmentAttributes %}{% set columns = columns|merge([atr.source]) %}{% endfor %}{{ columns | toJson }}"
          },
          "external_id": "{{segment.id}}"
        }
      },
      "responseFields": [
        {
          "value": "{{headers.X-Request-Id}}",
          "name": "externalAudienceId"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "delete": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/segments/{{segment.alias}}",
      "httpMethod": "DELETE",
      "headers": [
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "createDestination": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/createDestination",
      "httpMethod": "POST",
      "headers": [
        {
          "value": "application/json",
          "header": "Content-Type"
        },
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "requestBody": {
        "json": {
          "name": "{{destination.name}}",
          "type": "destination",
          "metadata": {
            "org_id": "{{destination.imsOrgId}}",
            "sandbox": "{{destination.sandboxName}}",
            "destination_id": "{{destination.id}}",
            "destination_name": "{{destination.name}}",
            "enrichmentAttributes": "{{destination.enrichmentAttributes}}"
          },
          "external_id": "{{destination.id}}"
        }
      },
      "responseFields": [
        {
          "value": "{{headers.X-Request-Id}}",
          "name": "externalAudienceId"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "updateDestination": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/updateDestination",
      "httpMethod": "POST",
      "headers": [
        {
          "value": "application/json",
          "header": "Content-Type"
        },
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "requestBody": {
        "json": {
          "name": "{{destination.name}}",
          "type": "destination",
          "metadata": {
            "org_id": "{{destination.imsOrgId}}",
            "sandbox": "{{destination.sandboxName}}",
            "destination_id": "{{destination.id}}",
            "destination_name": "{{destination.name}}",
            "enrichmentAttributes": "{{destination.enrichmentAttributes}}"
          },
          "external_id": "{{destination.id}}"
        }
      },
      "responseFields": [
        {
          "value": "{{headers.X-Request-Id}}",
          "name": "externalAudienceId"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "deleteDestination": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/deleteDestination",
      "httpMethod": "DELETE",
      "headers": [
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    }
  },
  "validations":[
      {
         "field":"string",
         "regex":"string"
      }
   ]
}'
```

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met details van uw bijgewerkte publiekssjabloon terug.

+++

## API-foutafhandeling

Destination SDK API-eindpunten volgen de algemene beginselen van Experience Platform API-foutberichten. Verwijs naar [&#x200B; API statuscodes &#x200B;](../../../landing/troubleshooting.md#api-status-codes) en [&#x200B; de fouten van de verzoekkopbal &#x200B;](../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van Experience Platform.

## Volgende stappen

Na het lezen van dit document weet u nu wanneer u publiekssjablonen gebruikt en hoe u een publiekssjabloon kunt bijwerken met het API-eindpunt van `/authoring/audience-templates` . Lees [&#x200B; hoe te om Destination SDK te gebruiken om uw bestemming &#x200B;](../guides/configure-destination-instructions.md) te vormen om te begrijpen waar deze stap in het proces past om uw bestemming te vormen.
