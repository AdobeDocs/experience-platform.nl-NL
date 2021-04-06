---
keywords: doelen;doel;doeldetailpagina;doeldetailpagina;doeldetailpagina
title: Doelgegevens weergeven
description: 'De detailspagina voor een individuele bestemming verstrekt een overzicht van de bestemmingsdetails. De details van de bestemming omvatten de bestemmingsnaam, identiteitskaart, segmenten die aan de bestemming worden in kaart gebracht, en controles om de activering uit te geven en de gegevensstroom toe te laten en onbruikbaar te maken. '
seo-description: De detailspagina voor een individuele bestemming verstrekt een overzicht van de bestemmingsdetails. De details van de bestemming omvatten de bestemmingsnaam, identiteitskaart, segmenten die aan de bestemming worden in kaart gebracht, en controles om de activering uit te geven en de gegevensstroom toe te laten en onbruikbaar te maken.
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
translation-type: tm+mt
source-git-commit: cc432f7c07f0f82deec653864154016638ec8138
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# Doelgegevens weergeven

## Overzicht {#overview}

In de gebruikersinterface van Adobe Experience Platform, kunt u de attributen en de activiteiten van uw bestemmingen bekijken en controleren. Deze details omvatten de naam en identiteitskaart van de bestemming, controles om de bestemmingen te activeren of onbruikbaar te maken, en meer. De details voor partijbestemmingen omvatten ook metriek voor geactiveerde profielverslagen en een geschiedenis van dataflow looppas.

>[!NOTE]
>
>De pagina met doeldetails maakt deel uit van de [!UICONTROL Destinations] werkruimte in [!DNL Platform] [!DNL UI]. Zie het [[!UICONTROL Destinations] overzicht van de werkruimte](./destinations-workspace.md) voor meer informatie.

## Doeldetails {#view-details} weergeven

Voer de onderstaande stappen uit om meer informatie over een bestaand doel weer te geven.

1. Meld u aan bij [Experience Platform UI](https://platform.adobe.com/) en selecteer **[!UICONTROL Destinations]** in de linkernavigatiebalk. Selecteer **[!UICONTROL Browse]** van de hoogste kopbal om uw bestaande bestemmingen te bekijken.

   ![Bladeren door doelen](../assets/ui/details-page/browse-destinations.png)

1. Selecteer het filterpictogram ![Filter-pictogram](../assets/ui/details-page/filter.png) linksboven om het deelvenster Sorteren te starten. Het deelvenster Sorteren bevat een lijst met al uw doelen. U kunt meer dan één bestemming van de lijst selecteren om een gefilterde selectie van gegevensstromen te zien verbonden aan de geselecteerde bestemming.

   ![Filterdoelen](../assets/ui/details-page/filter-destinations.png)

1. Selecteer de naam van het doel dat u wilt bekijken.

   ![Doel selecteren](../assets/ui/details-page/destination-select.png)

1. De detailspagina voor de bestemming verschijnt, tonend zijn beschikbare controles. Als u de details van een batchbestemming bekijkt, wordt ook een dashboard voor de bewaking weergegeven.

   ![Doelgegevens](../assets/ui/details-page/destination-details.png)

## Rechterspoor

De rechterrails geven de basisinformatie over de geselecteerde bestemming weer.

![rechterspoor](../assets/ui/details-page/right-sidebar.png)

In de volgende tabel worden de door het rechterspoor verstrekte controles en gegevens vermeld:

| Rechterspoor | Beschrijving |
| --- | --- |
| [!UICONTROL Activate] | Selecteer deze controle om uit te geven welke segmenten aan de bestemming in kaart worden gebracht. Zie de gids op [activerende segmenten aan een bestemming](./activate-destinations.md) voor meer informatie. |
| [!UICONTROL Delete] | Hiermee kunt u deze gegevensstroom verwijderen en de toewijzingen van eerder geactiveerde segmenten ongedaan maken, indien aanwezig. |
| [!UICONTROL Destination name] | Dit veld kan worden bewerkt om de naam van het doel bij te werken. |
| [!UICONTROL Description] | Dit veld kan worden bewerkt om een optionele beschrijving aan het doel toe te voegen. |
| [!UICONTROL Destination] | Vertegenwoordigt het bestemmingsplatform dat het publiek wordt verzonden naar. Zie [doelcatalogus](../catalog/overview.md) voor meer informatie. |
| [!UICONTROL Status] | Geeft aan of het doel is in- of uitgeschakeld. |
| [!UICONTROL Marketing actions] | Hiermee worden de marketingacties (gebruiksgevallen) aangegeven die voor deze bestemming gelden voor doeleinden van gegevensbeheer. |
| [!UICONTROL Category] | Geeft het doeltype aan. Zie [doelcatalogus](../catalog/overview.md) voor meer informatie. |
| [!UICONTROL Connection type] | Hiermee geeft u de vorm aan waarmee uw publiek naar het doel wordt gestuurd. Mogelijke waarden zijn [!UICONTROL Cookie] en [!UICONTROL Profile-based]. |
| [!UICONTROL Frequency] | Geeft aan hoe vaak het publiek naar de bestemming wordt gestuurd. Mogelijke waarden zijn [!UICONTROL Streaming] en [!UICONTROL Batch]. |
| [!UICONTROL Identity] | Vertegenwoordigt de identiteitsnaamruimte die door de bestemming wordt geaccepteerd, zoals `GAID`, `IDFA` of `email`. Zie [Naamruimte overzicht van naamruimte ](../../identity-service/namespaces.md) voor meer informatie over geaccepteerde naamruimten. |
| [!UICONTROL Created by] | Geeft de gebruiker aan die deze bestemming heeft gemaakt. |
| [!UICONTROL Created] | Hiermee wordt de UTC-datetime aangegeven waarop deze bestemming is gemaakt. |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL Enabled]/[!UICONTROL Disabled] toggle

Met de schakeloptie **[!UICONTROL Enabled]/[!UICONTROL Disabled]** kunt u alle gegevens die u exporteert naar de bestemming starten en pauzeren.

![Schakelen tussen uitschakelen inschakelen](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Dataflow runs]

Het [!UICONTROL Dataflow runs] lusje verstrekt metrische gegevens over uw dataflow looppas aan partijbestemmingen. Raadpleeg [Dataflows](monitor-dataflows.md) voor meer informatie.

## [!UICONTROL Activation data] {#activation-data}

Het [!UICONTROL Activation data] lusje toont een lijst van segmenten die aan de bestemming, met inbegrip van hun begindatum en einddatum (indien van toepassing) in kaart zijn gebracht. Als u de details over een bepaald segment wilt weergeven, selecteert u de naam in de lijst.

![Activeringsgegevens](../assets/ui/details-page/activation-data.png)

>[!NOTE]
>
>Voor details bij het onderzoeken van de detailspagina van een segment, verwijs naar [Overzicht van de Segmentatie UI](../../segmentation/ui/overview.md#segment-details).
