---
description: Deze pagina maakt een lijst en beschrijft de stappen om een op dossier-gebaseerde bestemming te vormen gebruikend Destination SDK.
title: Gebruik Destination SDK om een op een bestand gebaseerde bestemming te configureren
exl-id: 84d73452-88e4-4e0f-8fc7-d0d8e10f9ff5
source-git-commit: 45ba0db386f065206f89ed30bfe7b0c1b44f6173
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 0%

---

# Gebruik Destination SDK om een op een bestand gebaseerde bestemming te configureren

## Overzicht {#overview}

In deze pagina wordt beschreven hoe u de informatie in [Configuratieopties in de SDK Doelen](../functionality/configuration-options.md) en in andere Destination SDK-functionaliteit en API-referentiedocumenten om een [bestandsgebaseerd doel](../../destination-types.md#file-based). De stappen worden in de onderstaande volgorde weergegeven.

## Vereisten {#prerequisites}

Lees de onderstaande stappen voordat u verdergaat [Aan de slag met Destination SDK](../getting-started.md) pagina voor informatie over het verkrijgen van de vereiste autorisatiegeloofsbrieven van de Adobe I/O en andere eerste vereisten om met Destination SDK APIs te werken.

## Stappen om de configuratieopties in Destination SDK aan opstelling te gebruiken uw bestemming {#steps}

![Gedetailleerde stappen voor het gebruik van Destination SDK-eindpunten](../assets/guides/destination-sdk-steps-batch.png)

## Stap 1: Een server- en bestandsconfiguratie maken {#create-server-file-configuration}

Beginnen met [een server- en bestandsconfiguratie maken](../authoring-api/destination-server/create-destination-server.md) met de `/destinations-server` eindpunt.

Hieronder ziet u een voorbeeldconfiguratie voor een [!DNL Amazon S3] bestemming. Voor meer details over de gebieden die in de configuratie worden gebruikt en om andere soorten op dossier-gebaseerde bestemmingen te vormen, zie hun overeenkomstige [serverconfiguraties](../functionality/destination-server/server-specs.md).

**API-indeling**

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

Hieronder getoond is een voorbeeld van een bestemmingsconfiguratie, die door te gebruiken wordt gecreeerd `/destinations` API-eindpunt.

Om de server en dossierconfiguratie van stap 1 aan deze bestemmingsconfiguratie te verbinden, voeg toe `instance ID` van de server en bestandsconfiguratie als `destinationServerId` hier.

**API-indeling**

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

Voor sommige bestemmingen, vereist Destination SDK dat u een configuratie van publieksmeta-gegevens vormt om publiek in uw bestemming programmatically tot stand te brengen bij te werken of te schrappen. Zie [Metagegevensbeheer voor het publiek](../functionality/audience-metadata-management.md) voor informatie over wanneer u aan opstelling deze configuratie en hoe te om het moet doen.

Als u een configuratie van publieksmeta-gegevens gebruikt, moet u het met de bestemmingsconfiguratie verbinden u in stap 2 creeerde. Voeg instanceID van uw configuratie van publieksmeta-gegevens aan uw bestemmingsconfiguratie als toe `audienceTemplateId`.

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
    "audienceMetadataConfig":{
    "mapExperiencePlatformSegmentName":false,
    "mapExperiencePlatformSegmentId":false,
    "mapUserInput":false,
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

Afhankelijk van of u opgeeft `"authenticationRule": "CUSTOMER_AUTHENTICATION"` of `"authenticationRule": "PLATFORM_AUTHENTICATION"` in de bestemmingsconfiguratie hierboven, kunt u opstellingsauthentificatie voor uw bestemming door `/destination` of de `/credentials` eindpunt.

>[!NOTE]
>
>`CUSTOMER_AUTHENTICATION` is gemeenschappelijker van de twee authentificatieregels en is te gebruiken als u gebruikers vereist om één of andere vorm van authentificatie aan uw bestemming te verstrekken alvorens zij opstelling een verbinding kunnen en gegevens uitvoeren.

* Als u `"authenticationRule": "CUSTOMER_AUTHENTICATION"` in de bestemmingsconfiguratie, zie de volgende secties voor de authentificatietypen die door Destination SDK voor op dossier-gebaseerde bestemmingen worden gesteund:

   * [Amazon S3-verificatie](../functionality/destination-configuration/customer-authentication.md#s3)
   * [Azure Blob](../functionality/destination-configuration/customer-authentication.md#blob)
   * [Azure Data Lake Storage](../functionality/destination-configuration/customer-authentication.md#adls)
   * [Google Cloud Storage](../functionality/destination-configuration/customer-authentication.md#gcs)
   * [SFTP-verificatie met SSH-sleutel](../functionality/destination-configuration/customer-authentication.md#sftp-ssh)
   * [SFTP-verificatie met wachtwoord](../functionality/destination-configuration/customer-authentication.md#sftp-password)

* Als u `"authenticationRule": "PLATFORM_AUTHENTICATION"`, verwijst u naar de [documentatie van API voor credentiële configuratie](../credentials-api/create-credential-configuration.md#when-to-use).


## Stap 5: Test uw bestemming {#test-destination}

Nadat u de bestemming hebt ingesteld met de eindpunten van de configuratie in de vorige stappen, kunt u de opdracht [doeltestgereedschap](../testing-api/batch-destinations/file-based-destination-testing-overview.md) om de integratie tussen Adobe Experience Platform en uw bestemming te testen.

Als deel van het proces om uw bestemming te testen, moet u het Experience Platform UI gebruiken om publiek tot stand te brengen, dat u aan uw bestemming zult activeren. Raadpleeg de twee onderstaande bronnen voor instructies voor het maken van publiek in Experience Platform:

* [Een publiek maken - documentatiepagina](/help/segmentation/ui/overview.md#create-segment)
* [Een publiek maken - videodoorloop](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)

## Stap 6: Uw doel publiceren {#publish-destination}

>[!NOTE]
>
>Deze stap wordt niet vereist als u een privé bestemming voor uw eigen gebruik creeert, en kijkt niet om het in de catalogus van bestemmingen voor andere te gebruiken klanten te publiceren.

Na het vormen van en het testen van uw bestemming, gebruik [doel-publicatie-API](../publishing-api/create-publishing-request.md) om uw configuratie ter controle naar de Adobe te verzenden.

## Stap 7: Documenteer uw bestemming {#document-destination}

>[!NOTE]
>
>Deze stap wordt niet vereist als u een privé bestemming voor uw eigen gebruik creeert, en kijkt niet om het in de catalogus van bestemmingen voor andere te gebruiken klanten te publiceren.

Als u een Onafhankelijke Verkoper van de Software (ISV) of Integrator van het Systeem (SI) creeert [productievere integratie](../overview.md#productized-custom-integrations), gebruikt u de [zelfbedieningsdocumentatie](../docs-framework/documentation-instructions.md) om een pagina van de productdocumentatie voor uw bestemming in te stellen in [Catalogus Experience Platform-doelen](/help/destinations/catalog/overview.md).

## Stap 8: Plaats verzenden voor revisie door Adobe {#submit-for-review}

>[!NOTE]
>
>Deze stap wordt niet vereist als u een privé bestemming voor uw eigen gebruik creeert, en kijkt niet om het in de catalogus van bestemmingen voor andere te gebruiken klanten te publiceren.

Tot slot vóór de bestemming in de catalogus van het Experience Platform kan worden gepubliceerd en aan alle klanten van het Experience Platform zichtbaar, moet u de bestemming officieel voorleggen voor overzicht van de Adobe. Volledige informatie over hoe te vinden [een in Destination SDK gefabriceerde bestemming ter controle indienen](../guides/submit-destination.md).
