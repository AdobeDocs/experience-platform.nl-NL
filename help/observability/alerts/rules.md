---
keywords: Experience Platform;home;populaire onderwerpen;datumbereik
title: Standaardwaarschuwingsregels
description: In dit document worden de vooraf gedefinieerde waarschuwingsregels van het Experience Platform besproken.
feature: Alerts
exl-id: b4af1c15-b1bc-4e4b-a447-09cc17a63988
source-git-commit: d82487f34c0879ed27ac55e42d70346f45806131
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 8%

---

# Standaardwaarschuwingsregels

Adobe Experience Platform biedt verschillende vooraf gedefinieerde waarschuwingsregels die u voor uw organisatie kunt inschakelen. In de onderstaande tabel worden de details van deze door Adobe verstrekte waarschuwingsregels besproken. Voor meer algemene informatie over alarm in Experience Platform, zie [alarm overzicht](./overview.md).

| Regel | Beschrijving | Evaluatiefrequentie | Herhaal venster |
| --- | --- | --- | --- |
| Resources Flow Run Success | Deze waarschuwing wordt geactiveerd wanneer gegevens zijn ingevoerd via een bronverbinding. | N.v.t. | N.v.t. |
| Fout bij uitvoeren bronstroom | Deze waarschuwing treedt op wanneer een fout optreedt bij het opnemen van gegevens van een bronverbinding. | N.v.t. | N.v.t. |
| Vertraging segmenttaak | Deze waarschuwing wordt geactiveerd wanneer het voltooien van segmenttaken langer duurt dan 150 minuten. | 30 seconden | 3 uur |
| Segmentdefinitie uitgeschakeld | Deze waarschuwing wordt geactiveerd wanneer een segmentdefinitie is uitgeschakeld. | N.v.t. | N.v.t. |

{style=&quot;table-layout:auto&quot;}

<!-- (Definitions to be added once available)
| Entitlement Threshold Exceeded | This alert triggers when the number of created profiles exceeds 80% of your organization's entitlement. | 30 seconds | N/A |
| No ingestion activity in past 24 hours | This alert triggers when no new data has been ingested in the last 24-hour period. | 1 day | 1 day |
| SFTP source has not ingested data | This alert triggers when an [SFTP source](../../sources/connectors/cloud-storage/sftp.md) has not ingested any data within a certain time period. | 1 day | 1 day |
| Ingestion error rate exceeded | This alert triggers when the error rate for data ingestion exceeds 20%. | 30 seconds | 30 seconds |
| Feed Message | This alert when an identity sharing feed message has been sent to a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Access Revoked | This alert triggers when another Platform user revokes access to an identity sharing feed using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Modified | This alert triggers when an identity sharing feed is modified by a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Shared | This alert triggers when a user shares a new feed in [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Link Request | This alert triggers when a user requests to connect for partner sharing. | N/A | N/A |
| Link Action | This alert triggers when a user accepts a request to connect for partner sharing. | N/A | N/A |
-->
