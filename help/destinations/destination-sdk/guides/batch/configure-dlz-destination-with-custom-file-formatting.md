---
description: Leer hoe te om Destination SDK te gebruiken om een bestemming van de Landing van Gegevens (DLZ) met de opties van de douanedossier het formatteren en de configuratie van de douanedossier te vormen - noem.
title: Configureer een DLZ-bestemming (Data Landing Zone) met aangepaste opties voor bestandsindeling en aangepaste configuratie van bestandsnamen.
exl-id: 3a5c1188-c2b5-4e81-ae41-9fff797f08a6
source-git-commit: d47c82339afa602a9d6914c1dd36a4fc9528ea32
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---

# Een [!DNL Data Landing Zone (DLZ)] -doel configureren met aangepaste opties voor bestandsindeling en aangepaste configuratie van bestandsnaam

## Overzicht {#overview}

Deze pagina beschrijft hoe te om Destination SDK te gebruiken om a [!DNL Data Landing Zone] bestemming met het douane[&#x200B; dossier te vormen formatterend opties &#x200B;](configure-file-formatting-options.md) en een de naamconfiguratie van het douanedossier [&#128279;](../../functionality/destination-configuration/batch-configuration.md#file-name-configuration).

Op deze pagina worden alle configuratieopties weergegeven die beschikbaar zijn voor [!DNL Data Landing Zone] -doelen. U kunt de configuraties bewerken die in de onderstaande stappen worden weergegeven, of u kunt desgewenst bepaalde onderdelen van de configuraties verwijderen.

Voor gedetailleerde beschrijvingen van de hieronder gebruikte parameters, zie [&#x200B; configuratieopties in Doelen SDK &#x200B;](../../functionality/configuration-options.md).

## Vereisten {#prerequisites}

Alvorens aan de hieronder geschetste stappen vooruit te gaan, te lezen gelieve de [&#x200B; Destination SDK begonnen &#x200B;](../../getting-started.md) pagina voor informatie over het verkrijgen van de noodzakelijke de authentificatiegeloofsbrieven van de Adobe I/O en andere eerste vereisten om met Destination SDK APIs te werken.

## Stap 1: Een server- en bestandsconfiguratie maken {#create-server-file-configuration}

Begin door het `/destination-server` eindpunt te gebruiken [&#x200B; creeer een server en dossierconfiguratie &#x200B;](../../authoring-api/destination-server/create-destination-server.md).

**API formaat**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe configuratie van de bestemmingsserver, die door de parameters wordt gevormd die in de lading worden verstrekt.
De nuttige lading omvat hieronder een generische [!DNL Data Landing Zone] configuratie, met douane [&#x200B; CSV dossier het formatteren &#x200B;](../../functionality/destination-server/file-formatting.md) configuratieparameters die de gebruikers in Experience Platform UI kunnen bepalen.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
 -d '
{
   "name":"DLZ Destination Server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "fileConfigurations":{
         "compression":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.compression}}"
         },
         "fileType":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.fileType}}"
         },
         "csvOptions":{
            "sep":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.sep}}"
            },
            "encoding":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.encoding}}"
            },
            "quote":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.quote}}"
            },
            "quoteAll":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.quoteAll}}"
            },
            "escape":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.escape}}"
            },
            "escapeQuotes":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.escapeQuotes}}"
            },
            "header":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.header}}"
            },
            "ignoreLeadingWhiteSpace":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.ignoreLeadingWhiteSpace}}"
            },
            "nullValue":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.nullValue}}"
            },
            "dateFormat":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.dateFormat}}"
            },
            "charToEscapeQuoteEscaping":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.charToEscapeQuoteEscaping}}"
            },
            "emptyValue":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.dateFormat}}"
            }
         }
      }
   }
}'
```

Een succesvolle reactie keert de nieuwe configuratie van de bestemmingsserver, met inbegrip van het unieke herkenningsteken (`instanceId`) van de configuratie terug. Sla deze waarde op zoals deze in de volgende stap wordt vereist.

## Stap 2: Doelconfiguratie maken {#create-destination-configuration}

Na het creëren van de bestemmingsserver en de dossier het formatteren configuratie in de vorige stap, kunt u het `/destinations` API eindpunt nu gebruiken om een bestemmingsconfiguratie tot stand te brengen.

Om de serverconfiguratie in [&#x200B; stap 1 &#x200B;](#create-server-file-configuration) aan deze bestemmingsconfiguratie aan te sluiten, vervang de `destinationServerId` waarde in het API verzoek hieronder met de waarde die wordt verkregen wanneer het creëren van uw bestemmingsserver in [&#x200B; stap 1 &#x200B;](#create-server-file-configuration).

**API formaat**

```http
POST platform.adobe.io/data/core/activation/authoring/destinations
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"DLZ Destination",
   "description":"SSD DLZ Destination",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
       
   ],
   "customerEncryptionConfigurations":[
       
   ],
   "customerDataFields":[
      {
         "name":"path",
         "title":"Folder path",
         "description":"Enter the path to your Data Landing Zone folder",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"sep",
         "title":"Enter your desired separator for each field and value",
         "description":"Enter your desired separator for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Select the desired CSV file encoding",
         "description":"Select the desired CSV file encoding",
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
         "title":"Quoted values escape character",
         "description":"Enter the desired character to be used for escaping quoted values.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values.",
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
         "title":"Quote escaping character",
         "description":"Enter the desired character to be used for escaping quotes inside an already quoted value.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Enclose quoted values within quotes",
         "description":"Select whether values containing quotes should always be enclosed in quotes.",
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
         "title":"Generate file header.",
         "description":"Select whether to write the names of columns as the first line of the exported files.",
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
         "description":"Select whether leading whitespaces should be trimmed from exported values.",
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
         "title":"NULL value string format",
         "description":"Enter the string representation of a NULL value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Enter the desired date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Quote escaping escape character",
         "description":"Enter the desired character to be used for escaping the escaping of a quote character.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Empty value string format",
         "description":"Enter the string representation of an empty value.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Compression format",
         "description":"Select the desired file compression format.",
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
         "title":"File type",
         "description":"Select the exported file type.",
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
      "documentationLink":"https://www.adobe.io/apis/experienceplatform.html",
      "category":"DLZ",
      "connectionType":"Server-to-server",
      "frequency":"Batch",
      "flowRunsSupported":true,
      "monitoringSupported":true
   },
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
      "mapUserInput":false
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
         "authenticationRule":"NONE",
         "destinationServerId":"{{instanceID of your destination server}}"
      }
   ],
   "schemaConfig":{
      "profileRequired":true,
      "identityRequired":true,
      "segmentRequired":true
   },
   "batchConfig":{
      "allowMandatoryFieldSelection":true,
      "autoSelectJoinKeyOnPartnerSchemaSelection":false,
      "joinKeyTitle":"DEDUPLICATION KEY",
      "defaultExportMode":"DAILY_FULL_EXPORT",
      "allowedExportModes":[
         "DAILY_FULL_EXPORT",
         "FIRST_FULL_THEN_INCREMENTAL"
      ],
      "allowedScheduleFrequency":[
         "DAILY",
         "EVERY_3_HOURS",
         "EVERY_6_HOURS",
         "EVERY_12_HOURS",
         "EVERY_8_HOURS",
         "ONCE",
         "EVERY_HOUR"
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
      "allowDedupKeyFieldSelection":true
   },
   "backfillHistoricalProfileData":true
}'
```

Een succesvolle reactie keert de nieuwe bestemmingsconfiguratie, met inbegrip van het unieke herkenningsteken (`instanceId`) van de configuratie terug. Sla deze waarde op zoals nodig is als u meer HTTP-aanvragen moet indienen om de doelconfiguratie bij te werken.

## Stap 3: Verifieer de gebruikersinterface van het Experience Platform {#verify-ui}

Op basis van de bovenstaande configuraties wordt in de catalogus met Experience Platforms nu een nieuwe persoonlijke doelkaart weergegeven die u kunt gebruiken.

![&#x200B; opname die van het Scherm de pagina van de bestemmingscatalogus met een geselecteerde bestemmingskaart toont.](../../assets/guides/batch/dlz-destination-card.gif)

In de beelden en de opnamen hieronder, neem nota hoe de opties in het [&#x200B; activeringswerkschema voor op dossier-gebaseerde bestemmingen &#x200B;](../../../ui/activate-batch-profile-destinations.md) de opties aanpassen die u in de bestemmingsconfiguratie selecteerde.

Wanneer u details over de bestemming invult, ziet u hoe de velden omringd zijn de aangepaste gegevensvelden die u instelt in de configuratie.

>[!TIP]
>
>De orde waarin u de gebieden van douanegegevens aan de bestemmingsconfiguratie toevoegt wordt niet weerspiegeld in UI. De aangepaste gegevensvelden worden altijd weergegeven in de volgorde die wordt weergegeven in de onderstaande schermopname.

![&#x200B; vul bestemmingsdetails &#x200B;](../../assets/guides/batch/file-configuration-options.gif) in

Wanneer u exportintervallen wilt plannen, ziet u hoe de velden die u opgeeft, de velden zijn die u instelt in de `batchConfig` -configuratie.
![&#x200B; de uitvoer die opties plannen &#x200B;](../../assets/guides/batch/file-export-scheduling.png)

Wanneer u de opties voor de configuratie van bestandsnamen weergeeft, ziet u hoe de weergegeven velden de `filenameConfig` -opties vertegenwoordigen die u instelt in de configuratie.
![&#x200B; filename configuratieopties &#x200B;](../../assets/guides/batch/file-naming-options.gif)

Als u om het even welke hierboven vermelde gebieden wilt aanpassen, herhaal [&#x200B; stappen één &#x200B;](#create-server-file-configuration) en [&#x200B; twee &#x200B;](#create-destination-configuration) om de configuraties volgens uw behoeften te wijzigen.

## Stap 4: (Optioneel) Publish uw bestemming {#publish-destination}

>[!NOTE]
>
>Deze stap wordt niet vereist als u een privé bestemming voor uw eigen gebruik creeert, en kijkt niet om het in de catalogus van bestemmingen voor andere te gebruiken klanten te publiceren.

Na het vormen van uw bestemming, gebruik [&#x200B; bestemmings het publiceren API &#x200B;](../../publishing-api/create-publishing-request.md) om uw configuratie voor overzicht voor te leggen aan Adobe.

## Stap 5: (Optioneel) Documenteer uw bestemming {#document-destination}

>[!NOTE]
>
>Deze stap wordt niet vereist als u een privé bestemming voor uw eigen gebruik creeert, en kijkt niet om het in de catalogus van bestemmingen voor andere te gebruiken klanten te publiceren.

Als u een Onafhankelijke Verkoper van de Software (ISV) of Integrator van het Systeem (SI) creërend a [&#x200B; geproduceerde integratie &#x200B;](../../overview.md#productized-custom-integrations) bent, gebruik het [&#x200B; zelfbedienings documentatieproces &#x200B;](../../docs-framework/documentation-instructions.md) om een pagina van de productdocumentatie voor uw bestemming in de [&#x200B; catalogus van de bestemmingen van het Experience Platform &#x200B;](../../../catalog/overview.md) tot stand te brengen.

## Volgende stappen {#next-steps}

Door dit artikel te lezen, weet u nu hoe u een aangepaste [!DNL Data Landing Zone] -bestemming kunt maken met behulp van Destination SDK. Daarna, kan uw team het [&#x200B; activeringswerkschema voor op dossier-gebaseerde bestemmingen &#x200B;](../../../ui/activate-batch-profile-destinations.md) gebruiken om gegevens naar de bestemming uit te voeren.
