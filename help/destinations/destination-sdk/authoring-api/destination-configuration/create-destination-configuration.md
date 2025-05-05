---
description: Leer hoe u een API-aanroep kunt structureren om een doelconfiguratie te maken via Adobe Experience Platform Destination SDK.
title: Een doelconfiguratie maken
exl-id: aae4aaa8-1dd0-4041-a86c-5c86f04d7d13
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---

# Een doelconfiguratie maken

Deze pagina illustreert de API aanvraag en lading die u kunt gebruiken om uw eigen bestemmingsconfiguratie tot stand te brengen, gebruikend het `/authoring/destinations` API eindpunt.

Voor een gedetailleerde beschrijving van de mogelijkheden die u door dit eindpunt kunt vormen, lees de volgende artikelen:

* [Configuratie van klantverificatie](../../functionality/destination-configuration/customer-authentication.md)
* [OAuth2-vergunning](../../functionality/destination-configuration/oauth2-authorization.md)
* [Gegevensvelden van de klant](../../functionality/destination-configuration/customer-data-fields.md)
* [UI-kenmerken](../../functionality/destination-configuration/ui-attributes.md)
* [Schema-configuratie](../../functionality/destination-configuration/schema-configuration.md)
* [Configuratie naamruimte voor identiteit](../../functionality/destination-configuration/identity-namespace-configuration.md)
* [Levering bestemming](../../functionality/destination-configuration/destination-delivery.md)
* [Configuratie van metagegevens voor publiek](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [Configuratie van metagegevens voor publiek](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [Samenvoegingsbeleid](../../functionality/destination-configuration/aggregation-policy.md)
* [Batchconfiguratie](../../functionality/destination-configuration/batch-configuration.md)
* [Historische profielkwalificaties](../../functionality/destination-configuration/historical-profile-qualifications.md)

>[!IMPORTANT]
>
>Alle parameternamen en waarden die door Destination SDK worden gesteund zijn **gevoelig geval**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Aan de slag met API-bewerkingen voor doelconfiguratie {#get-started}

Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](../../getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings authoring en vereiste kopballen te verkrijgen.

## Een doelconfiguratie maken {#create}

U kunt een nieuwe bestemmingsconfiguratie tot stand brengen door een POST- verzoek aan het `/authoring/destinations` eindpunt te doen.

>[!TIP]
>
>**API eindpunt**: `platform.adobe.io/data/core/activation/authoring/destinations`

**API formaat**

```http
POST /authoring/destinations
```

Het volgende verzoek leidt tot een nieuwe [!DNL Amazon S3] bestemmingsconfiguratie, die door de parameters wordt gevormd die in de lading worden verstrekt. De nuttige lading omvat hieronder alle parameters voor op dossier-gebaseerde bestemmingen die door het `/authoring/destinations` eindpunt worden goedgekeurd.

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
| `name` | String | Hiermee geeft u de titel van het doel in de Experience Platform-catalogus aan. |
| `description` | String | Geef een beschrijving op die Adobe in de Experience Platform-doelcatalogus voor uw doelkaart zal gebruiken. Doel voor niet meer dan 4-5 zinnen. ![ het beeld van Experience Platform UI die de bestemmingsbeschrijving toont.](../../assets/authoring-api/destination-configuration/destination-description.png " beschrijving van de Bestemming "){width="100" zoomable="yes"} |
| `status` | String | Geeft de levenscyclusstatus van de doelkaart aan. Accepteerde waarden zijn `TEST` , `PUBLISHED` en `DELETED` . Gebruik `TEST` wanneer u eerst uw bestemming vormt. |
| `customerAuthenticationConfigurations.authType` | String | Geeft de configuratie aan die wordt gebruikt om Experience Platform-klanten te verifiëren bij uw doelserver. Zie [ configuratie van de klantenauthentificatie ](../../functionality/destination-configuration/customer-authentication.md) voor gedetailleerde informatie over de gesteunde authentificatietypen. |
| `customerDataFields.name` | String | Geef een naam op voor het aangepaste veld dat u introduceert. <br/><br/> zie {de gegevensgebieden van 1} Klant [&#128279;](../../functionality/destination-configuration/customer-data-fields.md) voor gedetailleerde informatie over deze montages.  ![ beeld UI van Experience Platform die de gebieden van klantengegevens toont.](../../assets/authoring-api/destination-configuration/customer-data-fields.png " het gegevensgebied van de Klant "){width="100" zoomable="yes"} |
| `customerDataFields.type` | String | Hiermee geeft u aan welk type aangepast veld u wilt gebruiken. Accepteerde waarden zijn `string` , `object` , `integer` . <br/><br/> zie {de gegevensgebieden van 1} Klant [&#128279;](../../functionality/destination-configuration/customer-data-fields.md) voor gedetailleerde informatie over deze montages. |
| `customerDataFields.title` | String | Hiermee wordt de naam van het veld aangegeven, zoals deze wordt weergegeven door klanten in de gebruikersinterface van Experience Platform. <br/><br/> zie {de gegevensgebieden van 1} Klant [&#128279;](../../functionality/destination-configuration/customer-data-fields.md) voor gedetailleerde informatie over deze montages. |
| `customerDataFields.description` | String | Geef een beschrijving op voor het aangepaste veld. Zie {de gegevensgebieden van 0} Klant [&#128279;](../../functionality/destination-configuration/customer-data-fields.md) voor gedetailleerde informatie over deze montages. |
| `customerDataFields.isRequired` | Boolean | Geeft aan of dit veld vereist is in de workflow voor doelinstellingen. <br/><br/> zie {de gegevensgebieden van 1} Klant [&#128279;](../../functionality/destination-configuration/customer-data-fields.md) voor gedetailleerde informatie over deze montages. |
| `customerDataFields.enum` | String | Hiermee geeft u het aangepaste veld weer als een vervolgkeuzemenu en geeft u de opties weer die beschikbaar zijn voor de gebruiker. <br/><br/> zie {de gegevensgebieden van 1} Klant [&#128279;](../../functionality/destination-configuration/customer-data-fields.md) voor gedetailleerde informatie over deze montages. |
| `customerDataFields.default` | String | Definieert de standaardwaarde in de lijst `enum` . |
| `customerDataFields.pattern` | String | Hiermee wordt, indien nodig, een patroon voor het aangepaste veld afgedwongen. Gebruik reguliere expressies om een patroon af te dwingen. Als uw klant-id&#39;s bijvoorbeeld geen cijfers of onderstrepingstekens bevatten, voert u `^[A-Za-z]+$` in dit veld in. <br/><br/> zie {de gegevensgebieden van 1} Klant [&#128279;](../../functionality/destination-configuration/customer-data-fields.md) voor gedetailleerde informatie over deze montages. |
| `uiAttributes.documentationLink` | String | Verwijst naar de documentatiepagina in de [ Catalogus van Doelen ](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html#catalog) voor uw bestemming. Gebruik `https://www.adobe.com/go/destinations-YOURDESTINATION-en` , waarbij `YOURDESTINATION` de naam van het doel is. Voor een doel met de naam Moviestar gebruikt u `https://www.adobe.com/go/destinations-moviestar-en` . Deze koppeling werkt alleen nadat Adobe uw doel live heeft ingesteld en de documentatie is gepubliceerd. <br/><br/> zie [ attributen UI ](../../functionality/destination-configuration/ui-attributes.md) voor gedetailleerde informatie over deze montages. ![ het beeld van Experience Platform UI die de documentatieverbinding toont.](../../assets/authoring-api/destination-configuration/documentation-url.png " Documentatie URL "){width="100" zoomable="yes"} |
| `uiAttributes.category` | String | Verwijst naar de rubriek die aan je bestemming in Adobe Experience Platform is toegewezen. Voor meer informatie, lees [ Categorieën van de Bestemming ](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html#destination-categories). Gebruik een van de volgende waarden: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments` . <br/><br/> zie [ attributen UI ](../../functionality/destination-configuration/ui-attributes.md) voor gedetailleerde informatie over deze montages. |
| `uiAttributes.connectionType` | String | Het type verbinding, afhankelijk van het doel. Ondersteunde waarden: <ul><li>`Server-to-server`</li><li>`Cloud storage`</li><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li><li>`DLZ`</li></ul> |
| `uiAttributes.frequency` | String | Verwijst naar het type gegevens die worden uitgevoerd door de bestemming wordt gesteund. Stel dit in op `Streaming` voor API-gebaseerde integratie of op `Batch` wanneer u bestanden exporteert naar uw doelen. |
| `identityNamespaces.externalId.acceptsAttributes` | Boolean | Geeft aan of klanten standaardprofielkenmerken kunnen toewijzen aan de identiteit die u configureert. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Boolean | Wijst erop als de klanten identiteiten kunnen in kaart brengen die tot [ douane namespaces ](/help/identity-service/features/namespaces.md#manage-namespaces) behoren aan de identiteit die u vormt. |
| `identityNamespaces.externalId.transformation` | String | _niet getoond in voorbeeldconfiguratie_. Wordt bijvoorbeeld gebruikt wanneer de klant van [!DNL Experience Platform] normale e-mailadressen heeft als attribuut en uw platform alleen gehashte e-mails accepteert. Hier geeft u de transformatie op die moet worden toegepast (zet de e-mail bijvoorbeeld om in kleine letters en vervolgens in de hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | Wijst op welke [ standaardidentiteit namespaces ](/help/identity-service/features/namespaces.md#standard) (bijvoorbeeld, IDFA) klanten aan de identiteit kunnen in kaart brengen die u vormt. <br> Wanneer u `acceptedGlobalNamespaces` gebruikt, kunt u `"requiredTransformation":"sha256(lower($))"` gebruiken om e-mailadressen of telefoonnummers in kleine letters te plaatsen en te hashen. |
| `destinationDelivery.authenticationRule` | String | Geeft aan hoe [!DNL Experience Platform] -klanten verbinding maken met uw doel. Accepteerde waarden zijn `CUSTOMER_AUTHENTICATION` , `PLATFORM_AUTHENTICATION` , `NONE` . <br> <ul><li>Gebruik `CUSTOMER_AUTHENTICATION` als Experience Platform-klanten zich via een gebruikersnaam en wachtwoord, een token aan de gebruiker of een andere verificatiemethode aanmelden op uw systeem. U kunt deze optie bijvoorbeeld ook selecteren als u `authType: OAUTH2` of `authType:BEARER` in `customerAuthenticationConfigurations` hebt geselecteerd. </li><li> Gebruik `PLATFORM_AUTHENTICATION` als er een wereldwijd verificatiesysteem is tussen Adobe en uw bestemming en de klant van [!DNL Experience Platform] geen verificatiereferenties hoeft op te geven om verbinding te maken met uw bestemming. In dit geval, moet u een geloofsbrieven tot stand brengen voorwerp gebruikend de [ geloofsbrieven API ](../../credentials-api/create-credential-configuration.md) configuratie. </li><li>Gebruik `NONE` als er geen verificatie vereist is om gegevens naar het doelplatform te verzenden. </li></ul> |
| `destinationDelivery.destinationServerId` | String | `instanceId` van het [ malplaatje van de bestemmingsserver ](../destination-server/create-destination-server.md) dat voor deze bestemming wordt gebruikt. |
| `backfillHistoricalProfileData` | Boolean | Bepaalt of historische profielgegevens worden geëxporteerd wanneer het publiek wordt geactiveerd naar het doel. Stel dit altijd in op `true` . |
| `segmentMappingConfig.mapUserInput` | Boolean | Controls whether the publiek mapping ID in the destination activation workflow is input by user. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Boolean | Controls whether the publiek mapping ID in the destination activation workflow is the Experience Platform publiek ID. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Boolean | Bepaalt of de publiekstoewijzings-id in de workflow voor doelactivering de Experience Platform-publieksnaam is. |
| `segmentMappingConfig.audienceTemplateId` | String | `instanceId` van het [ malplaatje van publieksmeta-gegevens ](../../metadata-api/create-audience-template.md) dat voor deze bestemming wordt gebruikt. |
| `schemaConfig.profileFields` | Array | Wanneer u vooraf gedefinieerde `profileFields` toevoegt, zoals in de bovenstaande configuratie wordt getoond, kunnen gebruikers Experience Platform-kenmerken toewijzen aan de vooraf gedefinieerde kenmerken aan de zijde van uw bestemming. |
| `schemaConfig.profileRequired` | Boolean | Gebruik `true` als gebruikers in staat moeten zijn om profielkenmerken van Experience Platform toe te wijzen aan aangepaste kenmerken aan de zijde van uw bestemming, zoals in de bovenstaande voorbeeldconfiguratie wordt getoond. |
| `schemaConfig.segmentRequired` | Boolean | Altijd `segmentRequired:true` gebruiken. |
| `schemaConfig.identityRequired` | Boolean | Gebruik `true` als u gebruikers naamruimten van Experience Platform kunt toewijzen aan uw gewenste schema. |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde bestemmingsconfiguratie terug.

+++

## API-foutafhandeling

Destination SDK API-eindpunten volgen de algemene beginselen van Experience Platform API-foutberichten. Verwijs naar [ API statuscodes ](../../../../landing/troubleshooting.md#api-status-codes) en [ de fouten van de verzoekkopbal ](../../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van Experience Platform.

## Volgende stappen

Nadat u dit document hebt gelezen, weet u nu hoe u een nieuwe doelconfiguratie kunt maken via het API-eindpunt van Destination SDK `/authoring/destinations` .

Raadpleeg de volgende artikelen voor meer informatie over wat u met dit eindpunt kunt doen:

* [Een doelconfiguratie ophalen](retrieve-destination-configuration.md)
* [Een doelconfiguratie bijwerken](update-destination-configuration.md)
* [Een doelconfiguratie verwijderen](delete-destination-configuration.md)

Om te begrijpen waar dit eindpunt in het bestemmings auteursproces past, zie de volgende artikelen:

* [Destination SDK gebruiken om een streamingbestemming te configureren](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Destination SDK gebruiken om een bestandsgebaseerde bestemming te configureren](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)
