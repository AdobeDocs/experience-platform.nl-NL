---
description: Deze pagina illustreert de API vraag die wordt gebruikt om een credentiële configuratie door Adobe Experience Platform Destination SDK terug te winnen.
title: Een referentieconfiguratie ophalen
exl-id: cec55073-6e2f-4412-a9dd-1aeb445279c0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# Een referentieconfiguratie ophalen

>[!IMPORTANT]
>
>**API eindpunt**: `platform.adobe.io/data/core/activation/authoring/credentials`

Deze pagina illustreert de API-aanvraag en -lading die u kunt gebruiken om een referentieconfiguratie op te halen met het API-eindpunt `/authoring/credentials` .

## Wanneer gebruikt u het API-eindpunt `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>In de meeste gevallen, te hoeven u ***niet*** om het `/credentials` API eindpunt te gebruiken. In plaats daarvan kunt u de verificatiegegevens voor uw doel configureren via de `customerAuthenticationConfigurations` -parameters van het `/destinations` -eindpunt.
> 
>Lees [ de authentificatieconfiguratie van de Klant ](../functionality/destination-configuration/customer-authentication.md) voor gedetailleerde informatie over de gesteunde authentificatietypen.

Gebruik dit API-eindpunt om alleen een referentie-configuratie te maken als er een algemeen verificatiesysteem is tussen Adobe en uw doelplatform. De [!DNL Experience Platform] -klant hoeft geen verificatiegegevens op te geven om verbinding te maken met uw bestemming. In dit geval moet u een referentieconfiguratie maken met het API-eindpunt van `/credentials` .

Wanneer het gebruiken van een globaal authentificatiesysteem, moet u `"authenticationRule":"PLATFORM_AUTHENTICATION"` in de [ 2} configuratie van de bestemmingslevering plaatsen, wanneer [ creërend een nieuwe bestemmingsconfiguratie ](../authoring-api/destination-configuration/create-destination-configuration.md).](../functionality/destination-configuration/destination-delivery.md)

>[!IMPORTANT]
>
>Alle parameternamen en waarden die door Destination SDK worden gesteund zijn **gevoelig geval**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Aan de slag met API-bewerkingen voor gebruikersgegevens {#get-started}

Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](../getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings authoring en vereiste kopballen te verkrijgen.

## Een referentieconfiguratie ophalen {#retrieve}

U kunt een [ bestaande ](create-credential-configuration.md) credentiële configuratie terugwinnen door een `GET` verzoek aan het `/authoring/credentials` eindpunt te doen.

**API formaat**

Gebruik de volgende API-indeling om alle referentieconfiguraties voor uw account op te halen.

```http
GET /authoring/credentials
```

Gebruik de volgende API-indeling om een specifieke referentieconfiguratie op te halen, gedefinieerd door de parameter `{INSTANCE_ID}` .

```http
GET /authoring/credentials/{INSTANCE_ID}
```

De volgende twee verzoeken winnen alle geloofsbrieven configuraties voor uw organisatie IMS, of een specifieke credentiële configuratie terug, afhankelijk van of u de `INSTANCE_ID` parameter in het verzoek overgaat.

Selecteer hieronder elk tabblad om de bijbehorende lading weer te geven.

>[!BEGINTABS]

>[!TAB  wint alle credentiële configuraties ] terug

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

Een succesvol antwoord retourneert HTTP-status 200 met een lijst van referentieconfiguraties waartoe u toegang hebt, op basis van de naam van de [!DNL IMS Org ID] en de sandbox die u hebt gebruikt. Eén `instanceId` komt overeen met één referentie-configuratie.

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

>[!TAB  wint een specifieke credentieconfiguratie ] terug

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

Een geslaagde reactie retourneert HTTP-status 200 met de details van de referentieconfiguratie die overeenkomen met de `instanceId` die op de aanvraag is opgegeven.

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

Destination SDK API-eindpunten volgen de algemene beginselen van Experience Platform API-foutberichten. Verwijs naar [ API statuscodes ](../../../landing/troubleshooting.md#api-status-codes) en [ de fouten van de verzoekkopbal ](../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van Experience Platform.

## Volgende stappen {#next-steps}

Nadat u dit document hebt gelezen, weet u nu hoe u details over uw referentie-configuraties kunt ophalen met behulp van het API-eindpunt van `/authoring/credentials` . Lees [ hoe te om Destination SDK te gebruiken om uw bestemming ](../guides/configure-destination-instructions.md) te vormen om te begrijpen waar deze stap in het proces past om uw bestemming te vormen.
