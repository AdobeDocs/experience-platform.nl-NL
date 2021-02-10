---
keywords: doelen;doel;doeldetailpagina;doeldetailpagina;doeldetailpagina
title: Doelgegevens weergeven
description: 'De detailspagina voor een individuele bestemming verstrekt een overzicht van de bestemmingsdetails, zoals de bestemmingsnaam, identiteitskaart, segmenten aan de bestemming in kaart worden gebracht, en controles om de activering uit te geven en de gegevensstroom toe te laten en onbruikbaar te maken. '
seo-description: 'De detailspagina voor een individuele bestemming verstrekt een overzicht van de bestemmingsdetails, zoals de bestemmingsnaam, identiteitskaart, segmenten aan de bestemming in kaart worden gebracht, en controles om de activering uit te geven en de gegevensstroom toe te laten en onbruikbaar te maken. '
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 1%

---


# Doelgegevens weergeven

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
| [!UICONTROL Identiteit] | Vertegenwoordigt de identiteitsnaamruimte die door de bestemming wordt geaccepteerd, zoals `GAID`, `IDFA` of `email`. Zie [Overzicht van naamruimte voor identiteiten](../../identity-service/namespaces.md) voor meer informatie over geaccepteerde naamruimten. |
| [!UICONTROL Gemaakt door] | Hiermee wordt de gebruiker aangegeven die deze bestemming heeft gemaakt. |
| [!UICONTROL Gemaakt] | Geeft de UTC-datum aan waarop deze bestemming is gemaakt. |

## [!UICONTROL Ingeschakeld]/ Uitgeschakeld

U kunt de schakelknop **[!UICONTROL Ingeschakeld]/[!UICONTROL Uitgeschakeld]** gebruiken om alle gegevensexports naar de bestemming te starten en te pauzeren.

![](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Dataflow-runs]

Het [!UICONTROL tabblad Dataflow bevat metrische gegevens over de dataflow die worden uitgevoerd naar batchbestemmingen. ] Er wordt een lijst met afzonderlijke runs en de bijbehorende metrics weergegeven, samen met de volgende totalen voor profielrecords:

* **[!UICONTROL Profielrecords geactiveerd]**: Het totale aantal profielrecords dat voor activering is gemaakt of bijgewerkt.
* **[!UICONTROL Profielrecords overgeslagen]**: Het totale aantal profielrecords dat voor activering wordt overgeslagen op basis van het profiel bestaat uit of ontbrekende kenmerken.

![](../assets/ui/details-page/dataflow-runs.png)

>[!NOTE]
>
>Dataflow-runs worden gegenereerd op basis van de planningsfrequentie van de doeldata. Een afzonderlijke dataflow looppas wordt gemaakt voor elk samenvoegbeleid dat op een segment wordt toegepast.

Als u de details van een bepaalde gegevensstroom wilt bekijken, selecteert u de begintijd van de runtime in de lijst. De detailpagina voor een dataflow-run bevat aanvullende informatie zoals de grootte van de verwerkte gegevens en een lijst met fouten die zijn opgetreden met details voor foutdiagnostiek.

![](../assets/ui/details-page/dataflow.png)

## [!UICONTROL Activeringsgegevens]

Op het tabblad [!UICONTROL Activeringsgegevens] wordt een lijst weergegeven met segmenten die aan de bestemming zijn toegewezen, inclusief de begin- en einddatum (indien van toepassing). Als u de details van een bepaald segment wilt bekijken, selecteert u de naam in de lijst.

![](../assets/ui/details-page/activation-data.png)

>[!NOTE]
>
>Raadpleeg het [Overzicht van de segmentatie-UI](../../segmentation/ui/overview.md#segment-details) voor meer informatie over het verkennen van de detailpagina van een segment.

## Volgende stappen

Dit document besprak de mogelijkheden van de pagina met doeldetails. Voor meer informatie over het beheren van bestemmingen in UI, zie het overzicht op [[!UICONTROL Doelen] werkruimte](./destinations-workspace.md).