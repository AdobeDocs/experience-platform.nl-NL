---
title: Breid dataset de uitvoerprogramma's voor dataflows uit die vóór November 2024 werden gecreeerd
description: Leer hoe te om het de uitvoerprogramma voor dataset uit te breiden uitvoerdataflows die vóór November 2024 worden gecreeerd die op 1 September, 2025 ophouden te werken.
type: Tutorial
exl-id: a756886b-3f4b-4427-bd26-817221ba68aa
source-git-commit: 0da592dd2846ed0f1eeb31102842c8895cac6952
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---

# Breid dataset de uitvoerprogramma&#39;s voor dataflows uit die vóór November 2024 werden gecreeerd

>[!IMPORTANT]
>
>**Vereiste Actie**: Als uw organisatie [&#x200B; dataflows van de datasetuitvoer &#x200B;](export-datasets.md) heeft die voorafgaand aan November 2024 worden gecreeerd, zullen deze dataflows ophouden werkend op 1st September, 2025. In deze handleiding wordt uitgelegd hoe u het exportschema na deze datum kunt uitbreiden voor de gegevensstromen die u wilt behouden.

## Overzicht {#overview}

In de [&#x200B; Versie van september 2024 van Experience Platform &#x200B;](/help/release-notes/2024/september-2024.md#destinations), introduceerde Adobe een standaardeinddatum van **1 mei, 2025** voor alle dataset uitvoerdataflows die vóór de versie van september 2024 werden gecreeerd.

**Deze datum is sindsdien bijgewerkt aan 1 September, 2025** voor alle dataflows van de datasetuitvoer die **voorafgaand aan November 2024** werden gecreeerd.

Dataset de uitvoerdataflows die vóór November 2024 worden gecreeerd zullen ophouden uitvoerend gegevens over **September 1, 2025** tenzij u manueel hun vervaldatum uitbreidt.

Als u de dataflows nodig hebt om het uitvoeren van gegevens na **1 September, 2025** te houden, moet u hun programma&#39;s voor elke bestemming uitbreiden waarnaar u datasets, door de stappen in deze gids te volgen uitvoert.

## Betrokken bestemmingen {#affected-destinations}

Uw organisatie kan actieve gegevens van de datasetuitvoer hebben die gegevens verzenden naar de hieronder vermelde bestemmingen. Volg de stappen in de volgende secties en bekijk de analyse video om te leren hoe te om te identificeren welke datasets worden geplaatst om te verlopen.

* [[!DNL Azure Data Lake Storage Gen2]](../catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../catalog/cloud-storage/sftp.md#changelog)
* [[!DNL Marketo Measure Ultimate]](../catalog/adobe/marketo-measure-ultimate.md)

## Videotutorial {#video}

Bekijk de video hieronder voor een geleidelijke demonstratie van hoe te om datasetuitvoer met komende einddata te identificeren en het uitvoerprogramma voor de gegevensstromen uit te breiden die u wilt houden.

>[!VIDEO](https://video.tv.adobe.com/v/3470518/)

## Stap 1: betrokken gegevensstromen identificeren {#identify-dataflows}

Alvorens het de uitvoerschema voor uw dataset uitvoerdataflows uit te breiden, moet u eerst identificeren welke dataflows door de aanstaande vervaldatum worden beïnvloed. Voer de onderstaande stappen uit om gegevensstromen te zoeken waarvoor actie nodig is.

1. Ga naar **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** in de gebruikersinterface van Experience Platform.
2. Selecteer **[!UICONTROL Activate]** op een bestemming die de actieve gegevens van de gegevensreeks de uitvoergegevens heeft.

   >[!TIP]
   >
   >Gebruik het filter **[!UICONTROL Data Types]** aan de linkerkant van de catalogus om beschikbare doelen te filteren op **[!UICONTROL Datasets]** .

3. Selecteer het gegevenstype **[!UICONTROL Datasets]** om alleen de gegevensstromen met gegevenssetexport weer te geven.
   ![&#x200B; Schermafbeelding die toont hoe te om dataflows door gegevenstype te filtreren.](/help/destinations/assets/ui/export-datasets/dataset-type.png)
4. Selecteer de kolomkop **[!UICONTROL Created]** en kies **[!UICONTROL Sort Ascending]** om de oudere gegevensstromen weer te geven.
   ![&#x200B; Scherenshot die toont hoe te om gegevens te sorteren oplopend.](/help/destinations/assets/ui/export-datasets/sort-ascending.png)
5. Identificeer welke dataflows die vóór November 2024 worden gecreeerd u wilt houden.

## Stap 2: Toegang tot de werkstroom van de uitvoerdatasets {#access-workflow}

Voor elke dataflow die u wilt houden, moet u tot het werkschema van de uitvoerdatasets toegang hebben om het programma te wijzigen.

1. Selecteer de naam van de gegevensstroom in de kolom **[!UICONTROL Name]** . Hiermee gaat u naar de pagina **[!UICONTROL Dataflow runs]** .
2. Selecteer op deze pagina de optie **[!UICONTROL Export datasets]** .
   ![&#x200B; Screenshot die de optie van de uitvoerdatasets in de dataflow looppas pagina toont.](/help/destinations/assets/ui/export-datasets/export-datasets-option.png)
3. Selecteer op de pagina **[!UICONTROL Select datasets]** de optie **[!UICONTROL Next]** . U te hoeven om geen nieuwe datasets aan dataflow toe te voegen.
4. Hiermee gaat u naar de pagina **[!UICONTROL Scheduling]** waar u ook een melding kunt zien waarin u wordt geïnformeerd over de vervaldatum van de gegevensset-export.
   ![&#x200B; de uitvoerdataflows van de Dataset met vervalbericht &#x200B;](/help/destinations/assets/ui/export-datasets/dataset-export-notification.png)

## Stap 3: Het exportschema uitbreiden {#extend-export-schedule}

Nu kunt u het uitvoerschema wijzigen om na 1 september 2025 te verlengen.

1. Selecteer **[!UICONTROL Edit schedule]**.
   ![&#x200B; Schermafbeelding van de Plannende stap die de Edit planningsknoop tonen.](/help/destinations/assets/ui/export-datasets/edit-schedule.png)
2. Selecteer een nieuw exportschema en selecteer vervolgens **[!UICONTROL Save]** .
   ![&#x200B; Schermafbeelding van de Plannende stap die de het plannen opties tonen.](/help/destinations/assets/ui/export-datasets/edit-schedule-calendar.png)

   >[!TIP]
   >
   >Controleer de [&#x200B; documentatie van de datasetuitvoer &#x200B;](export-datasets.md#scheduling) voor gedetailleerde begeleiding op hoe te om datasetuitvoerprogramma&#39;s te vormen.

## Wat gebeurt er als ik de deadline van 1 september 2025 mis? {#missed-deadline}

Als uw gegevensreeks de uitvoerdataflows op 1 September, 2025 verliep en u nog hen wilt uitbreiden, volg de stappen in de secties hierboven om hun programma uit te breiden.

Als u het uitvoerprogramma binnen 30 dagen uitbreidt (of minder als de [&#x200B; tijd-aan-levende reeks op de uitgevoerde dataset &#x200B;](/help/catalog/datasets/experience-event-dataset-retention-ttl-guide.md) minder dan 30 dagen is), kunt u nog een backfill van de gegevens krijgen die niet tussen 1 September en de datum werd uitgevoerd u de uitvoer opnieuw toelaten. Wanneer het plaatsen van een nieuwe eindtijd, zal er *niet* een volledige dossieruitvoer eerst zijn. In plaats daarvan zal de uitvoer stapsgewijs worden voortgezet vanaf het punt waar ze op 1 september zijn opgehouden.