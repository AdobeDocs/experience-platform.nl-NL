---
keywords: Experience Platform;home;populaire onderwerpen;datumbereik
title: Standaardwaarschuwingsregels
description: 'In dit document worden de vooraf gedefinieerde waarschuwingsregels van het Experience Platform besproken. '
source-git-commit: 8c00fb98a213b578f6970c1e1978f0159f8f38df
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 10%

---


# Standaardwaarschuwingsregels

Adobe Experience Platform biedt verschillende vooraf gedefinieerde waarschuwingsregels die u voor uw organisatie kunt inschakelen. In de onderstaande tabel worden de details van deze door Adobe verstrekte waarschuwingsregels besproken. Voor meer algemene informatie over alarm in Experience Platform, zie [alarm overzicht](./overview.md).

| Regel | Beschrijving | Evaluatiefrequentie | Herhaal venster |
| --- | --- | --- | --- |
| Titeldrempel overschreden | Deze waarschuwing treedt op wanneer het aantal gemaakte profielen meer dan 80% van de bevoegdheden van uw organisatie bedraagt. | 30 seconden | N.v.t. |
| Geen inname-activiteit in de afgelopen 24 uur | Deze waarschuwing treedt op wanneer geen nieuwe gegevens in de laatste periode van 24 uur zijn opgenomen. | 1 dag | 1 dag |
| SFTP-bron heeft geen gegevens opgenomen | Deze waarschuwing treedt op wanneer een [SFTP-bron](../../sources/connectors/cloud-storage/sftp.md) binnen een bepaalde tijdsperiode geen gegevens heeft ingevoerd. | 1 dag | 1 dag |
| Ingestiefout overschreden | Deze waarschuwing wordt geactiveerd wanneer de foutsnelheid voor het invoeren van gegevens hoger is dan 20%. | 30 seconden | 30 seconden |
| Feed-bericht | Deze waarschuwing wanneer een bericht van het delen van identiteit naar een gebruiker is verzonden gebruikend [Segment Match](../../segmentation/ui/segment-match.md). | N.v.t. | N.v.t. |
| Toegang tot feed ingetrokken | Deze waarschuwing wordt geactiveerd wanneer een andere gebruiker van het Platform de toegang tot een feed voor het delen van identiteiten intrekt met [Segmentovereenkomst](../../segmentation/ui/segment-match.md). | N.v.t. | N.v.t. |
| Diervoeders gewijzigd | Deze waarschuwing wordt geactiveerd wanneer een feed voor het delen van identiteiten door een gebruiker wordt gewijzigd met [Segment Match](../../segmentation/ui/segment-match.md). | N.v.t. | N.v.t. |
| Gedeelde feed | Deze waarschuwing wordt geactiveerd wanneer een gebruiker een nieuwe feed deelt in [Segment Match](../../segmentation/ui/segment-match.md). | N.v.t. | N.v.t. |
| Koppelingsverzoek | Deze waarschuwing treedt in werking wanneer een gebruiker om voor partner het delen verzoekt te verbinden. | N.v.t. | N.v.t. |
| Handeling voor koppeling | Deze waarschuwing treedt in werking wanneer een gebruiker een verzoek om voor partner het delen te verbinden goedkeurt. | N.v.t. | N.v.t. |
| Segmentdefinitie uitgeschakeld | Deze waarschuwing wordt geactiveerd wanneer een segmentdefinitie is uitgeschakeld. | N.v.t. | N.v.t. |
| Vertraging segmenttaak | Deze waarschuwing wordt geactiveerd wanneer het voltooien van segmenttaken langer duurt dan 150 minuten. | 30 seconden | 3 uur |
| Fout bij uitvoeren bronstroom | Deze waarschuwing treedt op wanneer een fout optreedt bij het opnemen van gegevens van een bronverbinding. | N.v.t. | N.v.t. |
| Resources Flow Run Success | Deze waarschuwing wordt geactiveerd wanneer gegevens zijn ingevoerd via een bronverbinding. | N.v.t. | N.v.t. |

{style=&quot;table-layout:auto&quot;}