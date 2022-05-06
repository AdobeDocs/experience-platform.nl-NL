---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API
title: API-eindpunt voor profielsysteemtaken
topic-legacy: guide
type: Documentation
description: Met Adobe Experience Platform kunt u een gegevensset of batch verwijderen uit de profielopslag om gegevens van het profiel in real-time te verwijderen die niet meer nodig zijn of die ten onrechte zijn toegevoegd. Hiervoor moet u de profiel-API gebruiken om een profielsysteemtaak te maken of een aanvraag te verwijderen.
exl-id: 75ddbf2f-9a54-424d-8569-d6737e9a590e
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1316'
ht-degree: 1%

---

# Het taakeindpunt van het profielsysteem (verzoeken van de Schrapping)

Met Adobe Experience Platform kunt u gegevens uit meerdere bronnen invoeren en robuuste profielen voor individuele klanten maken. Gegevens ingevoerd in [!DNL Platform] wordt opgeslagen in het dialoogvenster [!DNL Data Lake]en als de gegevenssets zijn ingeschakeld voor Profiel, worden die gegevens opgeslagen in de [!DNL Real-time Customer Profile] ook gegevens opslaan. Soms kan het nodig zijn om een gegevensset of batch uit de profielopslag te verwijderen om gegevens te verwijderen die niet meer nodig zijn of die ten onrechte zijn toegevoegd. Hiervoor moet u de [!DNL Real-time Customer Profile] API om een [!DNL Profile] systeemtaak, of `delete request`, die indien nodig ook kunnen worden gewijzigd, bewaakt of verwijderd.

>[!NOTE]
>
>Als u gegevenssets of batches wilt verwijderen uit het dialoogvenster [!DNL Data Lake], bezoek de [Overzicht van Catalog Service](../../catalog/home.md) voor meer informatie .

## Aan de slag

Het API-eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van het [[!DNL Real-time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Controleer voordat je doorgaat de [gids Aan de slag](getting-started.md) voor verbindingen aan verwante documentatie, een gids aan lezing de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om met succes vraag aan om het even welk Experience Platform API te maken.

## Verzoeken om verwijderen weergeven

Een verwijderingsverzoek is een langdurig, asynchroon proces, wat betekent dat uw organisatie mogelijk meerdere verwijderingsverzoeken tegelijk uitvoert. Als u alle verwijderingsaanvragen wilt weergeven die uw organisatie momenteel uitvoert, kunt u een aanvraag voor een GET indienen bij de `/system/jobs` eindpunt.

U kunt facultatieve vraagparameters ook gebruiken om de lijst van schrappingsverzoeken te filtreren die in de reactie zijn teruggekeerd. Als u meerdere parameters wilt gebruiken, scheidt u elke parameter met een en-teken (`&`).

**API-indeling**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| Parameter | Beschrijving |
|---|---|
| `start` | Verschuif de pagina met geretourneerde resultaten volgens de aanmaaktijd van de aanvraag. Voorbeeld: `start=4` |
| `limit` | Beperk het aantal geretourneerde resultaten. Voorbeeld: `limit=10` |
| `page` | Retourneer een specifieke pagina met resultaten volgens de aanmaaktijd van de aanvraag. Voorbeeld: `page=2` |
| `sort` | Resultaten sorteren op een bepaald veld in oplopende volgorde (`asc`) of aflopend (`desc`). De sorteerparameter werkt niet bij het retourneren van meerdere pagina&#39;s met resultaten. Voorbeeld: `sort=batchId:asc` |

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

De reactie bevat een array &#39;children&#39; met een object voor elke verwijderaanvraag die de details van die aanvraag bevat.

```json
{
  "_page": {
    "count": 100,
    "next": "K1JJRDpFaWc5QUwyZFgtMEpBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQVFBQWZBQUg0Ly9yL25PcmpmZndEZUR3QT0="
  },
  "children": [
    {
      "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
      "imsOrgId": "{ORG_ID}",
      "batchId": "8d075b5a178e48389126b9289dcfd0ac",
      "jobType": "DELETE",
      "status": "COMPLETED",
      "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
      "createEpoch": 1559026134,
      "updateEpoch": 1559026137
    },
    {
      "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
      "imsOrgId": "{ORG_ID}",
      "dataSetId": "5c802d3cd83fc114b741c4b5",
      "jobType": "DELETE",
      "status": "PROCESSING",
      "metrics": "{\"recordsProcessed\":0,\"timeTakenInSec\":15}",
      "createEpoch": 1559025404,
      "updateEpoch": 1559025406
    }
  ]
}
```

| Eigenschap | Beschrijving |
|---|---|
| `_page.count` | Het totale aantal aanvragen. Deze reactie is afgebroken voor de ruimte. |
| `_page.next` | Als er nog een pagina met resultaten is, bekijkt u de volgende pagina met resultaten door de id-waarde te vervangen in een [opzoekverzoek](#view-a-specific-delete-request) met de `"next"` opgegeven waarde. |
| `jobType` | Het type taak dat wordt gemaakt. In dit geval wordt altijd geretourneerd `"DELETE"`. |
| `status` | De status van de verwijderaanvraag. Mogelijke waarden zijn `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | Een object dat het aantal records bevat dat is verwerkt (`"recordsProcessed"`) en de tijd in seconden dat de aanvraag is verwerkt of hoe lang de aanvraag is voltooid (`"timeTakenInSec"`). |

## Een verwijderaanvraag maken {#create-a-delete-request}

Het in werking stellen van een nieuw schrappingsverzoek wordt gedaan door een verzoek van de POST aan `/systems/jobs` eindpunt, waar de identiteitskaart van de te schrappen dataset of partij in het lichaam van het verzoek wordt verstrekt.

### Een gegevensset verwijderen

Om een dataset van de opslag van het Profiel te schrappen, moet dataset identiteitskaart in het lichaam van het verzoek van de POST worden omvat. Deze actie zal ALLE gegevens voor een bepaalde dataset schrappen. [!DNL Experience Platform] staat u toe om datasets te schrappen die op zowel verslag als tijdreeksschema&#39;s worden gebaseerd.

**API-indeling**

```http
POST /system/jobs
```

**Verzoek**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

| Eigenschap | Beschrijving |
|---|---|
| `dataSetId` | **(Vereist)** De id van de gegevensset die u wilt verwijderen. |

**Antwoord**

Een geslaagde reactie retourneert de details van het nieuwe verwijderingsverzoek, inclusief een unieke, door het systeem gegenereerde, alleen-lezen-id voor de aanvraag. Dit kan worden gebruikt om het verzoek op te zoeken en zijn status te controleren. De `status` voor het verzoek op het tijdstip van aanmaak `"NEW"` totdat de verwerking wordt gestart. De `dataSetId` in het antwoord moet overeenkomen met de `dataSetId` verzonden in het verzoek.

```json
{
    "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
    "imsOrgId": "{ORG_ID}",
    "dataSetId": "5c802d3cd83fc114b741c4b5",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559025404,
    "updateEpoch": 1559025406
}
```

| Eigenschap | Beschrijving |
|---|---|
| `id` | De unieke, door het systeem gegenereerde, alleen-lezen-id van de verwijderaanvraag. |
| `dataSetId` | Identiteitskaart van de dataset, zoals die in het verzoek van de POST wordt gespecificeerd. |

### Een batch verwijderen

Om een partij te kunnen verwijderen, moet de partij-ID worden opgenomen in de hoofdtekst van de aanvraag voor de POST. Gelieve te worden geadviseerd dat u geen partijen voor datasets kunt schrappen die op verslagschema&#39;s worden gebaseerd. Alleen batches voor gegevenssets op basis van tijdreeksschema&#39;s mogen worden verwijderd.

>[!NOTE]
>
> De reden u niet batches voor datasets kunt schrappen die op verslagschema&#39;s worden gebaseerd is omdat de reeksen van de recordtype dataset vorige verslagen beschrijven en daarom niet &quot;undone&quot;of geschrapt kunnen zijn. De enige manier om het effect van onjuiste partijen voor datasets te verwijderen die op verslagschema&#39;s worden gebaseerd is de partij met de correcte gegevens opnieuw op te nemen om de onjuiste verslagen te beschrijven.

Voor meer informatie over record- en tijdreeksgedrag raadpleegt u de [sectie over XDM-gegevensgedrag](../../xdm/home.md#data-behaviors) in de [!DNL XDM System] overzicht.

**API-indeling**

```http
POST /system/jobs
```

**Verzoek**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

| Eigenschap | Beschrijving |
|---|---|
| `batchId` | **(Vereist)** De id van de batch die u wilt verwijderen. |

**Antwoord**

Een geslaagde reactie retourneert de details van het nieuwe verwijderingsverzoek, inclusief een unieke, door het systeem gegenereerde, alleen-lezen-id voor de aanvraag. Dit kan worden gebruikt om het verzoek op te zoeken en zijn status te controleren. De `"status"` voor het verzoek op het tijdstip van aanmaak `"NEW"` totdat de verwerking wordt gestart. De `"batchId"` waarde in de reactie moet overeenkomen met de waarde in `"batchId"` in de aanvraag verzonden waarde.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559026131,
    "updateEpoch": 1559026132
}
```

| Eigenschap | Beschrijving |
|---|---|
| `id` | De unieke, door het systeem gegenereerde, alleen-lezen-id van de verwijderaanvraag. |
| `batchId` | De id van de batch, zoals opgegeven in het verzoek om POST. |

Als u probeert om een schrappingsverzoek voor een partij van de dataset van het Verslag in werking te stellen, zult u een fout op 400 niveau ontmoeten, gelijkend op het volgende:

```json
{
    "requestId": "bc4eb29f-63a8-4653-9133-71238884bb81",
    "errors": {
        "400": [
            {
                "code": "500",
                "message": "Batch can only be specified for EE type 'a294e36d382649dab2cc6ad64a41b674'"
            }
        ]
    }
}
```

## Een specifiek verwijderingsverzoek weergeven {#view-a-specific-delete-request}

Als u een specifiek verwijderingsverzoek wilt weergeven, inclusief details zoals de status, kunt u een opzoekverzoek (GET) naar de `/system/jobs` en omvat identiteitskaart van het schrappingsverzoek in de weg.

**API-indeling**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| Parameter | Beschrijving |
|---|---|
| `{DELETE_REQUEST_ID}` | **(Vereist)** De id van de verwijderaanvraag die u wilt bekijken. |

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

In het antwoord worden de details van het verwijderingsverzoek weergegeven, inclusief de bijgewerkte status. De id van de verwijderaanvraag in de reactie (de `"id"` waarde) moet overeenkomen met de id die is verzonden in het aanvraagpad.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "COMPLETED",
    "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
    "createEpoch": 1559026134,
    "updateEpoch": 1559026137
}
```

| Properties | Beschrijving |
|---|---|
| `jobType` | Het type baan dat wordt gecreeerd, in dit geval zal het altijd terugkeren `"DELETE"`. |
| `status` | De status van de verwijderaanvraag. Mogelijke waarden: `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | Een array die het aantal records bevat dat is verwerkt (`"recordsProcessed"`) en de tijd in seconden dat de aanvraag is verwerkt of hoe lang de aanvraag is voltooid (`"timeTakenInSec"`). |

Zodra de status van het verwijderingsverzoek is `"COMPLETED"` U kunt bevestigen dat de gegevens zijn verwijderd door toegang te krijgen tot de verwijderde gegevens via de API voor gegevenstoegang. Voor instructies over hoe te om de Toegang API van Gegevens te gebruiken om tot datasets en partijen toegang te hebben, te herzien gelieve [Documentatie over gegevenstoegang](../../data-access/home.md).

## Een verwijderingsaanvraag verwijderen

[!DNL Experience Platform] Hiermee kunt u een eerdere aanvraag verwijderen. Dit kan om een aantal redenen nuttig zijn, bijvoorbeeld als de verwijdertaak niet is voltooid of vastgelopen in het verwerkingsstadium. Als u een verwijderingsaanvraag wilt verwijderen, kunt u een DELETE-aanvraag uitvoeren naar de `/system/jobs` eindpunt en omvat identiteitskaart van het schrappingsverzoek dat u aan de verzoekweg wenst te verwijderen.

**API-indeling**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| Parameter | Beschrijving |
|---|---|
| {DELETE_REQUEST_ID} | De id van de verwijderaanvraag die u wilt verwijderen. |

**Verzoek**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

Een succesvol verwijderingsverzoek retourneert HTTP Status 200 (OK) en een lege antwoordinstantie. U kunt bevestigen dat de aanvraag is verwijderd door een GET-aanvraag uit te voeren om de verwijderaanvraag met de id weer te geven. Dit zou een Status 404 van HTTP (niet Gevonden) moeten terugkeren, erop wijzend dat het schrappingsverzoek werd verwijderd.

## Volgende stappen

Nu u de stappen kent betrokken bij het schrappen van datasets en partijen van [!DNL Profile Store] binnen [!DNL Experience Platform]kunt u veilig gegevens verwijderen die ten onrechte zijn toegevoegd of die uw organisatie niet meer nodig heeft. Houd er rekening mee dat een verwijderingsaanvraag niet ongedaan kan worden gemaakt. Verwijder daarom alleen gegevens die u zeker weet dat u deze nu niet nodig hebt en in de toekomst niet meer nodig hebt.
