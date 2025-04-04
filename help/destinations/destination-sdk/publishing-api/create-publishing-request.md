---
description: Leer hoe u een API-aanroep kunt opmaken om een doelpublicatieaanvraag via Adobe Experience Platform Destination SDK te verzenden.
title: Een doelpublicatieverzoek maken
exl-id: 913be9de-a699-4756-885d-b3761ec729cb
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Een doelpublicatieverzoek maken

>[!IMPORTANT]
>
>U hoeft dit API-eindpunt alleen te gebruiken als u een geproductieerde (openbare) bestemming verzendt die door andere Experience Platform-klanten moet worden gebruikt. Als u een privé bestemming voor uw eigen gebruik creeert, te hoeven u niet om de bestemming formeel voor te leggen gebruikend het publiceren API.

>[!IMPORTANT]
>
>**API eindpunt**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Nadat u de bestemming hebt geconfigureerd en getest, kunt u deze naar Adobe verzenden voor revisie en publicatie. Lees [ voorlegt voor overzicht een bestemming die in Destination SDK ](../guides/submit-destination.md) voor alle andere stappen wordt geschreven u als deel van het proces van de bestemmingsvoorlegging moet doen.

Gebruik het API-eindpunt voor publicatiedoelen om een publicatieverzoek in te dienen wanneer:

* Als partner van Destination SDK, wilt u uw geproduceerde bestemming beschikbaar over alle organisaties van Experience Platform voor alle klanten van Experience Platform aan gebruik maken;
* U maakt *om het even welke updates* aan uw configuraties. De updates van de configuratie worden weerspiegeld in de bestemming slechts nadat u een nieuw het publiceren verzoek indient, dat door het team van Experience Platform wordt goedgekeurd.

>[!IMPORTANT]
>
>Alle parameternamen en waarden die door Destination SDK worden gesteund zijn **gevoelig geval**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Aan de slag met API-bewerkingen voor doelpublicatie {#get-started}

Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](../getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings authoring en vereiste kopballen te verkrijgen.

## Een doelconfiguratie verzenden voor publicatie {#create}

U kunt een bestemmingsconfiguratie voor het publiceren voorleggen door een POST- verzoek aan het `/authoring/destinations/publish` eindpunt te doen.

**API formaat**

```http
POST /authoring/destinations/publish
```

+++verzoek

Het volgende verzoek legt een bestemming voor publicatie voor, over de organisaties die door de parameters worden gevormd die in de lading worden verstrekt. De onderstaande lading bevat alle parameters die door het `/authoring/destinations/publish` -eindpunt worden geaccepteerd.

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
| `destinationId` | String | De bestemmingsidentiteitskaart van de bestemmingsconfiguratie die u voor het publiceren voorlegt. Krijg bestemmingsidentiteitskaart van een bestemmingsconfiguratie door [ te gebruiken wint een vraag van de bestemmingsconfiguratie ](../authoring-api/destination-configuration/retrieve-destination-configuration.md) API terug. |
| `destinationAccess` | String | Gebruik `ALL` voor uw doel om in de catalogus voor alle Experience Platform-klanten te verschijnen. |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 201 van HTTP met details van uw bestemmings terug publicatieverzoek.

+++

## API-foutafhandeling

Destination SDK API-eindpunten volgen de algemene beginselen van Experience Platform API-foutberichten. Verwijs naar [ API statuscodes ](../../../landing/troubleshooting.md#api-status-codes) en [ de fouten van de verzoekkopbal ](../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van Experience Platform.

## Volgende stappen

Nadat u dit document hebt gelezen, weet u nu hoe u een publicatieverzoek voor uw doel kunt indienen. Het Adobe Experience Platform-team zal uw publicatieverzoek beoordelen en met vijf werkdagen teruggaan naar u.
