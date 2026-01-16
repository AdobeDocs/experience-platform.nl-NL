---
description: Deze pagina beschrijft de diverse OAuth 2 vergunningsstromen die door Destination SDK worden gesteund, en verstrekt instructies aan opstelling OAuth 2 vergunning voor uw bestemming.
title: OAuth 2-vergunning
exl-id: 280ecb63-5739-491c-b539-3c62bd74e433
source-git-commit: 720f599810d119ac4997d24d400199d8efe087c2
workflow-type: tm+mt
source-wordcount: '2273'
ht-degree: 0%

---


# OAuth 2-vergunning

Destination SDK ondersteunt verschillende machtigingsmethoden voor uw bestemming. Onder deze is de optie om aan uw bestemming voor authentiek te verklaren door het [ OAuth 2 vergunningskader ](https://tools.ietf.org/html/rfc6749) te gebruiken.

Deze pagina beschrijft de diverse OAuth 2 vergunningsstromen die door Destination SDK worden gesteund, en verstrekt instructies aan opstelling OAuth 2 vergunning voor uw bestemming.

>[!IMPORTANT]
>
>Alle parameternamen en waarden die door Destination SDK worden gesteund zijn **gevoelig geval**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Ondersteunde integratietypen {#supported-integration-types}

Raadpleeg de onderstaande tabel voor meer informatie over de integratietypen die de op deze pagina beschreven functionaliteit ondersteunen.

| Type integratie | Ondersteunt functionaliteit |
|---|---|
| Integraties in realtime (streaming) | Ja |
| Op bestanden gebaseerde (batch) integratie | Nee |

## Hoe te om OAuth 2 vergunningsdetails aan uw bestemmingsconfiguratie toe te voegen {#how-to-setup}

### Vereisten in uw systeem {#prerequisites}

Als eerste stap moet u in uw systeem een app voor Adobe Experience Platform maken of Experience Platform op een andere manier in uw systeem registreren. Het doel is een cliënt-identiteitskaart en cliëntgeheim te produceren, die nodig zijn om Experience Platform aan uw bestemming voor authentiek te verklaren.

Als onderdeel van deze configuratie in uw systeem hebt u de Adobe Experience Platform OAuth 2 omleiding/callback-URL&#39;s nodig, die u uit de onderstaande lijst kunt halen.

* `https://platform-va7.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-nld2.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-aus5.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-can2.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-gbr9.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform.adobe.io/data/core/activation/oauth/api/v1/callback`

>[!IMPORTANT]
>
>De stap om een redirect/callback URL voor Adobe Experience Platform in uw systeem te registreren wordt vereist slechts voor [ OAuth 2 met het type van de toelage van de Code van de Toestemming ](#authorization-code). Voor de andere twee gesteunde subsidietypes (wachtwoord en cliëntgeloofsbrieven), kunt u deze stap overslaan.

Aan het eind van deze stap, zou u moeten hebben:

* een client-id;
* een clientgeheim;
* Adobe callback-URL (voor de autorisatiecode-subsidie).

### Wat je moet doen in Destination SDK {#to-do-in-destination-sdk}

Aan opstelling OAuth 2 vergunning voor uw bestemming in Experience Platform, moet u uw OAuth 2 details aan de [ bestemmingsconfiguratie ](../../authoring-api/destination-configuration/create-destination-configuration.md) toevoegen, onder de `customerAuthenticationConfigurations` parameter. Zie [ klantenauthentificatie ](../../functionality/destination-configuration/customer-authentication.md) voor gedetailleerde voorbeelden. Specifieke instructies over welke gebieden u aan uw configuratiemalplaatje, afhankelijk van uw OAuth 2 type van vergunningsvergunning moet toevoegen, zijn verder hieronder op deze pagina.

## Ondersteunde OAuth 2-subsidietypen {#oauth2-grant-types}

Experience Platform ondersteunt de drie OAuth 2-subsidietypen in de onderstaande tabel. Als u een aangepaste OAuth 2-instelling hebt, kan Adobe deze ondersteunen met behulp van aangepaste velden in uw integratie. Raadpleeg de secties voor elk type subsidie voor meer informatie.

>[!IMPORTANT]
>
>* U geeft de invoerparameters op volgens de instructies in de onderstaande secties. Adobe-interne systemen maken verbinding met het autorisatiesysteem van uw platform en nemen uitvoerparameters op, die worden gebruikt om de gebruiker te verifiëren en de autorisatie naar uw bestemming te behouden.
>* De invoerparameters die in de tabel vet worden gemarkeerd, zijn vereiste parameters in de OAuth 2-autorisatiestroom. De andere parameters zijn optioneel. Er zijn andere parameters van de douaneinput die niet hier worden getoond, maar bij lengte in de secties [ worden beschreven aanpassen uw configuratie OAuth 2 ](#customize-configuration) en [ het teken van de Toegang verfrist zich ](#access-token-refresh).

| OAuth 2 Grant | Invoer | Uitvoer |
|---------|----------|---------|
| Autorisatiecode | <ul><li><b> clientId </b></li><li><b> clientSecret </b></li><li>bereik</li><li><b> authenticationUrl </b></li><li><b> accessTokenUrl </b></li><li>refreshTokenUrl</li></ul> | <ul><li><b> accessToken </b></li><li>expiredIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Wachtwoord | <ul><li><b> clientId </b></li><li><b> clientSecret </b></li><li>bereik</li><li><b> accessTokenUrl </b></li><li><b> gebruikersbenaming </b></li><li><b> wachtwoord </b></li></ul> | <ul><li><b> accessToken </b></li><li>expiredIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Client Credential | <ul><li><b> clientId </b></li><li><b> clientSecret </b></li><li>bereik</li><li><b> accessTokenUrl </b></li></ul> | <ul><li><b> accessToken </b></li><li>expiredIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

De bovenstaande tabel bevat een lijst met velden die worden gebruikt in standaard OAuth 2-stromen. Naast deze standaardgebieden, kunnen diverse partnerintegraties extra input en output vereisen. Adobe heeft een flexibel OAuth 2-machtigingskader voor Destination SDK ontworpen dat wijzigingen in het bovenstaande standaardveldpatroon kan verwerken en een mechanisme ondersteunt om automatisch ongeldige uitvoer te genereren, zoals verlopen toegangstokens.

De uitvoer bevat in alle gevallen een toegangstoken dat door Experience Platform wordt gebruikt voor verificatie en handhaving van de autorisatie voor uw bestemming.

Het systeem dat Adobe heeft ontworpen voor OAuth 2-autorisatie:

* Ondersteunt alle drie OAuth 2-subsidies en verwerkt eventuele variaties in deze subsidies, zoals extra gegevensvelden, niet-standaard API-aanroepen en meer.
* Ondersteunt toegangstokens met variërende levenwaarden. Adobe raadt u aan de waarde van uw token-levensduur in te stellen op minimaal 24 uur.
* Ondersteunt OAuth 2-machtigingsstromen met of zonder tokens vernieuwen.

## OAuth 2 met vergunningscode {#authorization-code}

Als uw bestemming een standaardOAuth 2.0 stroom van de Code van de Vergunning steunt (lees de [ RFC normen specs ](https://tools.ietf.org/html/rfc6749#section-4.1)) of een variatie van het, raadpleeg de vereiste en facultatieve hieronder gebieden:

| OAuth 2 Grant | Invoer | Uitvoer |
|---------|----------|---------|
| Autorisatiecode | <ul><li><b> clientId </b></li><li><b> clientSecret </b></li><li>bereik</li><li><b> authenticationUrl </b></li><li><b> accessTokenUrl </b></li><li>refreshTokenUrl</li></ul> | <ul><li><b> accessToken </b></li><li>expiredIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

Aan opstelling deze vergunningsmethode voor uw bestemming, voeg de volgende lijnen aan uw configuratie toe, wanneer u [ een bestemmingsconfiguratie ](../../authoring-api/destination-configuration/create-destination-configuration.md) creeert:

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
      "scope": ["read", "write"],
      "options": {
          "useBasicAuth": true 
      }
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
| `refreshTokenUrl` | String | *Facultatief.* De URL aan uw zijde, die vernieuwt tokens uitgeeft. Vaak is de waarde van `refreshTokenUrl` gelijk aan die van `accessTokenUrl` . |
| `clientId` | String | De client-id die door uw systeem aan Adobe Experience Platform wordt toegewezen. |
| `clientSecret` | String | Het clientgeheim dat uw systeem aan Adobe Experience Platform toewijst. |
| `scope` | Lijst met tekenreeksen | *Facultatief*. Plaats het werkingsgebied van wat het toegangstoken Experience Platform toestaat om op uw middelen uit te voeren. Voorbeeld: &quot;read, write&quot;. |
| `options.useBasicAuth` | Boolean | *Facultatief*. Een booleaanse waarde die controleert hoe de cliëntgeloofsbrieven (cliënt identiteitskaart en cliëntgeheim) naar het symbolische eindpunt van de leverancier OAuth wanneer het ruilen van een vergunningscode voor een toegangstoken worden verzonden. <ul><li>Indien ingesteld op `false` of ongedefinieerd, worden de gegevens verzonden als `client_id` - en `client_secret` -parameters in de hoofdtekst van de POST-aanvraag (standaardgedrag).</li><li>Als deze parameter is ingesteld op `true` , worden de gegevens verzonden in de HTTP `Authorization` -header met de indeling Basisverificatie: `Authorization: Basic base64(clientID:clientSecret)` .</li></ul> Stel `useBasicAuth` in op `true` wanneer uw OAuth-provider vereist dat clientgegevens worden verzonden in de `Authorization` -header in plaats van in de aanvraagtekst. |

{style="table-layout:auto"}

## OAuth 2 with Password Grant

Voor OAuth 2 de subsidie van het Wachtwoord (lees de [ RFC normen specs ](https://tools.ietf.org/html/rfc6749#section-4.3)), vereist Experience Platform de gebruikersbenaming en het wachtwoord van de gebruiker. In de vergunningsstroom, ruilt Experience Platform deze geloofsbrieven voor een toegangstoken en, naar keuze, verfrist teken.
Adobe maakt gebruik van de standaardinvoer hieronder om de configuratie van de bestemming te vereenvoudigen, met de mogelijkheid om waarden te overschrijven:

| OAuth 2 Grant | Invoer | Uitvoer |
|---------|----------|---------|
| Wachtwoord | <ul><li><b> clientId </b></li><li><b> clientSecret </b></li><li>bereik</li><li><b> accessTokenUrl </b></li><li><b> gebruikersbenaming </b></li><li><b> wachtwoord </b></li></ul> | <ul><li><b> accessToken </b></li><li>expiredIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

>[!NOTE]
>
> U hoeft geen parameters voor `username` en `password` toe te voegen in de onderstaande configuratie. Wanneer u `"grant": "OAUTH2_PASSWORD"` toevoegt in de doelconfiguratie, vraagt het systeem de gebruiker een gebruikersnaam en wachtwoord op te geven in de Experience Platform-gebruikersinterface wanneer deze wordt geverifieerd op uw bestemming.

Aan opstelling deze vergunningsmethode voor uw bestemming, voeg de volgende lijnen aan uw configuratie toe, wanneer u [ een bestemmingsconfiguratie ](../../authoring-api/destination-configuration/create-destination-configuration.md) creeert:

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
| `scope` | Lijst met tekenreeksen | *Facultatief*. Plaats het werkingsgebied van wat het toegangstoken Experience Platform toestaat om op uw middelen uit te voeren. Voorbeeld: &quot;read, write&quot;. |

{style="table-layout:auto"}

## OAuth 2 met Client Credentials Grant

U kunt een OAuth 2 Credentials van de Cliënt vormen (lees de [ RFC normen specs ](https://tools.ietf.org/html/rfc6749#section-4.4)) bestemming, die de hieronder vermelde standaardinput en output steunt. U kunt de waarden aanpassen. Zie [ uw OAuth 2 configuratie ](#customize-configuration) voor details aanpassen.

| OAuth 2 Grant | Invoer | Uitvoer |
|---------|----------|---------|
| Client Credentials | <ul><li><b> clientId </b></li><li><b> clientSecret </b></li><li>bereik</li><li><b> accessTokenUrl </b></li></ul> | <ul><li><b> accessToken </b></li><li>expiredIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

Aan opstelling deze vergunningsmethode voor uw bestemming, voeg de volgende lijnen aan uw configuratie toe, wanneer u [ een bestemmingsconfiguratie ](../../authoring-api/destination-configuration/create-destination-configuration.md) creeert:

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
| `refreshTokenUrl` | String | *Facultatief.* De URL aan uw zijde, die vernieuwt tokens uitgeeft. Vaak is de waarde van `refreshTokenUrl` gelijk aan die van `accessTokenUrl` . |
| `clientId` | String | De client-id die door uw systeem aan Adobe Experience Platform wordt toegewezen. |
| `clientSecret` | String | Het clientgeheim dat uw systeem aan Adobe Experience Platform toewijst. |
| `scope` | Lijst met tekenreeksen | *Facultatief*. Plaats het werkingsgebied van wat het toegangstoken Experience Platform toestaat om op uw middelen uit te voeren. Voorbeeld: &quot;read, write&quot;. |

{style="table-layout:auto"}

## Uw OAuth 2-configuratie aanpassen {#customize-configuration}

De configuraties die in de bovenstaande secties worden beschreven, beschrijven standaard OAuth 2-subsidies. Nochtans, verstrekt het systeem dat door Adobe wordt ontworpen flexibiliteit zodat kunt u douaneparameters voor om het even welke variaties in OAuth 2 subsidie gebruiken. Als u de standaard OAuth 2-instellingen wilt aanpassen, gebruikt u de `authenticationDataFields` -parameters, zoals in de onderstaande voorbeelden wordt getoond.

### Voorbeeld 1: `authenticationDataFields` gebruiken voor het vastleggen van informatie die afkomstig is van het antwoord op de machtiging {#example-1}

In dit voorbeeld, heeft een bestemmingsplatform tokens verfrissen die na een bepaalde hoeveelheid tijd verlopen. In dit geval stelt de partner het aangepaste veld `refreshTokenExpiration` zo in dat de vervaldatum van het vernieuwingstoken wordt opgehaald uit het veld `refresh_token_expires_in` in de API-reactie.

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

### Voorbeeld 2: met `authenticationDataFields` een speciaal vernieuwingstoken maken {#example-2}

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

In dit voorbeeld, in plaats van het creëren van een globale cliëntidentiteitskaart en cliëntgeheim zoals aangetoond in de sectie [ Eerste vereisten in uw systeem ](#prerequisites), wordt de klant vereist om cliëntidentiteitskaart, cliëntgeheim, en rekeningsidentiteitskaart (identiteitskaart in te voeren die de klant gebruikt om in de bestemming te registreren)

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



U kunt de volgende parameters in `authenticationDataFields` gebruiken om uw configuratie aan te passen OAuth 2:

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `authenticationDataFields.name` | String | De naam van het aangepaste veld. |
| `authenticationDataFields.title` | String | Een titel die u voor het aangepaste veld kunt opgeven. |
| `authenticationDataFields.description` | String | Een beschrijving van het aangepaste gegevensveld dat u hebt ingesteld. |
| `authenticationDataFields.type` | String | Hiermee definieert u het type van het veld Aangepaste gegevens. <br> Geaccepteerde waarden: `string` , `boolean` , `integer` |
| `authenticationDataFields.isRequired` | Boolean | Geeft aan of het veld met aangepaste gegevens is vereist in de machtigingsstroom. |
| `authenticationDataFields.format` | String | Wanneer u `"format":"password"` selecteert, versleutelt Adobe de waarde van het veld met machtigingsgegevens. Bij gebruik met `"fieldType": "CUSTOMER"` wordt hiermee ook de invoer in de gebruikersinterface verborgen wanneer de gebruiker in het veld typt. |
| `authenticationDataFields.fieldType` | String | Geeft aan of de invoer afkomstig is van de partner (u) of van de gebruiker, wanneer deze uw bestemming in Experience Platform instelt. |
| `authenticationDataFields.value` | String. Booleaans. Geheel | De waarde van het veld met aangepaste gegevens. De waarde komt overeen met het gekozen type uit `authenticationDataFields.type` . |
| `authenticationDataFields.authenticationResponsePath` | String | Geeft aan naar welk veld van het API-antwoordpad u verwijst. |

{style="table-layout:auto"}

## Toegang token vernieuwen {#access-token-refresh}

Adobe heeft een systeem ontworpen waarmee verlopen toegangstokens worden vernieuwd zonder dat de gebruiker zich weer hoeft aan te melden bij uw platform. Het systeem kan een nieuw token genereren zodat de activering van uw bestemming naadloos voor de klant wordt voortgezet.

Om het teken van de opstellingstoegang te verfrissen zich, kunt u een templatized HTTP- verzoek moeten vormen die Adobe toestaat om een nieuw toegangstoken te krijgen, gebruikend verfrist symbolisch. Als het toegangstoken is verlopen, neemt Adobe het sjabloonverzoek dat door u wordt verstrekt, toevoegend de parameters u verstrekte. Gebruik de parameter `accessTokenRequest` om een toegangstoken te vormen verfrist zich mechanisme.


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
| `accessTokenRequest.destinationServerType` | String | Gebruik `URL_BASED` . |
| `accessTokenRequest.urlBasedDestination.url.templatingStrategy` | String | <ul><li>Gebruik `PEBBLE_V1` als u sjablonen voor de waarde in `accessTokenRequest.urlBasedDestination.url.value` gebruikt.</li><li> Gebruik `NONE` als de waarde in het veld `accessTokenRequest.urlBasedDestination.url.value` een constante is. </li></li> |
| `accessTokenRequest.urlBasedDestination.url.value` | String | De URL waar Experience Platform om het toegangstoken vraagt. |
| `accessTokenRequest.httpTemplate.requestBody.templatingStrategy` | String | <ul><li>Gebruik `PEBBLE_V1` als u sjablonen gebruikt voor de waarden in `accessTokenRequest.httpTemplate.requestBody.value` .</li><li> Gebruik `NONE` als de waarde in het veld `accessTokenRequest.httpTemplate.requestBody.value` een constante is. </li></li> |
| `accessTokenRequest.httpTemplate.requestBody.value` | String | Gebruik de sjabloontaal om velden in de HTTP-aanvraag aan te passen aan het eindpunt van het toegangstoken. Voor informatie over hoe te om het templating te gebruiken om gebieden aan te passen, verwijs naar de [ sectie van de overeenkomsten van de 0} malplaatjemeting {.](#templating-conventions) |
| `accessTokenRequest.httpTemplate.httpMethod` | String | Specificeert de methode die van HTTP wordt gebruikt om uw eindpunt van het toegangstoken te roepen. In de meeste gevallen is deze waarde `POST` . |
| `accessTokenRequest.httpTemplate.contentType` | String | Specificeert het inhoudstype van de vraag van HTTP aan uw toegangstoken eindpunt. <br> Bijvoorbeeld: `application/x-www-form-urlencoded` of `application/json` . |
| `accessTokenRequest.httpTemplate.headers` | String | Specificeert als om het even welke kopballen aan de vraag van HTTP aan uw toegangstoken eindpunt zouden moeten worden toegevoegd. |
| `accessTokenRequest.responseFields.templatingStrategy` | String | <ul><li>Gebruik `PEBBLE_V1` als u sjablonen gebruikt voor de waarden in `accessTokenRequest.responseFields.value` .</li><li> Gebruik `NONE` als de waarde in het veld `accessTokenRequest.responseFields.value` een constante is. </li></li> |
| `accessTokenRequest.responseFields.value` | String | De malplaatjetaal van het gebruik om tot gebieden in de reactie van HTTP van uw toegangstoken eindpunt toegang te hebben. Voor informatie over hoe te om het templating te gebruiken om gebieden aan te passen, verwijs naar de [ sectie van de overeenkomsten van de 0} malplaatjemeting {.](#templating-conventions) |
| `accessTokenRequest.validations.name` | String | Geeft de naam aan die u voor deze validatie hebt opgegeven. |
| `accessTokenRequest.validations.actualValue.templatingStrategy` | String | <ul><li>Gebruik `PEBBLE_V1` als u sjablonen gebruikt voor de waarden in `accessTokenRequest.validations.actualValue.value` .</li><li> Gebruik `NONE` als de waarde in het veld `accessTokenRequest.validations.actualValue.value` een constante is. </li></li> |
| `accessTokenRequest.validations.actualValue.value` | String | Gebruik een sjabloontaal voor toegang tot velden in de HTTP-respons. Voor informatie over hoe te om het templating te gebruiken om gebieden aan te passen, verwijs naar de [ sectie van de overeenkomsten van de 0} malplaatjemeting {.](#templating-conventions) |
| `accessTokenRequest.validations.expectedValue.templatingStrategy` | String | <ul><li>Gebruik `PEBBLE_V1` als u sjablonen gebruikt voor de waarden in `accessTokenRequest.validations.expectedValue.value` .</li><li> Gebruik `NONE` als de waarde in het veld `accessTokenRequest.validations.expectedValue.value` een constante is. </li></li> |
| `accessTokenRequest.validations.expectedValue.value` | String | Gebruik een sjabloontaal voor toegang tot velden in de HTTP-respons. Voor informatie over hoe te om het templating te gebruiken om gebieden aan te passen, verwijs naar de [ sectie van de overeenkomsten van de 0} malplaatjemeting {.](#templating-conventions) |

{style="table-layout:auto"}

## Sjabloonconventies {#templating-conventions}

Afhankelijk van de aanpassing van uw toestemming, zou u tot gegevensgebieden in de vergunningsreactie kunnen moeten toegang hebben, zoals aangetoond in de vorige sectie. Om dat te doen, gelieve zich met de [ Pebble het trillen taal ](https://pebbletemplates.io/) vertrouwd te maken die door Adobe wordt gebruikt en naar de malplaatjeovereenkomsten hieronder te verwijzen om uw OAuth 2 implementatie aan te passen.


| Voorvoegsel | Beschrijving | Voorbeeld |
|---------|----------|---------|
| authData | Heb toegang tot om het even welke partner of waarde van de klantengegevens. | `{{ authData.accessToken }}` |
| response.body | HTTP-responsinstantie | `{{ response.body.access_token }}` |
| response.status | HTTP-reactiestatus | `{{ response.status }}` |
| response.headers | HTTP-antwoordheaders | `{{ response.headers.server[0] }}` |
| userContext | Toegang tot informatie over de huidige autorisatiepoging | <ul><li>`{{ userContext.sandboxName }}`</li><li>`{{ userContext.sandboxId }}`</li><li>`{{ userContext.imsOrgId }}`</li><li>`{{ userContext.client }} // the client executing the authorization attempt`</li></ul> |

{style="table-layout:auto"}

## Volgende stappen {#next-steps}

Door dit artikel te lezen, hebt u nu inzicht in de OAuth 2 toestemmingspatronen die door Adobe Experience Platform worden gesteund en weet hoe te om uw bestemming met OAuth 2 vergunningssteun te vormen. Vervolgens kunt u Destination SDK gebruiken om uw door OAuth 2 ondersteunde bestemming in te stellen. Lees [ Destination SDK van het Gebruik om uw bestemming ](../../guides/configure-destination-instructions.md) voor volgende stappen te vormen.
