---
description: Deze pagina verklaart hoe te om het /authoring/testing/template/render eindpunt te gebruiken om te visualiseren hoe de getemplatificeerde gebieden van klantengegevens die in uw bestemmingsconfiguratie worden bepaald als zouden kijken.
title: Gevalideerde klantvelden valideren
exl-id: 8ed93f0c-3439-4d11-bb2f-d417a1e0b6a8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 1%

---


# Gevalideerde klantvelden valideren

## Overzicht {#overview}

Het `/authoring/testing/template/render` eindpunt helpt u visualiseren hoe de templatized [&#x200B; gebieden van klantengegevens &#x200B;](../../functionality/destination-configuration/customer-data-fields.md) die in uw bestemmingsconfiguratie worden bepaald als zouden kijken.

Het eindpunt produceert willekeurige waarden voor uw gebieden van klantengegevens, en keert hen in de reactie terug. Hierdoor kunt u de semantische structuur van gegevensvelden van klanten, zoals emmernamen of mappaden, valideren.

## Aan de slag {#getting-started}

Alvorens verder te gaan, te herzien gelieve [&#x200B; begonnen gids &#x200B;](../../getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings authoring en vereiste kopballen te verkrijgen.

## Vereisten {#prerequisites}

Voordat u het eindpunt `/template/render` kunt gebruiken, moet u controleren of aan de volgende voorwaarden is voldaan:

* U hebt een bestaande op dossier-gebaseerde bestemming die door Destination SDK wordt gecreeerd en u kunt het in uw [&#x200B; doelcatalogus &#x200B;](../../../ui/destinations-workspace.md) zien.
* Als u de API-aanvraag met succes wilt uitvoeren, hebt u de id van de doelinstantie nodig die overeenkomt met de doelinstantie die u wilt testen. Krijg bestemmingsidentiteitskaart die u in de API vraag, van URL zou moeten gebruiken, wanneer het doorbladeren van een verbinding met uw bestemming in Experience Platform UI.

  ![&#x200B; beeld UI die hoe te om bestemmingsidentiteitskaart van URL te krijgen toont.](../../assets/testing-api/get-destination-instance-id.png)

## Gelimiteerde klantvelden renderen {#render-customer-fields}

**API formaat**

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

Het verzoek hieronder roept het `/authoring/testing/template/render` eindpunt, dat een reactie met willekeurig geproduceerde waarden voor de twee hierboven vermelde gebieden van klantengegevens terugkeert.

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
| `destinationId` | Identiteitskaart van de [&#x200B; bestemmingsconfiguratie &#x200B;](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) die u test. |
| `templates` | De templatized gebiedsnamen die in uw [&#x200B; configuratie van de bestemmingsserver &#x200B;](../../authoring-api/destination-server/create-destination-server.md) worden bepaald. |

**Reactie**

Een geslaagde reactie retourneert een `HTTP 200 OK` -status en de hoofdtekst bevat willekeurig gegenereerde waarden voor uw sjabloonvelden.

Deze reactie kan u helpen de correcte structuur van uw gebieden van klantengegevens, zoals emmernamen of omslagwegen bevestigen.


```json
{
    "results": {
        "bucket": "hfWpE-bucket",
        "path": "hfWpE-bucket/ceC"
    }
}
```

## API-foutafhandeling {#api-error-handling}

Destination SDK API-eindpunten volgen de algemene beginselen van Experience Platform API-foutberichten. Verwijs naar [&#x200B; API statuscodes &#x200B;](../../../../landing/troubleshooting.md#api-status-codes) en [&#x200B; de fouten van de verzoekkopbal &#x200B;](../../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van Experience Platform.

## Volgende stappen {#next-steps}

Na het lezen van dit document, weet u nu hoe te om de configuratie te bevestigen van het gebied van klantengegevens die in uw [&#x200B; bestemmingsserver &#x200B;](../../authoring-api/destination-server/create-destination-server.md) wordt bepaald.
