---
description: Deze pagina bevat een overzicht en beschrijving van de stappen voor het configureren van een bestandsgebaseerde bestemming met Destination SDK.
title: Destination SDK gebruiken om een bestandsgebaseerde bestemming te configureren
exl-id: 84d73452-88e4-4e0f-8fc7-d0d8e10f9ff5
source-git-commit: 560200a6553a1aae66c608eef7901b3248c886b4
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 0%

---

# Destination SDK gebruiken om een bestandsgebaseerde bestemming te configureren

## Overzicht {#overview}

Deze pagina beschrijft hoe te om de informatie in [&#x200B; opties van de Configuratie in Doelen SDK &#x200B;](../functionality/configuration-options.md) en in andere functionaliteit van Destination SDK en API verwijzingsdocumenten te gebruiken om a [&#x200B; op dossier-gebaseerde bestemming &#x200B;](../../destination-types.md#file-based) te vormen. De stappen worden in de onderstaande volgorde weergegeven.

## Vereisten {#prerequisites}

Alvorens aan de hieronder getoonde stappen vooruit te gaan, te lezen gelieve [&#x200B; Destination SDK begonnen &#x200B;](../getting-started.md) pagina voor informatie over het verkrijgen van de noodzakelijke de authentificatiegeloofsbrieven van Adobe I/O en andere eerste vereisten om met Destination SDK APIs te werken.

## Stappen om de configuratieopties in Destination SDK aan opstelling te gebruiken uw bestemming {#steps}

![&#x200B; geïllustreerde stappen om eindpunten van Destination SDK te gebruiken &#x200B;](../assets/guides/destination-sdk-steps-batch.png)

## Stap 1: Een server- en bestandsconfiguratie maken {#create-server-file-configuration}

Begin door [&#x200B; creërend een server en dossierconfiguratie &#x200B;](../authoring-api/destination-server/create-destination-server.md) gebruikend het `/destinations-server` eindpunt.

Hieronder ziet u een voorbeeldconfiguratie voor een [!DNL Amazon S3] -doel. Voor meer details over de gebieden die in de configuratie worden gebruikt en om andere soorten op dossier-gebaseerde bestemmingen te vormen, zie hun overeenkomstige [&#x200B; serverconfiguraties &#x200B;](../functionality/destination-server/server-specs.md).

**API formaat**

```shell
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

```json
{
    "name": "S3 destination",
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
}
```

## Stap 2: Doelconfiguratie maken {#create-destination-configuration}

Hieronder ziet u een voorbeeld van een doelconfiguratie die is gemaakt met het API-eindpunt van `/destinations` .

Als u de server- en bestandsconfiguratie vanaf stap 1 wilt verbinden met deze doelconfiguratie, voegt u de `instance ID` van de server- en bestandsconfiguratie hier `destinationServerId` toe.

**API formaat**

```http
POST platform.adobe.io/data/core/activation/authoring/destinations
```

```json {line-numbers="true" highlight="83"}
{
    "name": "Amazon S3 destination",
    "description": "Amazon S3 destination is a fictional destination, used for this example.",
    "status": "Test",
    "customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
    "customerEncryptionConfigurations": [],
    "customerDataFields": [
        {
            "name": "bucketName",
            "title": "Amazon S3 bucket name",
            "description": "Enter the Amazon S3 Bucket name that will host the exported files.",
            "type": "string",
            "isRequired": true,
            "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "path",
            "title": "Amazon S3 path",
            "description": "Enter Amazon S3 folder path",
            "type": "string",
            "isRequired": true,
            "pattern": "^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "compression",
            "title": "Select compression type",
            "description": "Select the file compression type used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "enum": [
                "GZIP",
                "NONE",
                "bzip2",
                "lz4",
                "snappy",
                "deflate"
            ]
        },
        {
            "name": "fileType",
            "title": "Select a file format",
            "description": "Select the file format to be used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "hidden": false,
            "enum": [
                "csv",
                "json",
                "parquet"
            ],
            "default": "csv"
        }
    ],
    "uiAttributes": {
        "documentationLink": "https://www.adobe.com/go/destinations-YOURDESTINATION-en",
        "category": "S3",
        "connectionType": "S3",
        "flowRunsSupported": true,
        "monitoringSupported": true,
        "frequency": "Batch"
    },
    "destinationDelivery": [
        {
            "deliveryMatchers": [
                {
                    "type": "SOURCE",
                    "value": [
                        "batch"
                    ]
                }
            ],
            "authenticationRule": "CUSTOMER_AUTHENTICATION",
            "destinationServerId": "eec25bde-4f56-4c02-a830-9aa9ec73ee9d"
        }
    ],
    "schemaConfig": {
        "profileRequired": true,
        "segmentRequired": true,
        "identityRequired": true
    },
    "batchConfig": {
        "allowMandatoryFieldSelection": true,
        "allowDedupeKeyFieldSelection": true,
        "defaultExportMode": "DAILY_FULL_EXPORT",
        "allowedExportMode": [
            "DAILY_FULL_EXPORT",
            "FIRST_FULL_THEN_INCREMENTAL"
        ],
        "allowedScheduleFrequency": [
            "DAILY",
            "EVERY_3_HOURS",
            "EVERY_6_HOURS",
            "EVERY_8_HOURS",
            "EVERY_12_HOURS",
            "ONCE"
        ],
        "defaultFrequency": "DAILY",
        "defaultStartTime": "00:00",
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
      }
    },
    "backfillHistoricalProfileData": true
}
```

## Stap 3: configuratie van publiekmetagegevens maken {#create-audience-metadata-configuration}

Voor sommige bestemmingen, vereist Destination SDK dat u een configuratie van publieksmeta-gegevens vormt om publiek in uw bestemming programmatically tot stand te brengen bij te werken of te schrappen. Verwijs naar [&#x200B; het meta-gegevensbeheer van het publiek &#x200B;](../functionality/audience-metadata-management.md) voor informatie over wanneer u aan opstelling deze configuratie en hoe te om het te doen moet.

Als u een configuratie van publieksmeta-gegevens gebruikt, moet u het met de bestemmingsconfiguratie verbinden u in stap 2 creeerde. Voeg de instantie-id van de configuratie van de publieksmetagegevens als `audienceTemplateId` toe aan de doelconfiguratie.

```json {line-numbers="true" highlight="90"}
{
    "name": "Amazon S3 destination",
    "description": "Amazon S3 destination is a fictional destination, used for this example.",
    "status": "Test",
    "customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
    "customerEncryptionConfigurations": [],
    "customerDataFields": [
        {
            "name": "bucketName",
            "title": "Amazon S3 bucket name",
            "description": "Enter the Amazon S3 Bucket name that will host the exported files.",
            "type": "string",
            "isRequired": true,
            "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "path",
            "title": "Amazon S3 path",
            "description": "Enter Amazon S3 folder path",
            "type": "string",
            "isRequired": true,
            "pattern": "^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "compression",
            "title": "Select compression type",
            "description": "Select the file compression type used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "enum": [
                "GZIP",
                "NONE",
                "bzip2",
                "lz4",
                "snappy",
                "deflate"
            ]
        },
        {
            "name": "fileType",
            "title": "Select a file format",
            "description": "Select the file format to be used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "hidden": false,
            "enum": [
                "csv",
                "json",
                "parquet"
            ],
            "default": "csv"
        }
    ],
    "uiAttributes": {
        "documentationLink": "http://www.adobe.com/go/destinations-YOURDESTINATION-en",
        "category": "S3",
        "connectionType": "S3",
        "flowRunsSupported": true,
        "monitoringSupported": true,
        "frequency": "Batch"
    },
    "destinationDelivery": [
        {
            "deliveryMatchers": [
                {
                    "type": "SOURCE",
                    "value": [
                        "batch"
                    ]
                }
            ],
            "authenticationRule": "CUSTOMER_AUTHENTICATION",
            "destinationServerId": "eec25bde-4f56-4c02-a830-9aa9ec73ee9d"
        }
    ],
    "segmentMappingConfig":{
        "mapExperiencePlatformSegmentName":false,
        "mapExperiencePlatformSegmentId":false,
        "mapUserInput":false
    },
    "audienceMetadataConfig":{
        "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
    },   
    "schemaConfig": {
        "profileRequired": true,
        "segmentRequired": true,
        "identityRequired": true
    },
    "batchConfig": {
        "allowMandatoryFieldSelection": true,
        "allowDedupeKeyFieldSelection": true,
        "defaultExportMode": "DAILY_FULL_EXPORT",
        "allowedExportMode": [
            "DAILY_FULL_EXPORT",
            "FIRST_FULL_THEN_INCREMENTAL"
        ],
        "allowedScheduleFrequency": [
            "DAILY",
            "EVERY_3_HOURS",
            "EVERY_6_HOURS",
            "EVERY_8_HOURS",
            "EVERY_12_HOURS",
            "ONCE"
        ],
        "defaultFrequency": "DAILY",
        "defaultStartTime": "00:00",
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
      }
    },
    "backfillHistoricalProfileData": true
}
```

## Stap 4: De authentificatie van de opstelling {#set-up-authentication}

Afhankelijk van of u `"authenticationRule": "CUSTOMER_AUTHENTICATION"` of `"authenticationRule": "PLATFORM_AUTHENTICATION"` opgeeft in de bovenstaande doelconfiguratie, kunt u verificatie voor uw doel instellen met het `/destination` - of `/credentials` -eindpunt.

>[!NOTE]
>
>`CUSTOMER_AUTHENTICATION` is de gemeenschappelijkere van de twee authentificatieregels en is te gebruiken als u gebruikers om één of andere vorm van authentificatie aan uw bestemming alvorens zij opstelling een verbinding en uitvoergegevens vereist te verstrekken.

* Als u `"authenticationRule": "CUSTOMER_AUTHENTICATION"` in de bestemmingsconfiguratie selecteerde, zie de volgende secties voor de authentificatietypen die door Destination SDK voor op dossier-gebaseerde bestemmingen worden gesteund:

   * [Amazon S3-verificatie](../functionality/destination-configuration/customer-authentication.md#s3)
   * [Azure Blob](../functionality/destination-configuration/customer-authentication.md#blob)
   * [Azure Data Lake Storage](../functionality/destination-configuration/customer-authentication.md#adls)
   * [Google Cloud Storage](../functionality/destination-configuration/customer-authentication.md#gcs)
   * [SFTP-verificatie met SSH-sleutel](../functionality/destination-configuration/customer-authentication.md#sftp-ssh)
   * [SFTP-verificatie met wachtwoord](../functionality/destination-configuration/customer-authentication.md#sftp-password)

* Als u `"authenticationRule": "PLATFORM_AUTHENTICATION"` selecteerde, moet u de configuratie van de a [&#x200B; geloofsbrieven &#x200B;](../credentials-api/create-credential-configuration.md) tot stand brengen en identiteitskaart van het credentievoorwerp in de `authenticationId` parameter in de [&#x200B; configuratie van de bestemmingslevering &#x200B;](/help/destinations/destination-sdk/functionality/destination-configuration/destination-delivery.md#platform-authentication) overgaan.

## Stap 5: Test uw bestemming {#test-destination}

Na vestiging kunt uw bestemming die de configuratieeindpunten in de vorige stappen gebruiken, u het [&#x200B; bestemmings testende hulpmiddel &#x200B;](../testing-api/batch-destinations/file-based-destination-testing-overview.md) gebruiken om de integratie tussen Adobe Experience Platform en uw bestemming te testen.

Als onderdeel van het proces om uw bestemming te testen, moet u Experience Platform UI gebruiken om publiek tot stand te brengen, dat u aan uw bestemming zult activeren. Raadpleeg de twee onderstaande bronnen voor instructies voor het maken van soorten publiek in Experience Platform:

* [Een publiek maken - documentatiepagina](/help/segmentation/ui/audience-portal.md#create-audience)
* [&#x200B; creeer een publiek - videoanalyse &#x200B;](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=nl-NL)

## Stap 6: Uw doel publiceren {#publish-destination}

>[!NOTE]
>
>Deze stap wordt niet vereist als u een privé bestemming voor uw eigen gebruik creeert, en kijkt niet om het in de catalogus van bestemmingen voor andere te gebruiken klanten te publiceren.

Na het vormen van en het testen van uw bestemming, gebruik [&#x200B; bestemmings het publiceren API &#x200B;](../publishing-api/create-publishing-request.md) om uw configuratie voor overzicht naar Adobe voor te leggen.

## Stap 7: Documenteer uw bestemming {#document-destination}

>[!NOTE]
>
>Deze stap wordt niet vereist als u een privé bestemming voor uw eigen gebruik creeert, en kijkt niet om het in de catalogus van bestemmingen voor andere te gebruiken klanten te publiceren.

Als u een Onafhankelijke Verkoper van de Software (ISV) of Integrator van het Systeem (SI) creërend a [&#x200B; geproduceerde integratie &#x200B;](../overview.md#productized-custom-integrations) bent, gebruik het [&#x200B; zelfbedienings documentatieproces &#x200B;](../docs-framework/documentation-instructions.md) om een pagina van de productdocumentatie voor uw bestemming in de [&#x200B; de bestemmingscatalogus van Experience Platform &#x200B;](/help/destinations/catalog/overview.md) tot stand te brengen.

## Stap 8: Doel verzenden voor Adobe-revisie {#submit-for-review}

>[!NOTE]
>
>Deze stap wordt niet vereist als u een privé bestemming voor uw eigen gebruik creeert, en kijkt niet om het in de catalogus van bestemmingen voor andere te gebruiken klanten te publiceren.

Tot slot alvorens de bestemming in de catalogus van Experience Platform kan worden gepubliceerd en aan alle klanten van Experience Platform zichtbaar, moet u de bestemming officieel voorleggen voor de controle van Adobe. Vind volledige informatie over hoe te [&#x200B; voor overzicht voorleggen een geproduceerde die bestemming in Destination SDK &#x200B;](../guides/submit-destination.md) wordt authored.
