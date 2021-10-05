---
description: Deze pagina bevat een overzicht en beschrijving van alle API-bewerkingen die u kunt uitvoeren met het API-eindpunt `/authoring/destination.
title: API-eindpuntbewerkingen voor doelen
exl-id: 96755e9d-be62-432f-b985-91330575b395
source-git-commit: c334a11ff6a03b38883a5319bc41cbe3f93c0289
workflow-type: tm+mt
source-wordcount: '2407'
ht-degree: 1%

---

# API-bewerkingen voor bestemmingspunten {#destination-configuration}

>[!IMPORTANT]
>
>**API-eindpunt**:  `platform.adobe.io/data/core/activation/authoring/destinations`

Deze pagina bevat een overzicht en beschrijving van alle API-bewerkingen die u kunt uitvoeren met het API-eindpunt `/authoring/destinations`. Voor een beschrijving van de functionaliteit die door dit eindpunt wordt gesteund, lees [bestemmingsconfiguratie](./destination-configuration.md).

## Aan de slag met doel-API-bewerkingen {#get-started}

Alvorens verder te gaan, te herzien [begonnen gids](./getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmingsauteur en vereiste kopballen te verkrijgen.

## Configuratie maken voor een doel {#create}

U kunt een nieuwe bestemmingsconfiguratie tot stand brengen door een verzoek van de POST aan het `/authoring/destinations` eindpunt te doen.

**API-indeling**


```http
POST /authoring/destinations
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe bestemmingsconfiguratie, die door de parameters wordt gevormd die in de lading worden verstrekt. De hieronder vermelde lading omvat alle parameters die door het `/authoring/destinations` eindpunt worden goedgekeurd. Merk op dat u niet alle parameters op de vraag moet toevoegen en dat het malplaatje, volgens uw API vereisten aanpasbaar is.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
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
   "schemaConfig":{
      "profileFields":[
         {
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `name` | Tekenreeks | Geeft de titel van het doel in de catalogus Experience Platform aan |
| `description` | Tekenreeks | Geef een beschrijving op die Adobe in de Experience Platform-doelcatalogus voor uw doelkaart zal gebruiken. Doel voor niet meer dan 4-5 zinnen. |
| `status` | Tekenreeks | Geeft de levenscyclusstatus van de doelkaart aan. Accepteerde waarden zijn `TEST`, `PUBLISHED` en `DELETED`. Gebruik `TEST` wanneer u eerst uw bestemming vormt. |
| `customerAuthenticationConfigurations` | Tekenreeks | Wijst op de configuratie die wordt gebruikt om de klanten van het Experience Platform aan uw server voor authentiek te verklaren. Zie `authType` hieronder voor geaccepteerde waarden. |
| `customerAuthenticationConfigurations.authType` | Tekenreeks | Accepteerde waarden zijn `OAUTH2, BEARER`. |
| `customerDataFields.name` | Tekenreeks | Geef een naam op voor het aangepaste veld dat u introduceert. |
| `customerDataFields.type` | Tekenreeks | Hiermee geeft u aan welk type aangepast veld u wilt gebruiken. Accepteerde waarden zijn `string`, `object`, `integer` |
| `customerDataFields.title` | Tekenreeks | Hiermee wordt de naam van het veld aangegeven, zoals deze wordt weergegeven door klanten in de gebruikersinterface van het Experience Platform |
| `customerDataFields.description` | Tekenreeks | Geef een beschrijving op voor het aangepaste veld. |
| `customerDataFields.isRequired` | Boolean | Geeft aan of dit veld vereist is in de workflow voor doelinstellingen. |
| `customerDataFields.enum` | Tekenreeks | Hiermee geeft u het aangepaste veld weer als een vervolgkeuzemenu en geeft u de opties weer die beschikbaar zijn voor de gebruiker. |
| `customerDataFields.pattern` | Tekenreeks | Hiermee wordt, indien nodig, een patroon voor het aangepaste veld afgedwongen. Gebruik reguliere expressies om een patroon af te dwingen. Als uw klant-id&#39;s bijvoorbeeld geen cijfers of onderstrepingstekens bevatten, voert u `^[A-Za-z]+$` in dit veld in. |
| `uiAttributes.documentationLink` | Tekenreeks | Verwijst naar de documentatiepagina in [Catalogus van Doelen](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) voor uw bestemming. Gebruik `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, waarbij `YOURDESTINATION` de naam van uw bestemming is. Voor een bestemming genoemd Moviestar, zou u `https://www.adobe.com/go/destinations-moviestar-en` gebruiken. |
| `uiAttributes.category` | Tekenreeks | Verwijst naar de rubriek die aan je bestemming in Adobe Experience Platform is toegewezen. Lees [Doelcategorieën](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories) voor meer informatie. Gebruik een van de volgende waarden: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `uiAttributes.connectionType` | Tekenreeks | `Server-to-server` is momenteel de enige beschikbare optie. |
| `uiAttributes.frequency` | Tekenreeks | `Streaming` is momenteel de enige beschikbare optie. |
| `identityNamespaces.externalId.acceptsAttributes` | Boolean | Hiermee geeft u aan of uw doel standaardprofielkenmerken accepteert. Gewoonlijk worden deze kenmerken gemarkeerd in de documentatie van onze partners. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Boolean | Geeft aan of klanten aangepaste naamruimten kunnen instellen op uw bestemming. |
| `identityNamespaces.externalId.allowedAttributesTransformation` | Tekenreeks | _Niet weergegeven in voorbeeldconfiguratie_. Wordt bijvoorbeeld gebruikt wanneer de [!DNL Platform]-klant gewone e-mailadressen als kenmerk heeft en uw platform alleen gehashte e-mails accepteert. Hier geeft u de transformatie op die moet worden toegepast (zet de e-mail bijvoorbeeld om in kleine letters en vervolgens in de hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | Wordt gebruikt voor gevallen waarin uw platform [standaard naamruimten](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) accepteert (bijvoorbeeld IDFA), zodat u gebruikers van het Platform kunt beperken tot het selecteren van deze naamruimten. <br> Als u  `acceptedGlobalNamespaces`deze optie gebruikt, kunt u e-mailadressen of telefoonnummers in kleine letters  `"requiredTransformation":"sha256(lower($))"` en hashtags weergeven. |
| `destinationDelivery.authenticationRule` | Tekenreeks | Geeft aan hoe [!DNL Platform]-klanten verbinding maken met uw doel. Accepteerde waarden zijn `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Gebruik `CUSTOMER_AUTHENTICATION` als klanten van het Platform zich bij uw systeem via een gebruikersbenaming en een wachtwoord, een dragerteken, of een andere methode van authentificatie aanmelden. U kunt deze optie bijvoorbeeld selecteren als u `authType: OAUTH2` of `authType:BEARER` ook in `customerAuthenticationConfigurations` hebt geselecteerd. </li><li> Gebruik `PLATFORM_AUTHENTICATION` als er een wereldwijd verificatiesysteem is tussen Adobe en uw bestemming en de [!DNL Platform]-klant geen verificatiegegevens hoeft op te geven om verbinding te maken met uw bestemming. In dit geval, moet u een geloofsbrieven tot stand brengen voorwerp gebruikend de [Credentials](./credentials-configuration.md) configuratie. </li><li>Gebruik `NONE` als er geen verificatie vereist is om gegevens naar het doelplatform te verzenden. </li></ul> |
| `destinationDelivery.destinationServerId` | Tekenreeks | De `instanceId` van de [doelserversjabloon](./destination-server-api.md) die voor deze bestemming wordt gebruikt. |
| `backfillHistoricalProfileData` | Boolean | Bepaalt of historische profielgegevens worden geëxporteerd wanneer segmenten worden geactiveerd naar de bestemming. <br> <ul><li> `true`:  [!DNL Platform] verzendt de historische gebruikersprofielen die voor het segment kwalificeren alvorens het segment wordt geactiveerd. </li><li> `false`:  [!DNL Platform] omvat alleen gebruikersprofielen die in aanmerking komen voor het segment nadat het segment is geactiveerd. </li></ul> |
| `segmentMappingConfig.mapUserInput` | Boolean | Controls whether the segment mapping id in the destination activation workflow is input by user. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Boolean | Controls whether the segment mapping id in the destination activation workflow is the Experience Platform segment ID. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Boolean | Controls whether the segment mapping id in the destination activation workflow is the Experience Platform segment name. |
| `segmentMappingConfig.audienceTemplateId` | Boolean | De `instanceId` van de [publieksmeta-gegevenssjabloon](./audience-metadata-api.md) die voor deze bestemming wordt gebruikt. |
| `schemaConfig.profileFields` | Array | Wanneer u vooraf bepaalde `profileFields` zoals aangetoond in de configuratie hierboven toevoegt, zullen de gebruikers de optie hebben om de attributen van het Experience Platform aan de vooraf bepaalde attributen op de kant van uw bestemming in kaart te brengen. |
| `schemaConfig.profileRequired` | Boolean | Gebruik `true` als de gebruikers profielattributen van Experience Platform aan douanekenmerken op de kant van uw bestemming, zoals aangetoond in de voorbeeldconfiguratie hierboven zouden moeten kunnen in kaart brengen. |
| `schemaConfig.segmentRequired` | Boolean | Altijd `segmentRequired:true` gebruiken. |
| `schemaConfig.identityRequired` | Boolean | Gebruik `true` als u gebruikers identiteitsnaamruimten van Experience Platform aan uw gewenste schema zou moeten kunnen in kaart brengen. |
| `aggregation.aggregationType` | - | Selecteer `BEST_EFFORT` of `CONFIGURABLE_AGGREGATION`. De voorbeeldconfiguratie hierboven omvat `BEST_EFFORT` samenvoeging. Voor een voorbeeld van `CONFIGURABLE_AGGREGATION`, verwijs naar de voorbeeldconfiguratie in [bestemmingsconfiguratie](./destination-configuration.md#example-configuration) document. Merk op dat de parameters relevant voor configureerbare samenvoeging hieronder in deze lijst worden gedocumenteerd. |
| `aggregation.bestEffortAggregation.maxUsersPerRequest` | Geheel | Experience Platform kan meerdere geëxporteerde profielen samenvoegen in één HTTP-aanroep. Specificeer het maximumaantal profielen dat uw eindpunt in één enkele vraag van HTTP zou moeten ontvangen. Merk op dat dit een beste inspanningssamenvoeging is. Bijvoorbeeld, als u waarde 100 specificeert, zou het Platform om het even welk aantal profielen kunnen verzenden kleiner dan 100 op een vraag. <br> Als uw server niet meerdere gebruikers per aanvraag accepteert, stelt u deze waarde in op 1. |
| `aggregation.bestEffortAggregation.splitUserById` | Boolean | Gebruik deze vlag als de vraag aan de bestemming door identiteit zou moeten worden verdeeld. Stel deze markering in op `true` als uw server slechts één identiteit per aanroep accepteert, voor een bepaalde naamruimte. |
| `aggregation.configurableAggregation.splitUserById` | Boolean | Zie parameter in voorbeeldconfiguratie [here](./destination-configuration.md#example-configuration). Gebruik deze vlag als de vraag aan de bestemming door identiteit zou moeten worden verdeeld. Stel deze markering in op `true` als uw server slechts één identiteit per aanroep accepteert, voor een bepaalde naamruimte. |
| `aggregation.configurableAggregation.maxBatchAgeInSecs` | Geheel | *Maximumwaarde: 3600*. Zie parameter in voorbeeldconfiguratie [here](./destination-configuration.md#example-configuration). Samen met `maxNumEventsInBatch`, bepaalt dit hoe lang Experience Platform zou moeten wachten tot het verzenden van een API vraag naar uw eindpunt. <br> Als u bijvoorbeeld de maximumwaarde voor beide parameters gebruikt, wacht het Experience Platform 3600 seconden OF totdat er 10.000 gekwalificeerde profielen zijn voordat de API-aanroep wordt uitgevoerd, afhankelijk van wat zich het eerst voordoet. |
| `aggregation.configurableAggregation.maxNumEventsInBatch` | Geheel | *Maximumwaarde: 10000*. Zie parameter in voorbeeldconfiguratie [here](./destination-configuration.md#example-configuration). Zie `maxBatchAgeInSecs` net boven. |
| `aggregation.configurableAggregation.aggregationKey` | Boolean | Zie parameter in voorbeeldconfiguratie [here](./destination-configuration.md#example-configuration). Hiermee kunt u de geëxporteerde profielen samenvoegen die aan de bestemming zijn toegewezen op basis van de onderstaande parameters: <br> <ul><li>segment-id</li><li> segmentstatus </li><li> naamruimte identity </li></ul> |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentId` | Boolean | Zie parameter in voorbeeldconfiguratie [here](./destination-configuration.md#example-configuration). Stel dit in op `true` als u profielen wilt groeperen die naar uw doel zijn geëxporteerd op segment-id. |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentStatus` | Boolean | Zie parameter in voorbeeldconfiguratie [here](./destination-configuration.md#example-configuration). U moet zowel `includeSegmentId:true` als `includeSegmentStatus:true` plaatsen als u profielen wilt groeperen die naar uw bestemming door segment ID EN segmentstatus worden uitgevoerd. |
| `aggregation.configurableAggregation.aggregationKey.includeIdentity` | Boolean | Zie parameter in voorbeeldconfiguratie [here](./destination-configuration.md#example-configuration). Stel dit in op `true` als u profielen wilt groeperen die naar uw doel worden geëxporteerd via naamruimte voor identiteit. |
| `aggregation.configurableAggregation.aggregationKey.oneIdentityPerGroup` | Boolean | Zie parameter in voorbeeldconfiguratie [here](./destination-configuration.md#example-configuration). Gebruik deze parameter om op te geven of u wilt dat de geëxporteerde profielen worden samengevoegd tot groepen met één identiteit (GAID, IDFA, telefoonnummers, e-mail, enz.). |
| `aggregation.configurableAggregation.aggregationKey.groups` | Tekenreeks | Zie parameter in voorbeeldconfiguratie [here](./destination-configuration.md#example-configuration). Maak lijsten met identiteitsgroepen als u profielen wilt groeperen die naar uw doel zijn geëxporteerd door groepen naamruimte. U kunt bijvoorbeeld profielen die de mobiele id&#39;s IDFA en GAID bevatten, combineren in één aanroep naar uw bestemming en e-mails in een andere aanroep met behulp van de configuratie in het voorbeeld. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde bestemmingsconfiguratie terug.

## Doelconfiguraties weergeven {#retrieve-list}

U kunt een lijst van alle bestemmingsconfiguraties voor uw IMS Organisatie terugwinnen door een verzoek van de GET tot het `/authoring/destinations` eindpunt te richten.

**API-indeling**


```http
GET /authoring/destinations
```

**Verzoek**

Het volgende verzoek zal de lijst van bestemmingsconfiguraties terugwinnen die u toegang tot hebt, die op Organisatie IMS en zandbakconfiguratie wordt gebaseerd.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

De volgende reactie retourneert HTTP-status 200 met een lijst van bestemmingsconfiguraties waartoe u toegang hebt, op basis van de IMS-organisatie-id en de sandboxnaam die u hebt gebruikt. Eén `instanceId` komt overeen met de sjabloon voor één doel. De reactie is afgebroken voor de beknoptheid.

```json
{
   "items":[
      {
         "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
         "createdDate":"2020-10-28T06:14:09.784471Z",
         "lastModifiedDate":"2021-06-28T06:14:09.784471Z",
         "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
         "sandboxName":"prod",
         "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
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
               "pattern":"^[A-Za-z]+$"
            }
         ],
         "uiAttributes":{
            "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
            "category":"mobile",
            "connectionType":"Server-to-server",
            "frequency":"Streaming"
         },
         "identityNamespaces":{
            "external_id":{
               "acceptsAttributes":true,
               "acceptsCustomNamespaces":true,
               "acceptedGlobalNamespaces":{
                  "Email":{
                     
                  }
               }
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
         "schemaConfig":{
            "profileFields":[
               {
                  "name":"a_custom_attribute",
                  "title":"a_custom_attribute",
                  "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
                  "type":"string",
                  "isRequired":false,
                  "readOnly":false,
                  "hidden":false
               }
            ],
            "profileRequired":true,
            "segmentRequired":true,
            "identityRequired":true
         },
         "aggregation":{
            "aggregationType":"BEST_EFFORT",
            "bestEffortAggregation":{
               "maxUsersPerRequest":10,
               "splitUserById":false
            }
         },
         "destinationDelivery":[
            {
               "authenticationRule":"CUSTOMER_AUTHENTICATION",
               "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
            }
         ],
         "destConfigId":"410631b8-f6b3-4b7c-82da-7998aa3f327c",
         "backfillHistoricalProfileData":true
      }
   ]
}
    
```

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `name` | Tekenreeks | Geeft de titel van het doel in de catalogus met Experience Platforms aan. |
| `description` | Tekenreeks | Geef een beschrijving op die Adobe in de Experience Platform-doelcatalogus voor uw doelkaart zal gebruiken. Doel voor niet meer dan 4-5 zinnen. |
| `status` | Tekenreeks | Geeft de levenscyclusstatus van de doelkaart aan. Accepteerde waarden zijn `TEST`, `PUBLISHED` en `DELETED`. Gebruik `TEST` wanneer u eerst uw bestemming vormt. |
| `customerAuthenticationConfigurations` | Tekenreeks | Wijst op de configuratie die wordt gebruikt om de klanten van het Experience Platform aan uw server voor authentiek te verklaren. Zie `authType` hieronder voor geaccepteerde waarden. |
| `customerAuthenticationConfigurations.authType` | Tekenreeks | Accepteerde waarden zijn `OAUTH2, BEARER`. |
| `customerDataFields.name` | Tekenreeks | Geef een naam op voor het aangepaste veld dat u introduceert. |
| `customerDataFields.type` | Tekenreeks | Hiermee geeft u aan welk type aangepast veld u wilt gebruiken. Accepteerde waarden zijn `string`, `object`, `integer` |
| `customerDataFields.title` | Tekenreeks | Hiermee wordt de naam van het veld aangegeven, zoals deze wordt weergegeven door klanten in de gebruikersinterface van het Experience Platform |
| `customerDataFields.description` | Tekenreeks | Geef een beschrijving op voor het aangepaste veld. |
| `customerDataFields.isRequired` | Boolean | Geeft aan of dit veld vereist is in de workflow voor doelinstellingen. |
| `customerDataFields.enum` | Tekenreeks | Hiermee geeft u het aangepaste veld weer als een vervolgkeuzemenu en geeft u de opties weer die beschikbaar zijn voor de gebruiker. |
| `customerDataFields.pattern` | Tekenreeks | Hiermee wordt, indien nodig, een patroon voor het aangepaste veld afgedwongen. Gebruik reguliere expressies om een patroon af te dwingen. Als uw klant-id&#39;s bijvoorbeeld geen cijfers of onderstrepingstekens bevatten, voert u `^[A-Za-z]+$` in dit veld in. |
| `uiAttributes.documentationLink` | Tekenreeks | Verwijst naar de documentatiepagina in [Catalogus van Doelen](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) voor uw bestemming. Gebruik `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, waarbij `YOURDESTINATION` de naam van uw bestemming is. Voor een bestemming genoemd Moviestar, zou u `https://www.adobe.com/go/destinations-moviestar-en` gebruiken |
| `uiAttributes.category` | Tekenreeks | Verwijst naar de rubriek die aan je bestemming in Adobe Experience Platform is toegewezen. Lees [Doelcategorieën](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories) voor meer informatie. Gebruik een van de volgende waarden: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments` |
| `uiAttributes.connectionType` | Tekenreeks | `Server-to-server` is momenteel de enige beschikbare optie. |
| `uiAttributes.frequency` | Tekenreeks | `Streaming` is momenteel de enige beschikbare optie. |
| `identityNamespaces.externalId.acceptsAttributes` | Boolean | Hiermee geeft u aan of uw doel standaardprofielkenmerken accepteert. Gewoonlijk worden deze kenmerken gemarkeerd in de documentatie van onze partners. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Boolean | Geeft aan of klanten aangepaste naamruimten kunnen instellen op uw bestemming. Meer informatie over [aangepaste naamruimten](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#manage-namespaces) in Adobe Experience Platform. |
| `identityNamespaces.externalId.allowedAttributesTransformation` | Tekenreeks | _Niet weergegeven in voorbeeldconfiguratie_. Wordt bijvoorbeeld gebruikt wanneer de [!DNL Platform]-klant gewone e-mailadressen als kenmerk heeft en uw platform alleen gehashte e-mails accepteert. Hier geeft u de transformatie op die moet worden toegepast (zet de e-mail bijvoorbeeld om in kleine letters en vervolgens in de hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | Wordt gebruikt voor gevallen waarin uw platform [standaard naamruimten](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) accepteert (bijvoorbeeld IDFA), zodat u gebruikers van het Platform kunt beperken tot het selecteren van deze naamruimten. |
| `destinationDelivery.authenticationRule` | Tekenreeks | Geeft aan hoe [!DNL Platform]-klanten verbinding maken met uw doel. Accepteerde waarden zijn `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Gebruik `CUSTOMER_AUTHENTICATION` als klanten van het Platform zich bij uw systeem via een gebruikersbenaming en een wachtwoord, een dragerteken, of een andere methode van authentificatie aanmelden. U kunt deze optie bijvoorbeeld selecteren als u `authType: OAUTH2` of `authType:BEARER` ook in `customerAuthenticationConfigurations` hebt geselecteerd. </li><li> Gebruik `PLATFORM_AUTHENTICATION` als er een wereldwijd verificatiesysteem is tussen Adobe en uw bestemming en de [!DNL Platform]-klant geen verificatiegegevens hoeft op te geven om verbinding te maken met uw bestemming. In dit geval, moet u een geloofsbrieven tot stand brengen voorwerp gebruikend de [Credentials](./credentials-configuration.md) configuratie. </li><li>Gebruik `NONE` als er geen verificatie vereist is om gegevens naar het doelplatform te verzenden. </li></ul> |
| `destinationDelivery.destinationServerId` | Tekenreeks | De `instanceId` van de [doelserversjabloon](./destination-server-api.md) die voor deze bestemming wordt gebruikt. |
| `destConfigId` | Tekenreeks | Dit veld wordt automatisch gegenereerd en vereist geen invoer. |
| `backfillHistoricalProfileData` | Boolean | Bepaalt of historische profielgegevens worden geëxporteerd wanneer segmenten worden geactiveerd naar de bestemming. <br> <ul><li> `true`:  [!DNL Platform] verzendt de historische gebruikersprofielen die voor het segment kwalificeren alvorens het segment wordt geactiveerd. </li><li> `false`:  [!DNL Platform] omvat alleen gebruikersprofielen die in aanmerking komen voor het segment nadat het segment is geactiveerd. </li></ul> |
| `segmentMappingConfig.mapUserInput` | Boolean | Controls whether the segment mapping id in the destination activation workflow is input by user. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Boolean | Controls whether the segment mapping id in the destination activation workflow is the Experience Platform segment ID. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Boolean | Controls whether the segment mapping id in the destination activation workflow is the Experience Platform segment name. |
| `segmentMappingConfig.audienceTemplateId` | Boolean | De `instanceId` van de [publieksmeta-gegevenssjabloon](./audience-metadata-management.md) die voor deze bestemming wordt gebruikt. Als u een sjabloon voor publieksmetagegevens wilt instellen, leest u de [API-naslaggids voor publieksmetagegevens](./audience-metadata-api.md). |

{style=&quot;table-layout:auto&quot;}

## Een bestaande doelconfiguratie bijwerken {#update}

U kunt een bestaande bestemmingsconfiguratie bijwerken door een verzoek van de PUT aan het `/authoring/destinations` eindpunt en het verstrekken van instantiidentiteitskaart van de bestemmingsconfiguratie te doen u wilt bijwerken. In het lichaam van de vraag, verstrek de bijgewerkte bestemmingsconfiguratie.

**API-indeling**


```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{INSTANCE_ID}` | De id van de doelconfiguratie die u wilt bijwerken. |

**Verzoek**

Het volgende verzoek werkt een bestaande bestemmingsconfiguratie bij, die door de parameters wordt gevormd die in de nuttige lading worden verstrekt. In de voorbeeldvraag hieronder, werken wij de configuratie [eerder gecreeerd ](./destination-configuration-api.md#create) bij om GAID, IDFA, en gehakt e-mailherkenningstekens als identiteitsnaamruimten nu goed te keuren.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
   "createdDate":"2020-10-28T06:14:09.784471Z",
   "lastModifiedDate":"2021-04-28T06:14:09.784471Z",
   "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
   "sandboxName":"prod",
   "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
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
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "gaid":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "GAID":{
               
            }
         }
      },
      "idfa":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "IDFA":{
               
            }
         }
      },
      "email_lc_sha256":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation":"sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation":"sha256(lower($))"
            },
            "Email_LC_SHA256":{
               
            }
         }
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```

## Hiermee wordt een specifieke doelconfiguratie opgehaald {#get}

U kunt gedetailleerde informatie over een specifieke bestemmingsconfiguratie terugwinnen door een verzoek van de GET tot het `/authoring/destinations` eindpunt te richten en instantieidentiteitskaart van de bestemmingsconfiguratie te verstrekken u wilt terugwinnen.

**API-indeling**


```http
GET /authoring/destinations/{INSTANCE_ID}
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{INSTANCE_ID}` | Identiteitskaart van de bestemmingsconfiguratie u wilt terugwinnen. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met gedetailleerde informatie over de gespecificeerde bestemmingsconfiguratie terug.

```json
{
   "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
   "createdDate":"2020-10-28T06:14:09.784471Z",
   "lastModifiedDate":"2021-06-04T06:14:09.784471Z",
   "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
   "sandboxName":"prod",
   "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
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
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
               
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "gaid":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "GAID":{
               
            }
         }
      },
      "idfa":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "IDFA":{
               
            }
         }
      },
      "email_lc_sha256":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation":"sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation":"sha256(lower($))"
            },
            "Email_LC_SHA256":{
               
            }
         }
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```


## Een specifieke doelconfiguratie verwijderen {#delete}

U kunt de gespecificeerde bestemmingsconfiguratie schrappen door een verzoek van DELETE aan het `/authoring/destinations` eindpunt te doen en identiteitskaart van de bestemmingsconfiguratie te verstrekken u wenst om in de verzoekweg te schrappen.

**API-indeling**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{INSTANCE_ID}` | De `id` van de bestemmingsconfiguratie u wilt schrappen. |

**Verzoek**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 samen met een lege HTTP-respons.

## API-foutafhandeling

De eindpunten van SDK API van de bestemming volgen de algemene API van het Experience Platform foutenmeldingsbeginselen. Raadpleeg [API-statuscodes](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) en [headerfouten aanvragen](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) in de handleiding voor het oplossen van Platforms.

## Volgende stappen

Na het lezen van dit document, weet u nu hoe te om uw bestemming te vormen gebruikend het `/authoring/destinations` API eindpunt. Lees [hoe te om Doel SDK te gebruiken om uw bestemming te vormen](./configure-destination-instructions.md) om te begrijpen waar deze stap in het proces past om uw bestemming te vormen.
