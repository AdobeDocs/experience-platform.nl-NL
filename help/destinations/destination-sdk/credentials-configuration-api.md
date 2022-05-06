---
description: Op deze pagina worden alle API-bewerkingen beschreven die u kunt uitvoeren met het API-eindpunt `/authoring/credentials`.
title: API-bewerkingen van het eindpunt Credentials
exl-id: 89957f38-e7f4-452d-abc0-0940472103fe
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 2%

---

# API-bewerkingen van het eindpunt Credentials {#credentials}

>[!IMPORTANT]
>
>**API-eindpunt**: `platform.adobe.io/data/core/activation/authoring/credentials`

Deze pagina bevat een overzicht en beschrijving van alle API-bewerkingen die u kunt uitvoeren met de `/authoring/credentials` API-eindpunt.

Voor een beschrijving van de functionaliteit die door dit eindpunt wordt gesteund, lees:

* [Streaming doelconfiguratie](destination-configuration.md) voor de functionaliteit kunt u voor het stromen bestemmingen vormen.
* [Bestandsgebaseerde doelconfiguratie](file-based-destination-configuration.md) voor de functionaliteit kunt u voor op dossier-gebaseerde bestemmingen vormen.

## Wanneer gebruikt u de `/credentials` API-eindpunt {#when-to-use}

>[!IMPORTANT]
>
>In de meeste gevallen *niet* de `/credentials` API-eindpunt. In plaats daarvan, kunt u de authentificatieinformatie voor uw bestemming via vormen `customerAuthenticationConfigurations` parameters van de `/destinations` eindpunt. Lezen [Verificatieconfiguratie](./authentication-configuration.md#when-to-use) voor meer informatie .

Gebruik dit API-eindpunt en selecteer `PLATFORM_AUTHENTICATION` in de [doelconfiguratie](./destination-configuration.md#destination-delivery) als er een globaal authentificatiesysteem tussen Adobe en uw bestemming en is [!DNL Platform] de klant te hoeven om geen authentificatiegeloofsbrieven te verstrekken om met uw bestemming te verbinden. In dit geval moet u een object credentials maken met de opdracht `/credentials` API-eindpunt.

## Aan de slag met API-bewerkingen voor aanmeldingsconfiguratie {#get-started}

Controleer voordat je doorgaat de [gids Aan de slag](./getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings creatie en vereiste kopballen te verkrijgen.

## Een verificatieconfiguratie maken {#create}

U kunt een nieuwe geloofsgeloofsconfiguratie tot stand brengen door een verzoek van de POST aan `/authoring/credentials` eindpunt.

**API-indeling**

```http
POST /authoring/credentials
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe geloofsgeloofsconfiguratie, die door de parameters wordt gevormd die in de lading worden verstrekt. De hieronder vermelde lading omvat alle parameters die door `/authoring/credentials` eindpunt. Merk op dat u niet alle parameters op de vraag moet toevoegen en dat het malplaatje, volgens uw API vereisten aanpasbaar is.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
   },
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   },
   "sshAuthentication":{
      "username":"string",
      "sshKey":"string"
   },
   "azureAuthentication":{
      "url":"string",
      "tenant":"string",
      "servicePrincipalId":"string",
      "servicePrincipalKey":"string"
   },
   "azureConnectionStringAuthentication":{
      "connectionString":"string"
   },
   "basicAuthentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

| Parameter | Type | Beschrijving |
| -------- | ----------- | ----------- |
| `username` | Tekenreeks | Gebruikersnaam aanmeldnaam voor configuratie van referenties |
| `password` | Tekenreeks | Aanmeldingswachtwoord voor configuratie van referenties |
| `url` | Tekenreeks | URL van leverancier van autorisaties |
| `clientId` | Tekenreeks | Client-id van client/toepassingsreferentie |
| `clientSecret` | Tekenreeks | Clientgeheim van client/toepassingsreferentie |
| `accessToken` | Tekenreeks | Toegangstoken verstrekt door de vergunningverlener |
| `expiration` | Tekenreeks | De time-to-live voor het toegangstoken |
| `refreshToken` | Tekenreeks | Token vernieuwen die door de leverancier van de vergunning worden verstrekt |
| `header` | Tekenreeks | Alle kopteksten die vereist zijn voor autorisatie |
| `accessId` | Tekenreeks | Amazon S3 access ID |
| `secretKey` | Tekenreeks | Amazon S3 geheime sleutel |
| `sshKey` | Tekenreeks | SSH-sleutel voor SFTP met SSH-verificatie |
| `tenant` | Tekenreeks | Azure Data Lake Storage-huurder |
| `servicePrincipalId` | Tekenreeks | Azure Service Principal ID for Azure Data Lake Storage |
| `servicePrincipalKey` | Tekenreeks | Azure Service Principal Key for Azure Data Lake Storage |
| `connectionString` | Tekenreeks | Azure Blob Storage connection string |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde geloofsgeloofsconfiguratie terug.

## Configuraties van lijstreferenties {#retrieve-list}

U kunt een lijst van alle geloofsbrieven configuraties voor uw IMS Organisatie terugwinnen door een verzoek van de GET aan te dienen `/authoring/credentials` eindpunt.

**API-indeling**


```http
GET /authoring/credentials
```

**Verzoek**

Het volgende verzoek zal de lijst van geloofsgeloofsconfiguraties terugwinnen die u toegang tot hebt, op organisatie IMS en zandbakconfiguratie wordt gebaseerd.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

De volgende reactie retourneert HTTP-status 200 met een lijst van aanmeldingsconfiguraties waartoe u toegang hebt, op basis van de IMS-organisatie-id en de sandboxnaam die u hebt gebruikt. Eén `instanceId` komt overeen met de sjabloon voor één aanmeldingsconfiguratie. De reactie is afgebroken voor de beknoptheid.

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

U kunt een bestaande geloofsgeloofsconfiguratie bijwerken door een verzoek van de PUT aan `/authoring/credentials` eindpunt en het verstrekken van instanceID van de geloofsbrieven configuratie wilt u bijwerken. In het lichaam van de vraag, verstrek de bijgewerkte geloofsgeloofsconfiguratie.

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

U kunt gedetailleerde informatie over een specifieke geloofsbrieven configuratie terugwinnen door een verzoek van de GET aan `/authoring/credentials` eindpunt en het verstrekken van instanceID van de geloofsbrieven configuratie wilt u bijwerken.

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

U kunt de opgegeven aanmeldingsconfiguratie verwijderen door een DELETE-aanvraag in te dienen bij de `/authoring/credentials` eindpunt en het verstrekken van identiteitskaart van de geloofsbrieven configuratie u wenst om in de verzoekweg te schrappen.

**API-indeling**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{INSTANCE_ID}` | De `id` van de aanmeldingsconfiguratie die u wilt verwijderen. |

**Verzoek**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 samen met een lege HTTP-respons.

## API-foutafhandeling

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Zie [API-statuscodes](../../landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](../../landing/troubleshooting.md#request-header-errors) in de gids voor het oplossen van problemen met Platforms.

## Volgende stappen

Na het lezen van dit document weet u nu wanneer om het geloofsverbindendtepunt te gebruiken en hoe te opstelling een geloofsgeloofsconfiguratie gebruikend `/authoring/credentials` API-eindpunt of de `/authoring/destinations` eindpunt. Lezen [hoe te om Destination SDK te gebruiken om uw bestemming te vormen](./configure-destination-instructions.md) om te begrijpen waar deze stap in het proces past om uw bestemming te vormen.
