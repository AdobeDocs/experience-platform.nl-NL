---
keywords: Experience Platform;home;populaire onderwerpen;datumbereik
title: Standaardwaarschuwingsregels
description: In dit document worden de vooraf gedefinieerde waarschuwingsregels van het Experience Platform besproken.
feature: Alerts
exl-id: b4af1c15-b1bc-4e4b-a447-09cc17a63988
source-git-commit: f1098f5992068173f35cb1c53924a82df6996acb
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 0%

---

# Standaardwaarschuwingsregels

Adobe Experience Platform biedt verschillende vooraf gedefinieerde waarschuwingsregels die u voor uw organisatie kunt inschakelen. In dit document worden de bijzonderheden van deze door Adobe verstrekte waarschuwingsregels besproken. Voor meer algemene informatie over signaleringen in Experience Platform raadpleegt u de [waarschuwingsoverzicht](./overview.md).

Wanneer [het bekijken alarmregels in UI van het Platform](./ui.md), kunt u zich op elke regel afzonderlijk abonneren. Wanneer u zich abonneert op waarschuwingen via [I/O-gebeurtenismeldingen](./subscribe.md)De waarschuwingsregels zijn echter ingedeeld in verschillende abonnementspakketten. In de onderstaande tabellen wordt elke regel weergegeven met de corresponderende naam van het I/O-gebeurtenisabonnement.

## Gegevensinname

De volgende waarschuwingsregels gelden specifiek voor [Gegevensinname](../../ingestion/home.md) en  [bronnen](../../sources/home.md):

| Abonnement voor I/O-gebeurtenis | Alarmregel | Beschrijving |
| --- | --- | --- |
| Bron: Run-info | Bronnen Start Stroom | Deze waarschuwing wordt geactiveerd wanneer een bronverbinding gegevens begint te verwerken. |
| Bron: Run-info | Resources Flow Run Success | Deze waarschuwing wordt geactiveerd wanneer gegevens zijn ingevoerd via een bronverbinding. |
| Vertragingen, fouten en fouten bij uitvoering van bronstroom | Fout bij uitvoeren bronstroom | Deze waarschuwing treedt op wanneer een fout optreedt bij het opnemen van gegevens van een bronverbinding. |
| Vertragingen, fouten en fouten bij uitvoering van bronstroom | Vertraging bij inname | Deze waarschuwing wordt geactiveerd wanneer een batch-opname-flow langer duurt dan 150 minuten om te verwerken. |
| Vertragingen, fouten en fouten bij uitvoering van bronstroom | Gebrek aan vergisting | Deze waarschuwing stuurt u een bericht als de inname meer dan zeven uur wordt vertraagd en er geen gegevens aan het Platform worden gegeven. |
| Vertragingen, fouten en fouten bij uitvoering van bronstroom | Ingestief | Deze waarschuwing wordt geactiveerd wanneer de verhouding van mislukte records ten opzichte van alle records een drempel van 0,5% overschrijdt |

{style=&quot;table-layout:auto&quot;}

## Identiteitsservice

De volgende waarschuwingsregels gelden specifiek voor [Identiteitsservice](../../identity-service/home.md):

| Abonnement voor I/O-gebeurtenis | Alarmregel | Beschrijving |
| --- | --- | --- |
| Identiteitsinformatie | Start Identiteitsservicestroom | Deze waarschuwing treedt op wanneer een stroom van de Dienst van de Identiteit begint gegevens te verwerken. Met andere woorden, worden ingesloten gegevens geladen van het Datameer in de Dienst van de Identiteit. |
| Identiteitsinformatie | Workflow voor identiteitsservice | Deze waarschuwing wordt geactiveerd wanneer gegevens zijn geladen van het Data Lake naar Identity Service. |
| Vertragingen, fouten en fouten bij identiteitsverdenking | Vertraging bij uitvoering identiteitsservicestroom | Deze waarschuwing treedt in werking wanneer een stroom van de Dienst van de Identiteit duurt langer dan 150 minuten om te verwerken. |
| Vertragingen, fouten en fouten bij identiteitsverdenking | Fout bij uitvoeren van identiteitsservicestroom | Deze waarschuwing treedt op wanneer een fout optreedt bij het invoeren van gegevens in Identity Service. |

{style=&quot;table-layout:auto&quot;}

## Klantprofiel in realtime

De volgende waarschuwingsregels gelden specifiek voor [Klantprofiel in realtime](../../profile/home.md):

| Abonnement voor I/O-gebeurtenis | Alarmregel | Beschrijving |
| --- | --- | --- |
| Info over profielinsluiting | Start van profielstroom | Deze waarschuwing wordt geactiveerd wanneer een profielstroom wordt gestart met het verwerken van gegevens. |
| Info over profielinsluiting | Profielstroom is uitgevoerd | Deze waarschuwing wordt geactiveerd wanneer gegevens met succes worden geladen in Profiel van het Datameer. |
| Vertragingen, fouten en fouten bij het verwerken van profielen | Vertraging bij uitvoering van profielstroom | Deze waarschuwing wordt geactiveerd wanneer het laden van gegevens van het Data Lake in Profile langer duurt dan 150 minuten om te verwerken. |
| Vertragingen, fouten en fouten bij het verwerken van profielen | Fout bij uitvoeren van profielstroom | Deze waarschuwing treedt op wanneer een fout optreedt bij het opnemen van gegevens in het profiel. |

{style=&quot;table-layout:auto&quot;}

## Segmentatie

De volgende waarschuwingsregels gelden specifiek voor [Segmenteringsservice](../../segmentation/home.md):

| Abonnement voor I/O-gebeurtenis | Alarmregel | Beschrijving |
| --- | --- | --- |
| Informatie segmentevaluatie | Start segmenttaak | Deze waarschuwing treedt in werking wanneer een baan van de segmentevaluatie begint gegevens te verwerken. |
| Informatie segmentevaluatie | Segmenttaken voltooid | Deze waarschuwing treedt op wanneer een baan van de segmentevaluatie met succes voltooit. |
| Vertragingen, fouten en fouten bij de evaluatie van segmenten | Vertraging segmenttaak | Deze waarschuwing treedt in werking wanneer een segmentevaluatietaak langer duurt dan 150 minuten om te voltooien. |
| Vertragingen, fouten en fouten bij de evaluatie van segmenten | Fout in segmenttaak | Deze waarschuwing treedt in werking wanneer een baan van de segmentevaluatie in een fout resulteert. |
| Vertragingen, fouten en fouten bij de evaluatie van segmenten | Segmentdefinitie uitgeschakeld | Deze waarschuwing wordt geactiveerd wanneer een segmentdefinitie is uitgeschakeld als gevolg van een interne fout. Dit leidt automatisch tot een oorlogsruimte voor een technische team van Adobe om de kwestie te onderzoeken. Deze waarschuwing is alleen bedoeld als informatief en vereist geen actie van u. |

{style=&quot;table-layout:auto&quot;}

## Doelen

De volgende waarschuwingsregels gelden specifiek voor [bestemmingen](../../destinations/home.md):

| Abonnement voor I/O-gebeurtenis | Alarmregel | Beschrijving |
| --- | --- | --- |
| Run-info doelstroom | Start stroom bestemming | Deze waarschuwing activeert wanneer een bestemmingstroom begint een segment te activeren. |
| Run-info doelstroom | Uitvoersucces bestemming | Deze waarschuwing wordt geactiveerd wanneer een segment is geactiveerd naar een doel. |
| Vertragingen, fouten en fouten bij de uitvoering van de doelstroom | Uitvoervertraging bestemming | Deze waarschuwing wordt geactiveerd wanneer een doelstroom langer dan 150 minuten duurt om een segment te activeren. |
| Vertragingen, fouten en fouten bij de uitvoering van de doelstroom | Uitvoerfout bestemming | Deze waarschuwing wordt geactiveerd wanneer een fout optreedt tijdens het activeren van een segment op een doel. |

{style=&quot;table-layout:auto&quot;}

<!-- (Definitions to be added once available)
| Segment Job Delay | This alert triggers when a segment job takes longer than 150 minutes to complete. | N/A | 30 seconds | 3 hours |
| No Ingestion Activity in Past 24 Hours | This alert triggers when no new data has been ingested in the last 24-hour period. | N/A | 1 day | 1 day |
| Ingestion Error Rate Exceeded | This alert triggers when the error rate for data ingestion exceeds the allotted threshold. | 20% | 30 seconds | 30 seconds |
| Entitlement Threshold Exceeded | This alert triggers when the number of created profiles exceeds 80% of your organization's entitlement. | 30 seconds | N/A |
| SFTP source has not ingested data | This alert triggers when an [SFTP source](../../sources/connectors/cloud-storage/sftp.md) has not ingested any data within a certain time period. | 1 day | 1 day |
| Feed Message | This alert when an identity sharing feed message has been sent to a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Access Revoked | This alert triggers when another Platform user revokes access to an identity sharing feed using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Modified | This alert triggers when an identity sharing feed is modified by a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Shared | This alert triggers when a user shares a new feed in [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Link Request | This alert triggers when a user requests to connect for partner sharing. | N/A | N/A |
| Link Action | This alert triggers when a user accepts a request to connect for partner sharing. | N/A | N/A |
-->
