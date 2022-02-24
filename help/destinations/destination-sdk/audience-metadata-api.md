---
description: Op deze pagina worden alle API-bewerkingen beschreven die u kunt uitvoeren met het API-eindpunt `/authoring/publiek-templates`.
title: API-bewerkingen voor het eindpunt van metagegevens van het publiek
exl-id: 3444da8c-b2be-4254-980a-8cce7560134d
source-git-commit: afdabdebe9b82d828cb1941edb99ca2518a941a2
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 2%

---

# API-bewerkingen voor het eindpunt van metagegevens van het publiek

>[!IMPORTANT]
>
>**API-eindpunt**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Deze pagina bevat een overzicht en beschrijving van alle API-bewerkingen die u kunt uitvoeren met de `/authoring/audience-templates` API-eindpunt. Voor een beschrijving van wanneer om dit eindpunt te gebruiken, lees [beheer van metagegevens van het publiek](./audience-metadata-management.md).

## Aan de slag met API-bewerkingen voor publiekssjablonen {#get-started}

Controleer voordat je doorgaat de [gids Aan de slag](./getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings creatie en vereiste kopballen te verkrijgen.

## Een nieuwe publiekssjabloon maken {#create}

U kunt een nieuw publiekssjabloon maken door een POST aan te vragen bij de `/authoring/audience-templates` eindpunt.

**API-indeling**

```http
POST /authoring/audience-templates
```

**Verzoek**

Het volgende verzoek leidt tot een nieuw malplaatje van publieksmeta-gegevens, dat door de parameters wordt gevormd die in de lading worden verstrekt. De hieronder vermelde lading omvat alle parameters die door `/authoring/audience-templates` eindpunt. Merk op dat u niet alle parameters op de vraag moet toevoegen en dat het malplaatje, volgens uw API vereisten aanpasbaar is.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "metadataTemplate":{
      "name":"string",
      "create":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "update":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "delete":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "validate":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "notify":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      }
   },
   "validations":[
      {
         "field":"string",
         "regex":"string"
      }
   ]
}'
```

| Eigenschap | Type | Beschrijving |
| -------- | ----------- | ----------- |
| `name` | Tekenreeks | De naam van het malplaatje van publieksmeta-gegevens voor uw bestemming. Deze naam zal in om het even welk partner-specifiek foutenmelding in het gebruikersinterface van het Experience Platform verschijnen, dat door het foutenbericht wordt gevolgd van wordt ontleed `metadataTemplate.create.errorSchemaMap`. |
| `url` | Tekenreeks | De URL en het eindpunt van uw API, die voor het creëren van, het bijwerken van, het schrappen van, of het bevestigen van publiek/segmenten in uw platform wordt gebruikt. Twee voorbeelden uit de branche zijn: `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` en `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`. |
| `httpMethod` | Tekenreeks | De methode die op uw eindpunt wordt gebruikt programmatically tot stand te brengen, bij te werken, te schrappen, of het segment/het publiek in uw bestemming te bevestigen. Bijvoorbeeld: `POST`, `PUT`, `DELETE` |
| `headers.header` | Tekenreeks | Geeft alle HTTP-headers op die moeten worden toegevoegd aan de aanroep van de API. Bijvoorbeeld: `"Content-Type"` |
| `headers.value` | Tekenreeks | Geeft de waarde aan van HTTP-headers die moeten worden toegevoegd aan de aanroep van de API. Bijvoorbeeld: `"application/x-www-form-urlencoded"` |
| `requestBody` | Tekenreeks | Hier geeft u de inhoud op van de berichttekst die naar de API moet worden verzonden. De parameters die aan de `requestBody` Het object is afhankelijk van de velden die de API accepteert. Raadpleeg voor een voorbeeld de [eerste sjabloonvoorbeeld](./audience-metadata-management.md#example-1) in het document met de metagegevensfunctionaliteit van het publiek. |
| `responseFields.name` | Tekenreeks | Geef antwoordvelden op die de API retourneert wanneer deze wordt aangeroepen. Raadpleeg voor een voorbeeld de [sjabloonvoorbeelden](./audience-metadata-management.md#examples) in het document met de metagegevensfunctionaliteit van het publiek. |
| `responseFields.value` | Tekenreeks | Geef de waarde op van de reactievelden die de API retourneert wanneer deze wordt aangeroepen. |
| `responseErrorFields.name` | Tekenreeks | Geef antwoordvelden op die de API retourneert wanneer deze wordt aangeroepen. Raadpleeg voor een voorbeeld de [ sjabloonvoorbeelden](./audience-metadata-management.md#examples) in het document met de metagegevensfunctionaliteit van het publiek. |
| `responseErrorFields.value` | Tekenreeks | Parseert om het even welke foutenmeldingen die op API vraagreacties van uw bestemming zijn teruggekeerd. Deze foutberichten worden weergegeven in de gebruikersinterface van het Experience Platform. |
| `validations.field` | Tekenreeks | Geeft aan of validaties voor velden moeten worden uitgevoerd voordat API-aanroepen naar uw doel worden uitgevoerd. U kunt bijvoorbeeld `{{validations.accountId}}` om de account-id van de gebruiker te valideren. |
| `validations.regex` | Tekenreeks | Hiermee geeft u aan hoe het veld moet worden gestructureerd voordat de validatie wordt doorgegeven. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met details van uw onlangs gecreeerde publiekssjabloon terug.

## Sjabloon voor publiek bijwerken {#update}

U kunt een bestaande publiekssjabloon bijwerken door een PUT aan te vragen bij de `/authoring/audience-templates` eindpunt en het verstrekken van instanceID van het publiekssjabloon u wilt bijwerken. In het lichaam van de vraag, verstrek het bijgewerkte malplaatje.

**API-indeling**

```http
PUT /authoring/audience-templates/{INSTANCE_ID}
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{INSTANCE_ID}` | De id van de sjabloon voor publiekmetagegevens die u wilt bijwerken. |

**Verzoek**

Het volgende verzoek werkt een bestaand malplaatje van publiekmeta-gegevens bij, dat door de parameters wordt gevormd die in de lading worden verstrekt.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1.0/{{customerData.accountId}}/customaudiences?fields=name,description,account_id&subtype=CUSTOM&name={{segment.name}}&customer_file_source={{segment.metadata.customer_file_source}}&access_token={{authData.accessToken}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?field=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}&&name={{segment.name}}&description={{segment.description}}&customer_file_source={{segment.metadata.customer_file_source}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?fields=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "validate":{
         "url":"https://api.moviestar.com/v1.0/permissions?access_token={{authData.accessToken}}",
         "httpMethod":"GET",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.data[0].permission}}",
               "name":"Id"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      }
   }
}
```

## Een lijst met publiekssjablonen ophalen {#retrieve-list}

U kunt een lijst van alle publiekssjablonen voor uw IMS-organisatie ophalen door een GET-aanvraag in te dienen bij de `/authoring/audience-templates` eindpunt.

**API-indeling**


```http
GET /authoring/audience-templates
```

**Verzoek**

Het volgende verzoek zal de lijst van publieksmalplaatjes terugwinnen die u toegang tot hebt, die op Organisatie IMS en zandbakconfiguratie wordt gebaseerd.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

De volgende reactie retourneert HTTP-status 200 met een lijst van publiekmetagegevenssjablonen waartoe u toegang hebt, op basis van de IMS-organisatie-id en de sandboxnaam die u hebt gebruikt. Eén `instanceId` komt overeen met de sjabloon voor één bestemming. De reactie is afgebroken voor de beknoptheid.

```json
{
   "items":[
      {
         "instanceId":"12a3238f-b509-4a40-b8fb-0a5006e7901d",
         "createdDate":"2021-07-20T13:30:30.843054Z",
         "lastModifiedDate":"2021-07-21T16:33:05.787472Z",
         "metadataTemplate":{
            "create":{
               "url":"https://api.moviestar.com/v2/dmpSegments",
               "httpMethod":"POST",
               "headers":[
                  {
                     "value":"application/json",
                     "header":"Content-Type"
                  },
                  {
                     "value":"Bearer {{authData.accessToken}}",
                     "header":"Authorization"
                  }
               ],
               "requestBody":{
                  "json":{
                     "name":"{{segment.name}}",
                     "type":"USER",
                     "account":"{{customerData.accountId}}",
                     "accessPolicy":"PRIVATE",
                     "destinations":[
                        {
                           "destination":"MOVIESTAR"
                        }
                     ],
                     "sourcePlatform":"ADOBE"
                  }
               },
               "responseFields":[
                  {
                     "value":"{{headers.x-moviestar-id}}",
                     "name":"externalAudienceId"
                  }
               ],
               "responseErrorFields":[
                  {
                     "value":"{{message}}",
                     "name":"message"
                  }
               ]
            },
            "update":{
               "url":"https://api.moviestar.com/v2/dmpSegments/{{segment.alias}}",
               "httpMethod":"POST",
               "headers":[
                  {
                     "value":"application/json",
                     "header":"Content-Type"
                  },
                  {
                     "value":"Bearer {{authData.accessToken}}",
                     "header":"Authorization"
                  }
               ],
               "requestBody":{
                  "json":{
                     "patch":{
                        "$set":{
                           "name":"{{segment.name}}"
                        }
                     }
                  }
               },
               "responseErrorFields":[
                  {
                     "value":"{{message}}",
                     "name":"message"
                  }
               ]
            },
            "delete":{
               "url":"https://api.moviestar.com/v2/dmpSegments/{{segment.alias}}",
               "httpMethod":"DELETE",
               "headers":[
                  {
                     "value":"application/json",
                     "header":"Content-Type"
                  },
                  {
                     "value":"Bearer {{authData.accessToken}}",
                     "header":"Authorization"
                  }
               ],
               "responseErrorFields":[
                  {
                     "value":"{{message}}",
                     "name":"message"
                  }
               ]
            },
            "name":"Moviestar audience template - Third example"
         }
      }
   ]
}
```

## Een specifieke publiekssjabloon ophalen {#get}

U kunt gedetailleerde informatie over een specifiek publiekssjabloon terugwinnen door een verzoek van de GET tot de `/authoring/audience-templates` eindpunt en het verstrekken van instanceID van het publiekssjabloon u wilt terugwinnen.

**API-indeling**

```http
GET /authoring/audience-templates/{INSTANCE_ID}
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{INSTANCE_ID}` | De id van de publieksmetagegevenssjabloon die u wilt ophalen. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met gedetailleerde informatie over het gespecificeerde publiekssjabloon terug.

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}",
                     "source_type":"FIRST_PARTY",
                     "ad_account_id":"{{customerData.accountId}}",
                     "retention_in_days":180
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"PUT",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "id":"{{segment.alias}}",
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}"
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://adsapi.moviestar.com/v1/segments/{{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "name":"Moviestar destination audience template - Example 1"
   }
}
```


## Een specifieke publiekssjabloon verwijderen {#delete}

U kunt de gespecificeerde publiekssjabloon verwijderen door een DELETE-aanvraag in te dienen bij de `/authoring/audience-templates` eindpunt en het verstrekken van identiteitskaart van het publiekssjabloon u wenst om in de verzoekweg te schrappen.

**API-indeling**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{INSTANCE_ID}` | De `id` van de publiekssjabloon die u wilt verwijderen. |

**Verzoek**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 samen met een lege HTTP-respons.

## API-foutafhandeling

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Zie [API-statuscodes](../../landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](../../landing/troubleshooting.md#request-header-errors) in de gids voor het oplossen van problemen met Platforms.

## Volgende stappen

Na het lezen van dit document weet u nu wanneer u sjablonen voor publieksmetagegevens gebruikt en hoe u een sjabloon voor publieksmetagegevens configureert met de opdracht `/authoring/audience-templates` API-eindpunt. Lezen [hoe te om Destination SDK te gebruiken om uw bestemming te vormen](./configure-destination-instructions.md) om te begrijpen waar deze stap in het proces past om uw bestemming te vormen.
