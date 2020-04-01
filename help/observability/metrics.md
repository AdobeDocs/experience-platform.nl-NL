---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Beschikbare cijfers
topic: developer guide
translation-type: tm+mt
source-git-commit: 947955403a270914437d9172bca458f9c49ccd8f

---


# Lijst met beschikbare meetwaarden

Hieronder volgt een lijst van metriek die door de Inzichten van de Waardigheid, elk met hun bijbehorende dienst van het Platform, beschrijving, en toegelaten identiteitskaart vraagparameter worden blootgesteld.

| Metrische informatie | Platformservice | Beschrijving | ID-queryparameter |
| ---- | ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | Gegevensinname | Het totale aantal gemaakte gegevenssets. | N.v.t. |
| timeseries.ingestion.dataset.size | Gegevensinname | Cumulatieve grootte van alle gegevens die voor één dataset voor of alle datasets worden opgenomen. | Gegevensset-id (optioneel) |
| timeseries.ingestion.dataset.dailysize | Gegevensinname | Grootte van gegevens die op een dagelijkse gebruiksbasis voor één dataset of voor alle datasets worden opgenomen. | Gegevensset-id (optioneel) |
| timeseries.ingestion.dataset.batchfailed.count | Gegevensinname | Aantal ontbroken partijen voor één dataset of voor alle datasets. | Gegevensset-id (optioneel) |
| timeseries.ingestion.dataset.batchsuccess.count | Gegevensinname | Aantal partijen die voor één dataset of voor alle datasets worden opgenomen. | Gegevensset-id (optioneel) |
| timeseries.ingestion.dataset.recordsuccess.count | Gegevensinname | Aantal verslagen die voor één dataset of voor alle datasets worden opgenomen. | Gegevensset-id (optioneel) |
| timeseries.data.collection.validation.total.messages.rate | Gegevensverwerking (streaming) | Het totale aantal berichten voor één dataset of voor alle datasets. | Gegevensset-id (optioneel) |
| timeseries.data.collection.validation.valid.messages.rate | Gegevensverwerking (streaming) | Het totale aantal geldige berichten voor één dataset of voor alle datasets. | Gegevensset-id (optioneel) |
| timeseries.data.collection.validation.invalid.messages.rate | Gegevensverwerking (streaming) | Het totale aantal ongeldige berichten voor één dataset of voor alle datasets. | Gegevensset-id (optioneel) |
| timeseries.data.collection.validation.category.type.count | Gegevensverwerking (streaming) | Het totale aantal ongeldige &quot;type&quot;berichten voor één dataset of voor alle datasets. | Gegevensset-id (optioneel) |
| timeseries.data.collection.validation.category.range.count | Gegevensverwerking (streaming) | Het totale aantal ongeldige &quot;waaier&quot;berichten voor één dataset of voor alle datasets. | Gegevensset-id (optioneel) |
| timeseries.data.collection.validation.category.format.count | Gegevensverwerking (streaming) | Het totale aantal ongeldige &quot;formaat&quot;berichten voor één dataset of voor alle datasets. | Gegevensset-id (optioneel) |
| timeseries.data.collection.validation.category.pattern.count | Gegevensverwerking (streaming) | Het totale aantal ongeldige &quot;patroon&quot;berichten voor één dataset of voor alle datasets. | Gegevensset-id (optioneel) |
| timeseries.data.collection.validation.category.presence.count | Gegevensverwerking (streaming) | Het totale aantal ongeldige &quot;aanwezigheid&quot;berichten voor één dataset of voor alle datasets. | Gegevensset-id (optioneel) |
| timeseries.data.collection.validation.category.enum.count | Gegevensverwerking (streaming) | Het totale aantal ongeldige &quot;enum&quot;berichten voor één dataset of voor alle datasets. | Gegevensset-id (optioneel) |
| timeseries.data.collection.validation.category.unclassi.count | Gegevensverwerking (streaming) | Het totale aantal ongeldige &quot;niet-geclassificeerde&quot;berichten voor één dataset of voor alle datasets. | Gegevensset-id (optioneel) |
| timeseries.data.collection.validation.category.unknown.count | Gegevensverwerking (streaming) | Het totale aantal ongeldige &quot;onbekende&quot;berichten voor één dataset of voor alle datasets. | Gegevensset-id (optioneel) |
| timeseries.data.collection.inlet.total.messages.receive | Gegevensverwerking (streaming) | Het totale aantal berichten dat voor één gegevensinlaat of voor alle gegevensinlaten wordt ontvangen. | Inlaat-id (optioneel) |
| timeseries.data.collection.inlet.total.messages.size.receive | Gegevensverwerking (streaming) | Totale grootte van gegevens die voor één gegevensinlaat of voor alle gegevensinlaten worden ontvangen. | Inlaat-id (optioneel) |
| timeseries.data.collection.inlet.success | Gegevensverwerking (streaming) | Het totale aantal geslaagde HTTP-aanroepen naar één gegevensinlaat of naar alle gegevensinlaten. | Inlaat-id (optioneel) |
| timeseries.data.collection.inlet.failure | Gegevensverwerking (streaming) | Het totale aantal mislukte HTTP-aanroepen naar één gegevensinlaat of naar alle gegevensinlaten. | Inlaat-id (optioneel) |
| timeseries.profiles.dataset.recordread.count | Klantprofiel in realtime | Aantal verslagen die van het gegevensmeer door Profiel, voor één dataset of voor alle datasets worden gelezen. | Gegevensset-id (optioneel) |
| timeseries.profiles.dataset.recordsuccess.count | Klantprofiel in realtime | Aantal verslagen die aan hun gegevensbron door Profiel, voor één dataset of voor alle datasets worden geschreven. | Gegevensset-id (optioneel) |
| timeseries.profiles.dataset.recordfailed.count | Klantprofiel in realtime | Aantal verslagen door Profiel, voor één dataset of voor alle datasets ontbrak. | Gegevensset-id (optioneel) |
| timeseries.profiles.dataset.batchsuccess.count | Klantprofiel in realtime | Aantal partijen van het Profiel die voor een dataset of voor alle datasets worden opgenomen. | Gegevensset-id (optioneel) |
| timeseries.profiles.dataset.batchfailed.count | Klantprofiel in realtime | Het aantal batches van het profiel is mislukt voor één gegevensset of voor alle gegevenssets. | Gegevensset-id (optioneel) |
| timeseries.identity.dataset.recordsuccess.count | Identiteitsservice | Aantal verslagen die aan hun gegevensbron door de Dienst van de Identiteit, voor één dataset of alle datasets worden geschreven. | Gegevensset-id (optioneel) |
| timeseries.identity.dataset.recordfailed.count | Identiteitsservice | Aantal verslagen die door de Dienst van de Identiteit, voor één dataset of voor alle datasets worden ontbroken. | Gegevensset-id (optioneel) |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Identiteitsservice | Aantal identiteitsrecords dat is ingevoerd voor een naamruimte. | Naamruimte-id (**vereist**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Identiteitsservice | Aantal identiteitsrecords dat is mislukt door een naamruimte. | Naamruimte-id (**vereist**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Identiteitsservice | Aantal identiteitsrecords dat door een naamruimte is overgeslagen. | Naamruimte-id (**vereist**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Identiteitsservice | Aantal unieke identiteiten dat is opgeslagen in de identiteitsgrafiek voor uw IMS-organisatie. | N.v.t. |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Identiteitsservice | Aantal unieke identiteiten die in de identiteitsgrafiek voor een namespace worden opgeslagen. | Naamruimte-id (**vereist**) |
| timeseries.identity.graph.imsorg.numidgraph.count | Identiteitsservice | Aantal unieke grafiekidentiteiten die in de identiteitsgrafiek voor uw IMS Organisatie worden opgeslagen. | N.v.t. |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Identiteitsservice | Aantal unieke identiteiten die in de identiteitsgrafiek voor uw IMS Organisatie voor een bepaalde grafieksterkte worden opgeslagen (&quot;onbekend&quot;, &quot;zwak&quot;, of &quot;sterk&quot;). | Grafieksterkte (**vereist**) |
| timeseries.gdpr.job.totaljobs.count | GDPR | Het totale aantal banen dat door de GDPR is gecreëerd. | ENV (**vereist**) |
| timeseries.gdpr.job.completeJob.count | GDPR | Totaal aantal voltooide banen van GDPR. | ENV (**vereist**) |
| timeseries.gdpr.job.errorjobs.count | GDPR | Totaal aantal fouttaken van GDPR. | ENV (**vereist**) |
| timeseries.query.query.plannuleonce.count | Query-service | Het totale aantal eenmalige geplande query&#39;s. | N.v.t. |
| timeseries.queryservice.query.plannuledrepeat.count | Query-service | Het totale aantal terugkerende geplande query&#39;s. | N.v.t. |
| timeseries.queryservice.query.batchquery.count | Query-service | Het totale aantal uitgevoerde batchquery&#39;s. | N.v.t. |
| timeseries.queryservice.query.plannuledquery.count | Query-service | Het totale aantal uitgevoerde geplande query&#39;s. | N.v.t. |
| timeseries.queryservice.query.interactivequery.count | Query-service | Het totale aantal uitgevoerde interactieve query&#39;s. | N.v.t. |
| timeseries.queryservice.query.batchfrompsqlquery.count | Query-service | Het totale aantal uitgevoerde batchquery&#39;s van PSQL. | N.v.t. |