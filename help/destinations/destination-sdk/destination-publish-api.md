---
description: Deze pagina bevat een overzicht en beschrijving van alle API-bewerkingen die u kunt uitvoeren met het API-eindpunt `/authoring/destination/publish`.
title: API-eindpuntbewerkingen voor doelen publiceren
exl-id: 0564a132-42f4-478c-9197-9b051acf093c
source-git-commit: 1fb0fde2054528679235268ae96e3b7e78de80ef
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 1%

---

# API-bewerkingen voor eindpunt doelen publiceren {#publish-destination}

>[!IMPORTANT]
>
>U hoeft dit API-eindpunt alleen te gebruiken als u een geproductieerde (openbare) bestemming verzendt die door andere klanten van het Experience Platform moet worden gebruikt. Als u een privé bestemming voor uw eigen gebruik creeert, te hoeven u niet om de bestemming formeel voor te leggen gebruikend het publiceren API.

>[!IMPORTANT]
>
>**API-eindpunt**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Deze pagina bevat een overzicht en beschrijving van alle API-bewerkingen die u kunt uitvoeren met de `/authoring/destinations/publish` API-eindpunt.

Nadat u hebt gevormd en uw bestemming getest, kunt u het voorleggen aan Adobe voor overzicht en het publiceren. Lezen [Ter controle een bestemming verzenden die is geschreven in Destination SDK](./submit-destination.md) voor alle andere stappen moet u als deel van het proces van de bestemmingsvoorlegging doen.

Gebruik het API-eindpunt voor publicatiedoelen om een publicatieverzoek in te dienen wanneer:

* Als partner van Destination SDK, wilt u uw geproduceerde bestemming beschikbaar over alle organisaties van het Experience Platform voor alle klanten van het Experience Platform aan gebruik maken;
* U maakt *alle updates* naar uw configuraties. De updates van de configuratie worden weerspiegeld in de bestemming slechts nadat u een nieuw het publiceren verzoek indient, dat door het team van het Experience Platform wordt goedgekeurd.

<!-- * You want to make your custom destination available in your own Experience Platform organization, across all sandboxes. -->

## Aan de slag met API-bewerkingen voor doelpublicatie {#get-started}

Controleer voordat je doorgaat de [gids Aan de slag](./getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings creatie en vereiste kopballen te verkrijgen.

## Een doelconfiguratie verzenden voor publicatie {#create}

U kunt een bestemmingsconfiguratie voor het publiceren voorleggen door een verzoek van de POST aan de `/authoring/destinations/publish` eindpunt.

**API-indeling**

```http
POST /authoring/destinations/publish
```

**Verzoek**

Het volgende verzoek legt een bestemming voor publicatie voor, over de organisaties die door de parameters worden gevormd die in de lading worden verstrekt. De hieronder vermelde lading omvat alle parameters die door `/authoring/destinations/publish` eindpunt.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"ALL"
}
```

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `destinationId` | Tekenreeks | De bestemmingsidentiteitskaart van de bestemmingsconfiguratie die u voor het publiceren voorlegt. Krijg bestemmingsidentiteitskaart van een bestemmingsconfiguratie door te gebruiken [API-naslaggids voor doelconfiguratie](./destination-configuration-api.md#retrieve-list). |
| `destinationAccess` | Tekenreeks | Gebruiken `ALL` voor uw bestemming om in de catalogus voor alle klanten van het Experience Platform te verschijnen. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een succesvolle reactie keert status 201 van HTTP met details van uw bestemmings terug publicatieverzoek.

## Publicatieverzoeken voor bestemming weergeven {#retrieve-list}

U kunt een lijst van alle bestemmingen terugwinnen die voor publicatie voor uw organisatie IMS door een verzoek van de GET aan wordt voorgelegd `/authoring/destinations/publish` eindpunt.

**API-indeling**

```http
GET /authoring/destinations/publish
```

**Verzoek**

Het volgende verzoek wint de lijst van bestemmingen terug die voor publicatie worden voorgelegd die u toegang tot hebt, die op Organisatie IMS en zandbakconfiguratie wordt gebaseerd.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

De volgende reactie retourneert HTTP-status 200 met een lijst van doelen die zijn ingediend voor publicatie waartoe u toegang hebt, op basis van de IMS-organisatie-id en de sandboxnaam die u hebt gebruikt. Eén `configId` komt overeen met de publicatieaanvraag voor één bestemming.

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
| `publishDetailsList.destinationType` | Tekenreeks | Het type bestemming. Waarden kunnen `DEV` en `PUBLIC`. `DEV` komt overeen met het doel in uw organisatie Experience Platform. `PUBLIC` komt overeen met het doel dat u hebt verzonden voor publicatie. Denk aan deze twee opties in Git-termen, waar de `DEV` versie staat voor uw lokale ontwerpvertakking en de `PUBLIC` versie staat voor de externe hoofdvertakking. |
| `publishDetailsList.publishedDate` | Tekenreeks | De datum waarop de bestemming voor publicatie werd voorgelegd, in tijdperk. |

{style=&quot;table-layout:auto&quot;}

## Hiermee wordt de status van een specifiek publicatieverzoek voor een doel opgehaald {#get}

U kunt gedetailleerde informatie over een specifieke bestemmings terugwinnen publicatieverzoek door een verzoek van de GET aan `/authoring/destinations/publish` eindpunt en het verstrekken van identiteitskaart van de bestemming waarvoor u de het publiceren status wilt terugwinnen.

**API-indeling**

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{DESTINATION_ID}` | De id van het doel waarvoor u de publicatiestatus wilt ophalen. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish/1230e5e4-4ab8-4655-ae1e-a6296b30f2ec \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met gedetailleerde informatie over de gespecificeerde bestemmings terug publicatieverzoek.

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

## API-foutafhandeling

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Zie [API-statuscodes](../../landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](../../landing/troubleshooting.md#request-header-errors) in de gids voor het oplossen van problemen met Platforms.

## Volgende stappen

Nadat u dit document hebt gelezen, weet u nu hoe u een publicatieverzoek voor uw doel kunt indienen. Het Adobe Experience Platform-team zal uw publicatieaanvraag beoordelen en met vijf werkdagen teruggaan naar u.
