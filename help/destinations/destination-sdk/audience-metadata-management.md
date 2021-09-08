---
description: Gebruik publieksmetagegevenssjablonen om publiek in uw bestemming programmatisch te maken, bij te werken of te verwijderen. Adobe verstrekt een verlengbaar malplaatje van publieksmeta-gegevens, dat u kunt vormen gebaseerd op de specificaties van uw marketing API. Nadat u het malplaatje bepaalt, test en voorlegt, zal het door Adobe worden gebruikt om de API vraag aan uw bestemming te structureren.
title: Metagegevensbeheer voor het publiek
source-git-commit: d2452bf0e59866d3deca57090001c4c5a0935525
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 0%

---

# Metagegevensbeheer voor het publiek {#audience-metadata-management}

## Overzicht {#overview}

Gebruik publieksmetagegevenssjablonen om publiek in uw bestemming programmatisch te maken, bij te werken of te verwijderen. Adobe verstrekt een verlengbaar malplaatje van publieksmeta-gegevens, dat u kunt vormen gebaseerd op de specificaties van uw marketing API. Nadat u bepaalt, test, en voorlegt de configuratie, zal het door Adobe worden gebruikt om de API vraag aan uw bestemming te structureren.

U kunt de in dit document beschreven functionaliteit vormen door het `/authoring/audience-templates` API eindpunt te gebruiken. Lees [API-bewerkingen voor het eindpunt van metagegevens van het publiek](./audience-metadata-api.md) voor een volledige lijst met bewerkingen die u op het eindpunt kunt uitvoeren.

## Wanneer om het het beheerseindpunt van publiekmeta-gegevens te gebruiken {#when-to-use}

Afhankelijk van uw API configuratie, kunt u of niet het beheerseindpunt van publieksmeta-gegevens moeten gebruiken aangezien u uw bestemming in Experience Platform vormt. Gebruik het hieronder diagram van de beslissingsboom om te begrijpen wanneer om het eindpunt van publieksmeta-gegevens te gebruiken en hoe te om een malplaatje van publieksmeta-gegevens voor uw bestemming te vormen.

![Beslissingsboomdiagram](./assets/audience-metadata-decision-tree.png)

## Gebruik gevallen die worden ondersteund door het metagegevensbeheer van het publiek {#use-cases}

Met steun van publieksmeta-gegevens in Doel SDK, wanneer u uw bestemming van het Experience Platform vormt, kunt u de gebruikers van het Platform één van verscheidene opties geven wanneer zij segmenten aan uw bestemming in kaart brengen en activeren. U kunt de opties controleren beschikbaar aan de gebruiker via de parameters in de sectie van de segmentafbeelding van [bestemmingsconfiguratie](./destination-configuration.md#segment-mapping).

### Hoofdlettergebruik 1 - U hebt een API van derden en gebruikers hoeven geen toewijzings-id&#39;s in te voeren

Als u een API eindpunt hebt om segmenten of soorten publiek tot stand te brengen/bij te werken/te schrappen, kunt u de malplaatjes van publieksmeta-gegevens gebruiken om de SDK van de Bestemming te vormen om specs van uw segment te passen creeer/update/schrapt eindpunt. Experience Platform kan programmatically segmenten creëren/bijwerken/schrappen en meta-gegevens terug naar Experience Platform synchroniseren.

Wanneer het activeren van segmenten aan uw bestemming in het gebruikersinterface van het Experience Platform (UI), te hoeven de gebruikers niet om een gebied van de segmentafbeelding identiteitskaart in het activeringswerkschema manueel in te vullen.

### Hoofdlettergebruik 2 - Gebruikers moeten eerst een segment in uw bestemming maken en moeten handmatig een toewijzings-id invoeren

Als de segmenten en andere meta-gegevens door partners of gebruikers manueel in uw bestemming moeten worden gecreeerd, dan moeten de gebruikers manueel het gebied van identiteitskaart van de segmentafbeelding in het activeringswerkschema invullen om de segmentmeta-gegevens tussen uw bestemming en Experience Platform te synchroniseren.

![Invoer-toewijzing-id](./assets/input-mapping-id.png)

### Hoofdlettergebruik 3 - Uw doel accepteert de Experience Platform-segment-id, gebruikers hoeven de toewijzings-id niet handmatig in te voeren

Als uw bestemmingssysteem identiteitskaart van het Experience Platform segment goedkeurt, kunt u dit in uw malplaatje van publieksmeta-gegevens vormen. Gebruikers hoeven een segment-toewijzings-id niet te vullen wanneer ze een segment activeren.

## Algemene en uitbreidbare publiekssjabloon {#generic-and-extensible}

Om de hierboven vermelde gebruiksgevallen te ondersteunen, biedt Adobe u een algemene sjabloon die kan worden aangepast aan uw API-specificaties.

U kunt het generische malplaatje gebruiken om [een nieuw publiekssjabloon te creëren](./audience-metadata-api.md#create) als uw API steunt:

* De HTTP-methoden: POST, GET, PUT, DELETE, PATCH
* De verificatietypen: OAuth 1, OAuth 2 met verfrist teken, OAuth 2 met dragertoken
* De functies: een publiek maken, een publiek bijwerken, een publiek opvragen, een publiek verwijderen, referenties valideren

Het technische team van Adobe kan met u werken om het generische malplaatje met douanevelden uit te breiden als uw gebruiksgevallen het vereist.

## Sjabloonvoorbeelden {#template-examples}

Deze sectie omvat drie voorbeelden van generische configuraties van publieksmeta-gegevens, voor uw verwijzing, samen met beschrijvingen van de belangrijkste secties van de configuratie. U ziet dat de URL, kopteksten, verzoeken en antwoorden verschillen tussen de drie voorbeeldconfiguraties. Dit komt door de verschillende specificaties van de marketing-API van de drie voorbeeldplatforms.

In sommige voorbeelden worden macrovelden zoals `{{authData.accessToken}}` of `{{segment.name}}` gebruikt in de URL en in andere voorbeelden worden deze gebruikt in de kopteksten of in de aanvraagtekst. Het hangt echt af van uw marketing API specificaties.

| Sjabloonsectie | Beschrijving |
|--- |--- |
| `create` | Bevat alle vereiste componenten (URL, HTTP-methode, headers, request en response body) om een HTTP-aanroep naar uw API te maken, om programmatisch segmenten/publiek in uw platform te maken en de informatie weer te synchroniseren naar Adobe Experience Platform. |
| `update` | Bevat alle vereiste componenten (URL, HTTP-methode, headers, request en response body) om een HTTP-aanroep naar uw API uit te voeren, segmenten/publiek in uw platform programmatisch bij te werken en de informatie weer te synchroniseren naar Adobe Experience Platform. |
| `delete` | Omvat alle vereiste componenten (URL, methode HTTP, kopballen, verzoek en reactielichaam) om een vraag van HTTP aan uw API te maken, segmenten/publiek in uw platform programmatically te schrappen. |
| `validations` | Voert bevestigingen voor om het even welke gebieden in de malplaatjeconfiguratie in werking alvorens een vraag aan partner API te maken. U kunt bijvoorbeeld controleren of de account-id van de gebruiker correct is ingevoerd. |

{style=&quot;table-layout:auto&quot;}

### Eerste voorbeeld {#example-1}

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

### Tweede voorbeeld {#example-2}

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

### Derde voorbeeld {#example-3}

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

Zoek beschrijvingen van alle parameters in het malplaatje in de verwijzingsdocumentatie [de verrichtingen van het de meta-gegevenseindpunt van het publiek ](./audience-metadata-api.md).

## Macro&#39;s die in publieksmeta-gegevensmalplaatjes worden gebruikt

Om informatie zoals segment IDs, toegangstokens, foutenmeldingen, en meer tussen Experience Platform en uw API over te gaan, omvatten de publiekssjablonen macro&#39;s die u kunt gebruiken. Hieronder vindt u een beschrijving van de macro&#39;s die worden gebruikt in de drie configuratievoorbeelden op deze pagina:

| Macro | Beschrijving |
|--- |--- |
| `{{segment.alias}}` | Staat u toe om tot het segment alias in Experience Platform toegang te hebben. |
| `{{segment.name}}` | Staat u toe om tot de segmentnaam in Experience Platform toegang te hebben. |
| `{{segment.id}}` | Staat u toe om tot segmentidentiteitskaart in Experience Platform toegang te hebben. |
| `{{customerData.accountId}}` | Staat u toe om tot het gebied van accountIdentiteitskaart toegang te hebben dat u opstelling in de bestemmingsconfiguratie. |
| `{{oauth2ServiceAccessToken}}` | Staat u toe om een toegangstoken dynamisch te produceren die op uw configuratie OAuth 2 wordt gebaseerd. |
| `{{authData.accessToken}}` | Staat u toe om het toegangstoken tot uw API eindpunt over te gaan. Gebruik `{{authData.accessToken}}` als het Experience Platform niet-vervallende tokens zou moeten gebruiken om met uw bestemming te verbinden, anders `{{oauth2ServiceAccessToken}}` gebruiken om een toegangstoken te produceren. |
| `{{body.segments[0].segment.id}}` | Retourneert de unieke id van het gemaakte publiek als de waarde van de sleutel `externalAudienceId`. |
| `{{error.message}}` | Retourneert een foutbericht dat wordt weergegeven aan gebruikers in de gebruikersinterface van het Experience Platform. |

{style=&quot;table-layout:auto&quot;}
