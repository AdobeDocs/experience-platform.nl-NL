---
description: Deze pagina illustreert de API-aanroep die wordt gebruikt om een bestaande referentieconfiguratie bij te werken via Adobe Experience Platform Destination SDK.
title: Een referentieconfiguratie bijwerken
exl-id: ebff370c-9189-48df-871f-ed0e1cd535c8
source-git-commit: 560200a6553a1aae66c608eef7901b3248c886b4
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 2%

---

# Een referentieconfiguratie bijwerken

>[!IMPORTANT]
>
>**API eindpunt**: `platform.adobe.io/data/core/activation/authoring/credentials`

Deze pagina illustreert de API-aanvraag en lading die u kunt gebruiken om een bestaande referentieconfiguratie bij te werken met behulp van het API-eindpunt `/authoring/credentials` .

## Wanneer gebruikt u het API-eindpunt `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>In de meeste gevallen, te hoeven u ***niet*** om het `/credentials` API eindpunt te gebruiken. In plaats daarvan kunt u de verificatiegegevens voor uw doel configureren via de `customerAuthenticationConfigurations` -parameters van het `/destinations` -eindpunt.
> 
>Lees [ de authentificatieconfiguratie van de Klant ](../functionality/destination-configuration/customer-authentication.md) voor gedetailleerde informatie over de gesteunde authentificatietypen.

Gebruik dit API-eindpunt om alleen een referentie-configuratie te maken als er een algemeen verificatiesysteem is tussen Adobe en uw doelplatform. De [!DNL Experience Platform] -klant hoeft geen verificatiegegevens op te geven om verbinding te maken met uw bestemming. In dit geval moet u een referentieconfiguratie maken met het API-eindpunt van `/credentials` .

Wanneer het gebruiken van een globaal authentificatiesysteem, moet u `"authenticationRule":"PLATFORM_AUTHENTICATION"` in de [ 2} configuratie van de bestemmingslevering plaatsen, wanneer ](../functionality/destination-configuration/destination-delivery.md) creërend een nieuwe bestemmingsconfiguratie [. ](../authoring-api/destination-configuration/create-destination-configuration.md) Dan, moet u de configuratie van de a [ geloofsbrieven ](../credentials-api/create-credential-configuration.md) tot stand brengen en identiteitskaart van de referentie objecten in de `authenticationId` parameter in de [ configuratie van de bestemmingslevering ](/help/destinations/destination-sdk/functionality/destination-configuration/destination-delivery.md#platform-authentication) overgaan.

>[!IMPORTANT]
>
>Alle parameternamen en waarden die door Destination SDK worden gesteund zijn **gevoelig geval**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Aan de slag met API-bewerkingen voor gebruikersgegevens {#get-started}

Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](../getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings authoring en vereiste kopballen te verkrijgen.

## Een referentieconfiguratie bijwerken {#update}

U kunt een [ bestaande ](create-credential-configuration.md) credentiële configuratie bijwerken door een `PUT` verzoek aan het `/authoring/credentials` eindpunt met de bijgewerkte nuttige lading te doen.

Om een bestaande credentiële configuratie en zijn overeenkomstige `{INSTANCE_ID}` te verkrijgen, zie het artikel over [ het terugwinnen van een credentiële configuratie ](retrieve-credential-configuration.md).

**API formaat**

```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{INSTANCE_ID}` | De id van de referentieconfiguratie die u wilt bijwerken. Om een bestaande credentiële configuratie en zijn overeenkomstige `{INSTANCE_ID}` te verkrijgen, zie [ een credentiële configuratie ](retrieve-credential-configuration.md) terugwinnen. |

De volgende verzoeken werken bestaande credentiële configuraties bij, die door de parameters worden bepaald die in de lading worden verstrekt.

Selecteer hieronder elk tabblad om de bijbehorende lading weer te geven.

>[!BEGINTABS]

>[!TAB  Basis ]

**werk een basiscredentiële configuratie** bij

+++Verzoek

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
| `url` | String | URL van leverancier van machtigingen |
| `username` | String | Gebruikersnaam aanmeldnaam voor configuratie van aanmeldingsgegevens |
| `password` | String | Aanmeldingswachtwoord voor configuratie van referenties |

{style="table-layout:auto"}

+++

+++Antwoord

Een succesvolle reactie keert status 200 van HTTP met de details van uw bijgewerkte credentieconfiguratie terug.

+++

>[!TAB Amazon S3]

**werk een [!DNL Amazon S3] credentiële configuratie** bij

+++Verzoek

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
| `accessId` | String | [!DNL Amazon S3] toegangs-id |
| `secretKey` | String | [!DNL Amazon S3] geheime sleutel |

{style="table-layout:auto"}

+++

+++Antwoord

Een succesvolle reactie keert status 200 van HTTP met de details van uw bijgewerkte credentieconfiguratie terug.

+++

>[!TAB  SSH ]

**werk een [!DNL SSH] credentiële configuratie** bij

+++Verzoek

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
| `username` | String | Gebruikersnaam aanmeldnaam voor configuratie van aanmeldingsgegevens |
| `sshKey` | String | [!DNL SSH] -sleutel voor [!DNL SFTP] met [!DNL SSH] -verificatie |

{style="table-layout:auto"}

+++

+++Antwoord

Een succesvolle reactie keert status 200 van HTTP met de details van uw bijgewerkte credentieconfiguratie terug.

+++

>[!TAB  Azure de Opslag van het meer van Gegevens ]

**werk een [!DNL Azure Data Lake Storage] credentiële configuratie** bij

+++Verzoek

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
| `url` | String | URL van leverancier van machtigingen |
| `tenant` | String | Azure Data Lake Storage-huurder |
| `servicePrincipalId` | String | [!DNL Azure Service Principal] ID voor [!DNL Azure Data Lake Storage] |
| `servicePrincipalKey` | String | [!DNL Azure Service Principal Key] for [!DNL Azure Data Lake Storage] |

{style="table-layout:auto"}

+++

+++Antwoord

Een succesvolle reactie keert status 200 van HTTP met de details van uw bijgewerkte credentieconfiguratie terug.

+++

>[!TAB  Azure Blob Storage ]

**werk een [!DNL Azure Blob] credentiële configuratie** bij

+++Verzoek

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
| `connectionString` | String | [!DNL Azure Blob Storage] verbindingstekenreeks |

{style="table-layout:auto"}

+++

+++Antwoord

Een succesvolle reactie keert status 200 van HTTP met de details van uw bijgewerkte credentieconfiguratie terug.

+++

>[!ENDTABS]

## API-foutafhandeling {#error-handling}

Destination SDK API-eindpunten volgen de algemene beginselen van Experience Platform API-foutberichten. Verwijs naar [ API statuscodes ](../../../landing/troubleshooting.md#api-status-codes) en [ de fouten van de verzoekkopbal ](../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van Experience Platform.

## Volgende stappen {#next-steps}

Nadat u dit document hebt gelezen, weet u nu hoe u een referentieconfiguratie kunt bijwerken met behulp van het API-eindpunt van `/authoring/credentials` . Lees [ hoe te om Destination SDK te gebruiken om uw bestemming ](../guides/configure-destination-instructions.md) te vormen om te begrijpen waar deze stap in het proces past om uw bestemming te vormen.
