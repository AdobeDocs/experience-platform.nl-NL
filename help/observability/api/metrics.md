---
keywords: Experience Platform;startpagina;populaire onderwerpen
solution: Experience Platform
title: Metrics API Endpoint
description: Leer hoe u meetgegevens voor waarneembaarheid in Experience Platform ophaalt met behulp van de API Observability Insights.
exl-id: 08d416f0-305a-44e2-a2b7-d563b2bdd2d2
source-git-commit: a029d503d37d7e705897ce8efca98674ccf21780
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 1%

---

# Metrisch eindpunt

De metriek van de waarneming verstrekt inzicht in gebruiksstatistieken, historische tendensen, en prestatiesindicatoren voor diverse eigenschappen in Adobe Experience Platform. Het `/metrics` eindpunt in [!DNL Observability Insights API] staat u toe om metrische gegevens voor de activiteit van uw organisatie in programmatically terug te winnen [!DNL Platform].

>[!NOTE]
>
>De vorige versie van het metrieke eindpunt (V1) is afgekeurd. Dit document richt zich uitsluitend op de huidige versie (V2). Voor details op het V1 eindpunt voor erfenisimplementaties, gelieve te verwijzen naar de [ API verwijzing ](https://www.adobe.io/experience-platform-apis/references/observability-insights/#operation/retrieveMetricsV1).

## Aan de slag

Het API eindpunt dat in deze gids wordt gebruikt maakt deel uit van [[!DNL Observability Insights]  API ](https://www.adobe.io/experience-platform-apis/references/observability-insights/). Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welke [!DNL Experience Platform] API met succes te maken.

## Metrische waarden voor waarneembaarheid ophalen

U kunt metrische gegevens terugwinnen door een verzoek van de POST aan het `/metrics` eindpunt te doen, specificerend de metriek u in de nuttige lading wenst terug te winnen.

**API formaat**

```http
POST /metrics
```

**Verzoek**

```sh
curl -X POST \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            "aggregator": "sum"
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
          }
        ]
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `start` | De vroegste datum/tijd waarvan om metrische gegevens terug te winnen. |
| `end` | De recentste datum/tijd waarvan om metrische gegevens terug te winnen. |
| `granularity` | Een optioneel veld waarmee het tijdsinterval wordt aangegeven waarbinnen metrische gegevens moeten worden verdeeld. De waarde `DAY` retourneert bijvoorbeeld meetgegevens voor elke dag tussen de datum `start` en `end` , terwijl de waarde `MONTH` de metrische resultaten per maand groepeert. |
| `metrics` | Een array van objecten, één voor elke metrische waarde die u wilt ophalen. |
| `name` | De naam van een metrische waarde die wordt erkend door Observability Insights. Zie [ bijlage ](#available-metrics) voor een volledige lijst van toegelaten metrische namen. |
| `filters` | Een facultatief gebied dat u toestaat om metriek door specifieke datasets te filtreren. Het veld is een array van objecten (één voor elk filter), waarbij elk object de volgende eigenschappen bevat: <ul><li>`name`: Het type entiteit waarop maatgegevens moeten worden gefilterd. Momenteel wordt alleen `dataSets` ondersteund.</li><li>`value`: De id van een of meer gegevenssets. De veelvoudige dataset IDs kan als één enkel koord worden verstrekt, met elke identiteitskaart die door verticale barkarakters (`\|`) wordt gescheiden.</li><li>`groupBy`: Wanneer ingesteld op true, geeft dit aan dat de corresponderende `value` meerdere gegevenssets vertegenwoordigt waarvan de metrische resultaten afzonderlijk moeten worden geretourneerd. Indien ingesteld op false, worden de metrische resultaten voor die datasets gegroepeerd.</li></ul> |
| `aggregator` | Geeft de aggregatiefunctie aan die moet worden gebruikt om records met meerdere tijdreeksen te groeperen in één resultaat. De huidige ondersteunde aggregators zijn min, max, sum en avg, afhankelijk van de definitie van de metrische waarde. |

{style="table-layout:auto"}

**Reactie**

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
| `groupBy` | Als er meerdere gegevenssets zijn opgegeven in de eigenschap `filter` voor een metrische waarde en de optie `groupBy` is ingesteld op true in de aanvraag, bevat dit object de id van de gegevensset waarop de overeenkomende eigenschap `dps` van toepassing is.<br><br> als dit voorwerp leeg in de reactie lijkt, is het overeenkomstige `dps` bezit op alle datasets van toepassing die in de `filters` serie worden verstrekt (of alle datasets in [!DNL Platform] als geen filters werden verstrekt). |
| `dps` | De teruggekeerde gegevens voor bepaalde metrisch, filter, en tijdwaaier. Elke sleutel in dit object vertegenwoordigt een tijdstempel met een overeenkomende waarde voor de opgegeven metrische waarde. De tijdsperiode tussen elke datapoint is afhankelijk van de `granularity` -waarde die in de aanvraag is opgegeven. |

{style="table-layout:auto"}

## Bijlage

De volgende sectie bevat aanvullende informatie over het werken met het `/metrics` eindpunt.

### Beschikbare cijfers {#available-metrics}

In de volgende tabellen worden alle metriek weergegeven die door [!DNL Observability Insights] worden weergegeven, uitgesplitst naar [!DNL Platform] -service. Elke metrische waarde bevat een beschrijving en geaccepteerde ID-queryparameter.

>[!NOTE]
>
>Alle vermelde ID-queryparameters zijn optioneel, tenzij anders vermeld.

#### [!DNL Data Ingestion] {#ingestion}

In de volgende tabel worden de metriek voor Adobe Experience Platform [!DNL Data Ingestion] weergegeven. De metriek in **gewaagd** stromen ingestivingsmetriek.

| Metrische informatie | Beschrijving | ID-queryparameter |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.size | Cumulatieve grootte van alle gegevens die voor één dataset voor of alle datasets worden opgenomen. | Dataset-id |
| timeseries.ingestion.dataset.dailysize | Grootte van gegevens die op een dagelijkse gebruiksbasis voor één dataset of voor alle datasets worden opgenomen. | Dataset-id |
| timeseries.ingestion.dataset.batchfailed.count | Aantal ontbroken partijen voor één dataset of voor alle datasets. | Dataset-id |
| timeseries.ingestion.dataset.batchsuccess.count | Aantal partijen die voor één dataset of voor alle datasets worden opgenomen. | Dataset-id |
| timeseries.ingestion.dataset.recordsuccess.count | Aantal verslagen die voor één dataset of voor alle datasets worden opgenomen. | Dataset-id |
| **timeseries.data.collection.validation.category.presence.count** | Het totale aantal ongeldige &quot;aanwezigheid&quot;berichten voor één dataset of voor alle datasets. | Dataset-id |
| **timeseries.data.collection.inlet.total.messages.receive** | Het totale aantal berichten dat voor één gegevensinlaat of voor alle gegevensinlaten wordt ontvangen. | Inlet-id |
| **timeseries.data.collection.inlet.total.messages.size.receive** | Totale grootte van ontvangen gegevens voor één gegevensinlaat of voor alle gegevensinlaten. | Inlet-id |
| **timeseries.data.collection.inlet.success** | Het totale aantal geslaagde HTTP-aanroepen naar één gegevensinlaat of naar alle gegevensinlaten. | Inlet-id |
| **timeseries.data.collection.inlet.failure** | Het totale aantal mislukte HTTP-aanroepen naar één gegevensinlaat of naar alle gegevensinlaten. | Inlet-id |

{style="table-layout:auto"}

#### [!DNL Identity Service] {#identity}

In de volgende tabel worden de metriek voor Adobe Experience Platform [!DNL Identity Service] weergegeven.

| Metrische informatie | Beschrijving | ID-queryparameter |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Het aantal records dat door [!DNL Identity Service] naar de gegevensbron is geschreven, voor één gegevensset of voor alle gegevenssets. | Dataset-id |
| timeseries.identity.dataset.recordfailed.count | Het aantal records dat door [!DNL Identity Service] is mislukt, voor één gegevensset of voor alle gegevenssets. | Dataset-id |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Aantal identiteitsrecords overgeslagen. | Organisatie-ID |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Aantal unieke identiteiten die in de identiteitsgrafiek voor uw organisatie worden opgeslagen. | N.v.t. |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Aantal unieke identiteiten die in de identiteitsgrafiek voor een namespace worden opgeslagen. | Identiteitskaart van Namespace (**Vereiste**) |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Aantal unieke identiteiten dat in de identiteitsgrafiek voor uw organisatie voor een bepaalde grafieksterkte wordt opgeslagen (&quot;onbekend&quot;, &quot;zwak&quot; of &quot;sterk&quot;). | De sterkte van de grafiek (**Vereiste**) |

{style="table-layout:auto"}

#### [!DNL Real-Time Customer Profile] {#profile}

In de volgende tabel worden de metriek voor [!DNL Real-Time Customer Profile] weergegeven.

| Metrische informatie | Beschrijving | ID-queryparameter |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Het aantal records dat wordt gelezen vanuit de [!DNL Data Lake] by [!DNL Profile] , voor één gegevensset of voor alle gegevenssets. | Dataset-id |
| timeseries.profiles.dataset.recordsuccess.count | Het aantal records dat door [!DNL Profile] naar de gegevensbron is geschreven, voor één gegevensset of voor alle gegevenssets. | Dataset-id |
| timeseries.profiles.dataset.batchsuccess.count | Aantal [!DNL Profile] partijen die voor een dataset of voor alle datasets worden opgenomen. | Dataset-id |

{style="table-layout:auto"}

### Foutberichten

Reacties van het `/metrics` eindpunt kunnen foutberichten onder bepaalde omstandigheden retourneren. Deze foutberichten worden als volgt weergegeven:

```json
{
    "type": "http://ns.adobe.com/aep/errors/INSGHT-1000-400",
    "title": "Bad Request - Start date cannot be after end date.",
    "status": 400,
    "report": {
        "tenantInfo": {
            "sandboxName": "prod",
            "sandboxId": "49f58060-5d47-34rd-aawf-a5384333ff12",
            "imsOrgId": "{ORG_ID}"
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
| `report` | Bevat contextuele informatie over de fout, met inbegrip van de zandbak en de organisatie die in de verrichting worden gebruikt die het teweegbracht. |

{style="table-layout:auto"}

In de volgende tabel worden de verschillende foutcodes weergegeven die door de API kunnen worden geretourneerd:

| Foutcode | Titel | Beschrijving |
| --- | --- | --- |
| `INSGHT-1000-400` | Ongeldige payload verzoek | Er is iets mis met de lading van de aanvraag. Zorg ervoor dat u precies het nuttige lading formatteren zoals getoond [ hierboven ](#v2) aanpast. Om het even welke mogelijke redenen kunnen deze fout teweegbrengen:<ul><li>Vereiste velden ontbreken, zoals `aggregator`</li><li>Ongeldige meetgegevens</li><li>De aanvraag bevat een ongeldige aggregator</li><li>Een begindatum vindt plaats na een einddatum</li></ul> |
| `INSGHT-1001-400` | Metrische query mislukt | Er is een fout opgetreden bij het zoeken naar de metrische database, omdat een onjuiste aanvraag of de query zelf niet kan worden gescheiden. Zorg ervoor dat uw verzoek correct is geformatteerd alvorens opnieuw te proberen. |
| `INSGHT-1001-500` | Metrische query mislukt | Er is een fout opgetreden tijdens het zoeken naar de metrieke-database vanwege een serverfout. Probeer het verzoek opnieuw. Neem contact op met de Adobe als het probleem zich blijft voordoen. |
| `INSGHT-1002-500` | Servicefout | De aanvraag kan niet worden verwerkt vanwege een interne fout. Probeer het verzoek opnieuw. Neem contact op met de Adobe als het probleem zich blijft voordoen. |
| `INSGHT-1003-401` | Validatiefout van sandbox | De aanvraag kan niet worden verwerkt vanwege een sandboxvalidatiefout. Zorg ervoor dat de naam van de sandbox die u in de header `x-sandbox-name` hebt opgegeven, een geldige, ingeschakelde sandbox voor uw organisatie vertegenwoordigt voordat u het verzoek opnieuw probeert. |

{style="table-layout:auto"}
