---
description: Leer hoe u de API voor bestemmingstests kunt gebruiken om uw streamingdoelconfiguratie te testen voordat u deze publiceert.
title: Overzicht van de API voor streaming-bestemming
exl-id: 21e4d647-1168-4cb4-a2f8-22d201e39bba
source-git-commit: 0befd65b91e49cacab67c76fd9ed5d77bf790b9d
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---


# Overzicht van de API voor streaming-bestemming

Als deel van Destination SDK, verstrekt Adobe ontwikkelaarshulpmiddelen om u bij het vormen van en het testen van uw bestemming te helpen. Deze pagina beschrijft hoe te om uw bestemmingsconfiguratie te testen. Voor informatie over hoe u een sjabloon voor berichttransformatie kunt maken, leest u [Een sjabloon voor berichttransformatie maken en testen](../../testing-api/streaming-destinations/create-template.md).

Naar **test als uw bestemming correct wordt gevormd en om de integriteit van gegevensstromen aan uw gevormde bestemming te verifiëren**, gebruikt u de *Gereedschap Doel testen*. Met dit hulpmiddel, kunt u uw bestemmingsconfiguratie testen door berichten naar uw REST API eindpunt te verzenden.

Hieronder wordt geïllustreerd hoe het testen van uw bestemming past in de [doelconfiguratieworkflow](../../guides/configure-destination-instructions.md) in Destination SDK:

![Grafiek van waar de bestemmings testende stap in het werkschema van de bestemmingsconfiguratie past](../../assets/testing-api/test-destination-step.png)

## Gereedschap voor het testen van de bestemming - Doel en voorwaarden {#destination-testing-tool}

Gebruik het bestemmings testende hulpmiddel om uw bestemmingsconfiguratie te testen door berichten naar het partnereindpunt te verzenden u in [serverconfiguratie](../../authoring-api/destination-server/create-destination-server.md).

Controleer voordat u het gereedschap gebruikt of:
* Vorm uw bestemming door de stappen te volgen die in worden geschetst [doelconfiguratieworkflow](../../authoring-api/destination-configuration/create-destination-configuration.md) en
* Stel een verbinding met uw bestemming in, zoals in [Hoe te om bestemmingsID te krijgen](../../testing-api/streaming-destinations/destination-testing-api.md#get-destination-instance-id).

Met dit hulpmiddel, na het vormen van uw bestemming, kunt u:
* Test of uw bestemming correct wordt gevormd;
* Verifieer de integriteit van gegevensstromen aan uw gevormde bestemming.

### Hoe wordt het gebruikt {#how-to-use}

>[!NOTE]
>
>Voor volledige API-naslagdocumentatie leest u [API-bewerkingen voor doeltesten](../../testing-api/streaming-destinations/destination-testing-api.md).

U kunt vraag aan het bestemmings het testen API eindpunt met of zonder profielen op het verzoek toe te voegen.

Als u geen profielen aan de aanvraag toevoegt, genereert Adobe deze intern voor u en voegt u ze toe aan de aanvraag. Als u profielen wilt genereren voor gebruik in deze aanvraag, raadpleegt u de [Voorbeeld van API-naslaggids voor genereren van profielen](../../testing-api/streaming-destinations/sample-profile-generation-api.md). U moet profielen produceren die op het bronXDM schema worden gebaseerd, zoals aangetoond in [API-referentie](../../testing-api/streaming-destinations/sample-profile-generation-api.md#generate-sample-profiles-source-schema). Het bronschema is het [samenvoegingsschema](../../../../profile/ui/union-schema.md) van de sandbox die u gebruikt.

De reactie bevat het resultaat van de verwerking van het bestemmingsverzoek. Het verzoek omvat drie belangrijke onderdelen:
* Het verzoek dat door Adobe voor de bestemming wordt geproduceerd.
* De reactie die van uw bestemming wordt ontvangen.
* De lijst met profielen die in de aanvraag zijn verzonden, of de profielen [toegevoegd door u in het verzoek](../../testing-api/streaming-destinations/destination-testing-api.md#test-with-added-profiles), of gegenereerd door Adobe als [de hoofdtekst van de aanvraag voor het testen van de bestemming leeg was](../../testing-api/streaming-destinations/destination-testing-api.md#test-without-adding-profiles).

>[!NOTE]
>
>Adobe kan veelvoudige verzoek en reactieparen produceren. Als u bijvoorbeeld 10 profielen verzendt naar een doel met een `maxUsersPerRequest` waarde 7, er is één aanvraag met 7 profielen en een andere aanvraag met 3 profielen.

**Voorbeeldverzoek met profielparameter in de hoofdtekst**

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
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
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
               }
            ]
         },
         "attributes":{
            "key":{
               "value":"string"
            }
         }
      }
   ]
}'
```

**Voorbeeldverzoek zonder profielparameter in de hoofdtekst**


```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw ''
```

**Monsterreactie**

De inhoud van de `results.httpCalls` is specifiek voor uw REST API.

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
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
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

Voor beschrijvingen van de verzoek- en responsparameters raadpleegt u [API-bewerkingen voor doeltesten](../../testing-api/streaming-destinations/destination-testing-api.md).

## Volgende stappen

Na het testen van uw bestemming en het bevestigen dat het correct wordt gevormd, gebruik [doel-publicatie-API](../../publishing-api/create-publishing-request.md) om uw configuratie ter controle naar Adobe te verzenden.
