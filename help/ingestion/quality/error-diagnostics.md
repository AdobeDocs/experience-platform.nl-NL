---
keywords: Experience Platform;home;populaire onderwerpen;batch-opname;Batch-opname;partiële inname;Partiële inname;Fouten ophalen;Fout ophalen;Gedeeltelijke batch-opname;Gedeeltelijke batch-opname;Gedeeltelijke;Inslikken;Ingestie;Fouten diagnostiseren;Fouten opvragen;Fouten opsporen in diagnostiek;Fouten ophalen;Fouten ophalen;Fouten ophalen;
solution: Experience Platform
title: Diagnostiek gegevensinscriptiefout ophalen
topic-legacy: overview
description: Dit document bevat informatie over het controleren van batch-inname, het beheren van fouten bij gedeeltelijke batch-inname en een verwijzing naar typen partiële batch-inname.
exl-id: b885fb00-b66d-453b-80b7-8821117c2041
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 1%

---

# Diagnostische gegevens voor gegevensinvoer ophalen

Adobe Experience Platform biedt twee methoden voor het uploaden en opnemen van gegevens. U kunt batch-opname gebruiken, waardoor u gegevens kunt invoegen met verschillende bestandstypen (zoals CSV&#39;s), of streaming opname, waardoor u de gegevens kunt invoegen op [!DNL Platform] het gebruiken van het stromen eindpunten in echt - tijd.

Dit document bevat informatie over het controleren van batch-inname, het beheren van fouten bij gedeeltelijke batch-inname en een verwijzing naar typen partiële batch-inname.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
- [[!DNL Adobe Experience Platform Data Ingestion]](../home.md): De methoden waarmee gegevens kunnen worden verzonden naar [!DNL Experience Platform].

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] gids voor probleemoplossing.

### Waarden verzamelen voor vereiste koppen

Om vraag te maken aan [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in alle [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Alle bronnen in [!DNL Experience Platform], met inbegrip van die welke tot de [!DNL Schema Registry], geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over sandboxen in [!DNL Platform], zie de [overzichtsdocumentatie van sandbox](../../sandboxes/home.md).

## Foutendiagnostiek downloaden {#download-diagnostics}

Met Adobe Experience Platform kunnen gebruikers de foutdiagnose van de invoerbestanden downloaden. De diagnostiek blijft binnen [!DNL Platform] gedurende maximaal 30 dagen.

### Invoerbestanden weergeven {#list-files}

Het volgende verzoek wint een lijst van alle dossiers terug die in een gefinaliseerde partij worden verstrekt.

**API-indeling**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{BATCH_ID}` | De id van de batch die je opzoekt. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie retourneert JSON-objecten waarin wordt aangegeven waar de diagnostiek is opgeslagen.

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
                    "href": "https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json"
                }
            },
            "length": "1337",
            "name": "fileMetaData1.json"
        },
                {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2}/meta?path=input_files/fileMetaData2.json"
                }
            },
            "length": "1042",
            "name": "fileMetaData2.json"
        }
    ]
}
```

### Diagnose invoerbestand ophalen {#retrieve-diagnostics}

Nadat u een lijst met alle verschillende invoerbestanden hebt opgehaald, kunt u de diagnostiek van het afzonderlijke bestand ophalen met de volgende aanvraag.

**API-indeling**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files/{FILE}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{BATCH_ID}` | De id van de batch die je opzoekt. |
| `{FILE}` | De naam van het bestand dat u opent. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Als de reactie succesvol is, worden JSON-objecten geretourneerd die `path` objecten waarin wordt aangegeven waar de diagnostiek is opgeslagen. De reactie retourneert de `path` objecten in [JSON Lines](https://jsonlines.org/) gebruiken.

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## Fouten bij het ophalen van de batch {#retrieve-errors}

Als de partijen mislukkingen bevatten, zou u fouteninformatie over deze mislukkingen moeten terugwinnen zodat kunt u de gegevens opnieuw opnemen.

### Status controleren {#check-status}

Als u de status van de ingesloten batch wilt controleren, moet u de id van de batch opgeven in het pad van een GET-aanvraag. Voor meer informatie over het gebruik van deze API-aanroep leest u de [hulplijn voor eindpunt van catalogus](../../catalog/api/list-objects.md).

**API-indeling**

```http
GET /catalog/batches/{BATCH_ID}
GET /catalog/batches/{BATCH_ID}?{FILTER}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De `id` De waarde van de partij u de status van wilt controleren. |
| `{FILTER}` | Een queryparameter die wordt gebruikt om de resultaten te filteren die in de reactie worden geretourneerd. Meerdere parameters worden gescheiden door ampersands (`&`). Lees voor meer informatie de handleiding op [catalogusgegevens filteren](../../catalog/api/filter-data.md). |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/af838510-2233-11ea-acf0-f3edfcded2d2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respons zonder fouten**

Een geslaagde reactie retourneert met gedetailleerde informatie over de status van de batch.

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
        "imsOrg": "{ORG_ID}",
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
| `metrics.failedRecordCount` | Het aantal rijen dat niet kon worden verwerkt vanwege parseren, omzetten of valideren. Deze waarde kan worden afgeleid door de `inputRecordCount` van de `outputRecordCount`. Deze waarde wordt op alle batches gegenereerd, ongeacht of `errorDiagnostics` is ingeschakeld. |

**Reageren met fouten**

Als de partij één of meerdere fouten heeft en toegelaten foutendiagnostiek heeft, keert de reactie meer informatie over de fouten, zowel binnen de nuttige lading zelf als een downloadbaar foutendossier terug. De status van een batch met fouten kan nog steeds succesvol zijn.

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
        "imsOrg": "{ORG_ID}",
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
| `metrics.failedRecordCount` | Het aantal rijen dat niet kon worden verwerkt vanwege parseren, omzetten of valideren. Deze waarde kan worden afgeleid door de `inputRecordCount` van de `outputRecordCount`. Deze waarde wordt op alle batches gegenereerd, ongeacht of `errorDiagnostics` is ingeschakeld. |
| `errors.recordCount` | Het aantal rijen dat is mislukt voor de opgegeven foutcode. Deze waarde is **alleen** gegenereerd als `errorDiagnostics` is ingeschakeld. |

>[!NOTE]
>
>Als foutdiagnostiek niet beschikbaar is, wordt in plaats daarvan het volgende foutbericht weergegeven:
>
```json
>{
>       "errors": [{
>               "code": "INGEST-1211-400",
>               "description": "Encountered errors while parsing, converting or otherwise validating the data. Please resend the data with error diagnostics enabled to collect additional information on failure types"
>       }]
>}
>```

## Volgende stappen {#next-steps}

Deze zelfstudie besprak hoe u fouten met gedeeltelijke inname van batch kunt controleren. Lees voor meer informatie over het gebruik van batch [handleiding voor het ontwikkelen van batch-inhoud](../batch-ingestion/api-overview.md).

## Aanhangsel {#appendix}

Deze sectie verstrekt aanvullende informatie over de types van inname fout.

### Typen fout bij gedeeltelijk in batch opnemen {#partial-ingestion-types}

Gedeeltelijke batch-opname heeft drie verschillende fouttypen bij het invoeren van gegevens:

- [Onleesbare bestanden](#unreadable)
- [Ongeldige schema&#39;s of kopteksten](#schemas-headers)
- [Onscheidbare rijen](#unparsable)

### Onleesbare bestanden {#unreadable}

Als de ingesloten batch onleesbare bestanden bevat, worden de fouten van de batch toegevoegd aan de batch zelf. Meer informatie over het ophalen van de mislukte batch vindt u in de [hulplijn voor mislukte batches ophalen](../quality/retrieve-failed-batches.md).

### Ongeldige schema&#39;s of kopteksten {#schemas-headers}

Als de partij ingesloten een ongeldig schema of ongeldige kopballen heeft, zullen de fouten van de partij op de partij zelf worden vastgemaakt. Meer informatie over het ophalen van de mislukte batch vindt u in de [hulplijn voor mislukte batches ophalen](../quality/retrieve-failed-batches.md).

### Onscheidbare rijen {#unparsable}

Als de batch die u hebt ingevoegd onscheidbare rijen bevat, kunt u de volgende aanvraag gebruiken om een lijst weer te geven met bestanden die fouten bevatten.

**API-indeling**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De `id` waarde van de batch waarvan u foutgegevens ophaalt. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert een lijst met bestanden met fouten.

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

U kunt dan gedetailleerde informatie over de fouten terugwinnen gebruikend [diagnostische eindpunt van de herwinning](#retrieve-diagnostics).

Hieronder ziet u een voorbeeldreactie van het ophalen van het foutbestand:

```json
{
    "_corrupt_record": "{missingQuotes: 'v1'}",
    "_errors": [{
        "code": "1401",
        "message": "Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "parsing_errors_0.json"
}
```
