---
description: Deze pagina illustreert de API vraag die wordt gebruikt om een bestaande configuratie van de bestemmingsserver door Adobe Experience Platform Destination SDK bij te werken.
title: Een doelserverconfiguratie bijwerken
exl-id: 579d2cc1-5110-4fba-9dcc-ff4b8d259827
source-git-commit: e1dd6ae9bf28014e8e84de85bdf67707744ea0ad
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 2%

---

# Een doelserverconfiguratie bijwerken

Deze pagina illustreert de API-aanvraag en lading die u kunt gebruiken om een bestaande configuratie van de doelserver bij te werken met behulp van het API-eindpunt `/authoring/destination-servers` .

>[!TIP]
>
>Om het even welke updateverrichting op geproduceerde/openbare bestemmingen is zichtbaar slechts nadat u [ het publiceren API ](../../publishing-api/create-publishing-request.md) gebruikt en de update voor het overzicht van Adobe voorleggen.

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

## Een doelserverconfiguratie bijwerken {#update}

U kunt een [ bestaande ](create-destination-server.md) configuratie van de bestemmingsserver bijwerken door een `PUT` verzoek aan het `/authoring/destination-servers` eindpunt met de bijgewerkte nuttige lading te doen.

>[!TIP]
>
>**API eindpunt**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

Om een bestaande configuratie van de bestemmingsserver en zijn overeenkomstige `{INSTANCE_ID}` te verkrijgen, zie het artikel over [ het terugwinnen van een configuratie van de bestemmingsserver ](retrieve-destination-server.md).

**API formaat**

```http
PUT /authoring/destination-servers/{INSTANCE_ID}
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{INSTANCE_ID}` | De id van de configuratie van de doelserver die u wilt bijwerken. Om een bestaande configuratie van de bestemmingsserver en zijn overeenkomstige `{INSTANCE_ID}` te verkrijgen, zie [ een configuratie van de bestemmingsserver ](retrieve-destination-server.md) terugwinnen. |

De volgende verzoeken werken een bestaande configuratie van de bestemmingsserver bij, die door de parameters wordt gevormd die in de lading worden verstrekt.

Selecteer hieronder elk tabblad om de bijbehorende lading weer te geven.

>[!BEGINTABS]

>[!TAB  Real-time (het stromen) ]

+++Verzoek

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
| `name` | String | *Vereist.* Vertegenwoordigt een vriendelijke naam van uw server, die alleen zichtbaar is voor Adobe. Deze naam is niet zichtbaar aan partners of klanten. Voorbeeld `Moviestar destination server` . |
| `destinationServerType` | String | *Vereist.* Ingesteld op `URL_BASED` voor realtime (streaming) doelen. |
| `urlBasedDestination.url.templatingStrategy` | String | *Vereist.* <ul><li>Gebruik `PEBBLE_V1` als Adobe de URL in het onderstaande veld `value` moet transformeren. Gebruik deze optie als u een eindpunt als: `https://api.moviestar.com/data/{{customerData.region}}/items` hebt. </li><li> Gebruik `NONE` als er aan de Adobe-zijde geen transformatie nodig is, bijvoorbeeld als u een eindpunt hebt, zoals: `https://api.moviestar.com/data/items` .</li></ul> |
| `urlBasedDestination.url.value` | String | *Vereist.* Vul het adres in van het API-eindpunt waarmee Experience Platform verbinding moet maken. |
| `httpTemplate.httpMethod` | String | *Vereist.* De methode die Adobe gebruikt voor aanroepen van uw server. De opties zijn `GET`, `PUT`, `PUT`, `DELETE`, `PATCH` . |
| `httpTemplate.requestBody.templatingStrategy` | String | *Vereist.* Gebruik `PEBBLE_V1` . |
| `httpTemplate.requestBody.value` | String | *Vereist.* Deze tekenreeks is de versie met escape-teken die de gegevens van Experience Platform-klanten omzet in de indeling die uw service verwacht. <br> <ul><li> Voor informatie over hoe te om het malplaatje te schrijven, lees [ Gebruikend het malplaatjesectie ](../../functionality/destination-server/message-format.md#using-templating). </li><li> Voor meer informatie over karakter het ontsnappen, verwijs naar de [ norm RFC JSON, sectie zeven ](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Voor een voorbeeld van een eenvoudige transformatie, verwijs naar de [ transformatie van de Attributen van het Profiel ](../../functionality/destination-server/message-format.md#attributes). </li></ul> |
| `httpTemplate.contentType` | String | *Vereist.* Het inhoudstype dat uw server accepteert. Deze waarde is zeer waarschijnlijk `application/json` . |

{style="table-layout:auto"}

+++

+++Antwoord

Een succesvolle reactie keert status 200 van HTTP met de details van uw bijgewerkte configuratie van de bestemmingsserver terug.

+++

>[!TAB Amazon S3]

+++Verzoek

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

Een succesvolle reactie keert status 200 van HTTP met de details van uw bijgewerkte configuratie van de bestemmingsserver terug.

+++

>[!TAB SFTP]

+++Verzoek

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

Een succesvolle reactie keert status 200 van HTTP met de details van uw bijgewerkte configuratie van de bestemmingsserver terug.

+++

>[!TAB  Azure de Opslag van het meer van Gegevens ]

+++Verzoek

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
| `name` | String | De naam van de doelverbinding. |
| `destinationServerType` | String | Stel deze waarde in op basis van het doelplatform. Stel dit voor [!DNL Azure Data Lake Storage] -doelen in op `FILE_BASED_ADLS_GEN2` . |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | String | *Vereist.* Gebruik `PEBBLE_V1` . |
| `fileBasedAdlsGen2Destination.path.value` | String | Het pad naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen. |
| `fileConfigurations` | N.v.t. | Zie [ dossier het formatteren configuratie ](../../functionality/destination-server/file-formatting.md) voor gedetailleerde informatie over hoe te om deze montages te vormen. |

{style="table-layout:auto"}

+++

+++Antwoord

Een succesvolle reactie keert status 200 van HTTP met de details van uw bijgewerkte configuratie van de bestemmingsserver terug.

+++

>[!TAB  Azure Blob Storage ]

+++Verzoek

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

Een succesvolle reactie keert status 200 van HTTP met de details van uw bijgewerkte configuratie van de bestemmingsserver terug.

+++

>[!TAB  Gegevens Landing Zone (DLZ) ]

+++Verzoek

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

Een succesvolle reactie keert status 200 van HTTP met de details van uw bijgewerkte configuratie van de bestemmingsserver terug.

+++

>[!TAB  Google Cloud Storage ]

+++Verzoek

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

Een succesvolle reactie keert status 200 van HTTP met de details van uw bijgewerkte configuratie van de bestemmingsserver terug.

+++

>[!ENDTABS]

## API-foutafhandeling {#error-handling}

Destination SDK API-eindpunten volgen de algemene beginselen van Experience Platform API-foutberichten. Verwijs naar [ API statuscodes ](../../../../landing/troubleshooting.md#api-status-codes) en [ de fouten van de verzoekkopbal ](../../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van Experience Platform.

## Volgende stappen {#next-steps}

Nadat u dit document hebt gelezen, weet u nu hoe u een configuratie van een doelserver kunt bijwerken via het Destination SDK `/authoring/destination-servers` API-eindpunt.

Raadpleeg de volgende artikelen voor meer informatie over wat u met dit eindpunt kunt doen:

* [Een doelserverconfiguratie maken](create-destination-server.md)
* [De configuratie van een doelserver ophalen](retrieve-destination-server.md)
* [Een doelserverconfiguratie bijwerken](update-destination-server.md)
