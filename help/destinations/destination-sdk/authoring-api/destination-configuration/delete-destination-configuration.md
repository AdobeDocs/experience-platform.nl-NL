---
description: Deze pagina illustreert de API vraag die wordt gebruikt om een bestaande bestemmingsconfiguratie door Adobe Experience Platform Destination SDK te schrappen.
title: Een doelconfiguratie verwijderen
exl-id: c7309ab7-1b8d-46d4-8017-fd4aa5918cdd
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# Een doelconfiguratie verwijderen

Deze pagina illustreert de API-aanvraag en lading die u kunt gebruiken om een bestaande doelconfiguratie te verwijderen met behulp van het API-eindpunt `/authoring/destinations` .

>[!IMPORTANT]
>
>Alle parameternamen en waarden die door Destination SDK worden gesteund zijn **gevoelig geval**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Aan de slag met API-bewerkingen voor doelconfiguratie {#get-started}

Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](../../getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings authoring en vereiste kopballen te verkrijgen.

## Een doelconfiguratie verwijderen {#delete}

U kunt een [ bestaande ](create-destination-configuration.md) configuratie van de bestemmingsserver schrappen door a `DELETE` verzoek aan het `/authoring/destinations` eindpunt met `{INSTANCE_ID}` van de bestemmingsconfiguratie te maken die u wilt schrappen.

>[!TIP]
>
>**API eindpunt**: `platform.adobe.io/data/core/activation/authoring/destinations`

Om een bestaande bestemmingsconfiguratie en zijn overeenkomstige `{INSTANCE_ID}` te verkrijgen, zie het artikel over [ het terugwinnen van een bestemmingsconfiguratie ](retrieve-destination-configuration.md).

**API formaat**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{INSTANCE_ID}` | De `ID` van de doelconfiguratie die u wilt verwijderen. |

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

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Verwijs naar [ API statuscodes ](../../../../landing/troubleshooting.md#api-status-codes) en [ de fouten van de verzoekkopbal ](../../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van het Platform.

## Volgende stappen

Na het lezen van dit document, weet u nu hoe te om een bestaande bestemmingsconfiguratie door het Destination SDK `/authoring/destinations` API eindpunt te schrappen.

Raadpleeg de volgende artikelen voor meer informatie over wat u met dit eindpunt kunt doen:

* [Een doelconfiguratie maken](create-destination-configuration.md)
* [Een doelconfiguratie ophalen](retrieve-destination-configuration.md)
* [Een doelconfiguratie bijwerken](update-destination-configuration.md)
