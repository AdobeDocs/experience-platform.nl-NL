---
keywords: doelen activeren;gegevens activeren
title: Overzicht van activering
type: Tutorial
description: Leer hoe u het publiek in Adobe Experience Platform activeert voor verschillende soorten doelen.
exl-id: 987af401-2d93-45b4-a8f9-191e6058e4da
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# Overzicht van activering

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Adobe Experience Platform ondersteunt een groot aantal bestemmingen. De workflow voor publiekactivering varieert per bestemming, op basis van het type publieksgegevens dat door de gebruikers wordt ondersteund en de frequentie waarmee de gegevens worden geëxporteerd.

## Activeringsmethoden {#activation-methods}

Nadat u [ uw bestemming ](connect-destination.md) vormt, kunt u publiek op veelvoudige manieren activeren:

### Soorten publiek vanuit de catalogus met doelen activeren

Zie de volgende gidsen voor gedetailleerde informatie over het activeren van publiek aan uw bestemming van de catalogus van bestemmingen:

* [De publieksgegevens van de activering aan het stromen publiek de uitvoerbestemmingen](activate-segment-streaming-destinations.md)
* [De publieksgegevens van de activering aan het stromen profiel de uitvoerbestemmingen](activate-streaming-profile-destinations.md)
* [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](activate-batch-profile-destinations.md)

### Soorten publiek vanaf de pagina [!UICONTROL Browse] activeren

Voer de onderstaande stappen uit om gegevens vanaf de pagina **[!UICONTROL Browse]** naar uw doelen te activeren.

1. Ga naar **[!UICONTROL Connections > Destinations]** en selecteer de tab **[!UICONTROL Browse]** .

   ![ doorbladert lusje ](../assets/ui/activation-overview/browse-tab.png)

1. Zoek de doelverbinding die u wilt gebruiken om uw segmenten te activeren, selecteer de drie stippen in de kolom [!UICONTROL Name] en selecteer vervolgens **[!UICONTROL Activate audiences]** .

   ![ activeer publiek knoop ](../assets/ui/activation-overview/activate-segments.png)

1. Voer afhankelijk van het geselecteerde doel de stappen uit die in de onderstaande artikelen worden beschreven, te beginnen met de stap **[!UICONTROL Select segments]** , om de activeringsworkflow te voltooien:

   * [De publieksgegevens van de activering aan het stromen publiek de uitvoerbestemmingen](activate-segment-streaming-destinations.md)
   * [De publieksgegevens van de activering aan het stromen profiel de uitvoerbestemmingen](activate-streaming-profile-destinations.md)
   * [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](activate-batch-profile-destinations.md)

### Soorten publiek activeren op de pagina met publieksdetails {#activate-audience-details}

U kunt het publiek naar bestemmingen vanuit de pagina met publieksdetails activeren. Zie [ details van het publiek ](../../segmentation/ui/audience-portal.md#audience-details) voor meer informatie.

Voer afhankelijk van de geselecteerde bestemming de stappen uit die in de onderstaande artikelen worden beschreven om de activeringsworkflow te voltooien:

* [De publieksgegevens van de activering aan het stromen publiek de uitvoerbestemmingen](activate-segment-streaming-destinations.md)
* [De publieksgegevens van de activering aan het stromen profiel de uitvoerbestemmingen](activate-streaming-profile-destinations.md)
* [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](activate-batch-profile-destinations.md)
