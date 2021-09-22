---
description: De server en malplaatjespecs kunnen in de Doel SDK van Adobe Experience Platform via het gemeenschappelijke eindpunt `/authoring/bestemmings-servers worden gevormd.
title: Configuration options for server and template specs in Destination SDK
exl-id: cf493ed5-0bdb-4b90-b84d-73926a566a2a
source-git-commit: 2ed132cd16db64b5921c5632445956f750fead56
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 5%

---

# Configuratieopties voor server- en sjabloonspecificaties

## Overzicht {#overview}

De server- en sjabloonspecificaties kunnen worden geconfigureerd in Adobe Experience Platform Destination SDK via het gemeenschappelijke eindpunt `/authoring/destination-servers`. Lees [Doelen API eindpuntverrichtingen](./destination-server-api.md) voor een volledige lijst van verrichtingen u op het eindpunt kunt uitvoeren.

## Voorbeeldconfiguratie {#example-configuration}

```json
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

## Serverspecificaties {#server-specs}

![Serverconfiguratie gemarkeerd](./assets/server-configuration.png)

Klanten kunnen gegevens van Adobe Experience Platform naar uw bestemming activeren via HTTP-export. De serverconfiguratie bevat informatie over de server die de berichten ontvangt (de server aan uw kant).

Dit proces levert gebruikersgegevens als reeks berichten van HTTP aan uw bestemmingsplatform. De onderstaande parameters vormen de HTTP-serverspectsjabloon.

| Parameter | Type | Beschrijving |
|---|---|---|
| `name` | Tekenreeks | *Vereist.* Vertegenwoordigt een vriendschappelijke naam van uw server, zichtbaar slechts aan Adobe. Deze naam is niet zichtbaar aan partners of klanten. Voorbeeld `Moviestar destination server`. |
| `destinationServerType` | Tekenreeks | *Vereist.* `URL_BASED` is momenteel de enige beschikbare optie. |
| `templatingStrategy` | Tekenreeks | *Vereist.* <ul><li>Gebruik `PEBBLE_V1` als Adobe de URL moet transformeren in het onderstaande veld `value`. Gebruik deze optie als u een eindpunt als: `https://api.moviestar.com/data/{{customerData.region}}/items` </li><li> Gebruik `NONE` als er geen transformatie nodig is aan de Adobe zijde, bijvoorbeeld als u een eindpunt hebt zoals: `https://api.moviestar.com/data/items` </li></ul> |
| `value` | Tekenreeks | *Vereist.* Vul het adres van het API eindpunt in dat Experience Platform zou moeten verbinden met. |

{style=&quot;table-layout:auto&quot;}

<!--

|Parameter | Type | Description|
|---------|----------|------|
|`hostname` | String | This is the hostname of your server. Example `https://data-in.acmecompany.net`.  |
|`port` | integer | The server port of your destination, for example `443`, `80`. |
|`maxUsersPerRequest` | integer | Specifies the maximum number of users per request allowed for your server. |
|`path` | String | This represents the url path and parameters of your server. Example:  `/path/to/import` |
|`httpMethod` | String | The method that Adobe will use in calls to your server. Options are `GET`, `PUT`, `POST`, `DELETE`, `PATCH`, `OPTIONS`, `HEAD`. |
|`contentType` | String | Defines how to structure the content sent to your servers. Supported options are JSON and XML. |

-->

## Sjabloonspecificaties {#template-specs}

![Sjabloonconfiguratie gemarkeerd](./assets/template-configuration.png)

Met de sjabloonspecificatie kunt u configureren hoe het geëxporteerde bericht naar uw bestemming wordt opgemaakt. Adobe gebruikt een malplaatjetaal gelijkend op [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) om de gebieden van het schema XDM in een formaat om te zetten dat door uw bestemming wordt gesteund. Ga voor meer informatie over de transformatie naar de onderstaande koppelingen:

* [Berichtindeling](./message-format.md)
* [Een sjabloontaal gebruiken voor de transformaties voor identiteit, kenmerken en segmentlidmaatschap ](./message-format.md#using-templating)

>[!TIP]
>
>Adobe biedt een [ontwikkelaarshulpmiddel](./create-template.md) aan dat u helpt een malplaatje van de berichttransformatie tot stand brengen en testen.

| Parameter | Type | Beschrijving |
|---|---|---|
| `httpMethod` | Tekenreeks | *Vereist.* De methode die Adobe in vraag aan uw server zal gebruiken. De opties zijn `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | Tekenreeks | *Vereist.* Gebruik `PEBBLE_V1`. |
| `value` | Tekenreeks | *Vereist.* Dit koord is karakter-beschermde versie die de gegevens van de klanten van het Platform in het formaat omzet uw dienst verwacht. <br> Voor informatie hoe te om het malplaatje te schrijven, lees de  [Gebruikende malplaatjesectie](./message-format.md#using-templating). <br> Raadpleeg de  [RFC JSON-standaard, sectie 7](https://tools.ietf.org/html/rfc8259#section-7) voor meer informatie over het escapen van tekens. <br> Zie  [Profielkenmerktransformatie voor een voorbeeld van een eenvoudige ](./message-format.md#attributes) transformatie. |
| `contentType` | Tekenreeks | *Vereist.* Het inhoudstype dat uw server accepteert. Deze waarde is zeer waarschijnlijk `application/json`. |

{style=&quot;table-layout:auto&quot;}

<!--

|`requestBody` | String | The request body contains the data exported from Real-time CDP, activated to your destination. <br> We need to know which data format macros your destination should support. See [Outbound Template Macros](https://docs.adobe.com/content./en/audience-manager/user-guide/implementation-integration-guides/receiving-audience-data/batch-outbound-data-transfers/outbound-template-macros.html) and [Outbound Macro Examples](https://docs.adobe.com/content./en/audience-manager/user-guide/implementation-integration-guides/receiving-audience-data/batch-outbound-data-transfers/outbound-macro-examples.html) for examples from Adobe's DMP, Audience Manager. <br> See also, [Message format](#message-format) for further information.  |
|`queryParameters` | String | Request parameters defined as macros. See above.|



<br>&nbsp;

#### Example

A valid HTTP specs template could look like below:

```

{
  "name": "ACME company HTTP template",
  "type": "HTTP", 
  "httpTemplate": {
    "httpMethod": "POST",
    "requestBody": "{"AdvertiserId":"12345", "DataCenterId": 2, "SegmentID":"dfd215e4-8d6b-4fdb-90b9-fab4456f2c9d","Data":[{"Name":"4321"}]}",
    "queryParameters": "{"AdvertiserId":"12345", "DataCenterId": 2, "SegmentID":"dfd215e4-8d6b-4fdb-90b9-fab4456f2c9d","Data":[{"Name":"4321"}]}",
    "contentType": "JSON"
  }
}

```

// commenting out this part as these types of destination specs are not supported in phase one

### File specifications

File-based destinations deliver file exports containing segment qualifications and profile attributes to your preferred storage location. If you want to set up a batch file-based destination, the template we'll use will be as below:

## Server specs

The server configuration contains information about the server receiving the messages (the server on your side). 
Adobe Real-time CDP currently supports three types of server configurations:
* URL
* File-based SFTP
* File-based S3

For URL destinations, you would provide us your server's information, for File-based SFTP and File-based S3 you would provide information as to the storage locations where files should be delivered.
Provide us the necessary information about your server or storage locations, as shown in the sections below.


**urlBasedDestination**

|Parameter | Type | Description|
|---------|----------|------|
|`hostname` | String | This is the hostname of your server. Example `https://data-in.acmecompany.net`.  |
|`port` | integer | The server port of your destination, for example `443`, `80`. |
|`maxUsersPerRequest` | integer | Specifies the maximum number of users per request allowed for your server. |
|`path` | String | This represents the url path and parameters of your server. Example:  `/path/to/import` |


// commenting out this part as these types of destination specs are not supported in phase one

**SFTP Destinations**

For FTP destinations, we need the protocol details below:

Parameter | Type | 
---------|----------|
 hostname | String | 
 port | integer | 
 rootDirectory | String | 
 moveToWhenCompleted | integer | 
 tmpFileRename | integer | 
 encryptionMode | String |
 filenameSuffix | String | 

**Amazon S3 Destinations**

For Amazon S3 destinations, we need the protocol details below:

Parameter | Description | 
---------|----------|
 bucket | Your Amazon S3 bucket name | 
 path | Your Amazon S3 bucket path | 

-->
