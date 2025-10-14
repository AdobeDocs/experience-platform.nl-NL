---
title: Bestanden op aanvraag exporteren naar batchbestemmingen met de gebruikersinterface van Experience Platform
type: Tutorial
description: Leer hoe u bestanden op aanvraag exporteert naar batchbestemmingen met de gebruikersinterface van Experience Platform.
exl-id: 0cbe5089-b73d-4584-8451-2fc34d47c357
source-git-commit: d3bd76f5b36b6a6afcb67fe923eb8e4f3d7a9415
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 0%

---


# Bestanden op aanvraag exporteren naar batchbestemmingen met de gebruikersinterface van Experience Platform

>[!IMPORTANT]
> 
>Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

## **[!UICONTROL Export file now]**-overzicht {#overview}

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_activatenow"
>title="Bestand nu exporteren"
>abstract="Selecteer deze controle om een volledige dossieruitvoer naast om het even welke eerder geplande uitvoer te leveren. Het exporteren van het bestand wordt direct geactiveerd en de meest recente resultaten worden opgehaald uit Experience Platform-segmentatiebewerkingen."

Dit artikel verklaart hoe te om Experience Platform UI te gebruiken om dossiers op bestelling naar partijbestemmingen zoals [&#x200B; wolkenopslag &#x200B;](/help/destinations/catalog/cloud-storage/overview.md) en [&#x200B; e-mailmarketing &#x200B;](/help/destinations/catalog/email-marketing/overview.md) bestemmingen uit te voeren.

Met het besturingselement **[!UICONTROL Export file now]** kunt u een volledig bestand exporteren zonder het huidige exportschema van een eerder gepland publiek te onderbreken. Deze exportbewerking wordt uitgevoerd naast de eerder geplande exportbewerkingen en heeft geen invloed op de exportfrequentie van het publiek. Het exporteren van het bestand wordt direct geactiveerd en de meest recente resultaten worden opgehaald uit Experience Platform-segmentatiebewerkingen.

U kunt hiervoor ook de Experience Platform API&#39;s gebruiken. Lees hoe te [&#x200B; publiek op bestelling aan partijbestemmingen via ad-hoc activering API &#x200B;](/help/destinations/api/ad-hoc-activation-api.md) activeren.

## Vereisten {#prerequisites}

Om dossiers op bestelling naar partijbestemmingen uit te voeren, moet u met succes [&#x200B; verbonden aan een bestemming &#x200B;](./connect-destination.md) hebben. Als u dit niet reeds hebt gedaan, ga naar de [&#x200B; bestemmingscatalogus &#x200B;](../catalog/overview.md), doorblader de gesteunde bestemmingen, en vorm de bestemming die u wilt gebruiken.

## Bestanden op aanvraag exporteren {#how-to-export-files-on-demand}

1. Ga naar **[!UICONTROL Connections > Destinations]** en selecteer de tab **[!UICONTROL Browse]** en het filtersymbool om bestaande verbindingen met de gewenste batchbestemmingen weer te geven.

   ![&#x200B; Beeld die hoe te om aan doorbladeren lusje en filter bestaande dataflows te krijgen benadrukt.](../assets/ui/activate-on-demand/browse-tab.png)

2. Selecteer de gewenste doelverbinding om de bestaande gegevensstroom naar de bestemming te inspecteren.

   ![&#x200B; Beeld die een gefilterde dataflow benadrukt.](../assets/ui/activate-on-demand/filtered-dataflow.png)

3. Selecteer het tabblad **[!UICONTROL Activation data]** en selecteer het publiek waarvoor u bestanden op aanvraag wilt exporteren en selecteer het besturingselement **[!UICONTROL Export file now]** om een eenmalige export te activeren waarmee een bestand voor elk geselecteerd publiek naar uw batchdoel wordt geleverd.

   ![&#x200B; Beeld dat het dossier van de Uitvoer benadrukt nu knoop.](../assets/ui/activate-on-demand/bulk-export-file-now.png)

4. Selecteer **[!UICONTROL Yes]** om het exporteren van het bestand te bevestigen en te activeren.

   ![&#x200B; Beeld die het dossier van de Uitvoer tonen bevestigt nu dialoog.](../assets/ui/activate-on-demand/confirm-activation.png)

5. Er wordt een bevestigingsbericht weergegeven met de mededeling dat het exporteren van het bestand is gestart.

   ![&#x200B; Beeld die bevestiging van succesvolle ad hoc activering tonen.](../assets/ui/activate-on-demand/ad-hoc-success.png)

6. U kunt ook naar het tabblad **[!UICONTROL Dataflow runs]** gaan om te bevestigen dat het exporteren van het bestand is uitgeschakeld.

## Overwegingen {#considerations}

Houd rekening met het volgende wanneer u het besturingselement **[!UICONTROL Export file now]** gebruikt:

* **[!UICONTROL Export file now]** werkt alleen voor publiek wiens schema in de batchactiveringsgegevens de huidige datum overlapt. Dit omvat publiek met programma&#39;s die geen einddatum (de uitvoerfrequentie van **[!UICONTROL Once]**) hebben, of waar de einddatum nog niet is overgegaan.
* Wanneer het toevoegen van een publiek aan een bestaande dataflow, wacht minstens **één uur** alvorens de **[!UICONTROL Export file now]** controle te gebruiken.
* Als u het samenvoegbeleid van een publiek verandert, of als u een publiek creeert dat een nieuw samenvoegbeleid gebruikt, wacht 24 uur tot het gebruiken van de **[!UICONTROL Export file now]** controle.

## UI-foutberichten {#ui-error-messages}

Wanneer u het besturingselement **[!UICONTROL Export file now]** gebruikt, kunnen de onderstaande foutberichten optreden. Bekijk de tabel om te begrijpen hoe u deze kunt aanpakken wanneer ze worden weergegeven.

| Foutbericht | Resolutie |
|---------|----------|
| Uitvoeren wordt al uitgevoerd voor publiek `segment ID` voor bestelling `dataflow ID` met run-id `flow run ID` | Dit foutbericht geeft aan dat er momenteel een ad-hocactiveringsstroom actief is voor een publiek. Wacht tot de taak is voltooid voordat u de activeringstaak opnieuw start. |
| Soorten publiek `<segment name>` maken geen deel uit van deze gegevensstroom of van het planningsbereik! | Dit foutbericht geeft aan dat het publiek dat u hebt geselecteerd om te activeren, niet is toegewezen aan de gegevensstroom of dat het activeringsschema dat voor het publiek is ingesteld, is verlopen of nog niet is gestart. Controleer of het publiek inderdaad is toegewezen aan de dataflow en controleer of het activeringsschema voor het publiek de huidige datum overlapt. |

## Verwante informatie {#related-information}

* [Het publiek op aanvraag naar batchbestemmingen activeren met de Experience Platform API&#39;s](/help/destinations/api/ad-hoc-activation-api.md)
* [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](/help/destinations/ui/activate-batch-profile-destinations.md)
