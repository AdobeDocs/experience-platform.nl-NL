---
description: De server en malplaatjespecs kunnen in Adobe Experience Platform Destination SDK via het gemeenschappelijke eindpunt `/authoring/bestemmings-servers worden gevormd.
title: Configuratieopties voor server- en sjabloonspecificaties in Destination SDK
exl-id: cf493ed5-0bdb-4b90-b84d-73926a566a2a
source-git-commit: 92bca3600d854540fd2badd925e453fba41601a7
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 5%

---

# Configuratieopties voor streaming doelserver- en sjabloonspecificaties

## Overzicht {#overview}

De server en malplaatjespecs kunnen in Adobe Experience Platform Destination SDK via het gemeenschappelijke eindpunt worden gevormd `/authoring/destination-servers`. Lezen [API-eindpuntbewerkingen voor doelen](./destination-server-api.md) voor een volledige lijst van verrichtingen kunt u op het eindpunt uitvoeren.

## Serverspecificaties {#server-specs}

![Serverconfiguratie gemarkeerd](./assets/server-configuration.png)

Klanten kunnen gegevens van Adobe Experience Platform naar uw bestemming activeren via HTTP-export. De serverconfiguratie bevat informatie over de server die de berichten ontvangt (de server aan uw kant).

Dit proces levert gebruikersgegevens als reeks berichten van HTTP aan uw bestemmingsplatform. De onderstaande parameters vormen de HTTP-serverspectsjabloon.

| Parameter | Type | Beschrijving |
|---|---|---|
| `name` | Tekenreeks | *Vereist.* Vertegenwoordigt een vriendschappelijke naam van uw server, zichtbaar slechts aan Adobe. Deze naam is niet zichtbaar aan partners of klanten. Voorbeeld `Moviestar destination server`. |
| `destinationServerType` | Tekenreeks | *Vereist.* Instellen op `URL_BASED` voor streamingdoelen. |
| `templatingStrategy` | Tekenreeks | *Vereist.* <ul><li>Gebruiken `PEBBLE_V1` als u een macro in plaats van een vaste waarde in het dialoogvenster `value` veld. Gebruik deze optie als u een eindpunt als: `https://api.moviestar.com/data/{{customerData.region}}/items` </li><li> Gebruiken `NONE` als er aan de Adobe zijde geen transformatie nodig is, bijvoorbeeld als u een eindpunt hebt, zoals: `https://api.moviestar.com/data/items` </li></ul> |
| `value` | Tekenreeks | *Vereist.* Vul het adres van het API eindpunt in dat Experience Platform zou moeten verbinden met. |

{style=&quot;table-layout:auto&quot;}

## Sjabloonspecificaties {#template-specs}

![Sjabloonconfiguratie gemarkeerd](./assets/template-configuration.png)

Met de sjabloonspecificatie kunt u configureren hoe het geëxporteerde bericht naar uw bestemming wordt opgemaakt. Adobe gebruikt een sjabloontaal die lijkt op [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) om de velden van het XDM-schema om te zetten in een indeling die door uw bestemming wordt ondersteund. Ga voor meer informatie over de transformatie naar de onderstaande koppelingen:

* [Berichtindeling](./message-format.md)
* [Een sjabloontaal gebruiken voor de transformaties voor identiteit, kenmerken en segmentlidmaatschap ](./message-format.md#using-templating)

>[!TIP]
>
>Adobe biedt een [ontwikkelaarsgereedschap](./create-template.md) waarmee u een sjabloon voor berichttransformatie kunt maken en testen.

## Streaming doelvoorbeeldconfiguratie  {#example-configuration}

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

| Parameter | Type | Beschrijving |
|---|---|---|
| `httpMethod` | Tekenreeks | *Vereist.* De methode die Adobe in vraag aan uw server zal gebruiken. Opties zijn `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | Tekenreeks | *Vereist.* Gebruik `PEBBLE_V1`. |
| `value` | Tekenreeks | *Vereist.* Dit koord is karakter-beschermde versie die de gegevens van de klanten van het Platform in het formaat omzet uw dienst verwacht. <br> Lees voor meer informatie over het schrijven van de sjabloon de [Sjabloonsectie gebruiken](./message-format.md#using-templating). <br> Raadpleeg voor meer informatie over het escapen van tekens de [RFC JSON-standaard, sectie 7](https://tools.ietf.org/html/rfc8259#section-7). <br> Voor een voorbeeld van een eenvoudige transformatie raadpleegt u de [Profielkenmerken](./message-format.md#attributes) transformatie. |
| `contentType` | Tekenreeks | *Vereist.* Het inhoudstype dat uw server accepteert. Deze waarde is zeer waarschijnlijk `application/json`. |

{style=&quot;table-layout:auto&quot;}