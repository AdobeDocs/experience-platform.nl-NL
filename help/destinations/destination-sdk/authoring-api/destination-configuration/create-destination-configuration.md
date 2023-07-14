---
description: Leer hoe te om een API vraag te structureren om een bestemmingsconfiguratie door Adobe Experience Platform Destination SDK tot stand te brengen.
title: Een doelconfiguratie maken
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 1%

---


# Een doelconfiguratie maken

Deze pagina illustreert de API aanvraag en lading die u kunt gebruiken om uw eigen bestemmingsconfiguratie tot stand te brengen, gebruikend `/authoring/destinations` API-eindpunt.

Voor een gedetailleerde beschrijving van de mogelijkheden die u door dit eindpunt kunt vormen, lees de volgende artikelen:

* [Configuratie van klantverificatie](../../functionality/destination-configuration/customer-authentication.md)
* [OAuth2-verificatie](../../functionality/destination-configuration/oauth2-authentication.md)
* [Gegevensvelden van de klant](../../functionality/destination-configuration/customer-data-fields.md)
* [UI-kenmerken](../../functionality/destination-configuration/ui-attributes.md)
* [Schema-configuratie](../../functionality/destination-configuration/schema-configuration.md)
* [Configuratie naamruimte identiteit](../../functionality/destination-configuration/identity-namespace-configuration.md)
* [Levering bestemming](../../functionality/destination-configuration/destination-delivery.md)
* [Configuratie van metagegevens voor publiek](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [Configuratie van metagegevens voor publiek](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [Samenvoegingsbeleid](../../functionality/destination-configuration/aggregation-policy.md)
* [Batchconfiguratie](../../functionality/destination-configuration/batch-configuration.md)
* [Historische profielkwalificaties](../../functionality/destination-configuration/historical-profile-qualifications.md)

>[!IMPORTANT]
>
>Alle parameternamen en -waarden die door Destination SDK worden ondersteund, zijn **hoofdlettergevoelig**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Aan de slag met API-bewerkingen voor doelconfiguratie {#get-started}

Controleer voordat je doorgaat de [gids Aan de slag](../../getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings creatie en vereiste kopballen te verkrijgen.

## Een doelconfiguratie maken {#create}

U kunt een nieuwe bestemmingsconfiguratie tot stand brengen door een verzoek van de POST aan `/authoring/destinations` eindpunt.

>[!TIP]
>
>**API-eindpunt**: `platform.adobe.io/data/core/activation/authoring/destinations`

**API-indeling**

```http
POST /authoring/destinations
```

Met de volgende aanvraag wordt een nieuwe [!DNL Amazon S3] bestemmingsconfiguratie, die door de parameters wordt gevormd die in de lading worden verstrekt. De hieronder vermelde lading omvat alle parameters voor op dossier-gebaseerde bestemmingen die door `/authoring/destinations` eindpunt.

U hoeft niet alle parameters aan uw API-aanroep toe te voegen en de laadbewerking kan worden aangepast aan uw API-vereisten.

+++verzoek

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
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
         "title":"Select a fileType",
         "description":"Select fileType",
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
         "EVERY_8_HOURS",
         "EVERY_12_HOURS",
         "ONCE"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00",
      "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      },
      "backfillHistoricalProfileData":true
   }
}'
```

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `name` | Tekenreeks | Geeft de titel van het doel in de catalogus met Experience Platforms aan. |
| `description` | Tekenreeks | Geef een beschrijving op die Adobe in de Experience Platform-doelcatalogus voor uw doelkaart zal gebruiken. Doel voor niet meer dan 4-5 zinnen. ![UI-afbeelding van Platform met de doelbeschrijving.](../../assets/authoring-api/destination-configuration/destination-description.png "Doelbeschrijving"){width="100" zoomable="yes"} |
| `status` | Tekenreeks | Geeft de levenscyclusstatus van de doelkaart aan. Accepteerde waarden zijn `TEST`, `PUBLISHED`, en `DELETED`. Gebruiken `TEST` wanneer u eerst uw bestemming vormt. |
| `customerAuthenticationConfigurations.authType` | Tekenreeks | Wijst op de configuratie die wordt gebruikt om de klanten van het Experience Platform aan uw bestemmingsserver voor authentiek te verklaren. Zie [klantverificatieconfiguratie](../../functionality/destination-configuration/customer-authentication.md) voor gedetailleerde informatie over de gesteunde authentificatietypen. |
| `customerDataFields.name` | Tekenreeks | Geef een naam op voor het aangepaste veld dat u introduceert. <br/><br/> Zie [Gegevensvelden van de klant](../../functionality/destination-configuration/customer-data-fields.md) voor gedetailleerde informatie over deze instellingen. ![UI-afbeelding van Platform met gegevensvelden van klanten.](../../assets/authoring-api/destination-configuration/customer-data-fields.png "Veld voor klantgegevens"){width="100" zoomable="yes"} |
| `customerDataFields.type` | Tekenreeks | Hiermee geeft u aan welk type aangepast veld u wilt gebruiken. Accepteerde waarden zijn `string`, `object`, `integer`. <br/><br/> Zie [Gegevensvelden van de klant](../../functionality/destination-configuration/customer-data-fields.md) voor gedetailleerde informatie over deze instellingen. |
| `customerDataFields.title` | Tekenreeks | Hiermee wordt de naam van het veld aangegeven, zoals deze wordt weergegeven door klanten in de gebruikersinterface van het Experience Platform. <br/><br/> Zie [Gegevensvelden van de klant](../../functionality/destination-configuration/customer-data-fields.md) voor gedetailleerde informatie over deze instellingen. |
| `customerDataFields.description` | Tekenreeks | Geef een beschrijving op voor het aangepaste veld. Zie [Gegevensvelden van de klant](../../functionality/destination-configuration/customer-data-fields.md) voor gedetailleerde informatie over deze instellingen. |
| `customerDataFields.isRequired` | Boolean | Geeft aan of dit veld vereist is in de workflow voor doelinstellingen. <br/><br/> Zie [Gegevensvelden van de klant](../../functionality/destination-configuration/customer-data-fields.md) voor gedetailleerde informatie over deze instellingen. |
| `customerDataFields.enum` | Tekenreeks | Hiermee geeft u het aangepaste veld weer als een vervolgkeuzemenu en geeft u de opties weer die beschikbaar zijn voor de gebruiker. <br/><br/> Zie [Gegevensvelden van de klant](../../functionality/destination-configuration/customer-data-fields.md) voor gedetailleerde informatie over deze instellingen. |
| `customerDataFields.default` | Tekenreeks | Definieert de standaardwaarde op basis van een `enum` lijst. |
| `customerDataFields.pattern` | Tekenreeks | Hiermee wordt, indien nodig, een patroon voor het aangepaste veld afgedwongen. Gebruik reguliere expressies om een patroon af te dwingen. Als uw klant-id&#39;s bijvoorbeeld geen cijfers of onderstrepingstekens bevatten, voert u `^[A-Za-z]+$` op dit gebied. <br/><br/> Zie [Gegevensvelden van de klant](../../functionality/destination-configuration/customer-data-fields.md) voor gedetailleerde informatie over deze instellingen. |
| `uiAttributes.documentationLink` | Tekenreeks | Verwijst naar de documentatiepagina in [Doelcatalogus](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) voor uw bestemming. Gebruiken `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, waarbij `YOURDESTINATION` is de naam van uw bestemming. Voor een bestemming genoemd Moviestar, zou u gebruiken `https://www.adobe.com/go/destinations-moviestar-en`. Merk op dat deze verbinding slechts werkt nadat Adobe uw bestemming live plaatst en de documentatie wordt gepubliceerd. <br/><br/> Zie [UI-kenmerken](../../functionality/destination-configuration/ui-attributes.md) voor gedetailleerde informatie over deze instellingen. ![Platform-UI-afbeelding met de documentatiekoppeling.](../../assets/authoring-api/destination-configuration/documentation-url.png "Documentatie-URL"){width="100" zoomable="yes"} |
| `uiAttributes.category` | Tekenreeks | Verwijst naar de rubriek die aan je bestemming in Adobe Experience Platform is toegewezen. Lees voor meer informatie [Doelcategorieën](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). Gebruik een van de volgende waarden: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. <br/><br/> Zie [UI-kenmerken](../../functionality/destination-configuration/ui-attributes.md) voor gedetailleerde informatie over deze instellingen. |
| `uiAttributes.connectionType` | Tekenreeks | Het type verbinding, afhankelijk van het doel. Ondersteunde waarden: <ul><li>`Server-to-server`</li><li>`Cloud storage`</li><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li><li>`DLZ`</li></ul> |
| `uiAttributes.frequency` | Tekenreeks | Verwijst naar het type gegevens dat door de bestemming wordt gesteund. Instellen op `Streaming` voor API-gebaseerde integratie, of `Batch` wanneer u bestanden exporteert naar uw doelen. |
| `identityNamespaces.externalId.acceptsAttributes` | Boolean | Geeft aan of klanten standaardprofielkenmerken kunnen toewijzen aan de identiteit die u configureert. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Boolean | Geeft aan of klanten identiteiten kunnen toewijzen die horen bij [aangepaste naamruimten](/help/identity-service/namespaces.md#manage-namespaces) aan de identiteit die u vormt. |
| `identityNamespaces.externalId.transformation` | Tekenreeks | _Niet weergegeven in voorbeeldconfiguratie_. Wordt bijvoorbeeld gebruikt als de [!DNL Platform] de klant heeft onbewerkte e-mailadressen als attribuut en uw platform accepteert alleen gehashte e-mailadressen. Hier geeft u de transformatie op die moet worden toegepast (zet de e-mail bijvoorbeeld om in kleine letters en vervolgens in de hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | Geeft aan welke [standaardnaamruimten](/help/identity-service/namespaces.md#standard) (bijvoorbeeld, IDFA) klanten kunnen aan de identiteit in kaart brengen die u vormt. <br> Wanneer u `acceptedGlobalNamespaces`kunt u `"requiredTransformation":"sha256(lower($))"` om e-mailadressen of telefoonnummers in kleine letters en te hashen. |
| `destinationDelivery.authenticationRule` | Tekenreeks | Geeft aan hoe [!DNL Platform] klanten verbinden met uw bestemming. Accepteerde waarden zijn `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Gebruiken `CUSTOMER_AUTHENTICATION` als de klanten van het Platform zich in uw systeem via een gebruikersbenaming en een wachtwoord, een dragerteken, of een andere methode van authentificatie aanmelden. U kunt deze optie bijvoorbeeld selecteren als u `authType: OAUTH2` of `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> Gebruiken `PLATFORM_AUTHENTICATION` als er een globaal authentificatiesysteem tussen Adobe en uw bestemming en is [!DNL Platform] de klant te hoeven om geen authentificatiegeloofsbrieven te verstrekken om met uw bestemming te verbinden. In dit geval moet u een object credentials maken met de opdracht [aanmeldAPI](../../credentials-api/create-credential-configuration.md) configuratie. </li><li>Gebruiken `NONE` als geen authentificatie wordt vereist om gegevens naar uw bestemmingsplatform te verzenden. </li></ul> |
| `destinationDelivery.destinationServerId` | Tekenreeks | De `instanceId` van de [doelserversjabloon](../destination-server/create-destination-server.md) gebruikt voor deze bestemming. |
| `backfillHistoricalProfileData` | Boolean | Bepaalt of historische profielgegevens worden geëxporteerd wanneer het publiek wordt geactiveerd naar het doel. Altijd instellen op `true`. |
| `segmentMappingConfig.mapUserInput` | Boolean | Controls whether the publiek mapping ID in the destination activation workflow is input by user. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Boolean | Bepaalt of de publiekstoewijzings-id in de workflow voor doelactivering de Experience Platform-gebruikers-id is. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Boolean | Bepaalt of de publiekstoewijzings-id in de workflow voor doelactivering de publieksnaam van het Experience Platform is. |
| `segmentMappingConfig.audienceTemplateId` | Boolean | De `instanceId` van de [sjabloon voor doelmetagegevens](../../metadata-api/create-audience-template.md) gebruikt voor deze bestemming. |
| `schemaConfig.profileFields` | Array | Wanneer u vooraf gedefinieerde `profileFields` zoals aangetoond in de configuratie hierboven, zullen de gebruikers de optie hebben om de attributen van het Experience Platform aan de vooraf bepaalde attributen op de kant van uw bestemming in kaart te brengen. |
| `schemaConfig.profileRequired` | Boolean | Gebruiken `true` als de gebruikers profielattributen van Experience Platform aan douanekenmerken op de kant van uw bestemming zouden moeten kunnen in kaart brengen, zoals aangetoond in de voorbeeldconfiguratie hierboven. |
| `schemaConfig.segmentRequired` | Boolean | Altijd gebruiken `segmentRequired:true`. |
| `schemaConfig.identityRequired` | Boolean | Gebruiken `true` als u gebruikers identiteitsnaamruimten van Experience Platform aan uw gewenste schema zou moeten kunnen in kaart brengen. |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde bestemmingsconfiguratie terug.

+++

## API-foutafhandeling

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Zie [API-statuscodes](../../../../landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](../../../../landing/troubleshooting.md#request-header-errors) in de gids voor het oplossen van problemen met Platforms.

## Volgende stappen

Nadat u dit document hebt gelezen, weet u nu hoe u een nieuwe doelconfiguratie kunt maken via de Destination SDK `/authoring/destinations` API-eindpunt.

Raadpleeg de volgende artikelen voor meer informatie over wat u met dit eindpunt kunt doen:

* [Een doelconfiguratie ophalen](retrieve-destination-configuration.md)
* [Een doelconfiguratie bijwerken](update-destination-configuration.md)
* [Een doelconfiguratie verwijderen](delete-destination-configuration.md)

Om te begrijpen waar dit eindpunt in het bestemmings auteursproces past, zie de volgende artikelen:

* [Gebruik Destination SDK om een streamingbestemming te configureren](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Gebruik Destination SDK om een op een bestand gebaseerde bestemming te configureren](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)
