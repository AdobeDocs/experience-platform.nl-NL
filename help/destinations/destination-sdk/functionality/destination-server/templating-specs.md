---
description: Leer hoe te om de HTTP- verzoeken te formatteren die naar uw eindpunt worden verzonden. Gebruik het /authoring/bestemmings-servers eindpunt om bestemmings server te vormen die specs in Adobe Experience Platform Destination SDK templating.
title: Sjabloonspecificaties voor doelen die met Destination SDK zijn gemaakt
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 3%

---


# Sjabloonspecificaties voor bestemmingen die met Destination SDK zijn gemaakt

Gebruik het malplaatjespecifieke deel van de configuratie van de bestemmingsserver om te vormen hoe te om de HTTP- verzoeken te formatteren die naar uw bestemming worden verzonden.

In een sjabloonspecificatie kunt u definiëren hoe u profielkenmerkvelden transformeert tussen het XDM-schema en de indeling die uw platform ondersteunt.

Sjabloonspecificaties maken deel uit van de configuratie van de doelserver voor realtime (streaming) doelen.

Om te begrijpen waar deze component in een integratie past die met Destination SDK wordt gecreeerd, zie het diagram in [configuratieopties](../configuration-options.md) documentatie of bekijk de gids over hoe te [gebruik Destination SDK om een het stromen bestemming te vormen](../../guides/configure-destination-instructions.md#create-server-template-configuration).

U kunt de sjabloonspecificaties voor uw bestemming configureren via de `/authoring/destination-servers` eindpunt. Zie de volgende API verwijzingspagina&#39;s voor gedetailleerde API vraagvoorbeelden waar u de componenten kunt vormen die in deze pagina worden getoond.

* [Een doelserverconfiguratie maken](../../authoring-api/destination-server/create-destination-server.md)
* [Een doelserverconfiguratie bijwerken](../../authoring-api/destination-server/update-destination-server.md)

>[!IMPORTANT]
>
>Alle parameternamen en -waarden die door Destination SDK worden ondersteund, zijn **hoofdlettergevoelig**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Ondersteunde integratietypen {#supported-integration-types}

Raadpleeg de onderstaande tabel voor meer informatie over de integratietypen die de op deze pagina beschreven functionaliteit ondersteunen.

| Type integratie | Ondersteunt functionaliteit |
|---|---|
| Integraties in realtime (streaming) | Ja |
| Op bestanden gebaseerde (batch) integratie | Nee |

## Een sjabloonspecificatie configureren {#configure-template-spec}

Adobe gebruikt een sjabloontaal die lijkt op [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) om de velden van het XDM-schema om te zetten in een indeling die door uw bestemming wordt ondersteund.

![Sjabloonconfiguratie gemarkeerd](../../assets/functionality/destination-server/template-configuration.png)

Ga voor meer informatie over de transformatie naar de onderstaande koppelingen:

* [Berichtindeling](message-format.md)
* [Een sjabloontaal gebruiken voor de transformaties voor identiteit, kenmerken en publieksleiding](message-format.md#using-templating)

>[!TIP]
>
>Adobe biedt een [ontwikkelaarsgereedschap](../../testing-api/streaming-destinations/create-template.md) waarmee u een sjabloon voor berichttransformatie kunt maken en testen.

Zie onder een voorbeeld van een HTTP-aanvraagsjabloon, samen met beschrijvingen van elke individuele parameter.

```json
{
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
| `httpMethod` | Tekenreeks | *Vereist.* De methode die Adobe in vraag aan uw server zal gebruiken. Ondersteunde methoden: `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | Tekenreeks | *Vereist.* Gebruik `PEBBLE_V1`. |
| `value` | Tekenreeks | *Vereist.* Dit koord is de karakter-beschermde versie van het malplaatje dat de HTTP- verzoeken door Platform in het formaat formatteert dat door uw bestemming wordt verwacht. <br> Voor informatie over het schrijven van de sjabloon leest u de sectie over [gebruik maken van sjablonen](message-format.md#using-templating). <br> Raadpleeg voor meer informatie over het escapen van tekens de [RFC JSON-standaard, sectie 7](https://tools.ietf.org/html/rfc8259#section-7). <br> Voor een voorbeeld van een eenvoudige transformatie raadpleegt u de [profielkenmerken](message-format.md#attributes) transformatie. |
| `contentType` | Tekenreeks | *Vereist.* Het inhoudstype dat uw server accepteert. Afhankelijk van het type uitvoer dat uw transformatiesjabloon produceert, kan dit een van de ondersteunde uitvoerbestanden zijn [Inhoud van HTTP-toepassingen](https://www.iana.org/assignments/media-types/media-types.xhtml#application). In de meeste gevallen moet deze waarde worden ingesteld op `application/json`. |

{style="table-layout:auto"}

## Volgende stappen {#next-steps}

Na het lezen van dit artikel, zou u een beter inzicht in moeten hebben wat een malplaatjespecificatie is, en hoe u het kunt vormen.

Raadpleeg de volgende artikelen voor meer informatie over de andere componenten van de doelserver:

* [Server specs voor bestemmingen die met Destination SDK worden gecreeerd](server-specs.md)
* [Berichtindeling](message-format.md)
* [Configuratie bestandsindeling](file-formatting.md)