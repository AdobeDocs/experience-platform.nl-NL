---
description: Deze pagina bevat een overzicht en beschrijving van alle API-bewerkingen die u kunt uitvoeren met het API-eindpunt `/authoring/destination/publish`.
title: API-eindpuntbewerkingen voor doelen publiceren
exl-id: 0564a132-42f4-478c-9197-9b051acf093c
source-git-commit: 6dd8a94e46b9bee6d1407e7ec945a722d8d7ecdb
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 2%

---

# API-bewerkingen voor eindpunt doelen publiceren {#publish-destination}

>[!IMPORTANT]
>
>**API-eindpunt**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Deze pagina bevat een overzicht en beschrijving van alle API-bewerkingen die u kunt uitvoeren met de `/authoring/destinations/publish` API-eindpunt.

Nadat u hebt gevormd en uw bestemming getest, kunt u het voorleggen aan Adobe voor overzicht en het publiceren.

Gebruik het API-eindpunt voor publicatiedoelen om een publicatieverzoek in te dienen wanneer:
* Als partner van Destination SDK, wilt u uw geproduceerde bestemming beschikbaar over alle organisaties van het Experience Platform voor alle klanten van het Experience Platform aan gebruik maken;
* U wilt uw aangepaste bestemming beschikbaar maken in uw eigen organisatie van het Experience Platform, voor alle sandboxen.

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
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"LIMITED",
   "allowedOrgs":[
      "xyz@AdobeOrg",
      "lmn@AdobeOrg"
   ]
}
```

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `destinationId` | Tekenreeks | De bestemmingsidentiteitskaart van de bestemmingsconfiguratie die u voor het publiceren voorlegt. Krijg bestemmingsidentiteitskaart van een bestemmingsconfiguratie door te gebruiken [API-naslaggids voor doelconfiguratie](./destination-configuration-api.md#retrieve-list). |
| `destinationAccess` | Tekenreeks | `ALL` of `LIMITED`. Geef op of u uw bestemming wilt weergeven in de catalogus voor alle klanten van het Experience Platform of alleen voor bepaalde organisaties. <br> **Opmerking**: Als u `LIMITED`, zal de bestemming voor uw organisatie van het Experience Platform slechts worden gepubliceerd. Als u de bestemming aan een ondergroep van de organisaties van het Experience Platform voor klant testende doeleinden wilt publiceren, gelieve te bereiken aan de steun van de Adobe. |
| `allowedOrgs` | Tekenreeks | Als u `"destinationAccess":"LIMITED"`, de organisaties van het Experience Platform specificeren waarvoor de bestemming beschikbaar zal zijn. |

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

Het volgende verzoek zal de lijst van bestemmingen terugwinnen die voor publicatie worden voorgelegd die u toegang tot hebt, die op Organisatie IMS en zandbakconfiguratie wordt gebaseerd.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
         "configId":"string",
         "allowedOrgs":[
            "xyz@AdobeOrg",
            "lmn@AdobeOrg"
         ],
         "status":"TEST",
         "publishedDate":"1630617746"
      }
   ]
}
    
```

| Parameter | Type | Beschrijving |
|---------|----------|------|
| `destinationId` | Tekenreeks | De bestemmingsidentiteitskaart van de bestemmingsconfiguratie die u voor het publiceren hebt voorgelegd. |
| `publishDetailsList.configId` | Tekenreeks | De unieke id van de bestemming publiceert het verzoek voor uw verzonden bestemming. |
| `publishDetailsList.allowedOrgs` | Tekenreeks | Keert de organisaties van het Experience Platform terug waarvoor de bestemming beschikbaar zou moeten zijn. |
| `publishDetailsList.status` | Tekenreeks | De status van uw doelpublicatieverzoek. Mogelijke waarden zijn `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. |
| `publishDetailsList.publishedDate` | Tekenreeks | De datum waarop de bestemming voor publicatie werd voorgelegd, in tijdperk. |

{style=&quot;table-layout:auto&quot;}

## Een bestaand doelpublicatieverzoek bijwerken {#update}

U kunt de toegestane organisaties in een bestaand doel bijwerken publicatieverzoek door een PUT aan te vragen bij `/authoring/destinations/publish` eindpunt en het verstrekken van identiteitskaart van de bestemming waarvoor u de toegestane organisaties wilt bijwerken. In het lichaam van de vraag, verstrek de bijgewerkte toegestane organisaties.

**API-indeling**


```http
PUT /authoring/destinations/publish/{DESTINATION_ID}
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{DESTINATION_ID}` | De id van het doel waarvoor u de publicatieaanvraag wilt bijwerken. |

**Verzoek**

Het volgende verzoek werkt een bestaand bestemmingspublicatieverzoek bij, dat door de parameters wordt gevormd die in de lading worden verstrekt. In de voorbeeldvraag hieronder, werken wij de toegestane organisaties bij.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destinations/publish/1230e5e4-4ab8-4655-ae1e-a6296b30f2ec \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"LIMITED",
   "allowedOrgs":[
      "abc@AdobeOrg",
      "def@AdobeOrg"
   ]
}
```

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
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
         "configId":"string",
         "allowedOrgs":[
            "xyz@AdobeOrg",
            "lmn@AdobeOrg"
         ],
         "status":"TEST",
         "publishedDate":"string"
      }
   ]
}
```

## API-foutafhandeling

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Zie [API-statuscodes](../../landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](../../landing/troubleshooting.md#request-header-errors) in de gids voor het oplossen van problemen met Platforms.

## Volgende stappen

Nadat u dit document hebt gelezen, weet u nu hoe u een publicatieverzoek voor uw doel kunt indienen. Het Adobe Experience Platform-team zal uw publicatieaanvraag beoordelen en met vijf werkdagen teruggaan naar u.
