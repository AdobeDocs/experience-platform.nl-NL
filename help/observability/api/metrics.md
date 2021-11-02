---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Metrics API Endpoint
topic-legacy: developer guide
description: Leer hoe u meetgegevens voor waarneembaarheid in Experience Platform ophaalt met behulp van de API Observability Insights.
exl-id: 08d416f0-305a-44e2-a2b7-d563b2bdd2d2
source-git-commit: 5c893d7c8c455c86c94cd311a20ce774abcf65e0
workflow-type: tm+mt
source-wordcount: '1866'
ht-degree: 1%

---

# Metrisch eindpunt

De metriek van de waarneming verstrekt inzicht in gebruiksstatistieken, historische tendensen, en prestatiesindicatoren voor diverse eigenschappen in Adobe Experience Platform. De `/metrics` in de [!DNL Observability Insights API] staat u toe om metrische gegevens voor de activiteit van uw organisatie in programmatically terug te winnen [!DNL Platform].

>[!NOTE]
>
>De vorige versie van het metrieke eindpunt (V1) is afgekeurd. Dit document richt zich uitsluitend op de huidige versie (V2). Voor details op het V1 eindpunt voor erfenisimplementaties, gelieve te verwijzen naar [API-referentie](https://www.adobe.io/experience-platform-apis/references/observability-insights/#operation/retrieveMetricsV1).

## Aan de slag

Het API-eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van het [[!DNL Observability Insights] API](https://www.adobe.io/experience-platform-apis/references/observability-insights/). Controleer voordat je doorgaat de [gids Aan de slag](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document en belangrijke informatie betreffende vereiste kopballen die nodig zijn om met succes vraag aan om het even welk [!DNL Experience Platform] API.

## Metrische waarden voor waarneembaarheid ophalen

U kunt metrische gegevens terugwinnen door een verzoek van de POST aan `/metrics` eindpunt, die de metriek specificeren u in de nuttige lading wenst terug te winnen.

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
| `granularity` | Een optioneel veld waarmee het tijdsinterval wordt aangegeven waarbinnen metrische gegevens moeten worden verdeeld. Bijvoorbeeld een waarde van `DAY` retourneert meetgegevens voor elke dag tussen de `start` en `end` date, terwijl de waarde `MONTH` zou metrische resultaten door maand in plaats daarvan groeperen. Als u dit veld gebruikt, wordt een corresponderende `downsample` er moet ook een eigenschap worden verstrekt om de aggregatiefunctie aan te geven waarmee gegevens moeten worden gegroepeerd. |
| `metrics` | Een array van objecten, één voor elke metrische waarde die u wilt ophalen. |
| `name` | De naam van een metrische waarde die wordt erkend door Observability Insights. Zie de [aanhangsel](#available-metrics) voor een volledige lijst van toegelaten metrische namen. |
| `filters` | Een facultatief gebied dat u toestaat om metriek door specifieke datasets te filtreren. Het veld is een array van objecten (één voor elk filter), waarbij elk object de volgende eigenschappen bevat: <ul><li>`name`: Het type entiteit waarop maatgegevens moeten worden gefilterd. Alleen `dataSets` wordt ondersteund.</li><li>`value`: De id van een of meer gegevenssets. De veelvoudige dataset IDs kan als één enkel koord worden verstrekt, met elke identiteitskaart die door verticale barkarakters ( wordt gescheiden`\|`).</li><li>`groupBy`: Wanneer ingesteld op true, wordt hiermee aangegeven dat de corresponderende `value` vertegenwoordigt veelvoudige datasets de waarvan metrische resultaten afzonderlijk zouden moeten zijn teruggekeerd. Indien ingesteld op false, worden de metrische resultaten voor die datasets gegroepeerd.</li></ul> |
| `aggregator` | Geeft de aggregatiefunctie aan die moet worden gebruikt om records met meerdere tijdreeksen te groeperen in één resultaat. Voor gedetailleerde informatie over beschikbare aggregators, verwijs naar [OpenTSDB-documentatie](http://opentsdb.net/docs/build/html/user_guide/query/aggregators.html). |
| `downsample` | Een optioneel veld waarmee u een samenvoegfunctie kunt opgeven om de bemonsteringsfrequentie van metrische gegevens te verminderen door velden in intervallen te sorteren (of &quot;emmers&quot;). Het interval voor downsampling wordt bepaald door `granularity` eigenschap. Voor gedetailleerde informatie over downsampling raadpleegt u de [OpenTSDB-documentatie](http://opentsdb.net/docs/build/html/user_guide/query/downsampling.html). |

{style=&quot;table-layout:auto&quot;}

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
| `groupBy` | Als er meerdere gegevenssets zijn opgegeven in het dialoogvenster `filter` eigenschap voor metrisch en `groupBy` optie is ingesteld op true in het verzoek, dit object bevat de id van de dataset die de overeenkomstige `dps` eigenschap is van toepassing op.<br><br>Als dit object leeg wordt weergegeven in het antwoord, wordt het corresponderende `dps` eigenschap is van toepassing op alle gegevenssets die in de `filters` array (of alle gegevenssets in [!DNL Platform] als er geen filters zijn opgegeven). |
| `dps` | De teruggekeerde gegevens voor bepaalde metrisch, filter, en tijdwaaier. Elke sleutel in dit object vertegenwoordigt een tijdstempel met een overeenkomende waarde voor de opgegeven metrische waarde. De tijdperiode tussen elke datapoint is afhankelijk van `granularity` in de aanvraag opgegeven waarde. |

{style=&quot;table-layout:auto&quot;}

## Aanhangsel

De volgende sectie bevat aanvullende informatie over het werken met de `/metrics` eindpunt.

### Beschikbare cijfers {#available-metrics}

In de volgende tabellen worden alle metriek weergegeven die worden weergegeven door [!DNL Observability Insights], uitgesplitst naar [!DNL Platform] service. Elke metrische waarde bevat een beschrijving en geaccepteerde ID-queryparameter.

>[!NOTE]
>
>Alle vermelde ID-queryparameters zijn optioneel, tenzij anders vermeld.

#### [!DNL Data Ingestion] {#ingestion}

In de volgende tabel worden de maatstaven voor Adobe Experience Platform weergegeven [!DNL Data Ingestion]. Metrische gegevens in **vet** zijn streamingcijfers.

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

{style=&quot;table-layout:auto&quot;}

#### [!DNL Identity Service] {#identity}

In de volgende tabel worden de maatstaven voor Adobe Experience Platform weergegeven [!DNL Identity Service].

| Metrische informatie | Beschrijving | ID-queryparameter |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Aantal records dat naar de gegevensbron is geschreven door [!DNL Identity Service]voor één gegevensset of alle gegevensreeksen. | Dataset-id |
| timeseries.identity.dataset.recordfailed.count | Aantal records mislukt door [!DNL Identity Service]voor één gegevensset of voor alle gegevensreeksen. | Dataset-id |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Aantal identiteitsrecords dat is ingevoerd voor een naamruimte. | Namespace-id (**Vereist**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Aantal identiteitsrecords dat is mislukt door een naamruimte. | Namespace-id (**Vereist**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Aantal identiteitsrecords dat door een naamruimte is overgeslagen. | Namespace-id (**Vereist**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Aantal unieke identiteiten dat is opgeslagen in de identiteitsgrafiek voor uw IMS-organisatie. | N.v.t. |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Aantal unieke identiteiten die in de identiteitsgrafiek voor een namespace worden opgeslagen. | Namespace-id (**Vereist**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | Aantal unieke grafiekidentiteiten die in de identiteitsgrafiek voor uw IMS Organisatie worden opgeslagen. | N.v.t. |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Aantal unieke identiteiten die in de identiteitsgrafiek voor uw IMS Organisatie voor een bepaalde grafieksterkte worden opgeslagen (&quot;onbekend&quot;, &quot;zwak&quot;, of &quot;sterk&quot;). | Grafieksterkte (**Vereist**) |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Privacy Service] {#privacy}

In de volgende tabel worden de maatstaven voor Adobe Experience Platform weergegeven [!DNL Privacy Service].

| Metrische informatie | Beschrijving | ID-queryparameter |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | Het totale aantal banen dat door de GDPR is gecreëerd. | ENV (**Vereist**) |
| timeseries.gdpr.jobs.completedjobs.count | Totaal aantal voltooide banen van GDPR. | ENV (**Vereist**) |
| timeseries.gdpr.jobs.errorjobs.count | Totaal aantal fouttaken van GDPR. | ENV (**Vereist**) |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Query Service] {#query}

In de volgende tabel worden de maatstaven voor Adobe Experience Platform weergegeven [!DNL Query Service].

| Metrische informatie | Beschrijving | ID-queryparameter |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | Het totale aantal eenmalige geplande query&#39;s. | N.v.t. |
| timeseries.queryservice.query.scheduledrecurring.count | Het totale aantal terugkerende geplande query&#39;s. | N.v.t. |
| timeseries.queryservice.query.batchquery.count | Het totale aantal uitgevoerde batchquery&#39;s. | N.v.t. |
| timeseries.queryservice.query.scheduledquery.count | Het totale aantal uitgevoerde geplande query&#39;s. | N.v.t. |
| timeseries.queryservice.query.interactivequery.count | Het totale aantal uitgevoerde interactieve query&#39;s. | N.v.t. |
| timeseries.queryservice.query.batchfrompsqlquery.count | Het totale aantal uitgevoerde batchquery&#39;s van PSQL. | N.v.t. |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Real-time Customer Profile] {#profile}

De volgende tabel bevat metriek voor [!DNL Real-time Customer Profile].

| Metrische informatie | Beschrijving | ID-queryparameter |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Aantal records dat is gelezen van de [!DNL Data Lake] door [!DNL Profile]voor één gegevensset of voor alle gegevensreeksen. | Dataset-id |
| timeseries.profiles.dataset.recordsuccess.count | Aantal records dat naar de gegevensbron is geschreven door [!DNL Profile]voor één gegevensset of voor alle gegevensreeksen. | Dataset-id |
| timeseries.profiles.dataset.recordfailed.count | Aantal records mislukt door [!DNL Profile]voor één gegevensset of voor alle gegevensreeksen. | Dataset-id |
| timeseries.profiles.dataset.batchsuccess.count | Aantal [!DNL Profile] partijen die voor een dataset of voor alle datasets worden opgenomen. | Dataset-id |
| timeseries.profiles.dataset.batchfailed.count | Aantal [!DNL Profile] batches zijn mislukt voor één gegevensset of voor alle gegevenssets. | Dataset-id |
| platform.ups.ingest.streaming.request.m1_rate | Binnenkomend aanvraagpercentage. | IMS Org (**Vereist**) |
| platform.ups.ingest.streaming.access.put.success.m1_rate | Ingestie succespercentage. | IMS Org (**Vereist**) |
| platform.ups.ingest.streaming.records.created.m15_rate | Het tarief van nieuwe verslagen die voor een dataset worden opgenomen. | Dataset-id (**Vereist**) |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | Het tarief van uit-van-orde timestamped verslagen voor creeer verzoek om een dataset. | Dataset-id (**Vereist**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | Tijdstempel voor laatst maken recordverzoek voor een dataset. | Dataset-id (**Vereist**) |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | Snelheid van tijdstempelde records zonder volgorde voor updateverzoek voor een dataset. | Dataset-id (**Vereist**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | Tijdstempel voor laatste verzoek van updaterecord voor een gegevensset. | Dataset-id (**Vereist**) |
| platform.ups.ingest.streaming.record.size.m1_rate | Gemiddelde recordgrootte. | IMS Org (**Vereist**) |
| platform.ups.ingest.streaming.records.updated.m15_rate | Snelheid van updateverzoeken voor verslagen die voor een dataset worden opgenomen. | Dataset-id (**Vereist**) |

{style=&quot;table-layout:auto&quot;}

### Foutberichten

Reacties van de `/metrics` het eindpunt kan foutenmeldingen onder bepaalde voorwaarden terugkeren. Deze foutberichten worden in de volgende indeling geretourneerd:

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

{style=&quot;table-layout:auto&quot;}

In de volgende tabel worden de verschillende foutcodes weergegeven die door de API kunnen worden geretourneerd:

| Foutcode | Titel | Beschrijving |
| --- | --- | --- |
| `INSGHT-1000-400` | Ongeldige payload verzoek | Er is iets mis met de lading van de aanvraag. Zorg ervoor dat de ladingsopmaak exact overeenkomt met de weergave [boven](#v2). Om het even welke mogelijke redenen kunnen deze fout teweegbrengen:<ul><li>Vereiste velden ontbreken, zoals `aggregator`</li><li>Ongeldige meetgegevens</li><li>De aanvraag bevat een ongeldige aggregator</li><li>Een begindatum vindt plaats na een einddatum</li></ul> |
| `INSGHT-1001-400` | Metrische query mislukt | Er is een fout opgetreden bij het zoeken naar de metrische database, omdat een onjuiste aanvraag of de query zelf niet kan worden gescheiden. Zorg ervoor dat uw verzoek correct is geformatteerd alvorens opnieuw te proberen. |
| `INSGHT-1001-500` | Metrische query mislukt | Er is een fout opgetreden tijdens het zoeken naar de metrieke-database vanwege een serverfout. Probeer het verzoek opnieuw. Neem contact op met de Adobe-ondersteuning als het probleem zich blijft voordoen. |
| `INSGHT-1002-500` | Servicefout | De aanvraag kan niet worden verwerkt vanwege een interne fout. Probeer het verzoek opnieuw. Neem contact op met de Adobe-ondersteuning als het probleem zich blijft voordoen. |
| `INSGHT-1003-401` | Validatiefout van sandbox | De aanvraag kan niet worden verwerkt vanwege een sandboxvalidatiefout. Zorg ervoor dat de naam van de sandbox die u hebt opgegeven in het dialoogvenster `x-sandbox-name` vertegenwoordigt een geldige, ingeschakelde sandbox voor uw IMS-organisatie voordat u het verzoek opnieuw probeert. |

{style=&quot;table-layout:auto&quot;}
