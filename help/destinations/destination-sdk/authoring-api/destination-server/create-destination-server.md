---
description: Deze pagina illustreert de API-aanroep die wordt gebruikt om een doelserver te maken via Adobe Experience Platform Destination SDK.
title: Een doelserverconfiguratie maken
exl-id: 5c6b6cf5-a9d9-4c8a-9fdc-f8a95ab2a971
source-git-commit: e1dd6ae9bf28014e8e84de85bdf67707744ea0ad
workflow-type: tm+mt
source-wordcount: '2040'
ht-degree: 1%

---

# Een doelserverconfiguratie maken

Het maken van een doelserver is de eerste stap bij het maken van uw eigen bestemming met Destination SDK. De bestemmingsserver omvat configuratieopties voor de [ server ](../../functionality/destination-server/server-specs.md) en [ het templating ](../../functionality/destination-server/templating-specs.md) specs, het [ berichtformaat ](../../functionality/destination-server/message-format.md), en [ dossier het formatteren ](../../functionality/destination-server/file-formatting.md) opties (voor op dossier-gebaseerde bestemmingen).

Deze pagina illustreert de API-aanvraag en lading die u kunt gebruiken om uw eigen doelserver te maken met behulp van het API-eindpunt `/authoring/destination-servers` .

Voor een gedetailleerde beschrijving van de mogelijkheden die u door dit eindpunt kunt vormen, lees de volgende artikelen:

* [Serverspecificaties voor doelen die met Destination SDK zijn gemaakt](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Sjabloonspecificaties voor bestemmingen die zijn gemaakt met Destination SDK](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [Berichtindeling](../../../destination-sdk/functionality/destination-server/message-format.md)
* [Configuratie bestandsindeling](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Alle parameternamen en waarden die door Destination SDK worden gesteund zijn **gevoelig geval**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Aan de slag met API-bewerkingen voor doelserver {#get-started}

Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](../../getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings authoring en vereiste kopballen te verkrijgen.

## Een doelserverconfiguratie maken {#create}

U kunt een nieuwe configuratie voor de doelserver maken door een `POST` -aanvraag in te dienen bij het `/authoring/destination-servers` -eindpunt.

>[!TIP]
>
>**API eindpunt**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

**API formaat**

```http
POST /authoring/destination-servers
```

Afhankelijk van het bestemmingstype dat u creeert, moet u een lichtjes verschillend type van bestemmingsserver vormen.

### Statische schema-doelservers maken {#static-destination-servers}

Zie in de lusjes onder voorbeelden van bestemmingsservers voor bestemmingen die [ statische schema&#39;s ](../../functionality/destination-configuration/schema-configuration.md#attributes-schema) gebruiken.

De onderstaande voorbeeldladingen bevatten alle parameters die door elk type doelserver worden ondersteund. U hoeft niet alle parameters in uw verzoek op te nemen. De lading is klantgericht op uw behoeften.

Selecteer hieronder elk tabblad om de bijbehorende API-aanvragen weer te geven.

>[!BEGINTABS]

>[!TAB  Real-time (het stromen) ]

**creeer een (het stromen) bestemmingsserver in real time**

U moet een real-time (het stromen) bestemmingsserver tot stand brengen gelijkend op hieronder getoond wanneer u een (het stromen) op API-Gebaseerde integratie in real time vormt.

+++Verzoek

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
| `name` | String | *Vereist.* Vertegenwoordigt een vriendelijke naam van uw server, die alleen zichtbaar is voor Adobe. Deze naam is niet zichtbaar aan partners of klanten. Voorbeeld `Moviestar destination server` . |
| `destinationServerType` | String | *Vereist.* Ingesteld op `URL_BASED` voor realtime (streaming) doelen. |
| `urlBasedDestination.url.templatingStrategy` | String | *Vereist.* <ul><li>Gebruik `PEBBLE_V1` als Adobe de URL in het onderstaande veld `value` moet transformeren. Gebruik deze optie als u een eindpunt als `https://api.moviestar.com/data/{{customerData.region}}/items` hebt, waar het `region` -onderdeel kan verschillen tussen klanten. In dit geval moet u `region` ook vormen als gebied van a [ klantengegevens ](../../functionality/destination-configuration/customer-data-fields.md) in de [ bestemmingsconfiguratie ] (../destination-configuration/create-destination-configuration.md. </li><li> Gebruik `NONE` als er aan de Adobe-zijde geen transformatie nodig is, bijvoorbeeld als u een eindpunt hebt, zoals: `https://api.moviestar.com/data/items` .</li></ul> |
| `urlBasedDestination.url.value` | String | *Vereist.* Vul het adres in van het API-eindpunt waarmee Experience Platform verbinding moet maken. |
| `httpTemplate.httpMethod` | String | *Vereist.* De methode die Adobe gebruikt voor aanroepen van uw server. De opties zijn `GET`, `PUT`, `POST`, `DELETE`, `PATCH` . |
| `httpTemplate.requestBody.templatingStrategy` | String | *Vereist.* Gebruik `PEBBLE_V1` . |
| `httpTemplate.requestBody.value` | String | *Vereist.* Deze tekenreeks is de versie met escape-teken die de gegevens van Experience Platform-klanten omzet in de indeling die uw service verwacht. <br> <ul><li> Voor informatie over hoe te om het malplaatje te schrijven, lees [ Gebruikend het malplaatjesectie ](../../functionality/destination-server/message-format.md#using-templating). </li><li> Voor meer informatie over karakter het ontsnappen, verwijs naar de [ norm RFC JSON, sectie zeven ](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Voor een voorbeeld van een eenvoudige transformatie, verwijs naar de [ transformatie van de Attributen van het Profiel ](../../functionality/destination-server/message-format.md#attributes). </li></ul> |
| `httpTemplate.contentType` | String | *Vereist.* Het inhoudstype dat uw server accepteert. Deze waarde is zeer waarschijnlijk `application/json` . |

{style="table-layout:auto"}

+++

+++Antwoord

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde configuratie van de bestemmingsserver terug.

+++

>[!TAB Amazon S3]

**creeer een Amazon S3 bestemmingsserver**

U moet een [!DNL Amazon S3] doelserver maken die vergelijkbaar is met de hieronder weergegeven server wanneer u een op een bestand gebaseerde [!DNL Amazon S3] -bestemming configureert.

+++Verzoek

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
| `name` | String | De naam van de doelverbinding. |
| `destinationServerType` | String | Stel deze waarde in op basis van het doelplatform. Stel deze waarde voor [!DNL Amazon S3] in op `FILE_BASED_S3` . |
| `fileBasedS3Destination.bucket.templatingStrategy` | String | *Vereist.* Gebruik `PEBBLE_V1` . |
| `fileBasedS3Destination.bucket.value` | String | De naam van de [!DNL Amazon S3] emmer die door dit doel moet worden gebruikt. |
| `fileBasedS3Destination.path.templatingStrategy` | String | *Vereist.* Gebruik `PEBBLE_V1` . |
| `fileBasedS3Destination.path.value` | String | Het pad naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen. |
| `fileConfigurations` | N.v.t. | Zie [ dossier het formatteren configuratie ](../../functionality/destination-server/file-formatting.md) voor gedetailleerde informatie over hoe te om deze montages te vormen. |

{style="table-layout:auto"}

+++

+++Antwoord

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde configuratie van de bestemmingsserver terug.

+++

>[!TAB SFTP]

**creeer een [!DNL SFTP] bestemmingsserver**

U moet een [!DNL SFTP] doelserver maken die vergelijkbaar is met de hieronder weergegeven server wanneer u een op een bestand gebaseerde [!DNL SFTP] -bestemming configureert.

+++Verzoek

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
      "hostName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.hostName}}"
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
| `name` | String | De naam van de doelverbinding. |
| `destinationServerType` | String | Stel deze waarde in op basis van het doelplatform. Stel dit voor [!DNL SFTP] -doelen in op `FILE_BASED_SFTP` . |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | String | *Vereist.* Gebruik `PEBBLE_V1` . |
| `fileBasedSFTPDestination.rootDirectory.value` | String | De hoofdmap van de doelopslag. |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | String | *Vereist.* Gebruik `PEBBLE_V1` . |
| `fileBasedSFTPDestination.hostName.value` | String | De hostnaam van de bestemmingsopslag. |
| `port` | Geheel | De SFTP-serverpoort. |
| `encryptionMode` | String | Geeft aan of bestandsversleuteling moet worden gebruikt. Ondersteunde waarden: <ul><li>PGP</li><li>Geen</li></ul> |
| `fileConfigurations` | N.v.t. | Zie [ dossier het formatteren configuratie ](../../functionality/destination-server/file-formatting.md) voor gedetailleerde informatie over hoe te om deze montages te vormen. |

{style="table-layout:auto"}

+++

+++Antwoord

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde configuratie van de bestemmingsserver terug.

+++

>[!TAB  Azure de Opslag van het meer van Gegevens ]

**creeer een [!DNL Azure Data Lake Storage] bestemmingsserver**

U moet een [!DNL Azure Data Lake Storage] doelserver maken die vergelijkbaar is met de hieronder weergegeven server wanneer u een op een bestand gebaseerde [!DNL Azure Data Lake Storage] -bestemming configureert.

+++Verzoek

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
| `name` | String | De naam van de doelverbinding. |
| `destinationServerType` | String | Stel deze waarde in op basis van het doelplatform. Stel dit voor [!DNL Azure Data Lake Storage] -doelen in op `FILE_BASED_ADLS_GEN2` . |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | String | *Vereist.* Gebruik `PEBBLE_V1` . |
| `fileBasedAdlsGen2Destination.path.value` | String | Het pad naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen. |
| `fileConfigurations` | N.v.t. | Zie [ dossier het formatteren configuratie ](../../functionality/destination-server/file-formatting.md) voor gedetailleerde informatie over hoe te om deze montages te vormen. |

{style="table-layout:auto"}

+++

+++Antwoord

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde configuratie van de bestemmingsserver terug.

+++

>[!TAB  Azure Blob Storage ]

**creeer een [!DNL Azure Blob Storage] bestemmingsserver**

U moet een [!DNL Azure Blob Storage] doelserver maken die vergelijkbaar is met de hieronder weergegeven server wanneer u een op een bestand gebaseerde [!DNL Azure Blob Storage] -bestemming configureert.

+++Verzoek

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
| `name` | String | De naam van de doelverbinding. |
| `destinationServerType` | String | Stel deze waarde in op basis van het doelplatform. Stel dit voor [!DNL Azure Blob Storage] -doelen in op `FILE_BASED_AZURE_BLOB` . |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | String | *Vereist.* Gebruik `PEBBLE_V1` . |
| `fileBasedAzureBlobDestination.path.value` | String | Het pad naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | String | *Vereist.* Gebruik `PEBBLE_V1` . |
| `fileBasedAzureBlobDestination.container.value` | String | De naam van de [!DNL Azure Blob Storage] -container die door dit doel moet worden gebruikt. |
| `fileConfigurations` | N.v.t. | Zie [ dossier het formatteren configuratie ](../../functionality/destination-server/file-formatting.md) voor gedetailleerde informatie over hoe te om deze montages te vormen. |

{style="table-layout:auto"}

+++

+++Antwoord

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde configuratie van de bestemmingsserver terug.

+++

>[!TAB  Gegevens Landing Zone (DLZ) ]

**creeer a [!DNL Data Landing Zone (DLZ)] bestemmingsserver**

U moet een [!DNL Data Landing Zone (DLZ)] doelserver maken die vergelijkbaar is met de hieronder weergegeven server wanneer u een op een bestand gebaseerde [!DNL Data Landing Zone (DLZ)] -bestemming configureert.

+++Verzoek

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
      "useCase": "dlz_destination"
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
| `name` | String | De naam van de doelverbinding. |
| `destinationServerType` | String | Stel deze waarde in op basis van het doelplatform. Stel dit voor [!DNL Data Landing Zone] -doelen in op `FILE_BASED_DLZ` . |
| `fileBasedDlzDestination.path.templatingStrategy` | String | *Vereist.* Gebruik `PEBBLE_V1` . |
| `fileBasedDlzDestination.path.value` | String | Het pad naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen. |
| `fileConfigurations` | N.v.t. | Zie [ dossier het formatteren configuratie ](../../functionality/destination-server/file-formatting.md) voor gedetailleerde informatie over hoe te om deze montages te vormen. |

{style="table-layout:auto"}

+++

+++Antwoord

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde configuratie van de bestemmingsserver terug.

+++

>[!TAB  Google Cloud Storage ]

**creeer a [!DNL Google Cloud Storage] bestemmingsserver**

U moet een [!DNL Google Cloud Storage] doelserver maken die vergelijkbaar is met de hieronder weergegeven server wanneer u een op een bestand gebaseerde [!DNL Google Cloud Storage] -bestemming configureert.

+++Verzoek

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
| `name` | String | De naam van de doelverbinding. |
| `destinationServerType` | String | Stel deze waarde in op basis van het doelplatform. Stel dit voor [!DNL Google Cloud Storage] -doelen in op `FILE_BASED_GOOGLE_CLOUD` . |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | String | *Vereist.* Gebruik `PEBBLE_V1` . |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | String | De naam van de [!DNL Google Cloud Storage] emmer die door dit doel moet worden gebruikt. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | String | *Vereist.* Gebruik `PEBBLE_V1` . |
| `fileBasedGoogleCloudStorageDestination.path.value` | String | Het pad naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen. |
| `fileConfigurations` | N.v.t. | Zie [ dossier het formatteren configuratie ](../../functionality/destination-server/file-formatting.md) voor gedetailleerde informatie over hoe te om deze montages te vormen. |

{style="table-layout:auto"}

+++

+++Antwoord

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde configuratie van de bestemmingsserver terug.

+++

>[!ENDTABS]

### Dynamische schema-doelservers maken {#dynamic-schema-servers}

Met dynamische schema&#39;s kunt u dynamisch de ondersteunde doelkenmerken ophalen en schema&#39;s genereren op basis van uw eigen API. U moet een bestemmingsserver voor dynamische schema&#39;s vormen alvorens u het schema kunt vormen.

Zie in het lusje onder een voorbeeld van een bestemmingsserver voor bestemmingen die [ dynamische schema&#39;s ](../../functionality/destination-configuration/schema-configuration.md#dynamic-schema-configuration) gebruiken.

De nuttige voorbeeldlading hieronder omvat alle parameters die voor een dynamische schemaserver worden vereist.

>[!BEGINTABS]

>[!TAB  Dynamische schemaserver ]

**creeer een dynamische schemaserver**

U moet een dynamische schemaserver tot stand brengen gelijkend op hieronder getoond wanneer u een bestemming vormt die zijn profielschema van uw eigen API eindpunt terugwint. In tegenstelling tot een statisch schema gebruikt een dynamisch schema geen `profileFields` -array. In plaats daarvan gebruiken dynamische schema&#39;s een dynamische schemaserver die met uw eigen API verbindt van waar het de schemaconfiguratie terugwint.

+++Verzoek

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
| `name` | String | *Vereist.* Vertegenwoordigt een vriendelijke naam van uw dynamische schemaserver, die slechts voor Adobe zichtbaar is. |
| `destinationServerType` | String | *Vereist.* Ingesteld op `URL_BASED` voor dynamische schema-servers. |
| `urlBasedDestination.url.templatingStrategy` | String | *Vereist.* <ul><li>Gebruik `PEBBLE_V1` als Adobe de URL in het onderstaande veld `value` moet transformeren. Gebruik deze optie als u een eindpunt als: `https://api.moviestar.com/data/{{customerData.region}}/items` hebt. </li><li> Gebruik `NONE` als er aan de Adobe-zijde geen transformatie nodig is, bijvoorbeeld als u een eindpunt hebt, zoals: `https://api.moviestar.com/data/items` .</li></ul> |
| `urlBasedDestination.url.value` | String | *Vereist.* Vul het adres in van het API-eindpunt dat Experience Platform moet verbinden met de schemavelden en open deze om te vullen als doelvelden in de toewijzingsstap van de activeringsworkflow. |
| `httpTemplate.httpMethod` | String | *Vereist.* De methode die Adobe gebruikt voor aanroepen van uw server. Gebruik `GET` voor dynamische schemaservers. |
| `responseFields.templatingStrategy` | String | *Vereist.* Gebruik `PEBBLE_V1` . |
| `responseFields.value` | String | *Vereist.* Deze tekenreeks is de transformatiesjabloon met escape-teken dat de reactie die is ontvangen van de partner-API, transformeert naar het partnerschema dat wordt weergegeven in de Experience Platform-gebruikersinterface. <br> <ul><li> Voor informatie over hoe te om het malplaatje te schrijven, lees [ Gebruikend het malplaatjesectie ](../../functionality/destination-server/message-format.md#using-templating). </li><li> Voor meer informatie over karakter het ontsnappen, verwijs naar de [ norm RFC JSON, sectie zeven ](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Voor een voorbeeld van een eenvoudige transformatie, verwijs naar de [ transformatie van de Attributen van het Profiel ](../../functionality/destination-server/message-format.md#attributes). </li></ul> |

{style="table-layout:auto"}

+++

+++Antwoord

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde configuratie van de bestemmingsserver terug.

+++


>[!ENDTABS]


### Dynamische vervolgkeuzelijstservers maken {#dynamic-dropdown-servers}

Het gebruik [ dynamische dropdowns ](../../functionality/destination-configuration/customer-data-fields.md#dynamic-dropdown-selectors) om dropdown gebieden van klantengegevens dynamisch terug te winnen en te bevolken, die op uw eigen API worden gebaseerd. U kunt bijvoorbeeld een lijst ophalen met bestaande gebruikersaccounts die u wilt gebruiken voor een doelverbinding.

U moet een bestemmingsserver voor dynamische dropdowns vormen alvorens u het dynamische dropwdown gebied van de klantengegevens kunt vormen.

Zie op het tabblad onder een voorbeeld van een doelserver die wordt gebruikt om dynamisch de waarden op te halen die in een vervolgkeuzelijst, via een API, moeten worden weergegeven.

De nuttige voorbeeldlading hieronder omvat alle parameters die voor een dynamische schemaserver worden vereist.

>[!BEGINTABS]

>[!TAB  Dynamische dropdown server ]

**creeer een dynamische dropdown server**

U moet een dynamische dropdown server tot stand brengen gelijkend op hieronder getoond wanneer u een bestemming vormt die de waarden voor een dropdown gebied van de klantengegevens van uw eigen API eindpunt terugwint.

+++Verzoek

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
| `name` | String | *Vereist.* Vertegenwoordigt een vriendelijke naam van uw dynamische dropdown server, die slechts voor Adobe zichtbaar is. |
| `destinationServerType` | String | *Vereist.* Ingesteld op `URL_BASED` voor dynamische vervolgkeuzeservers. |
| `urlBasedDestination.url.templatingStrategy` | String | *Vereist.* <ul><li>Gebruik `PEBBLE_V1` als Adobe de URL in het onderstaande veld `value` moet transformeren. Gebruik deze optie als u een eindpunt als: `https://api.moviestar.com/data/{{customerData.region}}/items` hebt. </li><li> Gebruik `NONE` als er aan de Adobe-zijde geen transformatie nodig is, bijvoorbeeld als u een eindpunt hebt, zoals: `https://api.moviestar.com/data/items` .</li></ul> |
| `urlBasedDestination.url.value` | String | *Vereist.* Vul het adres in van het API-eindpunt dat Experience Platform moet verbinden met de dropwdown-waarden en haalt dit op. |
| `httpTemplate.httpMethod` | String | *Vereist.* De methode die Adobe gebruikt voor aanroepen van uw server. Gebruik `GET` voor dynamische dropdown-servers. |
| `httpTemplate.headers` | Object | *Optiona.l* omvat om het even welke kopballen die worden vereist om met de dynamische dropdown server te verbinden. |
| `responseFields.templatingStrategy` | String | *Vereist.* Gebruik `PEBBLE_V1` . |
| `responseFields.value` | String | *Vereist.* Deze tekenreeks is de transformatiesjabloon met escape-teken waarmee de reactie die u van uw API hebt ontvangen, wordt omgezet in de waarden die worden weergegeven in de gebruikersinterface van Experience Platform. <br> <ul><li> Voor informatie over hoe te om het malplaatje te schrijven, lees [ Gebruikend het malplaatjesectie ](../../functionality/destination-server/message-format.md#using-templating). </li><li> Voor meer informatie over karakter het ontsnappen, verwijs naar de [ norm RFC JSON, sectie zeven ](https://tools.ietf.org/html/rfc8259#section-7). |

{style="table-layout:auto"}

+++

+++Antwoord

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde configuratie van de bestemmingsserver terug.

+++

>[!ENDTABS]

## API-foutafhandeling {#error-handling}

Destination SDK API-eindpunten volgen de algemene beginselen van Experience Platform API-foutberichten. Verwijs naar [ API statuscodes ](../../../../landing/troubleshooting.md#api-status-codes) en [ de fouten van de verzoekkopbal ](../../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van Experience Platform.

## Volgende stappen {#next-steps}

Nadat u dit document hebt gelezen, weet u nu hoe u een nieuwe doelserver kunt maken via het Destination SDK `/authoring/destination-servers` API-eindpunt.

Raadpleeg de volgende artikelen voor meer informatie over wat u met dit eindpunt kunt doen:

* [De configuratie van een doelserver ophalen](retrieve-destination-server.md)
* [Een doelserverconfiguratie bijwerken](update-destination-server.md)
* [Een doelserverconfiguratie verwijderen](delete-destination-server.md)

Om te begrijpen waar dit eindpunt in het bestemmings auteursproces past, zie de volgende artikelen:

* [Destination SDK gebruiken om een streamingbestemming te configureren](../../guides/configure-destination-instructions.md#create-server-template-configuration)
* [Destination SDK gebruiken om een bestandsgebaseerde bestemming te configureren](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)
