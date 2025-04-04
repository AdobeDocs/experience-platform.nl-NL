---
title: Gegevenstype voor Media die gegevens rapporteren
description: Leer over Media die het gegevenstype van de Gegevens van de Ervaring van Gegevens van de Media melden Model (XDM).
exl-id: e8bf20a9-9ac0-4339-8200-5d6d9328ce3b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# [!UICONTROL Media Reporting Details] gegevenstype

>[!NOTE]
>
>De gebieden van de Inzameling van media vangen gegevens en verzenden het naar andere diensten van Adobe voor verdere verwerking. Media Reporting-velden worden door Adobe-services gebruikt voor het analyseren van de velden Media Collection die door gebruikers worden verzonden. Deze gegevens worden, samen met andere specifieke maatstaven voor gebruikers, berekend en gerapporteerd.

[!UICONTROL Media Reporting Details] is een standaard XDM-gegevenstype (Experience Data Model) waarmee essentiële gegevens over gebeurtenissen voor het afspelen van media worden vastgelegd. Gebruik het gegevenstype [!UICONTROL Media Reporting Details] om details vast te leggen, zoals de positie van de afspeelkop binnen de inhoud, unieke sessie-id&#39;s en verschillende geneste eigenschappen die onder andere betrekking hebben op de sessie. Dit gegevenstype biedt een uitgebreid overzicht van de afspeelervaring waarmee mediaconsumptiepatronen en bijbehorende gebeurtenissen tijdens afspeelsessies kunnen worden bijgehouden en geanalyseerd.

>[!NOTE]
>
>De onderstaande velden worden niet rechtstreeks gebruikt om aanvragen te maken. In plaats daarvan wordt de verzameling van velden die naar Adobe Experience Platform of Adobe Analytics worden verzonden, samengesteld op basis van uw aanvraaggegevens en worden metrische gegevens vervolgens opgenomen of verwerkt door de serverinfrastructuur. Hoewel Experience Platform verschillende typen gebruikersgebeurtenissen verzamelt, richten de geretourneerde rapporten zich op specifieke gebeurtenissen, zoals `media.sessionStart` , `media.adStart` en `media.sessionComplete` . Dit betekent dat hoewel u 12 types van gebeurtenissen tijdens inzameling overbrengt, uw rapporten slechts onderverdelingen zullen voorstellen die op de vijf hieronder vermelde gebeurtenissen worden gebaseerd.

++ + selecteren om een diagram van het gegevenstype [!UICONTROL Media Reporting Details] weer te geven.
![ een diagram van het [!UICONTROL Media Reporting Details] gegevenstype.](../images/data-types/media-reporting-details.png)
+++

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --------------------- | --------------- | --------- | ----------- |
| [!UICONTROL Advertising Details] | `advertisingDetails` | [[!UICONTROL advertisingDetails]](./advertising-details-reporting.md) | Advertising Details verwijzen naar specifieke informatie over reclameactiviteiten tijdens het ervaringsevenement. Dit zijn onder andere metagegevens voor advertenties, specificaties voor doelgroepen en prestatiewaarden. |
| [!UICONTROL Advertising Pod Details] | `advertisingPodDetails` | [[!UICONTROL advertisingPodDetails]](./advertising-pod-details-reporting.md) | Advertising Pod Details bevatten informatie over advertentiepods binnen de Experience Event. Het biedt inzichten in de volgorde van de advertenties, de inhoud en de betrokkenheidsmetriek. |
| [!UICONTROL Chapter Details] | `chapterDetails` | [[!UICONTROL chapterDetails]](./chapter-details-reporting.md) | Met Details van hoofdstuk worden gegevens vastgelegd die betrekking hebben op de hoofdstukken of gesegmenteerde delen van de inhoud. Deze biedt informatie over hoofdstukmarkeertekens, tijdlijnen en de bijbehorende metagegevens. |
| [!UICONTROL List Of States] | `states` | [[!UICONTROL playerStateData]](./player-state-data-reporting.md) | Het bezit van Staten is een serie die diverse staten door de ervaringsgebeurtenis vangt. Deze eigenschap biedt opeenvolgende gegevens over het afspelen, gebruikershandelingen of wijzigingen in de inhoud. |
| [!UICONTROL Qoe Data Details] | `qoeDataDetails` | [[!UICONTROL qoeDataDetails]](./qoe-data-details-reporting.md) | QoE (Quality of Experience) Gegevens leggen prestatiegerelateerde metriek en gegevens over gebruikerservaring vast. Het biedt inzicht in kwaliteit, reactiesnelheid en gebruikersinteracties. |
| [!UICONTROL Session Details] | `sessionDetails` | [[!UICONTROL sessionDetails]](./session-details-reporting.md) | Sessiedetails bevatten uitgebreide informatie over de ervaringsgebeurtenis, die inzichten biedt in gebruikersinteracties, duur en contextafhankelijke gegevens die betrekking hebben op de afspeelsessie. |
| [!UICONTROL The Custom Metadata] | `customMetadata` | [[!UICONTROL customMetadataDetails]](./custom-metadata-details-reporting.md) | Aangepaste metagegevens bevatten door de gebruiker gedefinieerde of aanvullende metagegevens die zijn gekoppeld aan de ervaringsgebeurtenis. Met deze metagegevens kunnen gepersonaliseerde of specifieke gegevens worden opgenomen in de context van de gebeurtenis. |
| [!UICONTROL Playhead] | `playhead` | integer | De afspeelkop vertegenwoordigt de huidige afspeelpositie in de media-inhoud. Voor live-inhoud wordt de huidige seconde van de dag aangegeven (0 &lt;= playhead &lt; 86400). Voor opgenomen inhoud geeft deze de huidige seconde van de duur van de inhoud weer (0 &lt;= playhead &lt; lengte van de inhoud). |

{style="table-layout:auto"}
