---
description: Deze pagina illustreert de API vraag die wordt gebruikt om een bestaande credentiële configuratie door Adobe Experience Platform Destination SDK bij te werken.
title: Een referentieconfiguratie bijwerken
exl-id: ebff370c-9189-48df-871f-ed0e1cd535c8
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 4%

---

# Een referentieconfiguratie bijwerken

>[!IMPORTANT]
>
>**API-eindpunt**: `platform.adobe.io/data/core/activation/authoring/credentials`

Deze pagina illustreert de API-aanvraag en lading die u kunt gebruiken om een bestaande referentieconfiguratie bij te werken met de `/authoring/credentials` API-eindpunt.

## Wanneer gebruikt u de `/credentials` API-eindpunt {#when-to-use}

>[!IMPORTANT]
>
>In de meeste gevallen ***niet*** de noodzaak `/credentials` API-eindpunt. In plaats daarvan, kunt u de authentificatieinformatie voor uw bestemming via vormen `customerAuthenticationConfigurations` parameters van de `/destinations` eindpunt.
> 
>Lezen [Configuratie van klantverificatie](../functionality/destination-configuration/customer-authentication.md) voor gedetailleerde informatie over de ondersteunde verificatietypen.

Gebruik dit API eindpunt om een credentiële configuratie tot stand te brengen slechts als er een globaal authentificatiesysteem tussen Adobe en uw bestemmingsplatform is, en [!DNL Platform] de klant te hoeven om geen authentificatiegeloofsbrieven te verstrekken om met uw bestemming te verbinden. In dit geval moet u een referentieconfiguratie maken met de `/credentials` API-eindpunt.

Wanneer het gebruiken van een globaal authentificatiesysteem, moet u plaatsen `"authenticationRule":"PLATFORM_AUTHENTICATION"` in de [bestemmingslevering](../functionality/destination-configuration/destination-delivery.md) configuratie, wanneer [het creëren van een nieuwe bestemmingsconfiguratie](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Alle parameternamen en -waarden die door Destination SDK worden ondersteund, zijn **hoofdlettergevoelig**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Aan de slag met API-bewerkingen voor gebruikersgegevens {#get-started}

Controleer voordat je doorgaat de [gids Aan de slag](../getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings creatie en vereiste kopballen te verkrijgen.

## Een referentieconfiguratie bijwerken {#update}

U kunt een [bestaand](create-credential-configuration.md) crediteurconfiguratie door een `PUT` verzoek aan de `/authoring/credentials` eindpunt met de bijgewerkte nuttige lading.

Een bestaande referentieconfiguratie en de bijbehorende `{INSTANCE_ID}`, zie het artikel over [ophalen van een referentieconfiguratie](retrieve-credential-configuration.md).

**API-indeling**

```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{INSTANCE_ID}` | De id van de referentieconfiguratie die u wilt bijwerken. Een bestaande referentieconfiguratie en de bijbehorende `{INSTANCE_ID}`, zie [Een referentieconfiguratie ophalen](retrieve-credential-configuration.md). |

De volgende verzoeken werken bestaande credentiële configuraties bij, die door de parameters worden bepaald die in de lading worden verstrekt.

Selecteer hieronder elk tabblad om de bijbehorende lading weer te geven.

>[!BEGINTABS]

>[!TAB Basis]

**Een basisconfiguratie voor referentie bijwerken**

+++verzoek

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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
| `url` | Tekenreeks | URL van leverancier van machtigingen |
| `username` | Tekenreeks | Gebruikersnaam aanmeldnaam voor configuratie van aanmeldingsgegevens |
| `password` | Tekenreeks | Aanmeldingswachtwoord voor configuratie van referenties |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met de details van uw bijgewerkte credentieconfiguratie terug.

+++

>[!TAB Amazon S3]

**Een update [!DNL Amazon S3] crediteurenconfiguratie**

+++verzoek

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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

Een succesvolle reactie keert status 200 van HTTP met de details van uw bijgewerkte credentieconfiguratie terug.

+++

>[!TAB SSH]

**Een update [!DNL SSH] crediteurenconfiguratie**

+++verzoek

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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
| `username` | Tekenreeks | Gebruikersnaam aanmeldnaam voor configuratie van aanmeldingsgegevens |
| `sshKey` | Tekenreeks | [!DNL SSH] toets voor [!DNL SFTP] with [!DNL SSH] verificatie |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met de details van uw bijgewerkte credentieconfiguratie terug.

+++

>[!TAB Azure Data Lake Storage]

**Een update [!DNL Azure Data Lake Storage] crediteurenconfiguratie**

+++verzoek

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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
| `url` | Tekenreeks | URL van leverancier van machtigingen |
| `tenant` | Tekenreeks | Azure Data Lake Storage-huurder |
| `servicePrincipalId` | Tekenreeks | [!DNL Azure Service Principal] ID voor [!DNL Azure Data Lake Storage] |
| `servicePrincipalKey` | Tekenreeks | [!DNL Azure Service Principal Key] for [!DNL Azure Data Lake Storage] |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met de details van uw bijgewerkte credentieconfiguratie terug.

+++

>[!TAB Azure Blob Storage]

**Een update [!DNL Azure Blob] crediteurenconfiguratie**

+++verzoek

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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

Een succesvolle reactie keert status 200 van HTTP met de details van uw bijgewerkte credentieconfiguratie terug.

+++

>[!ENDTABS]

## API-foutafhandeling {#error-handling}

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Zie [API-statuscodes](../../../landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van het Platform.

## Volgende stappen {#next-steps}

Nadat u dit document hebt gelezen, kunt u nu een referentieconfiguratie bijwerken met de `/authoring/credentials` API-eindpunt. Lezen [hoe te om Destination SDK te gebruiken om uw bestemming te vormen](../guides/configure-destination-instructions.md) om te begrijpen waar deze stap in het proces past om uw bestemming te vormen.
