---
description: Deze pagina maakt een lijst en beschrijft van alle API verrichtingen die u kunt uitvoeren gebruikend `/authoring/testing/destinationInstance/ ` API eindpunt, om te testen of uw bestemming correct wordt gevormd en om de integriteit van gegevensstromen aan uw gevormde bestemming te verifiëren.
title: API-bewerkingen voor doeltesten
exl-id: 2b54250d-ec30-4ad7-a8be-b86b14e4f074
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# API-bewerkingen voor doeltesten {#template-api-operations}

>[!IMPORTANT]
>
>**API-eindpunt**: `https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/`

Deze pagina bevat een overzicht en beschrijving van alle API-bewerkingen die u kunt uitvoeren met de `/authoring/testing/destinationInstance/` API eindpunt, om te testen als uw bestemming correct wordt gevormd en om de integriteit van gegevensstromen aan uw gevormde bestemming te verifiëren. Voor een beschrijving van de functionaliteit die door dit eindpunt wordt gesteund, lees [De doelconfiguratie testen](./test-destination.md).

U doet verzoeken aan het het testen eindpunt met of zonder profielen aan de vraag toe te voegen. Als u geen profielen op het verzoek verzendt, zal Adobe die intern voor u produceren en hen toevoegen aan het verzoek.

U kunt de [Voorbeeld van genereren van profiel-API](./sample-profile-generation-api.md) om profielen te maken die moeten worden gebruikt in aanvragen voor de API voor het testen van doelen.

## Hoe te om bestemmingsID te krijgen {#get-destination-instance-id}

>[!IMPORTANT]
>
>* Als u deze API wilt gebruiken, moet u een bestaande verbinding met uw doel hebben in de interface van het Experience Platform. Lezen [verbinding maken met doel](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) en [profielen en segmenten activeren naar een doel](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en) voor meer informatie . Na het vestigen van de verbinding aan uw bestemming, krijg identiteitskaart van de bestemmingsinstantie die u in API vraag aan dit eindpunt van URL zou moeten gebruiken wanneer [bladeren door een verbinding met uw bestemming](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html?lang=en).
   >![UI-afbeelding voor het ophalen van bestemmings-ID](./assets/get-destination-instance-id.png)


## Aan de slag met API-bewerkingen voor doeltesten {#get-started}

Controleer voordat je doorgaat de [gids Aan de slag](./getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings creatie en vereiste kopballen te verkrijgen.

## Test uw bestemmingsconfiguratie zonder profielen aan de vraag toe te voegen {#test-without-adding-profiles}

U kunt uw bestemmingsconfiguratie testen door een verzoek van de POST aan `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` eindpunt en verstrekkend bestemmingsidentiteitskaart van de bestemmingsinstantie van de bestemming die u test.

**API-indeling**


```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| Query-parameter | Beschrijving |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | De doel-instantie-id van het doel dat u test. |

**Verzoek**

Het volgende verzoek roept het REST API eindpunt van uw bestemming. Het verzoek wordt gevormd door `{DESTINATION_INSTANCE_ID}` queryparameter.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP samen met de API reactie van het REST API eindpunt van uw bestemming terug.

```json
{
   "results":[
      {
         "aggregationKey":{
            "destinationInstanceId":"string",
            "segmentId":"string",
            "segmentStatus":"realized",
            "identityNamespaces":[
               [
                  "email",
                  "phone"
               ]
            ]
         },
         "httpCalls":[
            {
               "traceId":"a06fec2d-a886-4219-8975-4e4b7ed26539",
               "request":{
                  "body":"{ \"attributes\": [  { \"external_id\": \"external_id-h29Fq\"  , \"AdobeExperiencePlatformSegments\": { \"add\": [  \"Nirvana fans\" ,  \"RHCP fans\"   ], \"remove\": [  ] }  ,  \"key\":  \"string\"    }  ] }",
                  "headers":[
                     {
                        "Content-Type":"application/json"
                     }
                  ],
                  "method":"POST",
                  "uri":"https://api.moviestar.com/users/track"
               },
               "response":{
                  "body":"{\"status\": \"success\"}",
                  "code":"200",
                  "headers":[
                     {
                        "Connection":"keep-alive"
                     },
                     {
                        "Content-Type":"application/json"
                     },
                     {
                        "Server":"nginx"
                     },
                     {
                        "Vary":"Origin,Accept-Encoding"
                     },
                     {
                        "transfer-encoding":"chunked"
                     }
                  ]
               }
            }
         ]
      }
   ],
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "03fb9938-8537-4b4c-87f9-9c4d413a0ee5":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872039Z",
                  "status":"realized"
               },
               "27e05542-d6a3-46c7-9c8e-d59d50229530":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872042Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"john.smith@abc.com"
         },
         "identityMap":{
            "ECID":[
               {
                  "id":"ECID-vlnt6"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"string"
            }
         }
      }
   ]
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `aggregationKey` | Omvat informatie over het samenvoegingsbeleid dat voor de bestemming wordt gevormd. Lees voor meer informatie de [Samenvoegingsbeleid](./destination-configuration.md#aggregation) in het doelconfiguratiedocument. |
| `traceId` | Een unieke id voor de bewerking. Wanneer het ontmoeten van fouten, kunt u deze identiteitskaart met het team van Adobe voor het oplossen van problemendoeleinden delen. |
| `results.httpCalls.request` | Omvat het verzoek dat door Adobe naar uw bestemming werd verzonden. |
| `results.httpCalls.response` | Omvat de reactie die door Adobe van uw bestemming wordt ontvangen. |
| `inputProfiles` | Omvat de profielen die op de vraag aan uw bestemming werden uitgevoerd. De profielen komen overeen met het bronschema. |

{style=&quot;table-layout:auto&quot;}

## Test uw bestemmingsconfiguratie met profielen die aan de vraag worden toegevoegd {#test-with-added-profiles}

U kunt uw bestemmingsconfiguratie testen door een verzoek van de POST aan `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` eindpunt en verstrekkend bestemmingsidentiteitskaart van de bestemmingsinstantie van de bestemming die u test.

**API-indeling**

```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| Query-parameter | Beschrijving |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | De doel-instantie-id van het doel dat u test. |

**Verzoek**

Het volgende verzoek roept het REST API eindpunt van uw bestemming. Het verzoek wordt gevormd door de parameters die in de lading en worden verstrekt `{DESTINATION_INSTANCE_ID}` queryparameter.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '{
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "374a9a6c-c719-4cdb-a660-155a2838e6d6":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248585Z",
                  "status":"realized"
               },
               "896f8776-9498-47b4-b994-51cb3f61c2c5":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248605Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "ECID":[
               {
                  "id":"ECID-Z3i2t"
               }
            ],
            "external_id":[
               {
                  "id":"external_id-h29Fq"
               }
            ]
         },
         "attributes":{
            "firstName":{
               "value":"John"
            }
         }
      }
   ]
}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP samen met de API reactie van het REST API eindpunt van uw bestemming terug.

```json
{
   "results":[
      {
         "aggregationKey":{
            "destinationInstanceId":"string",
            "segmentId":"string",
            "segmentStatus":"realized",
            "identityNamespaces":[
               [
                  "email",
                  "phone"
               ]
            ]
         },
         "httpCalls":[
            {
               "traceId":"a06fec2d-a886-4219-8975-4e4b7ed26539",
               "request":{
                  "body":"{ \"attributes\": [  { \"external_id\": \"external_id-h29Fq\"  , \"AdobeExperiencePlatformSegments\": { \"add\": [  \"Nirvana fans\" ,  \"RHCP fans\"   ], \"remove\": [  ] }  ,  \"key\":  \"string\"    }  ] }",
                  "headers":[
                     {
                        "Content-Type":"application/json"
                     }
                  ],
                  "method":"POST",
                  "uri":"https://api.moviestar.com/users/track"
               },
               "response":{
                  "body":"{\"status\": \"success\"}",
                  "code":"200",
                  "headers":[
                     {
                        "Connection":"keep-alive"
                     },
                     {
                        "Content-Type":"application/json"
                     },
                     {
                        "Server":"nginx"
                     },
                     {
                        "Vary":"Origin,Accept-Encoding"
                     },
                     {
                        "transfer-encoding":"chunked"
                     }
                  ]
               }
            }
         ]
      }
   ],
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "374a9a6c-c719-4cdb-a660-155a2838e6d6":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248585Z",
                  "status":"realized"
               },
               "896f8776-9498-47b4-b994-51cb3f61c2c5":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248605Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "ECID":[
               {
                  "id":"ECID-Z3i2t"
               }
            ],
            "external_id":[
               {
                  "id":"external_id-h29Fq"
               }
            ]
         },
         "attributes":{
            "firstName":{
               "value":"John"
            }
         }
      }
   ]
}
```

## API-foutafhandeling {#api-error-handling}

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Zie [API-statuscodes](../../landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](../../landing/troubleshooting.md#request-header-errors) in de gids voor het oplossen van problemen met Platforms.

## Volgende stappen

Nadat u dit document hebt gelezen, weet u nu hoe u de bestemming kunt testen. U kunt nu de Adobe gebruiken [zelfbedieningsdocumentatie](./docs-framework/documentation-instructions.md) om een documentatiepagina voor uw bestemming te maken.
