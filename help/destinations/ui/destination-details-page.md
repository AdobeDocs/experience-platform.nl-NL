---
keywords: destinations;destination;destinations detail page;destinations details page
title: Pagina Gegevens bestemming
seo-title: Pagina Gegevens bestemming
description: 'De detailspagina voor een individuele bestemming verstrekt een overzicht van de bestemmingsdetails, zoals de bestemmingsnaam, identiteitskaart, segmenten aan de bestemming in kaart worden gebracht, en controles om de activering uit te geven en de gegevensstroom toe te laten en onbruikbaar te maken. '
seo-description: 'De detailspagina voor een individuele bestemming verstrekt een overzicht van de bestemmingsdetails, zoals de bestemmingsnaam, identiteitskaart, segmenten aan de bestemming in kaart worden gebracht, en controles om de activering uit te geven en de gegevensstroom toe te laten en onbruikbaar te maken. '
translation-type: tm+mt
source-git-commit: 5f120a716cc3396ef7749463bb6052a8ced2fbb4
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 1%

---


# Pagina met doeldetails

In de gebruikersinterface van Adobe Experience Platform, kunt u de attributen en de activiteiten van uw bestemmingen bekijken en controleren. Deze details omvatten de naam en identiteitskaart van de bestemming, controles om de bestemmingen te activeren of onbruikbaar te maken, en meer. De details voor partijbestemmingen omvatten ook metriek voor geactiveerde profielverslagen en een geschiedenis van dataflow looppas.

>[!NOTE]
>
>De pagina met bestemmingsdetails maakt deel uit van de werkruimte [!UICONTROL Doelen] in de gebruikersinterface van het Platform. Zie het overzicht [[!UICONTROL van de werkruimte van] Doelen](./destinations-workspace.md) voor meer informatie.

Navigeer in de werkruimte **[!UICONTROL Doelen]** in de interface van het Platform naar het tabblad **[!UICONTROL Bladeren]** en selecteer de naam van een bestemming die u wilt weergeven.

![](../assets/ui/details-page/select-destination.png)

De detailspagina voor de bestemming verschijnt, tonend zijn beschikbare controles. Als u de details van een batchbestemming bekijkt, wordt ook een dashboard voor de bewaking weergegeven.

![](../assets/ui/details-page/details.png)

## Rechterspoor

De juiste spoorstaaf toont de basisinformatie over de bestemming.

![](../assets/ui/details-page/right-rail.png)

In de volgende tabel worden de door het rechterspoor verstrekte controles en gegevens vermeld:

| Rechterspoor | Beschrijving |
| --- | --- |
| [!UICONTROL Activeren] | Selecteer deze controle om uit te geven welke segmenten aan de bestemming in kaart worden gebracht. Zie de gids bij het [activeren van segmenten aan een bestemming](./activate-destinations.md) voor meer informatie. |
| [!UICONTROL Doelnaam] | Dit veld kan worden bewerkt om de naam van het doel bij te werken. |
| [!UICONTROL Beschrijving] | Dit veld kan worden bewerkt om een optionele beschrijving aan het doel toe te voegen. |
| [!UICONTROL Bestemming] | Vertegenwoordigt het bestemmingsplatform dat het publiek wordt verzonden naar. Zie de [bestemmingscatalogus](../catalog/overview.md) voor meer informatie. |
| [!UICONTROL Status] | Geeft aan of het doel is in- of uitgeschakeld. |
| [!UICONTROL Marketingacties] | Hiermee worden de marketingacties (gebruiksgevallen) aangegeven die voor deze bestemming gelden voor doeleinden van gegevensbeheer. |
| [!UICONTROL Categorie] | Geeft het doeltype aan. Zie de [bestemmingscatalogus](../catalog/overview.md) voor meer informatie. |
| [!UICONTROL Verbindingstype] | Hiermee geeft u de vorm aan waarmee uw publiek naar het doel wordt gestuurd. Mogelijke waarden zijn &quot;[!UICONTROL Cookie]&quot; en &quot;[!UICONTROL Op profiel gebaseerd]&quot;. |
| [!UICONTROL Frequentie] | Geeft aan hoe vaak het publiek naar de bestemming wordt gestuurd. Mogelijke waarden zijn &quot;[!UICONTROL Streaming]&quot; en &quot;[!UICONTROL Batch]&quot;. |
| [!UICONTROL Identiteit] | Vertegenwoordigt de identiteitsnaamruimte die door de bestemming wordt geaccepteerd, zoals `GAID`, `IDFA`of `email`. Zie het overzicht [van naamruimte](../../identity-service/namespaces.md)voor identiteiten voor meer informatie over geaccepteerde naamruimten. |
| [!UICONTROL Gemaakt door] | Geeft de gebruiker aan die deze bestemming heeft gemaakt. |
| [!UICONTROL Gemaakt] | Hiermee wordt de UTC-datetime aangegeven waarop deze bestemming is gemaakt. |

## [!UICONTROL Ingeschakeld]/[!UICONTROL Uitgeschakeld]

U kunt de **[!UICONTROL Toegelaten]/[!UICONTROL Uitgeschakelde]** knevel gebruiken om alle gegevensuitvoer naar de bestemming te beginnen en te pauzeren.

![](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Dataflow-uitvoering]

Het [!UICONTROL Dataflow looppas] lusje verstrekt metrische gegevens over uw dataflow looppas aan partijbestemmingen. Er wordt een lijst weergegeven met afzonderlijke uitvoeringen en de bijbehorende maatstaven, samen met de volgende totalen voor profielrecords:

* **[!UICONTROL Profielrecords geactiveerd]**: Het totale aantal profielrecords dat voor activering is gemaakt of bijgewerkt.
* **[!UICONTROL Profielrecords overgeslagen]**:  Het totale aantal profielrecords dat voor activering wordt overgeslagen op basis van het profiel, wordt afgesloten of ontbrekende kenmerken.

![](../assets/ui/details-page/dataflow-runs.png)

>[!NOTE]
>
>De looppas van Dataflow wordt geproduceerd gebaseerd op de planningsfrequentie van bestemmingsdataflow. Een afzonderlijke dataflow looppas wordt gemaakt voor elk samenvoegbeleid dat op een segment wordt toegepast.

Om de details van een bepaalde dataflow looppas te bekijken, selecteer de begintijd van de looppas van de lijst. De detailpagina voor een dataflow-run bevat aanvullende informatie zoals de grootte van de verwerkte gegevens en een lijst met eventuele fouten die zijn opgetreden met details voor de diagnose van fouten.

![](../assets/ui/details-page/dataflow.png)

## [!UICONTROL Segmenten]

Op het tabblad [!UICONTROL Segmenten] wordt een lijst weergegeven met segmenten die aan de bestemming zijn toegewezen, inclusief de begindatum en einddatum (indien van toepassing). Als u de details over een bepaald segment wilt weergeven, selecteert u de naam in de lijst.

![](../assets/ui/details-page/segments.png)

>[!NOTE]
>
>Voor details bij het onderzoeken van de detailspagina van een segment, verwijs naar het overzicht [van de](../../segmentation/ui/overview.md#segment-details)Segmentatie UI.

## Volgende stappen

Dit document besprak de mogelijkheden van de pagina met doeldetails. Voor meer informatie bij het beheren van bestemmingen in UI, zie het overzicht op de [[!UICONTROL werkruimte] van Doelen](./destinations-workspace.md).