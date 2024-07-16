---
description: Leer hoe u Destination SDK gebruikt om een Amazon S3-bestemming te configureren met vooraf gedefinieerde opties voor bestandsindeling en aangepaste configuratie van bestandsnamen.
title: Configureer een Amazon S3-bestemming met vooraf gedefinieerde opties voor bestandsindeling en aangepaste configuratie van bestandsnamen.
exl-id: 0ecd3575-dcda-4e5c-af5c-247d4ea13fa1
source-git-commit: 45ba0db386f065206f89ed30bfe7b0c1b44f6173
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 0%

---

# Een [!DNL Amazon S3] -doel configureren met vooraf gedefinieerde opties voor bestandsindeling en aangepaste configuratie van bestandsnaam

## Overzicht {#overview}

Deze pagina beschrijft hoe te om Destination SDK te gebruiken om een bestemming van Amazon S3 met vooraf bepaalde, standaard [ dossier het formatteren opties ](configure-file-formatting-options.md) en een douane [ dossier te vormen - noem configuratie ](../../functionality/destination-configuration/batch-configuration.md#file-name-configuration).

Op deze pagina worden alle configuratieopties weergegeven die beschikbaar zijn voor [!DNL Amazon S3] -doelen. U kunt de configuraties bewerken die in de onderstaande stappen worden weergegeven, of u kunt desgewenst bepaalde onderdelen van de configuraties verwijderen.

Voor gedetailleerde beschrijvingen van de hieronder gebruikte parameters, zie [ configuratieopties in Doelen SDK ](../../functionality/configuration-options.md).

## Vereisten {#prerequisites}

Alvorens aan de hieronder geschetste stappen vooruit te gaan, te lezen gelieve de [ Destination SDK begonnen ](../../getting-started.md) pagina voor informatie over het verkrijgen van de noodzakelijke de authentificatiegeloofsbrieven van de Adobe I/O en andere eerste vereisten om met Destination SDK APIs te werken.

## Stap 1: Een server- en bestandsconfiguratie maken {#create-server-file-configuration}

Begin door het `/destination-server` eindpunt te gebruiken [ creeer een server en dossierconfiguratie ](../../authoring-api/destination-server/create-destination-server.md).

**API formaat**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe configuratie van de bestemmingsserver, die door de parameters wordt gevormd die in de lading worden verstrekt.
De nuttige lading omvat hieronder een generische [!DNL Amazon S3] configuratie, met vooraf bepaalde, standaard [ CSV dossier het formatteren ](../../functionality/destination-server/file-formatting.md) configuratieparameters die de gebruikers in de Experience Platform UI kunnen bepalen.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "name": "Amazon S3 destination server with predefined default CSV options",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucket": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.bucketName}}"
        },
        "path": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.path}}"
        }
    },
    "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}'
```

Een succesvolle reactie keert de nieuwe configuratie van de bestemmingsserver, met inbegrip van het unieke herkenningsteken (`instanceId`) van de configuratie terug. Sla deze waarde op zoals deze in de volgende stap wordt vereist.

## Stap 2: Doelconfiguratie maken {#create-destination-configuration}

Na het creëren van de bestemmingsserver en de dossier het formatteren configuratie in de vorige stap, kunt u het `/destinations` API eindpunt nu gebruiken om een bestemmingsconfiguratie tot stand te brengen.

Om de serverconfiguratie in [ stap 1 ](#create-server-file-configuration) aan deze bestemmingsconfiguratie aan te sluiten, vervang de `destinationServerId` waarde in het API verzoek hieronder met de `instanceId` waarde die wordt verkregen wanneer het creëren van uw bestemmingsserver in [ stap 1 ](#create-server-file-configuration).

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
   "name":"Amazon S3 destination with predefined CSV formatting options",
   "description":"Amazon S3 destination with predefined CSV formatting options",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerEncryptionConfigurations":[
       
   ],
   "customerDataFields":[
      {
         "name":"bucketName",
         "title":"Enter the name of your Amazon S3 bucket",
         "description":"Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Enter the path to your S3 bucket folder",
         "description":"Enter the path to your S3 bucket folder",
         "type":"string",
         "isRequired":true,
         "pattern": "^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
         "readOnly":false,
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
      "documentationLink":"https://www.adobe.com/go/destinations-amazon-s3-en",
      "category":"cloudStorage",
      "icon":{
         "key":"amazonS3"
      },
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
   "schemaConfig":{
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
}'
```

Een succesvolle reactie keert de nieuwe bestemmingsconfiguratie, met inbegrip van het unieke herkenningsteken (`instanceId`) van de configuratie terug. Sla deze waarde op zoals nodig is als u meer HTTP-aanvragen moet indienen om de doelconfiguratie bij te werken.

## Stap 3: Verifieer de gebruikersinterface van het Experience Platform {#verify-ui}

Op basis van de bovenstaande configuraties wordt in de catalogus met Experience Platforms nu een nieuwe persoonlijke doelkaart weergegeven die u kunt gebruiken.

![ opname die van het Scherm de pagina van de bestemmingscatalogus met een geselecteerde bestemmingskaart toont.](../../assets/guides/batch/destination-card.gif)

In de beelden en de opnamen hieronder, neem nota hoe de opties in het [ activeringswerkschema voor op dossier-gebaseerde bestemmingen ](../../../ui/activate-batch-profile-destinations.md) de opties aanpassen die u in de bestemmingsconfiguratie selecteerde.

Wanneer u details over de bestemming invult, ziet u hoe de velden omringd zijn de aangepaste gegevensvelden die u instelt in de configuratie.

>[!TIP]
>
>De orde waarin u de gebieden van douanegegevens aan de bestemmingsconfiguratie toevoegt wordt niet weerspiegeld in UI. De gegevensvelden van de klant worden altijd weergegeven in de volgorde die hieronder in de schermopname wordt weergegeven.

![ het registreren van het scherm die de gebieden van klantengegevens tonen die in uw configuratie worden bepaald.](../../assets/guides/batch/file-configuration-options.gif)

Wanneer u exportintervallen wilt plannen, ziet u hoe de velden die u opgeeft, de velden zijn die u instelt in de `batchConfig` -configuratie.
![ de uitvoer die opties plannen ](../../assets/guides/batch/file-export-scheduling.png)

Wanneer u de opties voor de configuratie van bestandsnamen weergeeft, ziet u hoe de weergegeven velden de `filenameConfig` -opties vertegenwoordigen die u instelt in de configuratie.
![ filename configuratieopties ](../../assets/guides/batch/file-naming-options.gif)

Als u om het even welke hierboven vermelde gebieden wilt aanpassen, herhaal [ stappen één ](#create-server-file-configuration) en [ twee ](#create-destination-configuration) om de configuraties volgens uw behoeften te wijzigen.

## Stap 4: (Optioneel) Publish uw bestemming {#publish-destination}

>[!NOTE]
>
>Deze stap wordt niet vereist als u een privé bestemming voor uw eigen gebruik creeert, en kijkt niet om het in de catalogus van bestemmingen voor andere te gebruiken klanten te publiceren.

Na het vormen van uw bestemming, gebruik [ bestemmings het publiceren API ](../../publishing-api/create-publishing-request.md) om uw configuratie voor overzicht voor te leggen aan Adobe.

## Stap 5: (Optioneel) Documenteer uw bestemming {#document-destination}

>[!NOTE]
>
>Deze stap wordt niet vereist als u een privé bestemming voor uw eigen gebruik creeert, en kijkt niet om het in de catalogus van bestemmingen voor andere te gebruiken klanten te publiceren.

Als u een Onafhankelijke Verkoper van de Software (ISV) of Integrator van het Systeem (SI) creërend a [ geproduceerde integratie ](../../overview.md#productized-custom-integrations) bent, gebruik het [ zelfbedienings documentatieproces ](../../docs-framework/documentation-instructions.md) om een pagina van de productdocumentatie voor uw bestemming in de [ catalogus van de bestemmingen van het Experience Platform ](../../../catalog/overview.md) tot stand te brengen.

## Volgende stappen {#next-steps}

Door dit artikel te lezen, weet u nu hoe u een aangepaste [!DNL Amazon S3] -bestemming kunt maken met behulp van Destination SDK. Daarna, kan uw team het [ activeringswerkschema voor op dossier-gebaseerde bestemmingen ](../../../ui/activate-batch-profile-destinations.md) gebruiken om gegevens naar de bestemming uit te voeren.
