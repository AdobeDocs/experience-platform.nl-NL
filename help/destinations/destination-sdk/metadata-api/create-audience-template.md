---
description: Deze pagina illustreert de API vraag die wordt gebruikt om een publiekssjabloon door Adobe Experience Platform Destination SDK tot stand te brengen.
title: Een publiekssjabloon maken
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 3%

---


# Een publiekssjabloon maken

>[!IMPORTANT]
>
>**API-eindpunt**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Voor sommige bestemmingen die gebruikend Destination SDK worden gecreeerd, moet u een configuratie van publieksmeta-gegevens tot stand brengen programmatically om, segmentmeta-gegevens in de bestemming tot stand te brengen bij te werken of te schrappen. Op deze pagina ziet u hoe u de `/authoring/audience-templates` API eindpunt om de configuratie tot stand te brengen.

Voor een gedetailleerde beschrijving van de mogelijkheden die u door dit eindpunt kunt vormen, zie [beheer van metagegevens van het publiek](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Alle parameternamen en -waarden die door Destination SDK worden ondersteund, zijn **hoofdlettergevoelig**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Aan de slag met API-bewerkingen voor publiekssjablonen {#get-started}

Controleer voordat je doorgaat de [gids Aan de slag](../getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings creatie en vereiste kopballen te verkrijgen.

## Een publiekssjabloon maken {#create}

U kunt een nieuwe publiekssjabloon maken door een `POST` verzoek aan de `/authoring/audience-templates` eindpunt.

**API-indeling**

```http
POST /authoring/audience-templates
```

+++verzoek

Het volgende verzoek leidt tot een nieuw publieksmalplaatje, dat door de parameters wordt gevormd die in de lading worden verstrekt. De hieronder vermelde lading omvat alle parameters die door `/authoring/audience-templates` eindpunt. Merk op dat u niet alle parameters op de vraag moet toevoegen en dat het malplaatje, volgens uw API vereisten aanpasbaar is.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `requestBody` | Tekenreeks | Hier geeft u de inhoud op van de berichttekst die naar de API moet worden verzonden. De parameters die aan de `requestBody` Het object is afhankelijk van de velden die de API accepteert. Raadpleeg voor een voorbeeld de [eerste sjabloonvoorbeeld](../functionality/audience-metadata-management.md#example-1) in het document met de metagegevensfunctionaliteit van het publiek. |
| `responseFields.name` | Tekenreeks | Geef antwoordvelden op die de API retourneert wanneer deze wordt aangeroepen. Raadpleeg voor een voorbeeld de [sjabloonvoorbeelden](../functionality/audience-metadata-management.md#examples) in het document met de metagegevensfunctionaliteit van het publiek. |
| `responseFields.value` | Tekenreeks | Geef de waarde op van de reactievelden die de API retourneert wanneer deze wordt aangeroepen. |
| `responseErrorFields.name` | Tekenreeks | Geef antwoordvelden op die de API retourneert wanneer deze wordt aangeroepen. Raadpleeg voor een voorbeeld de [ sjabloonvoorbeelden](../functionality/audience-metadata-management.md#examples) in het document met de metagegevensfunctionaliteit van het publiek. |
| `responseErrorFields.value` | Tekenreeks | Parseert om het even welke foutenmeldingen die op API vraagreacties van uw bestemming zijn teruggekeerd. Deze foutberichten worden weergegeven in de gebruikersinterface van het Experience Platform. |
| `validations.field` | Tekenreeks | Geeft aan of validaties voor velden moeten worden uitgevoerd voordat API-aanroepen naar uw doel worden uitgevoerd. U kunt bijvoorbeeld `{{validations.accountId}}` om de account-id van de gebruiker te valideren. |
| `validations.regex` | Tekenreeks | Hiermee geeft u aan hoe het veld moet worden gestructureerd voordat de validatie wordt doorgegeven. |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met details van uw onlangs gecreeerde publiekssjabloon terug.

+++

## API-foutafhandeling

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Zie [API-statuscodes](../../../landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](../../../landing/troubleshooting.md#request-header-errors) in de gids voor het oplossen van problemen met Platforms.

## Volgende stappen

Na het lezen van dit document weet u nu wanneer u publiekssjablonen gebruikt en hoe u een publiekssjabloon kunt configureren met de `/authoring/audience-templates` API-eindpunt. Lezen [hoe te om Destination SDK te gebruiken om uw bestemming te vormen](../guides/configure-destination-instructions.md) om te begrijpen waar deze stap in het proces past om uw bestemming te vormen.
