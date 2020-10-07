---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Beschikbare cijfers
topic: developer guide
translation-type: tm+mt
source-git-commit: ae6f220cdec54851fb78b7ba8a8eb19f2d06b684
workflow-type: tm+mt
source-wordcount: '2007'
ht-degree: 1%

---


# Metrisch eindpunt

De metriek van de waarneming verstrekt inzicht in gebruiksstatistieken, historische tendensen, en prestatiesindicatoren voor diverse eigenschappen in Adobe Experience Platform. Het `/metrics` eindpunt in [!DNL Observability Insights API] staat u toe om metrische gegevens voor de activiteit van uw organisatie binnen programmatically terug te winnen [!DNL Platform].

## Aan de slag

Het API-eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [[!DNL Observability Insights] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml). Lees voordat u verdergaat de gids [Aan de](./getting-started.md) slag voor koppelingen naar gerelateerde documentatie, een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document en belangrijke informatie over vereiste headers die nodig zijn om aanroepen naar een willekeurige [!DNL Experience Platform] API mogelijk te maken.

## Metrische waarden voor waarneembaarheid ophalen

Er zijn twee ondersteunde methoden voor het ophalen van metrische gegevens met behulp van de API:

* [Versie 1](#v1): Geef metrische gegevens op met behulp van queryparameters.
* [Versie 2](#v2): Geef filters op en pas ze toe op metrische getallen met behulp van een JSON-payload.

### Versie 1 {#v1}

U kunt metrische gegevens terugwinnen door een verzoek van de GET aan het `/metrics` eindpunt te doen, die metriek door het gebruik van vraagparameters specificeren.

**API-indeling**

In de `metric` parameter moet ten minste één metrische waarde worden opgegeven. Andere vraagparameters zijn facultatief voor het filtreren resultaten.

```http
GET /metrics?metric={METRIC}
GET /metrics?metric={METRIC}&metric={METRIC_2}
GET /metrics?metric={METRIC}&id={ID}
GET /metrics?metric={METRIC}&dateRange={DATE_RANGE}
GET /metrics?metric={METRIC}&metric={METRIC_2}&id={ID}&dateRange={DATE_RANGE}
```

| Parameter | Beschrijving |
| --- | --- |
| `{METRIC}` | De metrisch u wilt blootstellen. Wanneer het combineren van veelvoudige metriek in één enkele vraag, moet u ampersand (`&`) gebruiken om individuele metriek te scheiden. Bijvoorbeeld, `metric={METRIC_1}&metric={METRIC_2}`. |
| `{ID}` | De id voor een bepaalde [!DNL Platform] bron waarvan u de meetgegevens wilt weergeven. Deze id kan optioneel, vereist of niet van toepassing zijn, afhankelijk van de gebruikte maatstaven. Zie de [bijlage](#available-metrics) voor een lijst van beschikbare metriek, met inbegrip van gesteunde (zowel vereiste als facultatieve) identiteitskaarts voor elke metrisch. |
| `{DATE_RANGE}` | Het datumbereik voor de metriek die u wilt weergeven, in de ISO 8601-indeling (bijvoorbeeld `2018-10-01T07:00:00.000Z/2018-10-09T07:00:00.000Z`). |

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics?metric=timeseries.ingestion.dataset.size&metric=timeseries.ingestion.dataset.recordsuccess.count&id=5cf8ab4ec48aba145214abeb&dateRange=2018-10-01T07:00:00.000Z/2019-06-06T07:00:00.000Z \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert een lijst met objecten die elk een tijdstempel bevatten binnen de opgegeven waarden `dateRange` en de bijbehorende waarden voor de metriek die in het aanvraagpad zijn opgegeven. Als het `id` van een [!DNL Platform] bron is opgenomen in het aanvraagpad, zijn de resultaten alleen van toepassing op die bron. Als het `id` wordt weggelaten, zullen de resultaten op alle toepasselijke middelen binnen uw IMS Organisatie van toepassing zijn.

```json
{
  "id": "5cf8ab4ec48aba145214abeb",
  "imsOrgId": "{IMS_ORG}",
  "timeseries": {
    "granularity": "MONTH",
    "items": [
      {
        "timestamp": "2019-06-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 1125,
          "timeseries.ingestion.dataset.size": 32320
        }
      },
      {
        "timestamp": "2019-05-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 1003,
          "timeseries.ingestion.dataset.size": 31409
        }
      },
      {
        "timestamp": "2019-04-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 740,
          "timeseries.ingestion.dataset.size": 25809
        }
      },
      {
        "timestamp": "2019-03-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 740,
          "timeseries.ingestion.dataset.size": 25809
        }
      },
      {
        "timestamp": "2019-02-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 390,
          "timeseries.ingestion.dataset.size": 16801
        }
      }
    ],
    "_page": null,
    "_links": null
  },
  "stats": {}
}
```

### Versie 2 {#v2}

U kunt metrieke gegevens terugwinnen door een verzoek van de POST aan het `/metrics` eindpunt te doen, specificerend de metriek u wenst om in de nuttige lading terug te winnen.

**API-indeling**

```http
POST /metrics
```

**Verzoek**

```sh
curl -X POST \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "start": "2020-07-14T00:00:00.000Z",
        "end": "2020-07-22T00:00:00.000Z",
        "granularity": "day",
        "metrics": [
          {
            "name": "timeseries.ingestion.dataset.recordsuccess.count",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
                "groupBy": true
              }
            ],
            "aggregator": "sum",
            "downsample": "sum"
          },
          {
            "name": "timeseries.ingestion.dataset.dailysize",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5eddb21420f516191b7a8dad",
                "groupBy": false
              }
            ],
            "aggregator": "sum",
            "downsample": "sum"
          }
        ]
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `start` | De vroegste datum/tijd waarvan om metrische gegevens terug te winnen. |
| `end` | De recentste datum/tijd waarvan om metrische gegevens terug te winnen. |
| `granularity` | Een optioneel veld waarmee het tijdsinterval wordt aangegeven waarbinnen metrische gegevens moeten worden verdeeld. Bijvoorbeeld, `DAY` keert een waarde van metriek voor elke dag tussen de `start` en `end` datum terug, terwijl een waarde van metrische resultaten door maand in plaats daarvan `MONTH` zou groeperen. Wanneer u dit veld gebruikt, moet ook een corresponderende `downsample` eigenschap worden opgegeven die de samenvoegfunctie aangeeft waarmee gegevens moeten worden gegroepeerd. |
| `metrics` | Een array van objecten, één voor elke metrische waarde die u wilt ophalen. |
| `name` | De naam van een metrische waarde die wordt erkend door Observability Insights. Zie het [bijlage](#available-metrics) voor een volledige lijst van toegelaten metrische namen. |
| `filters` | Een facultatief gebied dat u toestaat om metriek door specifieke datasets te filtreren. Het veld is een array van objecten (één voor elk filter), waarbij elk object de volgende eigenschappen bevat: <ul><li>`name`: Het type entiteit waarop maatgegevens moeten worden gefilterd. Momenteel wordt alleen `dataSets` ondersteund.</li><li>`value`: De id van een of meer gegevenssets. De veelvoudige dataset IDs kan als één enkel koord worden verstrekt, met elke identiteitskaart die door verticale barkarakters (`|`) wordt gescheiden.</li><li>`groupBy`: Wanneer geplaatst aan waar, wijst erop dat het corresponderen veelvoudige datasets `value` vertegenwoordigt de waarvan metrische resultaten afzonderlijk zouden moeten zijn teruggekeerd. Indien ingesteld op false, worden de metrische resultaten voor die datasets gegroepeerd.</li></ul> |
| `aggregator` | Geeft de aggregatiefunctie aan die moet worden gebruikt om records met meerdere tijdreeksen te groeperen in één resultaat. Raadpleeg de [OpenTSDB-documentatie](http://opentsdb.net/docs/build/html/user_guide/query/aggregators.html)voor gedetailleerde informatie over beschikbare aggregators. |
| `downsample` | Een optioneel veld waarmee u een samenvoegfunctie kunt opgeven om de bemonsteringsfrequentie van metrische gegevens te verminderen door velden in intervallen te sorteren (of &quot;emmers&quot;). Het interval voor downsampling wordt bepaald door het `granularity` bezit. Raadpleeg de [OpenTSDB-documentatie](http://opentsdb.net/docs/build/html/user_guide/query/downsampling.html)voor gedetailleerde informatie over downsampling. |

**Antwoord**

Een succesvolle reactie keert de resulterende datapoints voor de metriek en de filters terug die in het verzoek worden gespecificeerd.

```json
{
  "metricResponses": [
    {
      "metric": "timeseries.ingestion.dataset.recordsuccess.count",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
          "groupBy": true
        }
      ],
      "datapoints": [
        {
          "groupBy": {
            "dataSetId": "5edcfb2fbb642119194c7d94"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        },
        {
          "groupBy": {
            "dataSetId": "5eddb21420f516191b7a8dad"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        }
      ],
      "granularity": "DAY"
    },
    {
      "metric": "timeseries.ingestion.dataset.dailysize",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5eddb21420f516191b7a8dad",
          "groupBy": false
        }
      ],
      "datapoints": [
        {
          "groupBy": {},
          "dps": {
            "2020-07-14T00:00:00Z": 38455.0,
            "2020-07-15T00:00:00Z": 40213.0,
            "2020-07-16T00:00:00Z": 31476.0,
            "2020-07-17T00:00:00Z": 43705.0,
            "2020-07-18T00:00:00Z": 33227.0,
            "2020-07-19T00:00:00Z": 34977.0,
            "2020-07-20T00:00:00Z": 36735.0,
            "2020-07-21T00:00:00Z": 36737.0,
            "2020-07-22T00:00:00Z": 43715.0
          }
        }
      ],
      "granularity": "DAY"
    }
  ]
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `metricResponses` | Een array waarvan de objecten elk van de metriek vertegenwoordigen die in de aanvraag is opgegeven. Elk object bevat informatie over de filterconfiguratie en heeft metrische gegevens geretourneerd. |
| `metric` | De naam van een van de metriek die in de aanvraag wordt opgegeven. |
| `filters` | De filterconfiguratie voor gespecificeerde metrisch. |
| `datapoints` | Een array waarvan de objecten de resultaten van de opgegeven metrische waarde en filters vertegenwoordigen. Het aantal objecten in de array is afhankelijk van de filteropties in de aanvraag. Als er geen filters zijn opgegeven, bevat de array slechts één object dat alle gegevenssets vertegenwoordigt. |
| `groupBy` | Als de veelvoudige datasets in het `filter` bezit voor metrisch werden gespecificeerd, en de `groupBy` optie werd geplaatst aan waar in het verzoek, zal dit voorwerp identiteitskaart van de dataset bevatten die het overeenkomstige `dps` bezit op van toepassing is.<br><br>Als dit object leeg lijkt in de reactie, is de corresponderende `dps` eigenschap van toepassing op alle gegevenssets die in de `filters` array zijn opgenomen (of op alle gegevenssets waarin [!DNL Platform] als er geen filters zijn opgegeven). |
| `dps` | De teruggekeerde gegevens voor bepaalde metrisch, filter, en tijdwaaier. Elke sleutel in dit object vertegenwoordigt een tijdstempel met een overeenkomende waarde voor de opgegeven metrische waarde. De tijdspanne tussen elke datapoint hangt van de `granularity` waarde af die in het verzoek wordt gespecificeerd. |

## Aanhangsel

De volgende sectie bevat extra informatie over het werken met het `/metrics` eindpunt.

### Beschikbare cijfers {#available-metrics}

De volgende lijsten maken een lijst van alle metriek die door [!DNL Observability Insights], uitgesplitst door de [!DNL Platform] dienst worden blootgesteld. Elke metrische waarde bevat een beschrijving en geaccepteerde ID-queryparameter.

>[!NOTE]
>
>Alle vermelde ID-queryparameters zijn optioneel, tenzij anders vermeld.

#### [!DNL Data Ingestion] {#ingestion}

In de volgende tabel worden de maatstaven voor Adobe Experience Platform [!DNL Data Ingestion]weergegeven. Metriek in **vet** zijn streaming ingestion metrics.

| Metrische informatie | Beschrijving | ID-queryparameter |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | Het totale aantal gemaakte gegevenssets. | N.v.t. |
| timeseries.ingestion.dataset.size | Cumulatieve grootte van alle gegevens die voor één dataset voor of alle datasets worden opgenomen. | Dataset-id |
| timeseries.ingestion.dataset.dailysize | Grootte van gegevens die op een dagelijkse gebruiksbasis voor één dataset of voor alle datasets worden opgenomen. | Dataset-id |
| timeseries.ingestion.dataset.batchfailed.count | Aantal ontbroken partijen voor één dataset of voor alle datasets. | Dataset-id |
| timeseries.ingestion.dataset.batchsuccess.count | Aantal partijen die voor één dataset of voor alle datasets worden opgenomen. | Dataset-id |
| timeseries.ingestion.dataset.recordsuccess.count | Aantal verslagen die voor één dataset of voor alle datasets worden opgenomen. | Dataset-id |
| **timeseries.data.collection.validation.total.messages.rate** | Het totale aantal berichten voor één dataset of voor alle datasets. | Dataset-id |
| **timeseries.data.collection.validation.valid.messages.rate** | Het totale aantal geldige berichten voor één dataset of voor alle datasets. | Dataset-id |
| **timeseries.data.collection.validation.invalid.messages.rate** | Het totale aantal ongeldige berichten voor één dataset of voor alle datasets. | Dataset-id |
| **timeseries.data.collection.validation.category.type.count** | Het totale aantal ongeldige &quot;type&quot;berichten voor één dataset of voor alle datasets. | Dataset-id |
| **timeseries.data.collection.validation.category.range.count** | Het totale aantal ongeldige &quot;waaier&quot;berichten voor één dataset of voor alle datasets. | Dataset-id |
| **timeseries.data.collection.validation.category.format.count** | Het totale aantal ongeldige &quot;formaat&quot;berichten voor één dataset of voor alle datasets. | Dataset-id |
| **timeseries.data.collection.validation.category.pattern.count** | Het totale aantal ongeldige &quot;patroon&quot;berichten voor één dataset of voor alle datasets. | Dataset-id |
| **timeseries.data.collection.validation.category.presence.count** | Het totale aantal ongeldige &quot;aanwezigheid&quot;berichten voor één dataset of voor alle datasets. | Dataset-id |
| **timeseries.data.collection.validation.category.enum.count** | Het totale aantal ongeldige &quot;enum&quot;berichten voor één dataset of voor alle datasets. | Dataset-id |
| **timeseries.data.collection.validation.category.unclassi.count** | Het totale aantal ongeldige &quot;niet-geclassificeerde&quot;berichten voor één dataset of voor alle datasets. | Dataset-id |
| **timeseries.data.collection.validation.category.unknown.count** | Het totale aantal ongeldige &quot;onbekende&quot;berichten voor één dataset of voor alle datasets. | Dataset-id |
| **timeseries.data.collection.inlet.total.messages.receive** | Het totale aantal berichten dat voor één gegevensinlaat of voor alle gegevensinlaten wordt ontvangen. | Inlet-id |
| **timeseries.data.collection.inlet.total.messages.size.receive** | Totale grootte van gegevens die voor één gegevensinlaat of voor alle gegevensinlaten worden ontvangen. | Inlet-id |
| **timeseries.data.collection.inlet.success** | Het totale aantal geslaagde HTTP-aanroepen naar één gegevensinlaat of naar alle gegevensinlaten. | Inlet-id |
| **timeseries.data.collection.inlet.failure** | Het totale aantal mislukte HTTP-aanroepen naar één gegevensinlaat of naar alle gegevensinlaten. | Inlet-id |

#### [!DNL Identity Service] {#identity}

In de volgende tabel worden de maatstaven voor Adobe Experience Platform [!DNL Identity Service]weergegeven.

| Metrische informatie | Beschrijving | ID-queryparameter |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Aantal verslagen die aan hun gegevensbron door [!DNL Identity Service], voor één dataset of alle datasets worden geschreven. | Dataset-id |
| timeseries.identity.dataset.recordfailed.count | Aantal verslagen ontbrak door [!DNL Identity Service], voor één dataset of voor alle datasets. | Dataset-id |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Aantal identiteitsrecords dat is ingevoerd voor een naamruimte. | Naamruimte-id (**vereist**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Aantal identiteitsrecords dat is mislukt door een naamruimte. | Naamruimte-id (**vereist**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Aantal identiteitsrecords dat door een naamruimte is overgeslagen. | Naamruimte-id (**vereist**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Aantal unieke identiteiten dat is opgeslagen in de identiteitsgrafiek voor uw IMS-organisatie. | N.v.t. |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Aantal unieke identiteiten die in de identiteitsgrafiek voor een namespace worden opgeslagen. | Naamruimte-id (**vereist**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | Aantal unieke grafiekidentiteiten die in de identiteitsgrafiek voor uw IMS Organisatie worden opgeslagen. | N.v.t. |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Aantal unieke identiteiten die in de identiteitsgrafiek voor uw IMS Organisatie voor een bepaalde grafieksterkte worden opgeslagen (&quot;onbekend&quot;, &quot;zwak&quot;, of &quot;sterk&quot;). | Grafieksterkte (**vereist**) |

#### [!DNL Privacy Service] {#privacy}

In de volgende tabel worden de maatstaven voor Adobe Experience Platform [!DNL Privacy Service]weergegeven.

| Metrische informatie | Beschrijving | ID-queryparameter |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | Het totale aantal banen dat door de GDPR is gecreëerd. | ENV (**vereist**) |
| timeseries.gdpr.jobs.completedjobs.count | Totaal aantal voltooide banen van GDPR. | ENV (**vereist**) |
| timeseries.gdpr.jobs.errorjobs.count | Totaal aantal fouttaken van GDPR. | ENV (**vereist**) |

#### [!DNL Query Service] {#query}

In de volgende tabel worden de maatstaven voor Adobe Experience Platform [!DNL Query Service]weergegeven.

| Metrische informatie | Beschrijving | ID-queryparameter |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | Het totale aantal eenmalige geplande query&#39;s. | N.v.t. |
| timeseries.queryservice.query.scheduledrecurring.count | Het totale aantal terugkerende geplande query&#39;s. | N.v.t. |
| timeseries.queryservice.query.batchquery.count | Het totale aantal uitgevoerde batchquery&#39;s. | N.v.t. |
| timeseries.queryservice.query.scheduledquery.count | Het totale aantal uitgevoerde geplande query&#39;s. | N.v.t. |
| timeseries.queryservice.query.interactivequery.count | Het totale aantal uitgevoerde interactieve query&#39;s. | N.v.t. |
| timeseries.queryservice.query.batchfrompsqlquery.count | Het totale aantal uitgevoerde batchquery&#39;s van PSQL. | N.v.t. |

#### [!DNL Real-time Customer Profile] {#profile}

In de volgende tabel worden de metriek voor [!DNL Real-time Customer Profile].

| Metrische informatie | Beschrijving | ID-queryparameter |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Aantal verslagen die van [!DNL Data Lake] [!DNL Profile]door, voor één dataset of voor alle datasets worden gelezen. | Dataset-id |
| timeseries.profiles.dataset.recordsuccess.count | Aantal verslagen die aan hun gegevensbron door [!DNL Profile], voor één dataset of voor alle datasets worden geschreven. | Dataset-id |
| timeseries.profiles.dataset.recordfailed.count | Aantal verslagen ontbrak door [!DNL Profile], voor één dataset of voor alle datasets. | Dataset-id |
| timeseries.profiles.dataset.batchsuccess.count | Aantal [!DNL Profile] partijen die voor een dataset of voor alle datasets worden opgenomen. | Dataset-id |
| timeseries.profiles.dataset.batchfailed.count | Aantal ontbroken [!DNL Profile] partijen voor één dataset of voor alle datasets. | Dataset-id |
| platform.ups.ingest.streaming.request.m1_rate | Binnenkomend aanvraagpercentage. | IMS Org (**vereist**) |
| platform.ups.ingest.streaming.access.put.success.m1_rate | Ingestie succespercentage. | IMS Org (**vereist**) |
| platform.ups.ingest.streaming.records.created.m15_rate | Het tarief van nieuwe verslagen die voor een dataset worden opgenomen. | Gegevensset-id (**vereist**) |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | Het tarief van uit-van-orde timestamped verslagen voor creeer verzoek om een dataset. | Gegevensset-id (**vereist**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | Tijdstempel voor laatst maken recordverzoek voor een dataset. | Gegevensset-id (**vereist**) |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | Snelheid van tijdstempelde records zonder volgorde voor updateverzoek voor een dataset. | Gegevensset-id (**vereist**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | Tijdstempel voor laatste verzoek van updaterecord voor een gegevensset. | Gegevensset-id (**vereist**) |
| platform.ups.ingest.streaming.record.size.m1_rate | Gemiddelde recordgrootte. | IMS Org (**vereist**) |
| platform.ups.ingest.streaming.records.updated.m15_rate | Snelheid van updateverzoeken voor verslagen die voor een dataset worden opgenomen. | Gegevensset-id (**vereist**) |

### Foutberichten

De reacties van het `/metrics` eindpunt kunnen foutenmeldingen onder bepaalde voorwaarden terugkeren. Deze foutberichten worden in de volgende indeling geretourneerd:

```json
{
    "type": "http://ns.adobe.com/aep/errors/INSGHT-1000-400",
    "title": "Bad Request - Start date cannot be after end date.",
    "status": 400,
    "report": {
        "tenantInfo": {
            "sandboxName": "prod",
            "sandboxId": "49f58060-5d47-34rd-aawf-a5384333ff12",
            "imsOrgId": "{IMS_ORG}"
        },
        "additionalContext": null
    },
    "error-chain": [
        {
            "serviceId": "INSGHT",
            "errorCode": "INSGHT-1000-400",
            "invokingServiceId": "INSGHT",
            "unixTimeStampMs": 1602095177129
        }
    ]
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `title` | Een tekenreeks met het foutbericht en de mogelijke reden waarom het is opgetreden. |
| `report` | Bevat contextafhankelijke informatie over de fout, inclusief de sandbox en IMS Org die worden gebruikt in de bewerking die de fout heeft geactiveerd. |

In de volgende tabel worden de verschillende foutcodes weergegeven die door de API kunnen worden geretourneerd:

| Foutcode | Titel | Beschrijving |
| --- | --- | --- |
| `INSGHT-1000-400` | Ongeldige payload verzoek | Er is iets mis met de lading van de aanvraag. Zorg ervoor dat de ladingsopmaak exact overeenkomt met de [bovenstaande](#v2)weergave. Om het even welke mogelijke redenen kunnen deze fout teweegbrengen:<ul><li>Vereiste velden ontbreken, zoals `aggregator`</li><li>Ongeldige meetgegevens</li><li>De aanvraag bevat een ongeldige aggregator</li><li>Een begindatum vindt plaats na een einddatum</li></ul> |
| `INSGHT-1001-400` | Metrische query mislukt | Er is een fout opgetreden bij het zoeken naar de metrische database, omdat een onjuiste aanvraag of de query zelf niet kan worden gescheiden. Zorg ervoor dat uw verzoek correct is geformatteerd alvorens opnieuw te proberen. |
| `INSGHT-1001-500` | Metrische query mislukt | Er is een fout opgetreden tijdens het zoeken naar de metrieke-database vanwege een serverfout. Probeer het verzoek opnieuw. Neem contact op met de Adobe-ondersteuning als het probleem zich blijft voordoen. |
| `INSGHT-1002-500` | Servicefout | De aanvraag kan niet worden verwerkt vanwege een interne fout. Probeer het verzoek opnieuw. Neem contact op met de Adobe-ondersteuning als het probleem zich blijft voordoen. |
| `INSGHT-1003-401` | Validatiefout van sandbox | De aanvraag kan niet worden verwerkt vanwege een sandboxvalidatiefout. Zorg ervoor dat de naam van de sandbox die u in de `x-sandbox-name` header hebt opgegeven, een geldige, ingeschakelde sandbox voor uw IMS-organisatie vertegenwoordigt voordat u het verzoek opnieuw probeert. |
