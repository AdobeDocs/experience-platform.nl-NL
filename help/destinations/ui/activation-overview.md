---
keywords: doelen activeren;gegevens activeren
title: Overzicht van activering
type: Tutorial
description: Leer hoe u het publiek in Adobe Experience Platform activeert voor verschillende soorten doelen.
exl-id: 987af401-2d93-45b4-a8f9-191e6058e4da
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# Overzicht van activering

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Adobe Experience Platform ondersteunt een groot aantal bestemmingen. De workflow voor publiekactivering varieert per bestemming, op basis van het type publieksgegevens dat door de gebruikers wordt ondersteund en de frequentie waarmee de gegevens worden geëxporteerd.

## Activeringsmethoden {#activation-methods}

Na u [vorm uw bestemming](connect-destination.md), kunt u het publiek op meerdere manieren activeren:

### Soorten publiek vanuit de catalogus met doelen activeren

Zie de volgende gidsen voor gedetailleerde informatie over het activeren van publiek aan uw bestemming van de catalogus van bestemmingen:

* [De publieksgegevens van de activering aan het stromen publiek de uitvoerbestemmingen](activate-segment-streaming-destinations.md)
* [De publieksgegevens van de activering aan het stromen profiel de uitvoerbestemmingen](activate-streaming-profile-destinations.md)
* [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](activate-batch-profile-destinations.md)

### Soorten publiek vanuit de [!UICONTROL Browse] page

Voer de onderstaande stappen uit om gegevens vanuit de **[!UICONTROL Browse]** pagina.

1. Ga naar **[!UICONTROL Connections > Destinations]** en selecteert u de **[!UICONTROL Browse]** tab.

   ![Tabblad Bladeren](../assets/ui/activation-overview/browse-tab.png)

1. Zoek de doelverbinding die u wilt gebruiken om uw segmenten te activeren, selecteer de drie stippen in het dialoogvenster [!UICONTROL Name] kolom, selecteer dan **[!UICONTROL Activate audiences]**.

   ![Knop Soorten publiek activeren](../assets/ui/activation-overview/activate-segments.png)

1. Voer afhankelijk van de geselecteerde bestemming de stappen uit die in de onderstaande artikelen worden beschreven, te beginnen met de **[!UICONTROL Select segments]** stap, om de activeringsworkflow te voltooien:

   * [De publieksgegevens van de activering aan het stromen publiek de uitvoerbestemmingen](activate-segment-streaming-destinations.md)
   * [De publieksgegevens van de activering aan het stromen profiel de uitvoerbestemmingen](activate-streaming-profile-destinations.md)
   * [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](activate-batch-profile-destinations.md)

### Soorten publiek activeren vanaf de pagina Soorten publiek {#activate-segment-details}

U kunt het publiek activeren naar doelen op de pagina Soorten publiek. Zie [Segmentdetails](../../segmentation/ui/overview.md#segment-details) voor meer informatie .

Voer afhankelijk van de geselecteerde bestemming de stappen uit die in de onderstaande artikelen worden beschreven om de activeringsworkflow te voltooien:

* [De publieksgegevens van de activering aan het stromen publiek de uitvoerbestemmingen](activate-segment-streaming-destinations.md)
* [De publieksgegevens van de activering aan het stromen profiel de uitvoerbestemmingen](activate-streaming-profile-destinations.md)
* [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](activate-batch-profile-destinations.md)
