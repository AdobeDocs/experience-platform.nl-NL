---
description: Deze pagina illustreert de API vraag die wordt gebruikt om een bestaande bestemmingsconfiguratie door Adobe Experience Platform Destination SDK te schrappen.
title: Een doelconfiguratie verwijderen
exl-id: c7309ab7-1b8d-46d4-8017-fd4aa5918cdd
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 1%

---

# Een doelconfiguratie verwijderen

Deze pagina illustreert de API aanvraag en lading die u kunt gebruiken om een bestaande bestemmingsconfiguratie te schrappen, gebruikend `/authoring/destinations` API-eindpunt.

>[!IMPORTANT]
>
>Alle parameternamen en -waarden die door Destination SDK worden ondersteund, zijn **hoofdlettergevoelig**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Aan de slag met API-bewerkingen voor doelconfiguratie {#get-started}

Controleer voordat je doorgaat de [gids Aan de slag](../../getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings creatie en vereiste kopballen te verkrijgen.

## Een doelconfiguratie verwijderen {#delete}

U kunt een [bestaand](create-destination-configuration.md) doelserverconfiguratie door een `DELETE` verzoek aan de `/authoring/destinations` met de `{INSTANCE_ID}`van de bestemmingsconfiguratie die u wilt schrappen.

>[!TIP]
>
>**API-eindpunt**: `platform.adobe.io/data/core/activation/authoring/destinations`

Om een bestaande bestemmingsconfiguratie en zijn overeenkomstige te verkrijgen `{INSTANCE_ID}`, zie het artikel over [het terugwinnen van een bestemmingsconfiguratie](retrieve-destination-configuration.md).

**API-indeling**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{INSTANCE_ID}` | De `ID` van de bestemmingsconfiguratie u wilt schrappen. |

+++verzoek

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destinations/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++Response

Een geslaagde reactie retourneert HTTP-status 200 samen met een lege HTTP-respons.


## API-foutafhandeling {#error-handling}

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Zie [API-statuscodes](../../../../landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](../../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van het Platform.

## Volgende stappen

Na het lezen van dit document, weet u nu hoe te om een bestaande bestemmingsconfiguratie door de Destination SDK te schrappen `/authoring/destinations` API-eindpunt.

Raadpleeg de volgende artikelen voor meer informatie over wat u met dit eindpunt kunt doen:

* [Een doelconfiguratie maken](create-destination-configuration.md)
* [Een doelconfiguratie ophalen](retrieve-destination-configuration.md)
* [Een doelconfiguratie bijwerken](update-destination-configuration.md)
