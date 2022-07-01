---
description: Deze configuratie staat u toe om basisinformatie zoals uw bestemmingsnaam, categorie, beschrijving, embleem, en meer te wijzen. De montages in deze configuratie bepalen ook hoe de gebruikers van het Experience Platform aan uw bestemming voor authentiek verklaren, hoe het in het gebruikersinterface van het Experience Platform en de identiteiten verschijnt die naar uw bestemming kunnen worden uitgevoerd.
title: (Bèta) op dossier-gebaseerde opties van de bestemmingsconfiguratie voor Destination SDK
exl-id: 6b0a0398-6392-470a-bb27-5b34b0062793
source-git-commit: 301cef53644e813c3fd43e7f2dbaf730c9e5fc11
workflow-type: tm+mt
source-wordcount: '2294'
ht-degree: 2%

---

# (Beta) Bestandsgebaseerde doelconfiguratie {#destination-configuration}

## Overzicht {#overview}

>[!IMPORTANT]
>
>Bestandsgebaseerde doelondersteuning in Adobe Experience Platform Destination SDK staat momenteel in bètaversie. De documentatie en functionaliteit kunnen worden gewijzigd.

Deze configuratie staat u toe om essentiële informatie voor uw op dossier-gebaseerde bestemming, zoals uw bestemmingsnaam, categorie, beschrijving, en meer te wijzen. De montages in deze configuratie bepalen ook hoe de gebruikers van het Experience Platform aan uw bestemming voor authentiek verklaren, hoe het in het gebruikersinterface van het Experience Platform en de identiteiten verschijnt die naar uw bestemming kunnen worden uitgevoerd.

Deze configuratie verbindt ook de andere configuraties die voor uw bestemming worden vereist aan het werk - bestemmingsserver en publieksmeta-gegevens - aan dit. Lees hoe u naar de twee configuraties in een [hieronder](./destination-configuration.md#connecting-all-configurations).

U kunt de in dit document beschreven functionaliteit configureren met de `/authoring/destinations` API-eindpunt. Lezen [API-eindpuntbewerkingen voor doelen](./destination-configuration-api.md) voor een volledige lijst van verrichtingen kunt u op het eindpunt uitvoeren.

## Amazon S3-doelconfiguratievoorbeeld {#batch-example-configuration}

```json
{
   "name":"S3 Destination with CSV Options",
   "description":"S3 Destination with CSV Options",
   "status":"TEST",
   "maxProfileAttributes":"2000",
   "maxIdentityAttributes":"10",
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerEncryptionConfigurations":[
      
   ],
   "customerDataFields":[
      {
         "name":"bucket",
         "title":"Amazon S3 bucket name",
         "description":"Enter your Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Amazon S3 bucket path",
         "description":"Enter your S3 bucket path",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"sep",
         "title":"Enter a separator for each field and value",
         "description":"Enter a separator character for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Specify encoding (charset) of saved CSV files",
         "description":"Select encoding of csv files",
         "type":"string",
         "enum":[
            "UTF-8",
            "UTF-16"
         ],
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quote",
         "title":"Select a single character used for escaping quoted values",
         "description":"Select single charachter for escaping quoted values",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "default":"true",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escape",
         "title":"Select a single character used for escaping quotes",
         "description":"Select a single character used for escaping quotes inside an already quoted value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Escape quotes",
         "description":"A flag indicating whether values containing quotes should always be enclosed in quotes",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "isRequired":false,
         "default":"true",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"header",
         "title":"header",
         "description":"Writes the names of columns as the first line.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"ignoreLeadingWhiteSpace",
         "title":"Ignore leading white space",
         "description":"A flag indicating whether or not leading whitespaces from values being written should be skipped.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"nullValue",
         "title":"Select the string representation of a null value",
         "description":"Sets the string representation of a null value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Select the string that indicates a date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Char to escape quote escaping",
         "description":"Sets a single character used for escaping the escape for the quote character",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Select the string representation of an empty value",
         "description":"Select the string representation of an empty value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Select compression",
         "description":"Select compressiont",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "enum":[
            "SNAPPY",
            "GZIP",
            "DEFLATE",
            "NONE"
         ]
      },
      {
         "name":"fileType",
         "title":"Select a fileType",
         "description":"Select fileType",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false,
         "enum":[
            "csv",
            "json",
            "parquet"
         ],
         "default":"csv"
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"S3",
      "iconUrl":"https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
      "connectionType":"S3",
      "flowRunsSupported":true,
      "monitoringSupported":true,
      "frequency":"Batch"
   },
   "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ],
   "identityNamespaces":{
      "adobe_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "mobile_id":{
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
            "name":"phoneNo",
            "title":"phoneNo",
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
   "batchConfig":{
      "allowMandatoryFieldSelection":true,
      "allowDedupeKeyFieldSelection":true,
      "defaultExportMode":"DAILY_FULL_EXPORT",
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
         "ONCE"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00",
      "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      },
      "backfillHistoricalProfileData":true
   }
```

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `name` | Tekenreeks | Geeft de titel van het doel in de catalogus met Experience Platforms aan. |
| `description` | Tekenreeks | Geef een beschrijving voor uw doelkaart op in de catalogus met Experience Platforms doelen. Doel voor niet meer dan 4-5 zinnen. |
| `status` | Tekenreeks | Geeft de levenscyclusstatus van de doelkaart aan. Accepteerde waarden zijn `TEST`, `PUBLISHED`, en `DELETED`. Gebruiken `TEST` wanneer u eerst uw bestemming vormt. |
| `maxProfileAttributes` | Tekenreeks | Geeft het maximumaantal profielkenmerken aan dat klanten naar het doel kunnen exporteren. De standaardwaarde is `2000`. |
| `maxIdentityAttributes` | Tekenreeks | Geeft het maximumaantal naamruimten aan dat klanten naar het doel kunnen exporteren. De standaardwaarde is `10`. |

{style=&quot;table-layout:auto&quot;}

## Verificatieconfiguraties van de klant {#customer-authentication-configurations}

Deze sectie in de bestemmingsconfiguratie produceert [Nieuwe bestemming configureren](/help/destinations/ui/connect-destination.md) pagina in het gebruikersinterface van het Experience Platform, waar de gebruikers Experience Platform met de rekeningen verbinden zij met uw bestemming hebben.

```json
"customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
```

Afhankelijk van welke [verificatieoptie](authentication-configuration.md##supported-authentication-types) u in het `authType` wordt de pagina Experience Platform voor de gebruikers als volgt gegenereerd:

### Amazon S3-verificatie {#s3}

Wanneer u het Amazon S3 authentificatietype vormt, worden de gebruikers vereist om de S3 geloofsbrieven in te voeren.

![UI die met S3 authentificatie teruggeeft](assets/s3-authentication-ui.png)

### Azure Blob-verificatie  {#blob}

Wanneer u het verificatietype Azure Blob configureert, moeten gebruikers de verbindingstekenreeks invoeren.

![UI-weergave met Blob-verificatie](assets/blob-authentication-ui.png)

### SFTP met wachtwoordverificatie

Wanneer u SFTP met het type van wachtwoordauthentificatie vormt, worden de gebruikers vereist om de gebruikersbenaming en het wachtwoord van SFTP, evenals het domein en de haven van SFTP in te voeren (de standaardhaven is 22).

![UI-weergave met SFTP met wachtwoordverificatie](assets/sftp-password-authentication-ui.png)

### SFTP met SSH-sleutelverificatie

Wanneer u SFTP met SSH zeer belangrijke authentificatietype vormt, worden de gebruikers vereist om de gebruikersbenaming van SFTP en de sleutel van SSH, evenals het domein en de haven van SFTP in te voeren (de standaardhaven is 22).

![UI-weergave met SFTP met SSH-sleutelverificatie](assets/sftp-key-authentication-ui.png)

## Gegevensvelden van de klant {#customer-data-fields}

Gebruik deze sectie om gebruikers te vragen aangepaste velden in te vullen, specifiek voor uw doel, wanneer u verbinding maakt met het doel in de gebruikersinterface van het Experience Platform.

In het onderstaande voorbeeld: `customerDataFields` vereist dat gebruikers een naam voor hun bestemming invoeren en een [!DNL Amazon S3] De naam van de emmertje en de omslagweg, evenals een compressietype, dossierformaat, en verscheidene andere opties van de dossieruitvoer.

```json
 "customerDataFields":[
      {
         "name":"bucket",
         "title":"Amazon S3 bucket name",
         "description":"Enter your Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Amazon S3 bucket path",
         "description":"Enter your S3 bucket path",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"sep",
         "title":"Enter a separator for each field and value",
         "description":"Enter a separator character for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Specify encoding (charset) of saved CSV files",
         "description":"Select encoding of csv files",
         "type":"string",
         "enum":[
            "UTF-8",
            "UTF-16"
         ],
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quote",
         "title":"Select a single character used for escaping quoted values",
         "description":"Select single charachter for escaping quoted values",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "default":"true",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escape",
         "title":"Select a single character used for escaping quotes",
         "description":"Select a single character used for escaping quotes inside an already quoted value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Escape quotes",
         "description":"A flag indicating whether values containing quotes should always be enclosed in quotes",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "isRequired":false,
         "default":"true",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"header",
         "title":"header",
         "description":"Writes the names of columns as the first line.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"ignoreLeadingWhiteSpace",
         "title":"Ignore leading white space",
         "description":"A flag indicating whether or not leading whitespaces from values being written should be skipped.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"nullValue",
         "title":"Select the string representation of a null value",
         "description":"Sets the string representation of a null value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Select the string that indicates a date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Char to escape quote escaping",
         "description":"Sets a single character used for escaping the escape for the quote character",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Select the string representation of an empty value",
         "description":"Select the string representation of an empty value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Select compression",
         "description":"Select compressiont",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "enum":[
            "SNAPPY",
            "GZIP",
            "DEFLATE",
            "NONE"
         ]
      },
      {
         "name":"fileType",
         "title":"Select a fileType",
         "description":"Select fileType",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false,
         "enum":[
            "csv",
            "json",
            "parquet"
         ],
         "default":"csv"
      }
```

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `name` | Tekenreeks | Geef een naam op voor het aangepaste veld dat u introduceert. |
| `title` | Tekenreeks | Hiermee wordt de naam van het veld aangegeven, zoals deze wordt weergegeven door klanten in de gebruikersinterface van het Experience Platform. |
| `description` | Tekenreeks | Geef een beschrijving op voor het aangepaste veld. |
| `type` | Tekenreeks | Hiermee geeft u aan welk type aangepast veld u wilt gebruiken. Accepteerde waarden zijn `string`, `object`, `integer`. |
| `isRequired` | Boolean | Geeft aan of dit veld vereist is in de workflow voor doelinstellingen. |
| `pattern` | Tekenreeks | Hiermee wordt, indien nodig, een patroon voor het aangepaste veld afgedwongen. Gebruik reguliere expressies om een patroon af te dwingen. Als uw klant-id&#39;s bijvoorbeeld geen cijfers of onderstrepingstekens bevatten, voert u `^[A-Za-z]+$` op dit gebied. |
| `enum` | Tekenreeks | Hiermee geeft u het aangepaste veld weer als een vervolgkeuzemenu en geeft u de opties weer die beschikbaar zijn voor de gebruiker. |
| `default` | Tekenreeks | Definieert de standaardwaarde op basis van een `enum` lijst. |

{style=&quot;table-layout:auto&quot;}

## UI-kenmerken {#ui-attributes}

Deze sectie verwijst naar de elementen UI in de configuratie hierboven die Adobe voor uw bestemming in het gebruikersinterface van Adobe Experience Platform zou moeten gebruiken.

```json
"uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"S3",
      "iconUrl":"https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
      "connectionType":"S3",
      "flowRunsSupported":true,
      "monitoringSupported":true,
      "frequency":"Batch"
   }
```

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `documentationLink` | Tekenreeks | Verwijst naar de documentatiepagina in [Doelcatalogus](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) voor uw bestemming. Gebruiken `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, waarbij `YOURDESTINATION` is de naam van uw bestemming. Voor een bestemming genoemd Moviestar, zou u gebruiken `http://www.adobe.com/go/destinations-moviestar-en`. Merk op dat deze verbinding slechts werkt nadat Adobe uw bestemming live plaatst en de documentatie wordt gepubliceerd. |
| `category` | Tekenreeks | Verwijst naar de rubriek die aan je bestemming in Adobe Experience Platform is toegewezen. Lees voor meer informatie [Doelcategorieën](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html). Gebruik een van de volgende waarden: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `iconUrl` | Tekenreeks | De URL waar u het pictogram hebt gehost dat in de cataloguskaart van de doelen moet worden weergegeven. |
| `connectionType` | Tekenreeks | Het type verbinding, afhankelijk van het doel. Ondersteunde waarden: <ul><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li></ul> |
| `flowRunsSupported` | Boolean | Geeft aan of de doelverbinding is opgenomen in het dialoogvenster [UI voor flowuitvoering](../../dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard). Wanneer u deze instelling instelt op `true`: <ul><li>De **[!UICONTROL Last dataflow run date]** en **[!UICONTROL Last dataflow run status]** worden weergegeven in de doelpagina voor bladeren.</li><li>De **[!UICONTROL Dataflow runs]** en **[!UICONTROL Activation data]** tabbladen worden weergegeven op de pagina van de doelweergave.</li></ul> |
| `monitoringSupported` | Boolean | Geeft aan of de doelverbinding is opgenomen in het dialoogvenster [UI controleren](../ui/destinations-workspace.md#browse). Wanneer u deze instelling instelt op `true`de **[!UICONTROL View in monitoring]** Deze optie wordt weergegeven in de doelpagina Bladeren. |
| `frequency` | Tekenreeks | Verwijst naar het type gegevens dat door de bestemming wordt gesteund. Instellen op `Batch` voor op bestanden gebaseerde doelen. |

{style=&quot;table-layout:auto&quot;}

## Levering bestemming {#destination-delivery}

```json
 "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
```

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `authenticationRule` | Tekenreeks | Geeft aan hoe [!DNL Platform] klanten verbinden met uw bestemming. Accepteerde waarden zijn `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Gebruiken `CUSTOMER_AUTHENTICATION` als de klanten van het Platform zich bij uw systeem via om het even welke volgende methodes aanmelden: <ul><li>`"authType": "S3"`</li><li>`"authType":"AZURE_CONNECTION_STRING"`</li><li>`"authType":"AZURE_SERVICE_PRINCIPAL"`</li><li>`"authType":"SFTP_WITH_SSH_KEY"`</li><li>`"authType":"SFTP_WITH_PASSWORD"`</li></ul> </li><li> Gebruiken `PLATFORM_AUTHENTICATION` als er een globaal authentificatiesysteem tussen Adobe en uw bestemming en is [!DNL Platform] de klant te hoeven om geen authentificatiegeloofsbrieven te verstrekken om met uw bestemming te verbinden. In dit geval moet u een object credentials maken met de opdracht [Credentials](./credentials-configuration-api.md) configuratie. </li><li>Gebruiken `NONE` als geen authentificatie wordt vereist om gegevens naar uw bestemmingsplatform te verzenden. </li></ul> |
| `destinationServerId` | Tekenreeks | De `instanceId` van de [doelserverconfiguratie](./destination-server-api.md) gebruikt voor deze bestemming. |

{style=&quot;table-layout:auto&quot;}

## Configuratie segmenttoewijzing {#segment-mapping}

Deze sectie van de bestemmingsconfiguratie heeft op hoe segmentmeta-gegevens zoals segmentnamen of IDs tussen Experience Platform en uw bestemming zouden moeten worden gedeeld.

Via de `audienceTemplateId`Deze sectie koppelt deze configuratie ook aan de [doelmetagegevensconfiguratie](./audience-metadata-management.md).

```json
   "segmentMappingConfig":{
       "mapExperiencePlatformSegmentName":false,
       "mapExperiencePlatformSegmentId":false,
       "mapUserInput":false,
       "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
```

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `mapExperiencePlatformSegmentName` | Boolean | Controls whether the segment mapping id in the destination activation workflow is the Experience Platform segment name. |
| `mapExperiencePlatformSegmentId` | Boolean | Controls whether the segment mapping id in the destination activation workflow is the Experience Platform segment ID. |
| `mapUserInput` | Boolean | Controls whether the segment mapping id in the destination activation workflow is input by user. |
| `audienceTemplateId` | Boolean | De `instanceId` van de [sjabloon voor doelmetagegevens](./audience-metadata-management.md) gebruikt voor deze bestemming. Als u een sjabloon voor publieksmetagegevens wilt instellen, leest u de [API-naslaggids voor doelmetagegevens](./audience-metadata-api.md). |

## Schemaconfiguratie in de toewijzingsstap {#schema-configuration}

Gebruik de parameters in `schemaConfig` om de toewijzingsstap van de workflow voor doelactivering in te schakelen. Aan de hand van de onderstaande parameters kunt u bepalen of gebruikers van Experience Platforms profielkenmerken en/of identiteiten kunnen toewijzen aan uw bestandsdoel.

```json
"schemaConfig":{
      "profileFields":[
           {
              "name":"phoneNo",
              "title":"phoneNo",
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
}
```

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `profileFields` | Array | Wanneer u vooraf gedefinieerde `profileFields`, hebben de gebruikers van het Experience Platform de optie om de attributen van het Platform aan de vooraf bepaalde attributen in uw bestemming toe te wijzen. |
| `profileRequired` | Boolean | Gebruiken `true` als de gebruikers profielattributen van Experience Platform aan douanekenmerken op de kant van uw bestemming zouden moeten kunnen in kaart brengen, zoals aangetoond in de voorbeeldconfiguratie hierboven. |
| `segmentRequired` | Boolean | Altijd gebruiken `segmentRequired:true`. |
| `identityRequired` | Boolean | Gebruiken `true` als gebruikers naamruimten van het Experience Platform aan uw gewenste schema moeten kunnen toewijzen. |

{style=&quot;table-layout:auto&quot;}

### Dynamische schemaconfiguratie in de kaartstap {#dynamic-schema-configuration}

Adobe Experience Platform Destination SDK steunt partner-bepaalde schema&#39;s. Een partner-bepaald schema staat gebruikers toe om profielattributen en identiteiten aan douaneschema&#39;s in kaart te brengen die door bestemmingspartners worden bepaald, gelijkend op [streaming doelen](destination-configuration.md#schema-configuration) workflow.

Gebruik de parameters in  `dynamicSchemaConfig` om uw eigen schema te bepalen dat de de profielattributen en/of identiteiten van het Platform aan kunnen worden in kaart gebracht.

```json
"schemaConfig":{
   "dynamicSchemaConfig":{
      "dynamicEnum": {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}",
         "value": "Schema Name",
         "responseFormat": "SCHEMA"
      }
   },
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
}
```

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `profileRequired` | Boolean | Gebruiken `true` als de gebruikers profielattributen van Experience Platform aan douanekenmerken op de kant van uw bestemming zouden moeten kunnen in kaart brengen, zoals aangetoond in de voorbeeldconfiguratie hierboven. |
| `segmentRequired` | Boolean | Altijd gebruiken `segmentRequired:true`. |
| `identityRequired` | Boolean | Gebruiken `true` als gebruikers naamruimten van het Experience Platform aan uw gewenste schema moeten kunnen toewijzen. |
| `destinationServerId` | Tekenreeks | De `instanceId` van de [doelserverconfiguratie](./destination-server-api.md) gebruikt voor deze bestemming. |
| `authenticationRule` | Tekenreeks | Geeft aan hoe [!DNL Platform] klanten verbinden met uw bestemming. Accepteerde waarden zijn `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Gebruiken `CUSTOMER_AUTHENTICATION` als de klanten van het Platform zich bij uw systeem via om het even welke volgende methodes aanmelden: <ul><li>`"authType": "S3"`</li><li>`"authType":"AZURE_CONNECTION_STRING"`</li><li>`"authType":"AZURE_SERVICE_PRINCIPAL"`</li><li>`"authType":"SFTP_WITH_SSH_KEY"`</li><li>`"authType":"SFTP_WITH_PASSWORD"`</li></ul> </li><li> Gebruiken `PLATFORM_AUTHENTICATION` als er een globaal authentificatiesysteem tussen Adobe en uw bestemming en is [!DNL Platform] de klant te hoeven om geen authentificatiegeloofsbrieven te verstrekken om met uw bestemming te verbinden. In dit geval moet u een object credentials maken met de opdracht [Credentials](./credentials-configuration-api.md) configuratie. </li><li>Gebruiken `NONE` als geen authentificatie wordt vereist om gegevens naar uw bestemmingsplatform te verzenden. </li></ul> |
| `value` | Tekenreeks | De naam van het schema dat in het gebruikersinterface van het Experience Platform, in de toewijzingsstap moet worden getoond. |
| `responseFormat` | Tekenreeks | Altijd instellen op `SCHEMA` wanneer u een aangepast schema definieert. |

{style=&quot;table-layout:auto&quot;}

## Identiteiten en kenmerken {#identities-and-attributes}

De parameters in deze sectie bepalen welke identiteiten uw bestemming goedkeurt. Deze configuratie vult ook de doelidentiteiten en -kenmerken in de [toewijzingsstap](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) van de gebruikersinterface van het Experience Platform, waar de gebruikers identiteiten en attributen van hun schema&#39;s XDM aan het schema in uw bestemming in kaart brengen.


```json
"identityNamespaces": {
        "adobe_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        },
        "mobile_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        }
    },
```

U moet aangeven welke [!DNL Platform] id&#39;s die klanten kunnen exporteren naar uw bestemming. Enkele voorbeelden zijn [!DNL Experience Cloud ID], gehashte e-mail, apparaat-id ([!DNL IDFA], [!DNL GAID]). Deze waarden zijn [!DNL Platform] identiteitsnaamruimten die klanten vanaf uw bestemming kunnen toewijzen aan naamruimten. U kunt ook aangeven of klanten aangepaste naamruimten kunnen toewijzen aan identiteiten die door uw doel worden ondersteund.

Naamruimten vereisen geen 1-op-1-overeenkomst tussen [!DNL Platform] en uw bestemming.
Klanten kunnen bijvoorbeeld een [!DNL Platform] [!DNL IDFA] naamruimte naar een [!DNL IDFA] naamruimte vanaf uw bestemming, of ze kunnen hetzelfde toewijzen [!DNL Platform] [!DNL IDFA] naamruimte naar een [!DNL Customer ID] naamruimte in uw doel.

## Batchconfiguratie {#batch-configuration}

Deze sectie verwijst naar de instellingen voor het exporteren van bestanden in de bovenstaande configuratie die Adobe moet gebruiken voor uw doel in de Adobe Experience Platform-gebruikersinterface.

```json
"batchConfig":{
   "allowMandatoryFieldSelection":true,
   "allowDedupeKeyFieldSelection":true,
   "defaultExportMode":"DAILY_FULL_EXPORT",
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
      "ONCE"
   ],
   "defaultFrequency":"DAILY",
   "defaultStartTime":"00:00",
   "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      },
   }
```

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `allowMandatoryFieldSelection` | Boolean | Instellen op `true` zodat klanten kunnen opgeven welke profielkenmerken verplicht zijn. De standaardwaarde is `false`. Zie [Verplichte kenmerken](../ui/activate-batch-profile-destinations.md#mandatory-attributes) voor meer informatie . |
| `allowDedupeKeyFieldSelection` | Boolean | Instellen op `true` om klanten toe te staan deduplicatietoetsen te specificeren. De standaardwaarde is `false`.  Zie [Deduplicatietoetsen](../ui/activate-batch-profile-destinations.md#deduplication-keys) voor meer informatie . |
| `defaultExportMode` | Enum | Hiermee definieert u de standaardexportmodus voor bestanden. Ondersteunde waarden:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> De standaardwaarde is `DAILY_FULL_EXPORT`. Zie de [documentatie voor batchactivering](../ui/activate-batch-profile-destinations.md#scheduling) voor meer informatie over het plannen van het exporteren van bestanden. |
| `allowedExportModes` | Lijst | Hiermee definieert u de exportmodi voor bestanden die beschikbaar zijn voor klanten. Ondersteunde waarden:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | Lijst | Hiermee definieert u de exportfrequentie voor bestanden die beschikbaar is voor klanten. Ondersteunde waarden:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | Enum | Definieert de standaard exportfrequentie voor bestanden.Ondersteunde waarden:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> De standaardwaarde is `DAILY`. |
| `defaultStartTime` | Tekenreeks | Hiermee definieert u de standaardbegintijd voor het exporteren van het bestand. Gebruikt een bestandsindeling van 24 uur. De standaardwaarde is &quot;00:00&quot;. |
| `filenameConfig.allowedFilenameAppendOptions` | Tekenreeks | *Vereist*. Lijst met beschikbare bestandsnaammacro&#39;s waaruit gebruikers kunnen kiezen. Hiermee bepaalt u welke items aan geëxporteerde bestandsnamen worden toegevoegd (onder andere segment-id, naam van de organisatie, datum en tijd van export). Wanneer instellen `defaultFilename`, moet u dubbele macro&#39;s voorkomen. <br><br>Ondersteunde waarden: <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>Ongeacht de orde waarin u de macro&#39;s bepaalt, zal Experience Platform UI altijd hen in de hier voorgestelde orde tonen. <br><br> Indien `defaultFilename` is leeg, de `allowedFilenameAppendOptions` lijst moet ten minste één macro bevatten. |
| `filenameConfig.defaultFilenameAppendOptions` | Tekenreeks | *Vereist*. Vooraf geselecteerde standaardbestandsnaammacro&#39;s die gebruikers kunnen uitschakelen.<br><br> De macro&#39;s in deze lijst zijn een subset van de macro&#39;s die zijn gedefinieerd in `allowedFilenameAppendOptions`. |
| `filenameConfig.defaultFilename` | Tekenreeks | *Optioneel*. Hiermee definieert u de standaardbestandsnamen van macro&#39;s voor de geëxporteerde bestanden. Deze kunnen niet worden overschreven door gebruikers. <br><br>Elke macro gedefinieerd door `allowedFilenameAppendOptions` wordt toegevoegd na de `defaultFilename` macro&#39;s. <br><br>Indien `defaultFilename` is leeg, moet u ten minste één macro definiëren in `allowedFilenameAppendOptions`. |

{style=&quot;table-layout:auto&quot;}

### Configuratie bestandsnaam {#file-name-configuration}

Gebruik de configuratiesymbolen voor bestandsnamen om te definiëren wat de geëxporteerde bestandsnamen moeten bevatten. De macro&#39;s in de onderstaande tabel beschrijven de elementen in de gebruikersinterface in het dialoogvenster [bestandsnaamconfiguratie](../ui/activate-batch-profile-destinations.md#file-names) scherm.

Als beste praktijken moet u altijd omvatten `SEGMENT_ID` in de geëxporteerde bestandsnamen. Segment-id&#39;s zijn uniek, dus het opnemen ervan in de bestandsnaam is de beste manier om ervoor te zorgen dat bestandsnamen ook uniek zijn.

| Macro | UI-label | Beschrijving | Voorbeeld |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL Destination] | Doelnaam in de gebruikersinterface. | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL Segment ID] | Unieke, door Platform gegenereerde segment-id | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL Segment Name] | Door gebruiker gedefinieerde segmentnaam | VIP abonnee |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL Destination ID] | Unieke, door Platform gegenereerde id van de doelinstantie | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL Destination Name] | Door gebruiker gedefinieerde naam van de doelinstantie. | Mijn advertentiebestemming 2022 |
| `ORGANIZATION_NAME` | [!UICONTROL Organization Name] | Naam van de klantenorganisatie in Adobe Experience Platform. | Naam van mijn organisatie |
| `SANDBOX_NAME` | [!UICONTROL Sandbox Name] | Naam van de sandbox die door de klant wordt gebruikt. | prod |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL Date and time] | `DATETIME` en `TIMESTAMP` beide definiëren wanneer het bestand is gegenereerd, maar in verschillende indelingen. <br><br><ul><li>`DATETIME` gebruikt de volgende indeling: YYYMMDD_HMMSS.</li><li>`TIMESTAMP` gebruikt de Unix-indeling van 10 cijfers. </li></ul> `DATETIME` en `TIMESTAMP` elkaar uitsluiten en niet gelijktijdig kunnen worden gebruikt. | <ul><li>`DATETIME`: 20220509_210543</li><li>`TIMESTAMP`: 1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL Custom text] | Door de gebruiker gedefinieerde aangepaste tekst die in de bestandsnaam moet worden opgenomen. Kan niet gebruiken in `defaultFilename`. | My_custom_text |
| `TIMESTAMP` | [!UICONTROL Date and time] | Tijdstempel van 10 cijfers van het tijdstip waarop het bestand is gegenereerd, in Unix-indeling. | 1652131584 |

{style=&quot;table-layout:auto&quot;}

![UI-afbeelding die het configuratiescherm voor de bestandsnaam met vooraf geselecteerde macro&#39;s weergeeft](assets/file-name-configuration.png)

In het voorbeeld in de bovenstaande afbeelding wordt de volgende macroconfiguratie voor de bestandsnaam gebruikt:

```json
"filenameConfig":{
   "allowedFilenameAppendOptions":[
      "CUSTOM_TEXT",
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilenameAppendOptions":[
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilename": "%DESTINATION%"
}
```


## Historische profielkwalificaties {#profile-backfill}

U kunt de `backfillHistoricalProfileData` parameter in de bestemmingsconfiguratie om te bepalen als de historische profielkwalificaties naar uw bestemming zouden moeten worden uitgevoerd.

```json
   "backfillHistoricalProfileData":true
```

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `backfillHistoricalProfileData` | Boolean | Bepaalt of historische profielgegevens worden geëxporteerd wanneer segmenten worden geactiveerd naar de bestemming. <br> <ul><li> `true`: [!DNL Platform] verzendt de historische gebruikersprofielen die voor het segment kwalificeren alvorens het segment wordt geactiveerd. </li><li> `false`: [!DNL Platform] omvat alleen gebruikersprofielen die in aanmerking komen voor het segment nadat het segment is geactiveerd. </li></ul> |

{style=&quot;table-layout:auto&quot;}

## Hoe deze configuratie alle noodzakelijke informatie voor uw bestemming verbindt {#connecting-all-configurations}

Sommige van uw bestemmingsmontages moeten door worden gevormd [doelserver](./server-and-file-configuration.md) of de [doelmetagegevensconfiguratie](./audience-metadata-management.md). De bestemmingsconfiguratie die hier wordt beschreven verbindt al deze montages door de twee andere configuraties als volgt van verwijzingen te voorzien:

* Gebruik de `destinationServerId` om naar de bestemmingsserver en malplaatjeconfiguratie te verwijzen opstelling voor uw bestemming.
* Gebruik de `audienceMetadataId` om naar de configuratie van publieksmeta-gegevens te verwijzen opstelling voor uw bestemming.
