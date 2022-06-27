---
keywords: activering bewerken, doel bewerken, bestemming bewerken
title: Activeringsgegevens bewerken
type: Tutorial
description: Voer de stappen in dit artikel uit om een bestaande activeringsgegevensstroom in Adobe Experience Platform te bewerken.
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# Activeringsgegevens bewerken {#edit-activation-flows}

In Adobe Experience Platform kunt u verschillende componenten van bestaande activeringsgegevens naar doelen bewerken, zoals de geëxporteerde segmenten en profielkenmerken, de exportfrequentie, of de activeringsgegevensstroom is in- of uitgeschakeld, enzovoort.

## Gegevensstromen bewerken {#edit-dataflows}

Voer de onderstaande stappen uit om bestaande activeringsgegevens te bewerken:

1. Aanmelden bij de [UI Experience Platform](https://platform.adobe.com/) en selecteert u **[!UICONTROL Destinations]** in de linkernavigatiebalk. Selecteren **[!UICONTROL Browse]** van de hoogste kopbal om uw bestaande bestemmingsgegevens te bekijken.

   ![Bladeren door doelen](../assets/ui/edit-activation/browse-destinations.png)

2. Filterpictogram selecteren ![Filter-pictogram](../assets/ui/edit-activation/filter.png) bovenaan links om het deelvenster Sorteren te starten. Het deelvenster Sorteren bevat een lijst met al uw doelen. U kunt meer dan één bestemming van de lijst selecteren om een gefilterde selectie van gegevensstromen te zien verbonden aan de geselecteerde bestemming.

   ![Filterdoelen](../assets/ui/edit-activation/filter-destinations.png)

3. Selecteer de naam van de doelgegevensstroom die u wilt bewerken.

   ![Doel selecteren](../assets/ui/edit-activation/destination-select.png)

4. De **[!UICONTROL Dataflow runs]** wordt de pagina voor het doel weergegeven en worden de beschikbare besturingselementen weergegeven. Op dit punt, kunt u verscheidene componenten van de bestemmingsdataflow uitgeven:

   * Selecteren **[!UICONTROL Activate segments]** in de juiste spoorstaaf om te veranderen welke segmenten of profielattributen naar de bestemming te verzenden. Hiermee gaat u naar de activeringsworkflow, die afhankelijk is van het doeltype. Zie de handleidingen voor meer informatie:
      * [het activeren van publieksgegevens aan segment het stromen bestemmingen](./activate-segment-streaming-destinations.md) (bijvoorbeeld Facebook of Twitter);
      * [het activeren van publieksgegevens aan batch op profiel-gebaseerde bestemmingen](./activate-batch-profile-destinations.md) (bijvoorbeeld Amazon S3 of Oracle Eloqua);
      * [het activeren van publieksgegevens aan het stromen op profiel-gebaseerde bestemmingen](./activate-streaming-profile-destinations.md) (bijvoorbeeld HTTP-API of Amazon Kinesis).
   * Daarnaast kunt u de naam en beschrijving van de doelgegevensstroom bewerken.
   * U kunt de **[!UICONTROL Enabled]/[!UICONTROL Disabled]** schakelen om alle gegevens die u exporteert naar de bestemming te starten en pauzeren.

   ![Doelgegevens](../assets/ui/edit-activation/destination-details.png)

## Volgende stappen {#next-steps}

Door deze zelfstudie te volgen, hebt u de opdracht **[!UICONTROL destinations]** om bestaande doelgegevens bij te werken.

Voor meer informatie over bestemmingen, verwijs naar [Overzicht van doelen](../catalog/overview.md).
