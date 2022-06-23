---
description: Deze pagina maakt een lijst en beschrijft de stappen om een op dossier-gebaseerde bestemming te vormen gebruikend Destination SDK.
title: (Bèta) Gebruik Destination SDK om een op dossier-gebaseerde bestemming te vormen
exl-id: 84d73452-88e4-4e0f-8fc7-d0d8e10f9ff5
source-git-commit: 77c80c391ef6677f95af81ef15272380687e6789
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# (Bèta) Gebruik Destination SDK om een op dossier-gebaseerde bestemming te vormen

## Overzicht {#overview}

>[!IMPORTANT]
>
>De functionaliteit om op dossier-gebaseerde bestemmingen te vormen en voor te leggen gebruikend Adobe Experience Platform Destination SDK is momenteel in Bèta. De documentatie en functionaliteit kunnen worden gewijzigd.

In deze pagina wordt beschreven hoe u de informatie in [Configuratieopties in de SDK Doelen](./configuration-options.md) en in andere Destination SDK-functionaliteit en API-referentiedocumenten om een [bestandsgebaseerd doel](../../destinations/destination-types.md#file-based). De stappen worden in de onderstaande volgorde weergegeven.

## Vereisten {#prerequisites}

Lees de onderstaande stappen voordat u verdergaat [Aan de slag met Destination SDK](./getting-started.md) pagina voor informatie over het verkrijgen van de vereiste autorisatiegeloofsbrieven van de Adobe I/O en andere eerste vereisten om met Destination SDK APIs te werken.

## Stappen om de configuratieopties in Destination SDK aan opstelling te gebruiken uw bestemming {#steps}

![Gedetailleerde stappen voor het gebruik van Destination SDK-eindpunten](./assets/destination-sdk-steps-batch.png)

## Stap 1: Een server- en bestandsconfiguratie maken {#create-server-file-configuration}

Begin door een server en dossierconfiguratie te creëren gebruikend `/destinations-server` eindpunt (read [API-referentie](./destination-server-api.md)).

Hieronder ziet u een voorbeeldconfiguratie voor een [!DNL Amazon S3] bestemming. Andere soorten op dossier-gebaseerde bestemmingen vormen, zie hun overeenkomstige [serverconfiguraties](server-and-file-configuration.md).

**API-indeling**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

```json
{
    "name": "S3 destination",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucket": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.bucket}}"
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
            },
            "lineSep": {
                "templatingStrategy": "NONE",
                "value": "\n"
            }
        }
    }
}
```

## Stap 2: Doelconfiguratie maken {#create-destination-configuration}

Hieronder getoond is een voorbeeld van een bestemmingsconfiguratie, die door te gebruiken wordt gecreeerd `/destinations` API-eindpunt. Voor meer informatie over deze configuratie, verwijs naar [Doelconfiguratie](./file-based-destination-configuration.md).

Om de server en dossierconfiguratie in stap 1 met deze bestemmingsconfiguratie te verbinden, voeg instantieidentiteitskaart van de server en malplaatjeconfiguratie als toe `destinationServerId` hier.

**API-indeling**

```http
POST platform.adobe.io/data/core/activation/authoring/destinations
```

```json
{
    "name": "Amazon S3 destination",
    "description": "Amazon S3 destination is a fictional destination, used for this example.",
    "releaseNotes": "Test",
    "status": "Test",
    "customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
    "customerEncryptionConfigurations": [],
    "customerDataFields": [
        {
            "name": "bucket",
            "title": "Amazon S3 bucket name",
            "description": "Enter the Amazon S3 Bucket name that will host the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "path",
            "title": "Amazon S3 path",
            "description": "Enter Amazon S3 folder path",
            "type": "string",
            "isRequired": true,
            "pattern": "^[A-Za-z]+$",
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
        "defaultStartTime": "00:00"
    },
    "backfillHistoricalProfileData": true
}
```

## Stap 3: Configuratie van metagegevens voor het publiek maken {#create-audience-metadata-configuration}

Voor sommige bestemmingen, vereist Destination SDK dat u een configuratie van publieksmeta-gegevens vormt om publiek in uw bestemming programmatically tot stand te brengen bij te werken of te schrappen. Zie [Metagegevensbeheer voor het publiek](./audience-metadata-management.md) voor informatie over wanneer u aan opstelling deze configuratie en hoe te om het moet doen.

Als u een configuratie van publieksmeta-gegevens gebruikt, moet u het met de bestemmingsconfiguratie verbinden u in stap 2 creeerde. Voeg instanceID van uw configuratie van publieksmeta-gegevens aan uw bestemmingsconfiguratie als toe `audienceTemplateId`.

## Stap 4: Verificatie instellen {#set-up-authentication}

Afhankelijk van of u `"authenticationRule": "CUSTOMER_AUTHENTICATION"` of `"authenticationRule": "PLATFORM_AUTHENTICATION"` in de bestemmingsconfiguratie hierboven, kunt u opstellingsauthentificatie voor uw bestemming door te gebruiken `/destination` of de `/credentials` eindpunt.

* Als u `"authenticationRule": "CUSTOMER_AUTHENTICATION"` in de bestemmingsconfiguratie, zie de volgende secties voor de authentificatietypen die door Destination SDK voor op dossier-gebaseerde bestemmingen worden gesteund:

   * [Amazon S3-verificatie](authentication-configuration.md#s3)
   * [Azure Blob](authentication-configuration.md#blob)
   * [Azure Data Lake Storage](authentication-configuration.md#adls)
   * [Google Cloud Storage](authentication-configuration.md#gcs)
   * [SFTP-verificatie met SSH-sleutel](authentication-configuration.md#sftp-ssh)
   * [SFTP-verificatie met wachtwoord](authentication-configuration.md#sftp-password)

* Als u `"authenticationRule": "PLATFORM_AUTHENTICATION"`, verwijst u naar de [Verificatieconfiguratie](./authentication-configuration.md#when-to-use).


<!-- ## Step 5: Test your destination {#test-destination}

After setting up your destination using the configuration endpoints in the previous steps, you can use the [destination testing tool](./create-template.md) to test the integration between Adobe Experience Platform and your destination.

As part of the process to test your destination, you must use the Experience Platform UI to create segments, which you will activate to your destination. Refer to the two resources below for instructions how to create segments in Experience Platform:

* [Create a segment documentation page](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=en#create-segment)
* [Create a segment video walkthrough](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) -->

## Stap 5: Uw doel publiceren {#publish-destination}

Na het vormen van en het testen van uw bestemming, gebruik [doel-publicatie-API](./destination-publish-api.md) om uw configuratie ter controle naar Adobe te verzenden.

## Stap 6: Uw doel documenteren {#document-destination}

Als u een Onafhankelijke Verkoper van de Software (ISV) of Integrator van het Systeem (SI) creeert [productievere integratie](./overview.md#productized-custom-integrations), gebruikt u de [zelfbedieningsdocumentatie](./docs-framework/documentation-instructions.md) om een pagina van de productdocumentatie voor uw bestemming in te stellen in [Catalogus Experience Platform doelen](/help/destinations/catalog/overview.md).
