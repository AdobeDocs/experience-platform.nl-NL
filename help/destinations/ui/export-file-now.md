---
title: (Bèta) de dossiers van de uitvoer op bestelling aan partijbestemmingen gebruikend Experience Platform UI
type: Tutorial
description: Leer hoe u bestanden op aanvraag exporteert naar batchbestemmingen met behulp van de interface van het Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: ff0fe836b2bb181ae4395f1d04c04b8e51a5bac6
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---

# (Bèta) de dossiers van de uitvoer op bestelling aan partijbestemmingen gebruikend Experience Platform UI

>[!IMPORTANT]
>
>De **[!UICONTROL Export file now]** in Adobe Experience Platform Destination SDK is momenteel in bètaversie. De documentatie en functionaliteit kunnen worden gewijzigd.

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

## **[!UICONTROL Export file now]** - overzicht {#overview}

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_activatenow"
>title="Bestand nu exporteren"
>abstract="Selecteer deze controle om een volledige dossieruitvoer naast om het even welke eerder geplande uitvoer te leveren. De bestandsuitvoer wordt onmiddellijk geactiveerd en de meest recente resultaten worden opgehaald uit de gesegmenteerde Experience Platforms."

Dit artikel verklaart hoe te om Experience Platform UI te gebruiken om dossiers op bestelling naar partijbestemmingen zoals uit te voeren [cloudopslag](/help/destinations/catalog/cloud-storage/overview.md) en [e-mailmarketing](/help/destinations/catalog/email-marketing/overview.md) bestemmingen.

De **[!UICONTROL Export file now]** Met besturingselementen kunt u een volledig bestand exporteren zonder het huidige exportschema van een eerder gepland segment te onderbreken. Deze export komt bovenop de eerder geplande export en verandert de exportfrequentie van het segment niet. De bestandsuitvoer wordt onmiddellijk geactiveerd en de meest recente resultaten worden opgehaald uit de gesegmenteerde Experience Platforms.

U kunt hiervoor ook de Experience Platform-API&#39;s gebruiken. Lees hoe te [publiekssegmenten op aanvraag activeren voor batchbestemmingen via de API voor ad-hocactivering](/help/destinations/api/ad-hoc-activation-api.md).

## Vereisten {#prerequisites}

Als u bestanden op aanvraag wilt exporteren naar batchbestemmingen, moet u [verbonden met een bestemming](./connect-destination.md). Als u dat nog niet hebt gedaan, gaat u naar de [doelcatalogus](../catalog/overview.md), doorblader de gesteunde bestemmingen, en vorm de bestemming die u wilt gebruiken.

## Bestanden op aanvraag exporteren {#how-to-export-files-on-demand}

1. Ga naar **[!UICONTROL Connections > Destinations]**, selecteert u de **[!UICONTROL Browse]** en het filtersymbool om bestaande verbindingen aan uw gewenste partijbestemmingen te tonen.

   ![Afbeelding die markeert hoe u het tabblad Bladeren kunt gebruiken en bestaande gegevensstromen kunt filteren.](../assets/ui/activate-on-demand/browse-tab.png)

2. Selecteer de gewenste doelverbinding om de bestaande gegevensstroom naar de bestemming te inspecteren.

   ![Afbeelding die een gefilterde gegevensstroom markeert.](../assets/ui/activate-on-demand/filtered-dataflow.png)

3. Selecteer **[!UICONTROL Activation data]** en selecteert u het segment waarvoor u een bestand op aanvraag wilt exporteren en selecteert u het **[!UICONTROL Export file now]** besturingselement om een eenmalige export te activeren die een bestand naar uw batchbestemming levert.

   >[!IMPORTANT]
   >
   >Het selecteren van meerdere segmenten voor het bulksgewijs exporteren van bestanden wordt momenteel niet ondersteund in de gebruikersinterface. Gebruik de [API voor ad-hocactivering](/help/destinations/api/ad-hoc-activation-api.md) daartoe.

   ![Afbeelding die het exportbestand markeert, nu knop.](../assets/ui/activate-on-demand/activate-segment-on-demand.png)

4. Selecteren **[!UICONTROL Yes]** om het exporteren van het bestand te bevestigen en te activeren.

   ![Afbeelding die het dialoogvenster Bestand exporteren nu weergeeft.](../assets/ui/activate-on-demand/confirm-activation.png)

5. Er wordt een bevestigingsbericht weergegeven met de mededeling dat het exporteren van het bestand is gestart.

   ![Afbeelding met bevestiging van geslaagde ad-hocactivering.](../assets/ui/activate-on-demand/ad-hoc-success.png)

6. U kunt ook schakelen naar de **[!UICONTROL Dataflow runs]** om te bevestigen dat het exporteren van het bestand is uitgeschakeld.

## Overwegingen {#considerations}

Houd rekening met het volgende wanneer u de **[!UICONTROL Export file now]** besturingselement:

* **[!UICONTROL Export file now]** werkt alleen voor segmenten waarvan het schema in de batchactiveringsgegevens de huidige datum overlapt. Dit omvat segmenten met programma&#39;s die geen einddatum hebben (uitvoerfrequentie van **[!UICONTROL Once]**) of wanneer de einddatum nog niet is verstreken.
* Wanneer het toevoegen van een segment aan een bestaande dataflow, wacht minstens 15 minuten tot het gebruiken van **[!UICONTROL Export file now]** controle.
* Als u het de fusiebeleid van een segment verandert, of als u een segment creeert dat een nieuw fusiebeleid gebruikt, wacht 24 uur tot het gebruiken van **[!UICONTROL Export file now]** controle.

## UI-foutberichten {#ui-error-messages}

Wanneer u de **[!UICONTROL Export file now]** Als u de besturing hebt, kunnen de onderstaande foutberichten worden weergegeven. Bekijk de tabel om te begrijpen hoe u deze kunt aanpakken wanneer ze worden weergegeven.

| Foutbericht | Resolutie |
|---------|----------|
| Reeds lopend voor segment `segment ID` voor bestelling `dataflow ID` met run-id `flow run ID` | Dit foutbericht geeft aan dat momenteel een ad-hocactiveringsstroom wordt uitgevoerd voor een segment. Wacht tot de taak is voltooid voordat u de activeringstaak opnieuw start. |
| Segmenten `<segment name>` maakt geen deel uit van deze gegevensstroom of van het planningsbereik! | Dit foutbericht geeft aan dat de segmenten die u hebt geselecteerd om te activeren, niet zijn toegewezen aan de gegevensstroom of dat het activeringsschema voor de segmenten is verlopen of nog niet is gestart. Controleer of het segment inderdaad is toegewezen aan de dataflow en controleer of het schema voor segmentactivering overlapt met de huidige datum. |

## Verwante informatie {#related-information}

* [Activeer publiekssegmenten aan partijbestemmingen op bestelling gebruikend het Experience Platform APIs](/help/destinations/api/ad-hoc-activation-api.md)
* [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](/help/destinations/ui/activate-batch-profile-destinations.md)