---
title: Gegevenstype Gegevens media
description: Meer informatie over het gegevenstype Data Model (XDM) van het Data Model voor gegevens over mediagegevens.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# [!UICONTROL Media details information] gegevenstype

[!UICONTROL Media details information] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat essentiële details over media playbackgebeurtenissen vangt. Gebruik de [!UICONTROL Media details information] gegevenstype voor het vastleggen van details, zoals de positie van de afspeelkop binnen de inhoud, unieke sessie-id&#39;s en diverse geneste eigenschappen die onder andere betrekking hebben op de sessie. Dit gegevenstype biedt een uitgebreid overzicht van de afspeelervaring, waarmee mediaconsumptiepatronen en bijbehorende gebeurtenissen tijdens afspeelsessies kunnen worden bijgehouden en geanalyseerd.

+++Selecteer om een diagram van te tonen [!UICONTROL Media details information] gegevenstype.
![Een schema van de [!UICONTROL Media details information] gegevenstype.](../images/data-types/media-details-information.png)
+++

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --------------------- | --------------- | --------- | ----------- |
| [!UICONTROL Playhead] | `playhead` | integer | De afspeelkop vertegenwoordigt de huidige afspeelpositie in de media-inhoud. Voor live-inhoud wordt de huidige seconde van de dag aangegeven (0 &lt;= playhead &lt; 86400). Voor opgenomen inhoud geeft deze de huidige seconde van de duur van de inhoud weer (0 &lt;= playhead &lt; lengte van de inhoud). |
| [!UICONTROL Media Session ID] | `sessionID` | string | De mediasessie-id identificeert op unieke wijze een instantie van een inhoudsstroom tijdens een afzonderlijke afspeelsessie. Het dient als een onderscheidende id voor het bijhouden en beheren van de specifieke afspeelervaring die aan een gebruiker of kijker is gekoppeld. |
| [!UICONTROL Session Details] | `sessionDetails` | [[!UICONTROL sessionDetails]](./session-details-information.md) | Sessiedetails bevatten uitgebreide informatie over de ervaringsgebeurtenis, die inzichten biedt in gebruikersinteracties, duur en contextafhankelijke gegevens die betrekking hebben op de afspeelsessie. |
| [!UICONTROL Advertising Details] | `advertisingDetails` | [[!UICONTROL advertisingDetails]](./advertising-details-information.md) | Reclamedetails hebben betrekking op specifieke informatie over reclameactiviteiten tijdens het ervaringsevenement. Dit zijn onder andere metagegevens voor advertenties, specificaties voor doelgroepen en prestatiewaarden. |
| [!UICONTROL Advertising Pod Details] | `advertisingPodDetails` | [[!UICONTROL advertisingPodDetails]](./advertising-pod-details-information.md) | Details van advertentiepod bevatten informatie over advertentiepods binnen de ervaringsgebeurtenis. Het biedt inzichten in de volgorde van de advertenties, de inhoud en de betrokkenheidsmetriek. |
| [!UICONTROL Chapter Details] | `chapterDetails` | [[!UICONTROL chapterDetails]](./chapter-details-information.md) | Met Details van hoofdstuk worden gegevens vastgelegd die betrekking hebben op de hoofdstukken of gesegmenteerde delen van de inhoud. Deze biedt informatie over hoofdstukmarkeertekens, tijdlijnen en de bijbehorende metagegevens. |
| [!UICONTROL Error Details] | `errorDetails` | [[!UICONTROL errorDetails]](./error-details-information.md) | Foutdetails bevatten informatie over fouten die tijdens de ervaringsgebeurtenis zijn aangetroffen. Dit omvat foutcodes, beschrijvingen, tijdstempels en relevante contextuele gegevens. |
| [!UICONTROL Qoe Data Details] | `qoeDataDetails` | [[!UICONTROL qoeDataDetails]](./qoe-data-details-information.md) | QoE (Quality of Experience) Gegevens leggen prestatiegerelateerde metriek en gegevens over gebruikerservaring vast. Het biedt inzicht in kwaliteit, reactiesnelheid en gebruikersinteracties. |
| [!UICONTROL List Of States Start] | `statesStart` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | Het Begin van staten verstrekt een serie om van de staten aan het begin van de ervaringsgebeurtenis een lijst te maken. Deze bevat gegevens die betrekking hebben op het afspelen, handelingen van gebruikers of specifieke inhoud. |
| [!UICONTROL List Of States End] | `statesEnd` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | States End biedt een array om de statussen aan het einde van de ervaringsgebeurtenis weer te geven. Deze bevat details over de uiteindelijke afspeelstatus of de status van de inhoud. |
| [!UICONTROL List Of States] | `states` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | Het bezit van Staten is een serie die diverse staten door de ervaringsgebeurtenis vangt. Deze eigenschap biedt opeenvolgende gegevens over het afspelen, gebruikershandelingen of wijzigingen in de inhoud. |
| [!UICONTROL The Custom Metadata] | `customMetadata` | [[!UICONTROL customMetadataDetails]](./custom-metadata-details-information.md) | Aangepaste metagegevens bevatten door de gebruiker gedefinieerde of aanvullende metagegevens die zijn gekoppeld aan de ervaringsgebeurtenis. Met deze metagegevens kunnen gepersonaliseerde of specifieke gegevens worden opgenomen in de context van de gebeurtenis. |

{style="table-layout:auto"}

Voor meer informatie over de veldgroep raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json)
