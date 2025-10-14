---
title: Gegevenstype van verzameling media
description: Leer over het de gegevenstype van de Gegevens van de Ervaring van Media van de Inzameling van Media Model (XDM).
exl-id: 1faf60f7-6afb-4ce2-b50d-967776a57715
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---

# [!UICONTROL Media Collection Details] gegevenstype

[!UICONTROL Media Collection Details] is een standaard XDM-gegevenstype (Experience Data Model) waarmee essentiële gegevens over gebeurtenissen voor het afspelen van media worden vastgelegd. Gebruik het gegevenstype [!UICONTROL Media Collection Details] om details vast te leggen, zoals de positie van de afspeelkop binnen de inhoud, unieke sessie-id&#39;s en verschillende geneste eigenschappen die onder andere betrekking hebben op de sessie. Dit gegevenstype biedt een uitgebreid overzicht van de afspeelervaring waarmee mediaconsumptiepatronen en bijbehorende gebeurtenissen tijdens afspeelsessies kunnen worden bijgehouden en geanalyseerd.

>[!NOTE]
>
>De gebieden van de Inzameling van media vangen gegevens en verzenden het naar andere diensten van Adobe voor verdere verwerking. Media Reporting-velden worden door Adobe-services gebruikt voor het analyseren van de velden Media Collection die door gebruikers worden verzonden. Deze gegevens worden, samen met andere specifieke maatstaven voor gebruikers, berekend en gerapporteerd.

+++ selecteren om een diagram van het gegevenstype [!UICONTROL Media Collection details] weer te geven.
![&#x200B; een diagram van het [!UICONTROL Media Collection details information] gegevenstype.](../images/data-types/media-collection-details.png)
+++

| Weergavenaam | Eigenschap | Gebeurtenissen vereist voor | Gegevenstype | Beschrijving |
| ------------------------------------ | ----------------------- | ---------------------------------------------------------- | --------- | ----------- |
| [!UICONTROL Advertising Details] | `advertisingDetails` | `adStart` | [[!UICONTROL advertisingDetails] - Verzameling &#x200B;](./advertising-details-collection.md) | Advertising Details verwijzen naar specifieke informatie over reclameactiviteiten tijdens het ervaringsevenement. Dit zijn onder andere metagegevens voor advertenties, specificaties voor doelgroepen en prestatiewaarden. |
| [!UICONTROL Advertising Pod Details] | `advertisingPodDetails` | `adBreakStart` | [[!UICONTROL advertisingPodDetails] - Verzameling &#x200B;](./advertising-pod-details-collection.md) | Advertising Pod Details bevatten informatie over advertentiepods binnen de Experience Event. Het biedt inzichten in de volgorde van de advertenties, de inhoud en de betrokkenheidsmetriek. |
| [!UICONTROL Chapter Details] | `chapterDetails` | `chapterStart` | [[!UICONTROL chapterDetails] - Verzameling &#x200B;](./chapter-details-collection.md) | Met Details van hoofdstuk worden gegevens vastgelegd die betrekking hebben op de hoofdstukken of gesegmenteerde delen van de inhoud. Deze biedt informatie over hoofdstukmarkeertekens, tijdlijnen en de bijbehorende metagegevens. |
| [!UICONTROL Error Details] | `errorDetails` | `error` | [[!UICONTROL errorDetails] - Verzameling &#x200B;](./error-details-collection.md) | Foutdetails bevatten informatie over fouten die tijdens de ervaringsgebeurtenis zijn aangetroffen. Dit omvat foutcodes, beschrijvingen, tijdstempels en relevante contextuele gegevens. |
| [!UICONTROL List Of States End] | `statesEnd` | Wordt gebruikt in `statesUpdate` | [[!UICONTROL statesEnd] - Verzameling &#x200B;](./list-of-states-end-collection.md) | States End biedt een array om de statussen aan het einde van de ervaringsgebeurtenis weer te geven. Deze bevat details over de uiteindelijke afspeelstatus of de status van de inhoud. |
| [!UICONTROL List Of States Start] | `statesStart` | Wordt gebruikt in `statesUpdate` | [[!UICONTROL statesStart] - Verzameling &#x200B;](./list-of-states-start-collection.md) | Het Begin van staten verstrekt een serie om van de staten aan het begin van de ervaringsgebeurtenis een lijst te maken. Deze bevat gegevens die betrekking hebben op het afspelen, handelingen van gebruikers of specifieke inhoud. |
| [!UICONTROL Qoe Data Details] | `qoeDataDetails` | Optioneel voor iedereen | [[!UICONTROL qoeDataDetails] - Verzameling &#x200B;](./qoe-data-details-collection.md) | QoE (Quality of Experience) Gegevens leggen prestatiegerelateerde metriek en gegevens over gebruikerservaring vast. Het biedt inzicht in kwaliteit, reactiesnelheid en gebruikersinteracties. |
| [!UICONTROL Session Details] | `sessionDetails` | `sessionStart` | [[!UICONTROL sessionDetails] - Verzameling &#x200B;](./session-details-collection.md) | Sessiedetails bevatten uitgebreide informatie over de ervaringsgebeurtenis, die inzichten biedt in gebruikersinteracties, duur en contextafhankelijke gegevens die betrekking hebben op de afspeelsessie. |
| [!UICONTROL The Custom Metadata] | `customMetadata` | Optioneel voor `sessionStart`, `adStart`, `sessionStart` | [[!UICONTROL customMetadataDetails] - Verzameling &#x200B;](./custom-metadata-details-collection.md) | Aangepaste metagegevens bevatten door de gebruiker gedefinieerde of aanvullende metagegevens die zijn gekoppeld aan de ervaringsgebeurtenis. Met deze metagegevens kunnen gepersonaliseerde of specifieke gegevens worden opgenomen in de context van de gebeurtenis. |
| [!UICONTROL Media Session ID] | `sessionID` | Alle gebeurtenissen **behalve** `sessionStart` en gedownloade inhoud. | string | De mediasessie-id identificeert op unieke wijze een instantie van een inhoudsstroom tijdens een afzonderlijke afspeelsessie. Het dient als een onderscheidende id voor het bijhouden en beheren van de specifieke afspeelervaring die aan een gebruiker of kijker is gekoppeld.<br><em> Nota:<em>`sessionId` wordt verzonden op alle gebeurtenissen, behalve `sessionStart` en voor alle gedownloade gebeurtenissen. |
| [!UICONTROL Playhead] | `playhead` | Alle gebeurtenissen | integer | De afspeelkop vertegenwoordigt de huidige afspeelpositie in de media-inhoud. Voor live-inhoud wordt de huidige seconde van de dag aangegeven (0 &lt;= playhead &lt; 86400). Voor opgenomen inhoud geeft deze de huidige seconde van de duur van de inhoud weer (0 &lt;= playhead &lt; lengte van de inhoud). |

{style="table-layout:auto"}
