---
description: Deze pagina beschrijft de diverse OAuth 2 vergunningsstromen die door Destination SDK worden gesteund, en verstrekt instructies aan opstelling OAuth 2 vergunning voor uw bestemming.
title: OAuth 2-vergunning
exl-id: 280ecb63-5739-491c-b539-3c62bd74e433
source-git-commit: 7ba9971b44410e609c64f4dcf956a1976207353e
workflow-type: tm+mt
source-wordcount: '2181'
ht-degree: 0%

---


# OAuth 2-vergunning

Destination SDK steunt verscheidene vergunningsmethodes aan uw bestemming. Hieronder vindt u de optie voor verificatie bij uw bestemming met behulp van de optie [OAuth 2-vergunningskader](https://tools.ietf.org/html/rfc6749).

Deze pagina beschrijft de diverse OAuth 2 vergunningsstromen die door Destination SDK worden gesteund, en verstrekt instructies aan opstelling OAuth 2 vergunning voor uw bestemming.

>[!IMPORTANT]
>
>Alle parameternamen en -waarden die door Destination SDK worden ondersteund, zijn **hoofdlettergevoelig**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Ondersteunde integratietypen {#supported-integration-types}

Raadpleeg de onderstaande tabel voor meer informatie over de integratietypen die de op deze pagina beschreven functionaliteit ondersteunen.

| Type integratie | Ondersteunt functionaliteit |
|---|---|
| Integraties in realtime (streaming) | Ja |
| Op bestanden gebaseerde (batch) integratie | Nee |

## Hoe te om OAuth 2 vergunningsdetails aan uw bestemmingsconfiguratie toe te voegen {#how-to-setup}

### Vereisten in uw systeem {#prerequisites}

Als eerste stap moet u in uw systeem een app voor Adobe Experience Platform maken of op een andere manier Experience Platform in uw systeem registreren. Het doel is een cliëntidentiteitskaart en cliëntgeheim te produceren, die nodig zijn om Experience Platform aan uw bestemming voor authentiek te verklaren.

Als onderdeel van deze configuratie in uw systeem hebt u de Adobe Experience Platform OAuth 2 omleiding/callback-URL&#39;s nodig, die u uit de onderstaande lijst kunt halen.

* `https://platform-va7.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-nld2.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-aus5.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-can2.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-gbr9.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform.adobe.io/data/core/activation/oauth/api/v1/callback`

>[!IMPORTANT]
>
>De stap om een omleidings-/callback-URL voor Adobe Experience Platform in uw systeem te registreren is alleen vereist voor de [OAuth 2 met vergunningscode](#authorization-code) subsidietype. Voor de andere twee gesteunde subsidietypes (wachtwoord en cliëntgeloofsbrieven), kunt u deze stap overslaan.

Aan het eind van deze stap, zou u moeten hebben:
* een client-id;
* een clientgeheim;
* De callback-URL van de Adobe (voor de autorisatiecode-subsidie).

### Wat u moet doen in Destination SDK {#to-do-in-destination-sdk}

Om OAuth 2 vergunning voor uw bestemming in Experience Platform te plaatsen, moet u uw OAuth 2 details aan OAuth toevoegen [doelconfiguratie](../../authoring-api/destination-configuration/create-destination-configuration.md), onder de `customerAuthenticationConfigurations` parameter. Zie [klantverificatie](../../functionality/destination-configuration/customer-authentication.md) voor gedetailleerde voorbeelden. Specifieke instructies over welke gebieden u aan uw configuratiemalplaatje, afhankelijk van uw OAuth 2 type van vergunningsvergunning moet toevoegen, zijn verder hieronder op deze pagina.

## Ondersteunde OAuth 2-subsidietypen {#oauth2-grant-types}

Experience Platform steunt de drie OAuth 2 subsidietypes in onderstaande lijst. Als u een douane OAuth 2 opstelling hebt, kan de Adobe het met behulp van douanevelden in uw integratie steunen. Raadpleeg de secties voor elk type subsidie voor meer informatie.

>[!IMPORTANT]
>
>* U geeft de invoerparameters op volgens de instructies in de onderstaande secties. De Adobe-interne systemen verbinden met het vergunningssysteem van uw platform en grijpen outputparameters, die worden gebruikt om de gebruiker voor authentiek te verklaren en vergunning aan uw bestemming te handhaven.
>* De invoerparameters die in de tabel vet worden gemarkeerd, zijn vereiste parameters in de OAuth 2-autorisatiestroom. De andere parameters zijn optioneel. Er zijn andere aangepaste invoerparameters die hier niet worden weergegeven, maar die in de secties met een lengte worden beschreven [Uw OAuth 2-configuratie aanpassen](#customize-configuration) en [Toegang token vernieuwen](#access-token-refresh).

| OAuth 2 Grant | Invoer | Uitvoer |
|---------|----------|---------|
| Autorisatiecode | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>bereik</li><li><b>authenticationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiredIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Wachtwoord | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>bereik</li><li><b>accessTokenUrl</b></li><li><b>gebruikersnaam</b></li><li><b>password</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiredIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Client Credential | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>bereik</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiredIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

De bovenstaande tabel bevat een lijst met velden die worden gebruikt in standaard OAuth 2-stromen. Naast deze standaardgebieden, kunnen diverse partnerintegraties extra input en output vereisen. Adobe heeft een flexibel OAuth 2 vergunningskader voor Destination SDK ontworpen die veranderingen in het bovengenoemde standaardgebiedspatroon kan behandelen terwijl het steunen van een mechanisme om ongeldige output, zoals verlopen toegangstokens automatisch opnieuw te produceren.

De output omvat in alle gevallen een toegangstoken, dat door Experience Platform wordt gebruikt om vergunning aan uw bestemming voor authentiek te verklaren en te handhaven.

Het systeem dat de Adobe heeft ontworpen voor OAuth 2-autorisatie:
* Ondersteunt alle drie OAuth 2-subsidies en verwerkt eventuele variaties in deze subsidies, zoals extra gegevensvelden, niet-standaard API-aanroepen en meer.
* Ondersteunt toegangstokens met variërende levenwaarden, of het nu gaat om 90 dagen, 30 minuten of een andere levensduurwaarde die u opgeeft.
* Ondersteunt OAuth 2-machtigingsstromen met of zonder tokens vernieuwen.

## OAuth 2 met vergunningscode {#authorization-code}

Als uw bestemming een standaardstroom van de Code van de Toestemming van OAuth 2.0 steunt (lees [Specificaties van RFC-standaarden](https://tools.ietf.org/html/rfc6749#section-4.1)) of een variatie daarvan, de vereiste en facultatieve velden hieronder raadplegen:

| OAuth 2 Grant | Invoer | Uitvoer |
|---------|----------|---------|
| Autorisatiecode | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>bereik</li><li><b>authenticationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiredIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

Aan opstelling deze vergunningsmethode voor uw bestemming, voeg de volgende lijnen aan uw configuratie toe, wanneer u [een doelconfiguratie maken](../../authoring-api/destination-configuration/create-destination-configuration.md):

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
| `authType` | String | Gebruik &quot;OAUTH2&quot;. |
| `grant` | String | Gebruik &quot;OAUTH2_AUZATION_CODE&quot;. |
| `accessTokenUrl` | String | De URL aan uw zijde, die toegangstokens uitgeeft en, naar keuze, tokens verfrist. |
| `authorizationUrl` | String | De URL van uw verificatieserver, waar u de gebruiker omleidt om zich aan te melden bij uw toepassing. |
| `refreshTokenUrl` | String | *Optioneel.* De URL aan uw zijde, die vernieuwt tokens uitgeeft. Vaak, `refreshTokenUrl` is gelijk aan `accessTokenUrl`. |
| `clientId` | String | De client-id die door uw systeem aan Adobe Experience Platform wordt toegewezen. |
| `clientSecret` | String | Het clientgeheim dat uw systeem aan Adobe Experience Platform toewijst. |
| `scope` | Lijst met tekenreeksen | *Optioneel*. Plaats het werkingsgebied van wat het toegangstoken Experience Platform toestaat om op uw middelen uit te voeren. Voorbeeld: &quot;read, write&quot;. |

{style="table-layout:auto"}

## OAuth 2 with Password Grant

Voor de OAuth 2-wachtwoordsubsidie (lees de [Specificaties van RFC-standaarden](https://tools.ietf.org/html/rfc6749#section-4.3)), vereist Experience Platform de gebruikersnaam en het wachtwoord van de gebruiker. In de vergunningsstroom, ruilt het Experience Platform deze geloofsbrieven voor een toegangstoken en, naar keuze, verfrist teken.
Adobe maakt gebruik van de standaardinvoer hieronder om bestemmingsconfiguratie te vereenvoudigen, met de capaciteit om waarden met voeten te treden:

| OAuth 2 Grant | Invoer | Uitvoer |
|---------|----------|---------|
| Wachtwoord | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>bereik</li><li><b>accessTokenUrl</b></li><li><b>gebruikersnaam</b></li><li><b>password</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiredIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

>[!NOTE]
>
> U hoeft geen parameters toe te voegen voor `username` en `password` in de onderstaande configuratie. Wanneer u `"grant": "OAUTH2_PASSWORD"` in de bestemmingsconfiguratie, zal het systeem de gebruiker verzoeken om een gebruikersbenaming en een wachtwoord in het Experience Platform UI te verstrekken, wanneer zij aan uw bestemming voor authentiek verklaren.

Aan opstelling deze vergunningsmethode voor uw bestemming, voeg de volgende lijnen aan uw configuratie toe, wanneer u [een doelconfiguratie maken](../../authoring-api/destination-configuration/create-destination-configuration.md):

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
| `authType` | String | Gebruik &quot;OAUTH2&quot;. |
| `grant` | String | Gebruik &quot;OAUTH2_PASSWORD&quot;. |
| `accessTokenUrl` | String | De URL aan uw zijde, die toegangstokens uitgeeft en, naar keuze, tokens verfrist. |
| `clientId` | String | De client-id die door uw systeem aan Adobe Experience Platform wordt toegewezen. |
| `clientSecret` | String | Het clientgeheim dat uw systeem aan Adobe Experience Platform toewijst. |
| `scope` | Lijst met tekenreeksen | *Optioneel*. Plaats het werkingsgebied van wat het toegangstoken Experience Platform toestaat om op uw middelen uit te voeren. Voorbeeld: &quot;read, write&quot;. |

{style="table-layout:auto"}

## OAuth 2 met Client Credentials Grant

U kunt een OAuth 2 Credentials (lees [Specificaties van RFC-standaarden](https://tools.ietf.org/html/rfc6749#section-4.4)), die de hieronder vermelde standaardinvoer en -uitvoer ondersteunt. U kunt de waarden aanpassen. Zie [Uw OAuth 2-configuratie aanpassen](#customize-configuration) voor meer informatie.

| OAuth 2 Grant | Invoer | Uitvoer |
|---------|----------|---------|
| Client Credentials | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>bereik</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiredIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

Aan opstelling deze vergunningsmethode voor uw bestemming, voeg de volgende lijnen aan uw configuratie toe, wanneer u [een doelconfiguratie maken](../../authoring-api/destination-configuration/create-destination-configuration.md):

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
| `authType` | String | Gebruik &quot;OAUTH2&quot;. |
| `grant` | String | Gebruik &quot;OAUTH2_CLIENT_CREDENTIALS&quot;. |
| `accessTokenUrl` | String | De URL van uw verificatieserver, die een toegangstoken en een optioneel vernieuwingstoken uitgeeft. |
| `refreshTokenUrl` | String | *Optioneel.* De URL aan uw zijde, die vernieuwt tokens uitgeeft. Vaak, `refreshTokenUrl` is gelijk aan `accessTokenUrl`. |
| `clientId` | String | De client-id die door uw systeem aan Adobe Experience Platform wordt toegewezen. |
| `clientSecret` | String | Het clientgeheim dat uw systeem aan Adobe Experience Platform toewijst. |
| `scope` | Lijst met tekenreeksen | *Optioneel*. Plaats het werkingsgebied van wat het toegangstoken Experience Platform toestaat om op uw middelen uit te voeren. Voorbeeld: &quot;read, write&quot;. |

{style="table-layout:auto"}

## Uw OAuth 2-configuratie aanpassen {#customize-configuration}

De configuraties die in de bovenstaande secties worden beschreven, beschrijven standaard OAuth 2-subsidies. Nochtans, verstrekt het systeem dat door Adobe wordt ontworpen flexibiliteit zodat kunt u douaneparameters voor om het even welke variaties in OAuth 2 subsidie gebruiken. Als u de standaard OAuth 2-instellingen wilt aanpassen, gebruikt u de opdracht `authenticationDataFields` parameters, zoals in de onderstaande voorbeelden wordt getoond.

### Voorbeeld 1: gebruiken `authenticationDataFields` het verzamelen van informatie die afkomstig is van het antwoord op de vergunning {#example-1}

In dit voorbeeld, heeft een bestemmingsplatform tokens verfrissen die na een bepaalde hoeveelheid tijd verlopen. In dit geval stelt de partner de `refreshTokenExpiration` aangepast veld om de vervaldatum van het vernieuwingstoken op te halen in het dialoogvenster `refresh_token_expires_in` in de API-reactie.

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

### Voorbeeld 2: gebruiken `authenticationDataFields` om een speciaal vernieuwingstoken te verstrekken {#example-2}

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

In dit voorbeeld maakt u geen algemene client-id en clientgeheim, zoals in de sectie wordt getoond [Vereisten in uw systeem](#prerequisites), moet de klant client-id, clientgeheim en account-id invoeren (de id die de klant gebruikt om zich aan te melden bij het doel)

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
                    "source": "CUSTOMER"
                },
                {
                    "name": "clientSecret",
                    "title": "Client Secret",
                    "description": "Client Secret",
                    "type": "string",
                    "isRequired": true,
                    "format": "password",
                    "source": "CUSTOMER"
                },
                {
                    "name": "moviestarId",
                    "title": "Moviestar ID",
                    "description": "Moviestar ID",
                    "type": "string",
                    "isRequired": true,
                    "source": "CUSTOMER"
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



U kunt de volgende parameters gebruiken in `authenticationDataFields` om uw OAuth 2 configuratie aan te passen:

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `authenticationDataFields.name` | String | De naam van het aangepaste veld. |
| `authenticationDataFields.title` | String | Een titel die u voor het aangepaste veld kunt opgeven. |
| `authenticationDataFields.description` | String | Een beschrijving van het aangepaste gegevensveld dat u hebt ingesteld. |
| `authenticationDataFields.type` | String | Hiermee definieert u het type van het veld Aangepaste gegevens. <br> Geaccepteerde waarden: `string`, `boolean`, `integer` |
| `authenticationDataFields.isRequired` | Boolean | Geeft aan of het veld met aangepaste gegevens is vereist in de machtigingsstroom. |
| `authenticationDataFields.format` | String | Wanneer u `"format":"password"`, versleutelt de Adobe de waarde van het veld met machtigingsgegevens. Indien gebruikt met `"fieldType": "CUSTOMER"`Hiermee verbergt u ook de invoer in de gebruikersinterface wanneer de gebruiker in het veld typt. |
| `authenticationDataFields.fieldType` | String | Wijst erop of de input uit de partner (u) of van de gebruiker komt, wanneer zij opstelling uw bestemming in Experience Platform. |
| `authenticationDataFields.value` | String. Booleaans. Geheel | De waarde van het veld met aangepaste gegevens. De waarde komt overeen met het gekozen type `authenticationDataFields.type`. |
| `authenticationDataFields.authenticationResponsePath` | String | Geeft aan naar welk veld van het API-antwoordpad u verwijst. |

{style="table-layout:auto"}

## Toegang token vernieuwen {#access-token-refresh}

Adobe heeft een systeem ontworpen dat verlopen toegangstokens vernieuwt zonder dat de gebruiker zich weer hoeft aan te melden bij uw platform. Het systeem kan een nieuw token genereren zodat de activering van uw bestemming naadloos voor de klant wordt voortgezet.

Om het teken van de opstellingstoegang te verfrissen zich, kunt u een templatized HTTP- verzoek moeten vormen die Adobe toestaat om een nieuw toegangstoken te krijgen, gebruikend verfrist symbolisch. Als het toegangstoken is verlopen, neemt de Adobe het malplaatjeverzoek dat door u wordt verstrekt, toevoegend de parameters u verstrekte. Gebruik de `accessTokenRequest` parameter om een toegangstoken te vormen verfrist zich mechanisme.


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

U kunt de volgende parameters gebruiken in `accessTokenRequest` om uw token aan te passen vernieuwt proces:

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `accessTokenRequest.destinationServerType` | String | Gebruiken `URL_BASED`. |
| `accessTokenRequest.urlBasedDestination.url.templatingStrategy` | String | <ul><li>Gebruiken `PEBBLE_V1` als u sjablonen gebruikt voor de waarde in `accessTokenRequest.urlBasedDestination.url.value`.</li><li> Gebruiken `NONE` als de waarde in het veld `accessTokenRequest.urlBasedDestination.url.value` is een constante. </li></li> |
| `accessTokenRequest.urlBasedDestination.url.value` | String | De URL waar het Experience Platform om het toegangstoken verzoekt. |
| `accessTokenRequest.httpTemplate.requestBody.templatingStrategy` | String | <ul><li>Gebruiken `PEBBLE_V1` als u sjablonen gebruikt voor de waarden in `accessTokenRequest.httpTemplate.requestBody.value`.</li><li> Gebruiken `NONE` als de waarde in het veld `accessTokenRequest.httpTemplate.requestBody.value` is een constante. </li></li> |
| `accessTokenRequest.httpTemplate.requestBody.value` | String | Gebruik de sjabloontaal om velden in de HTTP-aanvraag aan te passen aan het eindpunt van het toegangstoken. Voor informatie over het gebruik van sjablonen om velden aan te passen, raadpleegt u de [sjabloonconventies](#templating-conventions) sectie. |
| `accessTokenRequest.httpTemplate.httpMethod` | String | Specificeert de methode die van HTTP wordt gebruikt om uw eindpunt van het toegangstoken te roepen. In de meeste gevallen is deze waarde `POST`. |
| `accessTokenRequest.httpTemplate.contentType` | String | Specificeert het inhoudstype van de vraag van HTTP aan uw toegangstoken eindpunt. <br> Bijvoorbeeld: `application/x-www-form-urlencoded` of `application/json`. |
| `accessTokenRequest.httpTemplate.headers` | String | Specificeert als om het even welke kopballen aan de vraag van HTTP aan uw toegangstoken eindpunt zouden moeten worden toegevoegd. |
| `accessTokenRequest.responseFields.templatingStrategy` | String | <ul><li>Gebruiken `PEBBLE_V1` als u sjablonen gebruikt voor de waarden in `accessTokenRequest.responseFields.value`.</li><li> Gebruiken `NONE` als de waarde in het veld `accessTokenRequest.responseFields.value` is een constante. </li></li> |
| `accessTokenRequest.responseFields.value` | String | De malplaatjetaal van het gebruik om tot gebieden in de reactie van HTTP van uw toegangstoken eindpunt toegang te hebben. Voor informatie over het gebruik van sjablonen om velden aan te passen, raadpleegt u de [sjabloonconventies](#templating-conventions) sectie. |
| `accessTokenRequest.validations.name` | String | Geeft de naam aan die u voor deze validatie hebt opgegeven. |
| `accessTokenRequest.validations.actualValue.templatingStrategy` | String | <ul><li>Gebruiken `PEBBLE_V1` als u sjablonen gebruikt voor de waarden in `accessTokenRequest.validations.actualValue.value`.</li><li> Gebruiken `NONE` als de waarde in het veld `accessTokenRequest.validations.actualValue.value` is een constante. </li></li> |
| `accessTokenRequest.validations.actualValue.value` | String | Gebruik een sjabloontaal voor toegang tot velden in de HTTP-respons. Voor informatie over het gebruik van sjablonen om velden aan te passen, raadpleegt u de [sjabloonconventies](#templating-conventions) sectie. |
| `accessTokenRequest.validations.expectedValue.templatingStrategy` | String | <ul><li>Gebruiken `PEBBLE_V1` als u sjablonen gebruikt voor de waarden in `accessTokenRequest.validations.expectedValue.value`.</li><li> Gebruiken `NONE` als de waarde in het veld `accessTokenRequest.validations.expectedValue.value` is een constante. </li></li> |
| `accessTokenRequest.validations.expectedValue.value` | String | Gebruik een sjabloontaal voor toegang tot velden in de HTTP-respons. Voor informatie over het gebruik van sjablonen om velden aan te passen, raadpleegt u de [sjabloonconventies](#templating-conventions) sectie. |

{style="table-layout:auto"}

## Sjabloonconventies {#templating-conventions}

Afhankelijk van de aanpassing van uw toestemming, zou u tot gegevensgebieden in de vergunningsreactie kunnen moeten toegang hebben, zoals aangetoond in de vorige sectie. Om dat te doen, moet u zich vertrouwd maken met de [Taal voor peersjablonen](https://pebbletemplates.io/) gebruikt door Adobe en verwijs naar de malplaatjeovereenkomsten hieronder om uw implementatie van OAuth 2 aan te passen.


| Voorvoegsel | Beschrijving | Voorbeeld |
|---------|----------|---------|
| authData | Heb toegang tot om het even welke partner of waarde van de klantengegevens. | ``{{ authData.accessToken }}`` |
| response.body | HTTP-responsinstantie | ``{{ response.body.access_token }}`` |
| response.status | HTTP-reactiestatus | ``{{ response.status }}`` |
| response.headers | HTTP-antwoordheaders | ``{{ response.headers.server[0] }}`` |
| userContext | Toegang tot informatie over de huidige autorisatiepoging | <ul><li>`{{ userContext.sandboxName }} `</li><li>`{{ userContext.sandboxId }} `</li><li>`{{ userContext.imsOrgId }} `</li><li>`{{ userContext.client }} // the client executing the authorization attempt `</li></ul> |

{style="table-layout:auto"}

## Volgende stappen {#next-steps}

Door dit artikel te lezen, hebt u nu inzicht in de OAuth 2 toestemmingspatronen die door Adobe Experience Platform worden gesteund en weet hoe te om uw bestemming met OAuth 2 vergunningssteun te vormen. Vervolgens kunt u met Destination SDK de OAuth 2-ondersteunde bestemming instellen. Lezen [Gebruik Destination SDK om uw bestemming te vormen](../../guides/configure-destination-instructions.md) voor de volgende stappen.
