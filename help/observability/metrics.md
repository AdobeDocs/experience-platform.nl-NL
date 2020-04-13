---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Beschikbare cijfers
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a988c990d3d4df706a44cdbc82f77bef20c2ea1

---


# Lijst met beschikbare meetwaarden

De volgende lijsten maken een lijst van alle metriek die door de Inzichten van de Waarneming, uitgesplitst door de dienst van het Platform worden blootgesteld. Elke metrische waarde bevat een beschrijving en geaccepteerde ID-queryparameter.

## Gegevensinname

In de volgende tabel worden de metriek voor gegevensinname van het Adobe Experience Platform beschreven. Metriek in **vet** zijn streaming ingestion metrics.

| Metrische informatie | Beschrijving | ID-queryparameter |
| ---- | ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | Het totale aantal gemaakte gegevenssets. | N.v.t. |
| timeseries.ingestion.dataset.size | Cumulatieve grootte van alle gegevens die voor één dataset voor of alle datasets worden opgenomen. | Gegevensset-id (optioneel) |
| timeseries.ingestion.dataset.dailysize | Grootte van gegevens die op een dagelijkse gebruiksbasis voor één dataset of voor alle datasets worden opgenomen. | Gegevensset-id (optioneel) |
| timeseries.ingestion.dataset.batchfailed.count | Aantal ontbroken partijen voor één dataset of voor alle datasets. | Gegevensset-id (optioneel) |
| timeseries.ingestion.dataset.batchsuccess.count | Aantal partijen die voor één dataset of voor alle datasets worden opgenomen. | Gegevensset-id (optioneel) |
| timeseries.ingestion.dataset.recordsuccess.count | Aantal verslagen die voor één dataset of voor alle datasets worden opgenomen. | Gegevensset-id (optioneel) |
| **timeseries.data.collection.validation.total.messages.rate** | Het totale aantal berichten voor één dataset of voor alle datasets. | Gegevensset-id (optioneel) |
| **timeseries.data.collection.validation.valid.messages.rate** | Het totale aantal geldige berichten voor één dataset of voor alle datasets. | Gegevensset-id (optioneel) |
| **timeseries.data.collection.validation.invalid.messages.rate** | Het totale aantal ongeldige berichten voor één dataset of voor alle datasets. | Gegevensset-id (optioneel) |
| **timeseries.data.collection.validation.category.type.count** | Het totale aantal ongeldige &quot;type&quot;berichten voor één dataset of voor alle datasets. | Gegevensset-id (optioneel) |
| **timeseries.data.collection.validation.category.range.count** | Het totale aantal ongeldige &quot;waaier&quot;berichten voor één dataset of voor alle datasets. | Gegevensset-id (optioneel) |
| **timeseries.data.collection.validation.category.format.count** | Het totale aantal ongeldige &quot;formaat&quot;berichten voor één dataset of voor alle datasets. | Gegevensset-id (optioneel) |
| **timeseries.data.collection.validation.category.pattern.count** | Het totale aantal ongeldige &quot;patroon&quot;berichten voor één dataset of voor alle datasets. | Gegevensset-id (optioneel) |
| **timeseries.data.collection.validation.category.presence.count** | Het totale aantal ongeldige &quot;aanwezigheid&quot;berichten voor één dataset of voor alle datasets. | Gegevensset-id (optioneel) |
| **timeseries.data.collection.validation.category.enum.count** | Het totale aantal ongeldige &quot;enum&quot;berichten voor één dataset of voor alle datasets. | Gegevensset-id (optioneel) |
| **timeseries.data.collection.validation.category.unclassi.count** | Het totale aantal ongeldige &quot;niet-geclassificeerde&quot;berichten voor één dataset of voor alle datasets. | Gegevensset-id (optioneel) |
| **timeseries.data.collection.validation.category.unknown.count** | Het totale aantal ongeldige &quot;onbekende&quot;berichten voor één dataset of voor alle datasets. | Gegevensset-id (optioneel) |
| **timeseries.data.collection.inlet.total.messages.receive** | Het totale aantal berichten dat voor één gegevensinlaat of voor alle gegevensinlaten wordt ontvangen. | Inlaat-id (optioneel) |
| **timeseries.data.collection.inlet.total.messages.size.receive** | Totale grootte van gegevens die voor één gegevensinlaat of voor alle gegevensinlaten worden ontvangen. | Inlaat-id (optioneel) |
| **timeseries.data.collection.inlet.success** | Het totale aantal geslaagde HTTP-aanroepen naar één gegevensinlaat of naar alle gegevensinlaten. | Inlaat-id (optioneel) |
| **timeseries.data.collection.inlet.failure** | Het totale aantal mislukte HTTP-aanroepen naar één gegevensinlaat of naar alle gegevensinlaten. | Inlaat-id (optioneel) |

## Identiteitsservice

In de volgende tabel worden de metriek voor Adobe Experience Platform Identity Service beschreven.

| Metrische informatie | Beschrijving | ID-queryparameter |
| ---- | ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Aantal verslagen die aan hun gegevensbron door de Dienst van de Identiteit, voor één dataset of alle datasets worden geschreven. | Gegevensset-id (optioneel) |
| timeseries.identity.dataset.recordfailed.count | Aantal verslagen die door de Dienst van de Identiteit, voor één dataset of voor alle datasets worden ontbroken. | Gegevensset-id (optioneel) |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Aantal identiteitsrecords dat is ingevoerd voor een naamruimte. | Naamruimte-id (**vereist**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Aantal identiteitsrecords dat is mislukt door een naamruimte. | Naamruimte-id (**vereist**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Aantal identiteitsrecords dat door een naamruimte is overgeslagen. | Naamruimte-id (**vereist**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Aantal unieke identiteiten dat is opgeslagen in de identiteitsgrafiek voor uw IMS-organisatie. | N.v.t. |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Aantal unieke identiteiten die in de identiteitsgrafiek voor een namespace worden opgeslagen. | Naamruimte-id (**vereist**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | Aantal unieke grafiekidentiteiten die in de identiteitsgrafiek voor uw IMS Organisatie worden opgeslagen. | N.v.t. |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Aantal unieke identiteiten die in de identiteitsgrafiek voor uw IMS Organisatie voor een bepaalde grafieksterkte worden opgeslagen (&quot;onbekend&quot;, &quot;zwak&quot;, of &quot;sterk&quot;). | Grafieksterkte (**vereist**) |

## Privacy Service

In de volgende tabel worden de meetgegevens voor de Adobe Experience Platform Privacy Service weergegeven.

| Metrische informatie | Beschrijving | ID-queryparameter |
| ---- | ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | Het totale aantal banen dat door de GDPR is gecreëerd. | ENV (**vereist**) |
| timeseries.gdpr.jobs.completedjobs.count | Totaal aantal voltooide banen van GDPR. | ENV (**vereist**) |
| timeseries.gdpr.jobs.errorjobs.count | Totaal aantal fouttaken van GDPR. | ENV (**vereist**) |

## Query-service

In de volgende tabel worden de metriek voor Adobe Experience Platform Query Service beschreven.

| Metrische informatie | Beschrijving | ID-queryparameter |
| ---- | ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | Het totale aantal eenmalige geplande query&#39;s. | N.v.t. |
| timeseries.queryservice.query.scheduledrecurring.count | Het totale aantal terugkerende geplande query&#39;s. | N.v.t. |
| timeseries.queryservice.query.batchquery.count | Het totale aantal uitgevoerde batchquery&#39;s. | N.v.t. |
| timeseries.queryservice.query.scheduledquery.count | Het totale aantal uitgevoerde geplande query&#39;s. | N.v.t. |
| timeseries.queryservice.query.interactivequery.count | Het totale aantal uitgevoerde interactieve query&#39;s. | N.v.t. |
| timeseries.queryservice.query.batchfrompsqlquery.count | Het totale aantal uitgevoerde batchquery&#39;s van PSQL. | N.v.t. |

## Klantprofiel in realtime

De volgende lijst schetst metriek voor het Profiel van de Klant in real time.

| Metrische informatie | Beschrijving | ID-queryparameter |
| ---- | ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Aantal verslagen die van het gegevensmeer door Profiel, voor één dataset of voor alle datasets worden gelezen. | Gegevensset-id (optioneel) |
| timeseries.profiles.dataset.recordsuccess.count | Aantal verslagen die aan hun gegevensbron door Profiel, voor één dataset of voor alle datasets worden geschreven. | Gegevensset-id (optioneel) |
| timeseries.profiles.dataset.recordfailed.count | Aantal verslagen door Profiel, voor één dataset of voor alle datasets ontbrak. | Gegevensset-id (optioneel) |
| timeseries.profiles.dataset.batchsuccess.count | Aantal partijen van het Profiel die voor een dataset of voor alle datasets worden opgenomen. | Gegevensset-id (optioneel) |
| timeseries.profiles.dataset.batchfailed.count | Het aantal batches van het profiel is mislukt voor één gegevensset of voor alle gegevenssets. | Gegevensset-id (optioneel) |
| platform.ups.ingest.streaming.request.m1_rate | Binnenkomend aanvraagpercentage. | IMS Org |
| platform.ups.ingest.streaming.access.put.success.m1_rate | Ingestie succespercentage. | IMS Org |
| platform.ups.ingest.streaming.records.created.m15_rate | Het tarief van nieuwe verslagen die voor een dataset worden opgenomen. | Dataset-id |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | Het tarief van uit-van-orde timestamped verslagen voor creeer verzoek om een dataset. | Dataset-id |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | Tijdstempel voor laatst maken recordverzoek voor een dataset. | Dataset-id |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | Snelheid van tijdstempelde records zonder volgorde voor updateverzoek voor een dataset. | Dataset-id |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | Tijdstempel voor laatste verzoek van updaterecord voor een gegevensset. | Dataset-id |
| platform.ups.ingest.streaming.record.size.m1_rate | Gemiddelde recordgrootte. | IMS Org |
| platform.ups.ingest.streaming.records.updated.m15_rate | Snelheid van updateverzoeken voor verslagen die voor een dataset worden opgenomen. | Dataset-id |
