---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Overzicht van gedeeltelijk in batch innemen van Adobe Experience Platforms
topic: overview
translation-type: tm+mt
source-git-commit: 83bb1ade8dbd9b1a166eb627d5d5d5eda987fa19
workflow-type: tm+mt
source-wordcount: '1243'
ht-degree: 0%

---



# Gedeeltelijke batch ingestie

Gedeeltelijke batch-opname is de mogelijkheid om gegevens met fouten in te voeren, tot een bepaalde drempel. Met deze mogelijkheid kunnen gebruikers al hun juiste gegevens in het Adobe Experience Platform opnemen terwijl al hun onjuiste gegevens afzonderlijk worden opgeslagen, samen met de redenen waarom dit niet het geval is.

Dit document bevat een zelfstudie voor het beheren van gedeeltelijke batch-opname.

Daarnaast bevat de [bijlage bij](#appendix) deze zelfstudie een verwijzing naar fouttypen voor gedeeltelijke batch-opname.

## Aan de slag

Deze zelfstudie vereist een praktische kennis van de verschillende diensten van de Adobe Experience Platform die betrokken zijn bij gedeeltelijke partijopname. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [Inname](./overview.md)in batch: De methode die gegevens uit gegevensbestanden, zoals CSV en Parquet, [!DNL Platform] opneemt en opslaat.
- [XDM (Experience Data Model)](../../xdm/home.md): Het gestandaardiseerde kader waardoor het Platform gegevens van de klantenervaring organiseert.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan APIs te maken. [!DNL Platform]

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van [!DNL Experience Platform] problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u aanroepen wilt uitvoeren naar [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](../../tutorials/authentication.md)voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen, zoals hieronder wordt getoond: [!DNL Experience Platform]

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor Platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Zie de documentatie over het [!DNL Platform]sandboxoverzicht voor meer informatie over sandboxen in [de](../../sandboxes/home.md)sandbox.

## Een batch voor gedeeltelijke batch-opname inschakelen in de API {#enable-api}

>[!NOTE]
>
>In deze sectie wordt beschreven hoe u een batch voor gedeeltelijke batch-opname via de API inschakelt. Voor instructies over het gebruiken van UI, te lezen gelieve een partij voor gedeeltelijke partijopname in de stap UI [](#enable-ui) toelaat.

U kunt een nieuwe partij tot stand brengen met gedeeltelijke toegelaten opname.

Als u een nieuwe batch wilt maken, volgt u de stappen in de ontwikkelaarshandleiding voor [batchverwerking](./api-overview.md). Als u de batchstap *Maken* hebt bereikt, voegt u het volgende veld toe aan de aanvraaginstantie:

```json
{
    ...
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
    ...
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

Om een nieuwe bronverbinding tot stand te brengen, volg de vermelde stappen in het [Bronoverzicht](../../sources/home.md). Zodra u de de detailstap *[!UICONTROL van de]* Dataflow bereikt, neem nota van de *[!UICONTROL Gedeeltelijke opname]* en van de *[!UICONTROL Diagnostiek]* van de Fout.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

Met de *[!UICONTROL optie Partiële]* inname kunt u het gebruik van gedeeltelijke batch-inname in- of uitschakelen.

De schakeloptie *[!UICONTROL Foutdiagnostiek]* wordt alleen weergegeven wanneer de schakeloptie *[!UICONTROL Partiële inname]* is uitgeschakeld. Met deze functie kunt u gedetailleerde foutberichten genereren [!DNL Platform] over ingesloten batches. Als de *[!UICONTROL schakeloptie Partiële inname]* is ingeschakeld, wordt de uitgebreide foutdiagnose automatisch afgedwongen.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

Met de *[!UICONTROL foutdrempel]* kunt u het percentage acceptabele fouten instellen voordat de gehele batch mislukt. Deze waarde is standaard ingesteld op 5%.

### Een bestaande gegevensset gebruiken {#existing-dataset}

Om een bestaande dataset te gebruiken, begin door een dataset te selecteren. De zijbalk rechts vult informatie over de gegevensset.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

Met de [!UICONTROL *[!UICONTROL optie Partiële]*] inname kunt u het gebruik van gedeeltelijke batch-inname in- of uitschakelen.

De schakeloptie *[!UICONTROL Foutdiagnostiek]* wordt alleen weergegeven wanneer de schakeloptie *[!UICONTROL Partiële inname]* is uitgeschakeld. Met deze functie kunt u gedetailleerde foutberichten genereren [!DNL Platform] over ingesloten batches. Als de *[!UICONTROL schakeloptie Partiële inname]* is ingeschakeld, wordt de uitgebreide foutdiagnose automatisch afgedwongen.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

Met de *[!UICONTROL foutdrempel]* kunt u het percentage acceptabele fouten instellen voordat de gehele batch mislukt. Deze waarde is standaard ingesteld op 5%.

Nu kunt u gegevens uploaden met de knop Gegevens **** toevoegen. Deze gegevens worden vervolgens gedeeltelijk opgenomen.

### De CSV-[!UICONTROL toewijzing aan het XDM-schema]gebruiken {#map-flow}

Als u de stroom &quot;CSV[!UICONTROL toewijzen aan XDM-schema]&quot; wilt gebruiken, volgt u de vermelde stappen in de zelfstudie [Een CSV-bestand toewijzen](../tutorials/map-a-csv-file.md). Zodra u de stap Gegevens ** toevoegen bereikt, neem nota van de *[!UICONTROL Gedeeltelijke opname]* en de diagnostische *[!UICONTROL gebieden van de]* Fout.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

Met de *[!UICONTROL optie Partiële]* inname kunt u het gebruik van gedeeltelijke batch-inname in- of uitschakelen.

De schakeloptie *[!UICONTROL Foutdiagnostiek]* wordt alleen weergegeven wanneer de schakeloptie *[!UICONTROL Partiële inname]* is uitgeschakeld. Met deze functie kunt u gedetailleerde foutberichten genereren [!DNL Platform] over ingesloten batches. Als de *[!UICONTROL schakeloptie Partiële inname]* is ingeschakeld, wordt de uitgebreide foutdiagnose automatisch afgedwongen.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

Met de *[!UICONTROL foutdrempel]* kunt u het percentage acceptabele fouten instellen voordat de gehele batch mislukt. Deze waarde is standaard ingesteld op 5%.

## Fouten bij gedeeltelijke inname van batch ophalen {#retrieve-errors}

Als de partijen mislukkingen bevatten, zult u fouteninformatie over deze mislukkingen moeten terugwinnen zodat kunt u de gegevens opnieuw opnemen.

### Status controleren {#check-status}

Om de status van de ingesloten batch te controleren, moet u de batch-id opgeven in het pad van een GET aanvraag.

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

**Antwoord**

Een succesvolle reactie retourneert HTTP status 200 met gedetailleerde informatie over de status van de batch.

```json
{
    "af838510-2233-11ea-acf0-f3edfcded2d2": {
        "status": "success",
        "tags": {
            ...
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
            ...
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
            "outputRecordCount": 497
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

Als de batch een fout heeft en foutdiagnose is ingeschakeld, is de status &#39;geslaagd&#39; met meer informatie over de fout in een downloadbaar foutbestand.

## Volgende stappen {#next-steps}

Dit leerprogramma behandelde hoe te om een dataset tot stand te brengen of te wijzigen om gedeeltelijke partijingestie toe te laten. Lees voor meer informatie over het in de partij innemen van de [partij de ontwikkelaarsgids](./api-overview.md).

## Typen fout bij gedeeltelijk in batch opnemen {#appendix}

Gedeeltelijke batch-opname heeft vier verschillende fouttypen bij het opnemen van gegevens.

- [Onleesbare bestanden](#unreadable)
- [Ongeldige schema&#39;s of kopteksten](#schemas-headers)
- [Onscheidbare rijen](#unparsable)
- [Ongeldige XDM-conversie](#conversion)

### Onleesbare bestanden {#unreadable}

Als de ingesloten batch onleesbare bestanden bevat, worden de fouten van de batch toegevoegd aan de batch zelf. Meer informatie over het ophalen van de mislukte batch vindt u in de handleiding voor het [ophalen van mislukte batches](../quality/retrieve-failed-batches.md).

### Ongeldige schema&#39;s of kopteksten {#schemas-headers}

Als de partij ingesloten een ongeldig schema of ongeldige kopballen heeft, zullen de fouten van de partij op de partij zelf worden vastgemaakt. Meer informatie over het ophalen van de mislukte batch vindt u in de handleiding voor het [ophalen van mislukte batches](../quality/retrieve-failed-batches.md).

### Onscheidbare rijen {#unparsable}

Als de partij ingesloten unparsable rijen heeft, zullen de fouten van de partij in een dossier worden opgeslagen dat kan worden betreden door het hieronder geschetste eindpunt te gebruiken.

**API-indeling**

```http
GET /export/batches/{BATCH_ID}/failed?path=parse_errors
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De `id` waarde van de partij u fouteninformatie van terugwint. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path=parse_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 met details van de onscheidbare rijen.

```json
{
    "_corrupt_record":"{missingQuotes:"v1"}",
    "_errors": [{
         "code":"1401",
         "message":"Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "a1.json"
}
```

### Ongeldige XDM-conversie {#conversion}

Als de partij ingesloten ongeldige XDM omzettingen heeft, zullen de fouten van de partij in een dossier worden opgeslagen dat door het volgende eindpunt kan worden betreden.

**API-indeling**

```http
GET /export/batches/{BATCH_ID}/failed?path=conversion_errors
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De `id` waarde van de partij u fouteninformatie van terugwint. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path=conversion_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met details van de mislukkingen in omzetting XDM terug.

```json
{
    "col1":"v1",
    "col2":"v2",
    "col3":[{
        "g1":"h1"
    }],
    "_errors":[{
        "column":"col3",
        "code":"123",
        "message":"Cannot convert array element from Object to String"
    }],
    "_filename":"a1.json"
},
{
    "col1":"v1",
    "col2":"v2",
    "col3":[{
        "g1":"h1"
    }],
    "_errors":[{
        "column":"col1",
        "code":"100",
        "message":"Cannot convert string to float"
    }],
    "_filename":"a2.json"
}
```
