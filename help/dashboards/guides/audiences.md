---
keywords: Experience Platform;profiel;publiek;publiek;publiek;segmentatie;gebruikersinterface;UI;aanpassing;publieksdashboard;dashboard
title: Handleiding voor publiek dashboard
description: Adobe Experience Platform biedt een dashboard waarmee u belangrijke informatie kunt bekijken over het publiek dat uw organisatie heeft gemaakt.
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: f4f4deda02c96e567cbd0815783f192d1c54096c
workflow-type: tm+mt
source-wordcount: '1969'
ht-degree: 0%

---

# [!UICONTROL Audiences] dashboard {#audiences-dashboard}

De gebruikersinterface van Adobe Experience Platform (UI) verstrekt een dashboard waardoor u belangrijke informatie over uw publiek kunt bekijken, zoals die tijdens een dagelijkse momentopname wordt gevangen. In deze handleiding wordt beschreven hoe u de [!UICONTROL Audiences] dashboard in UI en verstrekt meer informatie over de visualisaties die in het dashboard worden getoond.

Voor een overzicht van alle functies van de Adobe Experience Platform Segmentation Service in de gebruikersinterface van het Platform gaat u naar de [Handleiding voor segmentatieservice](../../segmentation/ui/overview.md).

## [!UICONTROL Audiences] dashboardgegevens

De [!UICONTROL Audiences] Het dashboard toont een momentopname van de attributen (verslag) gegevens die uw organisatie binnen de opslag van het Profiel in Experience Platform heeft. De momentopname bevat geen gebeurtenis (tijdreeks)-gegevens.

De kenmerkgegevens in de momentopname geven de gegevens precies zo weer als op het specifieke tijdstip waarop de momentopname is gemaakt. Met andere woorden, de momentopname is geen benadering of voorbeeld van de gegevens en de [!UICONTROL Audiences] Het dashboard wordt niet in real-time bijgewerkt.

>[!NOTE]
>
>Wijzigingen of updates die zijn aangebracht in de gegevens nadat de momentopname is gemaakt, worden pas in het dashboard weergegeven als de volgende momentopname is gemaakt.

## Ontdek de [!UICONTROL Audiences] dashboard {#explore}

Ga naar de [!UICONTROL Audiences] dashboard in de interface van het Platform, selecteert u **[!UICONTROL Audiences]** in het linkerspoor, dan selecteer **[!UICONTROL Overview]** om het dashboard weer te geven.

>[!NOTE]
>
>Als uw organisatie nieuw aan Platform is en nog niet de actieve datasets van het Profiel of gecreeerd verenigingsbeleid heeft, [!UICONTROL Audiences] het dashboard is niet zichtbaar. In plaats daarvan [!UICONTROL Overview] het lusje toont verbindingen en documentatie om u te helpen met segmentatie beginnen.

![De [!UICONTROL Audiences] dashboard [!UICONTROL Overview] tab met [!UICONTROL Audiences] en [!UICONTROL Overview] gemarkeerd.](../images/audiences/dashboard-overview.png)

### De [!UICONTROL Audiences] dashboard {#modify}

U kunt de weergave van het dialoogvenster [!UICONTROL Audiences] dashboard door **[!UICONTROL Modify dashboard]**. Hierdoor kunt u widgets verplaatsen, toevoegen en verwijderen van het dashboard en toegang krijgen tot de **[!UICONTROL Widget library]** om beschikbare widgets te verkennen en aangepaste widgets voor uw organisatie te maken.

Raadpleeg de [wijzigen, dashboards](../customize/modify.md) en [Overzicht van widgetbibliotheek](../customize/widget-library.md) documentatie voor meer informatie.

### Widgets toevoegen {#add-widget}

Selecteren **[!UICONTROL Add widget]** om naar de widgetbibliotheek te navigeren en een lijst met de beschikbare widgets te bekijken die aan uw dashboard moeten worden toegevoegd.

![De [!UICONTROL Audiences] dashboard-overzicht met [!UICONTROL Add widget] gemarkeerd.](../images/audiences/audiences-overview-add-widget.png)

In de widgetbibliotheek kunt u bladeren door de selectie van standaard- en aangepaste publiekswidgets. Raadpleeg de documentatie bij de widgetbibliotheek voor informatie over het toevoegen van widgets [Een widget toevoegen](../customize/widget-library.md#add-widgets).

## Een publiek selecteren {#select-audience}

Het dashboard selecteert automatisch een publiek om te tonen. U kunt het publiek echter wijzigen met het vervolgkeuzemenu of de publiekskiezer.

Als u een ander publiek wilt kiezen, selecteert u het vervolgkeuzemenu naast de naam van het publiek of opent u het dialoogvenster voor publieksselectie met de kiezer.

>[!IMPORTANT]
>
>Alleen publiek met een profielaantal boven nul wordt weergegeven in de lijst met selecteerbare soorten publiek.

![Het dashboardoverzicht Soorten publiek met het algemene vervolgkeuzemenu voor het publiek gemarkeerd.](../images/audiences/change-audience.png)

![De [!UICONTROL Select audience] een dialoogvenster waarin alle beschikbare soorten publiek worden weergegeven.](../images/audiences/select-audience-dialog.png)

## Widgets en metriek {#widgets-and-metrics}

De [!UICONTROL Audiences] Het dashboard bestaat uit widgets. Dit zijn alleen-lezen metriek die belangrijke informatie over het geselecteerde publiek verschaft.

De datum en tijd van de meest recente momentopname worden getoond bij de bovenkant van [!UICONTROL Overview] naast de publieksvervolgkeuzelijst. Alle widgetgegevens zijn nauwkeurig vanaf die datum en tijd. Het tijdstempel van de momentopname wordt in UTC weergegeven; het bevindt zich niet in de tijdzone van de individuele gebruiker of organisatie.

![Het tabblad Overzicht van soorten publiek met een widgettijdstempel gemarkeerd.](../images/audiences/widget-timestamp.png)

## Standaardwidgets {#standard-widgets}

Adobe biedt meerdere standaardwidgets die u kunt gebruiken voor het visualiseren van verschillende meetgegevens voor uw publiek. U kunt ook aangepaste widgets maken die u met uw organisatie kunt delen met de [!UICONTROL Widget library]. Als u meer wilt weten over het maken van aangepaste widgets, leest u eerst de [Overzicht van widgetbibliotheek](../customize/widget-library.md).

Als u meer wilt weten over elk van de beschikbare standaardwidgets, selecteert u de naam van een widget in de volgende lijst:

* [[!UICONTROL Audience size]](#audience-size)
* [[!UICONTROL Audience activation order]](#audience-activation-order)
* [[!UICONTROL Audience size trend]](#audience-size-trend)
* [[!UICONTROL Audience size change trend]](#audience-size-change-trend)
* [[!UICONTROL Audience size trend by identity]](#audience-size-trend-by-identity)
* [[!UICONTROL Audience overlap]](#audience-overlap)
* [[!UICONTROL Audience overlap report]](#audience-overlap-report)
* [[!UICONTROL Identity overlap]](#identity-overlap)
* [[!UICONTROL Profiles by identity]](#profiles-by-identity)
* [[!UICONTROL Scheduled activations]](#scheduled-activations)

### [!UICONTROL Audience size] {#audience-size}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesize"
>title="Grootte publiek"
>abstract="Deze widget geeft het totale aantal samengevoegde profielen in het geselecteerde publiek weer. Dit getal is afhankelijk van het samenvoegbeleid dat op de gegevens wordt toegepast en is correct op het moment van de meest recente opname."

De **[!UICONTROL Audience size]** widget geeft het totale aantal samengevoegde profielen weer binnen het geselecteerde publiek op het moment dat de opname werd gemaakt. Dit aantal is het resultaat van het toepassen van het beleid van de publiekssamenvoeging op uw gegevens van het Profiel om profielfragmenten samen te voegen en één enkel profiel voor elk individu in het publiek te vormen.

Raadpleeg voor meer informatie over fragmenten en samengevoegde profielen de [Overzicht van het realtime klantprofiel](../../profile/home.md).

![De [!UICONTROL Audiences] dashboard-overzicht met de [!UICONTROL Audience size] widget gemarkeerd.](../images/audiences/audience-size.png)

### [!UICONTROL Audience size trend] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesizetrend"
>title="Ontwikkeling van de omvang van het publiek"
>abstract="Deze widget bevat informatie over het totale aantal profielen dat voldoet aan de criteria van **alle** segmentdefinitie, zoals vastgelegd tijdens de dagelijkse momentopname, gedurende de laatste 30 dagen, 90 dagen, of 12 maanden."

De **[!UICONTROL Audience size trend]** widget geeft een lijngrafiek voor het totale aantal profielen die in aanmerking komen voor **alle** publiek gedurende een bepaalde periode. De trend van de publieksgrootte kan over 30 dagen, 90 dagen, en periodes van 12 maanden worden visualiseerd. De tijdsperiode wordt gekozen in een vervolgkeuzemenu in de widget. De publieksgrootte wordt weerspiegeld op de y-as en de tijd op de x-as.

Deze widget bevat ook de automatische [!UICONTROL Captions] waar een machine het leren model de grafiek en publieksgegevens analyseert en automatisch titels produceert om de belangrijkste tendensen en de belangrijke gebeurtenissen te beschrijven. Selecteren **[!UICONTROL Captions]** om het dialoogvenster voor automatische bijschriften te openen.

![De [!UICONTROL Audiences] In het overzicht ziet u de widget voor de trend om de omvang van de doelgroep te bepalen.](../images/audiences/audience-size-trend-captions.png)

Het dialoogvenster voor automatische bijschriften wordt geopend en verschaft inzicht in uw gegevens.

![Het dialoogvenster voor automatische bijschriften voor de trendwidget voor de doelgrootte.](../images/audiences/audience-size-trend-automatic-captions-dialog.png)

Voor meer informatie over de evaluatie van het publiek en over de vraag hoe profielen in aanmerking komen en van het publiek worden afgesloten, raadpleegt u de [Documentatie voor segmentatieservice](../../segmentation/home.md).

### [!UICONTROL Audience size change trend] {#audience-size-change-trend}

Deze widget geeft een lijngrafiekillustratie van het verschil tussen de meest recente dagelijkse momentopnamen in het totale aantal profielen dat voor een bepaald publiek is gekwalificeerd. Het publiek dat u voor analyse kiest, wordt geselecteerd in het keuzemenu met het overzicht. De periode van trendanalyse kan over 30 dagen, 90 dagen, en periodes van 12 maanden worden visualiseerd. De tijdsperiode wordt gekozen in een vervolgkeuzemenu in de widget. De publieksgrootte wordt weerspiegeld op de y-as en de tijd op de x-as.

![De widget voor het wijzigen van trends bij het bereik van publiek.](../images/audiences/audience-size-change-trend.png)

### [!UICONTROL Audience size trend by identity] {#audience-size-trend-by-identity}

Deze widget illustreert de trend van de publieksgrootte voor een bepaald publiek op basis van het gekozen type identiteit in het vervolgkeuzemenu van de widget. Het publiek dat voor analyse wordt gebruikt wordt geselecteerd van het overzichtsdrop-down. De periode van trendanalyse kan over 30 dagen, 90 dagen, en periodes van 12 maanden worden visualiseerd. De tijdsperiode wordt gekozen in een vervolgkeuzemenu in de widget.

![De trend voor de omvang van de doelgroep op identiteitswidget.](../images/audiences/audience-size-trend-by-identity.png)

### [!UICONTROL Audience activation order] {#audience-activation-order}

De [!UICONTROL Audience activation order] widget verstrekt een drie-kolom lijst die van de bestemmingsnaam, het platform, en de activeringsdatum van het publiek een lijst maakt. De lijst wordt geordend van hoog tot laag afhankelijk van recentie en kan maximaal 10 rijen bevatten.

![De widget voor de activeringsvolgorde van het publiek.](../images/audiences/audience-activation-order.png)

### [!UICONTROL Audience overlap] {#audience-overlap}

Deze widget gebruikt een Venn-diagram om het aantal mensen te visualiseren dat voldoet aan de criteria voor beide soorten publiek. Het publiek dat voor de vergelijking wordt gebruikt, wordt geselecteerd in de widgetdropdown menu&#39;s. Het totale aantal profielen in de desbetreffende segmentdefinitie kan worden gezien door de muis boven een cirkel of het snijpunt van het Venn-diagram te houden.

Met deze widget kunt u uw segmentatiestrategie optimaliseren door de gelijkenissen in de resultaten van uw segmentdefinities te visualiseren.

![De widget publiek overlapt.](../images/audiences/audience-overlap.png)

### [!UICONTROL Audience overlap report] {#audience-overlap-report}

Met deze widget wordt een tabel gemaakt waarin het profiel gegevens voor een bepaald publiek overlapt. Er wordt een lijst met vijf soorten publiek weergegeven, van de hoogste tot de laagste overlappende percentages, die wordt gekozen in het vervolgkeuzemenu boven in het scherm. Voor alle duidelijkheid wordt het gekozen publiek vermeld in het dialoogvenster [!UICONTROL AUDIENCE A NAME] kolom. Er wordt een analyse van de overlappende publiek gegeven voor het tweede publiek dat wordt vermeld in het dialoogvenster [!UICONTROL AUDIENCE B NAME] kolom. De procentuele overlapping wordt vermeld in de derde kolom, tot op twaalf decimalen nauwkeurig.

Het publiek overlapt rapport helpt u om nieuwe, krachtige soorten publiek te bouwen. Wanneer u een hoog percentage van de overlappingen observeert, kunt u het publiek onderdrukken en voorkomen dat hetzelfde publiek naar andere bestemmingen wordt gestuurd. Ze helpen u ook verborgen inzichten te identificeren die kunnen helpen met betere segmentatie. Met een laag percentage overlappingen kunt u unieke profielen zoeken.

Selecteren **[!UICONTROL View more]** om een dialoogvenster op volledig scherm te openen dat meer publiek overlappende gegevens bevat.

![De publiek overlapt rapport widget met View meer benadrukt.](../images/audiences/audience-overlap-report.png)

De [!UICONTROL Audience overlap report] wordt weergegeven. Dit dialoogvenster kan tot 50 rijen publiek bevatten die analyses overlappen die in zes kolommen zijn opgedeeld. Selecteer het instellingenpictogram (![Het instellingenpictogram.](../images/audiences/settings-icon.png)) om kolommen uit de tabel te verwijderen of toe te voegen.

![Het dialoogvenster Publiek overlapt het rapport.](../images/audiences/audience-overlap-report-dialog.png)

>[!NOTE]
>
>Selecteer **[!UICONTROL Overlapping]** kolomkop om de volgorde van de resultaten te wijzigen van het hoogste naar het laagste of het laagste naar het hoogste.

Als u het volledige rapport in de indeling PDF wilt downloaden, selecteert u het optiemenu (**`...`**) gevolgd door **[!UICONTROL Download]**.

![Het publiek overlapt het rapportdialoogvenster met de gemarkeerde ovalen en downloadoptie.](../images/audiences/audience-overlap-report-dialog-download.png)

Selecteer een rij in het rapport om een Venn-diagram van de overlappende analyse te openen. Houd de muisaanwijzer boven een gedeelte van het Venn-diagram om het aantal profielen in een dialoogvenster weer te geven.

![Het publiek overlapt rapportdialoog met een diagram van de Venn en een benadrukte rij.](../images/audiences/audience-overlap-report-dialog-venn.png)

Selecteren **[!UICONTROL Close]** om terug te keren naar de [!UICONTROL Audiences] dashboard.

### [!UICONTROL Identity overlap] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_identityoverlap"
>title="Identiteitsoverlapping"
>abstract="Deze widget toont de overlapping van profielen in uw publiek die beide gekozen identiteiten bevatten. De cirkels geven de relatieve grootte van elke identiteit weer. Het aantal profielen met beide naamruimten wordt weergegeven door de overlapping tussen de cirkels."

De **[!UICONTROL Identity overlap]** widget geeft een Venn-diagram weer of stelt een diagram in waarin de overlapping van profielen in uw publiek met meerdere identiteiten wordt getoond.

Gebruik de vervolgkeuzemenu&#39;s op de widget om de identiteiten te selecteren die u wilt vergelijken. De cirkels geven de relatieve grootte van elke gekozen identiteit weer, waarbij het aantal profielen dat beide naamruimten bevat, wordt weergegeven door de grootte van de overlapping tussen de cirkels.

Als een klant op meer dan één kanaal met uw merk communiceert, zullen de veelvoudige identiteiten met die individuele klant worden geassocieerd. Hierdoor is het waarschijnlijk dat in uw organisatie meerdere profielen met fragmenten van meerdere identiteiten voorkomen.

Ga voor meer informatie over identiteiten naar de [Identiteitsdocumentatie](../../identity-service/home.md).

![De [!UICONTROL Audiences] Overzicht van het dashboard waarbij de widget Identiteitsoverlap gemarkeerd is.](../images/audiences/identity-overlap.png)

### [!UICONTROL Profiles by identity] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_profilesbyidentity"
>title="Profielen op identiteit"
>abstract="Deze widget geeft de indeling van de identiteiten in elk samengevoegd profiel in het geselecteerde publiek weer."

De **[!UICONTROL Profiles by identity]** widget geeft de indeling van de identiteiten in elk samengevoegd profiel in het geselecteerde publiek weer. Het totale aantal profielen per identiteit kan hoger zijn dan het totale aantal profielen in het publiek, omdat aan één profiel meerdere identiteiten kunnen zijn gekoppeld. Met andere woorden, het optellen van de waarden die voor elke identiteit worden getoond kan meer dan de totale publieksgrootte totaal. Dit komt omdat als een klant op meer dan één kanaal met uw merk in wisselwerking staat, veelvoudige identiteiten met die individuele klant kunnen worden geassocieerd.

Selecteren **[!UICONTROL Captions]** om het dialoogvenster voor automatische bijschriften te openen.

![De [!UICONTROL Audiences] Overzicht van het dashboard waarbij de optie Profielen op identiteitswidget en Bijschriften is gemarkeerd.](../images/audiences/profiles-by-identity.png)

Een machine-leermodel produceert automatisch gegevensinzichten door de algemene distributie en belangrijkste dimensies van de gegevens te analyseren.

Ga voor meer informatie over identiteiten naar de [Identiteitsdocumentatie](../../identity-service/home.md).

### Geplande activeringen {#scheduled-activations}

De [!UICONTROL Scheduled activations] widget biedt een tabellarische weergave van de laatst geactiveerde doelen. De tabel bevat het doelplatform, de naam van de activeringsstroom naar dit doel en de begin- en einddatum van de activering voor het geselecteerde publiek. Als er geen einddatum voor de activering is opgegeven, wordt deze weergegeven als [!UICONTROL Ongoing]. Het publiek voor analyse wordt geselecteerd van dropdown bij de bovenkant van de pagina.

Met de widget kunt u in één oogopslag zien waar en wanneer het publiek wordt geactiveerd en kunt u dubbele of overbodige activeringen transparanter maken. Deze geaccumuleerde informatie benadrukt ook waar om het even welke activiteiten zijn weggelaten.

![De widget Geplande activeringen.](../images/audiences/scheduled-activations.png)

## Volgende stappen

Als u dit document volgt, kunt u nu de locatie [!UICONTROL Audiences] dashboard en selecteer het publiek dat u wilt weergeven. U moet ook weten welke maatstaven worden weergegeven in de beschikbare widgets. Als u meer wilt weten over het werken met doelgroepen in de gebruikersinterface van het Experience Platform, raadpleegt u de [Handleiding voor segmentatieservice](../../segmentation/ui/overview.md).
