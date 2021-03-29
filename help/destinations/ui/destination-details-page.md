---
keywords: doelen;doel;doeldetailpagina;doeldetailpagina;doeldetailpagina
title: Doelgegevens weergeven
description: 'De detailspagina voor een individuele bestemming verstrekt een overzicht van de bestemmingsdetails. De details van de bestemming omvatten de bestemmingsnaam, identiteitskaart, segmenten die aan de bestemming worden in kaart gebracht, en controles om de activering uit te geven en de gegevensstroom toe te laten en onbruikbaar te maken. '
seo-description: 'De detailspagina voor een individuele bestemming verstrekt een overzicht van de bestemmingsdetails. De details van de bestemming omvatten de bestemmingsnaam, identiteitskaart, segmenten die aan de bestemming worden in kaart gebracht, en controles om de activering uit te geven en de gegevensstroom toe te laten en onbruikbaar te maken. '
translation-type: tm+mt
source-git-commit: 4f5e7dfee17b2dde371efb82cf52d91c08696f39
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 0%

---


# Doelgegevens weergeven

## Overzicht {#overview}

In de gebruikersinterface van Adobe Experience Platform, kunt u de attributen en de activiteiten van uw bestemmingen bekijken en controleren. Deze details omvatten de naam en identiteitskaart van de bestemming, controles om de bestemmingen te activeren of onbruikbaar te maken, en meer. De details voor partijbestemmingen omvatten ook metriek voor geactiveerde profielverslagen en een geschiedenis van dataflow looppas.

>[!NOTE]
>
>De pagina met doeldetails maakt deel uit van de werkruimte [!UICONTROL Destinations] in de gebruikersinterface van het Platform. Zie het [[!UICONTROL Destinations] overzicht van de werkruimte](./destinations-workspace.md) voor meer informatie.

Navigeer in de **[!UICONTROL Destinations]** werkruimte in de interface van het Platform naar het tabblad **[!UICONTROL Browse]** en selecteer de naam van een doel dat u wilt weergeven.

![](../assets/ui/details-page/select-destination.png)

De detailspagina voor de bestemming verschijnt, tonend zijn beschikbare controles. Als u de details van een batchbestemming bekijkt, wordt ook een dashboard voor de bewaking weergegeven.

![](../assets/ui/details-page/details.png)

Daarnaast kunt u op het tabblad Bladeren de geselecteerde gegevensstroom verwijderen door het pictogram ![prullenbak](../assets/ui/details-page/trash-icon.png) te selecteren. Om het even welke segmenten die aan bestemmingen worden geactiveerd zullen worden unmapped alvorens dataflow wordt geschrapt.

![](../assets/ui/details-page/delete-flow.png)

## Rechterspoor

De juiste spoorstaaf toont de basisinformatie over de bestemming.

![](../assets/ui/details-page/right-rail.png)

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
| [!UICONTROL Connection type] | Hiermee geeft u de vorm aan waarmee uw publiek naar het doel wordt gestuurd. Mogelijke waarden zijn &quot;[!UICONTROL Cookie]&quot; en &quot;[!UICONTROL Profile-based]&quot;. |
| [!UICONTROL Frequency] | Geeft aan hoe vaak het publiek naar de bestemming wordt gestuurd. Mogelijke waarden zijn &quot;[!UICONTROL Streaming]&quot; en &quot;[!UICONTROL Batch]&quot;. |
| [!UICONTROL Identity] | Vertegenwoordigt de identiteitsnaamruimte die door de bestemming wordt geaccepteerd, zoals `GAID`, `IDFA` of `email`. Zie [Naamruimte overzicht van naamruimte ](../../identity-service/namespaces.md) voor meer informatie over geaccepteerde naamruimten. |
| [!UICONTROL Created by] | Geeft de gebruiker aan die deze bestemming heeft gemaakt. |
| [!UICONTROL Created] | Hiermee wordt de UTC-datetime aangegeven waarop deze bestemming is gemaakt. |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL Enabled]/[!UICONTROL Disabled] toggle

Met de schakeloptie **[!UICONTROL Enabled]/[!UICONTROL Disabled]** kunt u alle gegevens die u exporteert naar de bestemming starten en pauzeren.

![](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Dataflow runs]

Het [!UICONTROL Dataflow runs] lusje verstrekt metrische gegevens over uw dataflow looppas aan partijbestemmingen. Er wordt een lijst weergegeven met afzonderlijke uitvoeringen en de bijbehorende maatstaven, samen met de volgende totalen voor profielrecords:

* **[!UICONTROL Profile records activated]**: Het totale aantal profielrecords dat voor activering is gemaakt of bijgewerkt.
* **[!UICONTROL Profile records skipped]**: Het totale aantal profielrecords dat voor activering wordt overgeslagen op basis van het profiel, wordt afgesloten of ontbrekende kenmerken.

![](../assets/ui/details-page/dataflow-runs.png)

>[!NOTE]
>
>De looppas van Dataflow wordt geproduceerd gebaseerd op de planningsfrequentie van bestemmingsdataflow. Een afzonderlijke dataflow looppas wordt gemaakt voor elk samenvoegbeleid dat op een segment wordt toegepast.

Om de details van een bepaalde dataflow looppas te bekijken, selecteer de begintijd van de looppas van de lijst. De detailpagina voor een dataflow-run bevat aanvullende informatie zoals de grootte van de verwerkte gegevens en een lijst met eventuele fouten die zijn opgetreden met details voor de diagnose van fouten.

![](../assets/ui/details-page/dataflow.png)

## [!UICONTROL Activation data] {#activation-data}

Het [!UICONTROL Activation data] lusje toont een lijst van segmenten die aan de bestemming, met inbegrip van hun begindatum en einddatum (indien van toepassing) in kaart zijn gebracht. Als u de details over een bepaald segment wilt weergeven, selecteert u de naam in de lijst.

![](../assets/ui/details-page/activation-data.png)

>[!NOTE]
>
>Voor details bij het onderzoeken van de detailspagina van een segment, verwijs naar [Overzicht van de Segmentatie UI](../../segmentation/ui/overview.md#segment-details).

## Volgende stappen

Dit document besprak de mogelijkheden van de pagina met doeldetails. Voor meer informatie bij het beheren van bestemmingen in UI, zie het overzicht op [[!UICONTROL Destinations] werkruimte](./destinations-workspace.md).