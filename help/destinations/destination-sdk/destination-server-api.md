---
description: Deze pagina bevat een overzicht en beschrijving van alle API-bewerkingen die u kunt uitvoeren met het API-eindpunt `/authoring/destination-servers'. De server en malplaatjespecs voor uw bestemming kunnen in Adobe Experience Platform Destination SDK via het gemeenschappelijke eindpunt `/authoring/bestemmings-servers worden gevormd.
title: API-bewerkingen voor eindpunt doelserver
exl-id: a144b0fb-d34f-42d1-912b-8576296e59d2
source-git-commit: ce63d602e768d04ba7fdc6aded34869682ee7206
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 1%

---

# API-bewerkingen voor eindpunt doelserver

>[!IMPORTANT]
>
>**API-eindpunt**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

Deze pagina bevat een overzicht en beschrijving van alle API-bewerkingen die u kunt uitvoeren met de `/authoring/destination-servers` API-eindpunt. De server en malplaatjespecs voor uw bestemming kunnen in Adobe Experience Platform Destination SDK via het gemeenschappelijke eindpunt worden gevormd `/authoring/destination-servers`. Voor een beschrijving van de functionaliteit die door dit eindpunt wordt verstrekt, lees [server- en sjabloonspecificaties](./server-and-template-configuration.md).

## Aan de slag met API-bewerkingen voor doelserver {#get-started}

Controleer voordat je doorgaat de [gids Aan de slag](./getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings creatie en vereiste kopballen te verkrijgen.

## Configuratie maken voor een streaming doelserver {#create}

U kunt een nieuwe configuratie van de bestemmingsserver voor een het stromen bestemming tot stand brengen door een verzoek van de POST aan `/authoring/destination-servers` eindpunt.

**API-indeling**

```http
POST /authoring/destination-servers
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe configuratie van de bestemmingsserver, die door de parameters wordt gevormd die in de lading worden verstrekt. De hieronder vermelde lading omvat alle parameters die door `/authoring/destination-servers` eindpunt. Merk op dat u niet alle parameters op de vraag moet toevoegen en dat het malplaatje, volgens uw API vereisten aanpasbaar is.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
| -------- | ----------- | ----------- |
| `name` | Tekenreeks | *Vereist.* Vertegenwoordigt een vriendschappelijke naam van uw server, zichtbaar slechts aan Adobe. Deze naam is niet zichtbaar aan partners of klanten. Voorbeeld `Moviestar destination server`. |
| `destinationServerType` | Tekenreeks | *Vereist.* Instellen op `URL_BASED` voor streamingdoelen. |
| `urlBasedDestination.url.templatingStrategy` | Tekenreeks | *Vereist.* <ul><li>Gebruiken `PEBBLE_V1` als Adobe de URL moet transformeren in het dialoogvenster `value` veld hieronder. Gebruik deze optie als u een eindpunt als: `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Gebruiken `NONE` als er aan de Adobe zijde geen transformatie nodig is, bijvoorbeeld als u een eindpunt hebt, zoals: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Tekenreeks | *Vereist.* Vul het adres van het API eindpunt in dat Experience Platform zou moeten verbinden met. |
| `httpTemplate.httpMethod` | Tekenreeks | *Vereist.* De methode die Adobe in vraag aan uw server zal gebruiken. Opties zijn `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | Tekenreeks | *Vereist.* Gebruik `PEBBLE_V1`. |
| `httpTemplate.requestBody.value` | Tekenreeks | *Vereist.* Dit koord is karakter-beschermde versie die de gegevens van de klanten van het Platform aan het formaat omzet uw dienst verwacht. <br> <ul><li> Voor informatie over het schrijven van de sjabloon leest u de [Sjabloonsectie gebruiken](./message-format.md#using-templating). </li><li> Raadpleeg voor meer informatie over het escapen van tekens de [RFC JSON-standaard, sectie 7](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Voor een voorbeeld van een eenvoudige transformatie raadpleegt u de [Profielkenmerken](./message-format.md#attributes) transformatie. </li></ul> |
| `httpTemplate.contentType` | Tekenreeks | *Vereist.* Het inhoudstype dat uw server accepteert. Deze waarde is zeer waarschijnlijk `application/json`. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde configuratie van de bestemmingsserver terug.

## Configuratie maken voor een op een bestand gebaseerde doelserver {#create-file-based}

>[!IMPORTANT]
>
>Bestandsgebaseerde doelondersteuning in Adobe Experience Platform Destination SDK staat momenteel in bètaversie. De documentatie en functionaliteit kunnen worden gewijzigd.

### Voorbeeldconfiguratie SFTP-doelserver {#sftp-server-sample}

+++Een voorbeeld weergeven voor een [!DNL SFTP] doelserverconfiguratie

U kunt een nieuwe configuratie van de bestemmingsserver van SFTP tot stand brengen door een verzoek van de POST aan `/authoring/destination-servers` eindpunt.

**API-indeling**

```http
POST /authoring/destination-servers
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe configuratie van de bestemmingsserver, die door de parameters wordt gevormd die in de lading worden verstrekt. De hieronder vermelde lading omvat alle parameters die door `/authoring/destination-servers` eindpunt. Merk op dat u niet alle parameters op de vraag moet toevoegen en dat het malplaatje, volgens uw API vereisten aanpasbaar is.


```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSftpDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      }, 
      "port": 22,
      "encryptionMode" : "PGP"
   },
    "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "lineSep": {
                "templatingStrategy": "NONE",
                "value": "\n"
            }
        }
    }
}
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde configuratie van de bestemmingsserver terug.
+++

### [!DNL Amazon S3] voorbeeldconfiguratie doelserver {#s3-server-sample}

+++Een voorbeeld weergeven voor een [!DNL Amazon S3] doelserverconfiguratie

U kunt een nieuwe Amazon S3 configuratie van de bestemmingsserver tot stand brengen door een verzoek van de POST aan `/authoring/destination-servers` eindpunt.

**API-indeling**

```http
POST /authoring/destination-servers
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe configuratie van de bestemmingsserver, die door de parameters wordt gevormd die in de lading worden verstrekt. De hieronder vermelde lading omvat alle parameters die door `/authoring/destination-servers` eindpunt. Merk op dat u niet alle parameters op de vraag moet toevoegen en dat het malplaatje, volgens uw API vereisten aanpasbaar is.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "name": "S3 destination",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucket": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.bucket}}"
        },
        "path": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.path}}"
        }
    },
    "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "lineSep": {
                "templatingStrategy": "NONE",
                "value": "\n"
            }
        }
    }
}
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde configuratie van de bestemmingsserver terug.
+++

### [!DNL Azure Blob] voorbeeldconfiguratie doelserver {#blob-server-sample}

+++Een voorbeeld weergeven voor een [!DNL Azure Blob] doelserverconfiguratie

U kunt een nieuwe configuratie van de de bestemmingsserver van Azure Blob tot stand brengen door een verzoek van de POST aan `/authoring/destination-servers` eindpunt.

**API-indeling**

```http
POST /authoring/destination-servers
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe configuratie van de bestemmingsserver, die door de parameters wordt gevormd die in de lading worden verstrekt. De hieronder vermelde lading omvat alle parameters die door `/authoring/destination-servers` eindpunt. Merk op dat u niet alle parameters op de vraag moet toevoegen en dat het malplaatje, volgens uw API vereisten aanpasbaar is.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Blob destination server",
   "destinationServerType":"FILE_BASED_AZURE_BLOB",
   "fileBasedAzureBlobDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "container":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.container}}"
      }
   },
  "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "lineSep": {
                "templatingStrategy": "NONE",
                "value": "\n"
            }
        }
    }
}
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde configuratie van de bestemmingsserver terug.
+++

### [!DNL Azure Data Lake Storage] voorbeeldconfiguratie doelserver {#adls-server-sample}

+++Een voorbeeld weergeven voor een [!DNL Azure Data Lake Storage (ADLS)] doelserverconfiguratie

U kunt een nieuwe configuratie van de bestemmingsserver tot stand brengen ADLS door een verzoek van de POST aan `/authoring/destination-servers` eindpunt.

**API-indeling**

```http
POST /authoring/destination-servers
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe configuratie van de bestemmingsserver, die door de parameters wordt gevormd die in de lading worden verstrekt. De hieronder vermelde lading omvat alle parameters die door `/authoring/destination-servers` eindpunt. Merk op dat u niet alle parameters op de vraag moet toevoegen en dat het malplaatje, volgens uw API vereisten aanpasbaar is.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"ADLS destination server",
   "destinationServerType":"FILE_BASED_ADLS_GEN2",
   "fileBasedAdlsGen2Destination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   },
  "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "lineSep": {
                "templatingStrategy": "NONE",
                "value": "\n"
            }
        }
    }
}
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde configuratie van de bestemmingsserver terug.
+++

### [!DNL Data Landing Zone] (DLZ) de voorbeeldconfiguratie van de bestemmingsserver {#dlz-server-sample}

+++Een voorbeeld weergeven voor een [!DNL Data Landing Zone (DLZ)] doelserverconfiguratie

[!DNL Data Landing Zone] ([!DNL DLZ]) is [!DNL Azure Blob] -opslaginterface die door Adobe Experience Platform is ingericht, zodat u toegang hebt tot een veilige, op de cloud gebaseerde opslagvoorziening voor bestanden om bestanden in Platform te brengen.

U kunt een nieuwe configuratie van de bestemmingsserver tot stand brengen DLZ door een verzoek van de POST aan `/authoring/destination-servers` eindpunt.

**API-indeling**

```http
POST /authoring/destination-servers
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe configuratie van de bestemmingsserver, die door de parameters wordt gevormd die in de lading worden verstrekt. De hieronder vermelde lading omvat alle parameters die door `/authoring/destination-servers` eindpunt. Merk op dat u niet alle parameters op de vraag moet toevoegen en dat het malplaatje, volgens uw API vereisten aanpasbaar is.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"DLZ destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "Your use case"
   },
   "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "lineSep": {
                "templatingStrategy": "NONE",
                "value": "\n"
            }
        }
    }
}
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde configuratie van de bestemmingsserver terug.
+++

## Bestemmingsserverconfiguraties weergeven {#retrieve-list}

U kunt een lijst van alle configuraties van de bestemmingsserver voor uw IMS Organisatie terugwinnen door een verzoek van de GET tot de `/authoring/destination-servers` eindpunt.

**API-indeling**

```http
GET /authoring/destination-servers
```

**Verzoek**

Het volgende verzoek zal de lijst van de configuraties van de bestemmingsserver terugwinnen die u toegang tot hebt, die op Organisatie IMS en zandbakconfiguratie wordt gebaseerd.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

De volgende reactie retourneert HTTP-status 200 met een lijst van configuraties van doelservers waartoe u toegang hebt, op basis van de IMS-organisatie-id en de sandboxnaam die u hebt gebruikt. Eén `instanceId` komt overeen met de sjabloon voor één doelserver. De reactie is afgebroken voor de beknoptheid.

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

## Een bestaande doelserverconfiguratie bijwerken {#update}

U kunt een bestaande configuratie van de bestemmingsserver bijwerken door een verzoek van de PUT aan `/authoring/destination-servers` eindpunt en het verstrekken van instanceID van de configuratie van de bestemmingsserver u wilt bijwerken. In het lichaam van de vraag, verstrek de bijgewerkte configuratie van de bestemmingsserver.

**API-indeling**

```http
PUT /authoring/destination-servers/{INSTANCE_ID}
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{INSTANCE_ID}` | De id van de configuratie van de doelserver die u wilt bijwerken. |

**Verzoek**

Het volgende verzoek werkt een bestaande configuratie van de bestemmingsserver bij, die door de parameters wordt gevormd die in de lading worden verstrekt.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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

## Een specifieke configuratie van de doelserver ophalen {#get}

U kunt gedetailleerde informatie over een specifieke configuratie van de bestemmingsserver terugwinnen door een verzoek van de GET aan `/authoring/destination-servers` eindpunt en het verstrekken van instanceID van de configuratie van de bestemmingsserver u wilt bijwerken.

**API-indeling**

```http
GET /authoring/destination-servers/{INSTANCE_ID}
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{INSTANCE_ID}` | De id van de configuratie van de doelserver die u wilt ophalen. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met gedetailleerde informatie over de gespecificeerde configuratie van de bestemmingsserver terug.

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

## Een specifieke doelserverconfiguratie verwijderen {#delete}

U kunt de opgegeven configuratie van de doelserver verwijderen door een DELETE-aanvraag in te dienen bij de `/authoring/destination-servers` eindpunt en het verstrekken van identiteitskaart van de configuratie van de bestemmingsserver u wenst om in de verzoekweg te schrappen.

**API-indeling**

```http
DELETE /authoring/destination-servers/{INSTANCE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{INSTANCE_ID}` | De `id` van de configuratie van de bestemmingsserver u wilt schrappen. |

**Verzoek**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 samen met een lege HTTP-respons.

## API-foutafhandeling

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Zie [API-statuscodes](../../landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](../../landing/troubleshooting.md#request-header-errors) in de gids voor het oplossen van problemen met Platforms.

## Volgende stappen

Nadat u dit document hebt gelezen, weet u nu hoe u de doelserver en sjablonen kunt configureren met de `/authoring/destination-servers` API-eindpunt. Lezen [hoe te om Destination SDK te gebruiken om uw bestemming te vormen](./configure-destination-instructions.md) om te begrijpen waar deze stap in het proces past om uw bestemming te vormen.
