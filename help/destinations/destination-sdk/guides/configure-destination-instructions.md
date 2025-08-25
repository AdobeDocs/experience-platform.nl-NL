---
description: Op deze pagina vindt u een overzicht en beschrijving van de stappen voor het configureren van een streamingbestemming met Destination SDK.
title: Destination SDK gebruiken om een streamingbestemming te configureren
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: 560200a6553a1aae66c608eef7901b3248c886b4
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 0%

---

# Destination SDK gebruiken om een streamingbestemming te configureren

## Overzicht {#overview}

Deze pagina beschrijft hoe te om de informatie in [ opties van de Configuratie in Doelen SDK ](../functionality/configuration-options.md) en in andere functionaliteit van Destination SDK en API verwijzingsdocumenten te gebruiken om a [ het stromen bestemming ](../../destination-types.md#streaming-destinations) te vormen. De stappen worden in de onderstaande volgorde weergegeven.

## Vereisten {#prerequisites}

Alvorens aan de hieronder getoonde stappen vooruit te gaan, te lezen gelieve [ Destination SDK begonnen ](../getting-started.md) pagina voor informatie over het verkrijgen van de noodzakelijke de authentificatiegeloofsbrieven van Adobe I/O en andere eerste vereisten om met Destination SDK APIs te werken. Dit veronderstelt dat u het partnerschap en de toestemmingsvoorwaarden hebt voltooid en bereid bent te beginnen uw bestemming te ontwikkelen.

## Stappen om de configuratieopties in Destination SDK aan opstelling te gebruiken uw bestemming {#steps}

![ geïllustreerde stappen om eindpunten van Destination SDK te gebruiken ](../assets/guides/destination-sdk-steps.png)

## Stap 1: Maak een server en sjabloonconfiguratie {#create-server-template-configuration}

Begin door [ creërend een server en malplaatjeconfiguratie ](../authoring-api/destination-server/create-destination-server.md) gebruikend het `/destinations-server` eindpunt.

Hieronder ziet u een voorbeeldconfiguratie. Merk op dat het malplaatje van de berichttransformatie in de `requestBody.value` parameter in stap 3 wordt gericht, [ creeer transformatiemalplaatje ](#create-transformation-template).

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

Hieronder ziet u een voorbeeldconfiguratie voor een doelsjabloon die is gemaakt met het API-eindpunt van `/destinations` . Zie [ tot een bestemmingsconfiguratie ](../authoring-api/destination-configuration/create-destination-configuration.md) voor meer informatie leiden.

Als u de server- en sjabloonconfiguratie in stap 1 wilt verbinden met deze doelconfiguratie, voegt u de instantie-id van de server en de sjabloonconfiguratie hier `destinationServerId` toe.

>[!IMPORTANT]
>
>Om tot een correct gevormde (het stromen) bestemming in real time te leiden, moet u ** minstens één doelidentiteit in `identityNamespaces` toevoegen, zoals hieronder getoond. Als geen doelidentiteit wordt gevormd, zullen de gebruikers niet voorbij de [ stap van de Toewijzing ](../../ui/activate-segment-streaming-destinations.md#mapping) van het activeringswerkschema kunnen te werk gaan.

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
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false
   },
   "audienceMetadataConfig":{
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

## Stap 3: Creeer het malplaatje van de berichttransformatie - gebruik de malplaatjetaal om het formaat van de berichtoutput te specificeren {#create-transformation-template}

Op basis van de ladingen die uw bestemming ondersteunt, moet u een sjabloon maken die de indeling van de geëxporteerde gegevens van de Adobe XDM-indeling omzet in een indeling die door uw bestemming wordt ondersteund. Zie malplaatjevoorbeelden in de sectie [ Gebruikend een malplaatjetaal voor de identiteit, de attributen, en de transformaties van het publiekslidmaatschap ](../functionality/destination-server/message-format.md#using-templating) en gebruik het [ malplaatje auteursgereedschap ](../testing-api/streaming-destinations/create-template.md) dat door Adobe wordt verstrekt.

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

## Stap 4: configuratie van publiekmetagegevens maken {#create-audience-metadata-configuration}

Voor sommige bestemmingen, vereist Destination SDK dat u een configuratie van publieksmeta-gegevens vormt om publiek in uw bestemming programmatically tot stand te brengen bij te werken of te schrappen. Verwijs naar [ het meta-gegevensbeheer van het publiek ](../functionality/audience-metadata-management.md) voor informatie over wanneer u aan opstelling deze configuratie en hoe te om het te doen moet.

Als u een configuratie van publieksmeta-gegevens gebruikt, moet u het met de bestemmingsconfiguratie verbinden u in stap 2 creeerde. Voeg de instantie-id van de configuratie van de publieksmetagegevens als `audienceTemplateId` toe aan de doelconfiguratie.

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
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false
   },
   "audienceMetadataConfig":{
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


## Stap 5: De authentificatie van de opstelling {#set-up-authentication}

Afhankelijk van of u `"authenticationRule": "CUSTOMER_AUTHENTICATION"` of `"authenticationRule": "PLATFORM_AUTHENTICATION"` opgeeft in de bovenstaande doelconfiguratie, kunt u verificatie voor uw doel instellen met het `/destination` - of `/credentials` -eindpunt.

>[!NOTE]
>
>`CUSTOMER_AUTHENTICATION` is de gemeenschappelijkere van de twee authentificatieregels en is te gebruiken als u gebruikers om één of andere vorm van authentificatie aan uw bestemming alvorens zij opstelling een verbinding en uitvoergegevens vereist te verstrekken.

Als u `"authenticationRule": "CUSTOMER_AUTHENTICATION"` in de bestemmingsconfiguratie en uw bestemming selecteerde steunt OAuth 2 authentificatiemethode, lees [ OAuth 2 authentificatie ](../functionality/destination-configuration/oauth2-authorization.md).

Als u `"authenticationRule": "PLATFORM_AUTHENTICATION"` selecteerde, moet u de configuratie van de a [ geloofsbrieven ](../credentials-api/create-credential-configuration.md) tot stand brengen en identiteitskaart van het credentievoorwerp in de `authenticationId` parameter in de [ configuratie van de bestemmingslevering ](/help/destinations/destination-sdk/functionality/destination-configuration/destination-delivery.md#platform-authentication) overgaan.

## Stap 6: Test uw bestemming {#test-destination}

Na vestiging kunt uw bestemming die de configuratieeindpunten in de vorige stappen gebruiken, u het [ bestemmings testende hulpmiddel ](../testing-api/streaming-destinations/streaming-destination-testing-overview.md) gebruiken om de integratie tussen Adobe Experience Platform en uw bestemming te testen.

Als onderdeel van het proces om uw bestemming te testen, moet u Experience Platform UI gebruiken om segmenten tot stand te brengen, die u aan uw bestemming zult activeren. Raadpleeg de twee onderstaande bronnen voor instructies voor het maken van soorten publiek in Experience Platform:

* [Een pagina met publieksdocumentatie maken](/help/segmentation/ui/audience-portal.md#create-audience)
* [ creeer een analyse van de publieksvideo ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)

## Stap 7: Uw doel publiceren {#publish-destination}

>[!NOTE]
>
>Deze stap wordt niet vereist als u een privé bestemming voor uw eigen gebruik creeert, en kijkt niet om het in de catalogus van bestemmingen voor andere te gebruiken klanten te publiceren.

Na het vormen van en het testen van uw bestemming, gebruik [ bestemmings het publiceren API ](../publishing-api/create-publishing-request.md) om uw configuratie voor overzicht naar Adobe voor te leggen.

## Stap 8: Documenteer uw bestemming {#document-destination}

>[!NOTE]
>
>Deze stap wordt niet vereist als u een privé bestemming voor uw eigen gebruik creeert, en kijkt niet om het in de catalogus van bestemmingen voor andere te gebruiken klanten te publiceren.

Als u een Onafhankelijke Verkoper van de Software (ISV) of Integrator van het Systeem (SI) creërend a [ geproduceerde integratie ](../overview.md#productized-custom-integrations) bent, gebruik het [ zelfbedienings documentatieproces ](../docs-framework/documentation-instructions.md) om een pagina van de productdocumentatie voor uw bestemming in de [ de bestemmingscatalogus van Experience Platform ](/help/destinations/catalog/overview.md) tot stand te brengen.

## Stap 9: Doel verzenden voor Adobe-revisie {#submit-for-review}

>[!NOTE]
>
>Deze stap wordt niet vereist als u een privé bestemming voor uw eigen gebruik creeert, en kijkt niet om het in de catalogus van bestemmingen voor andere te gebruiken klanten te publiceren.

Tot slot alvorens de bestemming in de catalogus van Experience Platform kan worden gepubliceerd en aan alle klanten van Experience Platform zichtbaar, moet u de bestemming officieel voorleggen voor de controle van Adobe. Vind volledige informatie over hoe te [ voor overzicht voorleggen een geproduceerde die bestemming in Destination SDK ](../guides/submit-destination.md) wordt authored.
