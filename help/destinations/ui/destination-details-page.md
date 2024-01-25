---
keywords: doelen;doel;doeldetailpagina;doeldetailpagina;doeldetailpagina
title: Doelgegevens weergeven
description: De detailspagina voor een individuele bestemming verstrekt een overzicht van de bestemmingsdetails. De details van de bestemming omvatten de bestemmingsnaam, identiteitskaart, publiek in kaart gebracht aan de bestemming, en controles om de activering uit te geven en de gegevensstroom toe te laten en onbruikbaar te maken.
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 0%

---

# Doelgegevens weergeven

## Overzicht {#overview}

In de gebruikersinterface van Adobe Experience Platform, kunt u de attributen en de activiteiten van uw bestemmingen bekijken en controleren. Deze details omvatten de naam en identiteitskaart van de bestemming, controles om de bestemmingen te activeren of onbruikbaar te maken, en meer. De details omvatten ook metriek voor geactiveerd profielverslagen, geactiveerde identiteiten, ontbroken, en uitgesloten, en een geschiedenis van dataflow looppas.

>[!NOTE]
>
>De pagina met doeldetails maakt deel uit van de [!UICONTROL Destinations] werkruimte in de [!DNL Platform] [!DNL UI]. Zie de [[!UICONTROL Destinations] werkruimte - overzicht](./destinations-workspace.md) voor meer informatie .

## Doelgegevens weergeven {#view-details}

Voer de onderstaande stappen uit om meer informatie over een bestaand doel weer te geven.

1. Aanmelden bij de [UI EXPERIENCE PLATFORM](https://platform.adobe.com/) en selecteert u **[!UICONTROL Destinations]** in de linkernavigatiebalk. Selecteren **[!UICONTROL Browse]** van de hoogste kopbal om uw bestaande bestemmingen te bekijken.

   ![Bladeren door doelen](../assets/ui/details-page/browse-destinations.png)

1. Filterpictogram selecteren ![Filter-pictogram](../assets/ui/details-page/filter.png) bovenaan links om het deelvenster Sorteren te starten. Het deelvenster Sorteren bevat een lijst met al uw doelen. U kunt meer dan één bestemming van de lijst selecteren om een gefilterde selectie van gegevensstromen te zien verbonden aan de geselecteerde bestemming.

   ![Filterdoelen](../assets/ui/details-page/filter-destinations.png)

1. Selecteer de naam van het doel dat u wilt bekijken.

   ![Doel selecteren](../assets/ui/details-page/destination-select.png)

1. De detailspagina voor de bestemming verschijnt, tonend zijn beschikbare controles.

   ![Doelgegevens](../assets/ui/details-page/destination-details.png)

## Rechterspoor {#right-rail}

De rechterrails geven de basisinformatie over de geselecteerde bestemming weer.

![rechterspoor](../assets/ui/details-page/right-sidebar.png)

In de volgende tabel worden de door het rechterspoor verstrekte controles en gegevens vermeld:

| Rechterspoor | Beschrijving |
| --- | --- |
| [!UICONTROL Activate audiences] | Selecteer dit besturingselement om te bewerken welk publiek wordt toegewezen aan het doel, om exportschema&#39;s bij te werken of om toegewezen kenmerken en identiteiten toe te voegen en te verwijderen. Zie de hulplijnen op [het activeren van publieksgegevens aan publiek die bestemmingen stromen](./activate-segment-streaming-destinations.md), [het activeren van publieksgegevens aan batch op profiel-gebaseerde bestemmingen](./activate-batch-profile-destinations.md), en [het activeren van publieksgegevens aan het stromen op profiel-gebaseerde bestemmingen](./activate-streaming-profile-destinations.md) voor meer informatie . |
| [!UICONTROL Delete] | Hiermee kunt u deze gegevensstroom verwijderen en de toewijzing ongedaan maken van het publiek dat eerder is geactiveerd, indien aanwezig. |
| [!UICONTROL Destination name] | Dit veld kan worden bewerkt om de naam van het doel bij te werken. |
| [!UICONTROL Description] | Dit veld kan worden bewerkt om een optionele beschrijving aan het doel bij te werken of toe te voegen. |
| [!UICONTROL Destination] | Vertegenwoordigt het bestemmingsplatform dat het publiek wordt verzonden naar. Zie de [doelcatalogus](../catalog/overview.md) voor meer informatie . |
| [!UICONTROL Status] | Geeft aan of het doel is in- of uitgeschakeld. |
| [!UICONTROL Marketing actions] | Hiermee worden de marketingacties (gebruiksgevallen) aangegeven die voor deze bestemming gelden voor doeleinden van gegevensbeheer. |
| [!UICONTROL Category] | Geeft het doeltype aan. Zie de [doelcatalogus](../catalog/overview.md) voor meer informatie . |
| [!UICONTROL Connection type] | Hiermee geeft u de vorm aan waarmee uw publiek naar het doel wordt gestuurd. Mogelijke waarden zijn [!UICONTROL Cookie] en [!UICONTROL Profile-based]. |
| [!UICONTROL Frequency] | Geeft aan hoe vaak het publiek naar de bestemming wordt gestuurd. Mogelijke waarden zijn [!UICONTROL Streaming] en [!UICONTROL Batch]. |
| [!UICONTROL Identity] | Vertegenwoordigt de identiteitsnaamruimte die door de bestemming wordt geaccepteerd, zoals `GAID`, `IDFA`, of `email`. Voor meer informatie over geaccepteerde naamruimten raadpleegt u de [Overzicht van naamruimte in identiteit](../../identity-service/features/namespaces.md). |
| [!UICONTROL Created by] | Geeft de gebruiker aan die deze bestemming heeft gemaakt. |
| [!UICONTROL Created] | Hiermee wordt de UTC-datetime aangegeven waarop deze bestemming is gemaakt. |

{style="table-layout:auto"}

## [!UICONTROL Enabled]/[!UICONTROL Disabled] schakelen {#enabled-disabled-toggle}

U kunt de **[!UICONTROL Enabled]/[!UICONTROL Disabled]** schakelen om alle gegevens die u exporteert naar de bestemming te starten en pauzeren.

![Dataflow-schakeloptie in- of uitschakelen](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Dataflow runs] {#dataflow-runs}

De [!UICONTROL Dataflow runs] tab bevat metrische gegevens over uw gegevensstroom die naar batch- en streaming doelen worden uitgevoerd. Zie [Dataflows bewaken](monitor-dataflows.md) voor details en metrische definities.

>[!NOTE]
>
>* Functionaliteit voor het controleren van doelen wordt momenteel ondersteund voor alle doelen in Experience Platform *behalve* de [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md), [Aangepaste personalisatie](/help/destinations/catalog/personalization/custom-personalization.md) en [Soorten publiek Experience Cloud](/help/destinations/catalog/adobe/experience-cloud-audiences.md) bestemmingen.
>* Voor de [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md), en [HTTP-API](/help/destinations/catalog/streaming/http-destination.md) doelen, de metriek met betrekking tot uitgesloten, mislukte en geactiveerde identiteiten worden geschat. Hogere volumes activeringsgegevens leiden tot een hogere nauwkeurigheid van de meetwaarden.

![Dataflow-run-weergave](../assets/ui/details-page/dataflow-runs.png)

### Runtimeduur gegevensstroom {#dataflow-runs-duration}

Er is een verschil in de getoonde duur van dataflow looppas tussen het stromen en op dossier-gebaseerde bestemmingen.

### Streaming doelen {#streaming}

Terwijl de **[!UICONTROL Processing duration]** Voor de meeste streaming dataflow-runtime is dit ongeveer vier uur, zoals in de onderstaande afbeelding wordt getoond, is de werkelijke verwerkingstijd voor elke dataflow-run veel korter. Dataflow runtime vensters blijven open voor langer in het geval dat het Experience Platform moet opnieuw proberen makend vraag aan de bestemming en ook ervoor zorgen het niet op om het even welk laat aankomen gegevens voor zelfde tijdvenster mist.

![Afbeelding van de DataFlow voert de pagina uit met de kolom Verwerkingstijd gemarkeerd voor een streamingdoel.](/help/destinations/assets/ui/details-page/processing-time-dataflow-run-streaming.png)

Lees voor meer informatie over [dataflow wordt uitgevoerd naar streamingdoelen](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations) in de monitoringdocumentatie.

### Bestandsgebaseerde doelen {#file-based}

Voor dataflow wordt uitgevoerd naar op een bestand gebaseerde doelen, wordt de **[!UICONTROL Processing duration]** is afhankelijk van de grootte van de gegevens die worden geëxporteerd en het laden van het systeem. Bericht ook dat de dataflow looppas aan op dossier-gebaseerde bestemmingen uitgesplitst per publiek is.

![Afbeelding van de DataFlow voert de pagina uit met de kolom Verwerkingstijd gemarkeerd voor een op een bestand gebaseerd doel.](/help/destinations/assets/ui/details-page/processing-time-dataflow-run-file-based.png)

Lees voor meer informatie over [dataflow wordt uitgevoerd naar batchbestemmingen (op basis van bestanden)](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) in de monitoringdocumentatie.

## [!UICONTROL Activation data] {#activation-data}

De [!UICONTROL Activation data] wordt een lijst weergegeven van soorten publiek dat aan de bestemming is toegewezen, met inbegrip van hun begindatum en einddatum (indien van toepassing), en andere relevante informatie voor de gegevensexport, zoals het exporttype, de planning en de frequentie. Als u de details over een bepaald publiek wilt weergeven, selecteert u de naam in de lijst.

>[!TIP]
>
>Als u details wilt weergeven en bewerken over de kenmerken en identiteiten die aan een doel zijn toegewezen, selecteert u **[!UICONTROL Activate audiences]** in de [rechterspoor](#right-rail).

![Batchbestemming voor weergave van activeringsgegevens](../assets/ui/details-page/activation-data-batch.png)

![Streaming doel van gegevensweergave activeren](../assets/ui/details-page/activation-data-streaming.png)

>[!NOTE]
>
>Raadpleeg voor meer informatie over het verkennen van de detailpagina van een publiek de [Overzicht van de segmenteringsinterface](../../segmentation/ui/overview.md#segment-details).
