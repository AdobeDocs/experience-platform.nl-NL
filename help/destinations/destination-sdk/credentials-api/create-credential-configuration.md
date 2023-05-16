---
description: Deze pagina illustreert de API vraag die wordt gebruikt om een Adobe Experience Platform Destination SDK van de credentiële configuratie tot stand te brengen.
title: Een referentieconfiguratie maken
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 4%

---


# Een referentieconfiguratie maken

>[!IMPORTANT]
>
>**API-eindpunt**: `platform.adobe.io/data/core/activation/authoring/credentials`

Deze pagina illustreert de API aanvraag en lading die u kunt gebruiken om een credentiële configuratie tot stand te brengen gebruikend `/authoring/credentials` API-eindpunt.

## Wanneer gebruikt u de `/credentials` API-eindpunt {#when-to-use}

>[!IMPORTANT]
>
>In de meeste gevallen ***niet*** de `/credentials` API-eindpunt. In plaats daarvan, kunt u de authentificatieinformatie voor uw bestemming via vormen `customerAuthenticationConfigurations` parameters van de `/destinations` eindpunt.
> 
>Lezen [Configuratie van klantverificatie](../functionality/destination-configuration/customer-authentication.md) voor gedetailleerde informatie over de ondersteunde verificatietypen.

Gebruik dit API eindpunt om een credentiële configuratie tot stand te brengen slechts als er een globaal authentificatiesysteem tussen Adobe en uw bestemmingsplatform is, en het [!DNL Platform] de klant te hoeven om geen authentificatiegeloofsbrieven te verstrekken om met uw bestemming te verbinden. In dit geval moet u een referentieconfiguratie maken met de `/credentials` API-eindpunt.

Wanneer het gebruiken van een globaal authentificatiesysteem, moet u plaatsen `"authenticationRule":"PLATFORM_AUTHENTICATION"` in de [bestemmingslevering](../functionality/destination-configuration/destination-delivery.md) configuratie, wanneer [het creëren van een nieuwe bestemmingsconfiguratie](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Alle parameternamen en -waarden die door Destination SDK worden ondersteund, zijn **hoofdlettergevoelig**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Aan de slag met API-bewerkingen voor gebruikersgegevens {#get-started}

Controleer voordat je doorgaat de [gids Aan de slag](../getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings creatie en vereiste kopballen te verkrijgen.

## Een verificatieconfiguratie maken {#create}

U kunt een nieuwe geloofsgeloofsconfiguratie tot stand brengen door te maken `POST` verzoek aan de `/authoring/credentials` eindpunt.

**API-indeling**

```http
POST /authoring/credentials
```

De volgende verzoeken leiden tot nieuwe geloofsconfiguraties, die door de parameters worden bepaald die in de lading worden verstrekt.

Selecteer hieronder elk tabblad om de bijbehorende lading weer te geven.

>[!BEGINTABS]

>[!TAB Basis]

**Een basisconfiguratie voor referentie maken**

+++verzoek

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "basicAuthentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

| Parameter | Type | Beschrijving |
| -------- | ----------- | ----------- |
| `url` | Tekenreeks | URL van leverancier van autorisaties |
| `username` | Tekenreeks | Gebruikersnaam aanmeldnaam voor configuratie van referenties |
| `password` | Tekenreeks | Aanmeldingswachtwoord voor configuratie van referenties |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde geloofsgeloofsconfiguratie terug.

+++

>[!TAB Amazon S3]

**Een [!DNL Amazon S3] crediteurconfiguratie**

+++**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
}
```

| Parameter | Type | Beschrijving |
| -------- | ----------- | ----------- |
| `accessId` | Tekenreeks | [!DNL Amazon S3] toegangs-id |
| `secretKey` | Tekenreeks | [!DNL Amazon S3] geheime sleutel |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde geloofsgeloofsconfiguratie terug.

+++

>[!TAB SSH]

**Een SSH-referentieconfiguratie maken**

+++verzoek

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "sshAuthentication":{
      "username":"string",
      "sshKey":"string"
   }
}
```

| Parameter | Type | Beschrijving |
| -------- | ----------- | ----------- |
| `username` | Tekenreeks | Gebruikersnaam aanmeldnaam voor configuratie van referenties |
| `sshKey` | Tekenreeks | SSH-sleutel voor SFTP met SSH-verificatie |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde geloofsgeloofsconfiguratie terug.

+++

>[!TAB Azure Data Lake Storage]

**Een [!DNL Azure Data Lake Storage] crediteurconfiguratie**

+++verzoek

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "azureAuthentication":{
      "url":"string",
      "tenant":"string",
      "servicePrincipalId":"string",
      "servicePrincipalKey":"string"
   }
}
```

| Parameter | Type | Beschrijving |
| -------- | ----------- | ----------- |
| `url` | Tekenreeks | URL van leverancier van autorisaties |
| `tenant` | Tekenreeks | Azure Data Lake Storage-huurder |
| `servicePrincipalId` | Tekenreeks | Azure Service Principal ID for Azure Data Lake Storage |
| `servicePrincipalKey` | Tekenreeks | Azure Service Principal Key for Azure Data Lake Storage |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde geloofsgeloofsconfiguratie terug.

+++

>[!TAB Azure Blob Storage]

**Een [!DNL Azure Blob Storage] crediteurconfiguratie**

+++verzoek

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "azureConnectionStringAuthentication":{
      "connectionString":"string"
   }
}
```

| Parameter | Type | Beschrijving |
| -------- | ----------- | ----------- |
| `connectionString` | Tekenreeks | [!DNL Azure Blob Storage] verbindingstekenreeks |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde geloofsgeloofsconfiguratie terug.

+++

>[!ENDTABS]

## API-foutafhandeling {#error-handling}

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Zie [API-statuscodes](../../../landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](../../../landing/troubleshooting.md#request-header-errors) in de gids voor het oplossen van problemen met Platforms.

## Volgende stappen {#next-steps}

Na het lezen van dit document weet u nu wanneer om het geloofsverbindendtepunt te gebruiken en hoe te opstelling een geloofsgeloofsconfiguratie gebruikend `/authoring/credentials` API-eindpunt gelezen [hoe te om Destination SDK te gebruiken om uw bestemming te vormen](../guides/configure-destination-instructions.md) om te begrijpen waar deze stap in het proces past om uw bestemming te vormen.
