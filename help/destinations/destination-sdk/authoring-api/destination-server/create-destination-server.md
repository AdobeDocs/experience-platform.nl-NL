---
description: Deze pagina illustreert de API vraag die wordt gebruikt om een bestemmingsserver tot stand te brengen door Adobe Experience Platform Destination SDK.
title: Een doelserverconfiguratie maken
exl-id: 5c6b6cf5-a9d9-4c8a-9fdc-f8a95ab2a971
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '2039'
ht-degree: 5%

---

# Een doelserverconfiguratie maken

Het creëren van een bestemmingsserver is de eerste stap in het creëren van uw eigen bestemming met Destination SDK. De doelserver bevat configuratieopties voor de [server](../../functionality/destination-server/server-specs.md) en [sjablonen](../../functionality/destination-server/templating-specs.md) specs [berichtindeling](../../functionality/destination-server/message-format.md)en de [bestandsindeling](../../functionality/destination-server/file-formatting.md) opties (voor op bestanden gebaseerde doelen).

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

Afhankelijk van het bestemmingstype dat u creeert, moet u een lichtjes verschillend type van bestemmingsserver vormen.

### Statische schema-doelservers maken {#static-destination-servers}

Zie in de lusjes hieronder voorbeelden van bestemmingsservers voor bestemmingen die gebruiken [statische schema&#39;s](../../functionality/destination-configuration/schema-configuration.md#attributes-schema).

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
| `urlBasedDestination.url.templatingStrategy` | Tekenreeks | *Vereist.* <ul><li>Gebruiken `PEBBLE_V1` als de Adobe de URL in het dialoogvenster `value` veld hieronder. Gebruik deze optie als u een eindpunt als `https://api.moviestar.com/data/{{customerData.region}}/items`, waarbij de `region` onderdelen kunnen per klant verschillen. In dit geval moet u ook configureren `region` als [klantgegevensveld](../../functionality/destination-configuration/customer-data-fields.md) in de [doelconfiguratie](../destination-configuration/create-destination-configuration.md. </li><li> Gebruiken `NONE` als er aan de zijde van de Adobe geen transformatie nodig is, bijvoorbeeld als u een eindpunt hebt, zoals: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Tekenreeks | *Vereist.* Vul het adres van het API eindpunt in dat Experience Platform zou moeten verbinden met. |
| `httpTemplate.httpMethod` | Tekenreeks | *Vereist.* De methode die de Adobe in vraag aan uw server zal gebruiken. Opties zijn `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
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
| `fileBasedS3Destination.bucket.value` | Tekenreeks | De naam van [!DNL Amazon S3] emmer die door deze bestemming moet worden gebruikt. |
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
   "fileBasedSFTPDestination":{
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
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | Tekenreeks | *Vereist.* Gebruik `PEBBLE_V1`. |
| `fileBasedSFTPDestination.rootDirectory.value` | Tekenreeks | De hoofdmap van de doelopslag. |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | Tekenreeks | *Vereist.* Gebruik `PEBBLE_V1`. |
| `fileBasedSFTPDestination.hostName.value` | Tekenreeks | De hostnaam van de bestemmingsopslag. |
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
| `fileBasedAzureBlobDestination.container.value` | Tekenreeks | De naam van [!DNL Azure Blob Storage] container die door deze bestemming moet worden gebruikt. |
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
| `fileBasedGoogleCloudStorageDestination.bucket.value` | Tekenreeks | De naam van [!DNL Google Cloud Storage] emmer die door deze bestemming moet worden gebruikt. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | Tekenreeks | *Vereist.* Gebruik `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.path.value` | Tekenreeks | Het pad naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen. |
| `fileConfigurations` | N.v.t. | Zie [bestandsindelingconfiguratie](../../functionality/destination-server/file-formatting.md) voor gedetailleerde informatie over hoe te om deze montages te vormen. |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde configuratie van de bestemmingsserver terug.

+++

>[!ENDTABS]

### Dynamische schema-doelservers maken {#dynamic-schema-servers}

Met dynamische schema&#39;s kunt u dynamisch de ondersteunde doelkenmerken ophalen en schema&#39;s genereren op basis van uw eigen API. U moet een bestemmingsserver voor dynamische schema&#39;s vormen alvorens u het schema kunt vormen.

Zie in het lusje onder een voorbeeld van een bestemmingsserver voor bestemmingen die gebruiken [dynamische schema&#39;s](../../functionality/destination-configuration/schema-configuration.md#dynamic-schema-configuration).

De nuttige voorbeeldlading hieronder omvat alle parameters die voor een dynamische schemaserver worden vereist.

>[!BEGINTABS]

>[!TAB Dynamische schemaserver]

**Een dynamische schemaserver maken**

U moet een dynamische schemaserver tot stand brengen gelijkend op hieronder getoond wanneer u een bestemming vormt die zijn profielschema van uw eigen API eindpunt terugwint. In tegenstelling tot een statisch schema gebruikt een dynamisch schema geen `profileFields` array. In plaats daarvan gebruiken dynamische schema&#39;s een dynamische schemaserver die met uw eigen API verbindt van waar het de schemaconfiguratie terugwint.

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
| `urlBasedDestination.url.templatingStrategy` | Tekenreeks | *Vereist.* <ul><li>Gebruiken `PEBBLE_V1` als de Adobe de URL in het dialoogvenster `value` veld hieronder. Gebruik deze optie als u een eindpunt als: `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Gebruiken `NONE` als er aan de zijde van de Adobe geen transformatie nodig is, bijvoorbeeld als u een eindpunt hebt, zoals: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Tekenreeks | *Vereist.* Vul het adres van het API eindpunt in dat Experience Platform met zou moeten verbinden en de schemagebieden zou moeten terugwinnen om als doelgebieden in de afbeeldingsstap van het activeringswerkschema te bevolken. |
| `httpTemplate.httpMethod` | Tekenreeks | *Vereist.* De methode die de Adobe in vraag aan uw server zal gebruiken. Voor dynamische schemaservers, gebruik `GET`. |
| `responseFields.templatingStrategy` | Tekenreeks | *Vereist.* Gebruik `PEBBLE_V1`. |
| `responseFields.value` | Tekenreeks | *Vereist.* Dit koord is het karakter-ontsnapte transformatiemalplaatje dat de reactie omzet die van partner API in het partnerschema wordt ontvangen dat in Platform UI zal worden getoond. <br> <ul><li> Voor informatie over het schrijven van de sjabloon leest u de [Sjabloonsectie gebruiken](../../functionality/destination-server/message-format.md#using-templating). </li><li> Raadpleeg voor meer informatie over het escapen van tekens de [RFC JSON-standaard, sectie 7](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Voor een voorbeeld van een eenvoudige transformatie raadpleegt u de [Profielkenmerken](../../functionality/destination-server/message-format.md#attributes) transformatie. </li></ul> |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde configuratie van de bestemmingsserver terug.

+++


>[!ENDTABS]


### Dynamische vervolgkeuzelijstservers maken {#dynamic-dropdown-servers}

Gebruiken [dynamische dropdowns](../../functionality/destination-configuration/customer-data-fields.md#dynamic-dropdown-selectors) om dropdown de gegevensgebieden van de klantenklant dynamisch terug te winnen en te bevolken, gebaseerd op uw eigen API. U kunt bijvoorbeeld een lijst ophalen met bestaande gebruikersaccounts die u wilt gebruiken voor een doelverbinding.

U moet een bestemmingsserver voor dynamische dropdowns vormen alvorens u het dynamische dropwdown gebied van de klantengegevens kunt vormen.

Zie op het tabblad onder een voorbeeld van een doelserver die wordt gebruikt om dynamisch de waarden op te halen die in een vervolgkeuzelijst, via een API, moeten worden weergegeven.

De nuttige voorbeeldlading hieronder omvat alle parameters die voor een dynamische schemaserver worden vereist.

>[!BEGINTABS]

>[!TAB Dynamische dropdown-server]

**Een dynamische vervolgkeuzeserver maken**

U moet een dynamische dropdown server tot stand brengen gelijkend op hieronder getoond wanneer u een bestemming vormt die de waarden voor een dropdown gebied van de klantengegevens van uw eigen API eindpunt terugwint.

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
   "name":"Server for dynamic dropdown",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.users}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"GET",
      "headers":[
         {
            "header":"Authorization",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"My Bearer Token"
            }
         },
         {
            "header":"x-integration",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.integrationId}}"
            }
         },
         {
            "header":"Accept",
            "value":{
               "templatingStrategy":"NONE",
               "value":"application/json"
            }
         }
      ]
   },
   "responseFields":[
      {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{% set list = [] %} {% for record in response.body %} {% set list = list|merge([{'name' : record.name, 'value' : record.id }]) %} {% endfor %}{{ {'list': list} | toJson | raw }}",
         "name":"list"
      }
   ]
}
```

| Parameter | Type | Beschrijving |
| -------- | ----------- | ----------- |
| `name` | Tekenreeks | *Vereist.* Vertegenwoordigt een vriendschappelijke naam van uw dynamische dropdown server, zichtbaar slechts aan Adobe. |
| `destinationServerType` | Tekenreeks | *Vereist.* Instellen op `URL_BASED` voor dynamische dropdown servers. |
| `urlBasedDestination.url.templatingStrategy` | Tekenreeks | *Vereist.* <ul><li>Gebruiken `PEBBLE_V1` als de Adobe de URL in het dialoogvenster `value` veld hieronder. Gebruik deze optie als u een eindpunt als: `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Gebruiken `NONE` als er aan de zijde van de Adobe geen transformatie nodig is, bijvoorbeeld als u een eindpunt hebt, zoals: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Tekenreeks | *Vereist.* Vul het adres van het API eindpunt in dat Experience Platform met zou moeten verbinden en de dropwdown waarden terugwinnen. |
| `httpTemplate.httpMethod` | Tekenreeks | *Vereist.* De methode die de Adobe in vraag aan uw server zal gebruiken. Voor dynamische dropdown servers, gebruik `GET`. |
| `httpTemplate.headers` | Object | *Optiona.l* Neem alle vereiste headers op om verbinding te maken met de dynamische vervolgkeuzeserver. |
| `responseFields.templatingStrategy` | Tekenreeks | *Vereist.* Gebruik `PEBBLE_V1`. |
| `responseFields.value` | Tekenreeks | *Vereist.* Deze tekenreeks is de transformatiesjabloon met escape-teken waarmee de reactie die u van uw API hebt ontvangen, wordt omgezet in de waarden die worden weergegeven in de interface van het platform. <br> <ul><li> Voor informatie over het schrijven van de sjabloon leest u de [Sjabloonsectie gebruiken](../../functionality/destination-server/message-format.md#using-templating). </li><li> Raadpleeg voor meer informatie over het escapen van tekens de [RFC JSON-standaard, sectie 7](https://tools.ietf.org/html/rfc8259#section-7). |

{style="table-layout:auto"}

+++

+++Response

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde configuratie van de bestemmingsserver terug.

+++

>[!ENDTABS]

## API-foutafhandeling {#error-handling}

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Zie [API-statuscodes](../../../../landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](../../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van het Platform.

## Volgende stappen {#next-steps}

Nadat u dit document hebt gelezen, weet u nu hoe u een nieuwe doelserver kunt maken via de Destination SDK `/authoring/destination-servers` API-eindpunt.

Raadpleeg de volgende artikelen voor meer informatie over wat u met dit eindpunt kunt doen:

* [De configuratie van een doelserver ophalen](retrieve-destination-server.md)
* [Een doelserverconfiguratie bijwerken](update-destination-server.md)
* [Een doelserverconfiguratie verwijderen](delete-destination-server.md)

Om te begrijpen waar dit eindpunt in het bestemmings auteursproces past, zie de volgende artikelen:

* [Gebruik Destination SDK om een streamingbestemming te configureren](../../guides/configure-destination-instructions.md#create-server-template-configuration)
* [Gebruik Destination SDK om een op een bestand gebaseerde bestemming te configureren](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)
