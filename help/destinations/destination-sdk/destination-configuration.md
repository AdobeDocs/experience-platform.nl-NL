---
description: Deze configuratie staat u toe om basisinformatie zoals uw bestemmingsnaam, categorie, beschrijving, embleem, en meer te wijzen. De montages in deze configuratie bepalen ook hoe de gebruikers van het Experience Platform aan uw bestemming voor authentiek verklaren, hoe het in het gebruikersinterface van het Experience Platform en de identiteiten verschijnt die naar uw bestemming kunnen worden uitgevoerd.
title: Streaming doelconfiguratieopties voor Destination SDK
exl-id: b7e4db67-2981-4f18-b202-3facda5c8f0b
source-git-commit: e3886cbcde76e37263d2fa23769fb9e96501edc4
workflow-type: tm+mt
source-wordcount: '1784'
ht-degree: 2%

---

# Streaming doelconfiguratie {#destination-configuration}

## Overzicht {#overview}

Deze configuratie staat u toe om essentiële informatie voor uw het stromen bestemming, zoals uw bestemmingsnaam, categorie, beschrijving, en meer te wijzen. De montages in deze configuratie bepalen ook hoe de gebruikers van het Experience Platform aan uw bestemming voor authentiek verklaren, hoe het in het gebruikersinterface van het Experience Platform en de identiteiten verschijnt die naar uw bestemming kunnen worden uitgevoerd.

Deze configuratie verbindt ook de andere configuraties die voor uw bestemming worden vereist aan het werk - bestemmingsserver en publieksmeta-gegevens - aan dit. Lees hoe u naar de twee configuraties in een [hieronder](./destination-configuration.md#connecting-all-configurations).

U kunt de in dit document beschreven functionaliteit configureren met de `/authoring/destinations` API-eindpunt. Lezen [API-eindpuntbewerkingen voor doelen](./destination-configuration-api.md) voor een volledige lijst van verrichtingen kunt u op het eindpunt uitvoeren.

## Voorbeeld van streamingconfiguratie {#example-configuration}

Dit is een voorbeeldconfiguratie van een fictieve streamingbestemming, Moviestar, die eindpunten heeft op vier locaties over de hele wereld. De bestemming behoort tot de categorie mobiele bestemmingen.

```json
{
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
               
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "schemaConfig":{
      "profileRequired":false,
      "segmentRequired":true,
      "identityRequired":true
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "splitUserById":true,
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":false,
            "groups":[
               {
                  "namespaces":[
                     "IDFA",
                     "GAID"
                  ]
               },
               {
                  "namespaces":[
                     "EMAIL"
                  ]
               }
            ]
         }
      }
   },
   "backfillHistoricalProfileData":true
}
```

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `name` | Tekenreeks | Geeft de titel van het doel in de catalogus met Experience Platforms aan. |
| `description` | Tekenreeks | Geef een beschrijving voor uw doelkaart op in de catalogus met Experience Platforms doelen. Doel voor niet meer dan 4-5 zinnen. |
| `status` | Tekenreeks | Geeft de levenscyclusstatus van de doelkaart aan. Accepteerde waarden zijn `TEST`, `PUBLISHED`, en `DELETED`. Gebruiken `TEST` wanneer u eerst uw bestemming vormt. |

{style=&quot;table-layout:auto&quot;}

## Verificatieconfiguraties van de klant {#customer-authentication-configurations}

Deze sectie in de bestemmingsconfiguratie produceert [Nieuwe bestemming configureren](/help/destinations/ui/connect-destination.md) pagina in het gebruikersinterface van het Experience Platform, waar de gebruikers Experience Platform met de rekeningen verbinden zij met uw bestemming hebben. Afhankelijk van welke verificatieoptie u aangeeft in het dialoogvenster `authType` wordt de pagina Experience Platform voor de gebruikers als volgt gegenereerd:

### Waardere verificatie

Wanneer u het dragerauthentificatietype vormt, worden de gebruikers vereist om het dragerteken in te voeren dat zij uit uw bestemming verkrijgen.

![UI-weergave met dragerverificatie](assets/bearer-authentication-ui.png)

### OAuth 2-verificatie

Gebruikers selecteren **[!UICONTROL Connect to destination]** om de OAuth 2 authentificatiestroom aan uw bestemming, zoals aangetoond in het voorbeeld hieronder voor de bestemming van het publiek van de Douane van Twitter teweeg te brengen. Voor gedetailleerde informatie bij het vormen van OAuth 2 authentificatie aan uw bestemmingshindpunt, lees specifiek [Destination SDK OAuth 2-verificatiepagina](./oauth2-authentication.md).

![UI-weergave met OAuth 2-verificatie](assets/oauth2-authentication-ui.png)

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `customerAuthenticationConfigurations` | Tekenreeks | Wijst op de configuratie die wordt gebruikt om de klanten van het Experience Platform aan uw server voor authentiek te verklaren. Zie `authType` hieronder voor geaccepteerde waarden. |
| `authType` | Tekenreeks | Accepteerde waarden voor streamingdoelen zijn:<ul><li>`BEARER`. Als uw bestemming dragerauthentificatie steunt, plaats `"authType":"Bearer"` en  `"authenticationRule":"CUSTOMER_AUTHENTICATION"` in de [leveringssectie bestemming](./destination-configuration.md).</li><li>`OAUTH2`. Als uw bestemming OAuth 2 authentificatie steunt, plaats `"authType":"OAUTH2"` en voeg de vereiste gebieden voor OAuth 2 toe, zoals aangetoond in [Destination SDK OAuth 2-verificatiepagina](./oauth2-authentication.md). Bovendien instellen `"authenticationRule":"CUSTOMER_AUTHENTICATION"` in de [leveringssectie bestemming](./destination-configuration.md).</li> |

{style=&quot;table-layout:auto&quot;}

## Gegevensvelden van de klant {#customer-data-fields}

Gebruik deze sectie om gebruikers te vragen aangepaste velden in te vullen, specifiek voor uw doel, wanneer u verbinding maakt met het doel in de gebruikersinterface van het Experience Platform. De configuratie wordt weerspiegeld in de authentificatiestroom zoals hieronder getoond:

![Aangepaste veldverificatiestroom](./assets/custom-field-authentication-flow.png)

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `name` | Tekenreeks | Geef een naam op voor het aangepaste veld dat u introduceert. |
| `type` | Tekenreeks | Hiermee geeft u aan welk type aangepast veld u wilt gebruiken. Accepteerde waarden zijn `string`, `object`, `integer`. |
| `title` | Tekenreeks | Hiermee wordt de naam van het veld aangegeven, zoals deze wordt weergegeven door klanten in de gebruikersinterface van het Experience Platform. |
| `description` | Tekenreeks | Geef een beschrijving op voor het aangepaste veld. |
| `isRequired` | Boolean | Geeft aan of dit veld vereist is in de workflow voor doelinstellingen. |
| `enum` | Tekenreeks | Hiermee geeft u het aangepaste veld weer als een vervolgkeuzemenu en geeft u de opties weer die beschikbaar zijn voor de gebruiker. |
| `pattern` | Tekenreeks | Hiermee wordt, indien nodig, een patroon voor het aangepaste veld afgedwongen. Gebruik reguliere expressies om een patroon af te dwingen. Als uw klant-id&#39;s bijvoorbeeld geen cijfers of onderstrepingstekens bevatten, voert u `^[A-Za-z]+$` op dit gebied. |

{style=&quot;table-layout:auto&quot;}

## UI-kenmerken {#ui-attributes}

Deze sectie verwijst naar de elementen UI in de configuratie hierboven die Adobe voor uw bestemming in het gebruikersinterface van Adobe Experience Platform zou moeten gebruiken. Zie hieronder:

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `documentationLink` | Tekenreeks | Verwijst naar de documentatiepagina in [Doelcatalogus](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) voor uw bestemming. Gebruiken `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, waarbij `YOURDESTINATION` is de naam van uw bestemming. Voor een bestemming genoemd Moviestar, zou u gebruiken `http://www.adobe.com/go/destinations-moviestar-en` |
| `category` | Tekenreeks | Verwijst naar de rubriek die aan je bestemming in Adobe Experience Platform is toegewezen. Lees voor meer informatie [Doelcategorieën](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html). Gebruik een van de volgende waarden: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `connectionType` | Tekenreeks | `Server-to-server` is momenteel de enige beschikbare optie. |
| `frequency` | Tekenreeks | Verwijst naar het type gegevens dat door de bestemming wordt gesteund. Ondersteunde waarden: <ul><li>`Streaming`</li><li>`Batch`</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Schemaconfiguratie in de toewijzingsstap {#schema-configuration}

![Toewijzingsstap inschakelen](./assets/enable-mapping-step.png)

Gebruik de parameters in `schemaConfig` om de toewijzingsstap van de workflow voor doelactivering in te schakelen. Door de hieronder beschreven parameters te gebruiken, kunt u bepalen als de gebruikers van het Experience Platform profielattributen en/of identiteiten aan het gewenste schema op de kant van uw bestemming kunnen in kaart brengen.

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `profileFields` | Array | *Niet weergegeven in bovenstaande voorbeeldconfiguratie.* Wanneer u vooraf gedefinieerde `profileFields`, hebben de gebruikers van het Experience Platform de optie om de attributen van het Platform aan de vooraf bepaalde attributen op de kant van uw bestemming in kaart te brengen. |
| `profileRequired` | Boolean | Gebruiken `true` als de gebruikers profielattributen van Experience Platform aan douanekenmerken op de kant van uw bestemming zouden moeten kunnen in kaart brengen, zoals aangetoond in de voorbeeldconfiguratie hierboven. |
| `segmentRequired` | Boolean | Altijd gebruiken `segmentRequired:true`. |
| `identityRequired` | Boolean | Gebruiken `true` als gebruikers naamruimten van het Experience Platform aan uw gewenste schema moeten kunnen toewijzen. |

{style=&quot;table-layout:auto&quot;}


## Identiteiten en kenmerken {#identities-and-attributes}

De parameters in deze sectie bepalen welke identiteiten uw bestemming goedkeurt. Deze configuratie vult ook de doelidentiteiten en -kenmerken in de [toewijzingsstap](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) van de gebruikersinterface van het Experience Platform, waar de gebruikers identiteiten en attributen van hun schema&#39;s XDM aan het schema in uw bestemming in kaart brengen.

U moet aangeven welke [!DNL Platform] id&#39;s die klanten kunnen exporteren naar uw bestemming. Enkele voorbeelden zijn [!DNL Experience Cloud ID], gehashte e-mail, apparaat-id ([!DNL IDFA], [!DNL GAID]). Deze waarden zijn [!DNL Platform] identiteitsnaamruimten die klanten vanaf uw bestemming kunnen toewijzen aan naamruimten. U kunt ook aangeven of klanten aangepaste naamruimten kunnen toewijzen aan identiteiten die door uw doel worden ondersteund.

Naamruimten vereisen geen 1-op-1-overeenkomst tussen [!DNL Platform] en uw bestemming.
Klanten kunnen bijvoorbeeld een [!DNL Platform] [!DNL IDFA] naamruimte naar een [!DNL IDFA] naamruimte vanaf uw bestemming, of ze kunnen hetzelfde toewijzen [!DNL Platform] [!DNL IDFA] naamruimte naar een [!DNL Customer ID] naamruimte in uw doel.

Lees meer in de [Overzicht van naamruimte van id](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=nl).

![Doelidentiteiten renderen in de gebruikersinterface](./assets/target-identities-ui.png)

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `acceptsAttributes` | Boolean | Hiermee geeft u aan of uw doel standaardprofielkenmerken accepteert. Gewoonlijk, worden deze attributen benadrukt in de documentatie van partners. |
| `acceptsCustomNamespaces` | Boolean | Geeft aan of klanten aangepaste naamruimten kunnen instellen op uw bestemming. |
| `transformation` | Tekenreeks | *Niet weergegeven in voorbeeldconfiguratie*. Wordt bijvoorbeeld gebruikt als de [!DNL Platform] de klant heeft onbewerkte e-mailadressen als attribuut en uw platform accepteert alleen gehashte e-mailadressen. In dit object kunt u de transformatie uitvoeren die moet worden toegepast (de e-mail bijvoorbeeld omzetten in kleine letters en vervolgens hash). Zie voor een voorbeeld `requiredTransformation` in de [API-naslaggids voor doelconfiguratie](./destination-configuration-api.md#update). |
| `acceptedGlobalNamespaces` | - | Wordt gebruikt voor gevallen waarin uw platform accepteert [standaardnaamruimten](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) (bijvoorbeeld IDFA), zodat u gebruikers van het Platform kunt beperken tot het selecteren van deze naamruimten. |

{style=&quot;table-layout:auto&quot;}

## Levering bestemming {#destination-delivery}

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `authenticationRule` | Tekenreeks | Geeft aan hoe [!DNL Platform] klanten verbinden met uw bestemming. Accepteerde waarden zijn `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Gebruiken `CUSTOMER_AUTHENTICATION` als de klanten van het Platform zich in uw systeem via een gebruikersbenaming en een wachtwoord, een dragerteken, of een andere methode van authentificatie aanmelden. U kunt deze optie bijvoorbeeld selecteren als u `authType: OAUTH2` of `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> Gebruiken `PLATFORM_AUTHENTICATION` als er een globaal authentificatiesysteem tussen Adobe en uw bestemming en is [!DNL Platform] de klant te hoeven om geen authentificatiegeloofsbrieven te verstrekken om met uw bestemming te verbinden. In dit geval moet u een object credentials maken met de opdracht [Credentials](./credentials-configuration-api.md) configuratie. </li><li>Gebruiken `NONE` als geen authentificatie wordt vereist om gegevens naar uw bestemmingsplatform te verzenden. </li></ul> |
| `destinationServerId` | Tekenreeks | De `instanceId` van de [doelserverconfiguratie](./destination-server-api.md) gebruikt voor deze bestemming. |

{style=&quot;table-layout:auto&quot;}

## Configuratie segmenttoewijzing {#segment-mapping}

![Sectie voor configuratie van segmenttoewijzing](./assets/segment-mapping-configuration.png)

Deze sectie van de bestemmingsconfiguratie heeft op hoe segmentmeta-gegevens zoals segmentnamen of IDs tussen Experience Platform en uw bestemming zouden moeten worden gedeeld.

Via de `audienceTemplateId`Deze sectie koppelt deze configuratie ook aan de [doelmetagegevensconfiguratie](./audience-metadata-management.md).

De parameters die in de bovenstaande configuratie worden getoond, worden beschreven in de [API-naslaggids voor doelen](./destination-configuration-api.md).

## Samenvoegingsbeleid {#aggregation}

![Samenvoegingsbeleid in het configuratiesjabloon](./assets/aggregation-configuration.png)

Deze sectie staat u toe om het samenvoegingsbeleid te plaatsen dat het Experience Platform zou moeten gebruiken wanneer het uitvoeren van gegevens naar uw bestemming.

Een samenvoegingsbeleid bepaalt hoe de uitgevoerde profielen in de gegevensuitvoer worden gecombineerd. Beschikbare opties zijn:
* Beste inspanningsaggregatie
* Configureerbare samenvoeging (weergegeven in de bovenstaande configuratie)

De sectie lezen op [gebruiken van sjablonen](./message-format.md#using-templating) en de [samenvoegingssleutelvoorbeelden](./message-format.md#template-aggregation-key) om te begrijpen hoe te om het samenvoegingsbeleid in uw malplaatje van de berichttransformatie te omvatten dat op uw geselecteerd samenvoegingsbeleid wordt gebaseerd.

### Beste inspanningsaggregatie {#best-effort-aggregation}

>[!TIP]
>
>Gebruik deze optie als uw API-eindpunt minder dan 100 profielen per API-aanroep accepteert.

Deze optie werkt het best voor bestemmingen die minder profielen per verzoek verkiezen en eerder meer verzoeken met minder gegevens dan minder verzoeken met meer gegevens zouden nemen.

Gebruik de `maxUsersPerRequest` om het maximumaantal profielen te specificeren dat uw bestemming in een verzoek kan nemen.

### Configureerbare samenvoeging {#configurable-aggregation}

Deze optie werkt het best als u eerder grote partijen, met duizenden profielen op de zelfde vraag zou nemen. Met deze optie kunt u ook de geëxporteerde profielen samenvoegen op basis van complexe aggregatieregels.

Met deze optie kunt u:
* Stel de maximale tijd en het maximale aantal profielen in dat moet worden samengevoegd voordat een API-aanroep naar uw bestemming wordt uitgevoerd.
* De geëxporteerde profielen bundelen die aan de bestemming zijn toegewezen op basis van:
   * Segment-id;
   * segmentstatus;
   * Identiteit of groepen van identiteiten.

>[!NOTE]
>
>Wanneer het gebruiken van de configureerbare samenvoegingsoptie voor uw bestemming, houd rekening met de minimum en maximumwaarden die u voor de twee parameters kunt gebruiken `maxBatchAgeInSecs` (minimaal 1,800 en maximaal 3,600) en `maxNumEventsInBatch` (minimaal 1 000, maximaal 10 000).

Voor gedetailleerde uitleg van de aggregatieparameters raadpleegt u de [API-eindpuntbewerkingen voor doelen](./destination-configuration-api.md) referentiepagina, waar elke parameter wordt beschreven.

## Historische profielkwalificaties {#profile-backfill}

U kunt de `backfillHistoricalProfileData` parameter in de bestemmingsconfiguratie om te bepalen als de historische profielkwalificaties naar uw bestemming zouden moeten worden uitgevoerd.

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `backfillHistoricalProfileData` | Boolean | Bepaalt of historische profielgegevens worden geëxporteerd wanneer segmenten worden geactiveerd naar de bestemming. <br> <ul><li> `true`: [!DNL Platform] verzendt de historische gebruikersprofielen die voor het segment kwalificeren alvorens het segment wordt geactiveerd. </li><li> `false`: [!DNL Platform] omvat alleen gebruikersprofielen die in aanmerking komen voor het segment nadat het segment is geactiveerd. </li></ul> |

## Hoe deze configuratie alle noodzakelijke informatie voor uw bestemming verbindt {#connecting-all-configurations}

Sommige van uw bestemmingsmontages moeten door worden gevormd [doelserver](./server-and-template-configuration.md) of de [doelmetagegevensconfiguratie](./audience-metadata-management.md). De bestemmingsconfiguratie die hier wordt beschreven verbindt al deze montages door de twee andere configuraties als volgt van verwijzingen te voorzien:

* Gebruik de `destinationServerId` om naar de bestemmingsserver en malplaatjeconfiguratie te verwijzen opstelling voor uw bestemming.
* Gebruik de `audienceMetadataId` om naar de configuratie van publieksmeta-gegevens te verwijzen opstelling voor uw bestemming.