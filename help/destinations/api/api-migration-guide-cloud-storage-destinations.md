---
solution: Experience Platform
title: API-migratiegids voor cloudopslagdoelen
description: Meer informatie over de wijzigingen in de workflow om cloudopslagbestemmingen te activeren als onderdeel van de migratie naar de nieuwe doelkaarten voor cloudopslag met extra functionaliteit.
type: Tutorial
exl-id: 4acaf718-794e-43a3-b8f0-9b19177a2bc0
source-git-commit: b651d15260adbcd37fa396fa0b325a9674a92133
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 0%

---

# API-migratiegids voor cloudopslagdoelen

>[!IMPORTANT]
>
>* De functionaliteit die op deze pagina wordt beschreven, is beschikbaar voor klanten die de Real-Time CDP Premiere en Ultimate-pakketten hebben aangeschaft. Neem contact op met uw Adobe-vertegenwoordiger voor meer informatie.

## Migratiecontext {#migration-context}

Starten [Oktober 2022](/help/release-notes/2022/october-2022.md#new-or-updated-destinations)Met de nieuwe functies voor het exporteren van bestanden hebt u toegang tot de verbeterde aanpassingsfunctionaliteit wanneer u bestanden exporteert vanuit het Experience Platform:

* Extra [naamgevingsopties voor bestanden](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).
* Mogelijkheid om aangepaste bestandsheaders in uw geëxporteerde bestanden in te stellen via de [nieuwe toewijzingsstap](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* Mogelijkheid om de [bestandstype](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options) van het geëxporteerde bestand.
* Vermogen [de opmaak van geëxporteerde CSV-gegevensbestanden aanpassen](/help/destinations/ui/batch-destinations-file-formatting-options.md).

Deze functionaliteit wordt ondersteund door de onderstaande bètaboudopslagkaarten:

* [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

<!--

Commenting out the three net new cloud storage destinations

* [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)

-->

Merk op dat momenteel in het Experience Platform UI, u twee zij aan zij bestemmingskaarten van de drie bestemmingen kunt zien. Hieronder ziet u de [!DNL Amazon S3] oude en nieuwe bestemmingen. In alle gevallen worden de kaarten gemarkeerd met **Beta** Dit zijn de nieuwe doelkaarten.

![Afbeelding van de twee Amazon S3-doelkaarten in een weergave Naast elkaar.](../assets/catalog/cloud-storage/amazon-s3/two-amazons3-destination-cards.png)

Hoewel deze bestemmingen met verbeterde functionaliteit aanvankelijk als bèta werden aangeboden, *Adobe verplaatst nu alle Real-Time CDP-klanten naar de nieuwe cloudopslagbestemmingen*. Voor klanten die al [!DNL Amazon S3], [!DNL Azure Blob], of SFTP, betekent dit dat bestaande dataflows naar de nieuwe kaarten worden gemigreerd. Lees verder voor meer informatie over de specifieke wijzigingen als onderdeel van de migratie.

## Wie deze pagina van toepassing is op {#who-this-applies-to}

Als u al het [Flow Service-API](https://developer.adobe.com/experience-platform-apis/references/destinations/) Als u profielen wilt exporteren naar de Amazon S3-, Azure Blob- of SFTP-cloudopslagdoelen, is deze API-migratiegids op u van toepassing.

Als er scripts worden uitgevoerd in uw [!DNL Amazon S3], [!DNL Azure Blob]of SFTP-opslaglocaties voor de cloud boven op de geëxporteerde bestanden vanuit Experience Platform, zich ervan bewust zijn dat sommige parameters veranderen wat betreft de verbinding en de stroomspecificaties van de nieuwe kaarten, en wat betreft de toewijzingsstap.

Als u bijvoorbeeld een script gebruikt om doelgegevens naar de [!DNL Amazon S3] doel, gebaseerd op de verbindingsspecificatie van [!DNL Amazon S3] doel, moet u er rekening mee houden dat de verbindingsspecificatie wordt gewijzigd, zodat u de filters moet bijwerken.

## Relevante documentatiekoppelingen {#relevant-documentation-links}

Deze sectie bevat de relevante API-zelfstudie en referentiedocumentatie voor de verbeterde functionaliteit voor het exporteren van gegevens naar cloudopslagbestemmingen.

<!--

TBD if we keep this link but will likely remove it

[Legacy API tutorial to export data to cloud storage destinations](/help/destinations/api/connect-activate-batch-destinations.md) (outdated, do not use anymore)

-->
* [API-zelfstudie voor het exporteren van segmenten naar cloudopslagdoelen](/help/destinations/api/activate-segments-file-based-destinations.md)
* [Referentiedocumentatie voor de doelservice-API](https://developer.adobe.com/experience-platform-apis/references/destinations/)

## Samenvatting van achterwaarts incompatibele wijzigingen {#summary-backwards-incompatible-changes}

Met de migratie naar de nieuwe bestemmingen, stroomt al uw bestaande dataflows aan [!DNL Amazon S3], [!DNL Azure Blob]en SFTP-doelen krijgen nu nieuwe doelverbindingen en basisverbindingen toegewezen. De stap voor profieltoewijzing verandert ook. Achteruit incompatibele wijzigingen worden samengevat in de onderstaande secties voor elke bestemming. Ook de opties weergeven [woordenlijst met bestemmingen](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) voor meer informatie over de voorwaarden in onderstaande grafiek.

![Overzicht van migratiegids](/help/destinations/assets/api/api-migration-guide/migration-guide-diagram.png)

### Wijzigingen die niet compatibel zijn met de [!DNL Amazon S3] doel {#changes-amazon-s3-destination}

De achterwaarts incompatibele wijzigingen voor de API-gebruikers worden bijgewerkt `connection spec ID` en `flow spec ID` zoals weergegeven in onderstaande tabel:

| [!DNL Amazon S3] | Verouderd | Nieuw |
|---------|----------|---------|
| Stroomspecificatie | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 1a0514a6-33d4-4c7f-aff8-594799c47549 |
| Verbindingsspecificatie | 4890fc95-5a1f-4983-94bb-e060c08e3f81 | 4fce964d-3f37-408f-9778-e597338a21ee |

Bekijk de volledige erfenis en de nieuwe basisverbinding en de voorbeelden van de doelverbinding voor [!DNL Amazon S3] in de onderstaande tabbladen. De parameters die vereist zijn om basisverbindingen te maken voor [!DNL Amazon S3] de bestemmingen veranderen niet.

Op dezelfde manier zijn er geen achterwaarts-onverenigbare veranderingen in de parameters die worden vereist om doelverbindingen tot stand te brengen.

>[!BEGINTABS]

>[!TAB Verouderde basisverbinding en doelverbinding]

+++Verouderde weergave [!DNL base connection] for [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "amazon-s3",
  "connectionSpec": {
    "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Access Key",
    "params": {
      "authorizedDate": "2022-10-26",
      "s3SecretKey": "<your-secret-key>",
      "s3AccessKey": "<your-access-key>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"640418e2-0000-0200-0000-6359b9ef0000\"",
  "etag": "\"640418e2-0000-0200-0000-6359b9ef0000\""
}
```

+++

+++Verouderde weergave [!DNL target connection] for [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="12"}
{
  ...
  "name": "test 121",
  "baseConnectionId": "ee86d122-10d3-434b-81c7-7252e4d747a7",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
    "version": "1.0"
  },
  "params": {
    "mode": "S3",
    "path": "testpath",
    "bucketName": "test"
  },
  "version": "\"1609cd86-0000-0200-0000-63892cbb0000\"",
  "etag": "\"1609cd86-0000-0200-0000-63892cbb0000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "ee86d122-10d3-434b-81c7-7252e4d747a7",
      "connectionSpec": {
        "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!TAB Nieuwe basisverbinding en doelverbinding]

+++Nieuwe weergave [!DNL base connection] for [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "Amazon S3",
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Access Key",
    "params": {
      "authorizedDate": "2022-10-26",
      "s3SecretKey": "<your-secret-key>",
      "s3AccessKey": "<your-access-key>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"3708da21-0000-0200-0000-638940b10000\"",
  "etag": "\"3708da21-0000-0200-0000-638940b10000\""
}
```

+++

+++Nieuwe weergave [!DNL target connection] for [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="12, 16-27"}
{
  ...
  "name": "test 121",
  "baseConnectionId": "d114c86f-fd47-4bb6-846c-cb1d15a00fe9",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee",
    "version": "1.0"
  },
  "params": {
    "csvOptions": {
      "nullValue": "null",
      "emptyValue": "",
      "escape": "\\",
      "quote": "",
      "delimiter": ","
    },
    "compression": "NONE",
    "fileType": "CSV",
    "mode": "Server-to-server",
    "path": "testpath",
    "bucketName": "test"
  },
  "version": "\"1b0985c6-0000-0200-0000-638940b10000\"",
  "etag": "\"1b0985c6-0000-0200-0000-638940b10000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "d114c86f-fd47-4bb6-846c-cb1d15a00fe9",
      "connectionSpec": {
        "id": "4fce964d-3f37-408f-9778-e597338a21ee",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!ENDTABS]

### Wijzigingen die niet compatibel zijn met oudere versies [!DNL Azure Blob] doel {#changes-azure-blob-destination}

De achterwaarts incompatibele wijzigingen voor de API-gebruikers worden bijgewerkt `connection spec ID` en `flow spec ID` zoals weergegeven in onderstaande tabel:

| [!DNL Azure Blob] | Verouderd | Nieuw |
|---------|----------|---------|
| Stroomspecificatie | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 752d422f-b16f-4f0d-b1c6-26e448e3b388 |
| Verbindingsspecificatie | e258278b-a4cf-43ac-b158-4fa0ca0d948b | 6d6b59bf-fb58-4107-9064-4d246c0e5bb2 |

Bekijk de volledige erfenis en de nieuwe basisverbinding en de voorbeelden van de doelverbinding voor [!DNL Azure Blob] in de onderstaande tabbladen. De parameters die worden vereist om basisverbindingen voor de bestemmingen van Azure Blob tot stand te brengen veranderen niet.

Op dezelfde manier zijn er geen achterwaarts-onverenigbare veranderingen in de parameters die worden vereist om doelverbindingen tot stand te brengen.

>[!BEGINTABS]

>[!TAB Verouderde basisverbinding en doelverbinding]

+++Verouderde weergave [!DNL base connection] for [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "azure-blob",
  "connectionSpec": {
    "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "ConnectionString",
    "params": {
      "authorizedDate": "2022-06-02",
      "connectionString": "<your-connection-string>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  }, 
  "version": "\"d000d23c-0000-0200-0000-6299051c0000\"",
  "etag": "\"d000d23c-0000-0200-0000-6299051c0000\""
}
```

+++

+++Verouderde weergave [!DNL target connection] for [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="13"}
{
  ...
  "name": "v1",
  "description": "v2",
  "baseConnectionId": "d10fcecf-9963-4062-820c-0f878be98805",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
    "version": "1.0"
  },
  "params": {
    "mode": "AZURE_BLOB",
    "container": "usdasda",
    "path": "v3"
  },
  "version": "\"cb0468ba-0000-0200-0000-631ab0790000\"",
  "etag": "\"cb0468ba-0000-0200-0000-631ab0790000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "d10fcecf-9963-4062-820c-0f878be98805",
      "connectionSpec": {
        "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!TAB Nieuwe basisverbinding en doelverbinding]

+++Nieuwe weergave [!DNL base connection] for [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "Azure Blob Storage",
  "connectionSpec": {
    "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "ConnectionString",
    "params": {
      "authorizedDate": "2022-06-02",      
      "connectionString": "<your-connection-string>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"4008a892-0000-0200-0000-6389890d0000\"",
  "etag": "\"4008a892-0000-0200-0000-6389890d0000\""
}
```

+++

+++Nieuwe weergave [!DNL target connection] for [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="13, 17-25"}
{
  ...
  "name": "v1",
  "description": "v2",
  "baseConnectionId": "1329d183-a3ee-4454-ab3f-e2388082bf29",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
    "version": "1.0"
  },
  "params": {
    "csvOptions": {
      "nullValue": "null",
      "emptyValue": "",
      "escape": "\\",
      "quote": "",
      "delimiter": ","
    },
    "compression": "NONE",
    "fileType": "CSV",
    "mode": "Server-to-server",
    "container": "usdasda",
    "path": "v3"
  },
  "version": "\"5509fe3f-0000-0200-0000-638a28880000\"",
  "etag": "\"5509fe3f-0000-0200-0000-638a28880000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "1329d183-a3ee-4454-ab3f-e2388082bf29",
      "connectionSpec": {
        "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!ENDTABS]

### Achterwaarts incompatibele veranderingen in bestemming SFTP {#changes-sftp-destination}

De achterwaarts incompatibele wijzigingen voor de API-gebruikers worden bijgewerkt `connection spec ID` en `flow spec ID` zoals weergegeven in onderstaande tabel:

| SFTP | Verouderd | Nieuw |
|---------|----------|---------|
| Stroomspecificatie | 71471eba-b620-49e4-90fd-23f1fa0174d8 | fd36aaa4-bf2b-43fb-9387-43785eeeb799 |
| Verbindingsspecificatie | 64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0 | 36965a81-b1c6-401b-99f8-22508f1e6a26 |

Naast de bijgewerkte stroom en verbindingsspecificatie hierboven, zijn er veranderingen in de parameters die worden vereist wanneer het creëren van SFTP basisverbindingen.

* Eerder was voor de basisverbinding voor SFTP-doelen een `host` parameter. De naam van deze parameter is gewijzigd in `domain`.

Bekijk de volledige erfenis en nieuwe basisverbinding en de voorbeelden van de doelverbinding voor SFTP in de hieronder lusjes, met de lijnen die veranderen benadrukt. De parameters die worden vereist om doelverbindingen voor bestemmingen tot stand te brengen SFTP veranderen niet.

>[!BEGINTABS]

>[!TAB Verouderde basisverbinding en doelverbinding]

+++Verouderde weergave [!DNL base connection] voor SFTP - wachtwoordverificatie

```json {line-numbers="true" start-line="1" highlight="5,15"}
{
  ...
  "name": "sftp",
  "connectionSpec": {
    "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Basic Authentication for sftp",
    "params": {
      "authorizedDate": "2022-06-02",
      "password": "<your-password>",
      "userName": "DPID12345",
      "host": "ftp-out.demdex.com"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"d000013c-0000-0200-0000-629903bd0000\"",
  "etag": "\"d000013c-0000-0200-0000-629903bd0000\""
}
```

+++

+++Verouderde weergave [!DNL base connection] for [!DNL SFTP - SSH key] verificatie

```json {line-numbers="true" start-line="1" highlight="5,15"}
{
  ...
  "name": "sftp",
  "connectionSpec": {
    "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Basic Authentication for sftp",
    "params": {
      "authorizedDate": "2022-06-02",
      "sshKey": "<your-ssh-key>",
      "userName": "DPID12345",
      "port": 22
      "domain": "ftp-out.demdex.com"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"d000013c-0000-0200-0000-629903bd0000\"",
  "etag": "\"d000013c-0000-0200-0000-629903bd0000\""
}
```

+++

+++Verouderde weergave [!DNL target connection] voor SFTP

```json {line-numbers="true" start-line="1" highlight="13"}
{
  ...
  "name": "test sftp 6/2",
  "description": "",
  "baseConnectionId": "e6f3a300-0bf7-4755-b7f8-308dc2a99133",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
    "version": "1.0"
  },
  "params": {
    "mode": "FTP",
    "remotePath": "test"
  },
  "version": "\"8503ab91-0000-0200-0000-629903ce0000\"",
  "etag": "\"8503ab91-0000-0200-0000-629903ce0000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "e6f3a300-0bf7-4755-b7f8-308dc2a99133",
      "connectionSpec": {
        "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!TAB Nieuwe basisverbinding en doelverbinding]

+++Nieuwe weergave [!DNL base connection] for [!DNL SFTP - password authentication]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "SFTP",
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "SFTP with Password",
    "params": {
      "authorizedDate": "2022-06-02",
      "domain": "ftp-out.demdex.com",
      "username": "DPID12345",
      "password": "<your-password>",
      "port": 22      
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"420826cc-0000-0200-0000-638999a60000\"",
  "etag": "\"420826cc-0000-0200-0000-638999a60000\""
}
```

+++

+++Nieuwe weergave [!DNL base connection] for [!DNL SFTP - SSH key] verificatie

```json {line-numbers="true" start-line="1" highlight="5,12"}
{
  ...
  "name": "SFTP",
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Basic Authentication for sftp",
    "params": {
      "authorizedDate": "2022-06-02",
      "domain": "ftp-out.demdex.com",
      "username": "DPID12345",
      "sshKey": "<your-ssh-key>",
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"420826cc-0000-0200-0000-638999a60000\"",
  "etag": "\"420826cc-0000-0200-0000-638999a60000\""
}
```

+++

+++Nieuwe weergave [!DNL target connection] voor SFTP

```json {line-numbers="true" start-line="1" highlight="13, 17-25"}
{
  ...
  "name": "test sftp 6/2",
  "description": "",
  "baseConnectionId": "af63fbe1-45ff-4722-a9de-fbbe789dc7b0",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
    "version": "1.0"
  },
  "params": {
    "csvOptions": {
      "nullValue": "null",
      "emptyValue": "",
      "escape": "\\",
      "quote": "",
      "delimiter": ","
    },
    "compression": "NONE",
    "fileType": "CSV",
    "mode": "FTP",
    "remotePath": "test"
  },
  "version": "\"5509b5cf-0000-0200-0000-638a2ab60000\"",
  "etag": "\"5509b5cf-0000-0200-0000-638a2ab60000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "af63fbe1-45ff-4722-a9de-fbbe789dc7b0",
      "connectionSpec": {
        "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!ENDTABS]

### Met achterwaartse incompatibele wijzigingen die worden toegepast op [!DNL Amazon S3], [!DNL Azure Blob]en SFTP-doelen {#changes-all-destinations}

De stap van de profielkiezer in alle drie de bestemmingen wordt vervangen door een toewijzingsstap die u toestaat om de kolomkopballen in uw uitgevoerde dossiers anders te noemen, indien gewenst. Zie de afbeelding naast elkaar met de oude kenmerkenkiezer links en de nieuwe toewijzingsstap rechts.

![Overzicht van migratiegids](/help/destinations/assets/api/api-migration-guide/old-and-new-mapping-step.png)

Let op het volgende `profileSelectors` object in de oudere voorbeelden wordt vervangen door de nieuwe `profileMapping` object.

Volledige informatie over het instellen van de `profileMapping` object in het [API-zelfstudie voor het exporteren van gegevens naar cloudopslagdoelen](/help/destinations/api/activate-segments-file-based-destinations.md#attribute-and-identity-mapping).

>[!BEGINTABS]

>[!TAB Oude transformatieparameters]

+++Een voorbeeld van oude transformatieparameters weergeven

```json{line-numbers="true" start-line="1" highlight="4-40, 45-53"}
{
  "segmentSelectors": { // shortened for brevity since nothing changes in the segment selectors
  },  
  "profileSelectors": {
    "selectors": [
      {
        "type": "JSON_PATH",
        "value": {
          "path": "CORE",
          "operator": "EXISTS",
          "mapping": {
            "sourceType": "text/x.schema-path",
            "source": "CORE",
            "destination": "CORE",
            "identity": false,
            "primaryIdentity": false,
            "functionVersion": 0,
            "sourceAttribute": "CORE",
            "destinationXdmPath": "CORE"
          },
          "identity": {
            "namespace": "CORE"
          }
        }
      },
      ...
      {
        "type": "JSON_PATH",
        "value": {
          "path": "segmentMembership.status",
          "operator": "EXISTS",
          "mapping": {
            "sourceType": "text/x.schema-path",
            "source": "segmentMembership.status",
            "destination": "segmentMembership.status",
            "identity": false,
            "primaryIdentity": false,
            "functionVersion": 0,
            "sourceAttribute": "segmentMembership.status",
            "destinationXdmPath": "segmentMembership.status"
          }
        }
      }
    ],
    "mandatoryFields": [
      "CORE",
      "person.name.lastName",
      "personalEmail.address"
    ],
    "primaryFields": [
      {
        "identityNamespace": "CORE",
        "fieldType": "IDENTITY"
      }
    ]
  }
}
```

+++

>[!TAB Nieuwe transformatieparameters]

+++Bekijk een voorbeeld van transformatieparameters na de migratie

In het onderstaande configuratievoorbeeld ziet u hoe `profileSelectors` velden zijn vervangen door een `profileMapping` object.

```json {line-numbers="true" start-line="1" highlight="4-12, 18-20"}
{
  "segmentSelectors": { // shortened for brevity since nothing changes in the segment selectors
  },  
  "mandatoryFields": [
    "CORE",
    "person_name_lastName",
    "personalEmail_address"
  ],
  "primaryFields": [
    {
      "identityNamespace": "CORE",
      "fieldType": "IDENTITY"
    }
  ],
  "identityMapping": {
    "mappings": []
  },
  "profileMapping": {
    "mappingId": "40dfd952fe09498ba65145c7a5de3e07",
    "mappingVersion": 0
  },
  "attributeMapping": {}
}
```

+++

>[!ENDTABS]

## Tijdlijn en actiepunten voor migratie {#timeline-and-action-items}

De migratie van erfenisgegevens stroomt naar de nieuwe doelkaarten voor [!DNL Amazon S3], [!DNL Azure Blob]en SFTP-doelen worden uitgevoerd zodra uw organisatie gereed is om te migreren en niet later dan **26 juli 2023**.

U ontvangt herinneringse-mails van Adobe wanneer de migratiedatum nadert. Lees ter voorbereiding de sectie Actie-items hieronder om u voor te bereiden op de migratie.

### Actiepunten {#action-items}

Ter voorbereiding van de migratie van [!DNL Amazon S3], [!DNL Azure Blob]en SFTP-cloudopslagdoelen naar de nieuwe kaarten. Bereid u voor om uw scripts en geautomatiseerde API-aanroepen bij te werken, zoals hieronder wordt voorgesteld.

1. Werk om het even welke manuscripten of geautomatiseerde API vraag voor om het even welk bestaand bij [!DNL Amazon S3], [!DNL Azure Blob], of SFTP-cloudopslagdoelen uiterlijk 26 juli 2023. Alle geautomatiseerde API-aanroepen of scripts die gebruikmaken van de verouderde verbindingsspecificaties of flowspecificaties, moeten worden bijgewerkt naar de nieuwe verbindingsspecificaties of stroomspecificaties.
2. Neem contact op met uw Adobe-accountvertegenwoordiger wanneer uw scripts vóór 26 juli zijn bijgewerkt.
3. De `targetConnectionSpecId` kan als vlag worden gebruikt om te bepalen als dataflow aan de nieuwe bestemmingskaart is gemigreerd. U kunt uw scripts bijwerken met een `if` voorwaarde om de erfenis en bijgewerkte specificaties van de doelverbinding in te zien `flow.inheritedAttributes.targetConnections[0].connectionSpec.id` en bepalen of uw gegevensstroom is gemigreerd. U kunt de verouderde en nieuwe verbindingsspecificaties-id&#39;s zien in de specifieke secties op deze pagina voor elke bestemming.
4. Uw Adobe-accountteam zal u meer informatie geven over wanneer uw gegevensstromen worden gemigreerd.
5. Na 26 juli worden alle gegevensstromen gemigreerd. Al uw bestaande gegevensstromen zullen nu nieuwe stroomentiteiten (verbindingsspecificaties, stroom specs, basisverbindingen, en doelverbindingen) hebben. Om het even welke manuscripten of API vraag aan uw kant die de erfenisstroomentiteiten gebruiken zal ophouden werkend.

## Andere migratieoverwegingen {#other-considerations}

Houd er rekening mee dat er geen invloed is op uw bestaande exportschema tijdens of na de migratie.

## Volgende stappen {#next-steps}

Door deze pagina te lezen, weet u nu of u actie moet ondernemen ter voorbereiding op de migratie van de bestemmingen van de cloudopslag. U weet ook welke documentatiepagina&#39;s u wilt raadplegen wanneer u API-workflows instelt om bestanden vanuit het Experience Platform te exporteren naar de voorkeursopslaglocaties van de cloud. Vervolgens kunt u de API-zelfstudie bekijken op [gegevens exporteren naar cloudopslagbestemmingen](/help/destinations/api/activate-segments-file-based-destinations.md).
