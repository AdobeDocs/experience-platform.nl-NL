---
description: Deze pagina illustreert de API vraag die wordt gebruikt om een Adobe Experience Platform Destination SDK van de credentiële configuratie tot stand te brengen.
title: Een referentieconfiguratie maken
exl-id: 9844c9c5-d2dc-4d4b-ae93-759bf23b87fa
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 2%

---

# Een referentieconfiguratie maken

>[!IMPORTANT]
>
>**API eindpunt**: `platform.adobe.io/data/core/activation/authoring/credentials`

Deze pagina illustreert de API-aanvraag en -lading die u kunt gebruiken om een referentieconfiguratie te maken met behulp van het API-eindpunt `/authoring/credentials` .

## Wanneer gebruikt u het API-eindpunt `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>In de meeste gevallen, te hoeven u ***niet*** om het `/credentials` API eindpunt te gebruiken. In plaats daarvan kunt u de verificatiegegevens voor uw doel configureren via de `customerAuthenticationConfigurations` -parameters van het `/destinations` -eindpunt.
> 
>Lees [ de authentificatieconfiguratie van de Klant ](../functionality/destination-configuration/customer-authentication.md) voor gedetailleerde informatie over de gesteunde authentificatietypen.

Gebruik dit API eindpunt om een credentieconfiguratie tot stand te brengen slechts als er een globaal authentificatiesysteem tussen Adobe en uw bestemmingsplatform is, en de [!DNL Platform] klant te hoeven om geen authentificatiegeloofsbrieven te verstrekken om met uw bestemming te verbinden. In dit geval moet u een referentieconfiguratie maken met het API-eindpunt van `/credentials` .

Wanneer het gebruiken van een globaal authentificatiesysteem, moet u `"authenticationRule":"PLATFORM_AUTHENTICATION"` in de [ 2} configuratie van de bestemmingslevering plaatsen, wanneer [ creërend een nieuwe bestemmingsconfiguratie ](../authoring-api/destination-configuration/create-destination-configuration.md).](../functionality/destination-configuration/destination-delivery.md)

>[!IMPORTANT]
>
>Alle parameternamen en waarden die door Destination SDK worden gesteund zijn **gevoelig geval**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Aan de slag met API-bewerkingen voor gebruikersgegevens {#get-started}

Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](../getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings authoring en vereiste kopballen te verkrijgen.

## Een verificatieconfiguratie maken {#create}

U kunt een nieuwe aanmeldingsconfiguratie maken door een `POST` -aanvraag in te dienen bij het `/authoring/credentials` -eindpunt.

**API formaat**

```http
POST /authoring/credentials
```

De volgende verzoeken leiden tot nieuwe geloofsconfiguraties, die door de parameters worden bepaald die in de lading worden verstrekt.

Selecteer hieronder elk tabblad om de bijbehorende lading weer te geven.

>[!BEGINTABS]

>[!TAB  Basis ]

**creeer een basiscredentiële configuratie**

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
| `url` | String | URL van leverancier van machtigingen |
| `username` | String | Gebruikersnaam aanmeldnaam voor configuratie van aanmeldingsgegevens |
| `password` | String | Aanmeldingswachtwoord voor configuratie van referenties |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde geloofsgeloofsconfiguratie terug.

+++

>[!TAB Amazon S3]

**creeer een [!DNL Amazon S3] credentiële configuratie**

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
| `accessId` | String | [!DNL Amazon S3] toegangs-id |
| `secretKey` | String | [!DNL Amazon S3] geheime sleutel |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde geloofsgeloofsconfiguratie terug.

+++

>[!TAB  SSH ]

**creeer een SSH credentiële configuratie**

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
| `username` | String | Gebruikersnaam aanmeldnaam voor configuratie van aanmeldingsgegevens |
| `sshKey` | String | SSH-sleutel voor SFTP met SSH-verificatie |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde geloofsgeloofsconfiguratie terug.

+++

>[!TAB  Azure de Opslag van het meer van Gegevens ]

**creeer een [!DNL Azure Data Lake Storage] credentiële configuratie**

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
| `url` | String | URL van leverancier van machtigingen |
| `tenant` | String | Azure Data Lake Storage-huurder |
| `servicePrincipalId` | String | Azure Service Principal ID for Azure Data Lake Storage |
| `servicePrincipalKey` | String | Azure Service Principal Key for Azure Data Lake Storage |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde geloofsgeloofsconfiguratie terug.

+++

>[!TAB  Azure Blob Storage ]

**creeer een [!DNL Azure Blob Storage] credentiële configuratie**

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
| `connectionString` | String | [!DNL Azure Blob Storage] verbindingstekenreeks |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde geloofsgeloofsconfiguratie terug.

+++

>[!ENDTABS]

## API-foutafhandeling {#error-handling}

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Verwijs naar [ API statuscodes ](../../../landing/troubleshooting.md#api-status-codes) en [ de fouten van de verzoekkopbal ](../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van het Platform.

## Volgende stappen {#next-steps}

Na het lezen van dit document, weet u nu wanneer om het geloofseindeindpunt te gebruiken en hoe te opstelling een geloofsconfiguratie gebruikend het `/authoring/credentials` API eindpunt Lees [ hoe te om Destination SDK te gebruiken om uw bestemming ](../guides/configure-destination-instructions.md) te vormen om te begrijpen waar deze stap in het proces past om uw bestemming te vormen.
