---
description: Leer hoe te om specificaties van de bestemmingsserver in Adobe Experience Platform Destination SDK via &grave;/authoring/bestemmings-servers te vormen.
title: Serverspecificaties voor doelen die met Destination SDK zijn gemaakt
exl-id: 62202edb-a954-42ff-9772-863cea37a889
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2753'
ht-degree: 0%

---

# Serverspecificaties voor doelen die met Destination SDK zijn gemaakt

De serverspecificaties van de bestemming bepalen het type van bestemmingsplatform dat de gegevens van Adobe Experience Platform, en de communicatie parameters tussen Experience Platform en uw bestemming zal ontvangen. Bijvoorbeeld:

* A [&#x200B; het stromen &#x200B;](#streaming-example) specificatie van de bestemmingsserver bepaalt het de servereindpunt van HTTP dat de berichten van HTTP van Experience Platform zal ontvangen. Leren om te vormen hoe de vraag van HTTP aan het eindpunt wordt geformatteerd, lees de [&#x200B; het templating specs &#x200B;](templating-specs.md) pagina.
* Een [&#x200B; Amazon S3 &#x200B;](#s3-example) specificatie van de bestemmingsserver bepaalt de [!DNL S3] emmer naam en weg waar Experience Platform de dossiers zal uitvoeren.
* Een [&#x200B; SFTP &#x200B;](#sftp-example) specificatie van de bestemmingsserver bepaalt de gastheernaam, wortelfolder, communicatie haven, en encryptietype van de server SFTP waar Experience Platform de dossiers zal uitvoeren.

Om te begrijpen waar deze component in een integratie past die met Destination SDK wordt gecreeerd, zie het diagram in de [&#x200B; documentatie van configuratieopties &#x200B;](../configuration-options.md) of zie de volgende pagina&#39;s van het overzicht van bestemmingsconfiguratie:

* [Destination SDK gebruiken om een streamingbestemming te configureren](../../guides/configure-destination-instructions.md#create-server-template-configuratiom)
* [Destination SDK gebruiken om een bestandsgebaseerde bestemming te configureren](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)

U kunt de specificaties van de bestemmingsserver via het `/authoring/destination-servers` eindpunt vormen. Zie de volgende API verwijzingspagina&#39;s voor gedetailleerde API vraagvoorbeelden waar u de componenten kunt vormen die in deze pagina worden getoond.

* [Een doelserverconfiguratie maken](../../authoring-api/destination-server/create-destination-server.md)
* [Een doelserverconfiguratie bijwerken](../../authoring-api/destination-server/update-destination-server.md)

Op deze pagina worden alle typen doelservers weergegeven die door Destination SDK worden ondersteund, met alle bijbehorende configuratieparameters. Vervang bij het maken van uw bestemming de parameterwaarden door uw eigen waarden.

>[!IMPORTANT]
>
>Alle parameternamen en waarden die door Destination SDK worden gesteund zijn **gevoelig geval**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Ondersteunde integratietypen {#supported-integration-types}

Raadpleeg de onderstaande tabel voor meer informatie over de integratietypen die de op deze pagina beschreven functionaliteit ondersteunen.

| Type integratie | Ondersteunt functionaliteit |
|---|---|
| Integraties in realtime (streaming) | Ja |
| Op bestanden gebaseerde (batch) integratie | Ja |

Wanneer [&#x200B; creërend &#x200B;](../../authoring-api/destination-server/create-destination-server.md) of [&#x200B; het bijwerken &#x200B;](../../authoring-api/destination-server/update-destination-server.md) een bestemmingsserver, gebruik één van de configuraties van het servertype die in deze pagina worden beschreven. Afhankelijk van uw integratievereisten, zorg ervoor om de waarden van de steekproefparameter van deze voorbeelden met uw te vervangen.

## Velden met harde code en sjablonen {#templatized-fields}

Wanneer u een doelserver maakt via Destination SDK, kunt u configuratieparameterwaarden definiëren door deze hard te coderen in de configuratie of door gebruik te maken van sjabloonvelden. Met sjabloonvelden kunt u door de gebruiker opgegeven waarden lezen vanuit de gebruikersinterface van Experience Platform.

Doelserverparameters hebben twee configureerbare velden. Deze opties bepalen of u hard-gecodeerde of templatized waarden gebruikt.

| Parameter | Type | Beschrijving |
|---|---|---|
| `templatingStrategy` | String | *Vereist.* Bepaalt of er een hard-gecodeerde waarde via het `value` gebied, of een user-configurable waarde in UI wordt verstrekt. Ondersteunde waarden: <ul><li>`NONE`: gebruik deze waarde wanneer u de parameterwaarde via de parameter `value` hard codeert (zie de volgende rij). Voorbeeld:`"value": "my-storage-bucket"`.</li><li>`PEBBLE_V1`: gebruik deze waarde als u wilt dat de gebruikers een parameterwaarde opgeven in de gebruikersinterface. Voorbeeld: `"value": "{{customerData.bucket}}"` . </li></ul> |
| `value` | String | *Vereiste*. Definieert de parameterwaarde. Ondersteunde waardetypen <ul><li>**hard-gecodeerde waarde**: Gebruik een hard-gecodeerde waarde (zoals `"value": "my-storage-bucket"`) wanneer u geen gebruikers nodig hebt om een parameterwaarde in UI in te gaan. Wanneer een waarde hard wordt gecodeerd, moet `templatingStrategy` altijd worden ingesteld op `NONE` .</li><li>**Getemplates waarde**: Gebruik een getemplatificeerde waarde (zoals `"value": "{{customerData.bucket}}"`) wanneer u uw gebruikers een parameterwaarde in UI wilt verstrekken. Wanneer u getemplatificeerde waarden gebruikt, moet `templatingStrategy` altijd worden ingesteld op `PEBBLE_V1` .</li></ul> |

{style="table-layout:auto"}

### Wanneer moet u hard-gecodeerde en getemplatificeerde velden gebruiken?

Zowel hard-gecodeerde als templatized gebieden hebben hun eigen gebruik in Destination SDK, afhankelijk van welk type van integratie u creeert.

**het Verbinden met uw bestemming zonder gebruikersinput**

Wanneer de gebruikers [&#x200B; met uw bestemming &#x200B;](../../../ui/connect-destination.md) in Experience Platform UI verbinden, zou u het proces van de bestemmingsverbinding zonder hun input kunnen willen behandelen.

Hiervoor kunt u de verbindingsparameters van het doelplatform hard coderen in de serverspecificatie. Wanneer u hard-gecodeerde parameterwaarden in uw configuratie van de bestemmingsserver gebruikt, wordt de verbinding tussen Adobe Experience Platform en uw bestemmingsplatform behandeld zonder enige input van de gebruiker.

In het onderstaande voorbeeld maakt een partner een doelserver voor de landingszone van gegevens en het veld `path.value` wordt gecodeerd.

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

Dientengevolge, wanneer de gebruikers door het [&#x200B; leerprogramma van de bestemmingsverbinding &#x200B;](../../../ui/connect-destination.md) gaan, zullen zij geen [&#x200B; authentificatiestap &#x200B;](../../../ui/connect-destination.md#authenticate) zien. In plaats daarvan wordt de verificatie uitgevoerd door Experience Platform, zoals in de onderstaande afbeelding wordt getoond.

![&#x200B; beeld dat van Ui het authentificatiescherm tussen Experience Platform en een bestemming DLZ toont.](../../assets/functionality/destination-server/server-spec-hardcoded.png)

**Verbindend met uw bestemming met gebruikersinput**

Wanneer de verbinding tussen Experience Platform en uw bestemming na een specifieke gebruikersinput in Experience Platform UI zou moeten worden gevestigd, zoals het selecteren van een API eindpunt of het verstrekken van een gebiedswaarde, kunt u getemplatificeerde gebieden in de serverspecificatie gebruiken om de gebruikersinput te lezen en met uw bestemmingsplatform te verbinden.

In het voorbeeld hieronder, leidt een partner tot a [&#x200B; real time (het stromen) &#x200B;](#streaming-example) integratie en het `url.value` gebied gebruikt de getemplatificeerde parameter `{{customerData.region}}` om een deel van het API eindpunt te personaliseren dat op gebruikersinput wordt gebaseerd.

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

Om gebruikers de optie te geven om een waarde van Experience Platform UI te selecteren, moet de `region` parameter ook in de [&#x200B; bestemmingsconfiguratie &#x200B;](../../authoring-api/destination-configuration/create-destination-configuration.md) als gebied van klantengegevens worden bepaald, zoals hieronder getoond:

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

Dientengevolge, wanneer de gebruikers door het [&#x200B; leerprogramma van de bestemmingsverbinding &#x200B;](../../../ui/connect-destination.md) gaan, moeten zij een gebied selecteren alvorens zij met het bestemmingsplatform kunnen verbinden. Wanneer de gebruiker verbinding maakt met het doel, wordt het sjabloonveld `{{customerData.region}}` vervangen door de waarde die de gebruiker in de gebruikersinterface heeft geselecteerd, zoals wordt weergegeven in de onderstaande afbeelding.

![&#x200B; beeld van Ui dat het scherm van de bestemmingsverbinding met een gebiedselecteur toont.](../../assets/functionality/destination-server/server-spec-template-region.png)

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
| `name` | String | *Vereist.* Vertegenwoordigt een vriendelijke naam van uw server, die alleen zichtbaar is voor Adobe. Deze naam is niet zichtbaar aan partners of klanten. Voorbeeld: `Moviestar destination server` . |
| `destinationServerType` | String | *Vereist.* Stel dit in op `URL_BASED` voor streamingdoelen. |
| `templatingStrategy` | String | *Vereist.* <ul><li>Gebruik `PEBBLE_V1` als u in het veld `value` een getemplativeerd veld gebruikt in plaats van een hard gecodeerde waarde. Gebruik deze optie als u een eindpunt als: `https://api.moviestar.com/data/{{customerData.region}}/items` hebt, waar de gebruikers het eindpuntgebied van Experience Platform UI moeten selecteren. </li><li> Gebruik `NONE` als er geen getemplatificeerde transformatie aan de Adobe-zijde nodig is, bijvoorbeeld als u een eindpunt hebt, zoals: `https://api.moviestar.com/data/items` </li></ul> |
| `value` | String | *Vereist.* Vul het adres in van het API-eindpunt waarmee Experience Platform verbinding moet maken. |

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
| `name` | String | De naam van uw doelserver. |
| `destinationServerType` | String | Stel deze waarde in op basis van het doelplatform. Als u bestanden naar een [!DNL Amazon S3] emmertje wilt exporteren, stelt u deze in op `FILE_BASED_S3` . |
| `fileBasedS3Destination.bucket.templatingStrategy` | String | *Vereiste*. Stel deze waarde in op basis van het type waarde dat in het veld `bucket.value` wordt gebruikt.<ul><li>Stel deze waarde in op `PEBBLE_V1` als u wilt dat uw gebruikers hun eigen emmernaam invoeren in de gebruikersinterface van Experience Platform. In dit geval, moet u het `value` gebied templatiseren om een waarde van de [&#x200B; gebieden van klantengegevens &#x200B;](../destination-configuration/customer-data-fields.md) te lezen die door de gebruiker worden gevuld. Dit gebruiksgeval wordt in het bovenstaande voorbeeld getoond.</li><li>Als u een hard-gecodeerde emmernaam voor uw integratie, zoals `"bucket.value":"MyBucket"` gebruikt, dan plaats deze waarde aan `NONE`.</li></ul> |
| `fileBasedS3Destination.bucket.value` | String | De naam van de [!DNL Amazon S3] emmer die door dit doel moet worden gebruikt. Dit kan of een templatized gebied zijn dat de waarde van de [&#x200B; gebieden van klantengegevens &#x200B;](../destination-configuration/customer-data-fields.md) zal lezen die door de gebruiker (zoals aangetoond in het bovenstaande voorbeeld) worden ingevuld, of een hard-gecodeerde waarde, zoals `"value":"MyBucket"`. |
| `fileBasedS3Destination.path.templatingStrategy` | String | *Vereiste*. Stel deze waarde in op basis van het type waarde dat in het veld `path.value` wordt gebruikt.<ul><li>Als u wilt dat uw gebruikers hun eigen pad invoeren in de gebruikersinterface van Experience Platform, stelt u deze waarde in op `PEBBLE_V1` . In dit geval, moet u het `path.value` gebied templatiseren om een waarde van de [&#x200B; gebieden van klantengegevens &#x200B;](../destination-configuration/customer-data-fields.md) te lezen die door de gebruiker worden gevuld. Dit gebruiksgeval wordt in het bovenstaande voorbeeld getoond.</li><li>Als u een pad met harde codes gebruikt voor uw integratie, zoals `"bucket.value":"/path/to/MyBucket"` , stelt u deze waarde in op `NONE` .</li></ul> |
| `fileBasedS3Destination.path.value` | String | Het pad naar de [!DNL Amazon S3] emmer die door dit doel moet worden gebruikt. Dit kan of een templatized gebied zijn dat de waarde van de [&#x200B; gebieden van klantengegevens &#x200B;](../destination-configuration/customer-data-fields.md) zal lezen die door de gebruiker (zoals aangetoond in het bovenstaande voorbeeld) worden ingevuld, of een hard-gecodeerde waarde, zoals `"value":"/path/to/MyBucket"`. |

{style="table-layout:auto"}

## [!DNL SFTP] doelserver {#sftp-example}

Met deze doelserver kunt u bestanden met Adobe Experience Platform-gegevens exporteren naar uw [!DNL SFTP] -opslagserver.

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
| `name` | String | De naam van uw doelserver. |
| `destinationServerType` | String | Stel deze waarde in op basis van het doelplatform. Als u bestanden naar een [!DNL SFTP] -doel wilt exporteren, stelt u deze in op `FILE_BASED_SFTP` . |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | String | *Vereiste*. Stel deze waarde in op basis van het type waarde dat in het veld `rootDirectory.value` wordt gebruikt.<ul><li>Als u wilt dat uw gebruikers hun eigen pad naar de hoofdmap invoeren in de gebruikersinterface van Experience Platform, stelt u deze waarde in op `PEBBLE_V1` . In dit geval, moet u het `rootDirectory.value` gebied templatiseren om een user-provided waarde van de [&#x200B; gebieden van klantengegevens &#x200B;](../destination-configuration/customer-data-fields.md) te lezen die door de gebruiker worden ingevuld. Dit gebruiksgeval wordt in het bovenstaande voorbeeld getoond.</li><li>Als u een pad naar de hoofdmap met harde codes gebruikt voor uw integratie, zoals `"rootDirectory.value":"Storage/MyDirectory"` , stelt u deze waarde in op `NONE` .</li></ul> |
| `fileBasedSFTPDestination.rootDirectory.value` | String | Het pad naar de map die de geëxporteerde bestanden host. Dit kan of een templatized gebied zijn dat de waarde van de [&#x200B; gebieden van klantengegevens &#x200B;](../destination-configuration/customer-data-fields.md) zal lezen die door de gebruiker (zoals aangetoond in het bovenstaande voorbeeld) worden ingevuld, of een hard-gecodeerde waarde, zoals `"value":"Storage/MyDirectory"` |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | String | *Vereiste*. Stel deze waarde in op basis van het type waarde dat in het veld `hostName.value` wordt gebruikt.<ul><li>Als u wilt dat uw gebruikers hun eigen hostnaam invoeren in de gebruikersinterface van Experience Platform, stelt u deze waarde in op `PEBBLE_V1` . In dit geval, moet u het `hostName.value` gebied templatiseren om een user-provided waarde van de [&#x200B; gebieden van klantengegevens &#x200B;](../destination-configuration/customer-data-fields.md) te lezen die door de gebruiker worden ingevuld. Dit gebruiksgeval wordt in het bovenstaande voorbeeld getoond.</li><li>Als u een hard-gecodeerde gastheernaam voor uw integratie, zoals `"hostName.value":"my.hostname.com"` gebruikt, dan plaats deze waarde aan `NONE`.</li></ul> |
| `fileBasedSFTPDestination.hostName.value` | String | De hostnaam van uw SFTP-server. Dit kan of een templatized gebied zijn dat de waarde van de [&#x200B; gebieden van klantengegevens &#x200B;](../destination-configuration/customer-data-fields.md) zal lezen die door de gebruiker (zoals aangetoond in het bovenstaande voorbeeld) worden ingevuld, of een hard-gecodeerde waarde, zoals `"hostName.value":"my.hostname.com"`. |
| `port` | Geheel | De SFTP-serverpoort. |
| `encryptionMode` | String | Geeft aan of bestandsversleuteling moet worden gebruikt. Ondersteunde waarden: <ul><li>PGP</li><li>Geen</li></ul> |

{style="table-layout:auto"}

## [!DNL Azure Data Lake Storage] ([!DNL ADLS]) doelserver {#adls-example}

Met deze doelserver kunt u bestanden met Adobe Experience Platform-gegevens exporteren naar uw [!DNL Azure Data Lake Storage] -account.

In het onderstaande voorbeeld ziet u een voorbeeld van een doelserverconfiguratie voor een [!DNL Azure Data Lake Storage] -doel.

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
| `name` | String | De naam van de doelverbinding. |
| `destinationServerType` | String | Stel deze waarde in op basis van het doelplatform. Stel dit voor [!DNL Azure Data Lake Storage] -doelen in op `FILE_BASED_ADLS_GEN2` . |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | String | *Vereiste*. Stel deze waarde in op basis van het type waarde dat in het veld `path.value` wordt gebruikt.<ul><li>Stel deze waarde in op `PEBBLE_V1` als u wilt dat uw gebruikers het pad naar de [!DNL ADLS] -map invoeren in de gebruikersinterface van Experience Platform. In dit geval, moet u het `path.value` gebied templatiseren om een waarde van de [&#x200B; gebieden van klantengegevens &#x200B;](../destination-configuration/customer-data-fields.md) te lezen die door de gebruiker worden gevuld. Dit gebruiksgeval wordt in het bovenstaande voorbeeld getoond.</li><li>Als u een pad met harde codes gebruikt voor uw integratie, zoals `"abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/"` , stelt u deze waarde in op `NONE` .</li></ul> |
| `fileBasedAdlsGen2Destination.path.value` | String | Het pad naar de [!DNL ADLS] -opslagmap. Dit kan of een templatized gebied zijn dat de waarde van de [&#x200B; gebieden van klantengegevens &#x200B;](../destination-configuration/customer-data-fields.md) zal lezen die door de gebruiker (zoals aangetoond in het bovenstaande voorbeeld) worden ingevuld, of een hard-gecodeerde waarde, zoals `abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/`. |

{style="table-layout:auto"}

## [!DNL Azure Blob Storage] doelserver {#blob-example}

Met deze doelserver kunt u bestanden met Adobe Experience Platform-gegevens exporteren naar uw [!DNL Azure Blob Storage] -container.

In het onderstaande voorbeeld ziet u een voorbeeld van een doelserverconfiguratie voor een [!DNL Azure Blob Storage] -doel.

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
| `name` | String | De naam van de doelverbinding. |
| `destinationServerType` | String | Stel deze waarde in op basis van het doelplatform. Stel dit voor [!DNL Azure Blob Storage] -doelen in op `FILE_BASED_AZURE_BLOB` . |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | String | *Vereiste*. Stel deze waarde in op basis van het type waarde dat in het veld `path.value` wordt gebruikt.<ul><li>Als u uw gebruikers hun eigen [!DNL Azure Blob] [&#x200B; opslag rekening URI &#x200B;](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) in Experience Platform UI wilt invoeren, plaats deze waarde aan `PEBBLE_V1`. In dit geval, moet u het `path.value` gebied templatiseren om de waarde van de [&#x200B; gebieden van klantengegevens &#x200B;](../destination-configuration/customer-data-fields.md) te lezen die door de gebruiker worden gevuld. Dit gebruiksgeval wordt in het bovenstaande voorbeeld getoond.</li><li>Als u een pad met harde codes gebruikt voor uw integratie, zoals `"path.value": "https://myaccount.blob.core.windows.net/"` , stelt u deze waarde in op `NONE` . |
| `fileBasedAzureBlobDestination.path.value` | String | Het pad naar de [!DNL Azure Blob] -opslag. Dit kan of een templatized gebied zijn dat de waarde van de [&#x200B; gebieden van klantengegevens &#x200B;](../destination-configuration/customer-data-fields.md) zal lezen die door de gebruiker (zoals aangetoond in het bovenstaande voorbeeld) worden ingevuld, of een hard-gecodeerde waarde, zoals `https://myaccount.blob.core.windows.net/`. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | String | *Vereiste*. Stel deze waarde in op basis van het type waarde dat in het veld `container.value` wordt gebruikt.<ul><li>Als u uw gebruikers hun eigen [!DNL Azure Blob] [&#x200B; containernaam &#x200B;](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) in Experience Platform UI wilt invoeren, plaats deze waarde aan `PEBBLE_V1`. In dit geval, moet u het `container.value` gebied templatiseren om de waarde van de [&#x200B; gebieden van klantengegevens &#x200B;](../destination-configuration/customer-data-fields.md) te lezen die door de gebruiker worden gevuld. Dit gebruiksgeval wordt in het bovenstaande voorbeeld getoond.</li><li>Als u een hard-gecodeerde containernaam voor uw integratie gebruikt, zoals `"path.value: myContainer"`, dan plaats deze waarde aan `NONE`. |
| `fileBasedAzureBlobDestination.container.value` | String | De naam van de Azure Blob Storage-container die voor deze bestemming moet worden gebruikt. Dit kan of een templatized gebied zijn dat de waarde van de [&#x200B; gebieden van klantengegevens &#x200B;](../destination-configuration/customer-data-fields.md) zal lezen die door de gebruiker (zoals aangetoond in het bovenstaande voorbeeld) worden ingevuld, of een hard-gecodeerde waarde, zoals `myContainer`. |

{style="table-layout:auto"}

## [!DNL Data Landing Zone] ([!DNL DLZ]) doelserver {#dlz-example}

Met deze doelserver kunt u bestanden met Experience Platform-gegevens exporteren naar een [[!DNL Data Landing Zone]](../../../catalog/cloud-storage/data-landing-zone.md) -opslagruimte.

Het voorbeeld hieronder toont een voorbeeld van een configuratie van de bestemmingsserver voor een [!DNL Data Landing Zone] ([!DNL DLZ]) bestemming.

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
| `name` | String | De naam van de doelverbinding. |
| `destinationServerType` | String | Stel deze waarde in op basis van het doelplatform. Stel dit voor [!DNL Data Landing Zone] -doelen in op `FILE_BASED_DLZ` . |
| `fileBasedDlzDestination.path.templatingStrategy` | String | *Vereiste*. Stel deze waarde in op basis van het type waarde dat in het veld `path.value` wordt gebruikt.<ul><li>Als u wilt dat uw gebruikers hun eigen [!DNL Data Landing Zone] -account invoeren in de gebruikersinterface van Experience Platform, stelt u deze waarde in op `PEBBLE_V1` . In dit geval, moet u het `path.value` gebied templatiseren om een waarde van de [&#x200B; gebieden van klantengegevens &#x200B;](../destination-configuration/customer-data-fields.md) te lezen die door de gebruiker worden gevuld. Dit gebruiksgeval wordt in het bovenstaande voorbeeld getoond.</li><li>Als u een pad met harde codes gebruikt voor uw integratie, zoals `"path.value": "https://myaccount.blob.core.windows.net/"` , stelt u deze waarde in op `NONE` . |
| `fileBasedDlzDestination.path.value` | String | Het pad naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen. |

{style="table-layout:auto"}

## [!DNL Google Cloud Storage] doelserver {#gcs-example}

Met deze doelserver kunt u bestanden met Experience Platform-gegevens exporteren naar uw [!DNL Google Cloud Storage] -account.

In het onderstaande voorbeeld ziet u een voorbeeld van een doelserverconfiguratie voor een [!DNL Google Cloud Storage] -doel.

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
| `name` | String | De naam van de doelverbinding. |
| `destinationServerType` | String | Stel deze waarde in op basis van het doelplatform. Stel dit voor [!DNL Google Cloud Storage] -doelen in op `FILE_BASED_GOOGLE_CLOUD` . |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | String | *Vereiste*. Stel deze waarde in op basis van het type waarde dat in het veld `bucket.value` wordt gebruikt.<ul><li>Stel deze waarde in op `PEBBLE_V1` als u wilt dat uw gebruikers hun eigen [!DNL Google Cloud Storage] emmernaam invoeren in de gebruikersinterface van Experience Platform. In dit geval, moet u het `bucket.value` gebied templatiseren om een waarde van de [&#x200B; gebieden van klantengegevens &#x200B;](../destination-configuration/customer-data-fields.md) te lezen die door de gebruiker worden gevuld. Dit gebruiksgeval wordt in het bovenstaande voorbeeld getoond.</li><li>Als u een hard-gecodeerde emmernaam voor uw integratie, zoals `"bucket.value": "my-bucket"` gebruikt, dan plaats deze waarde aan `NONE`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | String | De naam van de [!DNL Google Cloud Storage] emmer die door dit doel moet worden gebruikt. Dit kan of een templatized gebied zijn dat de waarde van de [&#x200B; gebieden van klantengegevens &#x200B;](../destination-configuration/customer-data-fields.md) zal lezen die door de gebruiker (zoals aangetoond in het bovenstaande voorbeeld) worden ingevuld, of een hard-gecodeerde waarde, zoals `"value": "my-bucket"`. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | String | *Vereiste*. Stel deze waarde in op basis van het type waarde dat in het veld `path.value` wordt gebruikt.<ul><li>Als u wilt dat uw gebruikers hun eigen [!DNL Google Cloud Storage] emmerpad invoeren in de gebruikersinterface van Experience Platform, stelt u deze waarde in op `PEBBLE_V1` . In dit geval, moet u het `path.value` gebied templatiseren om een waarde van de [&#x200B; gebieden van klantengegevens &#x200B;](../destination-configuration/customer-data-fields.md) te lezen die door de gebruiker worden gevuld. Dit gebruiksgeval wordt in het bovenstaande voorbeeld getoond.</li><li>Als u een pad met harde codes gebruikt voor uw integratie, zoals `"path.value": "/path/to/my-bucket"` , stelt u deze waarde in op `NONE` .</li></ul> |
| `fileBasedGoogleCloudStorageDestination.path.value` | String | Het pad naar de [!DNL Google Cloud Storage] -map die door dit doel moet worden gebruikt. Dit kan of een templatized gebied zijn dat de waarde van de [&#x200B; gebieden van klantengegevens &#x200B;](../destination-configuration/customer-data-fields.md) zal lezen die door de gebruiker (zoals aangetoond in het bovenstaande voorbeeld) worden ingevuld, of een hard-gecodeerde waarde, zoals `"value": "/path/to/my-bucket"`. |

{style="table-layout:auto"}

## Volgende stappen {#next-steps}

Na het lezen van dit artikel, zou u een beter inzicht in moeten hebben wat een specificatie van de bestemmingsserver is, en hoe u het kunt vormen.

Raadpleeg de volgende artikelen voor meer informatie over de andere componenten van de doelserver:

* [Sjabloonspecificaties](templating-specs.md)
* [Berichtindeling](message-format.md)
* [Configuratie bestandsindeling](file-formatting.md)
