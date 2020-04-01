---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Handleiding voor ontwikkelaars van API voor gebruikersprofiel in realtime
topic: guide
translation-type: tm+mt
source-git-commit: d0ccaa5511375253a2eca8f1235c2f953b734709

---


# Systeemtaken profiel (aanvragen verwijderen)

Met het Adobe Experience Platform kunt u gegevens uit meerdere bronnen ophalen en robuuste profielen voor afzonderlijke klanten maken. Gegevens die in Platform worden opgenomen, worden opgeslagen in het Data Lake en in de gegevensopslag van het Profiel van de Klant in real time. Soms kan het nodig zijn om een gegevensset of batch uit de profielopslag te verwijderen om gegevens te verwijderen die niet meer nodig zijn of die ten onrechte zijn toegevoegd. Dit vereist het gebruiken van de Real-time API van het Profiel van de Klant om een systeembaan van het Profiel tot stand te brengen, die ook als &quot;schrappingsverzoek&quot;wordt bekend, die ook kan worden gewijzigd, worden gecontroleerd, of indien nodig worden verwijderd.

>[!NOTE]
>Als u gegevenssets of batches wilt verwijderen uit het Datameer, gaat u naar het overzicht [van de](../../catalog/home.md) Catalogusservice voor instructies.

## Aan de slag

De API eindpunten die in deze gids worden gebruikt maken deel uit van Real-time API van het Profiel van de Klant. Lees voordat u verdergaat de handleiding voor ontwikkelaars van de [realtime-API voor klantprofielen](getting-started.md). Met name bevat de sectie [Aan de](getting-started.md#getting-started) slag van de handleiding voor ontwikkelaars van profielen koppelingen naar verwante onderwerpen, een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document en belangrijke informatie over vereiste headers die nodig zijn om aanroepen naar API&#39;s van het Experience Platform met succes uit te voeren.

## Verzoeken om verwijderen weergeven

Een verwijderingsverzoek is een langdurig, asynchroon proces, wat betekent dat uw organisatie mogelijk meerdere verwijderingsverzoeken tegelijk uitvoert. Om alle schrappingsverzoeken te bekijken die uw organisatie momenteel loopt, kunt u een GET verzoek aan het `/system/jobs` eindpunt uitvoeren.

U kunt facultatieve vraagparameters ook gebruiken om de lijst van schrappingsverzoeken te filtreren die in de reactie zijn teruggekeerd. Als u meerdere parameters wilt gebruiken, scheidt u elke parameter met een en-teken (&amp;).

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
| `sort` | Sorteer de resultaten op een bepaald veld in oplopende (`asc`) of aflopende (`desc`) volgorde. De sorteerparameter werkt niet bij het retourneren van meerdere pagina&#39;s met resultaten. Voorbeeld: `sort=batchId:asc` |

**Verzoek**

```shell
curl -X POST \
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
| _page.count | Het totale aantal aanvragen. Deze reactie is afgebroken voor de ruimte. |
| _page.next | Als er nog een pagina met resultaten is, bekijkt u de volgende pagina met resultaten door de id-waarde in een [opzoekaanvraag](#view-a-specific-delete-request) te vervangen door de waarde &quot;next&quot;. |
| jobType | Het type taak dat wordt gemaakt. In dit geval retourneert deze altijd &quot;DELETE&quot;. |
| status | De status van de verwijderaanvraag. Mogelijke waarden zijn &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;COMPLETED&quot;, &quot;ERROR&quot;. |
| cijfers | Een object dat het aantal records bevat dat is verwerkt (&quot;recordsProcess&quot;) en de tijd in seconden dat het verzoek is verwerkt, of de tijd die het heeft geduurd voordat het verzoek is voltooid (&quot;timetakenInSec&quot;). |

## Een verwijderaanvraag maken {#create-a-delete-request}

Het in werking stellen van een nieuw schrappingsverzoek wordt gedaan door een POST- verzoek aan het `/systems/jobs` eindpunt, waar identiteitskaart van de te schrappen dataset of partij in het lichaam van het verzoek wordt verstrekt.

### Een gegevensset verwijderen

Om een dataset te schrappen, moet dataset identiteitskaart in het lichaam van het POST- verzoek worden omvat. Deze actie zal ALLE gegevens voor een bepaalde dataset schrappen. Het Platform van de ervaring staat u toe om datasets te schrappen die op zowel verslag als tijdreeksschema&#39;s worden gebaseerd.

>[!CAUTION]
> Wanneer het proberen om een profiel-Toegelaten dataset te schrappen gebruikend het Platform van de Ervaring UI, wordt de dataset onbruikbaar gemaakt voor opname maar zal niet worden geschrapt tot een schrappingsverzoek wordt gecreeerd gebruikend API. Zie de [bijlage](#appendix) bij dit document voor meer informatie.

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
| dataSetId | **(Vereist)** identiteitskaart van de dataset u wenst om te schrappen. |

**Antwoord**

Een geslaagde reactie retourneert de details van het nieuwe verwijderingsverzoek, inclusief een unieke, door het systeem gegenereerde, alleen-lezen-id voor de aanvraag. Dit kan worden gebruikt om het verzoek op te zoeken en zijn status te controleren. De `status` reden van de aanvraag op het moment van aanmaken is `"NEW"` totdat deze wordt verwerkt. Het antwoord `dataSetId` in de reactie moet overeenkomen met het antwoord dat in het verzoek is `dataSetId` verzonden.

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
| id | De unieke, door het systeem gegenereerde, alleen-lezen-id van de verwijderaanvraag. |
| dataSetId | De id van de gegevensset, zoals opgegeven in het POST-verzoek. |

### Een batch verwijderen

Om een partij te kunnen verwijderen, moet de partij-ID worden opgenomen in de hoofdtekst van de POST-aanvraag. Gelieve te worden geadviseerd dat u geen partijen voor datasets kunt schrappen die op verslagschema&#39;s worden gebaseerd. Alleen batches voor gegevenssets op basis van tijdreeksschema&#39;s mogen worden verwijderd.

>[!NOTE]
> De reden u niet batches voor datasets kunt schrappen die op verslagschema&#39;s worden gebaseerd is omdat de reeksen van de recordtype dataset vorige verslagen beschrijven en daarom niet &quot;undone&quot;of geschrapt kunnen zijn. De enige manier om het effect van onjuiste partijen voor datasets te verwijderen die op verslagschema&#39;s worden gebaseerd is de partij met de correcte gegevens opnieuw in te voeren om de onjuiste verslagen te beschrijven.

Voor meer informatie over record- en tijdreeksgedrag raadpleegt u de [sectie over XDM-gegevensgedrag](../../xdm/home.md#data-behaviors) in het XDM System-overzicht.

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
| batchId | **(Vereist)** De id van de batch die u wilt verwijderen. |

**Antwoord**

Een geslaagde reactie retourneert de details van het nieuwe verwijderingsverzoek, inclusief een unieke, door het systeem gegenereerde, alleen-lezen-id voor de aanvraag. Dit kan worden gebruikt om het verzoek op te zoeken en zijn status te controleren. De status van het verzoek op het moment van aanmaken is &#39;NEW&#39; totdat het wordt verwerkt. De &quot;batchId&quot; in de reactie moet overeenkomen met de &quot;batchId&quot; die in de aanvraag wordt verzonden.

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
| id | De unieke, door het systeem gegenereerde, alleen-lezen-id van de verwijderaanvraag. |
| batchId | De id van de batch, zoals opgegeven in de POST-aanvraag. |

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

Om een specifiek schrappingsverzoek, met inbegrip van details zoals zijn status te bekijken, kunt u een raadpleging (KRIJGEN) verzoek aan het `/system/jobs` eindpunt uitvoeren en identiteitskaart van het schrappingsverzoek in de weg omvatten.

**API-indeling**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| Parameter | Beschrijving |
|---|---|
| {DELETE_REQUEST_ID} | **(Vereist)** De id van het verwijderingsverzoek dat u wilt bekijken. |

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

| Eigenschappen | Beschrijving |
|---|---|
| jobType | Het type taak dat wordt gemaakt, retourneert in dit geval altijd &quot;DELETE&quot;. |
| status | De status van de verwijderaanvraag. Mogelijke waarden: &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;COMPLETED&quot;, &quot;ERROR&quot;. |
| cijfers | Een array die het aantal records bevat dat is verwerkt (&quot;recordsProcess&quot;) en de tijd in seconden dat de aanvraag is verwerkt, of de tijd die de aanvraag in beslag heeft genomen (&quot;timetakenInSec&quot;). |

Zodra de status van het verwijderingsverzoek &quot;COMPLETED&quot; is, kunt u bevestigen dat de gegevens zijn verwijderd door via de API voor gegevenstoegang toegang te krijgen tot de verwijderde gegevens. Voor instructies over hoe te om de Toegang API van Gegevens te gebruiken om tot datasets en partijen toegang te hebben, te herzien gelieve de documentatie [van de Toegang van](../../data-access/home.md)Gegevens.

## Een verwijderingsaanvraag verwijderen

Met het Experience Platform kunt u een eerdere aanvraag verwijderen. Dit kan om een aantal redenen nuttig zijn, bijvoorbeeld als de verwijdertaak niet is voltooid of vastgelopen in het verwerkingsstadium. Om een schrappingsverzoek te verwijderen, kunt u een verzoek van de SCHRAPPING aan het `/system/jobs` eindpunt uitvoeren en identiteitskaart van het schrappingsverzoek omvatten dat u wenst om aan de verzoekweg te verwijderen.

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

Een succesvol verwijderingsverzoek retourneert HTTP Status 200 (OK) en een lege antwoordinstantie. U kunt bevestigen het verzoek werd geschrapt door een GET verzoek uit te voeren om het schrappingsverzoek door zijn identiteitskaart te bekijken. Dit zou een Status 404 van HTTP (niet Gevonden) moeten terugkeren, erop wijzend dat het schrappingsverzoek werd verwijderd.

## Volgende stappen

Nu u de stappen kent betrokken bij het schrappen van datasets en partijen van de opslag van het Profiel binnen het Platform van de Ervaring, kunt u veilig gegevens schrappen die verkeerd zijn toegevoegd of dat uw organisatie niet meer nodig heeft. Houd er rekening mee dat een verwijderingsaanvraag niet ongedaan kan worden gemaakt. Verwijder daarom alleen gegevens die u zeker weet dat u deze nu niet nodig hebt en in de toekomst niet meer nodig hebt.

## Aanhangsel {#appendix}

De volgende informatie is supplementair aan de handeling van het schrappen van een dataset van de opslag van het Profiel.

### Een gegevensset verwijderen met de gebruikersinterface van het ervaringsplatform

Wanneer het gebruiken van het Platform van de Ervaring gebruikersinterface om een dataset te schrappen die voor Profiel is toegelaten, opent een dialoog vragend, &quot;bent u zeker u u deze dataset van het Meer van Gegevens van de Ervaring wilt schrappen? Gebruik de API &#39;profile systems job&#39; om deze dataset uit de profielservice te verwijderen.&quot;

Als u op **Verwijderen** in de gebruikersinterface klikt, wordt de gegevensset uitgeschakeld voor opname, maar wordt de gegevensset NIET automatisch verwijderd in de achterkant. Om de dataset permanent te schrappen, moet een schrappingsverzoek manueel gebruikend de stappen in deze gids voor het [creëren van een schrappingsverzoek](#create-a-delete-request)worden gecreeerd.

In de volgende afbeelding ziet u de waarschuwing wanneer u probeert een voor profiel ingeschakelde gegevensset te verwijderen met behulp van de gebruikersinterface.

![](../images/delete-profile-dataset.png)

Voor meer informatie betreffende het werken met datasets, gelieve te beginnen door het overzicht [van](../../catalog/datasets/overview.md)datasets te lezen.