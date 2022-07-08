---
description: Deze pagina verklaart hoe te om het /authoring/testing/template/render eindpunt te gebruiken om te visualiseren hoe de getemplatificeerde gebieden van klantengegevens die in uw bestemmingsconfiguratie worden bepaald als zouden kijken.
title: Gevalideerde klantvelden valideren
source-git-commit: fa092e4d1828d9ecd5bc98e3f225fa377f38065f
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 2%

---


# Gevalideerde klantvelden valideren

## Overzicht {#overview}

De `/authoring/testing/template/render` eindpunt helpt u visualiseren hoe templatized [klantgegevensvelden](file-based-destination-configuration.md#customer-data-fields) bepaald in uw bestemmingsconfiguratie zou als kijken.

Het eindpunt produceert willekeurige waarden voor uw gebieden van klantengegevens, en keert hen in de reactie terug. Hierdoor kunt u de semantische structuur van gegevensvelden van klanten, zoals emmernamen of mappaden, valideren.

## Aan de slag {#getting-started}

Controleer voordat je doorgaat de [gids Aan de slag](./getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings creatie en vereiste kopballen te verkrijgen.

## Vereisten {#prerequisites}

Voordat u de `/template/render` aan, zorg ervoor u aan de volgende voorwaarden voldoet:

* U hebt een bestaande op dossier-gebaseerde bestemming die door de Destination SDK wordt gecreeerd en u kunt het in uw zien [doelcatalogus](../ui/destinations-workspace.md).
* Als u de API-aanvraag met succes wilt uitvoeren, hebt u de id van de doelinstantie nodig die overeenkomt met de doelinstantie die u wilt testen. Krijg bestemmingsidentiteitskaart die u in de API vraag, van URL zou moeten gebruiken, wanneer het doorbladeren van een verbinding met uw bestemming in Platform UI.

   ![UI-afbeelding die laat zien hoe u de id van de doelinstantie opgehaald kunt krijgen via de URL.](assets/get-destination-instance-id.png)

## Gelimiteerde klantvelden renderen {#render-customer-fields}

**API-indeling**

```http
POST /authoring/testing/template/render/destination
```

Om het gedrag van dit API eindpunt te illustreren, overwegen een op dossier-gebaseerde bestemming met de volgende configuratie van de gebieden van klantengegevens:

```json
"fileBasedS3Destination":{
   "bucket":{
      "templatingStrategy":"PEBBLE_V1",
      "value":"{{customerData.bucket}}"
   },
   "path":{
      "templatingStrategy":"PEBBLE_V1",
      "value":"{{customerData.path}}"
   }
}
```

**Verzoek**

De onderstaande aanvraag roept de `/authoring/testing/template/render` eindpunt, dat een reactie met willekeurig geproduceerde waarden voor de twee hierboven vermelde gebieden van klantengegevens terugkeert.

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render/destination' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
    "destinationId": "{DESTINATION_CONFIGURATION_ID}",
    "templates": {
        "bucket": "{{customerData.bucket}}",
        "path": "{{customerData.bucket}}/{{customerData.path}}"
    }
}'
```

| Parameters | Beschrijving |
| -------- | ----------- |
| `destinationId` | De id van de [doelconfiguratie](file-based-destination-configuration.md) dat u test. |
| `templates` | De sjabloonveldnamen die zijn gedefinieerd in uw [doelserverconfiguratie](server-and-file-configuration.md). |

**Antwoord**

Een geslaagde reactie retourneert een `HTTP 200 OK` en de hoofdtekst bevat willekeurig gegenereerde waarden voor uw sjabloonvelden.

Deze reactie is bedoeld om u te helpen de correcte structuur van uw gebieden van klantengegevens, zoals emmernamen of omslagwegen bevestigen.


```json
{
    "results": {
        "bucket": "hfWpE-bucket",
        "path": "hfWpE-bucket/ceC"
    }
}
```

## API-foutafhandeling {#api-error-handling}

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Zie [API-statuscodes](../../landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](../../landing/troubleshooting.md#request-header-errors) in de gids voor het oplossen van problemen met Platforms.

## Volgende stappen {#next-steps}

Nadat u dit document hebt gelezen, weet u nu hoe u de configuratie van het gegevensveld van de klant kunt valideren die in uw [doelserver](server-and-file-configuration.md).
