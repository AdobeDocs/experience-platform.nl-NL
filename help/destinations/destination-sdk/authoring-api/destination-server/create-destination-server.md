---
description: Deze pagina illustreert de API vraag die wordt gebruikt om een bestemmingsserver tot stand te brengen door Adobe Experience Platform Destination SDK.
title: Een doelserverconfiguratie maken
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 6%

---


# Een doelserverconfiguratie maken

Het creëren van een bestemmingsserver is de eerste stap in het creëren van uw eigen bestemming met Destination SDK. De doelserver bevat configuratieopties voor de [server](../../functionality/destination-server/server-specs.md) en [sjablonen](../../functionality/destination-server/templating-specs.md) specs, de [berichtindeling](../../functionality/destination-server/message-format.md)en de [bestandsindeling](../../functionality/destination-server/file-formatting.md) opties (voor op bestanden gebaseerde doelen).

Deze pagina illustreert de API aanvraag en lading die u kunt gebruiken om uw eigen bestemmingsserver tot stand te brengen gebruikend `/authoring/destination-servers` API-eindpunt.

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

## Een doelserverconfiguratie maken {#create}

U kunt een nieuwe configuratie van de bestemmingsserver tot stand brengen door te maken `POST` verzoek aan de `/authoring/destination-servers` eindpunt.

>[!TIP]
>
>**API-eindpunt**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

**API-indeling**

```http
POST /authoring/destination-servers
```

Afhankelijk van het bestemmingstype dat u creeert, moet u een lichtjes verschillend type van bestemmingsserver vormen. Zie in de lusjes hieronder voorbeelden van bestemmingsservers voor elk bestemmingstype dat in Destination SDK wordt gesteund.

De onderstaande voorbeeldladingen bevatten alle parameters die door elk type doelserver worden ondersteund. U hoeft niet alle parameters in uw verzoek op te nemen. De lading is klantgericht op uw behoeften.

Selecteer hieronder elk tabblad om de bijbehorende API-aanvragen weer te geven.

>[!BEGINTABS]

>[!TAB Real-time (streaming)]

**Een realtime (streaming) doelserver maken**

U moet een real-time (het stromen) bestemmingsserver tot stand brengen gelijkend op hieronder getoond wanneer u een (het stromen) op API-Gebaseerde integratie in real time vormt.

+++verzoek

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
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
| `destinationServerType` | Tekenreeks | *Vereist.* Instellen op `URL_BASED` voor realtime (streaming) doelen. |
| `urlBasedDestination.url.templatingStrategy` | Tekenreeks | *Vereist.* <ul><li>Gebruiken `PEBBLE_V1` als Adobe de URL moet transformeren in het dialoogvenster `value` veld hieronder. Gebruik deze optie als u een eindpunt als `https://api.moviestar.com/data/{{customerData.region}}/items`, waarbij `region` onderdelen kunnen per klant verschillen. In dit geval moet u ook configureren `region` als [klantgegevensveld](../../functionality/destination-configuration/customer-data-fields.md) in de [doelconfiguratie](../destination-configuration/create-destination-configuration.md. </li><li> Gebruiken `NONE` als er aan de Adobe zijde geen transformatie nodig is, bijvoorbeeld als u een eindpunt hebt, zoals: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Tekenreeks | *Vereist.* Vul het adres van het API eindpunt in dat Experience Platform zou moeten verbinden met. |
| `httpTemplate.httpMethod` | Tekenreeks | *Vereist.* De methode die Adobe in vraag aan uw server zal gebruiken. Opties zijn `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | Tekenreeks | *Vereist.* Gebruik `PEBBLE_V1`. |
| `httpTemplate.requestBody.value` | Tekenreeks | *Vereist.* Dit koord is karakter-beschermde versie die de gegevens van de klanten van het Platform aan het formaat omzet uw dienst verwacht. <br> <ul><li> Voor informatie over het schrijven van de sjabloon leest u de [Sjabloonsectie gebruiken](../../functionality/destination-server/message-format.md#using-templating). </li><li> Raadpleeg voor meer informatie over het escapen van tekens de [RFC JSON-standaard, sectie 7](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Voor een voorbeeld van een eenvoudige transformatie raadpleegt u de [Profielkenmerken](../../functionality/destination-server/message-format.md#attributes) transformatie. </li></ul> |
| `httpTemplate.contentType` | Tekenreeks | *Vereist.* Het inhoudstype dat uw server accepteert. Deze waarde is zeer waarschijnlijk `application/json`. |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde configuratie van de bestemmingsserver terug.

+++

>[!TAB Amazon S3]

**Een Amazon S3-doelserver maken**

U moet een [!DNL Amazon S3] doelserver, vergelijkbaar met de server die hieronder wordt weergegeven wanneer u een bestand configureert [!DNL Amazon S3] bestemming.

+++verzoek

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
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

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde configuratie van de bestemmingsserver terug.

+++

>[!TAB SFTP]

**Een [!DNL SFTP] doelserver**

U moet een [!DNL SFTP] doelserver, vergelijkbaar met de server die hieronder wordt weergegeven wanneer u een bestand configureert [!DNL SFTP] bestemming.

+++verzoek

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
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

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde configuratie van de bestemmingsserver terug.

+++

>[!TAB Azure Data Lake Storage]

**Een [!DNL Azure Data Lake Storage] doelserver**

U moet een [!DNL Azure Data Lake Storage] doelserver, vergelijkbaar met de server die hieronder wordt weergegeven wanneer u een bestand configureert [!DNL Azure Data Lake Storage] bestemming.

+++verzoek

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
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

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde configuratie van de bestemmingsserver terug.

+++

>[!TAB Azure Blob Storage]

**Een [!DNL Azure Blob Storage] doelserver**

U moet een [!DNL Azure Blob Storage] doelserver, vergelijkbaar met de server die hieronder wordt weergegeven wanneer u een bestand configureert [!DNL Azure Blob Storage] bestemming.

+++verzoek

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
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

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde configuratie van de bestemmingsserver terug.

+++

>[!TAB Data Landing Zone (DLZ)]

**Een [!DNL Data Landing Zone (DLZ)] doelserver**

U moet een [!DNL Data Landing Zone (DLZ)] doelserver, vergelijkbaar met de server die hieronder wordt weergegeven wanneer u een bestand configureert [!DNL Data Landing Zone (DLZ)] bestemming.

+++verzoek

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
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

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde configuratie van de bestemmingsserver terug.

+++

>[!TAB Google Cloud Storage]

**Een [!DNL Google Cloud Storage] doelserver**

U moet een [!DNL Google Cloud Storage] doelserver, vergelijkbaar met de server die hieronder wordt weergegeven wanneer u een bestand configureert [!DNL Google Cloud Storage] bestemming.

+++verzoek

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
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

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde configuratie van de bestemmingsserver terug.

+++

>[!TAB Dynamische schemaserver]

**Een dynamische schemaserver maken**

U moet een dynamische schemaserver tot stand brengen gelijkend op hieronder getoond wanneer u een bestemming vormt die zijn profielschema van uw eigen API eindpunt terugwint. In tegenstelling tot een statisch schema, gebruikt een dynamisch schema geen `profileFields` array. In plaats daarvan gebruiken dynamische schema&#39;s een dynamische schemaserver die met uw eigen API verbindt van waar het de schemaconfiguratie terugwint.

+++verzoek

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Dynamic Schema Server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://YOUR_API_ENDPOINT/"
      }
   },
   "httpTemplate":{
      "httpMethod":"GET"
   },
   "responseFields":[
      {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{\n    \"type\":\"object\",\n    \"title\": \"Contact Schema\",\n    \"properties\": {\n        {% for setDefinition in response.body.items %}\n            \"{{setDefinition.key}}\": {\n                \"title\" : \"{{setDefinition.name.value}}\",\n                \"type\" : \"object\",\n                \"properties\": {\n                    {% for attribute in setDefinition.attributes %}\n                        \"{{attribute.key}}\": {\n                            \"title\" : \"{{attribute.name.value}}\",\n                            \"type\" : \"string\"\n                        }\n                        {% if not loop.last %},{%endif%}\n                    {% endfor %}\n                }\n            }\n            {% if not loop.last %},{%endif%}\n        {% endfor %}\n    }\n}",
         "name":"schema"
      }
   ]
}
```

| Parameter | Type | Beschrijving |
| -------- | ----------- | ----------- |
| `name` | Tekenreeks | *Vereist.* Vertegenwoordigt een vriendschappelijke naam van uw dynamische schemaserver, zichtbaar slechts aan Adobe. |
| `destinationServerType` | Tekenreeks | *Vereist.* Instellen op `URL_BASED` voor dynamische schemaservers. |
| `urlBasedDestination.url.templatingStrategy` | Tekenreeks | *Vereist.* <ul><li>Gebruiken `PEBBLE_V1` als Adobe de URL moet transformeren in het dialoogvenster `value` veld hieronder. Gebruik deze optie als u een eindpunt als: `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Gebruiken `NONE` als er aan de Adobe zijde geen transformatie nodig is, bijvoorbeeld als u een eindpunt hebt, zoals: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Tekenreeks | *Vereist.* Vul het adres van het API eindpunt in dat Experience Platform met zou moeten verbinden en de schemagebieden zou moeten terugwinnen om als doelgebieden in de afbeeldingsstap van het activeringswerkschema te bevolken. |
| `httpTemplate.httpMethod` | Tekenreeks | *Vereist.* De methode die Adobe in vraag aan uw server zal gebruiken. Voor dynamische schemaservers, gebruik `GET`. |
| `responseFields.templatingStrategy` | Tekenreeks | *Vereist.* Gebruik `PEBBLE_V1`. |
| `responseFields.value` | Tekenreeks | *Vereist.* Dit koord is het karakter-ontsnapte transformatiemalplaatje dat de reactie omzet die van partner API in het partnerschema wordt ontvangen dat in het Platform UI zal worden getoond. <br> <ul><li> Voor informatie over het schrijven van de sjabloon leest u de [Sjabloonsectie gebruiken](../../functionality/destination-server/message-format.md#using-templating). </li><li> Raadpleeg voor meer informatie over het escapen van tekens de [RFC JSON-standaard, sectie 7](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Voor een voorbeeld van een eenvoudige transformatie raadpleegt u de [Profielkenmerken](../../functionality/destination-server/message-format.md#attributes) transformatie. </li></ul> |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde configuratie van de bestemmingsserver terug.

+++

>[!ENDTABS]

## API-foutafhandeling {#error-handling}

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Zie [API-statuscodes](../../../../landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](../../../../landing/troubleshooting.md#request-header-errors) in de gids voor het oplossen van problemen met Platforms.

## Volgende stappen {#next-steps}

Nadat u dit document hebt gelezen, weet u nu hoe u een nieuwe doelserver kunt maken via de Destination SDK `/authoring/destination-servers` API-eindpunt.

Raadpleeg de volgende artikelen voor meer informatie over wat u met dit eindpunt kunt doen:

* [De configuratie van een doelserver ophalen](retrieve-destination-server.md)
* [Een doelserverconfiguratie bijwerken](update-destination-server.md)
* [Een doelserverconfiguratie verwijderen](delete-destination-server.md)

Om te begrijpen waar dit eindpunt in het bestemmings auteursproces past, zie de volgende artikelen:

* [Gebruik Destination SDK om een streamingbestemming te configureren](../../guides/configure-destination-instructions.md#create-server-template-configuration)
* [Gebruik Destination SDK om een op een bestand gebaseerde bestemming te configureren](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)