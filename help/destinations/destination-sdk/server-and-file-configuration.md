---
description: De server en de specificaties van de dossierconfiguratie voor op dossier-gebaseerde bestemmingen kunnen in Adobe Experience Platform Destination SDK via het /destination-servers eindpunt worden gevormd.
title: Configuratieopties voor op een bestand gebaseerde specificaties van de doelserver
exl-id: 56434e36-0458-45d9-961d-f6505de998f7
source-git-commit: 5506a938253083d3dfd657a787eae20a05b1c0a9
workflow-type: tm+mt
source-wordcount: '1274'
ht-degree: 5%

---

# Server- en bestandsconfiguratie voor op een bestand gebaseerde serverspecificaties

## Overzicht {#overview}

>[!IMPORTANT]
>
>De functionaliteit om op dossier-gebaseerde bestemmingen te vormen en voor te leggen gebruikend Adobe Experience Platform Destination SDK is momenteel in Bèta. De documentatie en functionaliteit kunnen worden gewijzigd.

Op deze pagina worden alle configuratieopties voor de server weergegeven voor de doelservers op basis van bestanden en ziet u hoe u verschillende opties voor de bestandsconfiguratie instelt voor gebruikers die bestanden exporteren van het Experience Platform naar uw bestemming.

De server en de specificaties van de dossierconfiguratie voor op dossier-gebaseerde bestemmingen kunnen in Adobe Experience Platform Destination SDK via worden gevormd `/destination-servers` eindpunt. Lezen [API-eindpuntbewerkingen van doelserver](./destination-server-api.md) voor een volledige lijst van verrichtingen kunt u op het eindpunt uitvoeren.

In de volgende secties vindt u specificaties voor doelservers die specifiek zijn voor elk ondersteund doeltype van een batch in Destination SDK.

## Amazon S3-bestemmingsserver, op basis van bestand, specificatie {#s3-example}

In het onderstaande voorbeeld ziet u een correcte configuratie van de doelserver voor een Amazon S3-bestemming.

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

{style=&quot;table-layout:auto&quot;}

## Specificatie van SFTP-doelserver op basis van bestanden {#sftp-example}

In het onderstaande voorbeeld ziet u een correcte configuratie van de doelserver voor een SFTP-bestemming.

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

{style=&quot;table-layout:auto&quot;}

## Op basis van bestand [!DNL Azure Data Lake Storage] ([!DNL ADLS]) specificatie doelserver {#adls-example}

In het onderstaande voorbeeld ziet u een correcte configuratie van de doelserver voor een [!DNL Azure Data Lake Storage] bestemming.

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

{style=&quot;table-layout:auto&quot;}

## Op basis van bestand [!DNL Azure Blob Storage] specificatie doelserver {#blob-example}

In het onderstaande voorbeeld ziet u een correcte configuratie van de doelserver voor een [!DNL Azure Blob Storage] bestemming.

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

{style=&quot;table-layout:auto&quot;}

## Op basis van bestand [!DNL Data Landing Zone] ([!DNL DLZ]) specificatie doelserver {#dlz-example}

In het onderstaande voorbeeld ziet u een correcte configuratie van de doelserver voor een [!DNL Data Landing Zone] ([!DNL DLZ]) bestemming.

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

{style=&quot;table-layout:auto&quot;}

## Op basis van bestand [!DNL Google Cloud Storage] specificatie doelserver {#gcs-example}

In het onderstaande voorbeeld ziet u een correcte configuratie van de doelserver voor een [!DNL Google Cloud Storage] bestemming.

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

{style=&quot;table-layout:auto&quot;}

## Configuratie bestandsindeling {#file-configuration}

In deze sectie worden de instellingen voor de bestandsindeling voor het geëxporteerde bestand beschreven `CSV` bestanden. U kunt verschillende eigenschappen van de geëxporteerde bestanden aanpassen aan de vereisten van het systeem voor het ontvangen van bestanden aan uw zijde, zodat u de bestanden die u van het Experience Platform hebt ontvangen, optimaal kunt lezen en interpreteren.

>[!NOTE]
>
>CSV-opties worden alleen ondersteund bij het exporteren van CSV-bestanden. De `fileConfigurations` is niet verplicht bij het instellen van een nieuwe doelserver. Als u geen waarden doorgeeft in de API-aanroep voor de CSV-opties, worden de standaardwaarden van de [referentietabel verderop](#file-formatting-reference-and-example) wordt gebruikt.

### Bestandsconfiguraties met CSV-opties en de `templatingStrategy` instellen op `NONE` {#file-configuration-templating-none}

In het onderstaande configuratievoorbeeld zijn alle CSV-opties vast. De exportinstellingen die zijn gedefinieerd in elk van de `csvOptions` parameters zijn definitief en gebruikers kunnen deze niet wijzigen.

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
            }
        },
        "maxFileRowCount":5000000
    }
```

### Bestandsconfiguraties met CSV-opties en de `templatingStrategy` instellen op `PEBBLE_V1` {#file-configuration-templating-pebble}

In het onderstaande configuratievoorbeeld zijn geen van de CSV-opties vast. De `value` in elk van de `csvOptions` parameters worden gevormd op een overeenkomstig gebied van klantengegevens door `/destinations` eindpunt (bijvoorbeeld `customerData.quote` voor de `quote` bestandsindeling) en gebruikers kunnen de gebruikersinterface van het Experience Platform gebruiken om een keuze te maken uit de verschillende opties die u configureert in het desbetreffende gegevensveld van de klant.

```json
  "fileConfigurations": {
    "compression": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{% if customerData contains 'compression' and customerData.compression is not empty %}{{customerData.compression}}{% else %}NONE{% endif %}"
    },
    "fileType": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{{customerData.fileType}}"
    },
    "csvOptions": {
      "sep": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'delimiter' %}{{customerData.csvOptions.delimiter}}{% else %},{% endif %}"
      },
      "quote": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'quote' %}{{customerData.csvOptions.quote}}{% else %}\"{% endif %}"
      },
      "escape": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'escape' %}{{customerData.csvOptions.escape}}{% else %}\\{% endif %}"
      },
      "nullValue": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'nullValue' %}{{customerData.csvOptions.nullValue}}{% else %}null{% endif %}"
      },
      "emptyValue": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'emptyValue' %}{{customerData.csvOptions.emptyValue}}{% else %}{% endif %}"
      }
    }
  }
```

### Volledige verwijzing en voorbeelden voor ondersteunde opties voor bestandsindeling {#file-formatting-reference-and-example}

>[!TIP]
>
>De hieronder beschreven opmaakopties voor CSV-bestanden worden ook beschreven in de [Handleiding voor Apache Spark voor CSV-bestanden](https://spark.apache.org/docs/latest/sql-data-sources-csv.html). De onderstaande beschrijvingen zijn ontleend aan de gids voor Apache Spark.

Hieronder ziet u een volledige verwijzing naar alle beschikbare opmaakopties voor bestanden in Destination SDK, naast uitvoervoorbeelden voor elke optie.

| Veld | Vereist/optioneel | Beschrijving | Standaardwaarde | Voorbeeld van uitvoer 1 | Voorbeeld van uitvoer 2 |
|---|---|---|---|---|---|
| `templatingStrategy` | Vereist | Voor elke optie voor bestandsindeling die u configureert, moet u de parameter toevoegen `templatingStrategy`, die twee waarden kunnen hebben: <br><ul><li>`NONE`: Gebruik deze waarde als u niet van plan bent gebruikers toe te staan om tussen verschillende waarden voor een configuratie te selecteren. Zie [deze configuratie](#file-configuration-templating-none) voor een voorbeeld waarin de opties voor bestandsindeling zijn gecorrigeerd.</li><li>`PEBBLE_V1`: Gebruik deze waarde als u gebruikers wilt toestaan om tussen verschillende waarden voor een configuratie te selecteren. In dit geval moet u ook een corresponderend gegevensveld voor de klant instellen in het dialoogvenster `/destination` eindpuntconfiguratie, aan oppervlakte de diverse opties aan gebruikers in UI. Zie [deze configuratie](#file-configuration-templating-pebble) voor een voorbeeld waarin gebruikers verschillende waarden voor opties voor bestandsindeling kunnen selecteren.</li></ul> | - | - | - |
| `compression.value` | Optioneel | Compressiecodec voor het opslaan van gegevens naar een bestand. Ondersteunde waarden: `none`, `bzip2`, `gzip`, `lz4`, en `snappy`. | `none` | - | - |
| `fileType.value` | Optioneel | Hiermee geeft u de indeling voor het uitvoerbestand op. Ondersteunde waarden: `csv`, `parquet`, en `json`. | `csv` | - | - |
| `csvOptions.quote.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Hiermee stelt u één teken in dat wordt gebruikt voor het escape-teken van geciteerde waarden, waarbij het scheidingsteken deel kan uitmaken van de waarde. | `null` | - | - |
| `csvOptions.quoteAll.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Geeft aan of alle waarden altijd tussen aanhalingstekens moeten worden geplaatst. Standaard worden alleen escape-waarden gebruikt die een aanhalingsteken bevatten. | `false` | `quoteAll`:`false` --> `male,John,"TestLastName"` | `quoteAll`:`true` -->`"male","John","TestLastName"` |
| `csvOptions.delimiter.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Hiermee stelt u een scheidingsteken in voor elk veld en elke waarde. Dit scheidingsteken kan een of meer tekens bevatten. | `,` | `delimiter`:`,` —> `comma-separated values"` | `delimiter`:`\t` —> `tab-separated values` |
| `csvOptions.escape.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Hiermee stelt u één teken in dat wordt gebruikt voor het escape-teken voor aanhalingstekens binnen een reeds geciteerde waarde. | `\` | `"escape"`:`"\\"` —> `male,John,"Test,\"LastName5"` | `"escape"`:`"'"` —> `male,John,"Test,'''"LastName5"` |
| `csvOptions.escapeQuotes.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Geeft aan of waarden met aanhalingstekens altijd tussen aanhalingstekens moeten worden geplaatst. Standaard worden alle waarden met een aanhalingsteken verwijderd. | `true` | - | - |
| `csvOptions.header.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Geeft aan of de namen van kolommen als de eerste regel in het geëxporteerde bestand moeten worden geschreven. | `true` | - | - |
| `csvOptions.ignoreLeadingWhiteSpace.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Hiermee wordt aangegeven of witruimten vóór elkaar worden bijgesneden op basis van waarden. | `true` | `ignoreLeadingWhiteSpace`:`true` —> `"male","John","TestLastName"` | `ignoreLeadingWhiteSpace`:`false`--> `"    male","John","TestLastName"` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Geeft aan of volgwitruimten moeten worden bijgesneden op basis van waarden. | `true` | `ignoreTrailingWhiteSpace`:`true` —> `"male","John","TestLastName"` | `ignoreTrailingWhiteSpace`:`false`—> `"male    ","John","TestLastName"` |
| `csvOptions.nullValue.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Stelt de tekenreeksrepresentatie in van een waarde null. | `""` | `nullvalue`:`""` —> `male,"",TestLastName` | `nullvalue`:`"NULL"` —> `male,NULL,TestLastName` |
| `csvOptions.dateFormat.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Geeft de datumnotatie aan. | `yyyy-MM-dd` | `dateFormat`:`yyyy-MM-dd` —> `male,TestLastName,John,2022-02-24` | `dateFormat`:`MM/dd/yyyy` —> `male,TestLastName,John,02/24/2022` |
| `csvOptions.timestampFormat.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Stelt de tekenreeks in die een tijdstempelindeling aangeeft. | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` | - | - |
| `csvOptions.charToEscapeQuoteEscaping.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Stelt één teken in dat wordt gebruikt voor escape voor het aanhalingsteken. | `\` wanneer de escape- en aanhalingstekens verschillend zijn. `\0` wanneer de escape- en aanhalingsteken hetzelfde zijn. | - | - |
| `csvOptions.emptyValue.value` | Optioneel | *Alleen voor`"fileType.value": "csv"`*. Stelt de tekenreeksrepresentatie in van een lege waarde. | `""` | `"emptyValue":""` --> `male,"",John` | `"emptyValue":"empty"` —> `male,empty,John` |

{style=&quot;table-layout:auto&quot;}