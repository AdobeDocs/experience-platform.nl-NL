---
description: De server en de specificaties van de dossierconfiguratie voor op dossier-gebaseerde bestemmingen kunnen in Adobe Experience Platform Destination SDK via het /destination-servers eindpunt worden gevormd.
title: (Bèta) de opties van de configuratie voor op dossier-gebaseerde bestemmingsserverspecificaties
exl-id: 56434e36-0458-45d9-961d-f6505de998f7
source-git-commit: 3c8ad296ab9f0ce62743466ca8823b13c4545a9d
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 8%

---

# (bèta) Server- en bestandsconfiguratie voor op een bestand gebaseerde serverspecificaties

## Overzicht {#overview}

>[!IMPORTANT]
>
>De functionaliteit om op dossier-gebaseerde bestemmingen te vormen en voor te leggen gebruikend Adobe Experience Platform Destination SDK is momenteel in Bèta. De documentatie en functionaliteit kunnen worden gewijzigd.

Op deze pagina worden alle opties voor serverconfiguratie voor uw bestandsgebaseerde doelservers beschreven en wordt uitgelegd hoe u verschillende opties voor bestandsconfiguratie instelt voor gebruikers die bestanden van het Experience Platform naar uw bestemming exporteren.

De server en de specificaties van de dossierconfiguratie voor op dossier-gebaseerde bestemmingen kunnen in Adobe Experience Platform Destination SDK via worden gevormd `/destination-servers` eindpunt. Lezen [API-eindpuntbewerkingen van doelserver](./destination-server-api.md) voor een volledige lijst van verrichtingen kunt u op het eindpunt uitvoeren.

## Amazon S3-bestemmingsserver, op basis van bestand, specificatie {#s3-example}

```json
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
       // See the file formatting configuration section further below on this page
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
| `fileConfigurations` | Object | Zie [bestandsindelingconfiguratie](#file-configuration) voor nadere uitleg over deze paragraaf. |

## Specificatie van SFTP-doelserver op basis van bestanden {#sftp-example}

```json
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSftpDestination":{
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
       // See the file formatting configuration section further below on this page
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
| `fileConfigurations` | Object | Zie [bestandsindelingconfiguratie](#file-configuration) voor nadere uitleg over deze paragraaf. |

## Op basis van bestand [!DNL Azure Data Lake Storage] ([!DNL ADLS]) specificatie doelserver {#adls-example}

```json
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
       // See the file formatting configuration section further below on this page
    }
}
```

| Parameter | Type | Beschrijving |
|---|---|---|
| `name` | Tekenreeks | De naam van de doelverbinding. |
| `destinationServerType` | Tekenreeks | Stel deze waarde in op basis van het doelplatform. Voor [!DNL Azure Data Lake Storage] doelen, stel deze in op `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Tekenreeks | *Vereist.* Gebruik `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | Tekenreeks | Het pad naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen. |
| `fileConfigurations` | Object | Zie [bestandsindelingconfiguratie](#file-configuration) voor nadere uitleg over deze paragraaf. |

## Op basis van bestand [!DNL Azure Blob Storage] specificatie doelserver {#blob-example}

```json
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
       // See the file formatting configuration section further below on this page
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
| `fileConfigurations` | Object | Zie [bestandsindelingconfiguratie](#file-configuration) voor nadere uitleg over deze paragraaf. |

## Op basis van bestand [!DNL Data Landing Zone] ([!DNL DLZ]) specificatie doelserver {#dlz-example}

```json
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
       // See the file formatting configuration section further below on this page
    }
}
```

| Parameter | Type | Beschrijving |
|---|---|---|
| `name` | Tekenreeks | De naam van de doelverbinding. |
| `destinationServerType` | Tekenreeks | Stel deze waarde in op basis van het doelplatform. Voor [!DNL Data Landing Zone] doelen, stel deze in op `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | Tekenreeks | *Vereist.*  Gebruik `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | Tekenreeks | Het pad naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen. |
| `fileConfigurations` | Object | Zie [bestandsindelingconfiguratie](#file-configuration) voor nadere uitleg over deze paragraaf. |

## Op basis van bestand [!DNL Google Cloud Storage] specificatie doelserver {#gcs-example}

```json
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
   "fileConfigurations":{
      // See the file formatting configuration section further below on this page
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
| `fileConfigurations` | Object | Zie [bestandsindelingconfiguratie](#file-configuration) voor nadere uitleg over deze paragraaf. |

## Configuratie bestandsindeling {#file-configuration}

In deze sectie worden de instellingen voor de bestandsindeling voor het geëxporteerde bestand beschreven `CSV` bestanden. U kunt verschillende eigenschappen van de geëxporteerde bestanden aanpassen aan de vereisten van het systeem voor het ontvangen van bestanden aan uw zijde, zodat u de bestanden die u van het Experience Platform hebt ontvangen, optimaal kunt lezen en interpreteren.

>[!NOTE]
>
>CSV-opties worden alleen ondersteund bij het exporteren van CSV-bestanden. De `fileConfigurations` is niet verplicht bij het instellen van een nieuwe doelserver. Als u geen waarden doorgeeft in de API-aanroep voor de CSV-opties, worden de standaardwaarden uit de onderstaande tabel gebruikt.

```json
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
        },
        "maxFileRowCount":5000000
    }
```

| Veld | Vereist/optioneel | Beschrijving | Standaardwaarde |
|---|---|---|---|
| `compression.value` | Optioneel | Compressiecodec voor het opslaan van gegevens naar een bestand. Ondersteunde waarden: `none`, `bzip2`, `gzip`, `lz4`, en `snappy`. | `none` |
| `fileType.value` | Optioneel | Hiermee geeft u de indeling voor het uitvoerbestand op. Ondersteunde waarden: `csv`, `parquet`, en `json`. | `csv` |
| `csvOptions.quote.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Hiermee stelt u één teken in dat wordt gebruikt voor het escape-teken van geciteerde waarden, waarbij het scheidingsteken deel kan uitmaken van de waarde. | `null` |
| `csvOptions.quoteAll.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Geeft aan of alle waarden altijd tussen aanhalingstekens moeten worden geplaatst. Standaard worden alleen escape-waarden gebruikt die een aanhalingsteken bevatten. | `false` |
| `csvOptions.escape.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Hiermee stelt u één teken in dat wordt gebruikt voor het escape-teken voor aanhalingstekens binnen een reeds geciteerde waarde. | `\` |
| `csvOptions.escapeQuotes.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Geeft aan of waarden met aanhalingstekens altijd tussen aanhalingstekens moeten worden geplaatst. Standaard worden alle waarden met een aanhalingsteken verwijderd. | `true` |
| `csvOptions.header.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Geeft aan of de namen van kolommen als eerste regel moeten worden geschreven. | `true` |
| `csvOptions.ignoreLeadingWhiteSpace.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Hiermee wordt aangegeven of witruimten vóór elkaar worden bijgesneden op basis van waarden. | `true` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Geeft aan of volgwitruimten moeten worden bijgesneden op basis van waarden. | `true` |
| `csvOptions.nullValue.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Stelt de tekenreeksrepresentatie in van een waarde null. | `""` |
| `csvOptions.dateFormat.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Geeft de datumnotatie aan. | `yyyy-MM-dd` |
| `csvOptions.timestampFormat.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Stelt de tekenreeks in die een tijdstempelindeling aangeeft. | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` |
| `csvOptions.charToEscapeQuoteEscaping.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Stelt één teken in dat wordt gebruikt voor escape voor het aanhalingsteken. | `\` wanneer de escape- en aanhalingstekens verschillend zijn. `\0` wanneer de escape- en aanhalingsteken hetzelfde zijn. |
| `csvOptions.emptyValue.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Stelt de tekenreeksrepresentatie in van een lege waarde. | `""` |
| `csvOptions.lineSep.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Hiermee definieert u het lijnscheidingsteken dat moet worden gebruikt voor schrijven. De maximumlengte is 1 teken. | `\n` |
| `maxFileRowCount` | Optioneel | Maximumaantal rijen dat het geëxporteerde bestand kan bevatten. Configureer dit op basis van de vereisten voor de bestandsgrootte van het doelplatform. | N.v.t. |
