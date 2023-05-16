---
description: Deze pagina maakt een lijst en beschrijft de stappen om een het stromen bestemming te vormen gebruikend Destination SDK.
title: Gebruik Destination SDK om een streamingbestemming te configureren
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: 0befd65b91e49cacab67c76fd9ed5d77bf790b9d
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---

# Gebruik Destination SDK om een streamingbestemming te configureren

## Overzicht {#overview}

In deze pagina wordt beschreven hoe u de informatie in [Configuratieopties in de SDK Doelen](../functionality/configuration-options.md) en in andere Destination SDK-functionaliteit en API-referentiedocumenten om een [streamingdoel](../../destination-types.md#streaming-destinations). De stappen worden in de onderstaande volgorde weergegeven.

## Vereisten {#prerequisites}

Lees de onderstaande stappen voordat u verdergaat [Aan de slag met Destination SDK](../getting-started.md) pagina voor informatie over het verkrijgen van de vereiste autorisatiegeloofsbrieven van de Adobe I/O en andere eerste vereisten om met Destination SDK APIs te werken. Dit veronderstelt dat u het partnerschap en de toestemmingsvoorwaarden hebt voltooid en bereid bent te beginnen uw bestemming te ontwikkelen.

## Stappen om de configuratieopties in Destination SDK aan opstelling te gebruiken uw bestemming {#steps}

![Gedetailleerde stappen voor het gebruik van Destination SDK-eindpunten](../assets/guides/destination-sdk-steps.png)

## Stap 1: Een server- en sjabloonconfiguratie maken {#create-server-template-configuration}

Beginnen met [een server- en sjabloonconfiguratie maken](../authoring-api/destination-server/create-destination-server.md) met de `/destinations-server` eindpunt.

Hieronder ziet u een voorbeeldconfiguratie. Merk op dat het malplaatje van de berichttransformatie in `requestBody.value` parameter wordt behandeld in stap 3; [Transformatiesjabloon maken](#create-transformation-template).

```shell
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

```json {line-numbers="true" highlight="14"}
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

Hieronder weergegeven is een voorbeeldconfiguratie voor een doelsjabloon, die is gemaakt met de `/destinations` API-eindpunt. Zie [een doelconfiguratie maken](../authoring-api/destination-configuration/create-destination-configuration.md) voor meer informatie .

Om de server en malplaatjeconfiguratie in stap 1 met deze bestemmingsconfiguratie te verbinden, voeg instantieidentiteitskaart van de server en malplaatjeconfiguratie als toe `destinationServerId` hier.

>[!IMPORTANT]
>
>Als u een correct geconfigureerde bestemming in real time (streaming) wilt maken, *moet* minstens één doelidentiteit toevoegen in `identityNamespaces`, zoals hieronder weergegeven. Als geen doelidentiteit wordt gevormd, zullen de gebruikers niet voorbij voorbij kunnen te werk gaan [Toewijzingsstap](../../ui/activate-segment-streaming-destinations.md#mapping) van de activeringsworkflow.

```shell
POST platform.adobe.io/data/core/activation/authoring/destinations
```

```json {line-numbers="true" highlight="74"}
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
   "audienceMetadataConfig":{
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
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000
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

Gebaseerd op de ladingen die uw bestemming steunt, moet u een malplaatje creëren dat het formaat van de uitgevoerde gegevens van Adobe XDM formaat in een formaat omzet dat door uw bestemming wordt gesteund. Zie sjabloonvoorbeelden in de sectie [Een sjabloontaal gebruiken voor de transformaties voor identiteit, kenmerken en segmentlidmaatschap](../functionality/destination-server/message-format.md#using-templating) en gebruiken de [sjabloonontwerpgereedschap](../testing-api/streaming-destinations/create-template.md) verstrekt door Adobe.

Zodra u een malplaatje van de berichttransformatie hebt gecreeerd dat voor u werkt, voeg het aan de server en malplaatjeconfiguratie toe u in stap 1 creeerde.

```json {line-numbers="true" highlight="13-14"}
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
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{\n    \"users\": [\n        {% for profile in input.profiles %}\n            {{profile|raw}}{% if not loop.last %},{% endif %}\n        {% endfor %}\n    ]\n}"
      },
      "contentType":"application/json"
   }
}
```

## Stap 4: Configuratie van metagegevens voor het publiek maken {#create-audience-metadata-configuration}

Voor sommige bestemmingen, vereist Destination SDK dat u een configuratie van publieksmeta-gegevens vormt om publiek in uw bestemming programmatically tot stand te brengen bij te werken of te schrappen. Zie [Metagegevensbeheer voor het publiek](../functionality/audience-metadata-management.md) voor informatie over wanneer u aan opstelling deze configuratie en hoe te om het moet doen.

Als u een configuratie van publieksmeta-gegevens gebruikt, moet u het met de bestemmingsconfiguratie verbinden u in stap 2 creeerde. Voeg instanceID van uw configuratie van publieksmeta-gegevens aan uw bestemmingsconfiguratie als toe `audienceTemplateId`.

```json {line-numbers="true" highlight="53"}
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
   "audienceMetadataConfig":{
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
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000
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


## Stap 5: Verificatie instellen {#set-up-authentication}

Afhankelijk van of u `"authenticationRule": "CUSTOMER_AUTHENTICATION"` of `"authenticationRule": "PLATFORM_AUTHENTICATION"` in de bestemmingsconfiguratie hierboven, kunt u opstellingsauthentificatie voor uw bestemming door te gebruiken `/destination` of de `/credentials` eindpunt.

Als u `"authenticationRule": "CUSTOMER_AUTHENTICATION"` in de bestemmingsconfiguratie en uw bestemming steunt de OAuth 2 authentificatiemethode, gelezen [OAuth 2-verificatie](../functionality/destination-configuration/oauth2-authentication.md).

Als u `"authenticationRule": "PLATFORM_AUTHENTICATION"`moet u een [aanmeldingsconfiguratie](../credentials-api/create-credential-configuration.md).

## Stap 6: Doel testen {#test-destination}

Nadat u de bestemming hebt ingesteld met de eindpunten van de configuratie in de vorige stappen, kunt u de opdracht [doeltestgereedschap](../testing-api/streaming-destinations/streaming-destination-testing-overview.md) om de integratie tussen Adobe Experience Platform en uw bestemming te testen.

Als deel van het proces om uw bestemming te testen, moet u het Experience Platform UI gebruiken om segmenten tot stand te brengen, die u aan uw bestemming zult activeren. Verwijs naar de twee hieronder middelen voor instructies hoe te om segmenten in Experience Platform tot stand te brengen:

* [Een pagina met segmentdocumentatie maken](/help/segmentation/ui/overview.md#create-segment)
* [Een doorlopende segmentvideo maken](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)

## Stap 7: Uw doel publiceren {#publish-destination}

>[!NOTE]
>
>Deze stap wordt niet vereist als u een privé bestemming voor uw eigen gebruik creeert, en kijkt niet om het in de catalogus van bestemmingen voor andere te gebruiken klanten te publiceren.

Na het vormen van en het testen van uw bestemming, gebruik [doel-publicatie-API](../publishing-api/create-publishing-request.md) om uw configuratie ter controle naar Adobe te verzenden.

## Stap 8: Uw doel documenteren {#document-destination}

>[!NOTE]
>
>Deze stap wordt niet vereist als u een privé bestemming voor uw eigen gebruik creeert, en kijkt niet om het in de catalogus van bestemmingen voor andere te gebruiken klanten te publiceren.

Als u een Onafhankelijke Verkoper van de Software (ISV) of Integrator van het Systeem (SI) creeert [productievere integratie](../overview.md#productized-custom-integrations), gebruikt u de [zelfbedieningsdocumentatie](../docs-framework/documentation-instructions.md) om een pagina van de productdocumentatie voor uw bestemming in te stellen in [Catalogus Experience Platform doelen](/help/destinations/catalog/overview.md).

## Stap 9: Doel verzenden voor revisie Adobe {#submit-for-review}

>[!NOTE]
>
>Deze stap wordt niet vereist als u een privé bestemming voor uw eigen gebruik creeert, en kijkt niet om het in de catalogus van bestemmingen voor andere te gebruiken klanten te publiceren.

Tot slot kan de bestemming in de catalogus van het Experience Platform worden gepubliceerd en zichtbaar aan alle klanten van het Experience Platform, u de bestemming voor overzicht van de Adobe officieel moeten voorleggen. Volledige informatie over hoe te vinden [een in Destination SDK gefabriceerde bestemming ter controle indienen](../guides/submit-destination.md).
