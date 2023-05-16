---
description: Deze pagina illustreert de API vraag die wordt gebruikt om een Adobe Experience Platform Destination SDK van de credentiële configuratie te schrappen.
title: Een referentieconfiguratie verwijderen
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---


# Een referentieconfiguratie verwijderen

>[!IMPORTANT]
>
>**API-eindpunt**: `platform.adobe.io/data/core/activation/authoring/credentials`

Deze pagina illustreert de API aanvraag en lading die u kunt gebruiken om een credentiële configuratie te schrappen gebruikend `/authoring/credentials` API-eindpunt.

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

## Een referentieconfiguratie verwijderen {#delete}

U kunt een [bestaand](create-credential-configuration.md) crediteurconfiguratie door een `DELETE` verzoek aan de `/authoring/credentials` met de `{INSTANCE_ID}`van de referentieconfiguratie die u wilt verwijderen.

Om een bestaande bestemmingsconfiguratie en zijn overeenkomstige te verkrijgen `{INSTANCE_ID}`, raadpleegt u het artikel over [ophalen van een referentieconfiguratie](retrieve-credential-configuration.md).

**API-indeling**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{INSTANCE_ID}` | De `ID` van de referentieconfiguratie die u wilt verwijderen. |

Met het volgende verzoek wordt een door de `{INSTANCE_ID}` parameter.

+++verzoek

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Response

Een geslaagde reactie retourneert HTTP-status 200 samen met een lege HTTP-respons.

+++

## API-foutafhandeling {#error-handling}

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Zie [API-statuscodes](../../../landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](../../../landing/troubleshooting.md#request-header-errors) in de gids voor het oplossen van problemen met Platforms.

## Volgende stappen {#next-steps}

Nadat u dit document hebt gelezen, weet u nu hoe u een referentieconfiguratie kunt verwijderen met de opdracht `/authoring/credentials` API-eindpunt. Lezen [hoe te om Destination SDK te gebruiken om uw bestemming te vormen](../guides/configure-destination-instructions.md) om te begrijpen waar deze stap in het proces past om uw bestemming te vormen.
