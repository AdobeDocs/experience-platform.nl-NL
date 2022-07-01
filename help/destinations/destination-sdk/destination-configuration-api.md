---
description: Deze pagina bevat een overzicht en beschrijving van alle API-bewerkingen die u kunt uitvoeren met het API-eindpunt `/authoring/destination.
title: API-eindpuntbewerkingen voor doelen
exl-id: 96755e9d-be62-432f-b985-91330575b395
source-git-commit: 301cef53644e813c3fd43e7f2dbaf730c9e5fc11
workflow-type: tm+mt
source-wordcount: '2571'
ht-degree: 1%

---

# API-bewerkingen voor bestemmingspunten {#destination-configuration}

>[!IMPORTANT]
>
>**API-eindpunt**: `platform.adobe.io/data/core/activation/authoring/destinations`

Deze pagina bevat een overzicht en beschrijving van alle API-bewerkingen die u kunt uitvoeren met de `/authoring/destinations` API-eindpunt. Voor een beschrijving van de functionaliteit die door dit eindpunt wordt gesteund, lees [doelconfiguratie](./destination-configuration.md).

## Aan de slag met doel-API-bewerkingen {#get-started}

Controleer voordat je doorgaat de [gids Aan de slag](./getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings creatie en vereiste kopballen te verkrijgen.

## Configuratie maken voor een streamingdoel {#create}

U kunt een nieuwe bestemmingsconfiguratie tot stand brengen door een verzoek van de POST aan `/authoring/destinations` eindpunt.

**API-indeling**

```http
POST /authoring/destinations
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe het stromen bestemmingsconfiguratie, die door de parameters wordt gevormd die in de lading worden verstrekt. De hieronder vermelde lading omvat alle parameters voor het stromen bestemmingen die door `/authoring/destinations` eindpunt. Merk op dat u niet alle parameters op de vraag moet toevoegen en dat het malplaatje, volgens uw API vereisten aanpasbaar is.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `status` | Tekenreeks | Geeft de levenscyclusstatus van de doelkaart aan. Accepteerde waarden zijn `TEST`, `PUBLISHED`, en `DELETED`. Gebruiken `TEST` wanneer u eerst uw bestemming vormt. |
| `customerAuthenticationConfigurations` | Tekenreeks | Wijst op de configuratie die wordt gebruikt om de klanten van het Experience Platform aan uw server voor authentiek te verklaren. Zie `authType` hieronder voor geaccepteerde waarden. |
| `customerAuthenticationConfigurations.authType` | Tekenreeks | Ondersteunde waarden voor streamingdoelen zijn: <ul><li>`OAUTH2`</li><li>`BEARER`</li></ul> Ondersteunde waarden voor op bestanden gebaseerde doelen zijn: <ul><li>`S3`</li><li>`AZURE_CONNECTION_STRING`</li><li>`AZURE_SERVICE_PRINCIPAL`</li><li>`SFTP_WITH_SSH_KEY`</li><li>`SFTP_WITH_PASSWORD`</li></ul> |
| `customerDataFields.name` | Tekenreeks | Geef een naam op voor het aangepaste veld dat u introduceert. |
| `customerDataFields.type` | Tekenreeks | Hiermee geeft u aan welk type aangepast veld u wilt gebruiken. Accepteerde waarden zijn `string`, `object`, `integer` |
| `customerDataFields.title` | Tekenreeks | Hiermee wordt de naam van het veld aangegeven, zoals deze wordt weergegeven door klanten in de gebruikersinterface van het Experience Platform |
| `customerDataFields.description` | Tekenreeks | Geef een beschrijving op voor het aangepaste veld. |
| `customerDataFields.isRequired` | Boolean | Geeft aan of dit veld vereist is in de workflow voor doelinstellingen. |
| `customerDataFields.enum` | Tekenreeks | Hiermee geeft u het aangepaste veld weer als een vervolgkeuzemenu en geeft u de opties weer die beschikbaar zijn voor de gebruiker. |
| `customerDataFields.pattern` | Tekenreeks | Hiermee wordt, indien nodig, een patroon voor het aangepaste veld afgedwongen. Gebruik reguliere expressies om een patroon af te dwingen. Als uw klant-id&#39;s bijvoorbeeld geen cijfers of onderstrepingstekens bevatten, voert u `^[A-Za-z]+$` op dit gebied. |
| `uiAttributes.documentationLink` | Tekenreeks | Verwijst naar de documentatiepagina in [Doelcatalogus](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) voor uw bestemming. Gebruiken `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, waarbij `YOURDESTINATION` is de naam van uw bestemming. Voor een bestemming genoemd Moviestar, zou u gebruiken `https://www.adobe.com/go/destinations-moviestar-en`. Merk op dat deze verbinding slechts werkt nadat Adobe uw bestemming live plaatst en de documentatie wordt gepubliceerd. |
| `uiAttributes.category` | Tekenreeks | Verwijst naar de rubriek die aan je bestemming in Adobe Experience Platform is toegewezen. Lees voor meer informatie [Doelcategorieën](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). Gebruik een van de volgende waarden: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `uiAttributes.connectionType` | Tekenreeks | `Server-to-server` is momenteel de enige beschikbare optie. |
| `uiAttributes.frequency` | Tekenreeks | `Streaming` is momenteel de enige beschikbare optie. |
| `identityNamespaces.externalId.acceptsAttributes` | Boolean | Hiermee geeft u aan of uw doel standaardprofielkenmerken accepteert. Gewoonlijk worden deze kenmerken gemarkeerd in de documentatie van onze partners. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Boolean | Geeft aan of klanten aangepaste naamruimten kunnen instellen op uw bestemming. |
| `identityNamespaces.externalId.transformation` | Tekenreeks | _Niet weergegeven in voorbeeldconfiguratie_. Wordt bijvoorbeeld gebruikt als de [!DNL Platform] de klant heeft onbewerkte e-mailadressen als attribuut en uw platform accepteert alleen gehashte e-mailadressen. Hier geeft u de transformatie op die moet worden toegepast (zet de e-mail bijvoorbeeld om in kleine letters en vervolgens in de hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | Wordt gebruikt voor gevallen waarin uw platform accepteert [standaardnaamruimten](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) (bijvoorbeeld IDFA), zodat u gebruikers van het Platform kunt beperken tot het selecteren van deze naamruimten. <br> Wanneer u `acceptedGlobalNamespaces`kunt u `"requiredTransformation":"sha256(lower($))"` om e-mailadressen of telefoonnummers in kleine letters en te hashen. |
| `destinationDelivery.authenticationRule` | Tekenreeks | Geeft aan hoe [!DNL Platform] klanten verbinden met uw bestemming. Accepteerde waarden zijn `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Gebruiken `CUSTOMER_AUTHENTICATION` als de klanten van het Platform zich in uw systeem via een gebruikersbenaming en een wachtwoord, een dragerteken, of een andere methode van authentificatie aanmelden. U kunt deze optie bijvoorbeeld selecteren als u `authType: OAUTH2` of `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> Gebruiken `PLATFORM_AUTHENTICATION` als er een globaal authentificatiesysteem tussen Adobe en uw bestemming en is [!DNL Platform] de klant te hoeven om geen authentificatiegeloofsbrieven te verstrekken om met uw bestemming te verbinden. In dit geval moet u een object credentials maken met de opdracht [Credentials](./credentials-configuration-api.md) configuratie. </li><li>Gebruiken `NONE` als geen authentificatie wordt vereist om gegevens naar uw bestemmingsplatform te verzenden. </li></ul> |
| `destinationDelivery.destinationServerId` | Tekenreeks | De `instanceId` van de [doelserversjabloon](./destination-server-api.md) gebruikt voor deze bestemming. |
| `backfillHistoricalProfileData` | Boolean | Bepaalt of historische profielgegevens worden geëxporteerd wanneer segmenten worden geactiveerd naar de bestemming. <br> <ul><li> `true`: [!DNL Platform] verzendt de historische gebruikersprofielen die voor het segment kwalificeren alvorens het segment wordt geactiveerd. </li><li> `false`: [!DNL Platform] omvat alleen gebruikersprofielen die in aanmerking komen voor het segment nadat het segment is geactiveerd. </li></ul> |
| `segmentMappingConfig.mapUserInput` | Boolean | Controls whether the segment mapping id in the destination activation workflow is input by user. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Boolean | Controls whether the segment mapping id in the destination activation workflow is the Experience Platform segment ID. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Boolean | Controls whether the segment mapping id in the destination activation workflow is the Experience Platform segment name. |
| `segmentMappingConfig.audienceTemplateId` | Boolean | De `instanceId` van de [sjabloon voor doelmetagegevens](./audience-metadata-api.md) gebruikt voor deze bestemming. |
| `schemaConfig.profileFields` | Array | Wanneer u vooraf gedefinieerde `profileFields` zoals aangetoond in de configuratie hierboven, zullen de gebruikers de optie hebben om de attributen van het Experience Platform aan de vooraf bepaalde attributen op de kant van uw bestemming in kaart te brengen. |
| `schemaConfig.profileRequired` | Boolean | Gebruiken `true` als de gebruikers profielattributen van Experience Platform aan douanekenmerken op de kant van uw bestemming zouden moeten kunnen in kaart brengen, zoals aangetoond in de voorbeeldconfiguratie hierboven. |
| `schemaConfig.segmentRequired` | Boolean | Altijd gebruiken `segmentRequired:true`. |
| `schemaConfig.identityRequired` | Boolean | Gebruiken `true` als u gebruikers identiteitsnaamruimten van Experience Platform aan uw gewenste schema zou moeten kunnen in kaart brengen. |
| `aggregation.aggregationType` | - | Selecteer `BEST_EFFORT` of `CONFIGURABLE_AGGREGATION`. De bovenstaande voorbeeldconfiguratie bevat `BEST_EFFORT` aggregatie. Een voorbeeld van `CONFIGURABLE_AGGREGATION`, raadpleegt u de voorbeeldconfiguratie in de [doelconfiguratie](./destination-configuration.md#example-configuration) document. De parameters relevant voor configureerbare samenvoeging zijn hieronder gedocumenteerd in deze lijst. |
| `aggregation.bestEffortAggregation.maxUsersPerRequest` | Geheel | Experience Platform kan meerdere geëxporteerde profielen samenvoegen in één HTTP-aanroep. Specificeer het maximumaantal profielen dat uw eindpunt in één enkele vraag van HTTP zou moeten ontvangen. Merk op dat dit een beste inspanningssamenvoeging is. Bijvoorbeeld, als u waarde 100 specificeert, zou het Platform om het even welk aantal profielen kunnen verzenden kleiner dan 100 op een vraag. <br> Als uw server niet meerdere gebruikers per aanvraag accepteert, stelt u deze waarde in op 1. |
| `aggregation.bestEffortAggregation.splitUserById` | Boolean | Gebruik deze vlag als de vraag aan de bestemming door identiteit zou moeten worden verdeeld. Deze markering instellen op `true` als uw server slechts één identiteit per vraag, voor een bepaalde namespace goedkeurt. |
| `aggregation.configurableAggregation.splitUserById` | Boolean | Zie parameter in voorbeeldconfiguratie [hier](./destination-configuration.md#example-configuration). Gebruik deze vlag als de vraag aan de bestemming door identiteit zou moeten worden verdeeld. Deze markering instellen op `true` als uw server slechts één identiteit per vraag, voor een bepaalde namespace goedkeurt. |
| `aggregation.configurableAggregation.maxBatchAgeInSecs` | Geheel | <ul><li>*Minimumwaarde: 1800*</li><li>*Maximumwaarde: 3600*</li><li>Zie parameter in voorbeeldconfiguratie [hier](./destination-configuration.md#example-configuration). Configureer een waarde tussen de minimaal en maximaal toegestane waarden. Samen met `maxNumEventsInBatch`, bepaalt deze parameter hoe lang Experience Platform zou moeten wachten tot het verzenden van een API vraag naar uw eindpunt. <br> Als u bijvoorbeeld de maximumwaarde voor beide parameters gebruikt, wacht het Experience Platform 3600 seconden OF totdat er 10.000 gekwalificeerde profielen zijn voordat de API-aanroep wordt uitgevoerd, afhankelijk van wat zich het eerst voordoet. </li></ul> |
| `aggregation.configurableAggregation.maxNumEventsInBatch` | Geheel | <ul><li>*Minimumwaarde: 1000*</li><li>*Maximumwaarde: 10000*</li><li>Zie parameter in voorbeeldconfiguratie [hier](./destination-configuration.md#example-configuration). Configureer een waarde tussen de minimaal en maximaal toegestane waarden. Zie voor een beschrijving van deze parameter `maxBatchAgeInSecs` net boven.</li></ul> |
| `aggregation.configurableAggregation.aggregationKey` | Boolean | Zie parameter in voorbeeldconfiguratie [hier](./destination-configuration.md#example-configuration). Hiermee kunt u de geëxporteerde profielen samenvoegen die aan de bestemming zijn toegewezen op basis van de onderstaande parameters: <br> <ul><li>segment-id</li><li> segmentstatus </li><li> naamruimte identity </li></ul> |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentId` | Boolean | Zie parameter in voorbeeldconfiguratie [hier](./destination-configuration.md#example-configuration). Stel deze in op `true` als u profielen wilt groeperen die naar uw bestemming door segmentID worden uitgevoerd. |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentStatus` | Boolean | Zie parameter in voorbeeldconfiguratie [hier](./destination-configuration.md#example-configuration). U moet beide instellen `includeSegmentId:true` en `includeSegmentStatus:true` als u profielen wilt groeperen die naar uw bestemming door segmentID EN segmentstatus worden uitgevoerd. |
| `aggregation.configurableAggregation.aggregationKey.includeIdentity` | Boolean | Zie parameter in voorbeeldconfiguratie [hier](./destination-configuration.md#example-configuration). Stel deze in op `true` als u profielen wilt groeperen die naar uw bestemming door identiteitsnamespace worden uitgevoerd. |
| `aggregation.configurableAggregation.aggregationKey.oneIdentityPerGroup` | Boolean | Zie parameter in voorbeeldconfiguratie [hier](./destination-configuration.md#example-configuration). Gebruik deze parameter om op te geven of u wilt dat de geëxporteerde profielen worden samengevoegd tot groepen met één identiteit (GAID, IDFA, telefoonnummers, e-mail, enz.). |
| `aggregation.configurableAggregation.aggregationKey.groups` | Tekenreeks | Zie parameter in voorbeeldconfiguratie [hier](./destination-configuration.md#example-configuration). Maak lijsten met identiteitsgroepen als u profielen wilt groeperen die naar uw doel zijn geëxporteerd door groepen naamruimte. U kunt bijvoorbeeld profielen die de mobiele id&#39;s IDFA en GAID bevatten, combineren in één aanroep naar uw bestemming en e-mails in een andere aanroep met behulp van de configuratie in het voorbeeld. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde bestemmingsconfiguratie terug.

## Configuratie maken voor een op een bestand gebaseerd doel {#create-file-based}

U kunt een nieuwe bestemmingsconfiguratie tot stand brengen door een verzoek van de POST aan `/authoring/destinations` eindpunt.

**API-indeling**

```http
POST /authoring/destinations
```

**Verzoek**

Met de volgende aanvraag wordt een nieuwe [!DNL Amazon S3] op dossier-gebaseerde bestemmingsconfiguratie, die door de parameters wordt gevormd die in de lading worden verstrekt. De hieronder vermelde lading omvat alle parameters voor op dossier-gebaseerde bestemmingen die door `/authoring/destinations` eindpunt. Merk op dat u niet alle parameters op de vraag moet toevoegen en dat het malplaatje, volgens uw API vereisten aanpasbaar is.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
        "name": "S3 Destination with CSV Options",
        "description": "S3 Destination with CSV Options",
        "releaseNotes": "S3 Destination with CSV Options",
        "status": "TEST",
        "customerAuthenticationConfigurations": [
            {
                "authType": "S3"
            }
        ],
        "customerEncryptionConfigurations": [
            {
                "encryptionAlgo": ""
            }
        ],
        "customerDataFields": [
            {
                "name": "bucket",
                "title": "Select S3 Bucket",
                "description": "Select S3 Bucket",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "path",
                "title": "S3 path",
                "description": "Select S3 Bucket",
                "type": "string",
                "isRequired": true,
                "pattern": "^[A-Za-z]+$",
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "sep",
                "title": "Select separator for each field and value",
                "description": "Select for each field and value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "encoding",
                "title": "Specify encoding (charset) of saved CSV files",
                "description": "Select encoding of csv files",
                "type": "string",
                "enum": ["UTF-8", "UTF-16"],
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "quote",
                "title": "Select a single character used for escaping quoted values",
                "description": "Select single charachter for escaping quoted values",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "quoteAll",
                "title": "Quote All",
                "description": "Select flag for escaping quoted values",
                "type": "string",
                "enum" : ["true","false"],
                "default": "true",
                "isRequired": true,
                "readOnly": false,
                "hidden": false
            },
             {
                "name": "escape",
                "title": "Select a single character used for escaping quotes",
                "description": "Select a single character used for escaping quotes inside an already quoted value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "escapeQuotes",
                "title": "Escape quotes",
                "description": "A flag indicating whether values containing quotes should always be enclosed in quotes",
                "type": "string",
                "enum" : ["true","false"],
                "isRequired": false,
                "default": "true",
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "header",
                "title": "header",
                "description": "Writes the names of columns as the first line.",
                "type": "string",
                "isRequired": false,
                "enum" : ["true","false"],
                "readOnly": false,
                "default": "true",
                "hidden": false
            },
            {
                "name": "ignoreLeadingWhiteSpace",
                "title": "Ignore leading white space",
                "description": "A flag indicating whether or not leading whitespaces from values being written should be skipped.",
                "type": "string",
                "isRequired": false,
                "enum" : ["true","false"],
                "readOnly": false,
                "default": "true",
                "hidden": false
            },
            {
                "name": "nullValue",
                "title": "Select the string representation of a null value",
                "description": "Sets the string representation of a null value. ",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "dateFormat",
                "title": "Date format",
                "description": "Select the string that indicates a date format. ",
                "type": "string",
                "default": "yyyy-MM-dd",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
             {
                "name": "charToEscapeQuoteEscaping",
                "title": "Char to escape quote escaping",
                "description": "Sets a single character used for escaping the escape for the quote character",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "emptyValue",
                "title": "Select the string representation of an empty value",
                "description": "Select the string representation of an empty value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "default": "",
                "hidden": false
            },
            {
                "name": "compression",
                "title": "Select compression",
                "description": "Select compressiont",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "enum" : ["SNAPPY","GZIP","DEFLATE", "NONE"]
            },
            {
                "name": "fileType",
                "title": "Select a fileType",
                "description": "Select fileType",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "hidden": false,
                "enum" :["csv", "json", "parquet"],
                "default" : "csv"
            }
        ],
        "uiAttributes": {
            "documentationLink": "https://www.adobe.io/apis/experienceplatform.html",
            "category": "S3",
            "iconUrl": "https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
            "connectionType": "S3",
            "flowRunsSupported": true,
            "monitoringSupported": true,
            "frequency": "Batch"
        },
        "destinationDelivery": [
            {
                "deliveryMatchers" : [
                    {
                        "type" : "SOURCE",
                        "value" : [
                            "batch"
                        ]
                    }
                ],
                "authenticationRule": "CUSTOMER_AUTHENTICATION",
                "destinationServerId": "{{destinationServerId}}"
            }
        ],
        "schemaConfig" : {
            "profileRequired" : true,
            "segmentRequired" : true,
            "identityRequired" : true
        },
        "batchConfig":{
            "allowMandatoryFieldSelection": true,
            "allowJoinKeyFieldSelection": true,
            "defaultExportMode": "DAILY_FULL_EXPORT",
            "allowedExportMode":[
                "DAILY_FULL_EXPORT",
                "FIRST_FULL_THEN_INCREMENTAL"
            ],
            "allowedScheduleFrequency":[
                "DAILY",
                "EVERY_3_HOURS",
                "EVERY_6_HOURS",
                "EVERY_8_HOURS",
                "EVERY_12_HOURS",
                "ONCE",
                "EVERY_HOUR"
            ],
            "defaultFrequency":"DAILY",
            "defaultStartTime":"00:00"
        },
        "backfillHistoricalProfileData": true
    }
```

Voor gedetailleerde beschrijvingen van alle bovenstaande parameters raadpleegt u [bestandsgebaseerde doelconfiguratie](file-based-destination-configuration.md).

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde bestemmingsconfiguratie terug.

## Doelconfiguraties weergeven {#retrieve-list}

U kunt een lijst van alle bestemmingsconfiguraties voor uw IMS Organisatie terugwinnen door een verzoek van de GET aan te dienen `/authoring/destinations` eindpunt.

**API-indeling**


```http
GET /authoring/destinations
```

**Verzoek**

Het volgende verzoek zal de lijst van bestemmingsconfiguraties terugwinnen die u toegang tot hebt, die op Organisatie IMS en zandbakconfiguratie wordt gebaseerd.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

De volgende reactie retourneert HTTP-status 200 met een lijst van bestemmingsconfiguraties waartoe u toegang hebt, op basis van de IMS-organisatie-id en de sandboxnaam die u hebt gebruikt. Eén `instanceId` komt overeen met de sjabloon voor één bestemming. De reactie is afgebroken voor de beknoptheid.

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
| `status` | Tekenreeks | Geeft de levenscyclusstatus van de doelkaart aan. Accepteerde waarden zijn `TEST`, `PUBLISHED`, en `DELETED`. Gebruiken `TEST` wanneer u eerst uw bestemming vormt. |
| `customerAuthenticationConfigurations` | Tekenreeks | Wijst op de configuratie die wordt gebruikt om de klanten van het Experience Platform aan uw server voor authentiek te verklaren. Zie `authType` hieronder voor geaccepteerde waarden. |
| `customerAuthenticationConfigurations.authType` | Tekenreeks | Accepteerde waarden zijn `OAUTH2, BEARER`. |
| `customerDataFields.name` | Tekenreeks | Geef een naam op voor het aangepaste veld dat u introduceert. |
| `customerDataFields.type` | Tekenreeks | Hiermee geeft u aan welk type aangepast veld u wilt gebruiken. Accepteerde waarden zijn `string`, `object`, `integer` |
| `customerDataFields.title` | Tekenreeks | Hiermee wordt de naam van het veld aangegeven, zoals deze wordt weergegeven door klanten in de gebruikersinterface van het Experience Platform |
| `customerDataFields.description` | Tekenreeks | Geef een beschrijving op voor het aangepaste veld. |
| `customerDataFields.isRequired` | Boolean | Geeft aan of dit veld vereist is in de workflow voor doelinstellingen. |
| `customerDataFields.enum` | Tekenreeks | Hiermee geeft u het aangepaste veld weer als een vervolgkeuzemenu en geeft u de opties weer die beschikbaar zijn voor de gebruiker. |
| `customerDataFields.pattern` | Tekenreeks | Hiermee wordt, indien nodig, een patroon voor het aangepaste veld afgedwongen. Gebruik reguliere expressies om een patroon af te dwingen. Als uw klant-id&#39;s bijvoorbeeld geen cijfers of onderstrepingstekens bevatten, voert u `^[A-Za-z]+$` op dit gebied. |
| `uiAttributes.documentationLink` | Tekenreeks | Verwijst naar de documentatiepagina in [Doelcatalogus](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) voor uw bestemming. Gebruiken `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, waarbij `YOURDESTINATION` is de naam van uw bestemming. Voor een bestemming genoemd Moviestar, zou u gebruiken `https://www.adobe.com/go/destinations-moviestar-en`. Merk op dat deze verbinding slechts werkt nadat Adobe uw bestemming live plaatst en de documentatie wordt gepubliceerd. |
| `uiAttributes.category` | Tekenreeks | Verwijst naar de rubriek die aan je bestemming in Adobe Experience Platform is toegewezen. Lees voor meer informatie [Doelcategorieën](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). Gebruik een van de volgende waarden: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments` |
| `uiAttributes.connectionType` | Tekenreeks | `Server-to-server` is momenteel de enige beschikbare optie. |
| `uiAttributes.frequency` | Tekenreeks | `Streaming` is momenteel de enige beschikbare optie. |
| `identityNamespaces.externalId.acceptsAttributes` | Boolean | Hiermee geeft u aan of uw doel standaardprofielkenmerken accepteert. Gewoonlijk worden deze kenmerken gemarkeerd in de documentatie van onze partners. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Boolean | Geeft aan of klanten aangepaste naamruimten kunnen instellen op uw bestemming. Meer informatie over [aangepaste naamruimten](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#manage-namespaces) in Adobe Experience Platform. |
| `identityNamespaces.externalId.transformation` | Tekenreeks | _Niet weergegeven in voorbeeldconfiguratie_. Wordt bijvoorbeeld gebruikt als de [!DNL Platform] de klant heeft onbewerkte e-mailadressen als attribuut en uw platform accepteert alleen gehashte e-mailadressen. Hier geeft u de transformatie op die moet worden toegepast (zet de e-mail bijvoorbeeld om in kleine letters en vervolgens in de hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | Wordt gebruikt voor gevallen waarin uw platform accepteert [standaardnaamruimten](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) (bijvoorbeeld IDFA), zodat u gebruikers van het Platform kunt beperken tot het selecteren van deze naamruimten. |
| `destinationDelivery.authenticationRule` | Tekenreeks | Geeft aan hoe [!DNL Platform] klanten verbinden met uw bestemming. Accepteerde waarden zijn `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Gebruiken `CUSTOMER_AUTHENTICATION` als de klanten van het Platform zich in uw systeem via een gebruikersbenaming en een wachtwoord, een dragerteken, of een andere methode van authentificatie aanmelden. U kunt deze optie bijvoorbeeld selecteren als u `authType: OAUTH2` of `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> Gebruiken `PLATFORM_AUTHENTICATION` als er een globaal authentificatiesysteem tussen Adobe en uw bestemming en is [!DNL Platform] de klant te hoeven om geen authentificatiegeloofsbrieven te verstrekken om met uw bestemming te verbinden. In dit geval moet u een object credentials maken met de opdracht [Credentials](./authentication-configuration.md) configuratie. </li><li>Gebruiken `NONE` als geen authentificatie wordt vereist om gegevens naar uw bestemmingsplatform te verzenden. </li></ul> |
| `destinationDelivery.destinationServerId` | Tekenreeks | De `instanceId` van de [doelserversjabloon](./destination-server-api.md) gebruikt voor deze bestemming. |
| `destConfigId` | Tekenreeks | Dit veld wordt automatisch gegenereerd en vereist geen invoer. |
| `backfillHistoricalProfileData` | Boolean | Bepaalt of historische profielgegevens worden geëxporteerd wanneer segmenten worden geactiveerd naar de bestemming. <br> <ul><li> `true`: [!DNL Platform] verzendt de historische gebruikersprofielen die voor het segment kwalificeren alvorens het segment wordt geactiveerd. </li><li> `false`: [!DNL Platform] omvat alleen gebruikersprofielen die in aanmerking komen voor het segment nadat het segment is geactiveerd. </li></ul> |
| `segmentMappingConfig.mapUserInput` | Boolean | Controls whether the segment mapping id in the destination activation workflow is input by user. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Boolean | Controls whether the segment mapping id in the destination activation workflow is the Experience Platform segment ID. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Boolean | Controls whether the segment mapping id in the destination activation workflow is the Experience Platform segment name. |
| `segmentMappingConfig.audienceTemplateId` | Boolean | De `instanceId` van de [sjabloon voor doelmetagegevens](./audience-metadata-management.md) gebruikt voor deze bestemming. Als u een sjabloon voor publieksmetagegevens wilt instellen, leest u de [API-naslaggids voor doelmetagegevens](./audience-metadata-api.md). |

{style=&quot;table-layout:auto&quot;}

## Een bestaande doelconfiguratie bijwerken {#update}

U kunt een bestaande bestemmingsconfiguratie bijwerken door een verzoek van de PUT aan `/authoring/destinations` eindpunt en het verstrekken van instanceID van de bestemmingsconfiguratie wilt u bijwerken. In het lichaam van de vraag, verstrek de bijgewerkte bestemmingsconfiguratie.

**API-indeling**


```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{INSTANCE_ID}` | De id van de doelconfiguratie die u wilt bijwerken. |

**Verzoek**

Het volgende verzoek werkt een bestaande bestemmingsconfiguratie bij, die door de parameters wordt gevormd die in de nuttige lading worden verstrekt. In de voorbeeldvraag hieronder, werken wij de configuratie bij [eerder gemaakt](./destination-configuration-api.md#create) om GAID, IDFA, en hashed e-mailherkenningstekens als identiteitsnamespaces nu goed te keuren.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

U kunt gedetailleerde informatie over een specifieke bestemmingsconfiguratie terugwinnen door een verzoek van de GET aan `/authoring/destinations` eindpunt en het verstrekken van instanceID van de bestemmingsconfiguratie u wilt terugwinnen.

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

U kunt de gespecificeerde bestemmingsconfiguratie schrappen door een verzoek van de DELETE aan te richten `/authoring/destinations` eindpunt en het verstrekken van identiteitskaart van de bestemmingsconfiguratie u wenst om in de verzoekweg te schrappen.

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 samen met een lege HTTP-respons.

## API-foutafhandeling

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Zie [API-statuscodes](../../landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](../../landing/troubleshooting.md#request-header-errors) in de gids voor het oplossen van problemen met Platforms.

## Volgende stappen

Na het lezen van dit document, weet u nu hoe te om uw bestemming te vormen gebruikend `/authoring/destinations` API-eindpunt. Lezen [hoe te om Destination SDK te gebruiken om uw bestemming te vormen](./configure-destination-instructions.md) om te begrijpen waar deze stap in het proces past om uw bestemming te vormen.
