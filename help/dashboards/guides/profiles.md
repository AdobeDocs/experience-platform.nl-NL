---
keywords: Experience Platform;profiel;real-time klantprofiel;gebruikersinterface;UI;aanpassing;profiel dashboard;dashboard
title: Profieldashboard
description: Adobe Experience Platform biedt een dashboard waarmee u belangrijke informatie kunt bekijken over de gegevens van het klantprofiel in realtime van uw organisatie.
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: 4bb0078b6687da5239f57e7285507815aa7f3255
workflow-type: tm+mt
source-wordcount: '3588'
ht-degree: 0%

---

# [!UICONTROL Profiles] dashboard

De gebruikersinterface van Adobe Experience Platform (UI) verstrekt een dashboard waardoor u belangrijke informatie over uw kunt bekijken [!DNL Real-time Customer Profile] gegevens, zoals vastgelegd tijdens een dagelijkse momentopname. In deze handleiding wordt beschreven hoe u de [!UICONTROL Profiles] dashboard in UI en verstrekt informatie betreffende de metriek die in het dashboard wordt getoond.

Voor een overzicht van alle profielfuncties in de gebruikersinterface van het Experience Platform gaat u naar de [Gebruikershandleiding voor gebruikersprofiel voor realtime klanten](../../profile/ui/user-guide.md).

## Profieldashboardgegevens

De [!UICONTROL Profiles] Het dashboard toont een momentopname van de attributen (verslag) gegevens die uw organisatie binnen de Opslag van het Profiel in Experience Platform heeft. De momentopname bevat geen gebeurtenis (tijdreeks)-gegevens.

De kenmerkgegevens in de momentopname geven de gegevens precies zo weer als op het specifieke tijdstip waarop de momentopname is gemaakt. Met andere woorden, de momentopname is geen benadering of voorbeeld van de gegevens, en het dashboard van het Profiel werkt niet in real time bij.

>[!NOTE]
>
>Wijzigingen of updates die zijn aangebracht in de gegevens nadat de momentopname is gemaakt, worden pas in het dashboard weergegeven als de volgende momentopname is gemaakt.

## De [!UICONTROL Profiles] dashboard

Ga naar de [!UICONTROL Profiles] dashboard in de interface van het Platform, selecteert u **[!UICONTROL Profiles]** in het linkerspoor, dan selecteer **[!UICONTROL Overview]** om het dashboard weer te geven.

>[!NOTE]
>
>Als uw organisatie nieuw aan Platform is en nog niet de actieve datasets van het Profiel of gecreeerd verenigingsbeleid heeft, [!UICONTROL Profiles] het dashboard is niet zichtbaar. In plaats daarvan [!UICONTROL Overview] op het tabblad vindt u koppelingen en documentatie om u te helpen aan de slag te gaan met het Real-Time Klantprofiel.

![](../images/profiles/dashboard-overview.png)

### Het wijzigen van [!UICONTROL Profiles] dashboard

U kunt de weergave van het dialoogvenster [!UICONTROL Profiles] dashboard door **[!UICONTROL Modify dashboard]**. Hierdoor kunt u widgets verplaatsen, toevoegen en verwijderen van het dashboard en toegang krijgen tot de **[!UICONTROL Widget library]** om beschikbare widgets te verkennen en aangepaste widgets voor uw organisatie te maken.

Raadpleeg de [wijzigen, dashboards](../customize/modify.md) en [Overzicht van widgetbibliotheek](../customize/widget-library.md) documentatie voor meer informatie.

## (Beta) Gegevens over de werkzaamheid van profielen {#profile-efficacy-insights}

>[!IMPORTANT]
>
>De functionaliteit voor het verkrijgen van inzicht in de werkzaamheid van het profiel is momenteel in bèta beschikbaar en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

De [!UICONTROL Efficacy] biedt metriek over de kwaliteit en volledigheid van uw profielgegevens door het gebruik van profieleffectiviteitswidgets. Deze widgets illustreren in een oogopslag de samenstelling van uw profielen, tendensen in volledigheid in tijd, en beoordelingen van de kwaliteit van uw profielgegevens.

![Het dashboard voor de werkzaamheid van het profiel.](../images/profiles/attributes-quality-assessment.png)

Zie de [sectie over de doeltreffendheid van profielen](#profile-efficacy-widgets) voor meer informatie over de widgets die momenteel beschikbaar zijn.

De indeling van dit dashboard kan ook worden aangepast door [**[!UICONTROL Modify dashboard]**](../customize/modify.md) van de [!UICONTROL Overview] tab.

## Bladeren door profielen {#browse-profiles}

De [!UICONTROL Browse] kunt u de alleen-lezen profielen die in uw organisatie worden opgenomen, doorzoeken en bekijken. Van hieruit kunt u belangrijke informatie zien die tot het profiel behoort met betrekking tot hun voorkeuren, gebeurtenissen uit het verleden, interacties en segmenten

Zie de documentatie over voor meer informatie over de mogelijkheden voor profielweergave die worden geboden in de interface van het Platform [browserprofielen in Real-time Customer Data Platform](../../rtcdp/profile/profile-browse.md).

## Beleid samenvoegen {#merge-policies}

De maatstaven die worden weergegeven in het dialoogvenster [!UICONTROL Profiles] Het dashboard is gebaseerd op samenvoegbeleid dat wordt toegepast op uw gegevens van het Profiel van de Klant in real time. Wanneer gegevens uit meerdere bronnen worden samengevoegd om het klantprofiel te maken, kunnen de gegevens conflicterende waarden bevatten. Bijvoorbeeld, kan één dataset een klant als &quot;enig&quot;vermelden terwijl een andere dataset de klant als &quot;gehuwd&quot;kan vermelden. Het is de taak van het fusiebeleid om te bepalen welke gegevens aan prioriteren en vertoning als deel van het profiel moeten.

Voor meer informatie over fusiebeleid, met inbegrip van hoe te om, een standaard fusiebeleid voor uw organisatie tot stand te brengen uit te geven en te verklaren, gelieve te beginnen door te lezen [overzicht van samenvoegbeleid](../../profile/merge-policies/overview.md).

Het dashboard selecteert automatisch een samenvoegbeleid dat moet worden gebruikt. Het toegepaste samenvoegbeleid kan worden gewijzigd via het vervolgkeuzemenu naast de naam van het samenvoegbeleid.

>[!NOTE]
>
>In het vervolgkeuzemenu ziet u alleen samenvoegbeleid voor de klasse Individueel profiel van XDM. Nochtans, als uw organisatie veelvoudige samenvoegingsbeleid heeft gecreeerd, kan het betekenen dat u zult moeten scrollen om de volledige lijst van beschikbare samenvoegingsbeleid te bekijken.

![](../images/profiles/select-merge-policy.png)

## Unieregelingen

De [!UICONTROL Union Schema] Het dashboard geeft het samenvoegingsschema voor een specifieke XDM-klasse weer. Als u **[!UICONTROL Class]** kunt u de samenvoegingsschema&#39;s voor verschillende XDM-klassen weergeven.

De schema&#39;s van de unie zijn samengesteld uit veelvoudige schema&#39;s die de zelfde klasse delen en voor Profiel toegelaten. Ze stellen u in staat om in één weergave een samenvoeging te zien van elk veld in elk schema dat dezelfde klasse deelt.

Zie de gids UI van het unieschema om meer over te leren [verenigingsschema&#39;s weergeven in de gebruikersinterface van het Platform](../../profile/ui/union-schema.md#view-union-schemas).

## Widgets en metriek

Het dashboard bestaat uit widgets. Dit zijn alleen-lezen metriek die belangrijke informatie over uw profielgegevens verschaft.

De datum en tijd &#39;laatst bijgewerkt&#39; op een widget geeft aan wanneer de laatste momentopname van de gegevens is gemaakt. De datum en het tijdstip van de momentopname worden in UTC vermeld; het bevindt zich niet in de tijdzone van de individuele gebruiker of organisatie.

## Standaardwidgets {#standard-widgets}

Adobe biedt meerdere standaardwidgets die u kunt gebruiken voor het visualiseren van verschillende meetgegevens die betrekking hebben op uw profielgegevens. U kunt ook aangepaste widgets maken die u met uw organisatie kunt delen met de [!UICONTROL Widget library]. Als u meer wilt weten over het maken van aangepaste widgets, leest u eerst de [Overzicht van widgetbibliotheek](../customize/widget-library.md).

Als u meer wilt weten over elk van de beschikbare standaardwidgets, selecteert u de naam van een widget in de volgende lijst:

* [[!UICONTROL Profile count]](#profile-count)
* [[!UICONTROL Profiles added]](#profiles-added)
* [[!UICONTROL Profiles added trend]](#profiles-added-trend)
* [[!UICONTROL Profiles by identity]](#profiles-by-identity)
* [[!UICONTROL Identity overlap]](#identity-overlap)
* [[!UICONTROL Single identity profiles]](#single-identity-profiles)
* [[!UICONTROL Unsegmented profiles]](#unsegmented-profiles)
* [[!UICONTROL Unsegmented profiles trend]](#unsegmented-profiles-trend)
* [[!UICONTROL Unsegmented profiles by identity]](#unsegmented-profiles-by-identity)
* [[!UICONTROL Audiences]](#audiences)
* [[!UICONTROL Audiences mapped to destination status]](#audiences-mapped-to-destination-status)
* [[!UICONTROL Audiences size]](#audiences-size)
* [[!UICONTROL Profile count trend]](#profile-count-trend)
* [[!UICONTROL Single identity profiles by identity]](#single-identity-profiles-by-identity)
* [[!UICONTROL Audience overlap by merge policy]](#audience-overlap-by-merge-policy)
* [[!UICONTROL Profiles count change trend by identity]](#profiles-count-change-trend-by-identity)

### [!UICONTROL Profile count] {#profile-count}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilecount"
>title="Aantal profielen"
>abstract="Deze widget geeft het totale aantal samengevoegde profielen weer in de profielopslag op het moment dat de momentopname werd gemaakt. Het getal is afhankelijk van het geselecteerde samenvoegbeleid dat wordt toegepast op de profielgegevens."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#profile-count" text="Meer informatie in documentatie"

De **[!UICONTROL Profile count]** In de widget wordt het totale aantal samengevoegde profielen weergegeven in de profielopslag op het moment dat de momentopname is gemaakt. Dit getal is het resultaat van het geselecteerde samenvoegbeleid dat wordt toegepast op de profielgegevens om profielfragmenten samen te voegen tot één profiel voor elke persoon.

Zie de [sectie over samenvoegbeleid eerder in dit document](#merge-policies) voor meer informatie.

>[!NOTE]
>
>De [!UICONTROL Profile count] widget kan een ander getal weergeven dan het aantal profielen dat wordt weergegeven op het tabblad [!UICONTROL Browse] in de [!UICONTROL Profiles] om meerdere redenen. De meest voorkomende reden hiervoor is omdat de [!UICONTROL Browse] tabblad verwijst naar het totale aantal samengevoegde profielen dat is gebaseerd op het standaardsamenvoegbeleid van uw organisatie, terwijl de [!UICONTROL Profile count] widget verwijst naar het totale aantal samengevoegde profielen op basis van het samenvoegbeleid dat u hebt geselecteerd voor weergave op het dashboard.
>
>Een andere algemene reden is dat er verschillen zijn tussen de tijd waarop de dashboardmomentopname wordt gemaakt en de tijd waarop de voorbeeldtaak voor de [!UICONTROL Browse] tab. U kunt zien wanneer de [!UICONTROL Profile count] widget is voor het laatst bijgewerkt door naar de tijdstempel op de widget te kijken en meer te weten te komen over de manier waarop de voorbeeldtaak wordt geactiveerd op het tabblad [!UICONTROL Browse] tabblad, zie de [sectie voor het aantal profielen in de gebruikersgids Gebruikersprofiel voor realtime klanten](https://experienceleague.adobe.com/docs/experience-platform/profile/ui/user-guide.html?lang=en#profile-count).

![](../images/profiles/profile-count.png)

### [!UICONTROL Profiles added] {#profiles-added}

<!-- This CONTEXTUALHELP was commented out because this widget name will change. Details in https://jira.corp.adobe.com/browse/PLAT-120313  -->

<!-- >[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesadded"
>title="Profiles added"
>abstract="This widget displays the total number of merged profiles **added** to the Profile Store at the time of the last snapshot. The number depends on the selected merge policy being applied to your Profile data."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#profiles-added" text="Learn more from documentation" -->

De **[!UICONTROL Profiles added]** In de widget wordt het totale aantal samengevoegde profielen weergegeven dat op het moment van de laatste opname aan de profielopslag is toegevoegd. Dit getal is het resultaat van het geselecteerde samenvoegbeleid dat wordt toegepast op de profielgegevens om profielfragmenten samen te voegen tot één profiel voor elke persoon. U kunt de keuzekiezer gebruiken om de profielen weer te geven die in de afgelopen 30 dagen, 90 dagen of 12 maanden zijn toegevoegd.

>[!NOTE]
>
>De [!UICONTROL Profiles added] widget geeft het aantal toegevoegde profielen aan **na** de eerste profielopname en de instelling van de Profile Store. Met andere woorden, als uw organisatie de Profile Store heeft ingesteld en op dag 1 4.000.000 heeft ingeslikt, is het dashboard binnen 24 uur beschikbaar, maar de [!UICONTROL Profiles added] widget wordt ingesteld op 0. Dit wordt gedaan om een piek te vermijden verbonden aan de aanvankelijke opname van profielen in het systeem. In de komende 30 dagen, neemt uw organisatie een extra 1.000.000 profielen in de Opslag van het Profiel op. Nadat de volgende opname wordt genomen, [!UICONTROL Profiles added] widget zou in totaal 1.000.000 toegevoegde profielen weergeven, terwijl de widget [!UICONTROL Profile count] widget zou in totaal 5.000.000 profielen weergeven.

![](../images/profiles/profiles-added.png)

### [!UICONTROL Profiles added trend] {#profiles-added-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesaddedtrend"
>title="Profielen hebben trend toegevoegd"
>abstract="Deze widget geeft het totale aantal samengevoegde profielen weer dat de afgelopen 30 dagen, 90 dagen of 12 maanden dagelijks aan de profielopslag is toegevoegd. Het nummer hangt ook af van het geselecteerde samenvoegbeleid dat wordt toegepast op de profielgegevens."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#profiles-count-trend" text="Meer informatie in documentatie"

De **[!UICONTROL Profiles added trend]** widget geeft het totale aantal samengevoegde profielen weer dat de afgelopen 30 dagen, 90 dagen of 12 maanden dagelijks aan de profielwinkel is toegevoegd. Dit aantal wordt bijgewerkt elke dag wanneer de momentopname wordt genomen, daarom als u profielen in Platform zou moeten opnemen, zou het aantal profielen niet worden weerspiegeld tot de volgende momentopname wordt genomen. Het aantal toegevoegde profielen is het resultaat van het geselecteerde samenvoegbeleid dat wordt toegepast op uw profielgegevens om profielfragmenten samen te voegen tot één profiel voor elke persoon.

Zie de [sectie over samenvoegbeleid eerder in dit document](#merge-policies) voor meer informatie.

De **[!UICONTROL Profiles added trend]** widget geeft een &#39;bijschriftknop&#39; in de rechterbovenhoek van de widget weer. Selecteren **[!UICONTROL Captions]** om het dialoogvenster voor automatische bijschriften te openen.

![Het tabblad Profieloverzicht waarin de trendwidget Profielen wordt weergegeven waaraan de knop Bijschriften is gemarkeerd.](../images/profiles/profiles-added-trend-captions.png)

Een machine het leren model produceert automatisch titels voor het beschrijven van de belangrijkste tendensen en belangrijke gebeurtenissen door de grafiek en de gegevens te analyseren.

![Het dialoogvenster voor automatische bijschriften voor de trendwidget voor profielen toegevoegd.](../images/profiles/profiles-added-trends-automatic-captions-dialog.png)

### [!UICONTROL Profiles by identity] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesbyidentity"
>title="Profielen op identiteit"
>abstract="Deze widget geeft de indeling van alle samengevoegde profielen in uw profielarchief op basis van identiteiten weer."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#profiles-by-identity" text="Meer informatie in documentatie"

De **[!UICONTROL Profiles by identity]** widget geeft de indeling van de identiteiten in alle samengevoegde profielen in uw profielarchief weer. Het totale aantal profielen op basis van identiteit (met andere woorden, door de waarden voor elke naamruimte bij elkaar op te tellen) kan hoger zijn dan het totale aantal samengevoegde profielen, omdat aan één profiel meerdere naamruimten kunnen zijn gekoppeld. Bijvoorbeeld, als een klant met uw merk op meer dan één kanaal in wisselwerking staat, zullen de veelvoudige namespaces met die individuele klant worden geassocieerd.

Zie de [sectie over samenvoegbeleid eerder in dit document](#merge-policies) voor meer informatie.

![Het overzichtdashboard Profielen met de widget Profielen op identiteit gemarkeerd.](../images/profiles/profiles-by-identity.png)

Selecteren **[!UICONTROL Captions]** om het dialoogvenster voor automatische bijschriften te openen.

![De profielen op dialoogvenster voor identiteitsondertitels.](../images/profiles/profiles-by-identity-captions.png)

Een machine-leermodel produceert automatisch gegevensinzichten door de algemene distributie en belangrijkste dimensies van de gegevens te analyseren.

Ga voor meer informatie over identiteiten naar de [Documentatie bij Adobe Experience Platform Identity Service](../../identity-service/home.md).

### [!UICONTROL Identity overlap] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_identityoverlap"
>title="Identiteitsoverlapping"
>abstract="Deze widget gebruikt een Venn-diagram om de overlapping weer te geven van profielen in uw profielarchief die de twee geselecteerde identiteiten bevatten."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#identity-overlap" text="Meer informatie in documentatie"

De **[!UICONTROL Identity overlap]** widget gebruikt een Venn-diagram, of een setdiagram, om de overlapping weer te geven van profielen in uw profielarchief die de twee geselecteerde identiteiten bevatten.

Gebruik de widgetvervolgkeuzemenu&#39;s om de identiteiten te selecteren die u wilt vergelijken. De cirkels tonen het relatieve totale aantal profielen die elke identiteit bevatten. Het aantal profielen met beide identiteiten wordt weergegeven door de grootte van de overlapping tussen de cirkels. Als een klant op meer dan één kanaal met uw merk in wisselwerking staat, zullen de veelvoudige identiteiten met die individuele klant worden geassocieerd, daarom is het waarschijnlijk dat uw organisatie veelvoudige profielen zal hebben die fragmenten van meer dan één identiteit bevatten.

Voor meer informatie over profielfragmenten begint u met het lezen van de sectie over [profielfragmenten versus samengevoegde profielen](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=en#profile-fragments-vs-merged-profiles) in het overzicht van het profiel van de Klant in real time.

Ga voor meer informatie over identiteiten naar de [Documentatie bij Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/profiles/identity-overlap.png)

### [!UICONTROL Single identity profiles] {#single-identity-profiles}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_singleidentityprofiles"
>title="Eén identiteitsprofiel"
>abstract="Deze widget bevat een aantal profielen van uw organisatie die slechts één type id hebben waarmee hun identiteit wordt gemaakt. Dit id-type kan een e-mail of een ECID zijn."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#single-identity-profiles" text="Meer informatie in documentatie"

De [!UICONTROL Single Identity Profiles] widget bevat een aantal profielen van uw organisatie die slechts één type id hebben waarmee hun identiteit wordt gemaakt. Dit id-type kan een e-mail of een ECID zijn. Het aantal profielen wordt gegenereerd op basis van de gegevens in de meest recente momentopname.

![Widget Single Identity Profiles.](../images/profiles/single-identity-profiles.png)

### [!UICONTROL Unsegmented profiles] {#unsegmented-profiles}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofiles"
>title="Niet-gesegmenteerde profielen"
>abstract="Deze widget geeft het totale aantal profielen weer dat niet aan een segment is gekoppeld en biedt de mogelijkheid om profielen in uw hele organisatie te activeren."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#unsegmented-profiles" text="Meer informatie in documentatie"

De [!UICONTROL Unsegmented Profiles] widget geeft het totale aantal profielen weer dat niet aan een segment is gekoppeld. Het gegenereerde nummer is nauwkeurig vanaf de laatste momentopname en biedt de mogelijkheid om het profiel in uw organisatie te activeren. Het wijst ook op de kans om profielen uit te sluiten die geen adequate ROI verstrekken.

![De widget Niet-gesegmenteerde profielen.](../images/profiles/unsegmented-profiles.png)

### [!UICONTROL Unsegmented profiles trend] {#unsegmented-profiles-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofilestrend"
>title="Trend voor niet-gesegmenteerde profielen"
>abstract="Deze widget verschaft een lijngrafiekillustratie voor het aantal profielen dat gedurende een bepaalde tijdsperiode niet aan een segment is gekoppeld. De trend van profielen die niet aan om het even welk segment verbonden zijn kan over 30 dagen, 90 dagen, en periodes van 12 maanden worden visualiseerd."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#unsegmented-profiles-trend" text="Meer informatie in documentatie"

De [!UICONTROL Unsegmented Profiles Trend] widget geeft een illustratie van de lijngrafiek voor het aantal profielen die niet aan om het even welk segment over een bepaalde periode in bijlage zijn. De trend van profielen die niet aan om het even welk segment verbonden zijn kan over 30 dagen, 90 dagen, en periodes van 12 maanden worden visualiseerd. De tijdsperiode wordt gekozen in een vervolgkeuzemenu in de widget. Het aantal profielen wordt weerspiegeld op de y-as en de tijd op de x-as.

![De trendwidget voor niet-gesegmenteerde profielen.](../images/profiles/unsegmented-profiles-trend.png)

### [!UICONTROL Unsegmented profiles by identity] {#unsegmented-profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofilesbyidentity"
>title="Gesegmenteerde profielen opsplitsen op identiteit"
>abstract="Deze widget categoriseert het totale aantal niet-gesegmenteerde profielen op basis van hun unieke id."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#unsegmented-profiles-by-identity" text="Meer informatie in documentatie"

De [!UICONTROL Unsegmented Profiles by Identity] widget categoriseert het totale aantal niet-gesegmenteerde profielen op basis van hun unieke id. De gegevens worden in een staafdiagram weergegeven, zodat ze gemakkelijk kunnen worden vergeleken.

![De widget Niet-gesegmenteerde profielen op basis van identiteit.](../images/profiles/unsegmented-profiles-by-identity.png)

### [!UICONTROL Audiences] {#audiences}

Deze widget geeft het totale aantal segmenten weer dat gereed is om te worden geactiveerd, op basis van het gekozen samenvoegbeleid dat op de profielgegevens wordt toegepast.

Selecteren **[!UICONTROL Audiences]** om naar de [!UICONTROL Segments] dashboard [!UICONTROL Browse] tab. Van daar kunt u een lijst van alle segmentdefinities voor uw organisatie zien.

![De widget Soorten publiek.](../images/profiles/audiences.png)

<!-- https://jira.corp.adobe.com/browse/PLAT-115291 -->

<!-- * [[!UICONTROL Audiences change trend]](#audiences-change-trend) -->
<!-- ### [!UICONTROL Audiences change trend] {#audiences-change-trend}

This line graph widget visualizes the change in the total number of audiences each day, trending over time. The change in the number of audiences is dependent on the selected merge policy being applied to your profile data. The period of analysis is selected from the widget dropdown menu. The bar chart can be visualized over 30 days, 90 days, and 12-month periods.  

The visualization allows you to monitor the overall health of audiences within Adobe Experience Platform by understanding trends in the growth or decline of the total number of audiences. -->

<!-- ![The Audiences change trend widget.]() -->

<!-- * [[!UICONTROL Audience overlap report]](#audience-overlap-report) -->
<!-- ### [!UICONTROL Audience overlap report] {#audience-overlap-report} -->

<!-- View an ordered list of audiences by highest or lowest overlap percentages by selected merge policy. -->
<!-- ![The Audiences overlap report widget.]() -->
<!-- https://jira.corp.adobe.com/browse/PLAT-126851 -->

### [!UICONTROL Audiences mapped to destination status] {#audiences-mapped-to-destination-status}

De [!UICONTROL Audiences mapped to destination status] widget geeft het totale aantal in kaart gebrachte en niet in kaart gebrachte doelgroepen in één meting weer en gebruikt een donutdiagram om het proportionele verschil tussen hun totalen aan te geven. De berekende aantallen zijn afhankelijk van het gekozen samenvoegbeleid.

Individuele tellingen voor of in kaart gebracht of unmapped publiek worden getoond in een dialoog wanneer de curseur over de respectieve sectie van de donutgrafiek beweegt.

![Het publiek dat is toegewezen aan de doelstatuswidget.](../images/profiles/audiences-mapped-to-destination-status.png)

### [!UICONTROL Audiences size] {#audiences-size}

De [!UICONTROL Audiences size] widget biedt een tabel met twee kolommen met maximaal 20 segmenten en het totale aantal soorten publiek in elk segment. De lijst wordt geordend van hoog tot laag op basis van het totale aantal doelgroepen. Het totale aantal publieksgrootten is afhankelijk van het toegepaste samenvoegingsbeleid.

![De widget voor soorten publiek.](../images/profiles/audiences-size.png)

Om uitvoerige informatie over een segment te zien, selecteer een segmentnaam van de lijst wordt verstrekt om aan te navigeren [!UICONTROL Segments] [!UICONTROL Detail] pagina. Ook door **[!UICONTROL View all segments]** vanaf het einde van de widget kunt u naar het [!UICONTROL Segments] [!UICONTROL Browse] om een bestaand segment te zoeken.

![De widget Doelgrootte met een segmentnaam en de gemarkeerde segmenttekst weergeven.](../images/profiles/audiences-size-view-all-segments.png)

Zie de documentatie voor meer informatie over de [[!UICONTROL Segments] [!UICONTROL  Browse] tab](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#browse).

### [!UICONTROL Profile count trend] {#profile-count-trend}

De [!UICONTROL Profile count trend] widget gebruikt een lijngrafiek om de trend in het totale aantal profielen in het systeem in tijd te illustreren. Dit totale aantal bevat alle profielen die sinds de laatste dagelijkse momentopname in het systeem zijn geïmporteerd. De gegevens kunnen gedurende perioden van 30 dagen, 90 dagen en 12 maanden worden weergegeven. De tijdsperiode wordt gekozen in een vervolgkeuzemenu in de widget.

![De trendwidget Aantal profielen.](../images/profiles/profile-count-trend.png)

### [!UICONTROL Single identity profiles by identity] {#single-identity-profiles-by-identity}

Deze widget gebruikt een staafdiagram om het totale aantal profielen te illustreren dat met slechts één unieke id wordt geïdentificeerd. De widget ondersteunt maximaal vijf van de meest voorkomende identiteiten.

Houd de muisaanwijzer boven afzonderlijke balken om een dialoogvenster weer te geven met het totale aantal profielen voor een identiteit.

![De widget Single Identity-profielen op basis van identiteit.](../images/profiles/single-identity-profiles-by-identity.png)

### [!UICONTROL Audience overlap by merge policy] {#audience-overlap-by-merge-policy}

Deze widget gebruikt een Venn-diagram om de overlapping van twee geselecteerde segmenten weer te geven. Het samenvoegbeleid wordt gekozen uit de overzichtsvervolgkeuzelijst boven aan de pagina en de segmenten voor analyse worden geselecteerd uit twee vervolgkeuzemenu&#39;s binnen de widget. Het totale aantal profielen binnen de relevante segmentdefinitie kan worden gezien door de cursor over een cirkel of de doorsnede te bewegen.

Aangezien widget de visuele oversteekplaats van segmentdefinities toont, kunt u uw segmenteringsstrategie optimaliseren door gelijkenissen tussen uw segmentdefinities te bestuderen.

![Het dashboard Profielen UI van het Platform met de dropdown van het fusiebeleid en widgetsegmentdalingen benadrukt.](../images/profiles/audience-overlap-by-merge-policy.png)

### [!UICONTROL Profiles count change trend by identity] {#profiles-count-change-trend-by-identity}

<!-- This widget uses a line graph to illustrate the change in number of profiles filtered by a chosen source identity and merge policy. -->

Deze widget filtert het aantal profielen op basis van een geselecteerde bronidentiteit en het samenvoegbeleid en illustreert vervolgens de wijziging in aantal voor verschillende periodes aan de hand van een lijngrafiek. Het samenvoegbeleid wordt geselecteerd in de overzichtsvervolgkeuzelijst boven aan de pagina. De bronidentiteit en de tijdsperiode worden geselecteerd in de widgetvervolgkeuzemenu&#39;s. De trend kan worden weergegeven over perioden van 30 dagen, 90 dagen en 12 maanden.

Met deze widget kunt u de behoeften voor doelactivering beheren door het groeipatroon van profielen aan te tonen die met een vereiste identiteit zijn gefilterd.

![De trend in het aantal profielen verandert per identiteitswidget.](../images/profiles/profiles-count-change-trend-by-identity.png)


## (bèta) Profielefficiëntiewidgets {#profile-efficacy-widgets}

>[!IMPORTANT]
>
>De widgets voor profieleffectiviteit zijn momenteel in bèta beschikbaar en niet voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

Adobe verstrekt veelvoudige widgets om de volledigheid van de ingebedde profielen beschikbaar voor uw gegevensanalyse te beoordelen. Elk van de widgets voor de profieleffectiviteit kan worden gefilterd door het samenvoegbeleid. Als u het filter Samenvoegbeleid wilt wijzigen, selecteert u de optie[!UICONTROL Profiles using merge policy] en kiest u het juiste beleid in de beschikbare lijst.

Als u meer wilt weten over elk van de widgets voor de doeltreffendheid van het profiel, selecteert u de naam van een widget in de volgende lijst:

* [[!UICONTROL Attribute quality assessment]](#attributes-quality-assessment)
* [[!UICONTROL Profiles by completeness]](#profiles-by-completeness)
* [[!UICONTROL Profiles completeness trend]](#profiles-completeness-trend)

### (bèta) [!UICONTROL Attributes quality assessment] {#attributes-quality-assessment}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_attributesqualityassessment"
>title="Kenmerken, kwaliteitsbeoordeling"
>abstract="Deze widget geeft de volledigheid en kardinaliteit van alle profielen weer, afhankelijk van hun kenmerken. Elke rij beschrijft één kenmerk. De **Profielen** bevat het aantal profielen met dit kenmerk en de waarden zijn niet-null. De **Volledigheid** Het percentage wordt bepaald door het totale aantal profielen dat dit kenmerk heeft en wordt gevuld met waarden die niet gelijk zijn aan null, gedeeld door het totale aantal niet-lege waarden in de profielen voor dat kenmerk. **Kardinaal** Hiermee wordt het totale aantal unieke niet-null-waarden van dit kenmerk voor alle kenmerken aangegeven."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#attributes-quality-assessment" text="Meer informatie in documentatie"

De [!UICONTROL Attribute quality assessment] widget geeft de volledigheid en de kardinaliteit van alle profielen aan volgens hun kenmerken . De gegevens zijn nauwkeurig tot de laatste verwerkingsdatum. Deze informatie wordt voorgesteld als een lijst met vier kolommen waar elke rij in de lijst één enkel attribuut vertegenwoordigt.

| Kolom | Beschrijving |
|---|---|
| Kenmerk | The name of the attribute. |
| Profielen | Het aantal profielen dat dit kenmerk heeft en dat is gevuld met waarden die niet &#39;null&#39; zijn. |
| Volledigheid | Dit percentage wordt bepaald door het totale aantal profielen dat dit kenmerk heeft en wordt gevuld met waarden die niet gelijk zijn aan null. Het getal wordt berekend door het totale aantal profielen te delen door het totale aantal niet-lege waarden in de profielen voor dat kenmerk. |
| Kardinaal | Het totale aantal **uniek** niet-null waarden van dit kenmerk. Deze wordt in alle profielen gemeten. |

![De widget voor kwaliteitsbeoordeling van kenmerken](../images/profiles/attributes-quality-assessment.png)

### (bèta) [!UICONTROL Profiles by completeness] {#profiles-by-completeness}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesbycompleteness"
>title="Profielen op volledigheid"
>abstract="In het donutdiagram wordt het percentage van profielkenmerken weergegeven dat wordt gevuld met waarden die niet gelijk zijn aan null voor alle waargenomen kenmerken. Het illustreert het percentage profielen dat hoog, gemiddeld of laag volledig is. Voor profielen met hoge volledigheid zijn meer dan 70% van de bijbehorende kenmerken ingevuld. Normale volledigheidprofielen hebben tussen 30% en 70% van hun gevulde kenmerken. Lage volledigheidsprofielen hebben minder dan 30% van hun attributen gevuld."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#profile-completeness" text="Meer informatie in documentatie"

De [!UICONTROL Profiles by completeness] widget maakt een donut-overzicht van de volledigheid van het profiel sinds de laatste verwerkingsdatum. De volledigheid van een profiel wordt gemeten door het percentage attributen die met niet-krachtwaarden onder alle waargenomen attributen worden gevuld.

Deze widget geeft het percentage profielen weer dat hoog, gemiddeld of laag volledig is. Door gebrek, zijn er drie gevormde niveaus van volledigheid:

* Hoge volledigheid: Profielen hebben meer dan 70% van hun kenmerken ingevuld.
* Normale volledigheid: Profielen hebben tussen 30% en 70% van de bijbehorende kenmerken ingevuld.
* Lage volledigheid: Profielen hebben minder dan 30% van de bijbehorende kenmerken ingevuld.

![De profielen op de widget Volledigheid](../images/profiles/profiles-by-completeness.png)

### (bèta) [!UICONTROL Profiles completeness trend] {#profiles-completeness-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilescompletenesstrend"
>title="trend van volledigheid profielen"
>abstract="Deze widget maakt een gestapeld vlakdiagram waarin de trend van de volledigheid van het profiel in de loop der tijd wordt weergegeven. De volledigheid wordt gemeten door het percentage attributen die met niet-krachteloze waarden onder alle waargenomen attributen worden gevuld."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#profile-completeness-trend" text="Meer informatie in documentatie"

Deze widget maakt een gestapeld vlakdiagram waarin de trend van de volledigheid van het profiel in de loop der tijd wordt weergegeven. De volledigheid wordt gemeten door het percentage attributen die met niet-krachtwaarden onder alle waargenomen attributen worden gevuld. De profielvolledigheid wordt gecategoriseerd als hoog, gemiddeld of laag volledig sinds de laatste verwerkingsdatum.

Op de x-as wordt de tijd weergegeven, op de y-as wordt het aantal profielen weergegeven en op de kleuren worden de drie niveaus van profielvolledigheid weergegeven.

De drie volledigheidsniveaus zijn:

* Hoge volledigheid: Profielen hebben meer dan 70% van de gevulde kenmerken.
* Normale volledigheid: Profielen zijn voor minder dan 70% en voor meer dan 30% gevuld.
* Lage volledigheid: Profielen zijn voor minder dan 30% gevuld.

![De widget voor trend naar volledigheid van profielen](../images/profiles/profiles-completeness-trend.png)

## Volgende stappen

Als u dit document volgt, kunt u nu het dashboard Profielen vinden en begrijpen welke maatstaven worden weergegeven in de beschikbare widgets. Meer informatie over werken met [!DNL Profile] gegevens in de gebruikersinterface van het Experience Platform, gelieve te verwijzen naar [Gebruikershandleiding voor gebruikersprofiel voor realtime klanten](../../profile/ui/user-guide.md).
