---
description: Op deze pagina worden alle API-bewerkingen beschreven die u kunt uitvoeren met het API-eindpunt `/authoring/credentials`.
title: API-bewerkingen van het eindpunt Credentials
source-git-commit: 19307fba8f722babe5b6d57e80735ffde00fc851
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 2%

---

# API-bewerkingen van het eindpunt Credentials {#credentials}

>[!IMPORTANT]
>
>**API-eindpunt**:  `platform.adobe.io/data/core/activation/authoring/credentials`

Deze pagina bevat een overzicht en beschrijving van alle API-bewerkingen die u kunt uitvoeren met het API-eindpunt `/authoring/credentials`.

## Wanneer wordt het API-eindpunt `/credentials` gebruikt {#when-to-use}

>[!IMPORTANT]
>
>In de meeste gevallen hoeft u *niet* het API-eindpunt `/credentials` te gebruiken. In plaats daarvan, kunt u de authentificatieinformatie voor uw bestemming via de `customerAuthenticationConfigurations` parameters van het `/destinations` eindpunt vormen. Lees [Credentials configuration](./credentials-configuration.md) voor meer informatie.

Gebruik dit API-eindpunt en selecteer `PLATFORM_AUTHENTICATION` in de [doelconfiguratie](./destination-configuration.md#destination-delivery) als er een wereldwijd verificatiesysteem tussen Adobe en uw bestemming is en de [!DNL Platform]-klant geen verificatiegegevens hoeft op te geven om verbinding te maken met uw bestemming. In dit geval moet u een aanmeldingsobject maken met het API-eindpunt `/credentials`.

<!--

Commenting out the example configurations

## Example configurations

**Example configuration for a Basic authentication credential configuration with username and password**

```json
{
  "type": "BASIC",
  "name": "YOUR_DESTINATION_NAME",
  "basicAuthentication": {
    "username": "YOUR_DESTINATION_SERVER_USERNAME",
    "password": "YOUR_DESTINATION_SERVER_PASSWORD"
  }
}

```

**Example configuration for an OAuth2 credential configuration**

```json

{
  "oauth2AccessTokenAuthentication": {
    "accessToken": "YOUR_DESTINATION_SERVER_ACCESS_TOKEN",
    "expiration": "YOUR_TOKEN_TIME_TO_LIVE",
    "username": "YOUR_DESTINATION_SERVER_USERNAME",
    "userId": "YOUR_DESTINATION_USER_ID",
    "url": "AUTHORIZATION_PROVIDER_URL",
    "header": "YOUR_AUTHORIZATION_HEADER"
  }
}

```

The sections below list out the necessary parameters for each authentication type. Let us know which authentication type your server uses and provide us with the relevant information for your server type.

## Basic authentication

|Parameter | Type | Description|
|---------|----------|------|
|`username` | String | credentials configuration login username |
|`password` | String | credentials configuration login password |



// commenting out this part as these types of authentication methods are not supported in phase one

### S3 authentication

|Parameter | Type | Description|
|---------|----------|------|
|accessId | String | credentials configuration S3 credential Access key ID |
|secretKey | String | credentials configuration S3 credential Secret key |

### SSH 

|Parameter | Type | Description|
|---------|----------|------|
|username | String | credentials configuration SSH username |
|SSHKey | String | credentials configuration SSH key |



## OAuth1

|Parameter | Type | Description|
|---------|----------|------|
|`apiKey` | String | A value used by the Destinations Service to identify itself to the Service Provider. |
|`apiSecret` | String | Secret used by the Destinations Service to establish ownership of the API key to the Service Provider. |
|`acccessToken` | String | A value used by the Destinations Service to gain access to the Protected Resources on behalf of the User |
|`tokenSecret` | String | A secret used by the Destinations Service to establish ownership of an access token. |

## OAuth2 user credentials

|Parameter | Type | Description|
|---------|----------|------|
|`clientId` | String | Client ID of Client/Application credential |
|`clientSecret` | String | Client secret of Client/Application credential |
|`username` | String | The user's username to log on to your platform. |
|`password` | String | The user's password to log on to your platform. |
|`url` | String | URL of authorization provider |
|`header` | String | Any header required for authorization |

## OAuth2 client credentials

|Parameter | Type | Description|
|---------|----------|------|
|`clientId` | String | Client ID of Client/Application credential |
|`clientSecret` | String | Client secret of Client/Application credential |
|`username`| String | URL of authorization provider |
|`password` | String | Any header required for authorization |

## OAuth2 access token

|Parameter | Type | Description|
|---------|----------|------|
|`accessToken` | String | Access token provided by the authorization provider |
|`expiration` | String | The time-to-live for the access token |
|`username` | String | The user's username to log on to your platform. |
|`userId` | String | The user's ID with your platform. |
|`url` | String | URL of authorization provider |
|`header` | String | Any header required for authorization |

## OAuth2 refresh token

|Parameter | Type | Description|
|---------|----------|------|
|`clientId` | String | Client ID of Client/Application credential |
|`clientSecret` | String | Client secret of Client/Application credential |
|`refreshToken` | String | Refresh token provided by the authorization provider |
|`url` | String | URL of authorization provider |
|`expiration` | String | The time-to-live for the refresh token |
|`header` | String | Any header required for authorization |

-->

## Aan de slag met API-bewerkingen voor aanmeldingsconfiguratie {#get-started}

Alvorens verder te gaan, te herzien [begonnen gids](./getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmingsauteur en vereiste kopballen te verkrijgen.

## Een verificatieconfiguratie maken {#create}

U kunt een nieuwe geloofsgeloofsconfiguratie tot stand brengen door een verzoek van de POST aan het `/authoring/credentials` eindpunt te doen.

**API-indeling**


```http
POST /authoring/credentials
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe geloofsgeloofsconfiguratie, die door de parameters wordt gevormd die in de lading worden verstrekt. De hieronder vermelde lading omvat alle parameters die door het `/authoring/credentials` eindpunt worden goedgekeurd. Merk op dat u niet alle parameters op de vraag moet toevoegen en dat het malplaatje, volgens uw API vereisten aanpasbaar is.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "oauth2UserAuthentication":{
      "url":"string",
      "clientId":"string",
      "clientSecret":"string",
      "username":"string",
      "password":"string",
      "header":"string"
   },
   "oauth2ClientAuthentication":{
      "url":"string",
      "clientId":"string",
      "clientSecret":"string",
      "header":"string",
      "developerToken":"string"
   },
   "oauth2AccessTokenAuthentication":{
      "accessToken":"string",
      "expiration":"string",
      "username":"string",
      "userId":"string",
      "url":"string",
      "header":"string"
   },
   "oauth2RefreshTokenAuthentication":{
      "refreshToken":"string",
      "expiration":"string",
      "clientId":"string",
      "clientSecret":"string",
      "url":"string",
      "header":"string"
   }
}
```

| Parameter | Type | Beschrijving |
| -------- | ----------- | ----------- |
| `username` | Tekenreeks | aanmeldingsgebruikersnaam voor gebruikersconfiguratie |
| `password` | Tekenreeks | aanmeldingswachtwoord voor gebruikersconfiguratie |
| `url` | Tekenreeks | URL van leverancier van autorisaties |
| `clientId` | Tekenreeks | Client-id van client/toepassingsreferentie |
| `clientSecret` | Tekenreeks | Clientgeheim van client/toepassingsreferentie |
| `accessToken` | Tekenreeks | Toegangstoken verstrekt door de vergunningverlener |
| `expiration` | Tekenreeks | De time-to-live voor het toegangstoken |
| `refreshToken` | Tekenreeks | Token vernieuwen die door de leverancier van de vergunning worden verstrekt |
| `header` | Tekenreeks | Alle kopteksten die vereist zijn voor autorisatie |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde geloofsgeloofsconfiguratie terug.

## Configuraties van lijstreferenties {#retrieve-list}

U kunt een lijst van alle geloofsbrieven configuraties voor uw IMS Organisatie terugwinnen door een verzoek van de GET aan het `/authoring/credentials` eindpunt te doen.

**API-indeling**


```http
GET /authoring/credentials
```

**Verzoek**

Het volgende verzoek zal de lijst van geloofsgeloofsconfiguraties terugwinnen die u toegang tot hebt, op organisatie IMS en zandbakconfiguratie wordt gebaseerd.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

De volgende reactie retourneert HTTP-status 200 met een lijst van aanmeldingsconfiguraties waartoe u toegang hebt, op basis van de IMS-organisatie-id en de sandboxnaam die u hebt gebruikt. Één `instanceId` beantwoordt aan het malplaatje voor één geloofsgeloofsconfiguratie. De reactie is afgebroken voor de beknoptheid.

```json
{
   "items":[
      {
         "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
         "createdDate":"2021-06-07T06:41:48.641943Z",
         "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
         "type":"OAUTH2_USER_CREDENTIAL",
         "name":"yourdestination",
         "oauth2UserAuthentication":{
            "url":"ABCD",
            "clientId":"ABCDEFGHIJKL",
            "clientSecret":"clientsecret",
            "username":"username",
            "password":"password",
            "header":"header"
         }
      }
   ]
}
    
```

## Een bestaande aanmeldingsconfiguratie bijwerken {#update}

U kunt een bestaande geloofsgeloofsconfiguratie bijwerken door een verzoek van de PUT aan het `/authoring/credentials` eindpunt en het verstrekken van instanceID van de geloofsbrieven configuratie te doen u wilt bijwerken. In het lichaam van de vraag, verstrek de bijgewerkte geloofsgeloofsconfiguratie.

**API-indeling**


```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{INSTANCE_ID}` | De id van de aanmeldingsconfiguratie die u wilt bijwerken. |

**Verzoek**

Het volgende verzoek werkt een bestaande geloofsgeloofsconfiguratie bij, die door de parameters wordt gevormd die in de lading worden verstrekt.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"OAUTH2_USER_CREDENTIAL",
   "name":"yourdestination",
   "oauth2UserAuthentication":{
      "url":"ABCD",
      "clientId":"ABCDEFGHIJKL",
      "clientSecret":"clientsecret",
      "username":"username",
      "password":"password",
      "header":"header"
   }
}
```





## Haal een specifieke geloofsbrieven configuratie terug {#get}

U kunt gedetailleerde informatie over een specifieke geloofsbrieven configuratie terugwinnen door een verzoek van de GET tot het `/authoring/credentials` eindpunt te richten en instantieidentiteitskaart van de geloofsbrieven te verstrekken configuratie u wilt bijwerken.

**API-indeling**


```http
GET /authoring/credentials/{INSTANCE_ID}
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{INSTANCE_ID}` | Identiteitskaart van de geloofsconfiguratie u wilt terugwinnen. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met gedetailleerde informatie over de gespecificeerde geloofsgeloofsconfiguratie terug.

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"OAUTH2_USER_CREDENTIAL",
   "name":"yourdestination",
   "oauth2UserAuthentication":{
      "url":"ABCD",
      "clientId":"ABCDEFGHIJKL",
      "clientSecret":"clientsecret",
      "username":"username",
      "password":"password",
      "header":"header"
   }
}
```


## Een specifieke aanmeldingsconfiguratie verwijderen {#delete}

U kunt de gespecificeerde geloofsgeloofsconfiguratie schrappen door een verzoek van DELETE aan het `/authoring/credentials` eindpunt te doen en identiteitskaart van de geloofsgeloofsconfiguratie te verstrekken u wenst om in de verzoekweg te schrappen.

**API-indeling**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{INSTANCE_ID}` | `id` van de geloofsbrieven configuratie u wilt schrappen. |

**Verzoek**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 samen met een lege HTTP-respons.

## API-foutafhandeling

De eindpunten van SDK API van de bestemming volgen de algemene API van het Experience Platform foutenmeldingsbeginselen. Raadpleeg [API-statuscodes](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) en [headerfouten aanvragen](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) in de handleiding voor het oplossen van Platforms.

## Volgende stappen

Na het lezen van dit document, weet u nu wanneer om het geloofsverbindendtepunt te gebruiken en hoe te opstelling een geloofsgeloofsconfiguratie gebruikend het `/authoring/credentials` API eindpunt of het `/authoring/destinations` eindpunt. Lees [hoe te om Doel SDK te gebruiken om uw bestemming te vormen](./configure-destination-instructions.md) om te begrijpen waar deze stap in het proces past om uw bestemming te vormen.
