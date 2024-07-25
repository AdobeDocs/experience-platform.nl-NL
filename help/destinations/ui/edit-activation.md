---
keywords: activering bewerken, doel bewerken, bestemming bewerken
title: Activeringsgegevens bewerken
type: Tutorial
description: Voer de stappen in dit artikel uit om een bestaande activeringsgegevensstroom in Adobe Experience Platform te bewerken.
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# Activeringsgegevens bewerken {#edit-activation-flows}

In Adobe Experience Platform kunt u verschillende componenten van bestaande activeringsgegevens naar doelen bewerken, zoals het geëxporteerde publiek en de profielkenmerken, de exportfrequentie, of de activeringsgegevensstroom is in- of uitgeschakeld, enzovoort.

## Gegevensstromen bewerken {#edit-dataflows}

Voer de onderstaande stappen uit om bestaande activeringsgegevens te bewerken:

1. Login aan het [ Experience Platform UI ](https://platform.adobe.com/) en selecteert **[!UICONTROL Destinations]** van de linkernavigatiebar. Selecteer **[!UICONTROL Browse]** in de bovenste koptekst om de bestaande doelgegevens weer te geven.

   ![ doorbladert bestemmingen ](../assets/ui/edit-activation/browse-destinations.png)

2. Selecteer het filterpictogram ![ filter-pictogram ](/help/images/icons/filter.png) op de bovenkant verlaten om het soortpaneel te lanceren. Het deelvenster Sorteren bevat een lijst met al uw doelen. U kunt meer dan één bestemming van de lijst selecteren om een gefilterde selectie van gegevensstromen te zien verbonden aan de geselecteerde bestemming.

   ![ bestemmingen van de Filter ](../assets/ui/edit-activation/filter-destinations.png)

3. Selecteer de naam van de doelgegevensstroom die u wilt bewerken.

   ![ Uitgezochte bestemming ](../assets/ui/edit-activation/destination-select.png)

4. De pagina **[!UICONTROL Dataflow runs]** voor het doel wordt weergegeven en de beschikbare besturingselementen worden weergegeven. Op dit punt, kunt u verscheidene componenten van de bestemmingsdataflow uitgeven:

   * Selecteer **[!UICONTROL Activate audiences]** in het rechterspoor om te wijzigen welk publiek of welke profielkenmerken naar de bestemming moeten worden verzonden. Hiermee gaat u naar de activeringsworkflow, die afhankelijk is van het doeltype. Zie de handleidingen voor meer informatie:
      * [ het activeren van publieksgegevens aan publiek die bestemmingen ](./activate-segment-streaming-destinations.md) stromen (bijvoorbeeld, Facebook of Twitter);
      * [ het activeren van publieksgegevens aan batch op profiel-gebaseerde bestemmingen ](./activate-batch-profile-destinations.md) (bijvoorbeeld, Amazon S3 of Oracle Eloqua);
      * [ het activeren van publieksgegevens aan het stromen op profiel-gebaseerde bestemmingen ](./activate-streaming-profile-destinations.md) (bijvoorbeeld, HTTP API of Amazon Kinesis).

   * Daarnaast kunt u de naam en beschrijving van de doelgegevensstroom bewerken.
   * Met de schakeloptie **[!UICONTROL Enabled]/[!UICONTROL Disabled]** kunt u alle gegevens die u exporteert naar het doel, starten en pauzeren.

   ![ de details van de Bestemming ](../assets/ui/edit-activation/destination-details.png)

## Volgende stappen {#next-steps}

Aan de hand van deze zelfstudie hebt u de **[!UICONTROL destinations]** -werkruimte gebruikt om bestaande doelgegevensstromen bij te werken.

Voor meer informatie over bestemmingen, verwijs naar het [ overzicht van bestemmingen ](../catalog/overview.md).
