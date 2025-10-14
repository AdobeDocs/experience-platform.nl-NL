---
description: Gebruik publieksmetagegevenssjablonen om publiek in uw bestemming programmatisch te maken, bij te werken of te verwijderen. Adobe biedt een uitbreidbare sjabloon voor publieksmetagegevens, die u kunt configureren op basis van de specificaties van uw marketing-API. Nadat u het malplaatje bepaalt, test en voorlegt, zal het door Adobe worden gebruikt om de API vraag aan uw bestemming te structureren.
title: Metagegevensbeheer voor het publiek
exl-id: 795e8adb-c595-4ac5-8d1a-7940608d01cd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 2%

---

# Metagegevensbeheer voor het publiek

Gebruik publieksmetagegevenssjablonen om publiek in uw bestemming programmatisch te maken, bij te werken of te verwijderen. Adobe biedt een uitbreidbare sjabloon voor publieksmetagegevens, die u kunt configureren op basis van de specificaties van uw marketing-API. Nadat u bepaalt, test, en voorlegt de configuratie, zal het door Adobe worden gebruikt om de API vraag aan uw bestemming te structureren.

U kunt de in dit document beschreven functionaliteit configureren met behulp van het API-eindpunt van `/authoring/audience-templates` . Lees [&#x200B; creeer een meta-gegevensmalplaatje &#x200B;](../metadata-api/create-audience-template.md) voor een volledige lijst van verrichtingen u op het eindpunt kunt uitvoeren.

## Wanneer om het het beheerseindpunt van publiekmeta-gegevens te gebruiken {#when-to-use}

Afhankelijk van uw API configuratie, kunt u of niet het beheerseindpunt van publieksmeta-gegevens moeten gebruiken aangezien u uw bestemming in Experience Platform vormt. Gebruik het hieronder diagram van de beslissingsboom om te begrijpen wanneer om het eindpunt van publieksmeta-gegevens te gebruiken en hoe te om een malplaatje van publieksmeta-gegevens voor uw bestemming te vormen.

![&#x200B; diagram van de de boomstructuur van het Besluit &#x200B;](../assets/functionality/audience-metadata-decision-tree.png)

## Gebruik gevallen die worden ondersteund door het metagegevensbeheer van het publiek {#use-cases}

Als u de Experience Platform-bestemming configureert en ondersteuning biedt voor publiekmetagegevens in Destination SDK, kunt u Experience Platform-gebruikers een van de volgende opties bieden wanneer zij doelgroepen toewijzen en activeren. U kunt de opties controleren beschikbaar aan de gebruiker via de parameters in de [&#x200B; sectie van de de meta-gegevensconfiguratie van het publiek &#x200B;](../functionality/destination-configuration/audience-metadata-configuration.md) van de bestemmingsconfiguratie.

### Hoofdlettergebruik 1 - U hebt een API van derden en gebruikers hoeven geen toewijzings-id&#39;s in te voeren

Als u een API eindpunt hebt om publiek of publiek tot stand te brengen/bij te werken/te schrappen, kunt u de malplaatjes van publieksmeta-gegevens gebruiken om Destination SDK te vormen om de specs van uw publiek te vormen creeer/update/schrapt eindpunt. Experience Platform kan publiek programmatisch maken/bijwerken/verwijderen en metagegevens weer synchroniseren met Experience Platform.

Wanneer gebruikers in de gebruikersinterface van Experience Platform (UI) een publiek naar uw doel activeren, hoeven zij niet handmatig een veld voor de publiek-toewijzingsid in te vullen in de activeringsworkflow.

### Hoofdlettergebruik 2 - Gebruikers moeten eerst een publiek in uw bestemming maken en moeten handmatig een toewijzings-id invoeren

Als het publiek en andere meta-gegevens door partners of gebruikers manueel in uw bestemming moeten worden gecreeerd, dan moeten de gebruikers manueel het gebied van identiteitskaart van de publiekstoewijzing in het activeringswerkschema invullen om de publiek-timetadata tussen uw bestemming en Experience Platform te synchroniseren.

![&#x200B; identiteitskaart van de Afbeelding van de Input &#x200B;](../assets/functionality/input-mapping-id.png)

### Hoofdlettergebruik 3 - Uw doel accepteert de Experience Platform-gebruikers-id, gebruikers hoeven de toewijzings-id niet handmatig in te voeren

Als uw doelsysteem de gebruikers-id van Experience Platform accepteert, kunt u dit configureren in de sjabloon voor publieksmetagegevens. Gebruikers hoeven geen gebruikers-id voor publiekstoewijzing te vullen wanneer zij een segment activeren.

## Algemene en uitbreidbare publiekssjabloon {#generic-and-extensible}

Ter ondersteuning van de bovenstaande gebruiksgevallen beschikt Adobe over een algemene sjabloon die kan worden aangepast aan uw API-specificaties.

U kunt het generische malplaatje gebruiken om [&#x200B; een nieuw publiekssjabloon &#x200B;](../metadata-api/create-audience-template.md) tot stand te brengen als uw API steunt:

* De HTTP-methoden POST, GET, PUT, DELETE, PATCH
* De authentificatietypen: OAuth 1, OAuth 2 met verfrist teken, OAuth 2 met dragertoken
* De functies: een publiek maken, een publiek bijwerken, een publiek krijgen, een publiek verwijderen, referenties valideren

Het technische team van Adobe kan met u samenwerken om het generische malplaatje met douanevelden uit te breiden als uw gebruiksgevallen het vereisen.


## Ondersteunde sjabloongebeurtenissen {#supported-events}

In de onderstaande tabel worden de gebeurtenissen beschreven die door publiekmetagegevenssjablonen worden ondersteund.

| Sjabloonsectie | Beschrijving |
|--- |--- |
| `create` | Bevat alle vereiste componenten (URL, HTTP-methode, headers, request en response body) om een HTTP-aanroep naar uw API te maken, om programmatisch segmenten/publiek in uw platform te maken en de informatie weer te synchroniseren naar Adobe Experience Platform. |
| `update` | Bevat alle vereiste componenten (URL, HTTP-methode, headers, request en response body) om een HTTP-aanroep naar uw API uit te voeren, om segmenten/publiek in uw platform programmatisch bij te werken en de informatie weer te synchroniseren naar Adobe Experience Platform. |
| `delete` | Omvat alle vereiste componenten (URL, methode HTTP, kopballen, verzoek en reactielichaam) om een vraag van HTTP aan uw API te maken, segmenten/publiek in uw platform programmatically te schrappen. |
| `validate` | Voert bevestigingen voor om het even welke gebieden in de malplaatjeconfiguratie in werking alvorens een vraag aan partner API te maken. U kunt bijvoorbeeld controleren of de account-id van de gebruiker correct is ingevoerd. |
| `notify` | Is alleen van toepassing op doelen die op bestanden zijn gebaseerd. Bevat alle vereiste componenten (URL, HTTP-methode, headers, request en response body) om een HTTP-aanroep naar de API uit te voeren, zodat u op de hoogte wordt gebracht van het exporteren van bestanden. |
| `createDestination` | Bevat alle vereiste componenten (URL, HTTP-methode, headers, request en response body) om een HTTP-aanroep naar uw API uit te voeren, om programmatisch een dataflow in uw platform te maken en de informatie weer te synchroniseren naar Adobe Experience Platform. |
| `updateDestination` | Bevat alle vereiste componenten (URL, HTTP-methode, headers, request en response body) om een HTTP-aanroep naar uw API uit te voeren, een gegevensstroom in uw platform programmatisch bij te werken en de informatie weer te synchroniseren naar Adobe Experience Platform. |
| `deleteDestination` | Bevat alle vereiste componenten (URL, HTTP-methode, headers, request en response body) om een HTTP-aanroep naar de API uit te voeren, om een gegevensstroom via programmacode van het platform te verwijderen. |

{style="table-layout:auto"}

## Configuratievoorbeelden {#configuration-examples}

Deze sectie omvat voorbeelden van generische configuraties van publieksmeta-gegevens, voor uw verwijzing.

U ziet dat de URL, kopteksten en aanvraagorganen verschillen tussen de drie voorbeeldconfiguraties. Dit komt door de verschillende specificaties van de marketing-API van de drie voorbeeldplatforms.

In sommige voorbeelden worden macrovelden zoals `{{authData.accessToken}}` of `{{segment.name}}` gebruikt in de URL. In andere voorbeelden worden deze gebruikt in de kopteksten of in de aanvraagtekst. Het gebruik ervan hangt af van uw API-specificaties voor marketing.

+++Streaming, voorbeeld 1

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

+++

+++Streaming, voorbeeld 2

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

+++

+++Streaming, voorbeeld 3

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

+++

+++Op bestand gebaseerd voorbeeld

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

+++

De beschrijvingen van de vondst van alle parameters in het malplaatje in [&#x200B; leiden tot een kijkmalplaatje &#x200B;](../metadata-api/create-audience-template.md) API verwijzing.

## Macro&#39;s die in publieksmeta-gegevensmalplaatjes worden gebruikt {#macros}

De publiekssjablonen bevatten macro&#39;s die u kunt gebruiken om informatie door te geven, zoals gebruikers-id&#39;s, toegangstoken, foutberichten en meer tussen Experience Platform en uw API. Hieronder vindt u een beschrijving van de macro&#39;s die worden gebruikt in de drie configuratievoorbeelden op deze pagina:

| Macro | Beschrijving |
|--- |--- |
| `{{segment.alias}}` | Hiermee krijgt u toegang tot de publiekalias in Experience Platform. |
| `{{segment.name}}` | Hiermee krijgt u toegang tot de publieksnaam in Experience Platform. |
| `{{segment.id}}` | Hiermee hebt u toegang tot de gebruikers-id in Experience Platform. |
| `{{customerData.accountId}}` | Staat u toe om tot het gebied van accountIdentiteitskaart toegang te hebben dat u opstelling in de bestemmingsconfiguratie. |
| `{{oauth2ServiceAccessToken}}` | Staat u toe om een toegangstoken dynamisch te produceren die op uw configuratie OAuth 2 wordt gebaseerd. |
| `{{authData.accessToken}}` | Staat u toe om het toegangstoken tot uw API eindpunt over te gaan. Gebruik `{{authData.accessToken}}` als Experience Platform niet-vervallende tokens moet gebruiken om verbinding te maken met uw bestemming, anders gebruikt u `{{oauth2ServiceAccessToken}}` om een toegangstoken te genereren. |
| `{{body.segments[0].segment.id}}` | Retourneert de unieke id van het gemaakte publiek als de waarde van de sleutel `externalAudienceId` . |
| `{{error.message}}` | Retourneert een foutbericht dat wordt weergegeven voor gebruikers in de gebruikersinterface van Experience Platform. |
| `{{{segmentEnrichmentAttributes}}}` | Hiermee krijgt u toegang tot alle verrijkingskenmerken voor een bepaald publiek.  Deze macro wordt ondersteund door de gebeurtenissen `create` , `update` en `delete` . Verrijkingskenmerken zijn alleen beschikbaar voor [Aangepaste upload-doelgroepen](destination-configuration/schema-configuration.md#external-audiences). Zie de [&#x200B; gids van de de activering van het partijpubliek &#x200B;](../../ui/activate-batch-profile-destinations.md#select-enrichment-attributes) om te zien hoe de selectie van de verrijkingsattributen werkt. |
| `{{destination.name}}` | Retourneert de naam van uw doel. |
| `{{destination.sandboxName}}` | Retourneert de naam van de Experience Platform-sandbox waarin uw doel is geconfigureerd. |
| `{{destination.id}}` | Keert identiteitskaart van uw bestemmingsconfiguratie terug. |
| `{{destination.imsOrgId}}` | Retourneert de IMS Org-id waar uw doel is geconfigureerd. |
| `{{destination.enrichmentAttributes}}` | Hiermee krijgt u toegang tot alle verrijkingskenmerken voor alle soorten publiek die aan een doel zijn toegewezen. Deze macro wordt ondersteund door de gebeurtenissen `createDestination` , `updateDestination` en `deleteDestination` . Verrijkingskenmerken zijn alleen beschikbaar voor [Aangepaste upload-doelgroepen](destination-configuration/schema-configuration.md#external-audiences). Zie de [&#x200B; gids van de de activering van het partijpubliek &#x200B;](../../ui/activate-batch-profile-destinations.md#select-enrichment-attributes) om te zien hoe de selectie van de verrijkingsattributen werkt. |
| `{{destination.enrichmentAttributes.<namespace>.<segmentId>}}` | Hiermee krijgt u toegang tot verrijkingskenmerken voor specifieke externe doelgroepen. Verrijkingskenmerken zijn alleen beschikbaar voor [Aangepaste upload-doelgroepen](destination-configuration/schema-configuration.md#external-audiences). Zie de [&#x200B; gids van de de activering van het partijpubliek &#x200B;](../../ui/activate-batch-profile-destinations.md#select-enrichment-attributes) om te zien hoe de selectie van de verrijkingsattributen werkt. |

{style="table-layout:auto"}
