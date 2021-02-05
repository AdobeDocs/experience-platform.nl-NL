---
keywords: doelen;doel;doeldetailpagina;doeldetailpagina;doeldetailpagina
title: Bekijk de Details van een Doel in UI
description: 'De detailspagina voor een individuele bestemming verstrekt een overzicht van de bestemmingsdetails, zoals de bestemmingsnaam, identiteitskaart, segmenten aan de bestemming in kaart worden gebracht, en controles om de activering uit te geven en de gegevensstroom toe te laten en onbruikbaar te maken. '
seo-description: 'De detailspagina voor een individuele bestemming verstrekt een overzicht van de bestemmingsdetails, zoals de bestemmingsnaam, identiteitskaart, segmenten aan de bestemming in kaart worden gebracht, en controles om de activering uit te geven en de gegevensstroom toe te laten en onbruikbaar te maken. '
translation-type: tm+mt
source-git-commit: 8d403e73a804953f9584d6a72f945d4444e65d11
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 1%

---


# De details van een bestemming weergeven

In de gebruikersinterface van Adobe Experience Platform, kunt u de attributen en de activiteiten van uw bestemmingen bekijken en controleren. Deze details omvatten de naam en identiteitskaart van de bestemming, controles om de bestemmingen te activeren of onbruikbaar te maken, en meer. De details voor partijbestemmingen omvatten ook metriek voor geactiveerde profielverslagen en een geschiedenis van dataflow looppas.

>[!NOTE]
>
>De pagina van bestemmingsdetails is een deel van [!UICONTROL Doelen] werkruimte in de UI van het Platform. Zie [[!UICONTROL Doelen] werkruimte overzicht](./destinations-workspace.md) voor meer informatie.

In **[!UICONTROL De werkruimte van Doelen]** binnen het Platform UI, navigeert aan **[!UICONTROL doorbladert]** tabel en selecteert de naam van een bestemming die u wilt bekijken.

![](../assets/ui/details-page/select-destination.png)

De detailspagina voor de bestemming verschijnt, tonend zijn beschikbare controles. Als u de details van een batchbestemming bekijkt, wordt ook een dashboard voor de bewaking weergegeven.

![](../assets/ui/details-page/details.png)

Daarnaast kunt u op het tabblad Bladeren de geselecteerde gegevensstroom verwijderen door het pictogram ![prullenbak](../assets/ui/details-page/trash-icon.png) te selecteren. Om het even welke segmenten die aan een bestemmingen worden geactiveerd zullen unmapped alvorens dataflow wordt geschrapt.

![](../assets/ui/details-page/delete-flow.png)

## Rechterspoor

De juiste spoorstaaf toont de basisinformatie over de bestemming.

![](../assets/ui/details-page/right-rail.png)

In de volgende tabel worden de door het rechterspoor verstrekte controles en gegevens vermeld:

| Rechterspoor | Beschrijving |
| --- | --- |
| [!UICONTROL Activeren] | Selecteer deze controle om uit te geven welke segmenten aan de bestemming in kaart worden gebracht. Zie de gids op [activerende segmenten aan een bestemming](./activate-destinations.md) voor meer informatie. |
| [!UICONTROL Verwijderen] | Hiermee kunt u deze gegevensstroom verwijderen en de eerder geactiveerde segmenten, indien aanwezig, deactiveren. |
| [!UICONTROL Doelnaam] | Dit veld kan worden bewerkt om de naam van het doel bij te werken. |
| [!UICONTROL Beschrijving] | Dit veld kan worden bewerkt om een optionele beschrijving aan het doel toe te voegen. |
| [!UICONTROL Bestemming] | Vertegenwoordigt het bestemmingsplatform dat het publiek wordt verzonden naar. Zie [doelcatalogus](../catalog/overview.md) voor meer informatie. |
| [!UICONTROL Status] | Geeft aan of het doel is in- of uitgeschakeld. |
| [!UICONTROL Marketingacties] | Hiermee worden de marketingacties (gebruiksgevallen) aangegeven die voor deze bestemming gelden voor doeleinden van gegevensbeheer. |
| [!UICONTROL Categorie] | Geeft het doeltype aan. Zie [doelcatalogus](../catalog/overview.md) voor meer informatie. |
| [!UICONTROL Verbindingstype] | Hiermee geeft u de vorm aan waarmee uw publiek naar het doel wordt gestuurd. Mogelijke waarden zijn &quot;[!UICONTROL Cookie]&quot; en &quot;[!UICONTROL Op profiel gebaseerde]&quot;. |
| [!UICONTROL Frequentie] | Geeft aan hoe vaak het publiek naar de bestemming wordt gestuurd. Mogelijke waarden zijn &quot;[!UICONTROL Streaming]&quot; en &quot;[!UICONTROL Batch]&quot;. |
| [!UICONTROL Identiteit] | Vertegenwoordigt de identiteitsnaamruimte die door de bestemming wordt geaccepteerd, zoals `GAID`, `IDFA` of `email`. Zie [Naamruimte overzicht van naamruimte ](../../identity-service/namespaces.md) voor meer informatie over geaccepteerde naamruimten. |
| [!UICONTROL Gemaakt door] | Geeft de gebruiker aan die deze bestemming heeft gemaakt. |
| [!UICONTROL Gemaakt] | Hiermee wordt de UTC-datetime aangegeven waarop deze bestemming is gemaakt. |

## [!UICONTROL Ingeschakeld]/ Uitgeschakeld

U kunt **[!UICONTROL Ingeschakeld ]/[!UICONTROL Uitgeschakeld]** gebruiken om alle gegevensexport naar de bestemming te starten en te pauzeren.

![](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Dataflow-uitvoering]

Het [!UICONTROL lusje Dataflow looppas] verstrekt metrische gegevens op uw dataflow looppas aan partijbestemmingen. Er wordt een lijst weergegeven met afzonderlijke uitvoeringen en de bijbehorende maatstaven, samen met de volgende totalen voor profielrecords:

* **[!UICONTROL Profielrecords geactiveerd]**: Het totale aantal profielrecords dat voor activering is gemaakt of bijgewerkt.
* **[!UICONTROL Profielrecords overgeslagen]**: Het totale aantal profielrecords dat voor activering wordt overgeslagen op basis van het profiel, wordt afgesloten of ontbrekende kenmerken.

![](../assets/ui/details-page/dataflow-runs.png)

>[!NOTE]
>
>De looppas van Dataflow wordt geproduceerd gebaseerd op de planningsfrequentie van bestemmingsdataflow. Een afzonderlijke dataflow looppas wordt gemaakt voor elk samenvoegbeleid dat op een segment wordt toegepast.

Om de details van een bepaalde dataflow looppas te bekijken, selecteer de begintijd van de looppas van de lijst. De detailpagina voor een dataflow-run bevat aanvullende informatie zoals de grootte van de verwerkte gegevens en een lijst met eventuele fouten die zijn opgetreden met details voor de diagnose van fouten.

![](../assets/ui/details-page/dataflow.png)

## [!UICONTROL Activeringsgegevens]

Op het tabblad [!UICONTROL Activeringsgegevens] wordt een lijst weergegeven met segmenten die aan de bestemming zijn toegewezen, inclusief de begindatum en einddatum (indien van toepassing). Als u de details over een bepaald segment wilt weergeven, selecteert u de naam in de lijst.

![](../assets/ui/details-page/activation-data.png)

>[!NOTE]
>
>Voor details bij het onderzoeken van de detailspagina van een segment, verwijs naar [Overzicht van de Segmentatie UI](../../segmentation/ui/overview.md#segment-details).

## Volgende stappen

Dit document besprak de mogelijkheden van de pagina met doeldetails. Voor meer informatie over het beheren van bestemmingen in UI, zie het overzicht op [[!UICONTROL Doelen] werkruimte](./destinations-workspace.md).