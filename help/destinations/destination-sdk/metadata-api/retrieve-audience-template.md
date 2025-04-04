---
description: Deze pagina illustreert de API vraag die wordt gebruikt om een publiekssjabloon door Adobe Experience Platform Destination SDK terug te winnen.
title: Een publiekssjabloon ophalen
exl-id: 44f2d571-49c5-4112-b3ee-bc839f2b0874
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# Een publiekssjabloon ophalen

>[!IMPORTANT]
>
>**API eindpunt**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Deze pagina illustreert de API-aanvraag en lading die u kunt gebruiken om een sjabloon voor publieksmetagegevens op te halen met het API-eindpunt `/authoring/audience-templates` .

Voor een gedetailleerde beschrijving van de mogelijkheden die u door dit eindpunt kunt vormen, zie [ beheer van publieksmeta-gegevens ](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Alle parameternamen en waarden die door Destination SDK worden gesteund zijn **gevoelig geval**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Aan de slag met API-bewerkingen voor publiekssjablonen {#get-started}

Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](../getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings authoring en vereiste kopballen te verkrijgen.

## Een publiekssjabloon ophalen {#retrieve}

U kunt een bestaande publiekssjabloon ophalen door een `GET` -aanvraag in te dienen bij het `/authoring/audience-templates` -eindpunt.

**API formaat**

Gebruik de volgende API-indeling om alle publiekssjablonen voor uw account op te halen.

```http
GET /authoring/audience-templates
```

Gebruik de volgende API-indeling om een specifieke publiekssjabloon op te halen, gedefinieerd door de parameter `{INSTANCE_ID}` .

```http
GET /authoring/audience-templates/{INSTANCE_ID}
```

Met de volgende twee verzoeken worden alle publiekssjablonen voor uw IMS-organisatie of een specifieke publiekssjabloon opgehaald, afhankelijk van het feit of u de parameter `INSTANCE_ID` in de aanvraag doorgeeft.

Selecteer hieronder elk tabblad om de bijbehorende lading weer te geven.

>[!BEGINTABS]

>[!TAB  wint alle publieksmalplaatjes ] terug

Met de volgende aanvraag wordt de lijst met publiekssjablonen opgehaald die u kunt gebruiken op basis van de configuratie van [!DNL IMS Org ID] en de sandbox.

+++verzoek

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Response

Een geslaagde reactie geeft HTTP-status 200 weer met een lijst van publiekssjablonen waartoe u toegang hebt, op basis van de naam van de [!DNL IMS Org ID] en de sandbox die u hebt gebruikt. Eén `instanceId` komt overeen met één publiekssjabloon.

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}",
                     "source_type":"FIRST_PARTY",
                     "ad_account_id":"{{customerData.accountId}}",
                     "retention_in_days":180
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"PUT",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "id":"{{segment.alias}}",
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}"
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://adsapi.moviestar.com/v1/segments/{{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "name":"Moviestar destination audience template - Example 1"
   }
}
```

+++

>[!TAB  wint een specifiek publiekssjabloon ] terug

Met de volgende aanvraag wordt de lijst met publiekssjablonen opgehaald die u kunt gebruiken op basis van de configuratie van [!DNL IMS Org ID] en de sandbox.

+++verzoek

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{INSTANCE_ID}` | De id van de publiekssjabloon die u wilt ophalen. |

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met de details van het publiekssjabloon terug die aan `{INSTANCE_ID}` beantwoorden op de vraag wordt verstrekt.

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}",
                     "source_type":"FIRST_PARTY",
                     "ad_account_id":"{{customerData.accountId}}",
                     "retention_in_days":180
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"PUT",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "id":"{{segment.alias}}",
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}"
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://adsapi.moviestar.com/v1/segments/{{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "name":"Moviestar destination audience template - Example 1"
   }
}
```

+++

>[!ENDTABS]

## API-foutafhandeling {#error-handling}

Destination SDK API-eindpunten volgen de algemene beginselen van Experience Platform API-foutberichten. Verwijs naar [ API statuscodes ](../../../landing/troubleshooting.md#api-status-codes) en [ de fouten van de verzoekkopbal ](../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van Experience Platform.

## Volgende stappen {#next-steps}

Nadat u dit document hebt gelezen, weet u nu hoe u details over de configuratie van de doelserver kunt ophalen met behulp van het API-eindpunt van `/authoring/destination-servers` . Lees [ hoe te om Destination SDK te gebruiken om uw bestemming ](../guides/configure-destination-instructions.md) te vormen om te begrijpen waar deze stap in het proces past om uw bestemming te vormen.
