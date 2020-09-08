---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Beschikbare cijfers
topic: developer guide
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 2%

---


# Metrisch eindpunt

De metriek van de waarneming verstrekt inzicht in gebruiksstatistieken, historische tendensen, en prestatiesindicatoren voor diverse eigenschappen in Adobe Experience Platform. Het `/metrics` eindpunt in [!DNL Observability Insights API] staat u toe om metrische gegevens voor de activiteit van uw organisatie binnen programmatically terug te winnen [!DNL Platform].

## Aan de slag

Het API-eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [[!DNL Observability Insights] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml). Lees voordat u verdergaat de gids [Aan de](./getting-started.md) slag voor koppelingen naar gerelateerde documentatie, een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document en belangrijke informatie over vereiste headers die nodig zijn om aanroepen naar een willekeurige [!DNL Experience Platform] API mogelijk te maken.

## Metrische waarden voor waarneembaarheid ophalen

U kunt de metriek van de waarneembaarheid terugwinnen door een verzoek van de GET tot het `/metrics` eindpunt in [!DNL Observability Insights] API te richten.

**API-indeling**

Wanneer het gebruiken van het `/metrics` eindpunt, moet minstens één metrische verzoekparameter worden verstrekt. Andere vraagparameters zijn facultatief voor het filtreren resultaten.

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
| `{ID}` | De id voor een bepaalde [!DNL Platform] bron waarvan u de meetgegevens wilt weergeven. Deze id kan optioneel, vereist of niet van toepassing zijn, afhankelijk van de gebruikte maatstaven. Zie de [bijlage](#available-metrics) voor een lijst van beschikbare metriek, evenals gesteunde IDs (zowel vereist als facultatief) voor elke metrisch. |
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