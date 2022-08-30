---
keywords: Experience Platform;profiel;segment;segmenten;segmentatie;gebruikersinterface;UI;aanpassing;segmentdashboard;dashboard
title: Handleiding dashboard voor segmenten
description: 'Adobe Experience Platform biedt een dashboard waarmee u belangrijke informatie kunt bekijken over segmenten die uw organisatie heeft gemaakt. '
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: 70fb980b276d256e0f7170b6e49527bca59adfe9
workflow-type: tm+mt
source-wordcount: '1594'
ht-degree: 0%

---

# Segmentdashboard {#segment-dashboard}

De gebruikersinterface van Adobe Experience Platform (UI) verstrekt een dashboard waardoor u belangrijke informatie over uw segmenten kunt bekijken, zoals die tijdens een dagelijkse momentopname wordt gevangen. Deze gids schetst hoe te om tot en met het segmentdashboard in UI toegang te hebben en te werken en verstrekt meer informatie betreffende de visualisaties die in het dashboard worden getoond.

Voor een overzicht van alle functies van de Adobe Experience Platform Segmentation Service in de gebruikersinterface van het Platform gaat u naar de [Handleiding voor segmentatieservice](../../segmentation/ui/overview.md).

## Segmentdashboardgegevens

Het segmentdashboard toont een momentopname van de attributen (verslag) gegevens die uw organisatie binnen de opslag van het Profiel in Experience Platform heeft. De momentopname bevat geen gebeurtenis (tijdreeks)-gegevens.

De kenmerkgegevens in de momentopname geven de gegevens precies zo weer als op het specifieke tijdstip waarop de momentopname is gemaakt. Met andere woorden, de momentopname is geen benadering of steekproef van de gegevens, en het segmentdashboard werkt niet in real time bij.

>[!NOTE]
>
>Wijzigingen of updates die zijn aangebracht in de gegevens nadat de momentopname is gemaakt, worden pas in het dashboard weergegeven als de volgende momentopname is gemaakt.

## Het segmentdashboard verkennen

Ga naar de [!UICONTROL Segments] dashboard in de interface van het Platform, selecteert u **[!UICONTROL Segments]** in het linkerspoor, dan selecteer **[!UICONTROL Overview]** om het dashboard weer te geven.

>[!NOTE]
>
>Als uw organisatie nieuw aan Platform is en nog niet de actieve datasets van het Profiel of gecreeerd verenigingsbeleid heeft, [!UICONTROL Segments] het dashboard is niet zichtbaar. In plaats daarvan [!UICONTROL Overview] het lusje toont verbindingen en documentatie om u te helpen met segmentatie beginnen.

![](../images/segments/dashboard-overview.png)

### Het wijzigen van [!UICONTROL Segments] dashboard

U kunt de weergave van het dialoogvenster [!UICONTROL Segments] dashboard door **[!UICONTROL Modify dashboard]**. Hierdoor kunt u widgets verplaatsen, toevoegen en verwijderen van het dashboard en toegang krijgen tot de **[!UICONTROL Widget library]** om beschikbare widgets te verkennen en aangepaste widgets voor uw organisatie te maken.

Raadpleeg de [wijzigen, dashboards](../customize/modify.md) en [Overzicht van widgetbibliotheek](../customize/widget-library.md) documentatie voor meer informatie.

## Een segment selecteren

Het dashboard selecteert automatisch een segment aan vertoning, nochtans kunt u het segment veranderen door het dropdown menu of de segmentselecteur te gebruiken.

Als u een ander segment wilt kiezen, selecteert u de vervolgkeuzelijst naast de segmentnaam of gebruikt u de segmentkiezer om het dialoogvenster voor segmentselectie te openen.

>[!IMPORTANT]
>
>Alleen segmenten met een profielaantal groter dan nul worden weergegeven in de lijst met selecteerbare segmenten.

![](../images/segments/change-segment.png)

![](../images/segments/select-segment-dialog.png)

## Widgets en metriek

Het segmentdashboard bestaat uit widgets. Dit zijn alleen-lezen metriek die belangrijke informatie over het geselecteerde segment verschaft.

De datum en tijd van de meest recente momentopname worden getoond bij de bovenkant van [!UICONTROL Overview] naast de segmentvervolgkeuzelijst. Alle widgetgegevens zijn nauwkeurig vanaf die datum en tijd. Het tijdstempel van de momentopname wordt in UTC weergegeven; het bevindt zich niet in de tijdzone van de individuele gebruiker of organisatie.

![Het tabblad Overzicht van segmenten met een widgettijdstempel gemarkeerd.](../images/segments/widget-timestamp.png)

## Standaardwidgets {#standard-widgets}

Adobe biedt meerdere standaardwidgets die u kunt gebruiken voor het visualiseren van verschillende maateenheden voor uw segmenten. U kunt ook aangepaste widgets maken die u met uw organisatie kunt delen met de [!UICONTROL Widget library]. Als u meer wilt weten over het maken van aangepaste widgets, leest u eerst de [Overzicht van widgetbibliotheek](../customize/widget-library.md).

Als u meer wilt weten over elk van de beschikbare standaardwidgets, selecteert u de naam van een widget in de volgende lijst:

* [[!UICONTROL Audience size]](#audience-size)
* [[!UICONTROL Audience activation order]](#audience-activation-order)
* [[!UICONTROL Audience size trend]](#audience-size-trend)
* [[!UICONTROL Audience size change trend]](#audience-size-change-trend)
* [[!UICONTROL Audience size trend by identity]](#audience-size-trend-by-identity)
* [[!UICONTROL Audience overlap]](#audience-overlap)
* [[!UICONTROL Identity overlap]](#identity-overlap)
* [[!UICONTROL Profiles by identity]](#profiles-by-identity)
* [[!UICONTROL Scheduled activations]](#scheduled-activations)

### [!UICONTROL Audience size] {#audience-size}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesize"
>title="Grootte publiek"
>abstract="Deze widget geeft het totale aantal samengevoegde profielen in het geselecteerde segment weer. Dit getal is afhankelijk van het samenvoegbeleid dat op de gegevens wordt toegepast en is correct op het moment van de meest recente opname."

De **[!UICONTROL Audience size]** widget geeft het totale aantal samengevoegde profielen weer binnen het geselecteerde segment op het moment dat de opname werd gemaakt. Dit getal is het resultaat van het toepassen van het samenvoegbeleid voor segmenten op de profielgegevens om profielfragmenten samen te voegen tot één profiel voor elke persoon in het segment.

Voor meer informatie over fragmenten en samengevoegde profielen, eerst leest u de [Overzicht van het realtime klantprofiel](../../profile/home.md).

![](../images/segments/audience-size.png)

### [!UICONTROL Audience size trend] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesizetrend"
>title="Ontwikkeling van de omvang van het publiek"
>abstract="Deze widget bevat informatie over het totale aantal profielen dat voldoet aan de criteria van **alle** segmentdefinitie, zoals vastgelegd tijdens de dagelijkse momentopname, gedurende de laatste 30 dagen, 90 dagen, of 12 maanden."

De **[!UICONTROL Audience size trend]** widget geeft een lijngrafiek voor het totale aantal profielen die voldoen aan de criteria van **alle** segmentdefinitie over een bepaalde periode. De trend van de publieksgrootte kan over 30 dagen, 90 dagen, en periodes van 12 maanden worden visualiseerd. De tijdsperiode wordt gekozen in een vervolgkeuzemenu in de widget. De publieksgrootte wordt weerspiegeld op de y-as en de tijd op de x-as.

Deze widget bevat ook de automatische [!UICONTROL Captions] waar een machine het leren model de grafiek en segmentgegevens analyseert en automatisch titels produceert om de belangrijkste tendensen en de belangrijke gebeurtenissen te beschrijven. Selecteren **[!UICONTROL Captions]** om het dialoogvenster voor automatische bijschriften te openen.

![In het segmentoverzicht wordt de widget voor de doelgrootte weergegeven.](../images/segments/audience-size-trend-captions.png)

Het dialoogvenster voor automatische bijschriften wordt geopend en verschaft inzicht in uw gegevens.

![Het dialoogvenster voor automatische bijschriften voor de trendwidget voor de doelgrootte.](../images/segments/audience-size-trend-automatic-captions-dialog.png)

Voor meer informatie over segmentevaluatie en hoe profielen in aanmerking komen en uit segmenten verdwijnen, raadpleegt u de [Documentatie voor segmentatieservice](../../segmentation/home.md).

### [!UICONTROL Audience size change trend] {#audience-size-change-trend}

Deze widget geeft een lijngrafiekillustratie van het verschil in het totale aantal profielen dat voor een bepaald segment in aanmerking kwam tussen de meest recente dagelijkse momentopnamen. Het voor analyse gekozen segment wordt geselecteerd uit het overzichtsvervolgkeuzemenu. De periode van trendanalyse kan over 30 dagen, 90 dagen, en periodes van 12 maanden worden visualiseerd. De tijdsperiode wordt gekozen in een vervolgkeuzemenu in de widget. De publieksgrootte wordt weerspiegeld op de y-as en de tijd op de x-as.

![De widget voor het wijzigen van trends bij het bereik van publiek.](../images/segments/audience-size-change-trend.png)

### [!UICONTROL Audience size trend by identity] {#audience-size-trend-by-identity}

Deze widget illustreert de trend van de publieksgrootte voor een bepaald segment op basis van het gekozen type identiteit in het vervolgkeuzemenu van de widget. Het segment dat voor analyse wordt gebruikt wordt geselecteerd van het overzichtsdrop-down. De periode van trendanalyse kan over 30 dagen, 90 dagen, en periodes van 12 maanden worden visualiseerd. De tijdsperiode wordt gekozen in een vervolgkeuzemenu in de widget.

![De trend voor de omvang van de doelgroep op identiteitswidget.](../images/segments/audience-size-trend-by-identity.png)

### [!UICONTROL Audience activation order] {#audience-activation-order}

De [!UICONTROL Audience activation order] widget biedt een tabel met drie kolommen waarin de [!UICONTROL destination name]de [!UICONTROL platform]en de activering [!UICONTROL date] van het publiek. De lijst wordt geordend van hoog tot laag afhankelijk van recentie en kan maximaal 10 rijen bevatten.

![De widget voor de activeringsvolgorde van het publiek.](../images/segments/audience-activation-order.png)

### [!UICONTROL Audience overlap] {#audience-overlap}

Deze widget vertegenwoordigt het aantal profielen van twee segmenten die aan de criteria voor beide segmentdefinities voldoen. De segmenten die voor vergelijking worden gebruikt, worden geselecteerd in de widgetdropdown menu&#39;s. Het totale aantal profielen in de desbetreffende segmentdefinitie kan worden gezien door de muis boven een cirkel of het snijpunt van het Venn-diagram te houden.

Met deze widget kunt u uw segmentatiestrategie optimaliseren door de gelijkenissen in de resultaten van uw segmentdefinities te visualiseren.

![De widget publiek overlapt.](../images/segments/audience-overlap.png)

<!-- * [[!UICONTROL Audience overlap report]](#audience-overlap-report) -->
<!-- ### [!UICONTROL Audience overlap report] {#audience-overlap-report} -->

<!-- View an ordered list of audiences by Highest or Lowest overlap percentages. -->

<!-- ![The Audience overlap report widget.]() -->

<!-- https://jira.corp.adobe.com/browse/PLAT-125511 -->

### [!UICONTROL Identity overlap] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_identityoverlap"
>title="Identiteitsoverlapping"
>abstract="Deze widget toont de overlapping van profielen in uw segment met beide gekozen identiteiten. De cirkels geven de relatieve grootte van elke identiteit weer. Het aantal profielen met beide naamruimten wordt weergegeven door de overlapping tussen de cirkels."

De **[!UICONTROL Identity overlap]** widget geeft een Venn-diagram weer of stelt een diagram in waarin de overlapping van profielen in uw segment met meerdere identiteiten wordt weergegeven.

Gebruik de vervolgkeuzemenu&#39;s op de widget om de identiteiten te selecteren die u wilt vergelijken. De cirkels geven de relatieve grootte van elke gekozen identiteit weer, waarbij het aantal profielen dat beide naamruimten bevat, wordt weergegeven door de grootte van de overlapping tussen de cirkels.

Als een klant op meer dan één kanaal met uw merk in wisselwerking staat, zullen de veelvoudige identiteiten met die individuele klant worden geassocieerd, daarom is het waarschijnlijk dat uw organisatie veelvoudige profielen zal hebben die fragmenten van meer dan één identiteit bevatten.

Ga voor meer informatie over identiteiten naar de [Documentatie bij Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/segments/identity-overlap.png)

### [!UICONTROL Profiles by identity] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_profilesbyidentity"
>title="Profielen op identiteit"
>abstract="Deze widget geeft de indeling van de identiteiten in elk samengevoegd profiel in het geselecteerde segment weer."

De **[!UICONTROL Profiles by identity]** widget geeft de indeling van de identiteiten in elk samengevoegd profiel in het geselecteerde segment weer. Het totale aantal profielen per identiteit kan hoger zijn dan het totale aantal profielen in het segment, omdat aan één profiel meerdere identiteiten kunnen zijn gekoppeld. Met andere woorden, het samenvoegen van de waarden die voor elke identiteit worden getoond kan meer dan de totale publieksgrootte in het segment totaal omdat als een klant met uw merk op meer dan één kanaal interactie aangaat, de veelvoudige identiteiten met die individuele klant kunnen worden geassocieerd.

Selecteren **[!UICONTROL Captions]** om het dialoogvenster voor automatische bijschriften te openen.

![De profielen op dialoogvenster voor identiteitsondertitels.](../images/segments/profiles-by-identity.png)

Een machine-leermodel produceert automatisch gegevensinzichten door de algemene distributie en belangrijkste dimensies van de gegevens te analyseren.

Ga voor meer informatie over identiteiten naar de [Documentatie bij Adobe Experience Platform Identity Service](../../identity-service/home.md).

### Geplande activeringen {#scheduled-activations}

De [!UICONTROL Scheduled activations] widget biedt een tabellarische weergave van de laatst geactiveerde doelen. De tabel bevat het doelplatform, de naam van de activeringsstroom naar dit doel en de begin- en einddatum van de activering voor het geselecteerde segment. Als er geen einddatum voor de activering is opgegeven, wordt deze weergegeven als [!UICONTROL Ongoing]. Het segment voor analyse wordt geselecteerd van dropdown bij de bovenkant van de pagina.

Met de widget kunt u in één oogopslag zien waar en wanneer het publiek wordt geactiveerd en kunt u dubbele of overbodige activeringen transparanter maken. Deze geaccumuleerde informatie benadrukt ook waar om het even welke activiteiten zijn weggelaten.

![De widget Geplande activeringen.](../images/segments/scheduled-activations.png)

## Volgende stappen

Door dit document te volgen, zou u van het segmentdashboard moeten kunnen de plaats bepalen en een segment selecteren om te bekijken. U moet ook weten welke maatstaven worden weergegeven in de beschikbare widgets. Als u meer wilt weten over het werken met segmenten in de gebruikersinterface van het Experience Platform, raadpleegt u de [Handleiding voor segmentatieservice](../../segmentation/ui/overview.md).
