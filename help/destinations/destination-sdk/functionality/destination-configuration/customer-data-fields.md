---
description: Leer hoe u invoervelden maakt in de gebruikersinterface van het Experience Platform waarmee uw gebruikers verschillende informatie kunnen opgeven die relevant is voor het maken van een verbinding en het exporteren van gegevens naar uw bestemming.
title: Gegevensvelden van de klant
exl-id: 7f5b8278-175c-4ab8-bf67-8132d128899e
source-git-commit: b35f584d13fb241c06b4045b525d84775ef8317c
workflow-type: tm+mt
source-wordcount: '1722'
ht-degree: 0%

---

# Gebruikersinvoer configureren via gegevensvelden van klanten

Wanneer het verbinden met uw bestemming in de UI van het Experience Platform, zou u uw gebruikers kunnen nodig hebben om specifieke configuratiedetails te verstrekken of specifieke opties te selecteren die u ter beschikking stelt aan hen. In Destination SDK worden deze opties gegevensvelden voor klanten genoemd.

Om te begrijpen waar deze component in een integratie past die met Destination SDK wordt gecreeerd, zie het diagram in de [ documentatie van configuratieopties ](../configuration-options.md) of zie de volgende pagina&#39;s van het overzicht van bestemmingsconfiguratie:

* [Gebruik Destination SDK om een streamingbestemming te configureren](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Gebruik Destination SDK om een op een bestand gebaseerde bestemming te configureren](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

## Gebruik gevallen voor gegevensvelden van klanten {#use-cases}

De gebieden van de klantengegevens van het gebruik voor een verscheidenheid van gebruiksgevallen waar u gebruikers nodig hebt om gegevens in de UI van het Experience Platform in te voeren. Gebruik bijvoorbeeld gegevensvelden van klanten wanneer gebruikers het volgende moeten opgeven:

* Namen en paden van cloudopslagemmertjes voor op bestanden gebaseerde doelen.
* De indeling die wordt geaccepteerd door de gegevensvelden van de klant.
* Beschikbare bestandcompressietypen waaruit gebruikers kunnen kiezen.
* Een lijst met beschikbare eindpunten voor integratie in real time (streaming).

U kunt de gebieden van klantengegevens via het `/authoring/destinations` eindpunt vormen. Zie de volgende API verwijzingspagina&#39;s voor gedetailleerde API vraagvoorbeelden waar u de componenten kunt vormen die in deze pagina worden getoond.

* [Een doelconfiguratie maken](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Een doelconfiguratie bijwerken](../../authoring-api/destination-configuration/update-destination-configuration.md)

In dit artikel worden alle ondersteunde configuratietypen voor klantgegevensvelden beschreven die u voor uw doel kunt gebruiken, en wordt aangegeven welke klanten in de gebruikersinterface van het Experience Platform zullen zien.

>[!IMPORTANT]
>
>Alle parameternamen en waarden die door Destination SDK worden gesteund zijn **gevoelig geval**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Ondersteunde integratietypen {#supported-integration-types}

Raadpleeg de onderstaande tabel voor meer informatie over de integratietypen die de op deze pagina beschreven functionaliteit ondersteunen.

| Type integratie | Ondersteunt functionaliteit |
|---|---|
| Integraties in realtime (streaming) | Ja |
| Op bestanden gebaseerde (batch) integratie | Ja |

## Ondersteunde parameters {#supported-parameters}

Wanneer u uw eigen gegevensvelden voor klanten maakt, kunt u de parameters in de onderstaande tabel gebruiken om hun gedrag te configureren.

| Parameter | Type | Vereist/optioneel | Beschrijving |
|---------|----------|------|---|
| `name` | String | Vereist | Geef een naam op voor het aangepaste veld dat u introduceert. Deze naam is niet zichtbaar in de gebruikersinterface van het platform, tenzij het veld `title` leeg is of ontbreekt. |
| `type` | String | Vereist | Hiermee geeft u het type van het aangepaste veld aan dat u wilt gebruiken. Geaccepteerde waarden: <ul><li>`string`</li><li>`object`</li><li>`integer`</li></ul> |
| `title` | String | Optioneel | Hiermee wordt de naam van het veld aangegeven, zoals deze wordt weergegeven door klanten in de gebruikersinterface van het platform. Als dit veld leeg is of ontbreekt, neemt de interface de veldnaam over van de waarde `name` . |
| `description` | String | Optioneel | Geef een beschrijving op voor het aangepaste veld. Deze beschrijving is niet zichtbaar in de interface van het Platform. |
| `isRequired` | Boolean | Optioneel | Geeft aan of gebruikers een waarde voor dit veld moeten opgeven in de workflow voor de doelconfiguratie. |
| `pattern` | String | Optioneel | Hiermee wordt, indien nodig, een patroon voor het aangepaste veld afgedwongen. Gebruik reguliere expressies om een patroon af te dwingen. Als uw klant-id&#39;s bijvoorbeeld geen cijfers of onderstrepingstekens bevatten, voert u `^[A-Za-z]+$` in dit veld in. |
| `enum` | String | Optioneel | Hiermee geeft u het aangepaste veld weer als een vervolgkeuzemenu en geeft u de opties weer die beschikbaar zijn voor de gebruiker. |
| `default` | String | Optioneel | Definieert de standaardwaarde in de lijst `enum` . |
| `hidden` | Boolean | Optioneel | Geeft aan of het gegevensveld van de klant al dan niet in de gebruikersinterface wordt weergegeven. |
| `unique` | Boolean | Optioneel | Gebruik deze parameter wanneer u een gebied van klantengegevens moet creëren de waarvan waarde over alle bestemmingsdataflows opstelling door de organisatie van een gebruiker uniek moet zijn. Bijvoorbeeld, moet het **[!UICONTROL Integration alias]** gebied in de [ Personalization van de Douane ](../../../catalog/personalization/custom-personalization.md) bestemming uniek zijn, betekenend dat twee afzonderlijke dataflows aan deze bestemming niet de zelfde waarde voor dit gebied kunnen hebben. |
| `readOnly` | Boolean | Optioneel | Geeft aan of de klant de waarde van het veld kan wijzigen of niet. |

{style="table-layout:auto"}

In het onderstaande voorbeeld definieert de sectie `customerDataFields` twee velden die gebruikers moeten invoeren in de interface van het platform wanneer ze verbinding maken met het doel:

* `Account ID`: Een gebruikersaccount-id voor het doelplatform.
* `Endpoint region`: Het regionale eindpunt van de API waarmee ze verbinding maken. In de sectie `enum` wordt een vervolgkeuzemenu gemaakt met de waarden die binnen de beschikbare ruimte voor de gebruikers zijn gedefinieerd.

```json
"customerDataFields":[
   {
      "name":"accountID",
      "title":"User account ID",
      "description":"User account ID for the destination platform.",
      "type":"string",
      "isRequired":true
   },
   {
      "name":"region",
      "title":"API endpoint region",
      "description":"The API endpoint region that the user should connect to.",
      "type":"string",
      "isRequired":true,
      "enum":[
         "EU"
         "US",
      ],
      "readOnly":false,
      "hidden":false
   }
]
```

De resulterende ervaring met de gebruikersinterface wordt weergegeven in de onderstaande afbeelding.

![ beeld van Ui dat een voorbeeld van de gebieden van klantengegevens toont.](../../assets/functionality/destination-configuration/customer-data-fields-example.png)

## Namen en beschrijvingen van doelverbindingen {#names-description}

Wanneer u een nieuw doel maakt, voegt Destination SDK automatisch **[!UICONTROL Name]** - en **[!UICONTROL Description]** -velden toe aan het scherm met de doelverbinding in de gebruikersinterface van het platform. Zoals u in het bovenstaande voorbeeld kunt zien, worden de velden **[!UICONTROL Name]** en **[!UICONTROL Description]** weergegeven in de gebruikersinterface zonder te worden opgenomen in de configuratie van de gegevensvelden van de klant.

>[!IMPORTANT]
>
>Als u **[!UICONTROL Name]** en **[!UICONTROL Description]** gebieden in de configuratie van de gebieden van klantengegevens toevoegt, zullen de gebruikers hen zien gedupliceerd in UI.

## Gegevensvelden van klanten bestellen {#ordering}

De orde waarin u de gebieden van klantengegevens in de bestemmingsconfiguratie toevoegt wordt weerspiegeld in Platform UI.

De onderstaande configuratie wordt bijvoorbeeld dienovereenkomstig weergegeven in de gebruikersinterface, waarbij de opties worden weergegeven in de volgorde **[!UICONTROL Name]**, **[!UICONTROL Description]**, **[!UICONTROL Bucket name]**, **[!UICONTROL Folder path]**, **[!UICONTROL File Type]** en **[!UICONTROL Compression format]** .

```json
"customerDataFields":[
{
   "name":"bucketName",
   "title":"Bucket name",
   "description":"Amazon S3 bucket name",
   "type":"string",
   "isRequired":true,
   "pattern":"(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
   "readOnly":false,
   "hidden":false
},
{
   "name":"path",
   "title":"Folder path",
   "description":"Enter the path to your S3 bucket folder",
   "type":"string",
   "isRequired":true,
   "pattern":"^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
   "readOnly":false,
   "hidden":false
},
{
   "name":"fileType",
   "title":"File Type",
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
}
]
```

![ Beeld dat de orde van dossier het formatteren opties in Experience Platform UI toont.](../../assets/functionality/destination-configuration/customer-data-fields-order.png)

## Gegevensvelden van klanten groeperen {#grouping}

U kunt meerdere gegevensvelden van klanten groeperen binnen één sectie. Wanneer het plaatsen van de verbinding aan de bestemming in UI, kunnen de gebruikers van een visuele groepering van gelijkaardige gebieden zien en profiteren.

Hiertoe maakt u met `"type": "object"` de groep en verzamelt u de gewenste gegevensvelden van de klant in een `properties` -object, zoals in de onderstaande afbeelding wordt getoond, waar de groepering **[!UICONTROL CSV Options]** wordt gemarkeerd.

```json {line-numbers="true" highlight="6-28"}
"customerDataFields":[
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ]
   }
]
```

![ Beeld die de gebieden van klantengegevens groeperen in UI tonen.](../../assets/functionality/destination-configuration/group-customer-data-fields.png)

## Drupdown-kiezers maken voor gegevensvelden van klanten {#dropdown-selectors}

In situaties waarin u gebruikers de keuze wilt laten tussen verschillende opties, bijvoorbeeld met welk teken de velden in CSV-bestanden worden afgebakend, kunt u vervolgkeuzelijsten toevoegen aan de gebruikersinterface.

Hiervoor gebruikt u het `namedEnum` -object zoals hieronder wordt weergegeven en configureert u een `default` -waarde voor de opties die de gebruiker kan selecteren.

```json {line-numbers="true" highlight="15-24"}
"customerDataFields":[
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ]
   }
]
```

![ het registreren van het Scherm die een voorbeeld van dropdown selecteurs tonen die met de hierboven getoonde configuratie worden gecreeerd.](../../assets/functionality/destination-configuration/customer-data-fields-dropdown.gif)

## Dynamische vervolgkeuzekiezers maken voor gegevensvelden van klanten {#dynamic-dropdown-selectors}

In situaties waarin u een API dynamisch wilt aanroepen en de reactie wilt gebruiken om de opties in een vervolgkeuzemenu dynamisch te vullen, kunt u een dynamische vervolgkeuzekiezer gebruiken.

De dynamische dropdown selecteurs kijken identiek aan de [ regelmatige dropdown selecteurs ](#dropdown-selectors) in UI. Het enige verschil is dat de waarden dynamisch worden opgehaald van een API.

Als u een dynamische vervolgkeuzekiezer wilt maken, moet u twee componenten configureren:

**Stap 1.** [ creeer een bestemmingsserver ](../../authoring-api/destination-server/create-destination-server.md#dynamic-dropdown-servers) met een `responseFields` malplaatje voor de dynamische API vraag, zoals hieronder getoond.

```json
{
   "name":"Server for dynamic dropdown",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":" <--YOUR-API-ENDPOINT-PATH--> "
      }
   },
   "httpTemplate":{
      "httpMethod":"GET",
      "headers":[
         {
            "header":"Authorization",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"My Bearer Token"
            }
         },
         {
            "header":"x-integration",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.integrationId}}"
            }
         },
         {
            "header":"Accept",
            "value":{
               "templatingStrategy":"NONE",
               "value":"application/json"
            }
         }
      ]
   },
   "responseFields":[
      {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{% set list = [] %} {% for record in response.body %} {% set list = list|merge([{'name' : record.name, 'value' : record.id }]) %} {% endfor %}{{ {'list': list} | toJson | raw }}",
         "name":"list"
      }
   ]
}
```

**Stap 2.** Gebruik het object `dynamicEnum` , zoals hieronder wordt weergegeven. In het onderstaande voorbeeld wordt het vervolgkeuzemenu `User` opgehaald met de dynamische server.


```json {line-numbers="true" highlight="13-21"}
"customerDataFields": [
  {
    "name": "integrationId",
    "title": "Integration ID",
    "type": "string",
    "isRequired": true
  },
  {
    "name": "userId",
    "title": "User",
    "type": "string",
    "isRequired": true,
    "dynamicEnum": {
      "queryParams": [
        "integrationId"
      ],
      "destinationServerId": "<~dynamic-field-server-id~>",
      "authenticationRule": "CUSTOMER_AUTHENTICATION",
      "value": "$.list",
      "responseFormat": "NAME_VALUE"
    }
  }
]
```

Stel de parameter `destinationServerId` in op de id van de doelserver die u bij stap 1 hebt gemaakt. U kunt de identiteitskaart van de bestemmingsserver in de reactie van [ zien wint een configuratie van de bestemmingsserver ](../../authoring-api/destination-server/retrieve-destination-server.md) API vraag terug.

## Geneste gegevensvelden voor klanten maken {#nested-fields}

U kunt geneste gegevensvelden voor klanten maken voor complexe integratiepatronen. Hierdoor kunt u een reeks selecties voor de klant koppelen.

U kunt bijvoorbeeld geneste gegevensvelden voor klanten toevoegen, zodat klanten een integratietype met uw bestemming moeten selecteren, gevolgd door onmiddellijk een andere selectie. De tweede selectie is een genest veld binnen het integratietype.

Als u een genest veld wilt toevoegen, gebruikt u de parameter `properties` (zie hieronder). In het configuratievoorbeeld hieronder, kunt u drie afzonderlijke genestelde gebieden binnen **zien uw bestemming - het Specifieke gebied van de Montages van de Integratie** klantengegevens.

>[!TIP]
>
>Vanaf de release van april 2024 kunt u een parameter `isRequired` instellen voor geneste velden. In het onderstaande configuratiefragment worden bijvoorbeeld de eerste twee geneste velden gemarkeerd als verplicht (gemarkeerde regel xxx) en kunnen klanten alleen verdergaan als ze een waarde voor het veld selecteren. Lees meer over vereiste gebieden in de [ gesteunde parameters ](#supported-parameters) sectie.

```json {line-numbers="true" highlight="11,20"}
    {
      "name": "yourdestination",
      "title": "Yourdestination - Integration Specific Settings",
      "type": "object",
      "properties": [
        {
          "name": "agreement",
          "title": "Advertiser data destination terms agreement. Enter I AGREE.",
          "type": "string",
          "isRequired": true,
          "pattern": "I AGREE",
          "readOnly": false,
          "hidden": false
        },
        {
          "name": "account-name",
          "title": "Account name",
          "type": "string",
          "isRequired": true,
          "readOnly": false,
          "hidden": false
        },
        {
          "name": "email",
          "title": "Email address",
          "type": "string",
          "isRequired": false,
          "pattern": "^[\\w-\\.]+@([\\w-]+\\.)+[\\w-]{2,4}$",
          "readOnly": false,
          "hidden": false
        }
      ],
      "isRequired": false,
      "readOnly": false,
      "hidden": false,
```

## Voorwaardelijke gegevensvelden voor klanten maken {#conditional-options}

U kunt voorwaardelijke gegevensvelden voor klanten maken die alleen in de activeringsworkflow worden weergegeven wanneer gebruikers een bepaalde optie selecteren.

U kunt bijvoorbeeld opties voor voorwaardelijke bestandsindeling maken die alleen worden weergegeven wanneer gebruikers een specifiek exporttype voor bestanden selecteren.

In de onderstaande configuratie wordt een voorwaardelijke groepering gemaakt voor opmaakopties voor CSV-bestanden. De CSV-bestandsopties worden alleen weergegeven wanneer de gebruiker CSV selecteert als het gewenste bestandstype voor exporteren.

Als u een veld als voorwaardelijk wilt instellen, gebruikt u de parameter `conditional` zoals hieronder wordt weergegeven:

```json
"conditional": {
   "field": "fileType",
   "operator": "EQUALS",
   "value": "CSV"
}
```

In een bredere context ziet u het veld `conditional` dat wordt gebruikt in de doelconfiguratie hieronder, naast de `fileType` tekenreeks en het object `csvOptions` waarin deze is gedefinieerd. De voorwaardelijke velden worden gedefinieerd in de parameter `properties` .

```json {line-numbers="true" highlight="3-15, 21-25"}
"customerDataFields":[
   {
      "name":"fileType",
      "title":"File Type",
      "description":"Select your file type",
      "type":"string",
      "isRequired":true,
      "enum":[
         "PARQUET",
         "CSV",
         "JSON"
      ],
      "readOnly":false,
      "hidden":false
   },
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "conditional":{
         "field":"fileType",
         "operator":"EQUALS",
         "value":"CSV"
      },
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"quote",
            "title":"Quote Character",
            "description":"Select your Quote character",
            "type":"string",
            "isRequired":false,
            "default":"",
            "namedEnum":[
               {
                  "name":"Double Quotes (\")",
                  "value":"\""
               },
               {
                  "name":"Null Character (\u0000)",
                  "value":"\u0000"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"escape",
            "title":"Escape Character",
            "description":"Select your Escape character",
            "type":"string",
            "isRequired":false,
            "default":"\\",
            "namedEnum":[
               {
                  "name":"Back Slash (\\)",
                  "value":"\\"
               },
               {
                  "name":"Single Quote (')",
                  "value":"'"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"emptyValue",
            "title":"Empty Value",
            "description":"Select the output value of blank fields",
            "type":"string",
            "isRequired":false,
            "default":"",
            "namedEnum":[
               {
                  "name":"Empty String",
                  "value":""
               },
               {
                  "name":"\"\"",
                  "value":"\"\""
               },
               {
                  "name":"null",
                  "value":"null"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"nullValue",
            "title":"Null Value",
            "description":"Select the output value of 'null' fields",
            "type":"string",
            "isRequired":false,
            "default":"null",
            "namedEnum":[
               {
                  "name":"Empty String",
                  "value":""
               },
               {
                  "name":"\"\"",
                  "value":"\"\""
               },
               {
                  "name":"null",
                  "value":"null"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ],
      "isRequired":false,
      "readOnly":false,
      "hidden":false
   }
]
```

Hieronder ziet u het resulterende UI-scherm op basis van de bovenstaande configuratie. Wanneer de gebruiker het bestandstype CSV selecteert, worden aanvullende opties voor bestandsindeling die verwijzen naar het CSV-bestandstype weergegeven in de gebruikersinterface.

![ het registreren van het scherm die de voorwaardelijke dossier het formatteren optie voor Csv- dossiers tonen.](../../assets/functionality/destination-configuration/customer-data-fields-conditional.gif)

## Toegang tot getemplatificeerde gegevensvelden van klanten {#accessing-templatized-fields}

Wanneer uw bestemming gebruikersinvoer vereist, moet u een selectie van gebieden van klantengegevens aan uw gebruikers verstrekken, die zij door de UI van het Platform kunnen invullen. Dan, moet u uw bestemmingsserver vormen om de gebruikersinput van de gebieden van de klantengegevens correct te lezen. Dit wordt gedaan door templatized gebieden.

Sjabloonvelden gebruiken de indeling `{{customerData.fieldName}}` , waarbij `fieldName` de naam is van het gegevensveld van de klant waaruit u informatie leest. Alle sjabloongegevensvelden van klanten worden voorafgegaan door `customerData.` en ingesloten door dubbele accolades `{{ }}` .

Bijvoorbeeld, denken wij de volgende Amazon S3 bestemmingsconfiguratie:

```json
"customerDataFields":[
   {
      "name":"bucketName",
      "title":"Enter the name of your Amazon S3 bucket",
      "description":"Amazon S3 bucket name",
      "type":"string",
      "isRequired":true,
      "pattern":"(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
      "readOnly":false,
      "hidden":false
   },
   {
      "name":"path",
      "title":"Enter the path to your S3 bucket folder",
      "description":"Enter the path to your S3 bucket folder",
      "type":"string",
      "isRequired":true,
      "pattern":"^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
      "readOnly":false,
      "hidden":false
   }
]
```

Deze configuratie vraagt uw gebruikers om hun [!DNL Amazon S3] emmernaam en omslagweg in hun respectieve gebieden van klantengegevens in te gaan.

Voor Experience Platform om correct met [!DNL Amazon S3] te verbinden, moet uw bestemmingsserver worden gevormd om de waarden van deze twee gebieden van klantengegevens te lezen, zoals hieronder getoond:

```json
 "fileBasedS3Destination":{
      "bucketName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucketName}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
```

De sjabloonwaarden `{{customerData.bucketName}}` en `{{customerData.path}}` lezen de door de gebruiker opgegeven waarden zodat het Experience Platform verbinding kan maken met het doelplatform.

Voor meer informatie over hoe te om uw bestemmingsserver te vormen om gematigde gebieden te lezen, zie de documentatie op [ hard-gecodeerd tegenover templatized gebieden ](../destination-server/server-specs.md#templatized-fields).

## Volgende stappen {#next-steps}

Nadat u dit artikel hebt gelezen, hebt u beter inzicht in hoe u uw gebruikers kunt toestaan om informatie in de gebruikersinterface van het Experience Platform in te voeren via de gegevensvelden van de klant. U weet nu ook hoe te om het juiste gebied van klantengegevens voor uw gebruiksgeval te selecteren, en, klantengegevensgebieden te vormen, te ordenen en te groeperen in de UI van het Platform.

Raadpleeg de volgende artikelen voor meer informatie over de andere doelcomponenten:

* [Verificatie door klant](customer-authentication.md)
* [OAuth2-vergunning](oauth2-authorization.md)
* [UI-kenmerken](ui-attributes.md)
* [Schema-configuratie](schema-configuration.md)
* [Configuratie naamruimte voor identiteit](identity-namespace-configuration.md)
* [Ondersteunde toewijzingsconfiguraties](supported-mapping-configurations.md)
* [Levering bestemming](destination-delivery.md)
* [Configuratie van metagegevens voor publiek](audience-metadata-configuration.md)
* [Samenvoegingsbeleid](aggregation-policy.md)
* [Batchconfiguratie](batch-configuration.md)
* [Historische profielkwalificaties](historical-profile-qualifications.md)
