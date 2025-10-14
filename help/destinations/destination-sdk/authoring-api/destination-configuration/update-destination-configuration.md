---
description: Deze pagina illustreert de API vraag die wordt gebruikt om een bestaande bestemmingsconfiguratie door Adobe Experience Platform Destination SDK bij te werken.
title: Een doelconfiguratie bijwerken
exl-id: d7f18689-9806-4f73-a63a-fa112569819c
source-git-commit: 163c6f6bacfd6f0928b1053bd146a2d4fc4c74d0
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# Een doelconfiguratie bijwerken

Deze pagina illustreert de API-aanvraag en lading die u kunt gebruiken om een bestaande doelconfiguratie bij te werken met behulp van het API-eindpunt `/authoring/destinations` .

>[!TIP]
>
>Om het even welke updateverrichting op geproduceerde/openbare bestemmingen is zichtbaar slechts nadat u [&#x200B; het publiceren API &#x200B;](../../publishing-api/create-publishing-request.md) gebruikt en de update voor het overzicht van Adobe voorleggen.

Lees de volgende artikelen voor een gedetailleerde beschrijving van de mogelijkheden van een doelconfiguratie:

* [Configuratie van klantverificatie](../../functionality/destination-configuration/customer-authentication.md)
* [OAuth2-vergunning](../../functionality/destination-configuration/oauth2-authorization.md)
* [Gegevensvelden van de klant](../../functionality/destination-configuration/customer-data-fields.md)
* [UI-kenmerken](../../functionality/destination-configuration/ui-attributes.md)
* [Schema-configuratie](../../functionality/destination-configuration/schema-configuration.md)
* [Configuratie naamruimte voor identiteit](../../functionality/destination-configuration/identity-namespace-configuration.md)
* [Levering bestemming](../../functionality/destination-configuration/destination-delivery.md)
* [Configuratie van metagegevens voor publiek](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [Configuratie van metagegevens voor publiek](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [Samenvoegingsbeleid](../../functionality/destination-configuration/aggregation-policy.md)
* [Batchconfiguratie](../../functionality/destination-configuration/batch-configuration.md)
* [Historische profielkwalificaties](../../functionality/destination-configuration/historical-profile-qualifications.md)

>[!IMPORTANT]
>
>Alle parameternamen en waarden die door Destination SDK worden gesteund zijn **gevoelig geval**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Aan de slag met API-bewerkingen voor doelconfiguratie {#get-started}

Alvorens verder te gaan, te herzien gelieve [&#x200B; begonnen gids &#x200B;](../../getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings authoring en vereiste kopballen te verkrijgen.

## Een doelconfiguratie bijwerken {#update}

U kunt een [&#x200B; bestaande &#x200B;](create-destination-configuration.md) bestemmingsconfiguratie bijwerken door een `PUT` verzoek aan het `/authoring/destinations` eindpunt met de bijgewerkte nuttige lading te doen.

>[!TIP]
>
>API-eindpunt: `platform.adobe.io/data/core/activation/authoring/destinations`

Om een bestaande bestemmingsconfiguratie en zijn overeenkomstige `{INSTANCE_ID}` te verkrijgen, zie het artikel over [&#x200B; het terugwinnen van een bestemmingsconfiguratie &#x200B;](retrieve-destination-configuration.md).

**API formaat**

```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{INSTANCE_ID}` | De id van de doelconfiguratie die u wilt bijwerken. Om een bestaande bestemmingsconfiguratie en zijn overeenkomstige `{INSTANCE_ID}` te verkrijgen, zie [&#x200B; een bestemmingsconfiguratie &#x200B;](retrieve-destination-configuration.md) terugwinnen. |

+++verzoek

Het volgende verzoek werkt de bestemming bij wij in [&#x200B; dit voorbeeld &#x200B;](create-destination-configuration.md#create) met verschillende `filenameConfig` opties creeerden.

```shell {line-numbers="true" highlight="115-128"}
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/{INSTANCE_ID} \
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
         "name":"bucket",
         "title":"Enter the name of your Amazon S3 bucket",
         "description":"Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Enter the path to your S3 bucket folder",
         "description":"Enter the path to your S3 bucket folder",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
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
         "ONCE"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00",
      "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%_%DESTINATION_INSTANCE_ID%,"
      },
      "backfillHistoricalProfileData":true
   }
}'
```

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met de details van uw bijgewerkte bestemmingsconfiguratie terug.

+++

## API-foutafhandeling {#error-handling}

Destination SDK API-eindpunten volgen de algemene beginselen van Experience Platform API-foutberichten. Verwijs naar [&#x200B; API statuscodes &#x200B;](../../../../landing/troubleshooting.md#api-status-codes) en [&#x200B; de fouten van de verzoekkopbal &#x200B;](../../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van Experience Platform.

## Volgende stappen

Nadat u dit document hebt gelezen, weet u nu hoe u een doelconfiguratie kunt bijwerken via het API-eindpunt van Destination SDK `/authoring/destinations` .

Raadpleeg de volgende artikelen voor meer informatie over wat u met dit eindpunt kunt doen:

* [Een doelconfiguratie maken](create-destination-configuration.md)
* [Een doelconfiguratie ophalen](retrieve-destination-configuration.md)
* [Een doelconfiguratie verwijderen](delete-destination-configuration.md)
