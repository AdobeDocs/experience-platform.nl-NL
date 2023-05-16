---
description: Deze pagina illustreert de API vraag die wordt gebruikt om een bestaande configuratie van de bestemmingsserver door Adobe Experience Platform Destination SDK bij te werken.
title: Een doelserverconfiguratie bijwerken
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 8%

---


# Een doelserverconfiguratie bijwerken

Deze pagina illustreert de API aanvraag en lading die u kunt gebruiken om een bestaande configuratie van de bestemmingsserver bij te werken, gebruikend `/authoring/destination-servers` API-eindpunt.

>[!TIP]
>
>Om het even welke updateverrichting op geproduceerde/openbare bestemmingen is zichtbaar slechts nadat u gebruikt [publicatie-API](../../publishing-api/create-publishing-request.md) en dient de update in voor Adobe review.

Voor een gedetailleerde beschrijving van de mogelijkheden die u door dit eindpunt kunt vormen, lees de volgende artikelen:

* [Server specs voor bestemmingen die met Destination SDK worden gecreeerd](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Sjabloonspecificaties voor doelen die met Destination SDK zijn gemaakt](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [Berichtindeling](../../../destination-sdk/functionality/destination-server/message-format.md)
* [Configuratie bestandsindeling](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Alle parameternamen en -waarden die door Destination SDK worden ondersteund, zijn **hoofdlettergevoelig**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Aan de slag met API-bewerkingen voor doelserver {#get-started}

Controleer voordat je doorgaat de [gids Aan de slag](../../getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings creatie en vereiste kopballen te verkrijgen.

## Een doelserverconfiguratie bijwerken {#update}

U kunt een [bestaand](create-destination-server.md) doelserverconfiguratie door een `PUT` verzoek aan de `/authoring/destination-servers` eindpunt met de bijgewerkte nuttige lading.

>[!TIP]
>
>**API-eindpunt**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

Om een bestaande configuratie van de bestemmingsserver en zijn overeenkomstige te verkrijgen `{INSTANCE_ID}`, raadpleegt u het artikel over [ophalen, configuratie van doelserver](retrieve-destination-server.md).

**API-indeling**

```http
PUT /authoring/destination-servers/{INSTANCE_ID}
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{INSTANCE_ID}` | De id van de configuratie van de doelserver die u wilt bijwerken. Om een bestaande configuratie van de bestemmingsserver en zijn overeenkomstige te verkrijgen `{INSTANCE_ID}`, zie [De configuratie van een doelserver ophalen](retrieve-destination-server.md). |

De volgende verzoeken werken een bestaande configuratie van de bestemmingsserver bij, die door de parameters wordt gevormd die in de lading worden verstrekt.

Selecteer hieronder elk tabblad om de bijbehorende lading weer te geven.

>[!BEGINTABS]

>[!TAB Real-time (streaming)]

+++verzoek

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers\{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
      "httpMethod":"PUT",
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
| `destinationServerType` | Tekenreeks | *Vereist.* Instellen op `URL_BASED` voor realtime (streaming) doelen. |
| `urlBasedDestination.url.templatingStrategy` | Tekenreeks | *Vereist.* <ul><li>Gebruiken `PEBBLE_V1` als Adobe de URL moet transformeren in het dialoogvenster `value` veld hieronder. Gebruik deze optie als u een eindpunt als: `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Gebruiken `NONE` als er aan de Adobe zijde geen transformatie nodig is, bijvoorbeeld als u een eindpunt hebt, zoals: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Tekenreeks | *Vereist.* Vul het adres van het API eindpunt in dat Experience Platform zou moeten verbinden met. |
| `httpTemplate.httpMethod` | Tekenreeks | *Vereist.* De methode die Adobe in vraag aan uw server zal gebruiken. Opties zijn `GET`, `PUT`, `PUT`, `DELETE`, `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | Tekenreeks | *Vereist.* Gebruik `PEBBLE_V1`. |
| `httpTemplate.requestBody.value` | Tekenreeks | *Vereist.* Dit koord is karakter-beschermde versie die de gegevens van de klanten van het Platform aan het formaat omzet uw dienst verwacht. <br> <ul><li> Voor informatie over het schrijven van de sjabloon leest u de [Sjabloonsectie gebruiken](../../functionality/destination-server/message-format.md#using-templating). </li><li> Raadpleeg voor meer informatie over het escapen van tekens de [RFC JSON-standaard, sectie 7](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Voor een voorbeeld van een eenvoudige transformatie raadpleegt u de [Profielkenmerken](../../functionality/destination-server/message-format.md#attributes) transformatie. </li></ul> |
| `httpTemplate.contentType` | Tekenreeks | *Vereist.* Het inhoudstype dat uw server accepteert. Deze waarde is zeer waarschijnlijk `application/json`. |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met de details van uw bijgewerkte configuratie van de bestemmingsserver terug.

+++

>[!TAB Amazon S3]

+++verzoek

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers\{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            }
        }
    }
}
```

| Parameter | Type | Beschrijving |
|---|---|---|
| `name` | Tekenreeks | De naam van de doelverbinding. |
| `destinationServerType` | Tekenreeks | Stel deze waarde in op basis van het doelplatform. Voor [!DNL Amazon S3], stelt u deze in op `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | Tekenreeks | *Vereist.* Gebruik `PEBBLE_V1`. |
| `fileBasedS3Destination.bucket.value` | Tekenreeks | De naam van de [!DNL Amazon S3] emmer die door deze bestemming moet worden gebruikt. |
| `fileBasedS3Destination.path.templatingStrategy` | Tekenreeks | *Vereist.* Gebruik `PEBBLE_V1`. |
| `fileBasedS3Destination.path.value` | Tekenreeks | Het pad naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen. |
| `fileConfigurations` | N.v.t. | Zie [bestandsindelingconfiguratie](../../functionality/destination-server/file-formatting.md) voor gedetailleerde informatie over hoe te om deze montages te vormen. |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met de details van uw bijgewerkte configuratie van de bestemmingsserver terug.

+++

>[!TAB SFTP]

+++verzoek

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            }
        }
    }
}
```

| Parameter | Type | Beschrijving |
|---|---|---|
| `name` | Tekenreeks | De naam van de doelverbinding. |
| `destinationServerType` | Tekenreeks | Stel deze waarde in op basis van het doelplatform. Voor [!DNL SFTP] doelen, stel deze in op `FILE_BASED_SFTP`. |
| `fileBasedSftpDestination.rootDirectory.templatingStrategy` | Tekenreeks | *Vereist.* Gebruik `PEBBLE_V1`. |
| `fileBasedSftpDestination.rootDirectory.value` | Tekenreeks | De hoofdmap van de doelopslag. |
| `fileBasedSftpDestination.hostName.templatingStrategy` | Tekenreeks | *Vereist.* Gebruik `PEBBLE_V1`. |
| `fileBasedSftpDestination.hostName.value` | Tekenreeks | De hostnaam van de bestemmingsopslag. |
| `port` | Geheel | De SFTP-serverpoort. |
| `encryptionMode` | Tekenreeks | Geeft aan of bestandsversleuteling moet worden gebruikt. Ondersteunde waarden: <ul><li>PGP</li><li>Geen</li></ul> |
| `fileConfigurations` | N.v.t. | Zie [bestandsindelingconfiguratie](../../functionality/destination-server/file-formatting.md) voor gedetailleerde informatie over hoe te om deze montages te vormen. |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met de details van uw bijgewerkte configuratie van de bestemmingsserver terug.

+++

>[!TAB Azure Data Lake Storage]

+++verzoek

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            }
        }
    }
}
```

| Parameter | Type | Beschrijving |
|---|---|---|
| `name` | Tekenreeks | De naam van de doelverbinding. |
| `destinationServerType` | Tekenreeks | Stel deze waarde in op basis van het doelplatform. Voor [!DNL Azure Data Lake Storage] doelen, stel deze in op `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Tekenreeks | *Vereist.* Gebruik `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | Tekenreeks | Het pad naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen. |
| `fileConfigurations` | N.v.t. | Zie [bestandsindelingconfiguratie](../../functionality/destination-server/file-formatting.md) voor gedetailleerde informatie over hoe te om deze montages te vormen. |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met de details van uw bijgewerkte configuratie van de bestemmingsserver terug.

+++

>[!TAB Azure Blob Storage]

+++verzoek

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_D} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            }
        }
    }
}
```

| Parameter | Type | Beschrijving |
|---|---|---|
| `name` | Tekenreeks | De naam van de doelverbinding. |
| `destinationServerType` | Tekenreeks | Stel deze waarde in op basis van het doelplatform. Voor [!DNL Azure Blob Storage] doelen, stel deze in op `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | Tekenreeks | *Vereist.* Gebruik `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.path.value` | Tekenreeks | Het pad naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | Tekenreeks | *Vereist.* Gebruik `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.container.value` | Tekenreeks | De naam van de [!DNL Azure Blob Storage] container die door deze bestemming moet worden gebruikt. |
| `fileConfigurations` | N.v.t. | Zie [bestandsindelingconfiguratie](../../functionality/destination-server/file-formatting.md) voor gedetailleerde informatie over hoe te om deze montages te vormen. |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met de details van uw bijgewerkte configuratie van de bestemmingsserver terug.

+++

>[!TAB Data Landing Zone (DLZ)]

+++verzoek

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            }
        }
    }
}
```

| Parameter | Type | Beschrijving |
|---|---|---|
| `name` | Tekenreeks | De naam van de doelverbinding. |
| `destinationServerType` | Tekenreeks | Stel deze waarde in op basis van het doelplatform. Voor [!DNL Data Landing Zone] doelen, stel deze in op `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | Tekenreeks | *Vereist.*  Gebruik `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | Tekenreeks | Het pad naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen. |
| `fileConfigurations` | N.v.t. | Zie [bestandsindelingconfiguratie](../../functionality/destination-server/file-formatting.md) voor gedetailleerde informatie over hoe te om deze montages te vormen. |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met de details van uw bijgewerkte configuratie van de bestemmingsserver terug.

+++

>[!TAB Google Cloud Storage]

+++verzoek

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Google Cloud Storage Server",
   "destinationServerType":"FILE_BASED_GOOGLE_CLOUD",
   "fileBasedGoogleCloudStorageDestination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
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
            }
        }
    }
}
```

| Parameter | Type | Beschrijving |
|---|---|---|
| `name` | Tekenreeks | De naam van de doelverbinding. |
| `destinationServerType` | Tekenreeks | Stel deze waarde in op basis van het doelplatform. Voor [!DNL Google Cloud Storage] doelen, stel deze in op `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | Tekenreeks | *Vereist.*  Gebruik `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | Tekenreeks | De naam van de [!DNL Google Cloud Storage] emmer die door deze bestemming moet worden gebruikt. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | Tekenreeks | *Vereist.* Gebruik `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.path.value` | Tekenreeks | Het pad naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen. |
| `fileConfigurations` | N.v.t. | Zie [bestandsindelingconfiguratie](../../functionality/destination-server/file-formatting.md) voor gedetailleerde informatie over hoe te om deze montages te vormen. |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met de details van uw bijgewerkte configuratie van de bestemmingsserver terug.

+++

>[!ENDTABS]

## API-foutafhandeling {#error-handling}

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Zie [API-statuscodes](../../../../landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](../../../../landing/troubleshooting.md#request-header-errors) in de gids voor het oplossen van problemen met Platforms.

## Volgende stappen {#next-steps}

Nadat u dit document hebt gelezen, weet u nu hoe u een configuratie van de doelserver kunt bijwerken via de Destination SDK `/authoring/destination-servers` API-eindpunt.

Raadpleeg de volgende artikelen voor meer informatie over wat u met dit eindpunt kunt doen:

* [Een doelserverconfiguratie maken](create-destination-server.md)
* [De configuratie van een doelserver ophalen](retrieve-destination-server.md)
* [Een doelserverconfiguratie bijwerken](update-destination-server.md)