---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Metrics API Endpoint
topic: developer guide
description: Leer hoe u meetgegevens voor waarneembaarheid in Experience Platform ophaalt met behulp van de API Observability Insights.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '2027'
ht-degree: 1%

---


# Metrisch eindpunt

De metriek van de waarneming verstrekt inzicht in gebruiksstatistieken, historische tendensen, en prestatiesindicatoren voor diverse eigenschappen in Adobe Experience Platform. Het `/metrics` eindpunt in [!DNL Observability Insights API] staat u toe om metrische gegevens voor de activiteit van uw organisatie in [!DNL Platform] programmatically terug te winnen.

## Aan de slag

Het API-eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [[!DNL Observability Insights] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml). Lees voordat u doorgaat de [Aan de slag-handleiding](./getting-started.md) voor koppelingen naar verwante documentatie, een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document en belangrijke informatie over vereiste headers die nodig zijn om aanroepen naar een [!DNL Experience Platform]-API te voltooien.

## Metrische waarden voor waarneembaarheid ophalen

Er zijn twee ondersteunde methoden voor het ophalen van metrische gegevens met behulp van de API:

* [Versie 1](#v1): Geef metrische gegevens op met behulp van queryparameters.
* [Versie 2](#v2): Geef filters op en pas ze toe op metrische getallen met behulp van een JSON-payload.

### Versie 1 {#v1}

U kunt metrische gegevens terugwinnen door een verzoek van de GET aan het `/metrics` eindpunt te doen, specificerend metriek door het gebruik van vraagparameters.

**API-indeling**

In de parameter `metric` moet ten minste één metrische waarde worden opgegeven. Andere vraagparameters zijn facultatief voor het filtreren resultaten.

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
| `{ID}` | De id voor een bepaalde [!DNL Platform]-bron waarvan u de metriek toegankelijk wilt maken. Deze id kan optioneel, vereist of niet van toepassing zijn, afhankelijk van de gebruikte maatstaven. Zie [appendix](#available-metrics) voor een lijst van beschikbare metriek, met inbegrip van ondersteunde IDs (zowel vereist als facultatief) voor elke metrisch. |
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

Een geslaagde reactie retourneert een lijst met objecten die elk een tijdstempel bevatten binnen de opgegeven `dateRange` en de bijbehorende waarden voor de metriek die zijn opgegeven in het aanvraagpad. Als `id` van een [!DNL Platform] middel in de verzoekweg inbegrepen is, zullen de resultaten slechts op die bepaalde bron van toepassing zijn. Als `id` wordt weggelaten, zullen de resultaten op alle toepasselijke middelen binnen uw IMS Organisatie van toepassing zijn.

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

U kunt metrieke gegevens terugwinnen door een POST verzoek aan het `/metrics` eindpunt te doen, specificerend de metriek u wenst om in de nuttige lading terug te winnen.

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
| `granularity` | Een optioneel veld waarmee het tijdsinterval wordt aangegeven waarbinnen metrische gegevens moeten worden verdeeld. Bijvoorbeeld, keert een waarde van `DAY` metriek voor elke dag tussen `start` en `end` datum terug, terwijl een waarde van `MONTH` metrische resultaten in plaats daarvan zou groeperen door maand. Wanneer u dit veld gebruikt, moet ook een corresponderende eigenschap `downsample` worden opgegeven om de samenvoegfunctie aan te geven waarmee gegevens moeten worden gegroepeerd. |
| `metrics` | Een array van objecten, één voor elke metrische waarde die u wilt ophalen. |
| `name` | De naam van een metrische waarde die wordt erkend door Observability Insights. Zie [appendix](#available-metrics) voor een volledige lijst van toegelaten metrische namen. |
| `filters` | Een facultatief gebied dat u toestaat om metriek door specifieke datasets te filtreren. Het veld is een array van objecten (één voor elk filter), waarbij elk object de volgende eigenschappen bevat: <ul><li>`name`: Het type entiteit waarop maatgegevens moeten worden gefilterd. Momenteel wordt alleen `dataSets` ondersteund.</li><li>`value`: De id van een of meer gegevenssets. De veelvoudige dataset IDs kan als één enkel koord worden verstrekt, met elke identiteitskaart die door verticale barkarakters (`|`) wordt gescheiden.</li><li>`groupBy`: Wanneer geplaatst aan waar, wijst erop dat het corresponderen veelvoudige datasets  `value` vertegenwoordigt de waarvan metrische resultaten afzonderlijk zouden moeten zijn teruggekeerd. Indien ingesteld op false, worden de metrische resultaten voor die datasets gegroepeerd.</li></ul> |
| `aggregator` | Geeft de aggregatiefunctie aan die moet worden gebruikt om records met meerdere tijdreeksen te groeperen in één resultaat. Raadpleeg de [OpenTSDB-documentatie](http://opentsdb.net/docs/build/html/user_guide/query/aggregators.html) voor gedetailleerde informatie over beschikbare aggregators. |
| `downsample` | Een optioneel veld waarmee u een samenvoegfunctie kunt opgeven om de bemonsteringsfrequentie van metrische gegevens te verminderen door velden in intervallen te sorteren (of &quot;emmers&quot;). Het interval voor het downsamplen wordt bepaald door de eigenschap `granularity`. Raadpleeg de [OpenTSDB-documentatie](http://opentsdb.net/docs/build/html/user_guide/query/downsampling.html) voor gedetailleerde informatie over downsampling. |

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
| `groupBy` | Als de veelvoudige datasets in het `filter` bezit voor metrisch werden gespecificeerd, en de `groupBy` optie werd geplaatst aan waar in het verzoek, zal dit voorwerp identiteitskaart van de dataset bevatten die het overeenkomstige `dps` bezit op van toepassing is.<br><br>Als dit object leeg lijkt in de reactie, is de corresponderende  `dps` eigenschap van toepassing op alle gegevenssets die in de  `filters` array zijn opgenomen (of op alle gegevenssets  [!DNL Platform] als er geen filters zijn opgegeven). |
| `dps` | De teruggekeerde gegevens voor bepaalde metrisch, filter, en tijdwaaier. Elke sleutel in dit object vertegenwoordigt een tijdstempel met een overeenkomende waarde voor de opgegeven metrische waarde. De tijdspanne tussen elke datapoint hangt van `granularity` waarde af in het verzoek wordt gespecificeerd die. |

## Aanhangsel

De volgende sectie bevat extra informatie over het werken met het `/metrics` eindpunt.

### Beschikbare cijfers {#available-metrics}

In de volgende tabellen worden alle metriek weergegeven die worden weergegeven door [!DNL Observability Insights], uitgesplitst op [!DNL Platform]-service. Elke metrische waarde bevat een beschrijving en geaccepteerde ID-queryparameter.

>[!NOTE]
>
>Alle vermelde ID-queryparameters zijn optioneel, tenzij anders vermeld.

#### [!DNL Data Ingestion] {#ingestion}

In de volgende tabel worden de metriek voor Adobe Experience Platform [!DNL Data Ingestion] weergegeven. Metrisch in **bold** zijn streaming ingestition metrics.

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

In de volgende tabel worden de metriek voor Adobe Experience Platform [!DNL Identity Service] weergegeven.

| Metrische informatie | Beschrijving | ID-queryparameter |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Aantal verslagen die aan hun gegevensbron door [!DNL Identity Service], voor één dataset of alle datasets worden geschreven. | Dataset-id |
| timeseries.identity.dataset.recordfailed.count | Aantal verslagen door [!DNL Identity Service], voor één dataset of voor alle datasets ontbroken. | Dataset-id |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Aantal identiteitsrecords dat is ingevoerd voor een naamruimte. | Naamruimte-id (**Required**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Aantal identiteitsrecords dat is mislukt door een naamruimte. | Naamruimte-id (**Required**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Aantal identiteitsrecords dat door een naamruimte is overgeslagen. | Naamruimte-id (**Required**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Aantal unieke identiteiten dat is opgeslagen in de identiteitsgrafiek voor uw IMS-organisatie. | N.v.t. |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Aantal unieke identiteiten die in de identiteitsgrafiek voor een namespace worden opgeslagen. | Naamruimte-id (**Required**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | Aantal unieke grafiekidentiteiten die in de identiteitsgrafiek voor uw IMS Organisatie worden opgeslagen. | N.v.t. |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Aantal unieke identiteiten die in de identiteitsgrafiek voor uw IMS Organisatie voor een bepaalde grafieksterkte worden opgeslagen (&quot;onbekend&quot;, &quot;zwak&quot;, of &quot;sterk&quot;). | Grafieksterkte (**Required**) |

#### [!DNL Privacy Service] {#privacy}

In de volgende tabel worden de metriek voor Adobe Experience Platform [!DNL Privacy Service] weergegeven.

| Metrische informatie | Beschrijving | ID-queryparameter |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | Het totale aantal banen dat door de GDPR is gecreëerd. | ENV (**Required**) |
| timeseries.gdpr.jobs.completedjobs.count | Totaal aantal voltooide banen van GDPR. | ENV (**Required**) |
| timeseries.gdpr.jobs.errorjobs.count | Totaal aantal fouttaken van GDPR. | ENV (**Required**) |

#### [!DNL Query Service] {#query}

In de volgende tabel worden de metriek voor Adobe Experience Platform [!DNL Query Service] weergegeven.

| Metrische informatie | Beschrijving | ID-queryparameter |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | Het totale aantal eenmalige geplande query&#39;s. | N.v.t. |
| timeseries.queryservice.query.scheduledrecurring.count | Het totale aantal terugkerende geplande query&#39;s. | N.v.t. |
| timeseries.queryservice.query.batchquery.count | Het totale aantal uitgevoerde batchquery&#39;s. | N.v.t. |
| timeseries.queryservice.query.scheduledquery.count | Het totale aantal uitgevoerde geplande query&#39;s. | N.v.t. |
| timeseries.queryservice.query.interactivequery.count | Het totale aantal uitgevoerde interactieve query&#39;s. | N.v.t. |
| timeseries.queryservice.query.batchfrompsqlquery.count | Het totale aantal uitgevoerde batchquery&#39;s van PSQL. | N.v.t. |

#### [!DNL Real-time Customer Profile] {#profile}

In de volgende tabel worden de metriek voor [!DNL Real-time Customer Profile] beschreven.

| Metrische informatie | Beschrijving | ID-queryparameter |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Aantal records die worden gelezen van [!DNL Data Lake] door [!DNL Profile], voor één dataset of voor alle datasets. | Dataset-id |
| timeseries.profiles.dataset.recordsuccess.count | Aantal verslagen die aan hun gegevensbron door [!DNL Profile], voor één dataset of voor alle datasets worden geschreven. | Dataset-id |
| timeseries.profiles.dataset.recordfailed.count | Aantal verslagen door [!DNL Profile], voor één dataset of voor alle datasets ontbroken. | Dataset-id |
| timeseries.profiles.dataset.batchsuccess.count | Aantal [!DNL Profile] partijen die voor een dataset of voor alle datasets worden opgenomen. | Dataset-id |
| timeseries.profiles.dataset.batchfailed.count | Aantal [!DNL Profile] ontbroken partijen voor één dataset of voor alle datasets. | Dataset-id |
| platform.ups.ingest.streaming.request.m1_rate | Binnenkomend aanvraagpercentage. | IMS Org (**Required**) |
| platform.ups.ingest.streaming.access.put.success.m1_rate | Ingestie succespercentage. | IMS Org (**Required**) |
| platform.ups.ingest.streaming.records.created.m15_rate | Het tarief van nieuwe verslagen die voor een dataset worden opgenomen. | Dataset-id (**Required**) |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | Het tarief van uit-van-orde timestamped verslagen voor creeer verzoek om een dataset. | Dataset-id (**Required**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | Tijdstempel voor laatst maken recordverzoek voor een dataset. | Dataset-id (**Required**) |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | Snelheid van tijdstempelde records zonder volgorde voor updateverzoek voor een dataset. | Dataset-id (**Required**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | Tijdstempel voor laatste verzoek van updaterecord voor een gegevensset. | Dataset-id (**Required**) |
| platform.ups.ingest.streaming.record.size.m1_rate | Gemiddelde recordgrootte. | IMS Org (**Required**) |
| platform.ups.ingest.streaming.records.updated.m15_rate | Snelheid van updateverzoeken voor verslagen die voor een dataset worden opgenomen. | Dataset-id (**Required**) |

### Foutberichten

Reacties van het `/metrics` eindpunt kunnen foutenmeldingen onder bepaalde voorwaarden terugkeren. Deze foutberichten worden in de volgende indeling geretourneerd:

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
| `INSGHT-1000-400` | Ongeldige payload verzoek | Er is iets mis met de lading van de aanvraag. Zorg ervoor dat u de ladingsformattering precies zoals getoond [hierboven ](#v2) aanpast. Om het even welke mogelijke redenen kunnen deze fout teweegbrengen:<ul><li>Vereiste velden ontbreken, zoals `aggregator`</li><li>Ongeldige meetgegevens</li><li>De aanvraag bevat een ongeldige aggregator</li><li>Een begindatum vindt plaats na een einddatum</li></ul> |
| `INSGHT-1001-400` | Metrische query mislukt | Er is een fout opgetreden bij het zoeken naar de metrische database, omdat een onjuiste aanvraag of de query zelf niet kan worden gescheiden. Zorg ervoor dat uw verzoek correct is geformatteerd alvorens opnieuw te proberen. |
| `INSGHT-1001-500` | Metrische query mislukt | Er is een fout opgetreden tijdens het zoeken naar de metrieke-database vanwege een serverfout. Probeer het verzoek opnieuw. Neem contact op met de Adobe-ondersteuning als het probleem zich blijft voordoen. |
| `INSGHT-1002-500` | Servicefout | De aanvraag kan niet worden verwerkt vanwege een interne fout. Probeer het verzoek opnieuw. Neem contact op met de Adobe-ondersteuning als het probleem zich blijft voordoen. |
| `INSGHT-1003-401` | Validatiefout van sandbox | De aanvraag kan niet worden verwerkt vanwege een sandboxvalidatiefout. Zorg ervoor dat de naam van de sandbox die u in de koptekst `x-sandbox-name` hebt opgegeven, een geldige, ingeschakelde sandbox voor uw IMS-organisatie vertegenwoordigt voordat u het verzoek opnieuw probeert. |
