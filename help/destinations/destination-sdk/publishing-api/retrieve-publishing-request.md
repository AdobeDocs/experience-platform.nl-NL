---
description: Deze pagina illustreert de API vraag die wordt gebruikt om details over een bestemmings het publiceren verzoek door Adobe Experience Platform Destination SDK terug te winnen.
title: Een doelpublicatieverzoek ophalen
exl-id: fceef12d-a52c-4259-a91e-7af88b132800
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---

# Een doelpublicatieverzoek ophalen

>[!IMPORTANT]
>
>U hoeft dit API-eindpunt alleen te gebruiken als u een geproductieerde (openbare) bestemming verzendt die door andere klanten van het Experience Platform moet worden gebruikt. Als u een privé bestemming voor uw eigen gebruik creeert, te hoeven u niet om de bestemming formeel voor te leggen gebruikend het publiceren API.

>[!IMPORTANT]
>
>**API eindpunt**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Nadat u hebt gevormd en uw bestemming getest, kunt u het voorleggen aan Adobe voor overzicht en het publiceren. Lees [ voorlegt voor overzicht een bestemming die in Destination SDK ](../guides/submit-destination.md) voor alle andere stappen wordt geschreven u als deel van het proces van de bestemmingsvoorlegging moet doen.

Gebruik het API-eindpunt voor publicatiedoelen om een publicatieverzoek in te dienen wanneer:

* Als partner van Destination SDK, wilt u uw geproduceerde bestemming beschikbaar over alle organisaties van het Experience Platform voor alle klanten van het Experience Platform aan gebruik maken;
* U maakt *om het even welke updates* aan uw configuraties. De updates van de configuratie worden weerspiegeld in de bestemming slechts nadat u een nieuw het publiceren verzoek indient, dat door het team van het Experience Platform wordt goedgekeurd.

>[!IMPORTANT]
>
>Alle parameternamen en waarden die door Destination SDK worden gesteund zijn **gevoelig geval**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Aan de slag met API-bewerkingen voor doelpublicatie {#get-started}

Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](../getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings authoring en vereiste kopballen te verkrijgen.

## Publicatieverzoeken voor bestemming weergeven {#retrieve-list}

U kunt een lijst van alle bestemmingen terugwinnen die voor publicatie voor uw organisatie IMS door een verzoek van de GET aan het `/authoring/destinations/publish` eindpunt worden voorgelegd te doen.

**API formaat**

Gebruik de volgende API-indeling om alle publicatieverzoeken voor uw account op te halen.

```http
GET /authoring/destinations/publish
```

Gebruik de volgende API-indeling om een specifieke publicatieaanvraag op te halen, die door de parameter `{DESTINATION_ID}` wordt gedefinieerd.

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

**Verzoek**

Met de volgende twee verzoeken worden alle publicatieverzoeken voor uw IMS-organisatie of een specifieke publicatieaanvraag opgehaald, afhankelijk van het feit of u de parameter `DESTINATION_ID` in de aanvraag doorgeeft.

Selecteer hieronder elk tabblad om de bijbehorende lading weer te geven.

>[!BEGINTABS]

>[!TAB  wint alle het publiceren verzoeken  terug]

+++verzoek

Met het volgende verzoek wordt de lijst opgehaald met publicatieverzoeken die u hebt verzonden, op basis van de configuratie van [!DNL IMS Org ID] en de sandbox.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Response

De volgende reactie retourneert HTTP-status 200 met een lijst van alle doelen die zijn verzonden voor publicatie waartoe u toegang hebt, op basis van de IMS-organisatie-id en de sandboxnaam die u hebt gebruikt. Eén `configId` komt overeen met de publicatieaanvraag voor één doel.

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
| `destinationId` | String | De bestemmingsidentiteitskaart van de bestemmingsconfiguratie die u voor het publiceren hebt voorgelegd. |
| `publishDetailsList.configId` | String | De unieke id van de bestemming publiceert het verzoek voor uw verzonden bestemming. |
| `publishDetailsList.allowedOrgs` | String | Keert de organisaties van het Experience Platform terug waarvoor de bestemming beschikbaar is. <br> <ul><li> Voor `"destinationType": "PUBLIC"` retourneert deze parameter `"*"` , wat betekent dat het doel beschikbaar is voor alle organisaties van het Experience Platform.</li><li> Voor `"destinationType": "DEV"` retourneert deze parameter de organisatie-id van de organisatie die u hebt gebruikt voor het schrijven en testen van het doel.</li></ul> |
| `publishDetailsList.status` | String | De status van uw doelpublicatieverzoek. Mogelijke waarden zijn `TEST` , `REVIEW` , `APPROVED` , `PUBLISHED` , `DENIED` , `REVOKED` , `DEPRECATED` . Doelen met de waarde `PUBLISHED` zijn live en kunnen door klanten van het Experience Platform worden gebruikt. |
| `publishDetailsList.destinationType` | String | Het type bestemming. Waarden kunnen `DEV` en `PUBLIC` zijn. `DEV` komt overeen met het doel in uw organisatie van het Experience Platform. `PUBLIC` komt overeen met het doel dat u hebt verzonden voor publicatie. Denk aan deze twee opties in Git-termen, waarbij de versie van `DEV` uw lokale ontwerpvertakking vertegenwoordigt en de versie van `PUBLIC` de externe hoofdvertakking. |
| `publishDetailsList.publishedDate` | String | De datum waarop de bestemming voor publicatie werd voorgelegd, in tijdperk. |

{style="table-layout:auto"}

+++

>[!TAB  wint een specifiek het publiceren verzoek  terug]

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

Als u een `DESTINATION_ID` in de API-aanroep hebt doorgegeven, retourneert de reactie HTTP-status 200 met gedetailleerde informatie over de opgegeven publicatieaanvraag voor de bestemming.

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
| `destinationId` | String | De bestemmingsidentiteitskaart van de bestemmingsconfiguratie die u voor het publiceren hebt voorgelegd. |
| `publishDetailsList.configId` | String | De unieke id van de bestemming publiceert het verzoek voor uw verzonden bestemming. |
| `publishDetailsList.allowedOrgs` | String | Keert de organisaties van het Experience Platform terug waarvoor de bestemming beschikbaar is. <br> <ul><li> Voor `"destinationType": "PUBLIC"` retourneert deze parameter `"*"` , wat betekent dat het doel beschikbaar is voor alle organisaties van het Experience Platform.</li><li> Voor `"destinationType": "DEV"` retourneert deze parameter de organisatie-id van de organisatie die u hebt gebruikt voor het schrijven en testen van het doel.</li></ul> |
| `publishDetailsList.status` | String | De status van uw doelpublicatieverzoek. Mogelijke waarden zijn `TEST` , `REVIEW` , `APPROVED` , `PUBLISHED` , `DENIED` , `REVOKED` , `DEPRECATED` . Doelen met de waarde `PUBLISHED` zijn live en kunnen door klanten van het Experience Platform worden gebruikt. |
| `publishDetailsList.destinationType` | String | Het type bestemming. Waarden kunnen `DEV` en `PUBLIC` zijn. `DEV` komt overeen met het doel in uw organisatie van het Experience Platform. `PUBLIC` komt overeen met het doel dat u hebt verzonden voor publicatie. Denk aan deze twee opties in Git-termen, waarbij de versie van `DEV` uw lokale ontwerpvertakking vertegenwoordigt en de versie van `PUBLIC` de externe hoofdvertakking. |
| `publishDetailsList.publishedDate` | String | De datum waarop de bestemming voor publicatie werd voorgelegd, in tijdperk. |

{style="table-layout:auto"}

+++

>[!ENDTABS]

## API-foutafhandeling

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Verwijs naar [ API statuscodes ](../../../landing/troubleshooting.md#api-status-codes) en [ de fouten van de verzoekkopbal ](../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van het Platform.
