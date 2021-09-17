---
description: Deze pagina beschrijft de diverse OAuth 2 authentificatiestromen die door Doel SDK worden gesteund, en verstrekt instructies aan opstelling OAuth 2 authentificatie voor uw bestemming.
title: OAuth 2-verificatie
exl-id: 280ecb63-5739-491c-b539-3c62bd74e433
source-git-commit: e8625d6de7707b3a159f95d4471a73cbbed25d21
workflow-type: tm+mt
source-wordcount: '2110'
ht-degree: 3%

---

# OAuth 2-verificatie

## Overzicht {#overview}

Gebruik de SDK van de Bestemming om Adobe Experience Platform toe te staan om met uw bestemming te verbinden door [OAuth 2 authentificatiekader](https://tools.ietf.org/html/rfc6749) te gebruiken.

Deze pagina beschrijft de diverse OAuth 2 authentificatiestromen die door Doel SDK worden gesteund, en verstrekt instructies aan opstelling OAuth 2 authentificatie voor uw bestemming.

## Hoe te om OAuth 2 authentificatiedetails aan uw bestemmingsconfiguratie toe te voegen {#how-to-setup}

### Vereisten in uw systeem {#prerequisites}

Als eerste stap moet u in uw systeem een app voor Adobe Experience Platform maken of op een andere manier Experience Platform in uw systeem registreren. Het doel is een cliëntidentiteitskaart en cliëntgeheim te produceren, die nodig zijn om Experience Platform aan uw bestemming voor authentiek te verklaren. Als onderdeel van deze configuratie in uw systeem hebt u de Adobe Experience Platform OAuth 2 omleiding/callback-URL&#39;s nodig, die u uit de onderstaande lijst kunt halen.

* `https://platform-va7.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-nld2.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-aus5.adobe.io/data/core/activation/oauth/api/v1/callback`

>[!IMPORTANT]
>
>De stap om een omleidings/callback URL voor Adobe Experience Platform in uw systeem te registreren wordt vereist slechts voor [OAuth 2 met de Code van de Toelating](./oauth2-authentication.md#authorization-code) subsidietype. Voor de andere twee gesteunde subsidietypes (wachtwoord en cliëntgeloofsbrieven), kunt u deze stap overslaan.

Aan het eind van deze stap, zou u moeten hebben:
* een client-id;
* een clientgeheim;
* URL voor Adobe (voor autorisatieverlening).

### Wat u in Doel SDK moet doen {#to-do-in-destination-sdk}

Als u OAuth 2-verificatie wilt instellen voor uw doel in Experience Platform, moet u uw OAuth 2-gegevens toevoegen aan de [doelconfiguratie](./destination-configuration.md), onder de `customerAuthenticationConfigurations`-parameter, door het `platform.adobe.io/data/core/activation/authoring/destinations` [API-eindpunt](./destination-configuration-api.md) te gebruiken. Zie [voorbeeldconfiguratie](./destination-configuration.md#example-configuration). Specifieke instructies over welke gebieden u aan uw configuratiemalplaatje, afhankelijk van uw OAuth 2 type van authentificatiesubsidie moet toevoegen, zijn verder hieronder op deze pagina.

## Ondersteunde OAuth 2-subsidietypen {#oauth2-grant-types}

Experience Platform steunt de drie OAuth 2 subsidietypes in onderstaande lijst. Als u een douane OAuth 2 opstelling hebt, kan Adobe het met behulp van douanevelden in uw integratie steunen. Raadpleeg de secties voor elk type subsidie voor meer informatie.

>[!IMPORTANT]
>
>* U geeft de invoerparameters op volgens de instructies in de onderstaande secties. Adobe-interne systemen maken verbinding met het verificatiesysteem van uw platform en nemen uitvoerparameters op, die worden gebruikt om de gebruiker te verifiëren en verificatie naar uw bestemming te behouden.
>* De invoerparameters die in de tabel vet worden gemarkeerd, zijn vereiste parameters in de OAuth 2-verificatiestroom. De andere parameters zijn optioneel. Er zijn andere parameters van de douaneinput die niet hier worden getoond, maar bij lengte in de secties [worden beschreven aanpassen uw configuratie OAuth 2](./oauth2-authentication.md#customize-configuration) en [Het teken van de toegang verfrist ](./oauth2-authentication.md#access-token-refresh).


| OAuth 2 Grant | Invoer | Uitvoer |
|---------|----------|---------|
| Autorisatiecode | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>bereik</li><li><b>authenticationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiredIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Wachtwoord | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>bereik</li><li><b>accessTokenUrl</b></li><li><b>gebruikersnaam</b></li><li><b>password</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiredIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Client Credential | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>bereik</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiredIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style=&quot;table-layout:auto&quot;}

De bovenstaande tabel bevat een lijst met velden die worden gebruikt in standaard OAuth 2-stromen. Naast deze standaardgebieden, kunnen diverse partnerintegraties extra input en output vereisen. Adobe heeft een flexibel OAuth 2 authentificatie/vergunningskader voor Doel SDK ontworpen die variaties aan het bovengenoemde standaardgebiedspatroon kan behandelen terwijl het steunen van een mechanisme om ongeldige output, zoals verlopen toegangstokens automatisch opnieuw te produceren.

De output omvat in alle gevallen een toegangstoken, dat door Experience Platform wordt gebruikt om authentificatie aan uw bestemming voor authentiek te verklaren en te handhaven.

Het systeem dat Adobe voor authentificatie OAuth 2 heeft ontworpen:
* Ondersteunt alle drie OAuth 2-subsidies en verwerkt eventuele variaties in deze subsidies, zoals extra gegevensvelden, niet-standaard API-aanroepen en meer.
* Ondersteunt toegangstokens met variërende levenwaarden, of het nu gaat om 90 dagen, 30 minuten of een andere levensduurwaarde die u opgeeft.
* Ondersteunt OAuth 2-machtigingsstromen met of zonder tokens vernieuwen.

## OAuth 2 met machtigingscode {#authorization-code}

Als uw bestemming een standaardOAuth 2.0 stroom van de Code van de Vergunning (lees [RFC normen specs](https://tools.ietf.org/html/rfc6749#section-4.1)) of een variatie van het steunt, raadpleeg de vereiste en facultatieve gebieden hieronder:

| OAuth 2 Grant | Invoer | Uitvoer |
|---------|----------|---------|
| Autorisatiecode | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>bereik</li><li><b>authenticationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiredIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style=&quot;table-layout:auto&quot;}

Om opstelling deze authentificatiemethode voor uw bestemming, voeg de volgende lijnen aan uw configuratie, in `/destinations` [eindpunt](./destination-configuration.md) toe:

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_AUTHORIZATION_CODE",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "authorizationUrl": "https://www.moviestar.com/dialog/OAuth",
      "refreshTokenUrl": "https://api.moviestar.com/OAuth/refresh_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
//...
}
```

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `authType` | Tekenreeks | Gebruik &quot;OAUTH2&quot;. |
| `grant` | Tekenreeks | Gebruik &quot;OAUTH2_AUZATION_CODE&quot;. |
| `accessTokenUrl` | Tekenreeks | De URL aan uw zijde, die toegangstokens uitgeeft en, naar keuze, tokens verfrist. |
| `authorizationUrl` | Tekenreeks | De URL van uw verificatieserver, waar u de gebruiker omleidt om zich aan te melden bij uw toepassing. |
| `refreshTokenUrl` | Tekenreeks | *Optioneel.* De URL aan uw zijde, die vernieuwt tokens uitgeeft. Vaak is `refreshTokenUrl` hetzelfde als `accessTokenUrl`. |
| `clientId` | Tekenreeks | De client-id die door uw systeem aan Adobe Experience Platform wordt toegewezen. |
| `clientSecret` | Tekenreeks | Het clientgeheim dat uw systeem aan Adobe Experience Platform toewijst. |
| `scope` | Lijst met tekenreeksen | *Optioneel*. Plaats het werkingsgebied van wat het toegangstoken Experience Platform toestaat om op uw middelen uit te voeren. Voorbeeld: &quot;read, write&quot;. |

{style=&quot;table-layout:auto&quot;}

## OAuth 2 with Password Grant

Voor de OAuth 2 toelage van het Wachtwoord (lees [RFC normen specs](https://tools.ietf.org/html/rfc6749#section-4.3)), vereist het Experience Platform de gebruikersbenaming en het wachtwoord van de gebruiker. In de authentificatiestroom, ruilt het Experience Platform deze geloofsbrieven voor een toegangstoken en, naar keuze, verfrist het teken.
Adobe maakt gebruik van de standaardinvoer hieronder om bestemmingsconfiguratie te vereenvoudigen, met de capaciteit om waarden met voeten te treden:

| OAuth 2 Grant | Invoer | Uitvoer |
|---------|----------|---------|
| Wachtwoord | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>bereik</li><li><b>accessTokenUrl</b></li><li><b>gebruikersnaam</b></li><li><b>password</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiredIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
> U hoeft geen parameters voor `username` en `password` in de onderstaande configuratie toe te voegen. Wanneer u `"grant": "OAUTH2_PASSWORD"` in de bestemmingsconfiguratie toevoegt, zal het systeem de gebruiker verzoeken om een gebruikersbenaming en een wachtwoord in het Experience Platform UI te verstrekken, wanneer zij aan uw bestemming voor authentiek verklaren.

Om opstelling deze authentificatiemethode voor uw bestemming, voeg de volgende lijnen aan uw configuratie, in `/destinations` [eindpunt](./destination-configuration.md) toe:

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_PASSWORD",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
```

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `authType` | Tekenreeks | Gebruik &quot;OAUTH2&quot;. |
| `grant` | Tekenreeks | Gebruik &quot;OAUTH2_PASSWORD&quot;. |
| `accessTokenUrl` | Tekenreeks | De URL aan uw zijde, die toegangstokens uitgeeft en, naar keuze, tokens verfrist. |
| `clientId` | Tekenreeks | De client-id die door uw systeem aan Adobe Experience Platform wordt toegewezen. |
| `clientSecret` | Tekenreeks | Het clientgeheim dat uw systeem aan Adobe Experience Platform toewijst. |
| `scope` | Lijst met tekenreeksen | *Optioneel*. Plaats het werkingsgebied van wat het toegangstoken Experience Platform toestaat om op uw middelen uit te voeren. Voorbeeld: &quot;read, write&quot;. |

{style=&quot;table-layout:auto&quot;}

## OAuth 2 met Client Credentials Grant

U kunt een OAuth 2 de Referentie van de Cliënt (lees [RFC normen specs](https://tools.ietf.org/html/rfc6749#section-4.4)) bestemming vormen, die de hieronder vermelde standaardinput en output steunt. U kunt de waarden aanpassen. Zie [Uw OAuth 2 configuratie](./oauth2-authentication.md#customize-configuration) voor details aanpassen.

| OAuth 2 Grant | Invoer | Uitvoer |
|---------|----------|---------|
| Client Credentials | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>bereik</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiredIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style=&quot;table-layout:auto&quot;}

Om opstelling deze authentificatiemethode voor uw bestemming, voeg de volgende lijnen aan uw configuratie, in `/destinations` [eindpunt](./destination-configuration.md) toe:

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_CLIENT_CREDENTIALS",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "refreshTokenUrl": "https://api.moviestar.com/OAuth/refresh_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
//...
}
```

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `authType` | Tekenreeks | Gebruik &quot;OAUTH2&quot;. |
| `grant` | Tekenreeks | Gebruik &quot;OAUTH2_CLIENT_CREDENTIALS&quot;. |
| `accessTokenUrl` | Tekenreeks | De URL van uw verificatieserver, die een toegangstoken en een optioneel vernieuwingstoken uitgeeft. |
| `refreshTokenUrl` | Tekenreeks | *Optioneel.* De URL aan uw zijde, die vernieuwt tokens uitgeeft. Vaak is `refreshTokenUrl` hetzelfde als `accessTokenUrl`. |
| `clientId` | Tekenreeks | De client-id die door uw systeem aan Adobe Experience Platform wordt toegewezen. |
| `clientSecret` | Tekenreeks | Het clientgeheim dat uw systeem aan Adobe Experience Platform toewijst. |
| `scope` | Lijst met tekenreeksen | *Optioneel*. Plaats het werkingsgebied van wat het toegangstoken Experience Platform toestaat om op uw middelen uit te voeren. Voorbeeld: &quot;read, write&quot;. |

{style=&quot;table-layout:auto&quot;}

## Uw OAuth 2-configuratie aanpassen {#customize-configuration}

De configuraties die in de bovenstaande secties worden beschreven, beschrijven standaard OAuth 2-subsidies. Nochtans, verstrekt het systeem dat door Adobe wordt ontworpen flexibiliteit zodat kunt u douaneparameters voor om het even welke variaties in OAuth 2 subsidie gebruiken. Als u de standaard OAuth 2-instellingen wilt aanpassen, gebruikt u de parameters `authenticationDataFields`, zoals in de onderstaande voorbeelden wordt getoond.

### Voorbeeld 1: Het gebruiken van `authenticationDataFields` om informatie te vangen die uit de authentificatiereactie komt {#example-1}

In dit voorbeeld, heeft een bestemmingsplatform tokens verfrissen die na een bepaalde hoeveelheid tijd verlopen. In dit geval stelt de partner het aangepaste veld `refreshTokenExpiration` in om de vervaldatum van het vernieuwingstoken in het veld `refresh_token_expires_in` in de API-reactie op te halen.

```json
{
   "customerAuthenticationConfigurations":[
      {
         "authType":"OAUTH2",
         "options":{
            
         },
         "grant":"OAUTH2_AUTHORIZATION_CODE",
         "accessTokenUrl":"https://api.moviestar.com/OAuth/access_token",
         "authorizationUrl":"https://api.moviestar.com/OAuth/authorization",
         "scope":[
            "read",
            "write",
            "delete"
         ],
         "refreshTokenUrl":"https://api.moviestar.com/OAuth/accessToken",
         "clientSecret":"client-secret-here",
         "authenticationDataFields":[
            {
               "name":"refreshTokenExpiration",
               "title":"Refresh Token Expires In",
               "description":"Time in seconds when the refresh token will expire",
               "type":"string",
               "isRequired":false,
               "source":"CUSTOMER",
               "authenticationResponsePath":"refresh_token_expires_in"
            }
         ]
      }
   ]
}  
```

### Voorbeeld 2: Het gebruiken van `authenticationDataFields` om een speciaal verfrist teken te verstrekken {#example-2}

In dit voorbeeld, plaatst een partner - omhoog hun bestemming om speciaal te verstrekken verfrist teken. Bovendien wordt de vervaldatum voor toegangstokens niet teruggekeerd in de API reactie zodat kunnen zij een standaardwaarde, in dit geval 3600 seconden hardcoderen.

```json
      "authenticationDataFields": [
        {
            "name": "refreshToken",
            "value": "special_refresh_token"
        },
        {
            "name": "expiresIn",
            "value": 3600
        } 
      ]
```

### Voorbeeld 3: De gebruiker voert cliënt ID en cliëntgeheim in wanneer zij de bestemming vormen {#example-3}

In dit voorbeeld moet de klant in plaats van een algemene client-id en een clientgeheim te maken, zoals wordt weergegeven in de sectie [Voorwaarden in uw systeem](./oauth2-authentication.md#prerequisites), de client-id, het clientgeheim en de account-id invoeren (de id die de klant gebruikt om zich aan te melden bij de bestemming).

```json
{
    //...
    "customerAuthenticationConfigurations": [
        {
            "authType": "OAUTH2",
            "grant": "OAUTH2_CLIENT_CREDENTIALS",
            "authenticationDataFields": [
                {
                    "name": "clientId",
                    "title": "Client ID",
                    "description": "Client ID",
                    "type": "string",
                    "isRequired": true,
                    "fieldType": "CUSTOMER"
                },
                {
                    "name": "clientSecret",
                    "title": "Client Secret",
                    "description": "Client Secret",
                    "type": "string",
                    "isRequired": true,
                    "format": "password",
                    "fieldType": "CUSTOMER"
                },
                {
                    "name": "moviestarId",
                    "title": "Moviestar ID",
                    "description": "Moviestar ID",
                    "type": "string",
                    "isRequired": true,
                    "fieldType": "CUSTOMER"
                }
            ],
            "accessTokenRequest": {
                "destinationServerType": "URL_BASED",
                "urlBasedDestination": {
                    "url": {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "https://{{ authData.moviestarId }}.yourdestination.com/identity/oauth/token"
                    }
                },
                "httpTemplate": {
                    "requestBody": {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ formUrlEncode('grant_type', 'client_credentials', 'client_id', authData.clientId, 'client_secret', authData.clientSecret) | raw }}"
                    },
                    "httpMethod": "POST",
                    "contentType": "application/x-www-form-urlencoded"
                },
                "responseFields": [
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.access_token }}",
                        "name": "accessToken"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.scope }}",
                        "name": "scope"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.token_type }}",
                        "name": "tokenType"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.expires_in }}",
                        "name": "expiresIn"
                    }
                ]
            }
        }
    ]
//...
}
```



U kunt de volgende parameters in `authenticationDataFields` gebruiken om uw configuratie aan te passen OAuth 2:

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `authenticationDataFields.name` | Tekenreeks | De naam van het aangepaste veld. |
| `authenticationDataFields.title` | Tekenreeks | Een titel die u voor het aangepaste veld kunt opgeven. |
| `authenticationDataFields.description` | Tekenreeks | Een beschrijving van het aangepaste gegevensveld dat u hebt ingesteld. |
| `authenticationDataFields.type` | Tekenreeks | Hiermee definieert u het type van het veld Aangepaste gegevens. <br> Geaccepteerde waarden:  `string`,  `boolean`,  `integer` |
| `authenticationDataFields.isRequired` | Boolean | Geeft aan of het aangepaste gegevensveld vereist is in de verificatiestroom. |
| `authenticationDataFields.format` | Tekenreeks | Wanneer u `"format":"password"` selecteert, codeert Adobe de waarde van het gebied van authentificatiegegevens. Wanneer gebruikt met `"fieldType": "CUSTOMER"`, verbergt dit ook de input in UI wanneer de gebruiker in het gebied typt. |
| `authenticationDataFields.fieldType` | Tekenreeks | Wijst erop of de input uit de partner (u) of van de gebruiker komt, wanneer zij opstelling uw bestemming in Experience Platform. |
| `authenticationDataFields.value` | Tekenreeks. Booleaans. Geheel | De waarde van het veld met aangepaste gegevens. De waarde komt overeen met het gekozen type uit `authenticationDataFields.type`. |
| `authenticationDataFields.authenticationResponsePath` | Tekenreeks | Geeft aan naar welk veld van het API-antwoordpad u verwijst. |

{style=&quot;table-layout:auto&quot;}

## Vernieuwen van toegangstoken {#access-token-refresh}

Adobe heeft een systeem ontworpen dat verlopen toegangstokens vernieuwt zonder dat de gebruiker zich weer hoeft aan te melden bij uw platform. Het systeem kan een nieuw token genereren zodat de activering van uw bestemming naadloos voor de klant wordt voortgezet.

Om het teken van de opstellingstoegang te verfrissen zich, kunt u een templatized HTTP- verzoek moeten vormen die Adobe toestaat om een nieuw toegangstoken te krijgen, gebruikend verfrist symbolisch. Als het toegangstoken is verlopen, neemt Adobe het sjabloonverzoek dat door u wordt verstrekt, toevoegend de parameters u verstrekte. Gebruik de `accessTokenRequest` parameter om een toegangstoken te vormen verfrist mechanisme.


```json
{
   "customerAuthenticationConfigurations":[
      {
         "authType":"OAUTH2",
         "grant":"OAUTH2_CLIENT_CREDENTIALS",
         "accessTokenRequest":{
            "destinationServerType":"URL_BASED",
            "urlBasedDestination":{
               "url":{
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"https://{{authData.customerId}}.yourdestination.com/identity/oauth/token"
               }
            },
            "httpTemplate":{
               "requestBody":{
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ formUrlEncode('grant_type', 'client_credentials', 'client_id', authData.clientId, 'client_secret', authData.clientSecret) | raw }}"
               },
               "httpMethod":"POST",
               "contentType":"application/x-www-form-urlencoded",
               "headers":[
                  
               ]
            },
            "responseFields":[
               {
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ response.body.expires_in }}",
                  "name":"expiresIn"
               },
               {
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ response.body.access_token }}",
                  "name":"accessToken"
               }
            ],
            "validations":[
               {
                  "name":"access_token validation",
                  "actualValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"{{response.body.access_token is empty }}"
                  },
                  "expectedValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"false"
                  }
               },
               {
                  "name":"response status",
                  "actualValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"{{ response.status }}"
                  },
                  "expectedValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"200"
                  }
               }
            ]
         }
      }
   ]
}
```

U kunt de volgende parameters in `accessTokenRequest` gebruiken om uw token aan te passen vernieuwt proces:

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `accessTokenRequest.destinationServerType` | Tekenreeks | Gebruik `URL_BASED`. |
| `accessTokenRequest.urlBasedDestination.url.templatingStrategy` | Tekenreeks | <ul><li>Gebruik `PEBBLE_V1` als u sjablonen voor de waarde in `accessTokenRequest.urlBasedDestination.url.value` gebruikt.</li><li> Gebruik `NONE` als de waarde in het veld `accessTokenRequest.urlBasedDestination.url.value` een constante is. </li></li> |
| `accessTokenRequest.urlBasedDestination.url.value` | Tekenreeks | De URL waar het Experience Platform om het toegangstoken verzoekt. |
| `accessTokenRequest.httpTemplate.requestBody.templatingStrategy` | Tekenreeks | <ul><li>Gebruik `PEBBLE_V1` als u sjablonen gebruikt voor de waarden in `accessTokenRequest.httpTemplate.requestBody.value`.</li><li> Gebruik `NONE` als de waarde in het veld `accessTokenRequest.httpTemplate.requestBody.value` een constante is. </li></li> |
| `accessTokenRequest.httpTemplate.requestBody.value` | Tekenreeks | Gebruik de sjabloontaal om velden in de HTTP-aanvraag aan te passen aan het eindpunt van het toegangstoken. Raadpleeg de sectie [Tijdelijke conventies](./oauth2-authentication.md#templating-conventions) voor informatie over hoe u sjablonen kunt gebruiken om velden aan te passen. |
| `accessTokenRequest.httpTemplate.httpMethod` | Tekenreeks | Specificeert de methode die van HTTP wordt gebruikt om uw eindpunt van het toegangstoken te roepen. In de meeste gevallen is deze waarde `POST`. |
| `accessTokenRequest.httpTemplate.contentType` | Tekenreeks | Specificeert het inhoudstype van de vraag van HTTP aan uw toegangstoken eindpunt. <br> Bijvoorbeeld:  `application/x-www-form-urlencoded` of  `application/json`. |
| `accessTokenRequest.httpTemplate.headers` | Tekenreeks | Specificeert als om het even welke kopballen aan de vraag van HTTP aan uw toegangstoken eindpunt zouden moeten worden toegevoegd. |
| `accessTokenRequest.responseFields.templatingStrategy` | Tekenreeks | <ul><li>Gebruik `PEBBLE_V1` als u sjablonen gebruikt voor de waarden in `accessTokenRequest.responseFields.value`.</li><li> Gebruik `NONE` als de waarde in het veld `accessTokenRequest.responseFields.value` een constante is. </li></li> |
| `accessTokenRequest.responseFields.value` | Tekenreeks | De malplaatjetaal van het gebruik om tot gebieden in de reactie van HTTP van uw toegangstoken eindpunt toegang te hebben. Raadpleeg de sectie [Tijdelijke conventies](./oauth2-authentication.md#templating-conventions) voor informatie over hoe u sjablonen kunt gebruiken om velden aan te passen. |
| `accessTokenRequest.validations.name` | Tekenreeks | Geeft de naam aan die u voor deze validatie hebt opgegeven. |
| `accessTokenRequest.validations.actualValue.templatingStrategy` | Tekenreeks | <ul><li>Gebruik `PEBBLE_V1` als u sjablonen gebruikt voor de waarden in `accessTokenRequest.validations.actualValue.value`.</li><li> Gebruik `NONE` als de waarde in het veld `accessTokenRequest.validations.actualValue.value` een constante is. </li></li> |
| `accessTokenRequest.validations.actualValue.value` | Tekenreeks | Gebruik een sjabloontaal voor toegang tot velden in de HTTP-respons. Raadpleeg de sectie [Tijdelijke conventies](./oauth2-authentication.md#templating-conventions) voor informatie over hoe u sjablonen kunt gebruiken om velden aan te passen. |
| `accessTokenRequest.validations.expectedValue.templatingStrategy` | Tekenreeks | <ul><li>Gebruik `PEBBLE_V1` als u sjablonen gebruikt voor de waarden in `accessTokenRequest.validations.expectedValue.value`.</li><li> Gebruik `NONE` als de waarde in het veld `accessTokenRequest.validations.expectedValue.value` een constante is. </li></li> |
| `accessTokenRequest.validations.expectedValue.value` | Tekenreeks | Gebruik een sjabloontaal voor toegang tot velden in de HTTP-respons. Raadpleeg de sectie [Tijdelijke conventies](./oauth2-authentication.md#templating-conventions) voor informatie over hoe u sjablonen kunt gebruiken om velden aan te passen. |

{style=&quot;table-layout:auto&quot;}

## Sjabloonconventies {#templating-conventions}

Afhankelijk van uw authentificatieaanpassing, zou u tot gegevensgebieden in de authentificatiereactie kunnen moeten toegang hebben, zoals aangetoond in de vorige sectie. Om dat te doen, gelieve zich met [Kiezels het templating taal](https://pebbletemplates.io/) vertrouwd te maken die door Adobe wordt gebruikt en te verwijzen naar de malplaatjeovereenkomsten hieronder om uw OAuth 2 implementatie aan te passen.


| Voorvoegsel | Beschrijving | Voorbeeld |
|---------|----------|---------|
| authData | Heb toegang tot om het even welke partner of waarde van de klantengegevens. | ``{{ authData.accessToken }}`` |
| response.body | HTTP-responsinstantie | ``{{ response.body.access_token }}`` |
| response.status | HTTP-reactiestatus | ``{{ response.status }}`` |
| response.headers | HTTP-antwoordheaders | ``{{ response.headers.server[0] }}`` |
| userContext | Toegang tot informatie over de huidige verificatiepoging | <ul><li>`{{ userContext.sandboxName }} `</li><li>`{{ userContext.sandboxId }} `</li><li>`{{ userContext.imsOrgId }} `</li><li>`{{ userContext.client }} // the client executing the authentication attempt `</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Volgende stappen {#next-steps}

Door dit artikel te lezen, hebt u nu inzicht in de OAuth 2 authentificatiepatronen die door Adobe Experience Platform worden gesteund en weet hoe te om uw bestemming met OAuth 2 authentificatiesteun te vormen. Daarna, kunt u opstelling uw 2-gesteunde bestemming OAuth gebruikend Doel SDK. Lees [Gebruik de Doel SDK om uw bestemming](./configure-destination-instructions.md) voor volgende stappen te vormen.
