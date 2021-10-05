---
description: Deze configuratie staat u toe om basisinformatie zoals uw bestemmingsnaam, categorie, beschrijving, embleem, en meer te wijzen. De montages in deze configuratie bepalen ook hoe de gebruikers van het Experience Platform aan uw bestemming voor authentiek verklaren, hoe het in het gebruikersinterface van het Experience Platform en de identiteiten verschijnt die naar uw bestemming kunnen worden uitgevoerd.
title: Opties voor doelconfiguratie voor doel-SDK
exl-id: b7e4db67-2981-4f18-b202-3facda5c8f0b
source-git-commit: 32b61276f3fe81ffa82fec1debf335ea51020ccd
workflow-type: tm+mt
source-wordcount: '1549'
ht-degree: 2%

---

# Doelconfiguratie {#destination-configuration}

## Overzicht {#overview}

Deze configuratie staat u toe om basisinformatie zoals uw bestemmingsnaam, categorie, beschrijving, embleem, en meer te wijzen. De montages in deze configuratie bepalen ook hoe de gebruikers van het Experience Platform aan uw bestemming voor authentiek verklaren, hoe het in het gebruikersinterface van het Experience Platform en de identiteiten verschijnt die naar uw bestemming kunnen worden uitgevoerd.

U kunt de in dit document beschreven functionaliteit vormen door het `/authoring/destinations` API eindpunt te gebruiken. Lees [Doelen API eindpuntverrichtingen](./destination-configuration-api.md) voor een volledige lijst van verrichtingen u op het eindpunt kunt uitvoeren.

## Voorbeeldconfiguratie {#example-configuration}

Hieronder ziet u een voorbeeldconfiguratie voor een fictieve bestemming, Moviestar, die eindpunten heeft op vier locaties over de hele wereld. De bestemming behoort tot de categorie mobiele bestemmingen. In de volgende secties wordt uitgelegd hoe deze configuratie wordt samengesteld.

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
         "maxBatchAgeInSecs":0,
         "maxNumEventsInBatch":0,
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
   }
}
```

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `name` | Tekenreeks | Geeft de titel van het doel in de catalogus met Experience Platforms aan. |
| `description` | Tekenreeks | Geef een beschrijving op die Adobe in de Experience Platform-doelcatalogus voor uw doelkaart zal gebruiken. Doel voor niet meer dan 4-5 zinnen. |
| `status` | Tekenreeks | Geeft de levenscyclusstatus van de doelkaart aan. Accepteerde waarden zijn `TEST`, `PUBLISHED` en `DELETED`. Gebruik `TEST` wanneer u eerst uw bestemming vormt. |

{style=&quot;table-layout:auto&quot;}

## Verificatieconfiguraties van de klant {#customer-authentication-configurations}

Deze sectie produceert de rekeningspagina in de gebruikersinterface van het Experience Platform, waar de gebruikers Experience Platform met de rekeningen verbinden zij met uw bestemming hebben. Afhankelijk van de verificatieoptie die u aangeeft in het veld `authType`, wordt de pagina Experience Platform als volgt voor de gebruikers gegenereerd:

**Waardere verificatie**

De gebruikers worden vereist om het dragerteken in te voeren dat zij van uw bestemming verkrijgen.

![UI-weergave met dragerverificatie](./assets/bearer-authentication-ui.png)

**OAuth 2-verificatie**

De gebruikers selecteren **[!UICONTROL Connect to destination]** om OAuth 2 authentificatiestroom aan uw bestemming teweeg te brengen.

![UI-weergave met OAuth 2-verificatie](./assets/oauth2-authentication-ui.png)


| Parameter | Type | Beschrijving |
|---------|----------|------|
| `customerAuthenticationConfigurations` | Tekenreeks | Wijst op de configuratie die wordt gebruikt om de klanten van het Experience Platform aan uw server voor authentiek te verklaren. Zie `authType` hieronder voor geaccepteerde waarden. |
| `authType` | Tekenreeks | Accepteerde waarden zijn `OAUTH2, BEARER`. <br><ul><li> Als uw bestemming OAuth 2 authentificatie steunt, selecteer `OAUTH2` waarde en voeg de vereiste gebieden voor OAuth 2, zoals aangetoond in de bestemmingsSDK OAuth 2 authentificatiepagina toe. Bovendien, zou u `authenticationRule=CUSTOMER_AUTHENTICATION` in [bestemmingsleveringssectie](./destination-configuration.md) moeten selecteren. </li><li>Selecteer `BEARER` en selecteer `authenticationRule=CUSTOMER_AUTHENTICATION` in de sectie [Doellevering](./destination-configuration.md) voor nauwkeurigere verificatie.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Gegevensvelden van de klant {#customer-data-fields}

Deze sectie staat partners toe om douanegebieden te introduceren. In de voorbeeldconfiguratie hierboven, `customerDataFields` vereist gebruikers om een eindpunt in de authentificatiestroom te selecteren en op hun klantID met de bestemming te wijzen. De configuratie wordt weerspiegeld in de authentificatiestroom zoals hieronder getoond:

![Aangepaste veldverificatiestroom](./assets/custom-field-authentication-flow.png)

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `name` | Tekenreeks | Geef een naam op voor het aangepaste veld dat u introduceert. |
| `type` | Tekenreeks | Hiermee geeft u aan welk type aangepast veld u wilt gebruiken. Accepteerde waarden zijn `string`, `object`, `integer`. |
| `title` | Tekenreeks | Hiermee wordt de naam van het veld aangegeven, zoals deze wordt weergegeven door klanten in de gebruikersinterface van het Experience Platform. |
| `description` | Tekenreeks | Geef een beschrijving op voor het aangepaste veld. |
| `isRequired` | Boolean | Geeft aan of dit veld vereist is in de workflow voor doelinstellingen. |
| `enum` | Tekenreeks | Hiermee geeft u het aangepaste veld weer als een vervolgkeuzemenu en geeft u de opties weer die beschikbaar zijn voor de gebruiker. |
| `pattern` | Tekenreeks | Hiermee wordt, indien nodig, een patroon voor het aangepaste veld afgedwongen. Gebruik reguliere expressies om een patroon af te dwingen. Als uw klant-id&#39;s bijvoorbeeld geen cijfers of onderstrepingstekens bevatten, voert u `^[A-Za-z]+$` in dit veld in. |

{style=&quot;table-layout:auto&quot;}

## UI-kenmerken {#ui-attributes}

Deze sectie verwijst naar de elementen UI in de configuratie hierboven die Adobe voor uw bestemming in het gebruikersinterface van Adobe Experience Platform zou moeten gebruiken. Zie hieronder:

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `documentationLink` | Tekenreeks | Verwijst naar de documentatiepagina in [Catalogus van Doelen](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) voor uw bestemming. Gebruik `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, waarbij `YOURDESTINATION` de naam van uw bestemming is. Voor een bestemming genoemd Moviestar, zou u `http://www.adobe.com/go/destinations-moviestar-en` gebruiken |
| `category` | Tekenreeks | Verwijst naar de rubriek die aan je bestemming in Adobe Experience Platform is toegewezen. Lees [Doelcategorieën](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html) voor meer informatie. Gebruik een van de volgende waarden: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `connectionType` | Tekenreeks | `Server-to-server` is momenteel de enige beschikbare optie. |
| `frequency` | Tekenreeks | `Streaming` is momenteel de enige beschikbare optie. |

{style=&quot;table-layout:auto&quot;}

## Schemaconfiguratie in de toewijzingsstap {#schema-configuration}

![Toewijzingsstap inschakelen](./assets/enable-mapping-step.png)

Gebruik de parameters in `schemaConfig` om de toewijzingsstap van de werkstroom van de bestemmingsactivering toe te laten. Door de hieronder beschreven parameters te gebruiken, kunt u bepalen als de gebruikers van het Experience Platform profielattributen en/of identiteiten aan het gewenste schema op de kant van uw bestemming kunnen in kaart brengen.

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `profileFields` | Array | *Niet weergegeven in bovenstaande voorbeeldconfiguratie.* Wanneer u vooraf gedefinieerde kenmerken toevoegt  `profileFields`, kunnen gebruikers de kenmerken van het Experience Platform toewijzen aan de vooraf gedefinieerde kenmerken aan de zijde van het doel. |
| `profileRequired` | Boolean | Gebruik `true` als de gebruikers profielattributen van Experience Platform aan douanekenmerken op de kant van uw bestemming, zoals aangetoond in de voorbeeldconfiguratie hierboven zouden moeten kunnen in kaart brengen. |
| `segmentRequired` | Boolean | Altijd `segmentRequired:true` gebruiken. |
| `identityRequired` | Boolean | Gebruik `true` als gebruikers naamruimten van Experience Platform aan uw gewenste schema zouden moeten kunnen in kaart brengen. |

{style=&quot;table-layout:auto&quot;}

## Identiteiten en kenmerken {#identities-and-attributes}

De parameters in deze sectie bepalen hoe de doelidentiteiten en de attributen in de afbeeldingsstap van het gebruikersinterface van het Experience Platform worden bevolkt, waar de gebruikers hun schema&#39;s XDM aan het schema in uw bestemming in kaart brengen.

Adobe moet weten welke [!DNL Platform] identiteiten klanten naar uw bestemming zullen kunnen uitvoeren. Enkele voorbeelden zijn [!DNL Experience Cloud ID], gehashte e-mail, apparaat-id ([!DNL IDFA], [!DNL GAID]). Deze waarden zijn [!DNL Platform] naamruimten die klanten kunnen toewijzen aan naamruimten vanaf uw bestemming.

Identiteitsnaamruimten vereisen geen 1-aan-1 correspondentie tussen [!DNL Platform] en uw bestemming.
Klanten kunnen bijvoorbeeld een naamruimte [!DNL Platform] [!DNL IDFA] toewijzen aan een naamruimte [!DNL IDFA] van uw bestemming, of ze kunnen dezelfde naamruimte [!DNL Platform] [!DNL IDFA] toewijzen aan een naamruimte [!DNL Customer ID] in uw bestemming.

Lees meer in [Naamruimte-overzicht](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=nl).

![Doelidentiteiten renderen in de gebruikersinterface](./assets/target-identities-ui.png)

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `acceptsAttributes` | Boolean | Hiermee geeft u aan of uw doel standaardprofielkenmerken accepteert. Gewoonlijk worden deze kenmerken gemarkeerd in de documentatie van onze partners. |
| `acceptsCustomNamespaces` | Boolean | Geeft aan of klanten aangepaste naamruimten kunnen instellen op uw bestemming. |
| `allowedAttributesTransformation` | Tekenreeks | *Niet weergegeven in voorbeeldconfiguratie*. Wordt bijvoorbeeld gebruikt wanneer de [!DNL Platform]-klant gewone e-mailadressen als kenmerk heeft en uw platform alleen gehashte e-mails accepteert. Hier geeft u de transformatie op die moet worden toegepast (zet de e-mail bijvoorbeeld om in kleine letters en vervolgens in de hash). |
| `acceptedGlobalNamespaces` | - | Wordt gebruikt voor gevallen waarin uw platform [standaard naamruimten](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) accepteert (bijvoorbeeld IDFA), zodat u gebruikers van het Platform kunt beperken tot het selecteren van deze naamruimten. |

{style=&quot;table-layout:auto&quot;}

## Levering bestemming {#destination-delivery}

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `authenticationRule` | Tekenreeks | Geeft aan hoe [!DNL Platform]-klanten verbinding maken met uw doel. Accepteerde waarden zijn `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Gebruik `CUSTOMER_AUTHENTICATION` als klanten van het Platform zich bij uw systeem via een gebruikersbenaming en een wachtwoord, een dragerteken, of een andere methode van authentificatie aanmelden. U kunt deze optie bijvoorbeeld selecteren als u `authType: OAUTH2` of `authType:BEARER` ook in `customerAuthenticationConfigurations` hebt geselecteerd. </li><li> Gebruik `PLATFORM_AUTHENTICATION` als er een wereldwijd verificatiesysteem is tussen Adobe en uw bestemming en de [!DNL Platform]-klant geen verificatiegegevens hoeft op te geven om verbinding te maken met uw bestemming. In dit geval, moet u een geloofsbrieven tot stand brengen voorwerp gebruikend de [Credentials](./credentials-configuration.md) configuratie. </li><li>Gebruik `NONE` als er geen verificatie vereist is om gegevens naar het doelplatform te verzenden. </li></ul> |
| `destinationServerId` | Tekenreeks | De `instanceId` van de [doelserverconfiguratie](./destination-server-api.md) die voor deze bestemming wordt gebruikt. |
| `backfillHistoricalProfileData` | Boolean | Bepaalt of historische profielgegevens worden geëxporteerd wanneer segmenten worden geactiveerd naar de bestemming. <br> <ul><li> `true`:  [!DNL Platform] verzendt de historische gebruikersprofielen die voor het segment kwalificeren alvorens het segment wordt geactiveerd. </li><li> `false`:  [!DNL Platform] omvat alleen gebruikersprofielen die in aanmerking komen voor het segment nadat het segment is geactiveerd. </li></ul> |

{style=&quot;table-layout:auto&quot;}

## Configuratie segmenttoewijzing {#segment-mapping}

![Sectie voor configuratie van segmenttoewijzing](./assets/segment-mapping-configuration.png)

Deze sectie van de bestemmingsconfiguratie heeft op hoe segmentmeta-gegevens zoals segmentnamen of IDs tussen Experience Platform en uw bestemming zouden moeten worden gedeeld.

Door `audienceTemplateId`, verbindt deze sectie ook deze configuratie met [publieksmeta-gegevensconfiguratie](./audience-metadata-management.md).

De parameters die in de configuratie hierboven worden getoond worden beschreven in [de referenties van het bestemmingseindpunt API](./destination-configuration-api.md).

## Samenvoegingsbeleid {#aggregation}

![Samenvoegingsbeleid in het configuratiesjabloon](./assets/aggregation-configuration.png)

Deze sectie staat u toe om het samenvoegingsbeleid te plaatsen dat het Experience Platform zal gebruiken wanneer het uitvoeren van gegevens naar uw bestemming.

Een samenvoegingsbeleid bepaalt hoe de uitgevoerde profielen samen in de gegevensuitvoer worden gecombineerd. Beschikbare opties zijn:
* Beste inspanningsaggregatie
* Configureerbare samenvoeging (weergegeven in de bovenstaande configuratie)

Lees de sectie over [het gebruiken van templating](./message-format.md#using-templating) en [samenvoeging zeer belangrijke voorbeelden](./message-format.md#template-aggregation-key) om te begrijpen hoe te om het samenvoegingsbeleid in uw malplaatje van de berichttransformatie te omvatten dat op uw geselecteerd samenvoegingsbeleid wordt gebaseerd.

### Beste inspanningsaggregatie {#best-effort-aggregation}

>[!TIP]
>
>Gebruik deze optie als uw API-eindpunt minder dan 100 profielen per API-aanroep accepteert.

Deze optie werkt het best voor bestemmingen die minder profielen per verzoek verkiezen en eerder meer verzoeken met minder gegevens dan minder verzoeken met meer gegevens zouden nemen.

Gebruik de parameter `maxUsersPerRequest` om het maximumaantal profielen te specificeren dat uw bestemming in een verzoek kan nemen.

### Configureerbare samenvoeging {#configurable-aggregation}

Deze optie werkt het best als u eerder grote partijen, met duizenden profielen op de zelfde vraag zou nemen. Met deze optie kunt u ook de geëxporteerde profielen samenvoegen op basis van complexe aggregatieregels.

Met deze optie kunt u:
* Stel de maximale tijd en het maximale aantal profielen in dat moet worden samengevoegd voordat een API-aanroep naar uw bestemming wordt uitgevoerd.
* De geëxporteerde profielen bundelen die aan de bestemming zijn toegewezen op basis van:
   * segment-id
   * segmentstatus
   * identiteit of groepen van identiteiten

Voor gedetailleerde verklaringen van de samenvoegingsparameters, verwijs naar [Doelen API eindpuntverrichtingen](./destination-configuration-api.md) verwijzingspagina, waar elke parameter wordt beschreven.

<!--

commenting out the `backfillHistoricalProfileData` parameter, which will only be used after an April release

|`backfillHistoricalProfileData` | Boolean | Controls whether historical profile data is exported when segments are activated to the destination. <br> <ul><li> `true`: [!DNL Platform] sends the historical user profiles that qualified for the segment before the segment is activated. </li><li> `false`: [!DNL Platform] only includes user profiles that qualify for the segment after the segment is activated. </li></ul> |

-->
