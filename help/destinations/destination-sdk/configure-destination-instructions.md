---
description: Deze pagina beschrijft hoe te om de verwijzingsinformatie in de opties van de Configuratie voor de Doelen SDK te gebruiken om uw bestemming te vormen gebruikend Doel SDK.
seo-description: This page describes how to use the reference information in Configuration options for the Destinations SDK to configure your destination using Destination SDK.
seo-title: How to use Destination SDK to configure your destination
title: Hoe te om Doel SDK te gebruiken om uw bestemming te vormen
source-git-commit: 2841adc0ce212a945c35ba38209d4c00c519ad7b
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 0%

---

# Hoe te om Doel SDK te gebruiken om uw bestemming te vormen

## Overzicht {#overview}

Deze pagina beschrijft hoe te om de verwijzingsinformatie in [Opties van de Configuratie in Doelen SDK](./configuration-options.md) te gebruiken om uw bestemming te vormen. De stappen worden in de onderstaande volgorde weergegeven.

## Vereisten {#prerequisites}

Lees voordat u verdergaat met de onderstaande stappen de pagina [Bestemmings-SDK aan de slag](./getting-started.md) voor informatie over het verkrijgen van de vereiste verificatiereferenties en andere voorwaarden voor het werken met SDK-API&#39;s voor Adobe I/O.

## Stappen om de configuratieopties in Doel SDK aan opstelling te gebruiken uw bestemming {#steps}

![Afgedrukte stappen van het gebruiken van eindpunten van SDK van de Bestemming](./assets/destination-sdk-steps.png)

## Stap 1: Een server- en sjabloonconfiguratie maken {#create-server-template-configuration}

Begin door een server en malplaatjeconfiguratie te creëren gebruikend het `/destinations-server` eindpunt (lees [API verwijzing](./destination-server-api.md)). Raadpleeg [Server- en sjabloonspecificaties](./configuration-options.md#server-and-template) in de verwijzingssectie voor meer informatie over de server- en sjabloonconfiguratie.

Hieronder ziet u een voorbeeldconfiguratie. Merk op dat het malplaatje van de berichttransformatie in de `requestBody.value` parameter in stap 3 wordt gericht, [creeer transformatiemalplaatje](./configure-destination-instructions.md#create-transformation-template).

```json
POST platform.adobe.io/data/core/activation/authoring/destination-servers

{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{endpoint.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"insert after you create a template in step 3"
      },
      "contentType":"application/json"
   }
}
```

## Stap 2: Doelconfiguratie maken {#create-destination-configuration}

Hieronder getoond is een voorbeeldconfiguratie voor een bestemmingsmalplaatje, die door het `/destinations` API eindpunt te gebruiken wordt gecreeerd. Voor meer informatie over dit malplaatje, verwijs naar [Configuratie van de Bestemming](./destination-configuration.md).

```json
POST platform.adobe.io/data/core/activation/authoring/destinations
 
{
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":""
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "aggregationPolicyId":null,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":true,
            "groups":null
         },
         "splitUserById":true,
         "maxBatchAgeInSecs":360,
         "maxNumEventsInBatch":100
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "inputSchemaId":"cc8621770a9243b98aba4df79898b1ed"
}
```

## Stap 3: Sjabloon voor berichttransformatie maken - gebruik sjabloontaal om de indeling voor berichtuitvoer op te geven {#create-transformation-template}

Gebaseerd op de ladingen die uw bestemming steunt, moet u een malplaatje creëren dat het formaat van de uitgevoerde gegevens van Adobe XDM formaat in een formaat omzet dat door uw bestemming wordt gesteund. Zie sjabloonvoorbeelden in de sectie [Een sjabloontaal gebruiken voor de transformaties voor identiteit, kenmerken en segmentlidmaatschap](./message-format.md#using-templating) en het [sjabloonontwerpgereedschap](./create-template.md) van Adobe gebruiken.

## Stap 4: Configuratie van metagegevens voor het publiek maken {#create-audience-metadata-configuration}

Voor sommige bestemmingen, vereist de Bestemming SDK dat u een malplaatje van publieksmeta-gegevens vormt om publiek in uw bestemming programmatically tot stand te brengen bij te werken of te schrappen. Raadpleeg [Metabeheer van publiek](./audience-metadata-management.md) voor informatie over wanneer u deze configuratie moet instellen en hoe u dit moet doen.

## Stap 5: Referentieconfiguratie maken/verificatie instellen {#set-up-authentication}

Afhankelijk van of u `"authenticationRule": "CUSTOMER_AUTHENTICATION"` of `"authenticationRule": "PLATFORM_AUTHENTICATION"` in de bestemmingsconfiguratie hierboven specificeert, kunt u opstellingsauthentificatie voor uw bestemming door `/destination` of `/credentials` eindpunt te gebruiken.

* **Meest voorkomende gevallen**: Als u selecteerde  `"authenticationRule": "CUSTOMER_AUTHENTICATION"` en uw bestemming de OAuth 2 authentificatiemethode steunt, lees  [OAuth 2 authentificatie](./oauth2-authentication.md).
* Als u `"authenticationRule": "PLATFORM_AUTHENTICATION"` selecteerde, verwijs naar [Credentials configuratie](./credentials-configuration.md) in de verwijzingsdocumentatie.

## Stap 6: Doel testen {#test-destination}

Nadat u de bestemming hebt ingesteld met behulp van de sjablonen in de vorige stappen, kunt u het [doeltestgereedschap](./create-template.md) gebruiken om de integratie tussen Adobe Experience Platform en uw bestemming te testen.

Als deel van het proces om uw bestemming te testen, moet u het Experience Platform UI gebruiken om segmenten tot stand te brengen, die u aan uw bestemming zult activeren. Verwijs naar de twee hieronder middelen voor instructies hoe te om segmenten in Experience Platform tot stand te brengen:

* [Een pagina met segmentdocumentatie maken](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=en#create-segment)
* [Een doorlopende segmentvideo maken](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)


## Stap 7: Uw doel publiceren {#publish-destination}

Na het vormen van en het testen van uw bestemming. gebruik [bestemmings het publiceren API](./destination-publish-api.md) om uw configuratie aan Adobe voor overzicht voor te leggen.

## Stap 8: Uw doel documenteren {#document-destination}

Als u een Onafhankelijke Verkoper van de Software (ISV) of Integrator van het Systeem (SI) creërend een [geproduceerde integratie](./overview.md#productized-custom-integrations) bent, gebruik [zelfde documentatieproces](./docs-framework/documentation-instructions.md) om een pagina van de productdocumentatie voor uw bestemming in [de catalogus van de bestemmingen van het Experience League te creëren ](/help/destinations/catalog/overview.md).