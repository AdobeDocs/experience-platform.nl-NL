---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
title: Systeemtaken profiel - Real-time API voor klantprofiel
topic: guide
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '1420'
ht-degree: 1%

---


# Het taakeindpunt van het profielsysteem (verzoeken van de Schrapping)

Met Adobe Experience Platform kunt u gegevens uit meerdere bronnen invoeren en robuuste profielen voor individuele klanten maken. Gegevens die in [!DNL Platform] worden ingevoerd, worden zowel in de [!DNL Data Lake] gegevensopslag als in de [!DNL Real-time Customer Profile] gegevensopslag opgeslagen. Soms kan het nodig zijn om een gegevensset of batch uit de profielopslag te verwijderen om gegevens te verwijderen die niet meer nodig zijn of die ten onrechte zijn toegevoegd. Hiervoor moet u de [!DNL Real-time Customer Profile] API gebruiken om een [!DNL Profile] systeemtaak te maken, ook wel een &quot;[!DNL delete request]&quot;-taak genoemd, die indien nodig ook kan worden gewijzigd, bewaakt of verwijderd.

>[!NOTE]
>
>Als u gegevenssets of batches wilt verwijderen uit de [!DNL Data Lake]catalogus, gaat u naar het overzicht [van de](../../catalog/home.md) Catalogusservice voor instructies.

## Aan de slag

Het API-eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)handleiding. Lees voordat u verdergaat de gids [Aan de](getting-started.md) slag voor koppelingen naar gerelateerde documentatie, een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document en belangrijke informatie over vereiste headers die nodig zijn om aanroepen naar een willekeurige [!DNL Experience Platform] API mogelijk te maken.

## Verzoeken om verwijderen weergeven

Een verwijderingsverzoek is een langdurig, asynchroon proces, wat betekent dat uw organisatie mogelijk meerdere verwijderingsverzoeken tegelijk uitvoert. Om alle schrappingsverzoeken te bekijken die uw organisatie momenteel loopt, kunt u een verzoek van de GET aan het `/system/jobs` eindpunt uitvoeren.

U kunt facultatieve vraagparameters ook gebruiken om de lijst van schrappingsverzoeken te filtreren die in de reactie zijn teruggekeerd. Als u meerdere parameters wilt gebruiken, scheidt u elke parameter met een en-teken (&amp;).

**API-indeling**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| Parameter | Beschrijving |
|---|---|
| `start` | Verschuif de pagina met geretourneerde resultaten volgens de aanmaaktijd van de aanvraag. Voorbeeld: *`start=4`* |
| `limit` | Beperk het aantal geretourneerde resultaten. Voorbeeld: *`limit=10`* |
| `page` | Retourneer een specifieke pagina met resultaten volgens de aanmaaktijd van de aanvraag. Voorbeeld: ***`page=2`*** |
| `sort` | Sorteer de resultaten op een bepaald veld in oplopende (*`asc`*) of aflopende (**`desc`**) volgorde. De sorteerparameter werkt niet bij het retourneren van meerdere pagina&#39;s met resultaten. Voorbeeld: `sort=batchId:asc` |

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
      "imsOrgId": "{IMS_ORG}",
      "batchId": "8d075b5a178e48389126b9289dcfd0ac",
      "jobType": "DELETE",
      "status": "COMPLETED",
      "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
      "createEpoch": 1559026134,
      "updateEpoch": 1559026137
    },
    {
      "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
      "imsOrgId": "{IMS_ORG}",
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
| `_page.next` | Als er nog een pagina met resultaten is, bekijkt u de volgende pagina met resultaten door de id-waarde in een [opzoekaanvraag](#view-a-specific-delete-request) te vervangen door de opgegeven `"next"` waarde. |
| `jobType` | Het type taak dat wordt gemaakt. In dit geval zal het altijd terugkeren `"DELETE"`. |
| `status` | De status van de verwijderaanvraag. Mogelijke waarden zijn `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | Een object dat het aantal records bevat dat is verwerkt (`"recordsProcessed"`) en de tijd in seconden dat de aanvraag is verwerkt, of de tijd die het duurt voordat de aanvraag is voltooid (`"timeTakenInSec"`). |

## Een verwijderaanvraag maken {#create-a-delete-request}

Het in werking stellen van een nieuw schrappingsverzoek wordt gedaan door een verzoek van de POST aan het `/systems/jobs` eindpunt, waar identiteitskaart van de te schrappen dataset of partij in het lichaam van het verzoek wordt verstrekt.

### Een gegevensset verwijderen

Om een dataset te schrappen, moet dataset identiteitskaart in het lichaam van het verzoek van de POST worden omvat. Deze actie zal ALLE gegevens voor een bepaalde dataset schrappen. [!DNL Experience Platform] staat u toe om datasets te schrappen die op zowel verslag als tijdreeksschema&#39;s worden gebaseerd.

>[!CAUTION]
>
> Wanneer het proberen om een [!DNL Profile]-toegelaten dataset te schrappen gebruikend [!DNL Experience Platform] UI, wordt de dataset onbruikbaar gemaakt voor opname maar zal niet worden geschrapt tot een schrappingsverzoek wordt gecreeerd gebruikend API. Zie de [bijlage](#appendix) bij dit document voor meer informatie.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

| Eigenschap | Beschrijving |
|---|---|
| `dataSetId` | **(Vereist)** identiteitskaart van de dataset u wenst om te schrappen. |

**Antwoord**

Een geslaagde reactie retourneert de details van het nieuwe verwijderingsverzoek, inclusief een unieke, door het systeem gegenereerde, alleen-lezen-id voor de aanvraag. Dit kan worden gebruikt om het verzoek op te zoeken en zijn status te controleren. De **`status`** reden van de aanvraag op het moment van aanmaken is *`"NEW"`* totdat deze wordt verwerkt. Het antwoord **`dataSetId`** in de reactie moet overeenkomen met het antwoord dat in het verzoek is ***`dataSetId`*** verzonden.

```json
{
    "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
    "imsOrgId": "{IMS_ORG}",
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

Voor meer informatie over record- en tijdreeksgedrag raadpleegt u de [sectie over XDM-gegevensgedrag](../../xdm/home.md#data-behaviors) in het [!DNL XDM System] overzicht.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

| Eigenschap | Beschrijving |
|---|---|
| `batchId` | **(Vereist)** De id van de batch die u wilt verwijderen. |

**Antwoord**

Een geslaagde reactie retourneert de details van het nieuwe verwijderingsverzoek, inclusief een unieke, door het systeem gegenereerde, alleen-lezen-id voor de aanvraag. Dit kan worden gebruikt om het verzoek op te zoeken en zijn status te controleren. De `"status"` reden van de aanvraag op het moment van aanmaken is `"NEW"` totdat deze wordt verwerkt. Het antwoord `"batchId"` in de reactie moet overeenkomen met het antwoord dat in het verzoek is `"batchId"` verzonden.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{IMS_ORG}",
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

Om een specifiek schrappingsverzoek, met inbegrip van details zoals zijn status te bekijken, kunt u een raadpleging (GET) verzoek aan het `/system/jobs` eindpunt uitvoeren en identiteitskaart van het schrappingsverzoek in de weg omvatten.

**API-indeling**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| Parameter | Beschrijving |
|---|---|
| `{DELETE_REQUEST_ID}` | **(Vereist)** De id van het verwijderingsverzoek dat u wilt bekijken. |

**Verzoek**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

In het antwoord worden de details van het verwijderingsverzoek weergegeven, inclusief de bijgewerkte status. De id van de verwijderaanvraag in de reactie moet overeenkomen met de id die in het aanvraagpad is verzonden.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{IMS_ORG}",
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
| `metrics` | Een array die het aantal records bevat dat is verwerkt (`"recordsProcessed"`) en de tijd in seconden dat de aanvraag is verwerkt, of de tijd die nodig was om de aanvraag te voltooien (`"timeTakenInSec"`). |

Zodra de status van de verwijderaanvraag is ingesteld, kunt `"COMPLETED"` u bevestigen dat de gegevens zijn verwijderd door via de API voor gegevenstoegang toegang te krijgen tot de verwijderde gegevens. Voor instructies over hoe te om de Toegang API van Gegevens te gebruiken om tot datasets en partijen toegang te hebben, te herzien gelieve de documentatie [van de Toegang van](../../data-access/home.md)Gegevens.

## Een verwijderingsaanvraag verwijderen

[!DNL Experience Platform] Hiermee kunt u een eerdere aanvraag verwijderen. Dit kan om een aantal redenen nuttig zijn, bijvoorbeeld als de verwijdertaak niet is voltooid of vastgelopen in het verwerkingsstadium. Om een schrappingsverzoek te verwijderen, kunt u een verzoek van DELETE aan het `/system/jobs` eindpunt uitvoeren en identiteitskaart van het schrappingsverzoek omvatten dat u wenst om aan de verzoekweg te verwijderen.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

Een succesvol verwijderingsverzoek retourneert HTTP Status 200 (OK) en een lege antwoordinstantie. U kunt bevestigen dat de aanvraag is verwijderd door een GET-aanvraag uit te voeren om de verwijderaanvraag met de id weer te geven. Dit zou een Status 404 van HTTP (niet Gevonden) moeten terugkeren, erop wijzend dat het schrappingsverzoek werd verwijderd.

## Volgende stappen

Nu u de stappen kent betrokken bij het schrappen van datasets en partijen van [!DNL Profile Store] binnen [!DNL Experience Platform], kunt u veilig gegevens schrappen die verkeerd zijn toegevoegd of dat uw organisatie niet meer nodig heeft. Houd er rekening mee dat een verwijderingsaanvraag niet ongedaan kan worden gemaakt. Verwijder daarom alleen gegevens die u zeker weet dat u deze nu niet nodig hebt en in de toekomst niet meer nodig hebt.

## Aanhangsel {#appendix}

De volgende informatie is aanvullend op het schrappen van een dataset van het [!DNL Profile Store].

### Een gegevensset verwijderen met de [!DNL Experience Platform] UI

Wanneer het gebruiken van het [!DNL Experience Platform] gebruikersinterface om een dataset te schrappen die voor is toegelaten [!DNL Profile], opent een dialoog vragend, &quot;bent u zeker u wilt deze dataset van [!DNL Experience Data Lake]? Gebruik de &#39;p[!DNL rofile systems jobs]&#39;-API om deze gegevensset uit de [!DNL Profile Service]te verwijderen.&quot;

Als u op **[!UICONTROL Verwijderen]** in de gebruikersinterface klikt, wordt de gegevensset uitgeschakeld voor opname, maar wordt de gegevensset NIET automatisch verwijderd in de achterkant. Om de dataset permanent te schrappen, moet een schrappingsverzoek manueel gebruikend de stappen in deze gids voor het [creëren van een schrappingsverzoek](#create-a-delete-request)worden gecreeerd.

Het volgende beeld toont de waarschuwing wanneer het proberen om een [!DNL Profile]-Toegelaten dataset te schrappen gebruikend UI.

![](../images/delete-profile-dataset.png)

Voor meer informatie betreffende het werken met datasets, gelieve te beginnen door het overzicht [van](../../catalog/datasets/overview.md)datasets te lezen.