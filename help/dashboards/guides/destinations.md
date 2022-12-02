---
keywords: Experience Platform;profiel;real-time klantprofiel;gebruikersinterface;UI;aanpassing;profiel dashboard;dashboard
title: Doeldashboardgids
description: Adobe Experience Platform biedt een dashboard waarmee u belangrijke informatie over de actieve doelen van uw organisatie kunt bekijken.
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: d9e10271db52f61cdc3e4adc546fe05adadb5a46
workflow-type: tm+mt
source-wordcount: '2852'
ht-degree: 0%

---

# [!UICONTROL Destinations] dashboard

De gebruikersinterface van Adobe Experience Platform (UI) verstrekt een dashboard waardoor u belangrijke informatie over de actieve bestemmingen van uw organisatie kunt bekijken, zoals die tijdens een dagelijkse momentopname wordt gevangen. Deze gids schetst hoe te om tot het dashboard van bestemmingen in UI toegang te hebben en te werken en verstrekt meer informatie betreffende de metriek die in het dashboard wordt getoond.

Voor een overzicht van de bestemmingen en een lijst van alle beschikbare bestemmingen in Experience Platform, gelieve te bezoeken [documentatie voor doelen](../../destinations/home.md).

## [!UICONTROL Destinations] dashboardgegevens {#destinations-dashboard-data}

Het dashboard van Doelen toont een momentopname van de bestemmingen die uw organisatie binnen Experience Platform heeft toegelaten. De gegevens in de momentopname geven de gegevens precies zo weer als op het specifieke tijdstip waarop de momentopname is gemaakt. Met andere woorden, de momentopname is geen benadering of steekproef van de gegevens, en het dashboard van bestemmingen werkt niet in real time bij.

>[!NOTE]
>
>Wijzigingen of updates die zijn aangebracht in de gegevens nadat de momentopname is gemaakt, worden pas in het dashboard weergegeven als de volgende momentopname is gemaakt.

## Ontdek de [!UICONTROL Destinations] dashboard {#explore}

Als u naar het dashboard voor doelen wilt navigeren binnen de interface van het Platform, selecteert u **[!UICONTROL Destinations]** in het linkerspoor, dan selecteer **[!UICONTROL Overview]** om het dashboard weer te geven.

De datum en tijd van de meest recente momentopname worden getoond bij de bovenkant van [!UICONTROL Overview] naast het vervolgkeuzemenu van het doel. Alle widgetgegevens zijn nauwkeurig vanaf die datum en tijd. Het tijdstempel van de momentopname wordt in UTC weergegeven; het bevindt zich niet in de tijdzone van de individuele gebruiker of organisatie.

>[!NOTE]
>
>Als uw organisatie nieuw aan Experience Platform is en nog geen actieve bestemmingen heeft, dashboard van Doelen en [!UICONTROL Overview] zijn niet zichtbaar. In plaats daarvan selecteert u [!UICONTROL Destinations] van de linkernavigatie toont de [!UICONTROL Catalog] tab. Meer informatie over de [!UICONTROL Catalog] tabblad, verwijst naar de [[!UICONTROL Destinations] werkruimtegids](../../destinations/ui/destinations-workspace.md).

![Het overzicht van de Doelen UI van het Platform met de meest recente benadrukte momentopname.](../images/destinations/snapshot-timestamp.png)

### De [!UICONTROL Destinations] dashboard {#modify}

Selecteren **[!UICONTROL Modify dashboard]** om de verschijning van het dashboard van bestemmingen te veranderen. Hierdoor kunt u widgets verplaatsen, toevoegen en verwijderen van het dashboard en toegang krijgen tot de widgetbibliotheek. In de widgetbibliotheek kunt u de beschikbare widgets verkennen en aangepaste widgets maken voor uw organisatie.

Raadpleeg de [wijzigen, dashboards](../customize/modify.md) en [Overzicht van widgetbibliotheek](../customize/widget-library.md) documentatie voor meer informatie.

### Widgets toevoegen {#add-widget}

Selecteren **[!UICONTROL Add widget]** om naar de widgetbibliotheek te navigeren en een lijst met de beschikbare widgets te bekijken die aan uw dashboard moeten worden toegevoegd.

![Het dashboardoverzicht Doelen met de markering Widget toevoegen.](../images/destinations/destinations-overview-add-widget.png)

In de widgetbibliotheek kunt u bladeren door de selectie van standaard- en aangepaste segmenuwidgets. Raadpleeg de documentatie bij de widgetbibliotheek voor informatie over het toevoegen van widgets [Een widget toevoegen](../customize/widget-library.md#add-widgets).

## Standaardwidgets {#standard-widgets}

Adobe verstrekt veelvoudige standaardwidgets die u kunt gebruiken om verschillende metriek met betrekking tot uw bestemmingen te visualiseren en de volledigheid van de segmenten beschikbaar voor uw gegevensanalyse te beoordelen. U kunt ook aangepaste widgets maken die u met uw organisatie kunt delen met de [!UICONTROL Widget library]. Als u meer wilt weten over het maken van aangepaste widgets, leest u eerst de [Overzicht van widgetbibliotheek](../customize/widget-library.md).

### Vereisten {#prerequisites}

Voordat u doorgaat met de beschrijvingen van standaardwidgets, moet u de definities van de volgende belangrijke termen die in de documentatie worden gebruikt, goed kennen:

* **Segment:** Een segment is **het geheel van regels** die kenmerken en gebeurtenisgegevens bevatten die een aantal profielen als een publiek kwalificeren.
* **Publiek**: Een publiek is **de reeks profielen** die voldoen aan de criteria van een segmentdefinitie.
* **Toegewezen/toewijzen**: Gegevenstoewijzing is het proces waarbij brongegevensvelden worden toegewezen aan verwante doelvelden in een doel.
* **Identiteit**: Een identiteit is een id die uniek een individuele klant vertegenwoordigt, zoals een cookie-id, apparaat-id of e-mailadres.
* **Activeren**: Activate is de actie die door een gebruiker wordt ondernomen om een segment of profielen aan een bestemming zoals Oracle Eloqua, Google, of Marketing Cloud Salesforce in kaart te brengen.

Als u meer wilt weten over elk van de beschikbare standaardwidgets, selecteert u de naam van een widget in de volgende lijst:

* [[!UICONTROL Most used destinations]](#most-used-destinations)
* [[!UICONTROL Recently created destinations]](#recently-created-destinations)
* [[!UICONTROL Recently activated segments]](#recently-activated-segments)
* [[!UICONTROL Recently activated segments by destination]](#recently-activated-segments-by-destination)
* [[!UICONTROL Audience size trend]](#audience-size-trend)
* [[!UICONTROL Unmapped segments by identity]](#unmapped-segments-by-identity)
* [[!UICONTROL Mapped segments by identity]](#mapped-segments-by-identity)
* [[!UICONTROL Common audiences]](#common-audiences)
* [[!UICONTROL Mapped audiences]](#mapped-audiences)
* [[!UICONTROL Mapped audience health]](#mapped-audience-health)
* [[!UICONTROL Destinations count]](#destinations-count)
* [[!UICONTROL Destination status]](#destination-status)
* [[!UICONTROL Active destinations by destination platform]](#active-destinations-by-destination-platform)
* [[!UICONTROL Activated audiences across all destinations]](#activated-audiences-across-all-destinations)
* [[!UICONTROL Activated audiences]](#activated-audiences)

### [!UICONTROL Most used destinations] {#most-used-destinations}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mostuseddestinations"
>title="Meest gebruikte bestemmingen"
>abstract="Deze widget geeft de meest actieve doelen van uw organisatie weer op basis van het aantal in kaart gebrachte segmenten. Deze getallen zijn nauwkeurig op het moment van de laatste opname. Deze rangschikking biedt inzicht in welke bestemmingen momenteel het meest worden gebruikt en markeert de doelen die mogelijk onderbenut zijn."

De **[!UICONTROL Most used destinations]** widget geeft de belangrijkste doelen van uw organisatie weer op basis van het aantal segmenten dat is toegewezen, vanaf de laatste momentopname. Deze rangschikking biedt inzicht in welke bestemmingen worden gebruikt en toont mogelijk ook de bestemmingen die mogelijk onderbenut zijn.

Bijvoorbeeld, als u een bestemming gisteren vormde maar geen segmenten aan het in kaart gebracht, zou u kunnen zien dat de bestemming momenteel onderbenut is.

Het aantal in kaart gebrachte segmenten die in de kolom van de segmenttelling worden getoond is nauwkeurig vanaf de laatste dagelijkse momentopname. Als u een nieuw segment toewijst aan de bestemming, wordt de telling pas bijgewerkt wanneer de volgende momentopname wordt gemaakt.

Als u de naam van een doel selecteert in de lijst die wordt weergegeven op de widget, gaat u naar de doeldetails die zijn gekoppeld vanuit het menu **[!UICONTROL Browse]** tab. U kunt ook **[!UICONTROL View All]** om naar de **[!UICONTROL Browse]** en selecteert u vervolgens de naam van een bestemming om de details ervan weer te geven.

![Het tabblad Overzicht van het dashboard Doelen met de meest gebruikte doelwidget gemarkeerd.](../images/destinations/most-used-destinations.png)

### [!UICONTROL Recently created destinations] {#recently-created-destinations}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlycreateddestinations"
>title="Onlangs gemaakte doelen"
>abstract="Deze widget geeft een lijst weer met de laatst geconfigureerde doelen binnen uw organisatie."

De **[!UICONTROL Recently created destinations]** widget laat u toe om een lijst van onlangs gevormde bestemmingen van uw organisatie te zien.

De gecreeerde getoonde datum is nauwkeurig aan de laatste dagelijkse momentopname. Met andere woorden, als u een nieuwe bestemming creeert, zal het niet in de lijst verschijnen tot nadat de volgende momentopname wordt genomen.

Als u de naam van een doel selecteert in de lijst die wordt weergegeven op de widget, gaat u naar de doeldetails die zijn gekoppeld vanuit het menu **[!UICONTROL Browse]** tab. U kunt ook **[!UICONTROL View All]** om naar de **[!UICONTROL Browse]** en selecteert u vervolgens de naam van een bestemming om de details ervan weer te geven.

Om meer over te leren hoe te om specifieke soorten bestemmingen te vormen, bezoek [documentatie voor doelen](../../destinations/home.md).

![Het tabblad Overzicht van het dashboard Doelen met de onlangs gemaakte widget voor doelen gemarkeerd.](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Recently activated segments] {#recently-activated-segments}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlyactivatedsegments"
>title="Onlangs geactiveerde segmenten"
>abstract="Deze widget bevat een lijst met de segmenten die het laatst zijn toegewezen aan een doel. Deze lijst verstrekt een momentopname van de segmenten en de bestemmingen die actief in gebruik in het systeem zijn en in het oplossen van problemen kunnen helpen om het even welke onjuiste afbeeldingen."

De **[!UICONTROL Recently activated segments]** widget bevat een lijst met de segmenten die het laatst zijn toegewezen aan een doel. Deze lijst verstrekt een momentopname van de segmenten en de bestemmingen die actief in gebruik in het systeem zijn en in het oplossen van problemen kunnen helpen om het even welke onjuiste afbeeldingen.

De bijgewerkte getoonde datum toont de laatste tijd het segment aan de bestemming werd geactiveerd en aan de laatste dagelijkse momentopname nauwkeurig is. Met andere woorden, als u een segment aan de bestemming activeert, zal de bijgewerkte datum niet veranderen tot na de volgende momentopname wordt genomen.

Als u de naam van een segment selecteert in de lijst die wordt weergegeven op de widget, gaat u naar de segmentdetails. U kunt ook **[!UICONTROL View All]** om aan het segment te navigeren doorbladert lusje en selecteert dan de naam van een segment om zijn details te bekijken.

Raadpleeg voor meer informatie over het werken met segmenten in Experience Platform de [Overzicht van segmentatieservice](../../segmentation/home.md).

![Het tabblad Overzicht van het dashboard Doelen met de widget Onlangs geactiveerde segmenten gemarkeerd.](../images/destinations/recently-activated-segments.png)

### [!UICONTROL Recently activated segments by destination] {#recently-activated-segments-by-destination}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlyactivatedsegmentsbydestination"
>title="Onlangs geactiveerde segmenten op doel"
>abstract="Met deze widget worden de bovenste vijf laatst geactiveerde segmenten in aflopende volgorde weergegeven, afhankelijk van het doel dat u hebt gekozen in de overzichtsvervolgkeuzelijst."

De **[!UICONTROL Recently activated segments by destination]** widget geeft de bovenste vijf laatst geactiveerde segmenten in aflopende volgorde weer, afhankelijk van het doel dat u hebt gekozen in de overzichtsvervolgkeuzelijst. Het lijkt op het [!UICONTROL Recently activated segments] widget, maar de gegevens worden weergegeven **alleen** wordt toegepast op het geselecteerde doel.

Deze widget bevat twee metriek: de segmentnaam en de datum dat het segment het laatst aan de bestemming werd geactiveerd. De weergegeven gegevens zijn correct vanaf de laatste dagelijkse momentopname.

U kunt de details van een segment bekijken door de naam van een segment van de getoonde lijst te selecteren.

![De onlangs geactiveerde segmenten op bestemmingswidget.](../images/destinations/recently-activated-segments-by-destination.png)

Zie de sectie met voorwaarden voor de [definities van gebruikte termen](#prerequisites) in deze beschrijving.

### [!UICONTROL Audience size trend] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_audiencesizetrend"
>title="Ontwikkeling van de omvang van het publiek"
>abstract="Deze widget illustreert het aantal profielen in het segment, dat dagelijks naar de bestemmingsrekening wordt verzonden. In het eerste vervolgkeuzemenu wordt de tijdsperiode voor de trend voor het publiek aangepast. Het tweede widgetdropdown menu selecteert het segment voor analyse. Het doel wordt gekozen uit de overzichtsvervolgkeuzelijst."

De **[!UICONTROL Audience size trend]** widget geeft de relatie weer van de profieltelling over een tijdsperiode voor een segment dat is toegewezen aan die doelaccount. De widget gebruikt een lijngrafiek om het aantal profielen in het segment te illustreren, die dagelijks naar de bestemmingsrekening worden verzonden.

Een tijdsperiode voor de publiekstrend over de afgelopen 30 dagen, 90 dagen, of 12 maanden, kan worden aangepast gebruikend het eerste drop-down menu.

Het tweede vervolgkeuzemenu bevat alle beschikbare segmenten die naar de doelaccount kunnen worden verzonden die boven aan het dashboard is gekozen.

![De widget voor de doelgrootte.](../images/destinations/audience-size-trend.png)

De **[!UICONTROL Audience size trend]** widget biedt een [!UICONTROL Captions] in de rechterbovenhoek van de widget. Selecteren **[!UICONTROL Captions]** om het dialoogvenster voor automatische bijschriften te openen. Een machine het leren model produceert automatisch titels om de belangrijkste tendensen en de belangrijke gebeurtenissen te beschrijven door de grafiek en de segmentgegevens te analyseren.

![Het dialoogvenster voor automatische bijschriften voor de trendwidget voor de doelgrootte.](../images/destinations/audience-size-trend-captions.png)

### [!UICONTROL Unmapped segments by identity] {#unmapped-segments-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_unmappedsegmentsbyidentity"
>title="Niet-toegewezen segmenten op identiteit"
>abstract="Deze widget bevat de bovenste vijf **ongestructureerd** segmenten gerangschikt op basis van het afnemende aantal identiteiten voor een bepaald doel en een bepaalde identiteit. De filter-id&#39;s die in het vervolgkeuzemenu van de widget worden weergegeven, veranderen afhankelijk van de doelaccount die boven aan de overzichtspagina is geselecteerd."

De **[!UICONTROL Unmapped segments by identity]** widget geeft de bovenste vijf weer **ongestructureerd** segmenten gerangschikt op basis van het afnemende aantal identiteiten voor een bepaald doel en een bepaalde identiteit. Het benadrukt segmenten die het meest voordelig zijn om aan de gekozen bestemmingsrekening in kaart te brengen die op gekozen identiteitskaart wordt gebaseerd.

Het vervolgkeuzemenu voor de doel-id filtert de beschikbare segmenten. De filter-id&#39;s in de vervolgkeuzelijst veranderen, afhankelijk van de doelaccount die boven aan de overzichtspagina is geselecteerd.

In de kolom met identiteiten wordt het aantal bron-id&#39;s in het segment geteld dat kan worden toegewezen aan de id die is gekozen in het vervolgkeuzemenu van de widget-id.

![De segmenten zonder toewijzing op de identiteitswidget.](../images/destinations/unmapped-segments-by-identity.png)

Zie de sectie met voorwaarden voor de [definities van gebruikte termen](#prerequisites) in deze beschrijving.

### [!UICONTROL Mapped segments by identity] {#mapped-segments-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mappedsegmentsbyidentity"
>title="Toegewezen segmenten op identiteit"
>abstract="Deze widget biedt een bovenste lijst van vijf **toegewezen** segmenten. De lijst wordt bevolen van hoog aan laag volgens het aantal bron IDs bevat binnen de segmenten. De doel-id die moet worden geteld, wordt geselecteerd in het vervolgkeuzemenu onder de titel van de widget. De doel-id&#39;s die beschikbaar zijn in de keuzelijst met widgets zijn afhankelijk van de bestemming die boven aan het overzichtsdashboard is gekozen."

Deze widget biedt een bovenste lijst van vijf **toegewezen** segmenten. De lijst wordt bevolen van hoog aan laag volgens het aantal bron IDs bevat binnen de segmenten. De doel-id die moet worden geteld, wordt geselecteerd in het vervolgkeuzemenu onder de titel van de widget. De doel-id&#39;s die beschikbaar zijn in de vervolgkeuzelijst in de widget, worden gewijzigd op basis van het doelaccountfilter dat boven aan het overzichtsdashboard is gekozen.

![De toegewezen segmenten op identiteitswidget.](../images/destinations/mapped-segments-by-identity.png)

De **[!UICONTROL Mapped segments by identity]** in één oogopslag wordt de nadruk gelegd op de waarschijnlijkheid om profielkansen voor een campagne binnen de gekozen bestemming met succes te richten . Een efficiënte gerichte campagne is niet afhankelijk van het aantal profielen dat naar de bestemming wordt verzonden, maar van het aantal bron-id&#39;s dat waarschijnlijk met de doel-id&#39;s wordt aangepast om nuttige en uitvoerbare gegevens te verschaffen.

### Algemeen publiek {#common-audiences}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_commonaudiences"
>title="Algemeen publiek"
>abstract="Deze widget bevat een lijst met de bovenste vijf segmenten die zijn geactiveerd voor de doelaccount die boven aan de pagina is gekozen, en het doel dat is geselecteerd in het vervolgkeuzemenu van de widget. De lijst met segmenten wordt geordend op basis van hoe recent ze zijn geactiveerd. Het laatst geactiveerde segment wordt bovenaan weergegeven."

De **[!UICONTROL Common audiences]** widget bevat een lijst met de bovenste vijf segmenten die worden geactiveerd over de doelaccount die boven aan de pagina is gekozen, en het doel dat is geselecteerd in de widgetvervolgkeuzelijst. De lijst met segmenten wordt geordend op basis van hoe recent ze zijn geactiveerd. Het laatst geactiveerde segment wordt bovenaan weergegeven.

De [!UICONTROL AUDIENCE SIZE] de kolom verstrekt het totale profielaantal van elk vermeld segment.

![De widget Algemeen publiek.](../images/destinations/common-audiences.png)

### Toegewezen publiek {#mapped-audiences}

De [!UICONTROL Mapped audiences] widget geeft het totale aantal toegewezen doelgroepen weer dat kan worden geactiveerd voor het doel dat boven aan de pagina is geselecteerd.

Selecteren **[!UICONTROL Segments]** om naar het dashboard Segmenten te navigeren [!UICONTROL Browse] tab. Deze werkruimte toont een lijst van alle segmentdefinities voor uw organisatie.

![De widget voor toegewezen doelgroepen.](../images/destinations/mapped-audiences.png)

### Gewijzigde gezondheid van het publiek {#mapped-audience-health}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mappedaudiencehealth"
>title="Gewijzigde gezondheid van het publiek"
>abstract="Deze widget biedt een lijst met maximaal 20 toegewezen segmenten waarvan het totale aantal profielen afwijkt met een factor van ten minste één standaardafwijking van de gemiddelde 30 dagen-publieksgrootte die aan die bestemming is toegewezen. Het verstrekt een berekende metrisch voor de spreiding van publieksgrootte van het gemiddelde over de laatste 30 dagen. De grootten van de doelgroep worden gesorteerd van hoog naar laag."

De widget biedt een lijst met maximaal 20 in kaart gebrachte segmenten waarvan het totale aantal profielen, vanaf de laatste dagelijkse momentopname, met een factor van minstens één standaardafwijking afwijkt van de gemiddelde 30 dagen-publieksgrootte die aan die bestemming is toegewezen.

Kortom, het biedt een berekende maatstaf voor de spreiding van de publieksformaten ten opzichte van het gemiddelde over de afgelopen 30 dagen. Het vergelijkt of de omvang van het publiek van vandaag buiten de historische standaardafwijking valt die in de afgelopen 30 dagen in de gegevens werd gezien.

Alle publieksgrootten in het systeem worden gesorteerd van hoge naar lage publieksgrootte, zoals aangegeven in het dialoogvenster [!UICONTROL LATEST SIZE] kolom.

Als het aantal aan een segment toegewezen profielen de afgelopen 30 dagen buiten één standaardafwijking van de gemiddelde toegewezen profielgrootte ligt, wijst dit op een anomalie in het systeem en het zou moeten worden onderzocht.

Als een segment binnen de [!UICONTROL Mapped audience health] widget wijkt met een ruime marge af, moet u naar het trenddiagram voor de doelgrootte verwijzen en het afwijkende segment zoeken. De trend kan meer inzicht in de gezondheid van uw segment verstrekken.

>[!NOTE]
>
>De standaardgrootte van de widget voor de volksgezondheid toewijzen kan de tabelinformatie belemmeren. Wijzig de grootte van de widget om de leesbaarheid van de omgezette segmentnamen en kolomtitels te verbeteren. Raadpleeg de documentatie bij het wijzigen van dashboards voor hulp bij [hoe u de grootte van een widget wijzigt](../customize/modify.md).

![De widget gezondheid voor het toegewezen publiek.](../images/destinations/mapped-audience-health.png)

### [!UICONTROL Destinations count] {#destinations-count}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_destinationscount"
>title="Aantal doelen"
>abstract="Deze widget geeft het totale aantal beschikbare eindpunten weer waarop een publiek kan worden geactiveerd en geleverd binnen het systeem. Dit aantal omvat zowel actieve als inactieve bestemmingen."

De [!UICONTROL Destinations count] widget geeft het totale aantal beschikbare eindpunten weer waarop een publiek kan worden geactiveerd en geleverd binnen het systeem. Dit aantal omvat zowel actieve als inactieve bestemmingen.

Onder het totale aantal, selecteer **[!UICONTROL Destinations]** om naar de bestemmingen te navigeren doorbladert tabel. Deze pagina bevat een lijst met alle doelen waarmee u tot op heden verbinding hebt gemaakt.

![De widget Aantal bestemmingen.](../images/destinations/destinations-count.png)

### [!UICONTROL Destination status] {#destination-status}

De [!UICONTROL Destination status] widget geeft het totale aantal ingeschakelde bestemmingen als één enkele metrische waarde weer en gebruikt een donutgrafiek om het proportionele verschil tussen toegelaten en gehandicapte bestemmingen te illustreren.

Individuele tellingen voor of toegelaten of gehandicapte bestemmingen worden getoond in een dialoog wanneer de curseur over de respectieve sectie van de donutgrafiek beweegt.

![De statuswidget Doel.](../images/destinations/destination-status.png)

### [!UICONTROL Active destinations by destination platform] {#active-destinations-by-destination-platform}

Widget verstrekt een twee kolomlijst om een lijst van actieve bestemmingsplatforms en het totale aantal actieve bestemmingen voor elk bestemmingsplatform te tonen. De lijst met doelplatforms is van hoog naar laag geordend.

![De actieve bestemmingen door bestemmingsplatformwidget.](../images/destinations/active-destinations-by-destination-platform.png)

### [!UICONTROL Activated audiences across all destinations] {#activated-audiences-across-all-destinations}

De [!UICONTROL Activated audiences across all destinations] widget geeft het totale aantal soorten publiek aan dat voor alle bestemmingen in één meting wordt geactiveerd.

>[!NOTE]
>
>Deze widget geeft het aantal doelgroepen weer en niet het aantal segmenten.

Dit getal is nauwkeurig tot aan de meest recente opname.

![Het actieve publiek voor alle doelen van de widget.](../images/destinations/activated-audiences-across-all-destinations.png)

Selecteren **[!UICONTROL Audiences]** om naar de bestemmingen te navigeren [!UICONTROL Browse] tab. Deze pagina verstrekt een lijst van alle toegelaten bestemmingen en een verscheidenheid van relevante metriek. Zie de documentatie voor meer informatie over de [[!UICONTROL Browse] tab](../../destinations/ui/destinations-workspace.md#browse).

Zie de sectie met voorwaarden voor de [definities van gebruikte termen](#prerequisites) in deze beschrijving.

### [!UICONTROL Activated audiences] {#activated-audiences}

Deze widget biedt één meting voor het totale aantal soorten publiek dat aan een doel wordt geactiveerd.

![De widget voor geactiveerd publiek.](../images/destinations/activated-audiences.png)

Selecteren **[!UICONTROL Audiences]** om naar de detailspagina van het bestemmingdashboard te navigeren. De [!UICONTROL Activation data] wordt een lijst weergegeven met segmenten die aan de bestemming zijn toegewezen, inclusief de begindatum en einddatum (indien van toepassing) en andere relevante informatie voor de gegevensexport, zoals het exporttype, de planning en de frequentie. Als u de details over een bepaald segment wilt weergeven, selecteert u de naam in de lijst.

![De pagina met informatie over het doeldashboard met het tabblad Activeringsgegevens is gemarkeerd.](../images/destinations/activation-data-tab.png)

Deze widget helpt u de waarde van uw bestemmingen te begrijpen die op het aantal publiek wordt gebaseerd dat bij een blik wordt geactiveerd. Het biedt ook eenvoudig toegang tot meer gedetailleerde informatie voor verdere analyse.

Zie de sectie met voorwaarden voor de [definities van gebruikte termen](#prerequisites) in deze beschrijving.

## Volgende stappen

Als u dit document volgt, kunt u nu het dashboard voor doelen vinden en begrijpen welke maatstaven worden weergegeven in de beschikbare widgets. Als u meer wilt weten over het werken met bestemmingen in Experience Platform, raadpleegt u de [documentatie voor doelen](../../destinations/home.md).
