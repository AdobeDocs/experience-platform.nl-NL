---
description: Deze pagina illustreert de API vraag die wordt gebruikt om een configuratie van de bestemmingsserver door Adobe Experience Platform Destination SDK terug te winnen.
title: De configuratie van een doelserver ophalen
exl-id: 1b375343-e793-4c91-856f-af66fe71822e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# De configuratie van een doelserver ophalen

Deze pagina illustreert de API-aanvraag en -lading die u kunt gebruiken om informatie over een bestaande configuratie van de doelserver op te halen met behulp van het API-eindpunt `/authoring/destination-servers` .

Lees de volgende artikelen voor een gedetailleerde beschrijving van de mogelijkheden die bestemmingsservers gebruiken:

* [Serverspecificaties voor doelen die met Destination SDK zijn gemaakt](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Sjabloonspecificaties voor bestemmingen die zijn gemaakt met Destination SDK](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [Berichtindeling](../../../destination-sdk/functionality/destination-server/message-format.md)
* [Configuratie bestandsindeling](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Alle parameternamen en waarden die door Destination SDK worden gesteund zijn **gevoelig geval**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Aan de slag met API-bewerkingen voor doelserver {#get-started}

Alvorens verder te gaan, te herzien gelieve [&#x200B; begonnen gids &#x200B;](../../getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings authoring en vereiste kopballen te verkrijgen.

## De configuratie van een doelserver ophalen {#retrieve}

U kunt een bestaande configuratie van de bestemmingsserver terugwinnen door `GET` verzoek aan het `/authoring/destination-servers` eindpunt te doen.

>[!TIP]
>
>**API eindpunt**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

**API formaat**

Gebruik de volgende API-indeling om alle configuraties van de doelserver voor uw account op te halen.

```http
GET /authoring/destination-servers
```

Gebruik de volgende API-indeling om een specifieke doelserverconfiguratie op te halen, gedefinieerd door de parameter `{INSTANCE_ID}` .

```http
GET /authoring/destination-servers/{INSTANCE_ID}
```

De volgende twee verzoeken winnen alle configuraties van de bestemmingsserver voor uw IMS Organisatie, of een specifieke configuratie van de bestemmingsserver terug, afhankelijk van of u de `INSTANCE_ID` parameter in het verzoek overgaat.

Selecteer hieronder elk tabblad om de bijbehorende lading en de reacties weer te geven.

>[!BEGINTABS]

>[!TAB wint alle configuraties van de bestemmingsserver  terug]

Met de volgende aanvraag wordt de lijst opgehaald met doelserverconfiguraties waartoe u toegang hebt, op basis van [!DNL IMS Org ID] en sandboxconfiguratie.

+++verzoek

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Response

Een succesvol antwoord retourneert HTTP-status 200 met een lijst van doelserverconfiguraties waartoe u toegang hebt, op basis van de naam van de [!DNL IMS Org ID] en de sandbox die u hebt gebruikt. Eén `instanceId` komt overeen met één doelserver. De voorbeeldreactie hieronder bevat twee configuraties van de doelserver.

```json
{
   "items":[
      {
         "instanceId":"2307ec2b-4798-45a4-9239-5d0a2fb0ed67",
         "createdDate":"2020-11-17T06:49:24.331012Z",
         "lastModifiedDate":"2020-11-17T06:49:24.331012Z",
         "name":"Moviestar Destination Server",
         "destinationServerType":"URL_BASED",
         "urlBasedDestination":{
            "url":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"https://go.{% if destination.config.domain == \"US\" %}moviestar.com{% else %}moviestar.eu{% endif%}/api/named_users/tags"
            }
         },
         "httpTemplate":{
            "requestBody":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{ \"audience\": { \"named_user_id\": [ {% for named_user in input.profile.identityMap.named_user_id %} \"{{ named_user.id }}\"{% if not loop.last %},{% endif %} {% endfor %} ] }, {% if addedSegments(input.profile.segmentMembership.ups) is not empty %} \"add\": { \"adobe-segments\": [ {% for added_segment in addedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[added_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} {% if addedSegments(input.profile.segmentMembership.ups) is not empty and removedSegments(input.profile.segmentMembership.ups) is not empty %} , {% endif %} {% if removedSegments(input.profile.segmentMembership.ups) is not empty %} \"remove\": { \"adobe-segments\": [ {% for removed_segment in removedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[removed_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} }"
            },
            "httpMethod":"POST",
            "contentType":"application/json",
            "headers":[
               {
                  "header":"Accept",
                  "value":{
                     "templatingStrategy":"NONE",
                     "value":"application/vnd.moviestar+json; version=3;"
                  }
               }
            ]
         },
         "qos":{
            "name":"freeform"
         }
      },
      {
         "instanceId":"d88de647-a352-4824-8b46-354afc7acbff",
         "createdDate":"2020-11-17T16:50:59.635228Z",
         "lastModifiedDate":"2020-11-17T16:50:59.635228Z",
         "name":"Test11 Destination Server",
         "destinationServerType":"URL_BASED",
         "urlBasedDestination":{
            "url":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"https://go.{% if destination.config.domain == \"US\" %}moviestar.com{% else %}moviestar.eu{% endif%}/api/named_users/tags"
            }
         },
         "httpTemplate":{
            "requestBody":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{ \"audience\": { \"named_user_id\": [ {% for named_user in input.profile.identityMap.named_user_id %} \"{{ named_user.id }}\"{% if not loop.last %},{% endif %} {% endfor %} ] }, {% if addedSegments(input.profile.segmentMembership.ups) is not empty %} \"add\": { \"adobe-segments\": [ {% for added_segment in addedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[added_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} {% if addedSegments(input.profile.segmentMembership.ups) is not empty and removedSegments(input.profile.segmentMembership.ups) is not empty %} , {% endif %} {% if removedSegments(input.profile.segmentMembership.ups) is not empty %} \"remove\": { \"adobe-segments\": [ {% for removed_segment in removedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[removed_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} }"
            },
            "httpMethod":"POST",
            "contentType":"application/json",
            "headers":[
               {
                  "header":"Accept",
                  "value":{
                     "templatingStrategy":"NONE",
                     "value":"application/vnd.moviestar+json; version=3;"
                  }
               }
            ]
         },
         "qos":{
            "name":"freeform"
         }
      }
   ]
}
```

+++

>[!TAB wint een specifieke configuratie van de bestemmingsserver  terug]

Het volgende verzoek zal een specifieke configuraties van de bestemmingsserver terugwinnen die door de `{INSTANCE_ID}` parameter worden bepaald.

+++verzoek

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{INSTANCE_ID}` | De id van de configuratie van de doelserver die u wilt ophalen. |

+++

+++Response

Een geslaagde reactie retourneert HTTP-status 200 met de configuratie van de doelserver die overeenkomt met de `{INSTANCE_ID}` die u hebt opgegeven.

```json
{
   "items":[
      {
         "instanceId":"2307ec2b-4798-45a4-9239-5d0a2fb0ed67",
         "createdDate":"2020-11-17T06:49:24.331012Z",
         "lastModifiedDate":"2020-11-17T06:49:24.331012Z",
         "name":"Moviestar Destination Server",
         "destinationServerType":"URL_BASED",
         "urlBasedDestination":{
            "url":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"https://go.{% if destination.config.domain == \"US\" %}moviestar.com{% else %}moviestar.eu{% endif%}/api/named_users/tags"
            }
         },
         "httpTemplate":{
            "requestBody":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{ \"audience\": { \"named_user_id\": [ {% for named_user in input.profile.identityMap.named_user_id %} \"{{ named_user.id }}\"{% if not loop.last %},{% endif %} {% endfor %} ] }, {% if addedSegments(input.profile.segmentMembership.ups) is not empty %} \"add\": { \"adobe-segments\": [ {% for added_segment in addedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[added_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} {% if addedSegments(input.profile.segmentMembership.ups) is not empty and removedSegments(input.profile.segmentMembership.ups) is not empty %} , {% endif %} {% if removedSegments(input.profile.segmentMembership.ups) is not empty %} \"remove\": { \"adobe-segments\": [ {% for removed_segment in removedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[removed_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} }"
            },
            "httpMethod":"POST",
            "contentType":"application/json",
            "headers":[
               {
                  "header":"Accept",
                  "value":{
                     "templatingStrategy":"NONE",
                     "value":"application/vnd.moviestar+json; version=3;"
                  }
               }
            ]
         },
         "qos":{
            "name":"freeform"
         }
      }
   ]
}
```

+++

>[!ENDTABS]

## API-foutafhandeling {#error-handling}

Destination SDK API-eindpunten volgen de algemene beginselen van Experience Platform API-foutberichten. Verwijs naar [&#x200B; API statuscodes &#x200B;](../../../../landing/troubleshooting.md#api-status-codes) en [&#x200B; de fouten van de verzoekkopbal &#x200B;](../../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van Experience Platform.

## Volgende stappen {#next-steps}

Na het lezen van dit document weet u nu hoe u een configuratie van de doelserver kunt ophalen via het Destination SDK `/authoring/destination-servers` API-eindpunt.

Raadpleeg de volgende artikelen voor meer informatie over wat u met dit eindpunt kunt doen:

* [Een doelserverconfiguratie maken](create-destination-server.md)
* [Een doelserverconfiguratie bijwerken](update-destination-server.md)
* [Een doelserverconfiguratie verwijderen](delete-destination-server.md)
