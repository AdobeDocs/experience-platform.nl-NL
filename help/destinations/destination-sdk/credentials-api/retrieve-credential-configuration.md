---
description: Deze pagina illustreert de API vraag die wordt gebruikt om een credentiële configuratie door Adobe Experience Platform Destination SDK terug te winnen.
title: Een referentieconfiguratie ophalen
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 0%

---


# Een referentieconfiguratie ophalen

>[!IMPORTANT]
>
>**API-eindpunt**: `platform.adobe.io/data/core/activation/authoring/credentials`

Deze pagina illustreert de API aanvraag en lading die u kunt gebruiken om een credentiële configuratie terug te winnen gebruikend `/authoring/credentials` API-eindpunt.

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

## Een referentieconfiguratie ophalen {#retrieve}

U kunt een [bestaand](create-credential-configuration.md) crediteurconfiguratie door een `GET` verzoek aan de `/authoring/credentials` eindpunt.

**API-indeling**

Gebruik de volgende API-indeling om alle referentieconfiguraties voor uw account op te halen.

```http
GET /authoring/credentials
```

Gebruik de volgende API-indeling om een specifieke referentieconfiguratie op te halen, gedefinieerd door de `{INSTANCE_ID}` parameter.

```http
GET /authoring/credentials/{INSTANCE_ID}
```

De volgende twee verzoeken winnen alle geloofsconfiguraties voor uw IMS Organisatie, of een specifieke credentiële configuratie terug, afhankelijk van of u de overgaan `INSTANCE_ID` in de aanvraag.

Selecteer hieronder elk tabblad om de bijbehorende lading weer te geven.

>[!BEGINTABS]

>[!TAB Alle referentieconfiguraties ophalen]

+++verzoek

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Response

Een geslaagde reactie retourneert HTTP-status 200 met een lijst van referentieconfiguraties waartoe u toegang hebt, op basis van de [!DNL IMS Org ID] en de naam van de sandbox die u hebt gebruikt. Eén `instanceId` komt overeen met één referentie-configuratie.

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"s3Authentication",
   "name":"yourdestination",
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
},
{
   "instanceId":"a25bffa0-3127-4030-895d-1d1236bb3680",
   "createdDate":"2022-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2022-08-07T06:41:48.641943Z",
   "type":"basic",
   "name":"yourdestination",
   "s3Authentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

+++

>[!TAB Een specifieke referentieconfiguratie ophalen]

+++verzoek

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{INSTANCE_ID}` | De id van de referentieconfiguratie die u wilt ophalen. |

+++

+++Response

Een geslaagde reactie retourneert HTTP-status 200 met de details van de referentieconfiguratie die overeenkomen met de `instanceId` verstrekt op verzoek.

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"s3Authentication",
   "name":"yourdestination",
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
}
```

+++

>[!ENDTABS]

## API-foutafhandeling {#error-handling}

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Zie [API-statuscodes](../../../landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](../../../landing/troubleshooting.md#request-header-errors) in de gids voor het oplossen van problemen met Platforms.

## Volgende stappen {#next-steps}

Nadat u dit document hebt gelezen, weet u nu hoe u details over uw referentieconfiguraties kunt ophalen met de `/authoring/credentials` API-eindpunt. Lezen [hoe te om Destination SDK te gebruiken om uw bestemming te vormen](../guides/configure-destination-instructions.md) om te begrijpen waar deze stap in het proces past om uw bestemming te vormen.
