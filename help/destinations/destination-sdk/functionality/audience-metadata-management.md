---
description: Gebruik publieksmetagegevenssjablonen om publiek in uw bestemming programmatisch te maken, bij te werken of te verwijderen. Adobe verstrekt een verlengbaar malplaatje van publieksmeta-gegevens, dat u kunt vormen gebaseerd op de specificaties van uw marketing API. Nadat u het malplaatje bepaalt, test en voorlegt, zal het door Adobe worden gebruikt om de API vraag aan uw bestemming te structureren.
title: Metagegevensbeheer voor het publiek
exl-id: 795e8adb-c595-4ac5-8d1a-7940608d01cd
source-git-commit: 3660c3a342af07268d2ca2c907145df8237872a1
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 0%

---

# Metagegevensbeheer voor het publiek

Gebruik publieksmetagegevenssjablonen om publiek in uw bestemming programmatisch te maken, bij te werken of te verwijderen. Adobe verstrekt een verlengbaar malplaatje van publieksmeta-gegevens, dat u kunt vormen gebaseerd op de specificaties van uw marketing API. Nadat u bepaalt, test, en voorlegt de configuratie, zal het door Adobe worden gebruikt om de API vraag aan uw bestemming te structureren.

U kunt de in dit document beschreven functionaliteit configureren met de opdracht `/authoring/audience-templates` API-eindpunt. Lezen [een sjabloon voor metagegevens maken](../metadata-api/create-audience-template.md) voor een volledige lijst van verrichtingen kunt u op het eindpunt uitvoeren.

## Wanneer om het het beheerseindpunt van publiekmeta-gegevens te gebruiken {#when-to-use}

Afhankelijk van uw API configuratie, kunt u of niet het beheerseindpunt van publieksmeta-gegevens moeten gebruiken aangezien u uw bestemming in Experience Platform vormt. Gebruik het hieronder diagram van de beslissingsboom om te begrijpen wanneer om het eindpunt van publieksmeta-gegevens te gebruiken en hoe te om een malplaatje van publieksmeta-gegevens voor uw bestemming te vormen.

![Beslissingsboomdiagram](../assets/functionality/audience-metadata-decision-tree.png)

## Gebruik gevallen die worden ondersteund door het metagegevensbeheer van het publiek {#use-cases}

Met de steun van publieksmeta-gegevens in Destination SDK, wanneer u uw bestemming van het Experience Platform vormt, kunt u de gebruikers van het Platform één van verscheidene opties geven wanneer zij in kaart brengen en publiek activeren aan uw bestemming. U kunt de opties bepalen die beschikbaar zijn voor de gebruiker via de parameters in het dialoogvenster [Configuratie van metagegevens voor publiek](../functionality/destination-configuration/audience-metadata-configuration.md) sectie van de bestemmingsconfiguratie.

### Hoofdlettergebruik 1 - U hebt een API van derden en gebruikers hoeven geen toewijzings-id&#39;s in te voeren

Als u een API eindpunt hebt om publiek of publiek tot stand te brengen/bij te werken/te schrappen, kunt u de malplaatjes van publieksmeta-gegevens gebruiken om Destination SDK te vormen om de specificaties van uw publiek te passen creeer/update/schrapt eindpunt. Experience Platform kan publiek programmatically creëren/bijwerken/schrappen en meta-gegevens terug naar Experience Platform synchroniseren.

Wanneer het activeren van publiek aan uw bestemming in het gebruikersinterface van het Experience Platform (UI), te hoeven de gebruikers niet om een gebied van identiteitskaart van de publiekstoewijzing in het activeringswerkschema manueel in te vullen.

### Hoofdlettergebruik 2 - Gebruikers moeten eerst een publiek in uw bestemming maken en moeten handmatig een toewijzings-id invoeren

Als het publiek en andere meta-gegevens door partners of gebruikers manueel in uw bestemming moeten worden gecreeerd, dan moeten de gebruikers het gebied van identiteitskaart van de publiekstoewijzing in het activeringswerkschema manueel invullen om de publiekMeta-gegevens tussen uw bestemming en Experience Platform te synchroniseren.

![Invoer-toewijzing-id](../assets/functionality/input-mapping-id.png)

### Hoofdlettergebruik 3 - Uw doel accepteert de gebruikers-id van het Experience Platform, gebruikers hoeven de toewijzing-id niet handmatig in te voeren

Als uw bestemmingssysteem de identiteitskaart van het publiek van het Experience Platform goedkeurt, kunt u dit in uw malplaatje van publieksmeta-gegevens vormen. Gebruikers hoeven geen gebruikers-id voor publiekstoewijzing te vullen wanneer zij een segment activeren.

## Algemene en uitbreidbare publiekssjabloon {#generic-and-extensible}

Ter ondersteuning van de hierboven vermelde gebruiksgevallen beschikt de Adobe over een algemene sjabloon die kan worden aangepast aan uw API-specificaties.

U kunt de generieke sjabloon gebruiken om [een nieuwe publiekssjabloon maken](../metadata-api/create-audience-template.md) als uw API ondersteuning biedt voor:

* De HTTP-methoden: POST, GET, PUT, DELETE, PATCH
* De authentificatietypen: OAuth 1, OAuth 2 met verfrist teken, OAuth 2 met dragertoken
* De functies: een publiek maken, een publiek bijwerken, een publiek krijgen, een publiek verwijderen, referenties valideren

Het technische team van de Adobe kan met u werken om het generische malplaatje met douanevelden uit te breiden als uw gebruiksgevallen het vereisen.

## Configuratievoorbeelden {#configuration-examples}

Deze sectie omvat drie voorbeelden van generische configuraties van publieksmeta-gegevens, voor uw verwijzing, samen met beschrijvingen van de belangrijkste secties van de configuratie. U ziet dat de URL, kopteksten, verzoeken en antwoorden verschillen tussen de drie voorbeeldconfiguraties. Dit komt door de verschillende specificaties van de marketing-API van de drie voorbeeldplatforms.

Merk op dat in sommige voorbeelden macrogebieden zoals `{{authData.accessToken}}` of `{{segment.name}}` worden gebruikt in de URL, en in andere voorbeelden worden deze gebruikt in de kopballen of het verzoeklichaam. Dit hangt echt af van uw API-specificaties voor marketing.

| Sjabloonsectie | Beschrijving |
|--- |--- |
| `create` | Bevat alle vereiste componenten (URL, HTTP-methode, headers, request en response body) om een HTTP-aanroep naar uw API te maken, om programmatisch segmenten/publiek in uw platform te maken en de informatie weer te synchroniseren naar Adobe Experience Platform. |
| `update` | Bevat alle vereiste componenten (URL, HTTP-methode, headers, request en response body) om een HTTP-aanroep naar uw API uit te voeren, om segmenten/publiek in uw platform programmatisch bij te werken en de informatie weer te synchroniseren naar Adobe Experience Platform. |
| `delete` | Omvat alle vereiste componenten (URL, methode HTTP, kopballen, verzoek en reactielichaam) om een vraag van HTTP aan uw API te maken, segmenten/publiek in uw platform programmatically te schrappen. |
| `validate` | Voert bevestigingen voor om het even welke gebieden in de malplaatjeconfiguratie in werking alvorens een vraag aan partner API te maken. U kunt bijvoorbeeld controleren of de account-id van de gebruiker correct is ingevoerd. |
| `notify` | Is alleen van toepassing op doelen die op bestanden zijn gebaseerd. Bevat alle vereiste componenten (URL, HTTP-methode, headers, request en response body) om een HTTP-aanroep naar de API uit te voeren, zodat u op de hoogte wordt gebracht van het exporteren van bestanden. |

{style="table-layout:auto"}

### Streaming voorbeeld 1 {#example-1}

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
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
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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

### Streaming voorbeeld 2 {#example-2}

```json
{
   "instanceId":"12c78017-5af3-4d4e-8f9c-d330c547c482",
   "createdDate":"2021-07-20T13:27:37.029490Z",
   "lastModifiedDate":"2021-07-20T18:53:03.622306Z",
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

### Streaming voorbeeld 3 {#example-3}

```json
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
```


### Voorbeeld op basis van bestand {#example-file-based}

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
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
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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
      "notify":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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

Beschrijvingen van alle parameters in de sjabloon zoeken in het dialoogvenster [Een publiekssjabloon maken](../metadata-api/create-audience-template.md) API-referentie.

## Macro&#39;s die in publieksmeta-gegevensmalplaatjes worden gebruikt {#macros}

Om informatie zoals publiek IDs, toegangstoken, foutenmeldingen, en meer tussen Experience Platform en uw API over te gaan, omvatten de publiekssjablonen macro&#39;s die u kunt gebruiken. Hieronder vindt u een beschrijving van de macro&#39;s die worden gebruikt in de drie configuratievoorbeelden op deze pagina:

| Macro | Beschrijving |
|--- |--- |
| `{{segment.alias}}` | Hiermee krijgt u toegang tot de publiekalias in het Experience Platform. |
| `{{segment.name}}` | Hiermee krijgt u toegang tot de publieksnaam in het Experience Platform. |
| `{{segment.id}}` | Hiermee hebt u toegang tot de gebruikers-id in het Experience Platform. |
| `{{customerData.accountId}}` | Staat u toe om tot het gebied van accountIdentiteitskaart toegang te hebben dat u opstelling in de bestemmingsconfiguratie. |
| `{{oauth2ServiceAccessToken}}` | Staat u toe om een toegangstoken dynamisch te produceren die op uw configuratie OAuth 2 wordt gebaseerd. |
| `{{authData.accessToken}}` | Staat u toe om het toegangstoken tot uw API eindpunt over te gaan. Gebruiken `{{authData.accessToken}}` als het Experience Platform niet-vervallende tokens zou moeten gebruiken om met uw bestemming te verbinden, anders gebruik `{{oauth2ServiceAccessToken}}` om een toegangstoken te produceren. |
| `{{body.segments[0].segment.id}}` | Hiermee wordt de unieke id van het gemaakte publiek geretourneerd als de waarde van de sleutel `externalAudienceId`. |
| `{{error.message}}` | Retourneert een foutbericht dat wordt weergegeven aan gebruikers in de gebruikersinterface van het Experience Platform. |

{style="table-layout:auto"}
