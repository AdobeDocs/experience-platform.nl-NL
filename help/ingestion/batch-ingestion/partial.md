---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Overzicht van gedeeltelijke invoer van Adobe Experience Platform-batch
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 0%

---



# Gedeeltelijke batch ingestie

Gedeeltelijke batch-opname is de mogelijkheid om gegevens met fouten in te voeren, tot een bepaalde drempel. Met deze functie kunnen gebruikers al hun juiste gegevens in Adobe Experience Platform opnemen terwijl al hun onjuiste gegevens afzonderlijk worden opgeslagen, samen met informatie over waarom de gegevens ongeldig zijn.

Dit document bevat een zelfstudie voor het beheren van gedeeltelijke batch-opname.

Daarnaast bevat de [bijlage bij](#appendix) deze zelfstudie een verwijzing naar fouttypen voor gedeeltelijke batch-opname.

## Aan de slag

Deze zelfstudie vereist een praktische kennis van de verschillende Adobe Experience Platform-services die betrokken zijn bij gedeeltelijke batchopname. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [Inname](./overview.md)in batch: De methode die gegevens uit gegevensbestanden, zoals CSV en Parquet, [!DNL Platform] opneemt en opslaat.
- [[!DNL Experience Data Model] (XDM)](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Platform] georganiseerd.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan APIs te maken. [!DNL Platform]

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van [!DNL Experience Platform] problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u aanroepen wilt uitvoeren naar [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](../../tutorials/authentication.md)voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen, zoals hieronder wordt getoond: [!DNL Experience Platform]

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Zie de documentatie over het [!DNL Platform]sandboxoverzicht voor meer informatie over sandboxen in [de](../../sandboxes/home.md)sandbox.

## Een batch voor gedeeltelijke batch-opname inschakelen in de API {#enable-api}

>[!NOTE]
>
>In deze sectie wordt beschreven hoe u een batch voor gedeeltelijke batch-opname via de API inschakelt. Voor instructies over het gebruiken van UI, te lezen gelieve een partij voor gedeeltelijke partijopname in de stap UI [](#enable-ui) toelaat.

U kunt een nieuwe partij tot stand brengen met gedeeltelijke toegelaten opname.

Als u een nieuwe batch wilt maken, volgt u de stappen in de ontwikkelaarshandleiding voor [batchverwerking](./api-overview.md). Als u de batchstap **[!UICONTROL Maken]** hebt bereikt, voegt u het volgende veld toe aan de aanvraaginstantie:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `enableErrorDiagnostics` | Een vlag die toestaat [!DNL Platform] om gedetailleerde foutenmeldingen over uw partij te produceren. |
| `partialIngestionPercentage` | Het percentage van aanvaardbare fouten vóór de volledige partij zal ontbreken. In dit voorbeeld kan maximaal 5% van de batch fouten zijn voordat deze mislukt. |


## Een batch voor gedeeltelijke batch-opname inschakelen in de gebruikersinterface {#enable-ui}

>[!NOTE]
>
>In deze sectie wordt beschreven hoe u een batch voor gedeeltelijke batchinvoer via de gebruikersinterface inschakelt. Als u al een batch voor gedeeltelijke batch-opname hebt ingeschakeld met de API, kunt u verdergaan met de volgende sectie.

Om een partij voor gedeeltelijke opname door [!DNL Platform] UI toe te laten, kunt u een nieuwe partij door bronverbindingen tot stand brengen, een nieuwe partij in een bestaande dataset tot stand brengen, of een nieuwe partij tot stand brengen door &quot;[!UICONTROL Kaart CSV aan stroom]XDM&quot;.

### Een nieuwe bronverbinding maken {#new-source}

Om een nieuwe bronverbinding tot stand te brengen, volg de vermelde stappen in het [Bronoverzicht](../../sources/home.md). Zodra u de de detailstap **[!UICONTROL van de]** Dataflow bereikt, neem nota van de **[!UICONTROL Gedeeltelijke opname]** en van de **[!UICONTROL Diagnostiek]** van de Fout.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

Met de **[!UICONTROL optie Partiële]** inname kunt u het gebruik van gedeeltelijke batch-inname in- of uitschakelen.

De schakeloptie **[!UICONTROL Foutdiagnostiek]** wordt alleen weergegeven wanneer de schakeloptie **[!UICONTROL Partiële inname]** is uitgeschakeld. Met deze functie kunt u gedetailleerde foutberichten genereren [!DNL Platform] over ingesloten batches. Als de *[!UICONTROL schakeloptie Partiële inname]* is ingeschakeld, wordt de uitgebreide foutdiagnose automatisch afgedwongen.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

Met de **[!UICONTROL foutdrempel]** kunt u het percentage acceptabele fouten instellen voordat de gehele batch mislukt. Deze waarde is standaard ingesteld op 5%.

### Een bestaande gegevensset gebruiken {#existing-dataset}

Om een bestaande dataset te gebruiken, begin door een dataset te selecteren. De zijbalk rechts vult informatie over de gegevensset.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

Met de **[!UICONTROL optie Partiële]** inname kunt u het gebruik van gedeeltelijke batch-inname in- of uitschakelen.

De schakeloptie **[!UICONTROL Foutdiagnostiek]** wordt alleen weergegeven wanneer de schakeloptie **[!UICONTROL Partiële inname]** is uitgeschakeld. Met deze functie kunt u gedetailleerde foutberichten genereren [!DNL Platform] over ingesloten batches. Als de **[!UICONTROL schakeloptie Partiële inname]** is ingeschakeld, wordt de uitgebreide foutdiagnose automatisch afgedwongen.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

Met de **[!UICONTROL foutdrempel]** kunt u het percentage acceptabele fouten instellen voordat de gehele batch mislukt. Deze waarde is standaard ingesteld op 5%.

Nu kunt u gegevens uploaden met de knop Gegevens **** toevoegen. Deze gegevens worden vervolgens gedeeltelijk opgenomen.

### De CSV-[!UICONTROL toewijzing aan het XDM-schema]gebruiken {#map-flow}

Als u de stroom &quot;CSV[!UICONTROL toewijzen aan XDM-schema]&quot; wilt gebruiken, volgt u de vermelde stappen in de zelfstudie [Een CSV-bestand toewijzen](../tutorials/map-a-csv-file.md). Zodra u de stap Gegevens **** toevoegen bereikt, neem nota van de **[!UICONTROL Gedeeltelijke opname]** en de diagnostische **[!UICONTROL gebieden van de]** Fout.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

Met de **[!UICONTROL optie Partiële]** inname kunt u het gebruik van gedeeltelijke batch-inname in- of uitschakelen.

De schakeloptie **[!UICONTROL Foutdiagnostiek]** wordt alleen weergegeven wanneer de schakeloptie **[!UICONTROL Partiële inname]** is uitgeschakeld. Met deze functie kunt u gedetailleerde foutberichten genereren [!DNL Platform] over ingesloten batches. Als de **[!UICONTROL schakeloptie Partiële inname]** is ingeschakeld, wordt de uitgebreide foutdiagnose automatisch afgedwongen.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

Met de **[!UICONTROL foutdrempel]** kunt u het percentage acceptabele fouten instellen voordat de gehele batch mislukt. Deze waarde is standaard ingesteld op 5%.

## Metagegevens op bestandsniveau downloaden {#download-metadata}

In Adobe Experience Platform kunnen gebruikers de metagegevens van de invoerbestanden downloaden. De metagegevens blijven maximaal 30 dagen bewaard. [!DNL Platform]

### Invoerbestanden weergeven {#list-files}

Met het volgende verzoek kunt u een lijst weergeven met alle bestanden die in een voltooide batch zijn opgegeven.

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvol antwoord retourneert HTTP-status 200 met JSON-objecten die padobjecten bevatten waarin wordt aangegeven waar de metagegevens zijn opgeslagen.

```json
{
    "_page": {
        "count": 1,
        "limit": 100
    },
    "data": [
        {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files/fileMetaData1.json"
                }
            },
            "length": "1337",
            "name": "fileMetaData1.json"
        },
                {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files/fileMetaData2.json"
                }
            },
            "length": "1042",
            "name": "fileMetaData2.json"
        }
    ]
}
```

### Metagegevens van invoerbestanden ophalen {#retrieve-metadata}

Nadat u een lijst met alle verschillende invoerbestanden hebt opgehaald, kunt u de metagegevens van het afzonderlijke bestand ophalen met behulp van het volgende eindpunt.

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvol antwoord retourneert HTTP-status 200 met JSON-objecten die padobjecten bevatten waarin wordt aangegeven waar de metagegevens zijn opgeslagen.

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## Fouten bij gedeeltelijke inname van batch ophalen {#retrieve-errors}

Als de partijen mislukkingen bevatten, zult u fouteninformatie over deze mislukkingen moeten terugwinnen zodat kunt u de gegevens opnieuw opnemen.

### Status controleren {#check-status}

Als u de status van de ingesloten batch wilt controleren, moet u de id van de batch opgeven in het pad van een GET-aanvraag.

**API-indeling**

```http
GET /catalog/batches/{BATCH_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De `id` waarde van de partij u de status van wilt controleren. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respons zonder fouten**

Een succesvolle reactie retourneert HTTP status 200 met gedetailleerde informatie over de status van de batch.

```json
{
    "af838510-2233-11ea-acf0-f3edfcded2d2": {
        "status": "success",
        "tags": {
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5deac2648a19d218a888d2b1"
            }
        ],
        "id": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "externalId": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "{IMS_ORG}",
        "started": 1576741718543,
        "metrics": {
            "inputByteSize": 568,
            "inputFileCount": 4,
            "inputRecordCount": 519,
            "outputRecordCount": 497,
            "failedRecordCount": 0
        },
        "completed": 1576741722026,
        "created": 1576741597205,
        "createdClient": "{API_KEY}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1576741722644,
        "version": "1.0.5"
    }    
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `metrics.failedRecordCount` | Het aantal rijen dat niet kon worden verwerkt vanwege parseren, omzetten of valideren. Deze waarde kan worden afgeleid door de waarde `inputRecordCount` van de `outputRecordCount`. Deze waarde wordt op alle batches gegenereerd, ongeacht of deze `errorDiagnostics` is ingeschakeld. |

**Reageren met fouten**

Als de batch een of meer fouten bevat en foutdiagnostiek ingeschakeld is, krijgt de status meer informatie over de fouten die in de reactie en in een downloadbaar foutbestand worden opgegeven. `success`

```json
{
    "01E8043CY305K2MTV5ANH9G1GC": {
        "status": "success",
        "tags": {
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5deac2648a19d218a888d2b1"
            }
        ],
        "id": "01E8043CY305K2MTV5ANH9G1GC",
        "externalId": "01E8043CY305K2MTV5ANH9G1GC",
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "{IMS_ORG}",
        "started": 1576741718543,
        "metrics": {
            "inputByteSize": 568,
            "inputFileCount": 4,
            "inputRecordCount": 519,
            "outputRecordCount": 514,
            "failedRecordCount": 5
        },
        "completed": 1576741722026,
        "created": 1576741597205,
        "createdClient": "{API_KEY}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1576741722644,
        "version": "1.0.5",
        "errors": [
           {
             "code": "INGEST-1212-400",
             "description": "Encountered 5 errors in the data. Successfully ingested 514 rows. Please review the associated diagnostic files for more details."
           },
           {
             "code": "INGEST-1401-400",
             "description": "The row has corrupted data and cannot be read or parsed. Fix the corrupted data and try again.",
             "recordCount": 2
           },
           {
             "code": "INGEST-1555-400",
             "description": "A required field is either missing or has a value of null. Add the required field to the input row and try again.",
             "recordCount": 3
           }
        ]
    }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `metrics.failedRecordCount` | Het aantal rijen dat niet kon worden verwerkt vanwege parseren, omzetten of valideren. Deze waarde kan worden afgeleid door de waarde `inputRecordCount` van de `outputRecordCount`. Deze waarde wordt op alle batches gegenereerd, ongeacht of deze `errorDiagnostics` is ingeschakeld. |
| `errors.recordCount` | Het aantal rijen dat is mislukt voor de opgegeven foutcode. Deze waarde wordt **alleen** gegenereerd als `errorDiagnostics` deze is ingeschakeld. |

>[!NOTE]
>
>Als foutdiagnostiek niet beschikbaar is, wordt in plaats daarvan het volgende foutbericht weergegeven:
> 
```json
> {
>         "errors": [{
>                 "code": "INGEST-1211-400",
>                 "description": "Encountered errors while parsing, converting or otherwise validating the data. Please resend the data with error diagnostics enabled to collect additional information on failure types"
>         }]
> }
> ```

## Volgende stappen {#next-steps}

Dit leerprogramma behandelde hoe te om een dataset tot stand te brengen of te wijzigen om gedeeltelijke partijingestie toe te laten. Lees voor meer informatie over het in de partij innemen van de [partij de ontwikkelaarsgids](./api-overview.md).

## Typen fout bij gedeeltelijk in batch opnemen {#appendix}

Gedeeltelijke batch-opname heeft drie verschillende fouttypen bij het opnemen van gegevens.

- [Onleesbare bestanden](#unreadable)
- [Ongeldige schema&#39;s of kopteksten](#schemas-headers)
- [Onscheidbare rijen](#unparsable)

### Onleesbare bestanden {#unreadable}

Als de ingesloten batch onleesbare bestanden bevat, worden de fouten van de batch toegevoegd aan de batch zelf. Meer informatie over het ophalen van de mislukte batch vindt u in de handleiding voor het [ophalen van mislukte batches](../quality/retrieve-failed-batches.md).

### Ongeldige schema&#39;s of kopteksten {#schemas-headers}

Als de partij ingesloten een ongeldig schema of ongeldige kopballen heeft, zullen de fouten van de partij op de partij zelf worden vastgemaakt. Meer informatie over het ophalen van de mislukte batch vindt u in de handleiding voor het [ophalen van mislukte batches](../quality/retrieve-failed-batches.md).

### Onscheidbare rijen {#unparsable}

Als de batch die u hebt ingevoegd onscheidbare rijen bevat, kunt u het volgende eindpunt gebruiken om een lijst met bestanden weer te geven die fouten bevatten.

**API-indeling**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De `id` waarde van de partij u fouteninformatie van terugwint. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 met een lijst van de bestanden die fouten bevatten.

```json
{
    "data": [
        {
            "name": "conversion_errors_0.json",
            "length": "1162",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors%2Fconversion_errors_0.json"
                }
            }
        },
        {
            "name": "parsing_errors_0.json",
            "length": "153",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors%2Fparsing_errors_0.json"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 2
    }
}
```

U kunt gedetailleerde informatie over de fouten dan terugwinnen gebruikend het eindpunt [van de](#retrieve-metadata)meta-gegevensherwinning.

Hieronder ziet u een voorbeeldreactie van het ophalen van het foutbestand:

```json
{
    "_corrupt_record": "{missingQuotes: "v1"}",
    "_errors": [{
        "code": "1401",
        "message": "Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "parsing_errors_0.json"
}
```
