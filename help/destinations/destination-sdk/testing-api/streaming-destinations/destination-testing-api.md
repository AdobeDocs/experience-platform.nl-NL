---
description: Leer hoe te om bestemmings het testen API te gebruiken om te testen als uw het stromen bestemming correct wordt gevormd en de integriteit van gegevensstromen aan uw gevormde bestemming te verifiëren.
title: Streaming doel testen met voorbeeldprofielen
exl-id: 2b54250d-ec30-4ad7-a8be-b86b14e4f074
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---


# Streaming doel testen met voorbeeldprofielen {#template-api-operations}

>[!IMPORTANT]
>
>**API eindpunt**: `https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/`

Deze pagina maakt een lijst en beschrijft van alle API verrichtingen die u het gebruiken van het `/authoring/testing/destinationInstance/` API eindpunt kunt uitvoeren, om te testen of uw bestemming correct wordt gevormd en om de integriteit van gegevensstromen aan uw gevormde bestemming te verifiëren. Voor een beschrijving van de functionaliteit die door dit eindpunt wordt gesteund, lees [ test uw bestemmingsconfiguratie ](streaming-destination-testing-overview.md).

U doet verzoeken aan het het testen eindpunt met of zonder profielen aan de vraag toe te voegen. Als u geen profielen verzendt op de aanvraag, genereert Adobe deze intern voor u en voegt ze toe aan de aanvraag.

U kunt de [ generatie API van de profielgeneratie van de Steekproef gebruiken ](sample-profile-generation-api.md) om profielen tot stand te brengen in verzoeken aan de bestemmings het testen API te gebruiken.

## Hoe te om bestemmingsID te krijgen {#get-destination-instance-id}

>[!IMPORTANT]
>
>* Als u deze API wilt gebruiken, moet u een bestaande verbinding met uw doel hebben in de gebruikersinterface van Experience Platform. Lees [ verbind met bestemming ](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) en [ activeer profielen en publiek aan een bestemming ](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html) voor meer informatie.
>* Na het vestigen van de verbinding aan uw bestemming, krijg identiteitskaart van de bestemmingsinstantie die u in API vraag aan dit eindpunt zou moeten gebruiken wanneer [ doorbladert een verbinding met uw bestemming ](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html).
>  >![UI beeld hoe te om identiteitskaart van de bestemmingsinstantie te krijgen ](../../assets/testing-api/get-destination-instance-id.png)

## Aan de slag met API-bewerkingen voor doeltesten {#get-started}

Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](../../getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings authoring en vereiste kopballen te verkrijgen.

## Test uw bestemmingsconfiguratie zonder profielen aan de vraag toe te voegen {#test-without-adding-profiles}

U kunt uw bestemmingsconfiguratie testen door een POST- verzoek aan het `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` eindpunt te doen en bestemmingsidentiteitskaart van de bestemmingsinstantie van de bestemming te verstrekken die u test.

**API formaat**


```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| Query-parameter | Beschrijving |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | De doel-instantie-id van het doel dat u test. |

**Verzoek**

Het volgende verzoek roept het REST API eindpunt van uw bestemming. Het verzoek wordt gevormd door de `{DESTINATION_INSTANCE_ID}` vraagparameter.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Reactie**

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
| `aggregationKey` | Omvat informatie over het samenvoegingsbeleid dat voor de bestemming wordt gevormd. Voor meer informatie, lees de [ documentatie van het beleid van de Samenvoeging 0} {.](../../functionality/destination-configuration/aggregation-policy.md) |
| `traceId` | Een unieke id voor de bewerking. Als er fouten optreden, kunt u deze id delen met het Adobe-team voor probleemoplossing. |
| `results.httpCalls.request` | Bevat de aanvraag die door Adobe naar uw bestemming is verzonden. |
| `results.httpCalls.response` | Bevat het antwoord dat Adobe van je bestemming heeft ontvangen. |
| `inputProfiles` | Omvat de profielen die op de vraag aan uw bestemming werden uitgevoerd. De profielen komen overeen met het bronschema. |

{style="table-layout:auto"}

## Test uw bestemmingsconfiguratie met profielen die aan de vraag worden toegevoegd {#test-with-added-profiles}

U kunt uw bestemmingsconfiguratie testen door een POST- verzoek aan het `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` eindpunt te doen en bestemmingsidentiteitskaart van de bestemmingsinstantie van de bestemming te verstrekken die u test.

**API formaat**

```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| Query-parameter | Beschrijving |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | De doel-instantie-id van het doel dat u test. |

**Verzoek**

Het volgende verzoek roept het REST API eindpunt van uw bestemming. Het verzoek wordt gevormd door de parameters die in de nuttige lading en de `{DESTINATION_INSTANCE_ID}` vraagparameter worden verstrekt.

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

**Reactie**

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

Destination SDK API-eindpunten volgen de algemene beginselen van Experience Platform API-foutberichten. Verwijs naar [ API statuscodes ](../../../../landing/troubleshooting.md#api-status-codes) en [ de fouten van de verzoekkopbal ](../../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van het Platform.

## Volgende stappen

Nadat u dit document hebt gelezen, weet u nu hoe u de bestemming kunt testen. U kunt Adobe [ zelfbediening documentatieproces ](../../docs-framework/documentation-instructions.md) nu gebruiken om een documentatiepagina voor uw bestemming tot stand te brengen.
