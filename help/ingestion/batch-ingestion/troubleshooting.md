---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform - Handleiding voor het oplossen van problemen met batchverwerking
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 79466c78fd78c0f99f198b11a9117c946736f47a

---


# Handleiding voor het oplossen van problemen met inslikken

Met deze documentatie kunt u veelgestelde vragen met betrekking tot de batchgegevens voor het Adobe Experience Platform beantwoorden.

## Blokvraag API

### Zijn de partijen onmiddellijk actief na het ontvangen van HTTP 200 O.K. van CompleteBatch API?

De `200 OK` reactie van de API betekent dat de batch is geaccepteerd voor verwerking. De batch is pas actief als de eindtoestand ervan, zoals Actief of Mislukt, is bereikt.

### Kan de aanroep van de CompleteBatch-API opnieuw worden uitgevoerd nadat deze is mislukt?

Ja, het is veilig om de API-aanroep opnieuw te proberen. Ondanks de mislukking, is het mogelijk dat de verrichting daadwerkelijk slaagde en de partij met succes werd goedgekeurd. Van clients wordt echter verwacht dat ze opnieuw proberen in het geval van een API-fout, en ze worden in feite aangemoedigd om het opnieuw te proberen. Als de bewerking daadwerkelijk is gelukt, retourneert de API ook na het opnieuw proberen.

### Wanneer moet de API voor grote bestanden uploaden worden gebruikt?

De aanbevolen bestandsgrootte voor het gebruik van de API voor het uploaden van grote bestanden is 256 MB of groter. Meer informatie over het gebruik van de API voor het uploaden van grote bestanden vindt u [hier](./api-overview.md#ingest-large-parquet-files).

### Waarom mislukt de aanroep van de API voor groot bestand?

Als stukken van een groot bestand elkaar overlappen of ontbreken, reageert de server op een HTTP 400 Bad Request. Dit kan voorkomen omdat het mogelijk is overlappende blokken te uploaden, aangezien de waaierbevestigingen op het tijdstip van dossiervoltooiing worden gedaan, wanneer de dossierbrokken samen worden vastgemaakt.

## Ondersteuning voor spijsvertering

### Wat zijn de ondersteunde indelingen?

Momenteel worden Parquet en JSON ondersteund. CSV wordt ondersteund op oudere basis - terwijl gegevens worden bevorderd tot master en voorbereidende controles worden uitgevoerd, worden geen moderne functies zoals conversie, partitionering of rijvalidatie ondersteund.

### Waar moet het invoerformaat voor de batch worden gespecificeerd?

De invoernotatie moet worden opgegeven op het moment dat de batch wordt gemaakt tijdens het laden. Hieronder ziet u een voorbeeld van het opgeven van de notatie voor batchinvoer:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
    }'
```

### Hoe wordt JSON met meerdere regels ingenomen?

Als u JSON met meerdere regels wilt gebruiken, moet de `isMultiLineJson` markering worden ingesteld op het moment dat de batch wordt gemaakt. Hieronder ziet u een voorbeeld:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json",
                "isMultiLineJson": true
           }
      }'
```

### Wat is het verschil tussen JSON-lijnen (single-line JSON) en multi-line JSON?

Voor JSON-regels is er één JSON-object per regel. Bijvoorbeeld:

```json
{"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}}
{"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}}
{"string":"string3","int":3,"array":[3,6,9],"dict": {"key": "value3", "extra_key": "extra_value3"}}
```

Voor JSON met meerdere regels kan één object meerdere regels beslaan, terwijl alle objecten in een JSON-array zijn opgenomen. Bijvoorbeeld:

```json
[
    {"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}},
    {"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}},
    {
        "string": "string3",
        "int": 3,
        "array": [
            3,
            6,
            9
        ],
        "dict": {
            "key": "value3",
            "extra_key": "extra_value3"
        }
    }
]
```

Standaard wordt bij Batch-gegevensinname gebruikgemaakt van een JSON-regel met één regel.

### Wordt CSV-opname ondersteund?

CSV-inname wordt alleen ondersteund voor platte schema&#39;s. Het opnemen van hiërarchische gegevens in CSV wordt momenteel niet ondersteund.

Om alle functies voor gegevensinvoer te kunnen gebruiken, moet de indeling JSON of Parquet worden gebruikt.

### Welke validatietypen worden op de gegevens uitgevoerd?

Er worden drie validatieniveaus toegepast op de gegevens:

- Het schema - de Ingestie van de Partij zorgt ervoor dat het schema van de opgenomen gegevens het schema van de dataset aanpast.
- Het Type van gegevens - de Opname van de Partij zorgt ervoor dat het type voor elk opgenomen gebied het type aanpast dat in het schema van de dataset wordt bepaald.
- Restricties - De Ingestie van de Partij verzekert beperkingen, zoals &quot;Vereist&quot;, &quot;enum&quot;, en &quot;formaat&quot;worden behoorlijk bepaald in de schemadefinitie.

### Hoe kan een reeds opgenomen partij worden vervangen?

Een reeds opgenomen partij kan worden vervangen door de eigenschap van de Replay van de Partij te gebruiken. Meer informatie over Batch Replay vindt u [hier](./api-overview.md#replay-a-batch).

### Hoe wordt de inname van batch gecontroleerd?

Zodra een partij voor partijbevordering is gesignaleerd, kan de vooruitgang van de partijingestie met het volgende verzoek worden gecontroleerd:

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

Met dit verzoek krijgt u een vergelijkbaar antwoord:

```http
200 OK
```

```json
{
    "{BATCH_ID}":{
        "imsOrg":"{IMS_ORG}",
        "created":1494349962314,
        "createdClient":"{API_KEY}",
        "createdUser":"{USER_ID}",
        "updatedUser":"{USER_ID}",
        "completed":1494349963467,
        "externalId":"{EXTERNAL_ID}",
        "status":"staging",
        "errors":[],
    }
}
```

## Batchstatussen

### Wat zijn de mogelijke batchstaten?

Een batch kan in de levenscyclus de volgende statussen doorlopen:

| Status | Gegevens naar stramien geschreven | Beschrijving |
| ------ | ---------------------- | ----------- |
| Verlaten |  | De client heeft de batch niet binnen de verwachte tijd voltooid. |
| Afgebroken |  | De client heeft via de API&#39;s voor gegevensverwerking in batch expliciet een afbreekbewerking voor de opgegeven batch aangeroepen. Wanneer de status van een batch is geladen, kan de batch niet worden afgebroken. |
| Actief/Succes | x | De partij is met succes gepromoot van stadium aan meester, en is nu beschikbaar voor downstreamconsumptie. **Opmerking:** Actief en Succes worden door elkaar gebruikt. |
| Gearchiveerd |  | De partij is gearchiveerd in de koelkast. |
| Mislukt/Mislukt |  | Een eindstaat die uit of slechte configuratie en/of slechte gegevens voortvloeit. Er wordt een bewerkbare fout opgenomen, samen met de batch, om clients in staat te stellen de gegevens te corrigeren en opnieuw te verzenden. **Opmerking:** Mislukt en Mislukt worden onderling verwisselbaar gebruikt. |
| Inactief | x | De batch is gepromoveerd, maar deze is teruggezet of verlopen. De partij zal niet meer voor downstreamconsumptie beschikbaar zijn, maar de onderliggende gegevens blijven in Master totdat deze bewaard, gearchiveerd of anderszins verwijderd zijn. |
| Laden |  | De client schrijft momenteel gegevens voor de batch. De partij is op dit moment **niet** klaar voor promotie. |
| Geladen |  | De client heeft het schrijven van gegevens voor de batch voltooid. De partij is klaar voor promotie. |
| Behouden |  | De gegevens zijn uit Master genomen en bevinden zich in een speciaal archief in het Adobe Data Lake. |
| Staging |  | De klant heeft de batch met succes voor promotie gesignaleerd en de gegevens worden gefaseerd voor consumptie stroomafwaarts. |
| Opnieuw proberen |  | De cliënt heeft de partij voor bevordering gesignaleerd, maar wegens een fout, wordt de partij opnieuw geprobeerd door de dienst van de Controle van de Partij. Deze staat kan worden gebruikt om cliënten te vertellen dat er een vertraging in het opnemen van de gegevens kan zijn. |
| Gestopt |  | De cliënt heeft de partij voor bevordering gesignaleerd, maar na `n` herpogingen door de dienst van de Controle van de Partij, heeft de partijbevordering vastgelopen. |

### Wat betekent &#39;Staging&#39; voor batches?

Wanneer een partij zich in &quot;Staging&quot; bevindt, betekent dit dat de partij met succes is gesignaleerd voor promotie en dat de gegevens worden gefaseerd voor consumptie verderop.

### Wat betekent het als een partij &quot;Opnieuw probeert&quot;?

Wanneer een batch zich in &quot;Opnieuw proberen&quot; bevindt, betekent dit dat de gegevensopname van de batch tijdelijk is gestopt vanwege intermitterende problemen. Wanneer dit gebeurt, vereist het geen klanteninterventie.

### Wat betekent het wanneer een partij &quot;wordt afgebroken&quot;?

Wanneer een partij in &quot;Geroepen&quot;is, betekent het dat de Diensten van de Ingestie van Gegevens moeilijkheden ervaren die de partij opnemen en alle pogingen zijn uitgeput.

### Wat betekent het als een partij nog &quot;Lading&quot;is?

Wanneer een batch wordt geladen, betekent dit dat de API van CompleteBatch niet is aangeroepen om de batch te promoten.

### Is er een manier om te weten of een partij met succes is opgenomen?

Als de batchstatus &quot;Actief&quot; is, is de batch ingeslikt. Volg de [eerder](#how-is-batch-ingestion-monitored)beschreven stappen om de status van de batch te achterhalen.

### Wat gebeurt er als een batch mislukt?

Wanneer een partij ontbreekt, kan de reden het in de `errors` sectie van de lading worden geïdentificeerd. Hier volgen voorbeelden van fouten:

```json
    "errors":[
        {
            "code":"106",
            "description":"Dataset file is empty. Please upload file with data.",
            "rows":[]
        },
        {
            "code":"118",
            "description":"CSV file contains empty header row.",
            "rows":[]
        }
    ]
```

Nadat de fouten zijn gecorrigeerd, kan de batch opnieuw worden geüpload.

## Batchondersteuning

### Hoe moeten batches worden verwijderd?

In plaats van rechtstreeks uit Catalogus te schrappen, zouden de partijen moeten worden verwijderd gebruikend één van beide hieronder verstrekt methode:

1. Als de partij in uitvoering is, moet de partij worden afgebroken.
2. Indien de batch succesvol wordt gecontroleerd, dient de batch te worden teruggedraaid.

### Welke gegevens op batchniveau zijn beschikbaar?

De volgende cijfers op batchniveau zijn beschikbaar voor batches in de staat Actief/Succes:

| Metrisch | Beschrijving |
| ------ | ----------- |
| inputByteSize | The total number of bytes staged for Data Ingestie Services to process. |
| inputRecordSize | The total number of rows staged for Data Ingestie Services to process. |
| outputByteSize | Het totale aantal bytes die door de Diensten van de Ingestie van Gegevens aan het Meer van Gegevens worden uitgevoerd. |
| outputRecordSize | Het totale aantal rijen dat door de Diensten van de Ingestie van Gegevens aan het meer van Gegevens wordt uitgevoerd. |
| partitieCount | The total number of partitions written into Data Lake. |

### Waarom zijn metriek niet beschikbaar op sommige partijen?

Er zijn twee redenen waarom de metriek niet beschikbaar op uw partij kan zijn:

1. De batch heeft nooit de status Actief/Succes bereikt.
2. De batch is gepromoot via een verouderd promotiepad, zoals CSV-opname.

### Wat betekenen de verschillende statuscodes?

| Statuscode | Beschrijving |
| ----------- | ----------- |
| 106 | Het gegevensbestand van de dataset is leeg. |
| 118 | Het CSV-bestand bevat een lege koptekstrij. |
| 200 | De partij is goedgekeurd voor verwerking, en zal overgang aan een definitieve staat, zoals Actief of Mislukt. Na verzending kan de batch gecontroleerd worden aan de hand van het `GetBatch` eindpunt. |
| 400 | Onjuist verzoek. Wordt geretourneerd als een batch ontbrekende of overlappende blokken bevat. |

[large-file-upload]: batch_data_ingestion_developer_guide.md#how-to-ingest-large-parquet-files
