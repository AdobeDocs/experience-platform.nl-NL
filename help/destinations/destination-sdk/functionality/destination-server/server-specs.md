---
description: Leer hoe te om de specificaties van de bestemmingsserver in Adobe Experience Platform Destination SDK via ` te vormen/creatie/bestemming-servers' eindpunt.
title: Server specs voor bestemmingen die met Destination SDK worden gecreeerd
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '2750'
ht-degree: 2%

---


# Server specs voor bestemmingen die met Destination SDK worden gecreeerd

De serverspecificaties van de bestemming bepalen het type van bestemmingsplatform dat de gegevens van Adobe Experience Platform, en de communicatie parameters tussen Platform en uw bestemming zal ontvangen. Bijvoorbeeld:

* A [streaming](#streaming-example) De specificatie van de bestemmingsserver bepaalt het de servereindpunt van HTTP dat de berichten van HTTP van Platform zal ontvangen. Leren om te vormen hoe de vraag van HTTP aan het eindpunt geformatteerd is, lees [sjabloonspecificaties](templating-specs.md) pagina.
* An [Amazon S3](#s3-example) de specificatie van de doelserver bepaalt [!DNL S3] De naam van de emmer en de weg waar het Platform de dossiers zal uitvoeren.
* An [SFTP](#sftp-example) De specificaties van de bestemmingsserver bepalen de gastheernaam, de wortelfolder, de communicatie haven, en het encryptietype van de server SFTP waar het Platform de dossiers zal uitvoeren.

Om te begrijpen waar deze component in een integratie past die met Destination SDK wordt gecreeerd, zie het diagram in [configuratieopties](../configuration-options.md) documentatie of zie de volgende pagina&#39;s van het overzicht van bestemmingsconfiguratie:

* [Gebruik Destination SDK om een streamingbestemming te configureren](../../guides/configure-destination-instructions.md#create-server-template-configuratiom)
* [Gebruik Destination SDK om een op een bestand gebaseerde bestemming te configureren](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)

U kunt de specificaties van de doelserver configureren via de `/authoring/destination-servers` eindpunt. Zie de volgende API verwijzingspagina&#39;s voor gedetailleerde API vraagvoorbeelden waar u de componenten kunt vormen die in deze pagina worden getoond.

* [Een doelserverconfiguratie maken](../../authoring-api/destination-server/create-destination-server.md)
* [Een doelserverconfiguratie bijwerken](../../authoring-api/destination-server/update-destination-server.md)

Deze pagina toont alle types van bestemmingsserver die door Destination SDK, met al hun configuratieparameters worden gesteund. Vervang bij het maken van uw bestemming de parameterwaarden door uw eigen waarden.

>[!IMPORTANT]
>
>Alle parameternamen en -waarden die door Destination SDK worden ondersteund, zijn **hoofdlettergevoelig**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Ondersteunde integratietypen {#supported-integration-types}

Raadpleeg de onderstaande tabel voor meer informatie over de integratietypen die de op deze pagina beschreven functionaliteit ondersteunen.

| Type integratie | Ondersteunt functionaliteit |
|---|---|
| Integraties in realtime (streaming) | Ja |
| Op bestanden gebaseerde (batch) integratie | Ja |

Wanneer [maken](../../authoring-api/destination-server/create-destination-server.md) of [bijwerken](../../authoring-api/destination-server/update-destination-server.md) Als bestemmingsserver, gebruik één van de configuraties van het servertype die in deze pagina worden beschreven. Afhankelijk van uw integratievereisten, zorg ervoor om de waarden van de steekproefparameter van deze voorbeelden met uw te vervangen.

## Velden met harde code en gematigde velden {#templatized-fields}

Wanneer het creëren van een bestemmingsserver door Destination SDK, kunt u configuratieparameterwaarden of door hard-coderen hen in de configuratie, of door templatized gebieden te gebruiken bepalen. Met sjabloonvelden kunt u door de gebruiker opgegeven waarden lezen vanuit de gebruikersinterface van het Platform.

Doelserverparameters hebben twee configureerbare velden. Deze opties bepalen of u hard-gecodeerde of templatized waarden gebruikt.

| Parameter | Type | Beschrijving |
|---|---|---|
| `templatingStrategy` | Tekenreeks | *Vereist.* Hiermee wordt bepaald of er een waarde met harde code wordt opgegeven via het dialoogvenster `value` of een door de gebruiker instelbare waarde in de gebruikersinterface. Ondersteunde waarden: <ul><li>`NONE`: Gebruik deze waarde wanneer u de parameterwaarde via de `value` parameter (zie de volgende rij). Voorbeeld:`"value": "my-storage-bucket"`.</li><li>`PEBBLE_V1`: Gebruik deze waarde als u wilt dat uw gebruikers een parameterwaarde opgeven in de gebruikersinterface. Voorbeeld: `"value": "{{customerData.bucket}}"`. </li></ul> |
| `value` | Tekenreeks | *Vereist*. Definieert de parameterwaarde. Ondersteunde waardetypen: <ul><li>**Waarde met harde code**: Een hard-gecodeerde waarde gebruiken (zoals `"value": "my-storage-bucket"`) wanneer u niet wilt dat gebruikers een parameterwaarde in de gebruikersinterface invoeren. Bij hard coderen van een waarde `templatingStrategy` moet altijd worden ingesteld op `NONE`.</li><li>**Sjabloonwaarde**: Gebruik een getemplatificeerde waarde (zoals `"value": "{{customerData.bucket}}"`) als u wilt dat de gebruikers een parameterwaarde opgeven in de gebruikersinterface. Bij gebruik van getemplatificeerde waarden `templatingStrategy` moet altijd worden ingesteld op `PEBBLE_V1`.</li></ul> |

{style="table-layout:auto"}

### Wanneer moet u hard-gecodeerde en getemplatificeerde velden gebruiken?

Zowel hard-gecodeerde als templatized gebieden hebben hun eigen gebruik in Destination SDK, afhankelijk van welk type van integratie u creeert.

**Verbinding maken met uw bestemming zonder gebruikersinvoer**

Wanneer gebruikers [verbinden met uw bestemming](../../../ui/connect-destination.md) in Platform UI, zou u het proces van de bestemmingsverbinding zonder hun input kunnen willen behandelen.

Hiervoor kunt u de verbindingsparameters van het doelplatform hard coderen in de serverspecificatie. Wanneer u hard-gecodeerde parameterwaarden in uw configuratie van de bestemmingsserver gebruikt, wordt de verbinding tussen Adobe Experience Platform en uw bestemmingsplatform behandeld zonder enige input van de gebruiker.

In het voorbeeld hieronder, leidt een partner tot een Gegevens Landing Zone bestemmingsserver met `path.value` veld dat hardcoded is.

```json
{
   "name":"Data Landing Zone destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"NONE",
         "value":"Your/hardcoded/path/here"
      },
      "useCase": "Your use case"
   }
}
```

Dit betekent dat wanneer gebruikers de [zelfstudie over doelverbinding](../../../ui/connect-destination.md), zullen zij geen [verificatiestap](../../../ui/connect-destination.md#authenticate). In plaats daarvan wordt de verificatie door het Platform afgehandeld, zoals in de onderstaande afbeelding wordt getoond.

![Een afbeelding van de ui die het authentificatiescherm tussen Platform en een bestemming DLZ toont.](../../assets/functionality/destination-server/server-spec-hardcoded.png)

**Verbinding maken met uw bestemming met gebruikersinvoer**

Wanneer de verbinding tussen Platform en uw bestemming na een specifieke gebruikersinput in het Platform UI zou moeten worden gevestigd, zoals het selecteren van een API eindpunt of het verstrekken van een gebiedswaarde, kunt u getemplatificeerde gebieden in de serverspecificatie gebruiken om de gebruikersinput te lezen en met uw bestemmingsplatform te verbinden.

In het onderstaande voorbeeld maakt een partner een [real-time (streaming)](#streaming-example) integratie en de `url.value` veld gebruikt getemplatificeerde parameter `{{customerData.region}}` om een deel van het API eindpunt te personaliseren dat op gebruikersinput wordt gebaseerd.

```json
{
   "name":"Templatized API endpoint example",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.yourcompany.com/data/{{customerData.region}}/items"
      }
   }
}
```

Als u gebruikers de mogelijkheid wilt geven een waarde te selecteren in de gebruikersinterface van het Platform, kunt u de `region` moet ook in de [doelconfiguratie](../../authoring-api/destination-configuration/create-destination-configuration.md) als gegevensveld voor klanten, zoals hieronder wordt getoond:

```json
"customerDataFields":[
   {
      "name":"region",
      "title":"Region",
      "description":"Select an option",
      "type":"string",
      "isRequired":true,
      "readOnly":false,
      "enum":[
         "US",
         "EU"
      ]
   }
```

Dit betekent dat wanneer gebruikers de [zelfstudie over doelverbinding](../../../ui/connect-destination.md), moeten ze een gebied selecteren voordat ze verbinding kunnen maken met het doelplatform. Wanneer ze verbinding maken met het doel, wordt het sjabloonveld `{{customerData.region}}` wordt vervangen door de waarde die de gebruiker in de gebruikersinterface heeft geselecteerd, zoals wordt weergegeven in de onderstaande afbeelding.

![UI-afbeelding die het scherm van de doelverbinding weergeeft met een regiokiezer.](../../assets/functionality/destination-server/server-spec-template-region.png)

## Doelserver in realtime (streaming) {#streaming-example}

Met dit type doelserver kunt u gegevens vanuit Adobe Experience Platform naar uw bestemming exporteren via HTTP-aanvragen. De serverconfiguratie bevat informatie over de server die de berichten ontvangt (de server aan uw kant).

Dit proces levert gebruikersgegevens als reeks berichten van HTTP aan uw bestemmingsplatform. De onderstaande parameters vormen de HTTP-serverspectsjabloon.

Het voorbeeld hieronder toont een voorbeeld van een configuratie van de bestemmingsserver voor een (het stromen) bestemming in real time.

```json
{
   "name":"Your destination server name",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{YOUR_API_ENDPOINT}"
      }
   }
}
```

| Parameter | Type | Beschrijving |
|---|---|---|
| `name` | Tekenreeks | *Vereist.* Vertegenwoordigt een vriendschappelijke naam van uw server, zichtbaar slechts aan Adobe. Deze naam is niet zichtbaar aan partners of klanten. Voorbeeld: `Moviestar destination server`. |
| `destinationServerType` | Tekenreeks | *Vereist.* Stel deze in op `URL_BASED` voor streamingdoelen. |
| `templatingStrategy` | Tekenreeks | *Vereist.* <ul><li>Gebruiken `PEBBLE_V1` als u een sjabloonveld gebruikt in plaats van een hard gecodeerde waarde in het dialoogvenster `value` veld. Gebruik deze optie als u een eindpunt als: `https://api.moviestar.com/data/{{customerData.region}}/items`, waar de gebruikers het eindpuntgebied van het Platform UI moeten selecteren. </li><li> Gebruiken `NONE` als er aan de Adobe zijde geen getemplatificeerde transformatie nodig is, bijvoorbeeld als u een eindpunt hebt, zoals: `https://api.moviestar.com/data/items` </li></ul> |
| `value` | Tekenreeks | *Vereist.* Vul het adres van het API eindpunt in dat Experience Platform zou moeten verbinden met. |

{style="table-layout:auto"}

## [!DNL Amazon S3] doelserver {#s3-example}

Met deze doelserver kunt u bestanden met Adobe Experience Platform-gegevens exporteren naar uw Amazon S3-opslagruimte.

Het voorbeeld hieronder toont een voorbeeld van een configuratie van de bestemmingsserver voor een bestemming van Amazon S3.

```json
{
   "name":"Amazon S3 destination",
   "destinationServerType":"FILE_BASED_S3",
   "fileBasedS3Destination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
}
```

| Parameter | Type | Beschrijving |
|---|---|---|
| `name` | Tekenreeks | De naam van uw doelserver. |
| `destinationServerType` | Tekenreeks | Stel deze waarde in op basis van het doelplatform. Bestanden exporteren naar een [!DNL Amazon S3] emmertje, deze instellen op `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | Tekenreeks | *Vereist*. Stel deze waarde in op basis van het type waarde dat wordt gebruikt in het dialoogvenster `bucket.value` veld.<ul><li>Als u wilt dat uw gebruikers hun eigen emmernaam invoeren in de gebruikersinterface van het Experience Platform, stelt u deze waarde in op `PEBBLE_V1`. In dit geval moet u de opdracht `value` veld voor het lezen van een waarde uit het deelvenster [klantgegevensvelden](../destination-configuration/customer-data-fields.md) ingevuld door de gebruiker. Dit gebruiksgeval wordt in het bovenstaande voorbeeld getoond.</li><li>Als u een hard-gecodeerde emmernaam voor uw integratie gebruikt, zoals `"bucket.value":"MyBucket"`Stel deze waarde vervolgens in op `NONE`.</li></ul> |
| `fileBasedS3Destination.bucket.value` | Tekenreeks | De naam van de [!DNL Amazon S3] emmer die door deze bestemming moet worden gebruikt. Dit kan een getemplativeerd veld zijn dat de waarde van het veld [klantgegevensvelden](../destination-configuration/customer-data-fields.md) ingevuld door de gebruiker (zoals in het bovenstaande voorbeeld) of een hard gecodeerde waarde, zoals `"value":"MyBucket"`. |
| `fileBasedS3Destination.path.templatingStrategy` | Tekenreeks | *Vereist*. Stel deze waarde in op basis van het type waarde dat wordt gebruikt in het dialoogvenster `path.value` veld.<ul><li>Als u wilt dat uw gebruikers hun eigen pad invoeren in de gebruikersinterface van het Experience Platform, stelt u deze waarde in op `PEBBLE_V1`. In dit geval moet u de opdracht `path.value` veld voor het lezen van een waarde uit het deelvenster [klantgegevensvelden](../destination-configuration/customer-data-fields.md) ingevuld door de gebruiker. Dit gebruiksgeval wordt in het bovenstaande voorbeeld getoond.</li><li>Als u een hard-gecodeerd weg voor uw integratie gebruikt, zoals `"bucket.value":"/path/to/MyBucket"`Stel deze waarde vervolgens in op `NONE`.</li></ul> |
| `fileBasedS3Destination.path.value` | Tekenreeks | Het pad naar de [!DNL Amazon S3] emmer die door deze bestemming moet worden gebruikt. Dit kan een getemplativeerd veld zijn dat de waarde van het veld [klantgegevensvelden](../destination-configuration/customer-data-fields.md) ingevuld door de gebruiker (zoals in het bovenstaande voorbeeld) of een hard gecodeerde waarde, zoals `"value":"/path/to/MyBucket"`. |

{style="table-layout:auto"}

## [!DNL SFTP] doelserver {#sftp-example}

Met deze doelserver kunt u bestanden met Adobe Experience Platform-gegevens exporteren naar uw [!DNL SFTP] opslagserver.

Het voorbeeld hieronder toont een voorbeeld van een configuratie van de bestemmingsserver voor een bestemming SFTP.

```json
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
      "port":22,
      "encryptionMode":"PGP"
   }
}
```

| Parameter | Type | Beschrijving |
|---|---|---|
| `name` | Tekenreeks | De naam van uw doelserver. |
| `destinationServerType` | Tekenreeks | Stel deze waarde in op basis van het doelplatform. Bestanden exporteren naar een [!DNL SFTP] doel, deze instellen op `FILE_BASED_SFTP`. |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | Tekenreeks | *Vereist*. Stel deze waarde in op basis van het type waarde dat wordt gebruikt in het dialoogvenster `rootDirectory.value` veld.<ul><li>Als u wilt dat uw gebruikers hun eigen pad naar de hoofdmap invoeren in de gebruikersinterface van het Experience Platform, stelt u deze waarde in op `PEBBLE_V1`. In dit geval moet u de opdracht `rootDirectory.value` veld voor het lezen van een door de gebruiker opgegeven waarde uit het dialoogvenster [klantgegevensvelden](../destination-configuration/customer-data-fields.md) ingevuld door de gebruiker. Dit gebruiksgeval wordt in het bovenstaande voorbeeld getoond.</li><li>Als u een hard-gecodeerd weg van de wortelfolder voor uw integratie gebruikt, zoals `"rootDirectory.value":"Storage/MyDirectory"`Stel deze waarde vervolgens in op `NONE`.</li></ul> |
| `fileBasedSFTPDestination.rootDirectory.value` | Tekenreeks | Het pad naar de map die de geëxporteerde bestanden host. Dit kan een getemplativeerd veld zijn dat de waarde van het veld [klantgegevensvelden](../destination-configuration/customer-data-fields.md) ingevuld door de gebruiker (zoals in het bovenstaande voorbeeld) of een hard gecodeerde waarde, zoals `"value":"Storage/MyDirectory"` |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | Tekenreeks | *Vereist*. Stel deze waarde in op basis van het type waarde dat wordt gebruikt in het dialoogvenster `hostName.value` veld.<ul><li>Als u wilt dat uw gebruikers hun eigen hostnaam invoeren in de gebruikersinterface van het Experience Platform, stelt u deze waarde in op `PEBBLE_V1`. In dit geval moet u de opdracht `hostName.value` veld voor het lezen van een door de gebruiker opgegeven waarde uit het dialoogvenster [klantgegevensvelden](../destination-configuration/customer-data-fields.md) ingevuld door de gebruiker. Dit gebruiksgeval wordt in het bovenstaande voorbeeld getoond.</li><li>Als u een hard-gecodeerde gastheernaam voor uw integratie gebruikt, zoals `"hostName.value":"my.hostname.com"`Stel deze waarde vervolgens in op `NONE`.</li></ul> |
| `fileBasedSFTPDestination.hostName.value` | Tekenreeks | De hostnaam van uw SFTP-server. Dit kan een getemplativeerd veld zijn dat de waarde van het veld [klantgegevensvelden](../destination-configuration/customer-data-fields.md) ingevuld door de gebruiker (zoals in het bovenstaande voorbeeld) of een hard gecodeerde waarde, zoals `"hostName.value":"my.hostname.com"`. |
| `port` | Geheel | De SFTP-serverpoort. |
| `encryptionMode` | Tekenreeks | Geeft aan of bestandsversleuteling moet worden gebruikt. Ondersteunde waarden: <ul><li>PGP</li><li>Geen</li></ul> |

{style="table-layout:auto"}

## [!DNL Azure Data Lake Storage] ([!DNL ADLS]) doelserver {#adls-example}

Met deze doelserver kunt u bestanden met Adobe Experience Platform-gegevens exporteren naar uw [!DNL Azure Data Lake Storage] account.

Het voorbeeld hieronder toont een voorbeeld van een configuratie van de bestemmingsserver voor een [!DNL Azure Data Lake Storage] bestemming.

```json
{
   "name":"ADLS destination server",
   "destinationServerType":"FILE_BASED_ADLS_GEN2",
   "fileBasedAdlsGen2Destination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
}
```

| Parameter | Type | Beschrijving |
|---|---|---|
| `name` | Tekenreeks | De naam van de doelverbinding. |
| `destinationServerType` | Tekenreeks | Stel deze waarde in op basis van het doelplatform. Voor [!DNL Azure Data Lake Storage] doelen, stel deze in op `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Tekenreeks | *Vereist*. Stel deze waarde in op basis van het type waarde dat wordt gebruikt in het dialoogvenster `path.value` veld.<ul><li>Als u wilt dat de gebruikers hun [!DNL ADLS] mappad in de gebruikersinterface van het Experience Platform, stel deze waarde in op `PEBBLE_V1`. In dit geval moet u de opdracht `path.value` veld voor het lezen van een waarde uit het dialoogvenster [klantgegevensvelden](../destination-configuration/customer-data-fields.md) ingevuld door de gebruiker. Dit gebruiksgeval wordt in het bovenstaande voorbeeld getoond.</li><li>Als u een hard-gecodeerd weg voor uw integratie gebruikt, zoals `"abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/"`Stel deze waarde vervolgens in op `NONE`.</li></ul> |
| `fileBasedAdlsGen2Destination.path.value` | Tekenreeks | Het pad naar uw [!DNL ADLS] opslagmap. Dit kan een getemplativeerd veld zijn dat de waarde van het veld [klantgegevensvelden](../destination-configuration/customer-data-fields.md) ingevuld door de gebruiker (zoals in het bovenstaande voorbeeld) of een hard gecodeerde waarde, zoals `abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/`. |

{style="table-layout:auto"}

## [!DNL Azure Blob Storage] doelserver {#blob-example}

Met deze doelserver kunt u bestanden met Adobe Experience Platform-gegevens exporteren naar uw [!DNL Azure Blob Storage] container.

Het voorbeeld hieronder toont een voorbeeld van een configuratie van de bestemmingsserver voor een [!DNL Azure Blob Storage] bestemming.

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
   }
}
```

| Parameter | Type | Beschrijving |
|---|---|---|
| `name` | Tekenreeks | De naam van de doelverbinding. |
| `destinationServerType` | Tekenreeks | Stel deze waarde in op basis van het doelplatform. Voor [!DNL Azure Blob Storage] doelen, stel deze in op `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | Tekenreeks | *Vereist*. Stel deze waarde in op basis van het type waarde dat wordt gebruikt in het dialoogvenster `path.value` veld.<ul><li>Als u wilt dat uw gebruikers hun eigen gegevens invoeren [!DNL Azure Blob] [URI opslagaccount](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) in de interface van het Experience Platform stelt u deze waarde in op `PEBBLE_V1`. In dit geval moet u de opdracht `path.value` te lezen uit het veld [klantgegevensvelden](../destination-configuration/customer-data-fields.md) ingevuld door de gebruiker. Dit gebruiksgeval wordt in het bovenstaande voorbeeld getoond.</li><li>Als u een hard-gecodeerd weg voor uw integratie gebruikt, zoals `"path.value": "https://myaccount.blob.core.windows.net/"`Stel deze waarde vervolgens in op `NONE`. |
| `fileBasedAzureBlobDestination.path.value` | Tekenreeks | Het pad naar uw [!DNL Azure Blob] opslag. Dit kan een getemplativeerd veld zijn dat de waarde van het veld [klantgegevensvelden](../destination-configuration/customer-data-fields.md) ingevuld door de gebruiker (zoals in het bovenstaande voorbeeld) of een hard gecodeerde waarde, zoals `https://myaccount.blob.core.windows.net/`. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | Tekenreeks | *Vereist*. Stel deze waarde in op basis van het type waarde dat wordt gebruikt in het dialoogvenster `container.value` veld.<ul><li>Als u wilt dat uw gebruikers hun eigen gegevens invoeren [!DNL Azure Blob] [containernaam](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) in de interface van het Experience Platform stelt u deze waarde in op `PEBBLE_V1`. In dit geval moet u de opdracht `container.value` te lezen uit het veld [klantgegevensvelden](../destination-configuration/customer-data-fields.md) ingevuld door de gebruiker. Dit gebruiksgeval wordt in het bovenstaande voorbeeld getoond.</li><li>Als u een hard-gecodeerde containernaam voor uw integratie gebruikt, zoals `"path.value: myContainer"`Stel deze waarde vervolgens in op `NONE`. |
| `fileBasedAzureBlobDestination.container.value` | Tekenreeks | De naam van de Azure Blob Storage-container die voor deze bestemming moet worden gebruikt. Dit kan een getemplativeerd veld zijn dat de waarde van het veld [klantgegevensvelden](../destination-configuration/customer-data-fields.md) ingevuld door de gebruiker (zoals in het bovenstaande voorbeeld) of een hard gecodeerde waarde, zoals `myContainer`. |

{style="table-layout:auto"}

## [!DNL Data Landing Zone] ([!DNL DLZ]) doelserver {#dlz-example}

Met deze doelserver kunt u bestanden met Platform-gegevens exporteren naar een [[!DNL Data Landing Zone]](../../../catalog/cloud-storage/data-landing-zone.md) opslag.

In het onderstaande voorbeeld ziet u een voorbeeld van een configuratie van een doelserver voor een [!DNL Data Landing Zone] ([!DNL DLZ]) bestemming.

```json
{
   "name":"Data Landing Zone destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "Your use case"
   }
}
```

| Parameter | Type | Beschrijving |
|---|---|---|
| `name` | Tekenreeks | De naam van de doelverbinding. |
| `destinationServerType` | Tekenreeks | Stel deze waarde in op basis van het doelplatform. Voor [!DNL Data Landing Zone] doelen, stel deze in op `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | Tekenreeks | *Vereist*. Stel deze waarde in op basis van het type waarde dat wordt gebruikt in het dialoogvenster `path.value` veld.<ul><li>Als u wilt dat uw gebruikers hun eigen gegevens invoeren [!DNL Data Landing Zone] -account in de gebruikersinterface van het Experience Platform. Stel deze waarde in op `PEBBLE_V1`. In dit geval moet u de opdracht `path.value` veld voor het lezen van een waarde uit het deelvenster [klantgegevensvelden](../destination-configuration/customer-data-fields.md) ingevuld door de gebruiker. Dit gebruiksgeval wordt in het bovenstaande voorbeeld getoond.</li><li>Als u een hard-gecodeerd weg voor uw integratie gebruikt, zoals `"path.value": "https://myaccount.blob.core.windows.net/"`Stel deze waarde vervolgens in op `NONE`. |
| `fileBasedDlzDestination.path.value` | Tekenreeks | Het pad naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen. |

{style="table-layout:auto"}

## [!DNL Google Cloud Storage] doelserver {#gcs-example}

Met deze doelserver kunt u bestanden met Platform-gegevens exporteren naar uw [!DNL Google Cloud Storage] account.

In het onderstaande voorbeeld ziet u een voorbeeld van een configuratie van een doelserver voor een [!DNL Google Cloud Storage] bestemming.

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
   }
}
```

| Parameter | Type | Beschrijving |
|---|---|---|
| `name` | Tekenreeks | De naam van de doelverbinding. |
| `destinationServerType` | Tekenreeks | Stel deze waarde in op basis van het doelplatform. Voor [!DNL Google Cloud Storage] doelen, stel deze in op `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | Tekenreeks | *Vereist*. Stel deze waarde in op basis van het type waarde dat wordt gebruikt in het dialoogvenster `bucket.value` veld.<ul><li>Als u wilt dat uw gebruikers hun eigen gegevens invoeren [!DNL Google Cloud Storage] bucketnaam in de gebruikersinterface van het Experience Platform, stel deze waarde in op `PEBBLE_V1`. In dit geval moet u de opdracht `bucket.value` veld voor het lezen van een waarde uit het dialoogvenster [klantgegevensvelden](../destination-configuration/customer-data-fields.md) ingevuld door de gebruiker. Dit gebruiksgeval wordt in het bovenstaande voorbeeld getoond.</li><li>Als u een hard-gecodeerde emmernaam voor uw integratie gebruikt, zoals `"bucket.value": "my-bucket"`Stel deze waarde vervolgens in op `NONE`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | Tekenreeks | De naam van de [!DNL Google Cloud Storage] emmer die door deze bestemming moet worden gebruikt. Dit kan een getemplativeerd veld zijn dat de waarde van het veld [klantgegevensvelden](../destination-configuration/customer-data-fields.md) ingevuld door de gebruiker (zoals in het bovenstaande voorbeeld) of een hard gecodeerde waarde, zoals `"value": "my-bucket"`. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | Tekenreeks | *Vereist*. Stel deze waarde in op basis van het type waarde dat wordt gebruikt in het dialoogvenster `path.value` veld.<ul><li>Als u wilt dat uw gebruikers hun eigen gegevens invoeren [!DNL Google Cloud Storage] emmerpad in de interface van het Experience Platform, stel deze waarde in op `PEBBLE_V1`. In dit geval moet u de opdracht `path.value` veld voor het lezen van een waarde uit het deelvenster [klantgegevensvelden](../destination-configuration/customer-data-fields.md) ingevuld door de gebruiker. Dit gebruiksgeval wordt in het bovenstaande voorbeeld getoond.</li><li>Als u een hard-gecodeerd weg voor uw integratie gebruikt, zoals `"path.value": "/path/to/my-bucket"`Stel deze waarde vervolgens in op `NONE`.</li></ul> |
| `fileBasedGoogleCloudStorageDestination.path.value` | Tekenreeks | Het pad naar de [!DNL Google Cloud Storage] map die door dit doel moet worden gebruikt. Dit kan een getemplativeerd veld zijn dat de waarde van het veld [klantgegevensvelden](../destination-configuration/customer-data-fields.md) ingevuld door de gebruiker (zoals in het bovenstaande voorbeeld) of een hard gecodeerde waarde, zoals `"value": "/path/to/my-bucket"`. |

{style="table-layout:auto"}

## Volgende stappen {#next-steps}

Na het lezen van dit artikel, zou u een beter inzicht in moeten hebben wat een specificatie van de bestemmingsserver is, en hoe u het kunt vormen.

Raadpleeg de volgende artikelen voor meer informatie over de andere componenten van de doelserver:

* [Sjabloonspecificaties](templating-specs.md)
* [Berichtindeling](message-format.md)
* [Configuratie bestandsindeling](file-formatting.md)
