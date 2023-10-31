---
description: Deze pagina illustreert de API vraag die wordt gebruikt om details over een bestemmings het publiceren verzoek door Adobe Experience Platform Destination SDK terug te winnen.
title: Een doelpublicatieverzoek ophalen
exl-id: fceef12d-a52c-4259-a91e-7af88b132800
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 2%

---

# Een doelpublicatieverzoek ophalen

>[!IMPORTANT]
>
>U hoeft dit API-eindpunt alleen te gebruiken als u een geproductieerde (openbare) bestemming verzendt die door andere klanten van het Experience Platform moet worden gebruikt. Als u een privé bestemming voor uw eigen gebruik creeert, te hoeven u niet om de bestemming formeel voor te leggen gebruikend het publiceren API.

>[!IMPORTANT]
>
>**API-eindpunt**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Nadat u hebt gevormd en uw bestemming getest, kunt u het voorleggen aan Adobe voor overzicht en het publiceren. Lezen [Ter controle een bestemming verzenden die is geschreven in Destination SDK](../guides/submit-destination.md) voor alle andere stappen moet u als deel van het proces van de bestemmingsvoorlegging doen.

Gebruik het API-eindpunt voor publicatiedoelen om een publicatieverzoek in te dienen wanneer:

* Als partner van Destination SDK, wilt u uw geproduceerde bestemming beschikbaar over alle organisaties van het Experience Platform voor alle klanten van het Experience Platform aan gebruik maken;
* U maakt *alle updates* naar uw configuraties. De updates van de configuratie worden weerspiegeld in de bestemming slechts nadat u een nieuw het publiceren verzoek indient, dat door het team van het Experience Platform wordt goedgekeurd.

>[!IMPORTANT]
>
>Alle parameternamen en -waarden die door Destination SDK worden ondersteund, zijn **hoofdlettergevoelig**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Aan de slag met API-bewerkingen voor doelpublicatie {#get-started}

Controleer voordat je doorgaat de [gids Aan de slag](../getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings creatie en vereiste kopballen te verkrijgen.

## Publicatieverzoeken voor bestemming weergeven {#retrieve-list}

U kunt een lijst van alle bestemmingen terugwinnen die voor publicatie voor uw organisatie IMS door een verzoek van de GET aan wordt voorgelegd `/authoring/destinations/publish` eindpunt.

**API-indeling**

Gebruik de volgende API-indeling om alle publicatieverzoeken voor uw account op te halen.

```http
GET /authoring/destinations/publish
```

Gebruik de volgende API-indeling om een specifieke publicatieaanvraag op te halen, gedefinieerd door de `{DESTINATION_ID}` parameter.

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

**Verzoek**

De volgende twee verzoeken winnen alle het publiceren verzoeken voor uw IMS Organisatie, of een specifiek het publiceren verzoek terug, afhankelijk van of u overgaan `DESTINATION_ID` in de aanvraag.

Selecteer hieronder elk tabblad om de bijbehorende lading weer te geven.

>[!BEGINTABS]

>[!TAB Alle publicatieverzoeken ophalen]

+++verzoek

Met het volgende verzoek wordt de lijst met publicatieverzoeken opgehaald die u hebt verzonden, op basis van [!DNL IMS Org ID] en sandboxconfiguratie.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Response

De volgende reactie retourneert HTTP-status 200 met een lijst van alle doelen die zijn verzonden voor publicatie waartoe u toegang hebt, op basis van de IMS-organisatie-id en de sandboxnaam die u hebt gebruikt. Eén `configId` komt overeen met de publicatieaanvraag voor één bestemming.

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"ab41387c0-4772-4709-a3ce-6d5fee654520",
         "allowedOrgs":[
            "716543205DB85F7F0A495E5B@AdobeOrg"
         ],
         "status":"TEST",
         "destinationType":"DEV"
      },
      {
         "configId":"cd568c67-f25e-47e4-b9a2-d79297a20b27",
         "allowedOrgs":[
            "*"
         ],
         "status":"DEPRECATED",
         "destinationType":"PUBLIC",
         "publishedDate":1630525501009
      },
      {
         "configId":"ef6f07154-09bc-4bee-8baf-828ea9c92fba",
         "allowedOrgs":[
            "*"
         ],
         "status":"PUBLISHED",
         "destinationType":"PUBLIC",
         "publishedDate":1630531586002
      }
   ]
}
```

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `destinationId` | Tekenreeks | De bestemmingsidentiteitskaart van de bestemmingsconfiguratie die u voor het publiceren hebt voorgelegd. |
| `publishDetailsList.configId` | Tekenreeks | De unieke id van de bestemming publiceert het verzoek voor uw verzonden bestemming. |
| `publishDetailsList.allowedOrgs` | Tekenreeks | Keert de organisaties van het Experience Platform terug waarvoor de bestemming beschikbaar is. <br> <ul><li> Voor `"destinationType": "PUBLIC"`, retourneert deze parameter `"*"`, hetgeen betekent dat de bestemming beschikbaar is voor alle organisaties van de Experience Platform.</li><li> Voor `"destinationType": "DEV"`, retourneert deze parameter de organisatie-id van de organisatie die u hebt gebruikt voor het schrijven en testen van het doel.</li></ul> |
| `publishDetailsList.status` | Tekenreeks | De status van uw doelpublicatieverzoek. Mogelijke waarden zijn `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. Doelen met de waarde `PUBLISHED` live zijn en door klanten in de Experience Platform kunnen worden gebruikt. |
| `publishDetailsList.destinationType` | Tekenreeks | Het type bestemming. Waarden kunnen `DEV` en `PUBLIC`. `DEV` komt overeen met het doel in uw organisatie Experience Platform. `PUBLIC` komt overeen met het doel dat u hebt verzonden voor publicatie. Denk aan deze twee opties in Git-termen, waar de `DEV` versie vertegenwoordigt uw lokale auteurstak en `PUBLIC` versie staat voor de externe hoofdvertakking. |
| `publishDetailsList.publishedDate` | Tekenreeks | De datum waarop de bestemming voor publicatie werd voorgelegd, in tijdperk. |

{style="table-layout:auto"}

+++

>[!TAB Een specifiek publicatieverzoek ophalen]

+++verzoek

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish/{DESTINATION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{DESTINATION_ID}` | De id van het doel waarvoor u de publicatiestatus wilt ophalen. |

+++

+++Response

Als u een `DESTINATION_ID` in de API vraag, keert de reactie status 200 van HTTP met gedetailleerde informatie over de gespecificeerde bestemming terug publiceer verzoek.

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"123cs780-ce29-434f-921e-4ed6ec2a6c35",
         "allowedOrgs": [
            "*"
         ],    
         "status":"PUBLISHED",
         "destinationType": "PUBLIC",
         "publishedDate":"1630617746"
      }
   ]
}
```

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `destinationId` | Tekenreeks | De bestemmingsidentiteitskaart van de bestemmingsconfiguratie die u voor het publiceren hebt voorgelegd. |
| `publishDetailsList.configId` | Tekenreeks | De unieke id van de bestemming publiceert het verzoek voor uw verzonden bestemming. |
| `publishDetailsList.allowedOrgs` | Tekenreeks | Keert de organisaties van het Experience Platform terug waarvoor de bestemming beschikbaar is. <br> <ul><li> Voor `"destinationType": "PUBLIC"`, retourneert deze parameter `"*"`, hetgeen betekent dat de bestemming beschikbaar is voor alle organisaties van de Experience Platform.</li><li> Voor `"destinationType": "DEV"`, retourneert deze parameter de organisatie-id van de organisatie die u hebt gebruikt voor het schrijven en testen van het doel.</li></ul> |
| `publishDetailsList.status` | Tekenreeks | De status van uw doelpublicatieverzoek. Mogelijke waarden zijn `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. Doelen met de waarde `PUBLISHED` live zijn en door klanten in de Experience Platform kunnen worden gebruikt. |
| `publishDetailsList.destinationType` | Tekenreeks | Het type bestemming. Waarden kunnen `DEV` en `PUBLIC`. `DEV` komt overeen met het doel in uw organisatie Experience Platform. `PUBLIC` komt overeen met het doel dat u hebt verzonden voor publicatie. Denk aan deze twee opties in Git-termen, waar de `DEV` versie vertegenwoordigt uw lokale auteurstak en `PUBLIC` versie staat voor de externe hoofdvertakking. |
| `publishDetailsList.publishedDate` | Tekenreeks | De datum waarop de bestemming voor publicatie werd voorgelegd, in tijdperk. |

{style="table-layout:auto"}

+++

>[!ENDTABS]

## API-foutafhandeling

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Zie [API-statuscodes](../../../landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van het Platform.
