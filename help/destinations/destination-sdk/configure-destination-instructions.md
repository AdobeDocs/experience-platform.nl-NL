---
description: Deze pagina maakt een lijst en beschrijft de stappen om een het stromen bestemming te vormen gebruikend de SDK van de Bestemming.
title: Hoe te om Bestemming SDK te gebruiken om een het stromen bestemming te vormen
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: a7c36f1a157b6020fede53e5c1074d966f26cf3d
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 0%

---

# Hoe te om Bestemming SDK te gebruiken om een het stromen bestemming te vormen

## Overzicht {#overview}

In deze pagina wordt beschreven hoe u de informatie in [Configuratieopties in de SDK Doelen](./configuration-options.md) en in andere bestemmingsSDK-functionaliteit en API-referentiedocumenten om een [streamingdoel](/help/destinations/destination-types.md#streaming-destinations). De stappen worden in de onderstaande volgorde weergegeven.

>[!NOTE]
>
>Het vormen van een partijbestemming door Doel SDK wordt momenteel niet gesteund.

## Vereisten {#prerequisites}

Lees de onderstaande stappen voordat u verdergaat [Aan de slag met de doel-SDK](./getting-started.md) pagina voor informatie over het verkrijgen van de noodzakelijke authentificatiegeloofsbrieven van de Adobe I/O en andere eerste vereisten om met de APIs van SDK van de Bestemming te werken.

## Stappen om de configuratieopties in Doel SDK aan opstelling te gebruiken uw bestemming {#steps}

![Afgedrukte stappen van het gebruiken van eindpunten van SDK van de Bestemming](./assets/destination-sdk-steps.png)

## Stap 1: Een server- en sjabloonconfiguratie maken {#create-server-template-configuration}

Begin door een server en malplaatjeconfiguratie te creëren gebruikend `/destinations-server` eindpunt (read [API-referentie](./destination-server-api.md)). Voor meer informatie over de server en malplaatjeconfiguratie, verwijs naar [Server- en sjabloonspecificaties](./configuration-options.md#server-and-template) in de referentiesectie.

Hieronder ziet u een voorbeeldconfiguratie. Merk op dat het malplaatje van de berichttransformatie in `requestBody.value` parameter wordt behandeld in stap 3; [Transformatiesjabloon maken](./configure-destination-instructions.md#create-transformation-template).

```json
POST platform.adobe.io/data/core/activation/authoring/destination-servers

{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
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

Hieronder weergegeven is een voorbeeldconfiguratie voor een doelsjabloon, die is gemaakt met de `/destinations` API-eindpunt. Voor meer informatie over deze sjabloon raadpleegt u [Doelconfiguratie](./destination-configuration.md).

Om de server en malplaatjeconfiguratie in stap 1 met deze bestemmingsconfiguratie te verbinden, voeg instantieidentiteitskaart van de server en malplaatjeconfiguratie als toe `destinationServerId` hier.

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
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
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
   ]
}
```

## Stap 3: Sjabloon voor berichttransformatie maken - gebruik sjabloontaal om de indeling voor berichtuitvoer op te geven {#create-transformation-template}

Gebaseerd op de ladingen die uw bestemming steunt, moet u een malplaatje creëren dat het formaat van de uitgevoerde gegevens van Adobe XDM formaat in een formaat omzet dat door uw bestemming wordt gesteund. Zie sjabloonvoorbeelden in de sectie [Een sjabloontaal gebruiken voor de transformaties voor identiteit, kenmerken en segmentlidmaatschap](./message-format.md#using-templating) en gebruiken de [sjabloonontwerpgereedschap](./create-template.md) verstrekt door Adobe.

Zodra u een malplaatje van de berichttransformatie hebt gecreeerd dat voor u werkt, voeg het aan de server en malplaatjeconfiguratie toe u in stap 1 creeerde.

## Stap 4: Configuratie van metagegevens voor het publiek maken {#create-audience-metadata-configuration}

Voor sommige bestemmingen, vereist de Bestemming SDK dat u een configuratie van publieksmeta-gegevens vormt om publiek in uw bestemming programmatically tot stand te brengen bij te werken of te schrappen. Zie [Metagegevensbeheer voor het publiek](./audience-metadata-management.md) voor informatie over wanneer u aan opstelling deze configuratie en hoe te om het moet doen.

Als u een configuratie van publieksmeta-gegevens gebruikt, moet u het met de bestemmingsconfiguratie verbinden u in stap 2 creeerde. Voeg instanceID van uw configuratie van publieksmeta-gegevens aan uw bestemmingsconfiguratie als toe `audienceTemplateId`.

## Stap 5: Referentieconfiguratie maken/verificatie instellen {#set-up-authentication}

Afhankelijk van of u `"authenticationRule": "CUSTOMER_AUTHENTICATION"` of `"authenticationRule": "PLATFORM_AUTHENTICATION"` in de bestemmingsconfiguratie hierboven, kunt u opstellingsauthentificatie voor uw bestemming door te gebruiken `/destination` of de `/credentials` eindpunt.

* **Meest voorkomende gevallen**: Als u `"authenticationRule": "CUSTOMER_AUTHENTICATION"` in de bestemmingsconfiguratie en uw bestemming steunt de OAuth 2 authentificatiemethode, gelezen [OAuth 2-verificatie](./oauth2-authentication.md).
* Als u `"authenticationRule": "PLATFORM_AUTHENTICATION"`, zie [Credentials configuratie](./credentials-configuration.md) in de referentiedocumentatie.

## Stap 6: Doel testen {#test-destination}

Nadat u de bestemming hebt ingesteld met de eindpunten van de configuratie in de vorige stappen, kunt u de opdracht [doeltestgereedschap](./create-template.md) om de integratie tussen Adobe Experience Platform en uw bestemming te testen.

Als deel van het proces om uw bestemming te testen, moet u het Experience Platform UI gebruiken om segmenten tot stand te brengen, die u aan uw bestemming zult activeren. Verwijs naar de twee hieronder middelen voor instructies hoe te om segmenten in Experience Platform tot stand te brengen:

* [Een pagina met segmentdocumentatie maken](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=en#create-segment)
* [Een doorlopende segmentvideo maken](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)

## Stap 7: Uw doel publiceren {#publish-destination}

Na het vormen van en het testen van uw bestemming, gebruik [doel-publicatie-API](./destination-publish-api.md) om uw configuratie ter controle naar Adobe te verzenden.

## Stap 8: Uw doel documenteren {#document-destination}

Als u een Onafhankelijke Verkoper van de Software (ISV) of Integrator van het Systeem (SI) creeert [productievere integratie](./overview.md#productized-custom-integrations), gebruikt u de [zelfbedieningsdocumentatie](./docs-framework/documentation-instructions.md) om een pagina van de productdocumentatie voor uw bestemming in te stellen in [Catalogus Experience League doelen](/help/destinations/catalog/overview.md).
