---
description: Deze pagina illustreert de API vraag die wordt gebruikt om een publiekssjabloon door Adobe Experience Platform Destination SDK tot stand te brengen.
title: Een publiekssjabloon maken
exl-id: 98d30002-d462-4008-9337-7de0cd608194
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# Een publiekssjabloon maken

>[!IMPORTANT]
>
>**API eindpunt**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Voor sommige bestemmingen die met Destination SDK worden gecreeerd, moet u een configuratie van publieksmeta-gegevens creëren programmatically om, publieksmeta-gegevens in de bestemming te creëren bij te werken of te schrappen. Op deze pagina ziet u hoe u het API-eindpunt `/authoring/audience-templates` gebruikt om de configuratie te maken.

Voor een gedetailleerde beschrijving van de mogelijkheden die u door dit eindpunt kunt vormen, zie [ beheer van publieksmeta-gegevens ](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Alle parameternamen en waarden die door Destination SDK worden gesteund zijn **gevoelig geval**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Aan de slag met API-bewerkingen voor publiekssjablonen {#get-started}

Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](../getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings authoring en vereiste kopballen te verkrijgen.

## Een publiekssjabloon maken {#create}

U kunt een nieuwe publiekssjabloon maken door een `POST` -aanvraag in te dienen bij het `/authoring/audience-templates` -eindpunt.

**API formaat**

```http
POST /authoring/audience-templates
```

+++verzoek

Het volgende verzoek leidt tot een nieuw publieksmalplaatje, dat door de parameters wordt gevormd die in de lading worden verstrekt. De onderstaande lading bevat alle parameters die door het `/authoring/audience-templates` -eindpunt worden geaccepteerd. Merk op dat u niet alle parameters op de vraag moet toevoegen en dat het malplaatje, volgens uw API vereisten aanpasbaar is.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/audience-templates \
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

| Eigenschap | Type | Beschrijving |
| -------- | ----------- | ----------- |
| `name` | String | De naam van het malplaatje van publieksmeta-gegevens voor uw bestemming. Deze naam zal in om het even welk partner-specifiek foutenmelding in het gebruikersinterface van Experience Platform verschijnen. |
| `url` | String | De URL en het eindpunt van uw API, die voor het creëren van, het bijwerken van, het schrappen van, of het bevestigen van publiek en/of dataflows in uw platform wordt gebruikt. Twee voorbeelden uit de branche zijn: `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` en `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}` . |
| `httpMethod` | String | De methode die op uw eindpunt wordt gebruikt programmatically tot stand te brengen, bij te werken, te schrappen, of het publiek in uw bestemming te bevestigen. Bijvoorbeeld: `POST`, `PUT`, `DELETE` |
| `headers.header` | String | Geeft alle HTTP-headers op die moeten worden toegevoegd aan de aanroep van de API. Bijvoorbeeld: `"Content-Type"` |
| `headers.value` | String | Geeft de waarde aan van HTTP-headers die moeten worden toegevoegd aan de aanroep van de API. Bijvoorbeeld: `"application/x-www-form-urlencoded"` |
| `requestBody` | String | Hier geeft u de inhoud op van de berichttekst die naar de API moet worden verzonden. Welke parameters aan het `requestBody` -object moeten worden toegevoegd, is afhankelijk van de velden die de API accepteert. Verwijs naar de [ gesteunde documentatie van macro&#39;s ](../functionality/audience-metadata-management.md#macros) om te leren wat u in het berichtlichaam kunt omvatten. |
| `responseFields.name` | String | Geef antwoordvelden op die de API retourneert wanneer deze wordt aangeroepen. Bijvoorbeeld, verwijs naar de [ malplaatjevoorbeelden ](../functionality/audience-metadata-management.md#examples) in het document van de de meta-gegevensfunctionaliteit van het publiek. |
| `responseFields.value` | String | Geef de waarde op van de reactievelden die de API retourneert wanneer deze wordt aangeroepen. |
| `responseErrorFields.name` | String | Geef antwoordvelden op die de API retourneert wanneer deze wordt aangeroepen. Bijvoorbeeld, verwijs naar de [ malplaatjevoorbeelden ](../functionality/audience-metadata-management.md#examples) in het document van de de meta-gegevensfunctionaliteit van het publiek. |
| `responseErrorFields.value` | String | Parseert om het even welke foutenmeldingen die op API vraagreacties van uw bestemming zijn teruggekeerd. Deze foutberichten worden weergegeven in de gebruikersinterface van Experience Platform. |
| `validations.field` | String | Geeft aan of validaties voor velden moeten worden uitgevoerd voordat API-aanroepen naar uw doel worden uitgevoerd. U kunt bijvoorbeeld `{{validations.accountId}}` gebruiken om de account-id van de gebruiker te valideren. |
| `validations.regex` | String | Hiermee geeft u aan hoe het veld moet worden gestructureerd voordat de validatie wordt doorgegeven. |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met details van uw onlangs gecreeerde publiekssjabloon terug.

+++

## API-foutafhandeling

Destination SDK API-eindpunten volgen de algemene beginselen van Experience Platform API-foutberichten. Verwijs naar [ API statuscodes ](../../../landing/troubleshooting.md#api-status-codes) en [ de fouten van de verzoekkopbal ](../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van Experience Platform.

## Volgende stappen

Nadat u dit document hebt gelezen, weet u nu wanneer u publiekssjablonen wilt gebruiken en hoe u een publiekssjabloon kunt configureren met het API-eindpunt van `/authoring/audience-templates` . Lees [ hoe te om Destination SDK te gebruiken om uw bestemming ](../guides/configure-destination-instructions.md) te vormen om te begrijpen waar deze stap in het proces past om uw bestemming te vormen.
