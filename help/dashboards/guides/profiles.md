---
keywords: Experience Platform;profiel;real-time klantprofiel;gebruikersinterface;UI;aanpassing;profiel dashboard;dashboard
title: Handleiding voor het dashboard voor profielen
description: Adobe Experience Platform biedt een dashboard waarmee u belangrijke informatie kunt bekijken over de gegevens van het realtime klantprofiel van uw organisatie.
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: cd57ca50537d928025a5164b6a7d0ead490162ba
workflow-type: tm+mt
source-wordcount: '4058'
ht-degree: 0%

---

# [!UICONTROL Profiles] dashboard

De gebruikersinterface van Adobe Experience Platform (UI) verstrekt een dashboard waardoor u belangrijke informatie over uw kunt bekijken [!DNL Real-Time Customer Profile] gegevens, zoals vastgelegd tijdens een dagelijkse momentopname. In deze handleiding wordt beschreven hoe u het dashboard Profielen in de gebruikersinterface kunt openen en gebruiken en wordt informatie gegeven over de metriek die in het dashboard wordt weergegeven.

Zie de [Gebruikershandleiding voor realtime gebruikersprofiel van klanten](../../profile/ui/user-guide.md) voor een overzicht van de eigenschappen van het Profiel binnen het gebruikersinterface van het Experience Platform.

## Profieldashboardgegevens

Op het dashboard Profielen wordt een momentopname weergegeven van de kenmerkgegevens (record) die uw organisatie heeft in de profielopslag in Experience Platform. De momentopname bevat geen gebeurtenis (tijdreeks)-gegevens.

De kenmerkgegevens in de momentopname geven de gegevens precies zo weer als op het specifieke tijdstip waarop de momentopname is gemaakt. Met andere woorden, de momentopname is geen benadering of voorbeeld van de gegevens, en het dashboard van het Profiel werkt niet in real time bij.

>[!NOTE]
>
>Wijzigingen of updates die zijn aangebracht in de gegevens nadat de momentopname is gemaakt, worden pas in het dashboard weergegeven als de volgende momentopname is gemaakt.

## Het dashboard Profielen verkennen

Als u naar het dashboard Profielen in de interface van het platform wilt navigeren, selecteert u **[!UICONTROL Profiles]** in de linkerspoorstaaf, dan selecteer **[!UICONTROL Overview]** om het dashboard weer te geven.

>[!NOTE]
>
>Als uw organisatie nieuw aan Platform is en nog geen actieve datasets van het Profiel of gecreeerd samenvoegbeleid heeft, is het dashboard van Profielen niet zichtbaar. In plaats daarvan [!UICONTROL Overview] op het tabblad vindt u koppelingen en documentatie om u te helpen aan de slag te gaan met Real-Time Klantprofiel.

![Het dashboard Profielen Experience Platform met profielen en overzicht gemarkeerd.](../images/profiles/dashboard-overview.png)

### Het dashboard Profielen wijzigen

U kunt de weergave van het dashboard Profielen wijzigen door **[!UICONTROL Modify dashboard]**. U kunt widgets verplaatsen, toevoegen, vergroten, verkleinen en verwijderen van het dashboard en toegang krijgen tot de **[!UICONTROL Widget library]** om beschikbare widgets te verkennen en aangepaste widgets voor uw organisatie te maken.

Raadpleeg voor meer informatie de [wijzigen, dashboards](../customize/modify.md) en [Overzicht van widgetbibliotheek](../customize/widget-library.md) documentatie.

### Widgets toevoegen {#add-widget}

Selecteren **[!UICONTROL Add widget]** om naar de widgetbibliotheek te navigeren en een lijst met de beschikbare widgets te bekijken die aan uw dashboard moeten worden toegevoegd.

![Het dashboardoverzicht Profielen met de toegevoegde widget gemarkeerd.](../images/profiles/profiles-overview-add-widget.png)

In de widgetbibliotheek kunt u bladeren door de selectie van standaard- en aangepaste publiekswidgets. Raadpleeg de documentatie bij de widgetbibliotheek voor informatie over het toevoegen van widgets [Een widget toevoegen](../customize/widget-library.md#add-widgets).

<!-- ## (Beta) Profile efficacy insights {#profile-efficacy-insights}

>[!IMPORTANT]
>
>The profile efficacy insight functionality is currently in beta and are not available to all users. The documentation and the functionality are subject to change.

The [!UICONTROL Efficacy] tab provides metrics on the quality and completeness of your profile data through the use of profile efficacy widgets. These widgets illustrate at a glance the composition of your profiles, trends in completeness over time, and assessments on the quality of your profile data.

![The profile efficacy dashboard.](../images/profiles/attributes-quality-assessment.png)

See the [profile efficacy widgets section](#profile-efficacy-widgets) for more information on the widgets currently available.

The layout of this dashboard is also customizable by selecting [**[!UICONTROL Modify dashboard]**](../customize/modify.md) from the [!UICONTROL Overview] tab. -->

## Bladeren door profielen {#browse-profiles}

De [!UICONTROL Browse] kunt u de alleen-lezen profielen die in uw organisatie worden opgenomen, doorzoeken en bekijken. Van hieruit kunt u belangrijke informatie zien die tot het profiel behoort met betrekking tot hun voorkeuren, gebeurtenissen uit het verleden, interacties en doelgroepen.

Raadpleeg de documentatie over [browserprofielen in Adobe Real-time Customer Data Platform](../../rtcdp/profile/profile-browse.md).

## Beleid samenvoegen {#merge-policies}

De metriek die in het dashboard van Profielen wordt getoond is gebaseerd op samenvoegbeleid dat op uw gegevens van het Profiel van de Klant in real time wordt toegepast. Wanneer gegevens uit meerdere bronnen worden samengevoegd om het klantprofiel te maken, kunnen de gegevens conflicterende waarden bevatten. Bijvoorbeeld, kan één dataset een klant als &quot;enig&quot;vermelden terwijl een andere dataset de klant als &quot;gehuwd&quot;kan vermelden. Het is de taak van het fusiebeleid om te bepalen welke gegevens aan prioriteit en vertoning als deel van het profiel moeten.

Voor meer informatie over fusiebeleid, met inbegrip van hoe te om, een standaard fusiebeleid voor uw organisatie tot stand te brengen uit te geven uit te voeren, verwijs naar [overzicht van samenvoegbeleid](../../profile/merge-policies/overview.md).

Op het dashboard wordt automatisch een samenvoegbeleid geselecteerd dat moet worden gebruikt. Het toegepaste samenvoegbeleid kan worden gewijzigd via het vervolgkeuzemenu naast de naam van het samenvoegbeleid.

>[!NOTE]
>
>Het vervolgkeuzemenu bevat alleen samenvoegbeleidsregels die gebruikmaken van de `_xdm.context.profile` schema. Nochtans, als uw organisatie veelvoudige samenvoegingsbeleid heeft gecreeerd, kan het betekenen dat u moet scrollen om de volledige lijst van beschikbare samenvoegingsbeleid te bekijken.

![Het tabblad Profielen met de vervolgkeuzelijst Samenvoegbeleid gemarkeerd.](../images/profiles/select-merge-policy.png)

## Unieregelingen

De [!UICONTROL Union Schema] Het dashboard geeft het samenvoegingsschema voor een specifieke XDM-klasse weer. Als u **[!UICONTROL Class]** in het vervolgkeuzemenu kunt u de samenvoegingsschema&#39;s voor verschillende XDM-klassen weergeven.

De schema&#39;s van de unie zijn samengesteld uit veelvoudige schema&#39;s die de zelfde klasse delen en voor Profiel toegelaten. Ze stellen u in staat om in één weergave een samenvoeging te zien van elk veld in elk schema dat dezelfde klasse deelt.

Meer informatie over [Unieschema&#39;s weergeven in de interface van het platform](../../profile/ui/union-schema.md#view-union-schemas), raadpleegt u de UI-handleiding voor het samenvoegingsschema.

## Widgets en metriek

Het dashboard bestaat uit widgets. Dit zijn alleen-lezen metriek die belangrijke informatie over uw profielgegevens verschaft.

De datum en tijd van de meest recente opname worden boven aan het dialoogvenster [!UICONTROL Overview] naast de vervolgkeuzelijst Samenvoegingsbeleid. Alle widgetgegevens zijn nauwkeurig vanaf die datum en tijd. De tijdstempel van de momentopname wordt opgegeven in UTC; deze bevindt zich niet in de tijdzone van de individuele gebruiker of organisatie.

![Het tabblad Overzicht van het dashboard Profielen met de meest recente tijdstempel voor momentopnamen gemarkeerd.](../images/profiles/snapshot-timestamp.png)

## Standaardwidgets {#default-widgets}

Voor alle nieuwe Adobe Experience Platform-instanties wordt een standaardwidgetbelasting opgegeven die de meest recente inzichten van uw gegevens belicht. De volgende widgets zijn vooraf geconfigureerd in uw segmentweergave van meet af aan. Hieronder vindt u volledige informatie over het doel en de functie van de widgets.

* [[!UICONTROL Profile count]](#profile-count)
* [[!UICONTROL Profile count change]](#profile-count-change)
* [[!UICONTROL Profiles count change trend]](#profiles-count-change-trend)
* [[!UICONTROL Profiles by identity]](#profiles-by-identity)
* [[!UICONTROL Identity overlap]](#identity-overlap)

>[!NOTE]
>
>Vanaf 26 juli 2023 [!UICONTROL Profiles], [!UICONTROL Audiences], en [!UICONTROL Destinations] De overzichtdashboards zijn teruggesteld aan een nieuwe gebrek widget lading-uit voor alle gebruikers die hun meningen in de voorafgaande zes maanden niet veranderden. Raadpleeg de documentatie in het dialoogvenster [Doelen](./destinations.md#default-widgets) en [Soorten publiek](./audiences.md#default-widgets) standaardwidgetsecties voor details waarop widgets zijn opgenomen als onderdeel van de standaard-widget-taaktaken. U kunt uw dashboardwidgets op dezelfde manier blijven aanpassen als voorheen.

## AI-widgets van klant {#customer-ai-profiles-widgets}

Klant-AI wordt gebruikt om aangepaste eigenschapscores zoals churn en conversie voor individuele profielen op schaal te genereren. De AI van de klant doet dit door bestaande gegevens van de Gebeurtenis van de Consumentenervaring te analyseren om te voorspellen **scores voor churn- of conversiedichtheid**. Deze zeer nauwkeurige modellen van de klantenneiging staan voor nauwkeurigere segmentatie en het richten toe. De [verdeling van scores](#customer-ai-distribution-of-scores) en [overzicht van scores](#customer-ai-scoring-summary) inzichten tonen de verdeeldheid in uw publiek aan . Ze benadrukken welke profielen de hoge/lage/gemiddelde dichtheid zijn en hoe deze over het aantal profielen worden verdeeld.

* [[!UICONTROL Customer AI scoring summary]](#customer-ai-scoring-summary)
* [[!UICONTROL Customer AI distribution of scores]](#customer-ai-distribution-of-scores)

### [!UICONTROL Customer AI distribution of scores] {#customer-ai-distribution-of-scores}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_distributionOfScores"
>title="Verdeling van scores"
>abstract="Deze widget visualiseert de verdeling van het totale aantal profielen aan de hand van hun eigenschapscores in stappen van 5 procent. De verdeling van het profielaantal wordt bepaald door het AI-model en het geselecteerde samenvoegbeleid. U kunt het AI-model wijzigen in het vervolgkeuzemenu onder de titel van de widget."

De [!UICONTROL Customer AI distribution of scores] widget categoriseert het totale aantal profielen op basis van hun populatiescore . De verdeling van het profielaantal wordt bepaald door het AI model en het geselecteerde fusiebeleid, dan visualiseerd in vijf percententoename die op hun neiging wijzen. Het aantal profielen wordt opgegeven langs de Y-as en de dichtheidsscores langs de X-as.

>[!NOTE]
>
>Als de visualisatie een conversiesnelheidsscore is, worden de hoge scores groen en de lage scores rood weergegeven. Als je de eigenheid van de kroon voorspelt, wordt deze gespiegeld, dan zijn de hoge scores rood en zijn de lage scores groen. Het gemiddelde emmertje blijft geel ongeacht welk aandrijvingstype u kiest.

Het AI-model waarmee de densiteitsscores worden bepaald, wordt gekozen uit de vervolgkeuzelijst onder de titel van de widget. Het vervolgkeuzemenu bevat een lijst met alle geconfigureerde AI-modellen van de Klant. Selecteer het juiste AI-model voor uw analyse in de lijst met beschikbare modellen. Als er geen AI-model van de Klant beschikbaar is, geeft een bericht in de widget u de opdracht ten minste één AI-model van de Klant te configureren en wordt een hyperlink naar de configuratiepagina van het AI-model van de Klant weergegeven. Zie de documentatie voor instructies op [hoe te om een instantie van de KlantAI te vormen](../../intelligent-services/customer-ai/user-guide/configure.md).

>[!NOTE]
>
>Selecteer de vervolgkeuzelijst direct onder het tabblad Overzicht om het samenvoegbeleid te wijzigen dat bepaalt welke profielen in de analyse worden opgenomen. Zie de sectie over [beleid samenvoegen](#merge-policies) voor een korte beschrijving, of [overzicht van samenvoegbeleid](../../profile/merge-policies/overview.md) voor meer informatie .

Als u naar de pagina Gedetailleerde inzichten voor het geselecteerde AI-model van de Klant wilt navigeren, selecteert u **[!UICONTROL View model details]**.

![Het Experience Platform Soorten publiek dashboard met het [!UICONTROL Customer AI distribution of scores] widget en [!UICONTROL View model details] gemarkeerd.](../images/segments/customer-ai-distribution-of-scores.png)

De gedetailleerde pagina met modelinzichten wordt weergegeven.

![De pagina met inzichten voor de AI van de Klant.](../images/profiles/customer-ai-insights-page.png)

Meer informatie over de AI van de Klant vindt u op de [Dreamweaver-handleiding voor inzichten](../../intelligent-services/customer-ai/user-guide/discover-insights.md).

### [!UICONTROL Customer AI scoring summary] {#customer-ai-scoring-summary}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_scoringSummary"
>title="Overzicht van scores"
>abstract="Deze widget geeft het totale aantal scoreprofielen weer en categoriseert deze in emmers met een hoge, gemiddelde en lage dichtheid. Het donutdiagram illustreert de proportionele samenstelling van totale profielen in hoge, gemiddelde en lage dichtheid."

Deze widget geeft het totale aantal profielen met een score weer en categoriseert deze in emmers met een hoge, gemiddelde en lage dichtheid, respectievelijk groen, geel en rood. Een donutdiagram illustreert de proportionele samenstelling van profielen tussen hoge, gemiddelde en lage eigenschappen. Een profiel komt in aanmerking voor een hoge dichtheid van meer dan 75, een gemiddelde dichtheid tussen 25 en 74 en een lage dichtheid onder 24. Een legenda geeft de kleurcode en drempelwaarden van eigenschappen aan. De tellingen van het profiel voor de hoge, middelgrote, en lage eigenschappen worden getoond in een dialoog wanneer de curseur over de respectieve sectie van de donutgrafiek beweegt.

>[!NOTE]
>
>Als de visualisatie een conversiesnelheidsscore is, worden de hoge scores groen en de lage scores rood weergegeven. Als je de eigenheid van de kroon voorspelt, wordt deze gespiegeld, dan zijn de hoge scores rood en zijn de lage scores groen. Het gemiddelde emmertje blijft geel ongeacht welk aandrijvingstype u kiest.

Het vervolgkeuzemenu onder de widgettitel bevat een lijst met alle geconfigureerde AI-modellen van de Klant. Selecteer het juiste AI-model voor uw analyse in de lijst met beschikbare modellen. Als er geen AI-model van de Klant beschikbaar is, geeft een bericht in de widget u de opdracht ten minste één AI-model van de Klant te configureren en wordt een hyperlink naar de configuratiepagina van het AI-model van de Klant weergegeven. Zie de documentatie op [hoe te om een instantie van de KlantAI te vormen](../../intelligent-services/customer-ai/user-guide/configure.md) voor gedetailleerde instructies.

>[!NOTE]
>
>Het totale aantal berekende profielen is afhankelijk van het gekozen samenvoegingsbeleid. Als u het gebruikte samenvoegingsbeleid wilt wijzigen, selecteert u de vervolgkeuzelijst direct onder het tabblad Overzicht. Zie de sectie over [beleid samenvoegen](#merge-policies) voor een korte beschrijving, of [overzicht van samenvoegbeleid](../../profile/merge-policies/overview.md) voor meer informatie .

![Het dashboard Soorten publiek van het Experience Platform met de overzichtswidget voor scores van de Klant AI gemarkeerd.](../images/segments/customer-ai-scoring-summary.png)

Als u naar de pagina Gedetailleerde inzichten voor het geselecteerde AI-model van de Klant wilt navigeren, selecteert u **[!UICONTROL View model details]**. Meer informatie over de AI van de Klant vindt u op de [Dreamweaver-handleiding voor inzichten](../../intelligent-services/customer-ai/user-guide/discover-insights.md).

## Standaardwidgets {#standard-widgets}

Adobe biedt meerdere standaardwidgets die u kunt gebruiken voor het visualiseren van verschillende meetgegevens die betrekking hebben op de profielgegevens. U kunt ook aangepaste widgets maken die u met uw organisatie kunt delen met de [!UICONTROL Widget library]. Als u meer wilt weten over het maken van aangepaste widgets, leest u eerst de [Overzicht van widgetbibliotheek](../customize/widget-library.md).

Als u meer wilt weten over elk van de beschikbare standaardwidgets, selecteert u de naam van een widget in de volgende lijst:

* [[!UICONTROL Profile count]](#profile-count)
* [[!UICONTROL Profile count trend]](#profile-count-trend)
* [[!UICONTROL Profile count change]](#profile-count-change)
* [[!UICONTROL Profiles count change trend]](#profiles-count-change-trend)
* [[!UICONTROL Profiles count change trend by identity]](#profiles-count-change-trend-by-identity)
* [[!UICONTROL Profiles by identity]](#profiles-by-identity)
* [[!UICONTROL Identity overlap]](#identity-overlap)
* [[!UICONTROL Single identity profiles]](#single-identity-profiles)
* [[!UICONTROL Single identity profiles by identity]](#single-identity-profiles-by-identity)
* [[!UICONTROL Unsegmented profiles]](#unsegmented-profiles)
* [[!UICONTROL Unsegmented profiles change trend]](#unsegmented-profiles-change-trend)
* [[!UICONTROL Unsegmented profiles by identity]](#unsegmented-profiles-by-identity)
* [[!UICONTROL Audiences]](#audiences)
* [[!UICONTROL Audiences mapped to destination status]](#audiences-mapped-to-destination-status)
* [[!UICONTROL Audiences size]](#audiences-size)
* [[!UICONTROL Audience overlap by merge policy]](#audience-overlap-by-merge-policy)
* [[!UICONTROL Audience overlap report]](#audience-overlap-report)

### [!UICONTROL Profile count] {#profile-count}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilecount"
>title="Aantal profielen"
>abstract="Deze widget geeft het totale aantal samengevoegde profielen weer in de profielopslag op het moment dat de momentopname werd gemaakt. Het getal is afhankelijk van het geselecteerde samenvoegbeleid dat wordt toegepast op de profielgegevens."

De **[!UICONTROL Profile count]** In de widget wordt het totale aantal samengevoegde profielen weergegeven in de profielenwinkel op het moment dat de momentopname is gemaakt. Dit getal is het resultaat van het geselecteerde samenvoegbeleid dat wordt toegepast op de profielgegevens om profielfragmenten samen te voegen tot één profiel voor elke persoon.

Zie de [sectie over samenvoegbeleid eerder in dit document](#merge-policies) voor meer informatie.

>[!NOTE]
>
>De [!UICONTROL Profile count] widget kan een ander getal weergeven dan het aantal profielen dat wordt weergegeven op het tabblad [!UICONTROL Browse] in de [!UICONTROL Profiles] om meerdere redenen. De meest voorkomende reden voor dit verschil is dat [!UICONTROL Browse] tabblad verwijst naar het totale aantal samengevoegde profielen dat is gebaseerd op het standaardsamenvoegbeleid van uw organisatie, terwijl de [!UICONTROL Profile count] widget verwijst naar het totale aantal samengevoegde profielen op basis van het samenvoegbeleid dat u hebt geselecteerd voor weergave op het dashboard.
>
>Een andere algemene reden is dat er verschillen zijn tussen de tijd waarop de dashboardmomentopname wordt gemaakt en de tijd waarop de voorbeeldtaak voor de [!UICONTROL Browse] tab. U kunt zien wanneer de [!UICONTROL Profile count] widget is voor het laatst bijgewerkt door naar de tijdstempel op de widget te kijken. Meer informatie over de manier waarop de voorbeeldtaak wordt geactiveerd op het tabblad [!UICONTROL Browse] tabblad, zie de [de sectie van het profielaantal in de Realtime gids van het Profiel van de Klant UI](https://experienceleague.adobe.com/docs/experience-platform/profile/ui/user-guide.html?lang=en#profile-count).

![Het dashboard Profielen Experience Platform met de widget Aantal profielen gemarkeerd.](../images/profiles/profile-count.png)

### [!UICONTROL Profile count trend] {#profile-count-trend}

De [!UICONTROL Profile count trend] widget gebruikt een lijngrafiek om de trend in het totale aantal profielen in het systeem in tijd te illustreren. Dit totale aantal bevat alle profielen die sinds de laatste dagelijkse momentopname in het systeem zijn geïmporteerd. De gegevens kunnen gedurende perioden van 30 dagen, 90 dagen en 12 maanden worden weergegeven. De tijdsperiode wordt gekozen in een vervolgkeuzemenu in de widget.

![De trendwidget Aantal profielen.](../images/profiles/profile-count-trend.png)

### [!UICONTROL Profile count change] {#profile-count-change}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilescountchange"
>title="Wijziging van aantal profielen"
>abstract="Deze widget geeft het totale aantal samengevoegde profielen weer **added** naar de profielenwinkel op het moment van de laatste opname. Het getal is afhankelijk van het geselecteerde samenvoegbeleid dat wordt toegepast op de profielgegevens."

De **[!UICONTROL Profile count change]** wordt het aantal samengevoegde profielen weergegeven dat sinds de vorige momentopname aan de profielopslag is toegevoegd. Dit getal is het resultaat van het geselecteerde samenvoegbeleid dat wordt toegepast op de profielgegevens om profielfragmenten samen te voegen tot één profiel voor elke persoon. U kunt de keuzekiezer gebruiken om het aantal toegevoegde profielen weer te geven in de afgelopen 30 dagen, 90 dagen of 12 maanden.

>[!NOTE]
>
>De [!UICONTROL Profile count change] widget geeft het aantal toegevoegde profielen aan **na** de eerste profielopname en de instelling van de Profile Store. Met andere woorden, als uw organisatie de Profile Store heeft ingesteld en op dag 1 4.000.000 heeft ingeslikt, is het dashboard binnen 24 uur beschikbaar, maar de [!UICONTROL Profile count change] widget wordt ingesteld op 0. Deze telmethode wordt gebruikt om een piek te voorkomen die verband houdt met de eerste opname van profielen in het systeem. In de komende 30 dagen, neemt uw organisatie een extra 1.000.000 profielen in de Opslag van het Profiel op. Nadat de volgende opname wordt genomen, [!UICONTROL Profile count change] widget zou in totaal 1.000.000 toegevoegde profielen weergeven, terwijl de widget [!UICONTROL Profile count] widget zou in totaal 5.000.000 profielen weergeven.

![Het UI-profieldashboard van het platform met de widget voor het wijzigen van het aantal profielen gemarkeerd.](../images/profiles/profile-count-change.png)

### [!UICONTROL Profiles count change trend] {#profiles-count-change-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesaddedtrend"
>title="Ontwikkeling van aantal profielen"
>abstract="Deze widget geeft het aantal samengevoegde profielen weer dat de afgelopen 30 dagen, 90 dagen of 12 maanden dagelijks aan de profielwinkel is toegevoegd. Het nummer hangt ook af van het geselecteerde samenvoegbeleid dat wordt toegepast op de profielgegevens."

De **[!UICONTROL Profiles count change trend]** widget geeft het totale aantal samengevoegde profielen weer dat de afgelopen 30 dagen, 90 dagen of 12 maanden dagelijks aan de profielwinkel is toegevoegd. Dit aantal wordt bijgewerkt elke dag wanneer de momentopname wordt genomen, daarom als u profielen in Platform zou moeten opnemen, zou het aantal profielen niet worden weerspiegeld tot de volgende momentopname wordt genomen. Het aantal toegevoegde profielen is het resultaat van het geselecteerde samenvoegbeleid dat wordt toegepast op uw profielgegevens om profielfragmenten samen te voegen tot één profiel voor elke persoon.

Raadpleeg voor meer informatie de [sectie over samenvoegbeleid eerder in dit document](#merge-policies).

De **[!UICONTROL Profiles count change trend]** widget geeft een &#39;bijschriftknop&#39; in de rechterbovenhoek van de widget weer. Selecteer **[!UICONTROL Captions]**.

![Het tabblad Profieloverzicht waarin de trendwijzigingswidget voor het aantal profielen wordt weergegeven met de knop Bijschriften gemarkeerd.](../images/profiles/profiles-count-change-trend-captions.png)

Een machine het leren model produceert automatisch titels voor het beschrijven van de belangrijkste tendensen en belangrijke gebeurtenissen door de grafiek en de gegevens te analyseren. Annotaties worden op basis van de bijschriften toegevoegd aan het diagram. Selecteer een bijschrift waarop u de bijbehorende annotatie wilt toepassen.

![Het dialoogvenster met automatische bijschriften voor de trendwidget voor het aantal profielen verandert.](../images/profiles/profiles-added-trends-automatic-captions-dialog-with-annotation.png)

### [!UICONTROL Profiles count change trend by identity] {#profiles-count-change-trend-by-identity}

<!-- This widget uses a line graph to illustrate the change in number of profiles filtered by a chosen source identity and merge policy. -->

Deze widget filtert het aantal profielen op basis van een geselecteerde bronidentiteit en voegt het beleid samen. Vervolgens wordt de wijziging in aantal voor verschillende periodes aan de hand van een lijngrafiek getoond. Het samenvoegbeleid wordt geselecteerd in de overzichtsvervolgkeuzelijst boven aan de pagina, de bronidentiteit en de tijdsperiode worden geselecteerd in de widgetvervolgkeuzemenu&#39;s. De trend kan worden weergegeven over perioden van 30 dagen, 90 dagen en 12 maanden.

Met deze widget kunt u de behoeften voor doelactivering beheren door het groeipatroon van profielen aan te tonen die met een vereiste identiteit zijn gefilterd.

![De trend in het aantal profielen verandert per identiteitswidget.](../images/profiles/profiles-count-change-trend-by-identity.png)

### [!UICONTROL Profiles by identity] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesbyidentity"
>title="Profielen op identiteit"
>abstract="Deze widget geeft de indeling van alle samengevoegde profielen in uw profielarchief op basis van identiteiten weer."

De **[!UICONTROL Profiles by identity]** widget geeft de indeling van de identiteiten in alle samengevoegde profielen in uw profielarchief weer. Het totale aantal profielen op basis van identiteit (met andere woorden, door de waarden voor elke naamruimte bij elkaar op te tellen) kan hoger zijn dan het totale aantal samengevoegde profielen, omdat aan één profiel meerdere naamruimten kunnen zijn gekoppeld. Bijvoorbeeld, als een klant met uw merk op meer dan één kanaal in wisselwerking staat, zouden de veelvoudige namespaces met die individuele klant worden geassocieerd.

Raadpleeg voor meer informatie de [sectie over samenvoegbeleid eerder in dit document](#merge-policies).

![Het overzichtdashboard Profielen met de widget Profielen op identiteit gemarkeerd.](../images/profiles/profiles-by-identity.png)

Selecteer **[!UICONTROL Captions]**.

![De profielen op dialoogvenster voor identiteitsondertitels.](../images/profiles/profiles-by-identity-captions.png)

Een machine-leermodel produceert automatisch gegevensinzichten door de algemene distributie en belangrijkste dimensies van de gegevens te analyseren.

Raadpleeg voor meer informatie over identiteiten de [Documentatie bij Adobe Experience Platform Identity Service](../../identity-service/home.md).

### [!UICONTROL Identity overlap] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_identityoverlap"
>title="Identiteitsoverlapping"
>abstract="Deze widget gebruikt een Venn-diagram om de overlapping weer te geven van profielen in uw profielarchief die de twee geselecteerde identiteiten bevatten."

De **[!UICONTROL Identity overlap]** widget gebruikt een Venn-diagram, of een setdiagram, om de overlapping weer te geven van profielen in uw profielarchief die de twee geselecteerde identiteiten bevatten.

Gebruik de widgetvervolgkeuzemenu&#39;s om de identiteiten te selecteren die u wilt vergelijken. De cirkels tonen het relatieve totale aantal profielen die elke identiteit bevatten. Het aantal profielen met beide identiteiten wordt weergegeven door de grootte van de overlapping tussen de cirkels. Als een klant op meer dan één kanaal met uw merk communiceert, zouden veelvoudige identiteiten met die individuele klant worden geassocieerd. In dit geval is het waarschijnlijk dat uw organisatie meerdere profielen heeft die fragmenten van meer dan één identiteit bevatten.

Raadpleeg de sectie over profielfragmenten voor meer informatie over profielfragmenten [profielfragmenten versus samengevoegde profielen](../../profile/home.md#profile-fragments-vs-merged-profiles) in het overzicht van het profiel van de Klant in real time.

Raadpleeg voor meer informatie over identiteiten de [Documentatie bij Adobe Experience Platform Identity Service](../../identity-service/home.md).

![Het dashboardoverzicht van Profielen met de widget Identiteitsoverlap gemarkeerd.](../images/profiles/identity-overlap.png)

### [!UICONTROL Single identity profiles] {#single-identity-profiles}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_singleidentityprofiles"
>title="Eén identiteitsprofiel"
>abstract="Deze widget bevat een aantal profielen van uw organisatie die slechts één type id hebben waarmee hun identiteit wordt gemaakt. Dit id-type kan een e-mail of een ECID zijn."

De [!UICONTROL Single Identity Profiles] widget bevat een aantal profielen van uw organisatie die slechts één type id hebben waarmee hun identiteit wordt gemaakt. Dit id-type kan een e-mail of een ECID zijn. Het aantal profielen wordt gegenereerd op basis van de gegevens in de meest recente momentopname.

![Widget Single Identity Profiles.](../images/profiles/single-identity-profiles.png)

### [!UICONTROL Single identity profiles by identity] {#single-identity-profiles-by-identity}

Deze widget gebruikt een staafdiagram om het totale aantal profielen te illustreren dat met slechts één unieke id wordt geïdentificeerd. De widget ondersteunt maximaal vijf van de meest voorkomende identiteiten.

Als u een dialoogvenster wilt weergeven waarin het totale aantal profielen voor een identiteit wordt weergegeven, houdt u de cursor boven afzonderlijke balken.

![De widget Single Identity-profielen op basis van identiteit.](../images/profiles/single-identity-profiles-by-identity.png)

### [!UICONTROL Unsegmented profiles] {#unsegmented-profiles}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofiles"
>title="Niet-gesegmenteerde profielen"
>abstract="Deze widget geeft het totale aantal profielen weer dat niet aan een publiek is gekoppeld en biedt de mogelijkheid om profielen in uw hele organisatie te activeren."

De [!UICONTROL Unsegmented Profiles] widget geeft het totale aantal profielen weer dat niet aan een publiek is gekoppeld. Het gegenereerde nummer is nauwkeurig vanaf de laatste momentopname en biedt de mogelijkheid om het profiel in uw organisatie te activeren. Het wijst ook op de kans om profielen uit te sluiten die geen adequate ROI verstrekken.

![De widget Niet-gesegmenteerde profielen.](../images/profiles/unsegmented-profiles.png)

### [!UICONTROL Unsegmented profiles change trend] {#unsegmented-profiles-change-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofilestrend"
>title="Trend voor niet-gesegmenteerde profielen"
>abstract="Deze widget bevat een lijngrafiekillustratie voor het aantal profielen dat gedurende een bepaalde tijdsperiode niet aan een publiek is gekoppeld. De trend van profielen die niet aan een publiek zijn gekoppeld, kan worden weergegeven over perioden van 30 dagen, 90 dagen en 12 maanden."

De [!UICONTROL Unsegmented profiles change trend] widget gebruikt een lijngrafiek om het aantal profielen te illustreren dat sinds de laatste dagmomentopname wordt toegevoegd die niet aan om het even welk publiek in bijlage zijn. De veranderende trend van profielen die niet aan om het even welk publiek worden verbonden kan over 30 dagen, 90 dagen, en periodes van 12 maanden worden visualiseerd. De tijdsperiode wordt gekozen in een vervolgkeuzemenu in de widget. Het aantal profielen wordt weerspiegeld op de y-as en de tijd op de x-as.

![De trendwidget voor niet-gesegmenteerde profielen verandert.](../images/profiles/unsegmented-profiles-change-trend.png)

### [!UICONTROL Unsegmented profiles by identity] {#unsegmented-profiles-by-identity}

>[!NOTE]
>
>De niet-gesegmenteerde profielen per identiteitswidget zijn vanaf oktober 2022 afgekeurd en zijn niet meer beschikbaar.

<!-- 

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofilesbyidentity"
>title="Unsegmented profiles by identity"
>abstract="This widget categorizes the total number of unsegmented profiles by their unique identifier."

The [!UICONTROL Unsegmented Profiles by Identity] widget categorizes the total number of unsegmented profiles by their unique identifier. The data is visualized in a bar chart for ease of comparison. 

![The Unsegmented Profiles by Identity widget.](../images/profiles/unsegmented-profiles-by-identity.png) -->

### [!UICONTROL Audiences] {#audiences}

Deze widget geeft het totale aantal soorten publiek weer dat gereed is om te worden geactiveerd, afhankelijk van het gekozen samenvoegbeleid dat op de profielgegevens wordt toegepast.

Selecteren **[!UICONTROL Audiences]** om naar de [!UICONTROL Audiences] dashboard [!UICONTROL Browse] tab. Van daar, kunt u een lijst van alle segmentdefinities voor uw organisatie zien.

![De widget Soorten publiek.](../images/profiles/audiences.png)

<!-- https://jira.corp.adobe.com/browse/PLAT-115291 -->

<!-- * [[!UICONTROL Audiences change trend]](#audiences-change-trend) -->
<!-- ### [!UICONTROL Audiences change trend] {#audiences-change-trend}

This line graph widget visualizes the change in the total number of audiences each day, trending over time. The change in the number of audiences is dependent on the selected merge policy being applied to your profile data. The period of analysis is selected from the widget dropdown menu. The bar chart can be visualized over 30 days, 90 days, and 12-month periods.

The visualization allows you to monitor the overall health of audiences within Adobe Experience Platform by understanding trends in the growth or decline of the total number of audiences. -->

<!-- ![The Audiences change trend widget.]() -->

### [!UICONTROL Audience overlap report] {#audience-overlap-report}

Deze widget maakt een tabularisatie van de gegevensoverlapping van alle beschikbare soorten publiek die door samenvoegbeleid worden gefilterd. Een lijst van vijf publiek dat van hoogste tot laagste overlappende percentages wordt gerangschikt wordt verstrekt voor het fusiebeleid dat van het dropdown menu bij de bovenkant van het scherm wordt gekozen. De twee geanalyseerde doelgroepen worden vermeld in de [!UICONTROL AUDIENCE A NAME] en [!UICONTROL AUDIENCE B NAME] kolommen. De procentuele overlapping wordt vermeld in de derde kolom, tot op twaalf decimalen nauwkeurig.

Het publiek overlapt rapport helpt u om nieuwe, krachtige soorten publiek te bouwen. Wanneer u een hoog percentage van de overlappingen observeert, kunt u het publiek onderdrukken en voorkomen dat hetzelfde publiek naar andere bestemmingen wordt gestuurd. Ze helpen u ook verborgen inzichten te identificeren die kunnen helpen met betere segmentatie. Met een laag percentage overlappingen kunt u unieke profielen zoeken.

Selecteren **[!UICONTROL View more]** om een dialoogvenster op volledig scherm te openen dat meer publiek overlappende gegevens bevat.

![De publiek overlapt rapport widget met View meer benadrukt.](../images/profiles/profiles-audience-overlap-report.png)

De [!UICONTROL Audience overlap report] wordt weergegeven. Dit dialoogvenster kan tot 50 rijen publiek bevatten die analyses overlappen die in zes kolommen zijn opgedeeld. Als u kolommen uit de tabel wilt verwijderen of toevoegen, selecteert u het instellingenpictogram (![Het instellingenpictogram.](../images/profiles/settings-icon.png)).

![Het dialoogvenster Publiek overlapt het rapport.](../images/profiles/profiles-audience-overlap-report-dialog.png)

>[!NOTE]
>
>Als u de rangschikking van de resultaten wilt wijzigen van het hoogste naar het laagste naar het hoogste, selecteert u de optie **[!UICONTROL Overlapping]** kolomkop.

Als u het volledige rapport in de indeling PDF wilt downloaden, selecteert u het optiemenu (**`...`**) gevolgd door **[!UICONTROL Download]**.

![Het publiek overlapt het rapportdialoogvenster met de gemarkeerde ovalen en downloadoptie.](../images/profiles/profiles-audience-overlap-report-dialog-download.png)

Om een diagram van Venn van de overlappende analyse te openen, selecteer een rij van het rapport. Houd de muisaanwijzer boven een gedeelte van het Venn-diagram om het aantal profielen in een dialoogvenster weer te geven.

![Het publiek overlapt rapportdialoog met een diagram van de Venn en een benadrukte rij.](../images/profiles/profiles-audience-overlap-report-dialog-venn.png)

Selecteren **[!UICONTROL Close]** om terug te keren naar de [!UICONTROL Profiles] dashboard.

### [!UICONTROL Audiences mapped to destination status] {#audiences-mapped-to-destination-status}

De [!UICONTROL Audiences mapped to destination status] widget geeft het totale aantal in kaart gebrachte en niet in kaart gebrachte doelgroepen in één meting weer en gebruikt een donutgrafiek om het proportionele verschil tussen hun totalen aan te geven. De berekende aantallen zijn afhankelijk van het gekozen samenvoegbeleid.

Individuele tellingen voor of in kaart gebracht of unmapped publiek worden getoond in een dialoog wanneer de curseur over de respectieve sectie van de donutgrafiek beweegt.

![Het publiek dat is toegewezen aan de doelstatuswidget.](../images/profiles/audiences-mapped-to-destination-status.png)

### [!UICONTROL Audiences size] {#audiences-size}

De [!UICONTROL Audiences size] widget biedt een tabel met twee kolommen met de namen van maximaal 20 soorten publiek en het totale aantal profielen in elk publiek. De lijst wordt geordend van hoog tot laag op basis van het totale aantal profielen in het publiek. De totale telling van de doelgrootte is afhankelijk van het toegepaste samenvoegingsbeleid.

![De widget voor soorten publiek.](../images/profiles/audiences-size.png)

Als u uitgebreide informatie over een publiek wilt weergeven, selecteert u een publieksnaam in de lijst die wordt weergegeven om naar het deelvenster [!UICONTROL Audiences] [!UICONTROL Detail] pagina. Ook door **[!UICONTROL View all audiences]** vanaf het einde van de widget kunt u naar het [!UICONTROL Audiences] [!UICONTROL Browse] om een bestaand publiek te zoeken.

![De widget voor soorten publiek met een publieksnaam en de tekst voor alle soorten publiek weergeven zijn gemarkeerd.](../images/profiles/audiences-size-view-all-audiences.png)

Zie de documentatie voor meer informatie over de [[!UICONTROL Audiences] [!UICONTROL  Browse] tab](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#browse).

### [!UICONTROL Audience overlap by merge policy] {#audience-overlap-by-merge-policy}

Deze widget gebruikt een Venn-diagram om de overlapping van twee geselecteerde doelgroepen weer te geven. Het samenvoegbeleid wordt gekozen uit de overzichtsvervolgkeuzelijst boven aan de pagina en het publiek voor analyse wordt geselecteerd uit twee vervolgkeuzemenu&#39;s in de widget. Het totale aantal profielen binnen de relevante segmentdefinitie kan worden gezien door de cursor over een cirkel of de doorsnede te bewegen.

Aangezien widget de visuele oversteekplaats van segmentdefinities toont, kunt u uw segmenteringsstrategie optimaliseren door gelijkenissen tussen uw segmentdefinities te bestuderen.

![Het dashboard Profielen van het Platform UI met de dropdown van het fusiebeleid en widgetpublieksdropdowns benadrukt.](../images/profiles/audience-overlap-by-merge-policy.png)


<!-- ## (Beta) Profile efficacy widgets {#profile-efficacy-widgets}

>[!IMPORTANT]
>
>The profile efficacy widgets are currently in Beta and are not available to all users. The documentation and the functionality are subject to change.

Adobe provides multiple widgets to assess the completeness of the ingested profiles available for your data analysis. Each of the profile efficacy widgets can be filtered by the merge policy. To change the merge policy filter, select the[!UICONTROL Profiles using merge policy] dropdown and choose the appropriate policy from the available list.

To learn more about each of the profile efficacy widgets, select the name of a widget from the following list:

* [[!UICONTROL Attribute quality assessment]](#attributes-quality-assessment)
* [[!UICONTROL Profiles by completeness]](#profiles-by-completeness)
* [[!UICONTROL Profiles completeness trend]](#profiles-completeness-trend)

### (Beta) [!UICONTROL Attributes quality assessment] {#attributes-quality-assessment}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_attributesqualityassessment"
>title="Attributes quality assessment"
>abstract="This widget shows the completeness and cardinality of all profiles according to their attributes. Each row describes one attribute. The **Profiles** column provides the number of profiles that have this attribute and are filled with non-null values. The **Completeness** percentage is determined by the total number of profiles that have this attribute and are filled with non-null values divided by the total number of non-empty values in the profiles for that attribute. **Cardinality** provides the total number of unique non-null values of this attribute across all attributes."

The [!UICONTROL Attribute quality assessment] widget shows the completeness and cardinality of all profiles according to their attributes. The data is accurate to the last processing date. This information is presented as a table with four columns where each row in the table represents a single attribute.

| Column  | Description  |
|---|---|
| Attribute  | The name of the attribute.  |
| Profiles  | The number of profiles that have this attribute and are filled with non-null values.  |
| Completeness  | This percentage is determined by the total number of profiles that have this attribute and are filled with non-null values. The number is calculated by dividing the total number of profiles by the total number of non-empty values in the profiles for that attribute.  |
| Cardinality  | The total number of **unique** non-null values of this attribute. It is measured across all profiles. |

![The attributes quality assessment widget](../images/profiles/attributes-quality-assessment.png)

### (Beta) [!UICONTROL Profiles by completeness] {#profiles-by-completeness}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesbycompleteness"
>title="Profiles by completeness"
>abstract="The donut chart displays the percentage of profile attributes that are filled with non-null values among all observed attributes. It illustrates the proportion of profiles that are of high, medium, or low completeness. High completeness profiles have more than 70% of their attributes filled. Medium completeness profiles have between 30% and 70% of their attributes filled. Low completeness profiles have less than 30% of their attributes filled."

The [!UICONTROL Profiles by completeness] widget creates a donut chart of profile completeness since the last processing date. The completeness of a profile is measured by the percentage of attributes that are filled with non-null values among all observed attributes.

This widget shows the proportion of profiles that are of high, medium, or low completeness. By default, there are three levels of completeness configured: 

* High completeness: Profiles have more than 70% of their attributes filled. 
* Medium completeness: Profiles have between 30% and 70% of their attributes filled. 
* Low completeness: Profiles have less than 30% of their attributes filled. 

![The profiles by completeness widget](../images/profiles/profiles-by-completeness.png)

### (Beta) [!UICONTROL Profiles completeness trend] {#profiles-completeness-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilescompletenesstrend"
>title="Profiles completeness trend"
>abstract="This widget creates a stacked area chart to depict the trend of profile completeness over time. Completeness is measured by the percentage of attributes that are filled with non-null values among all observed attributes."

This widget creates a stacked area chart to depict the trend of profile completeness over time. Completeness is measured by the percentage of attributes filled with non-null values among all observed attributes. It categorizes the profile completeness as high, medium, or low completeness since the last processing date.

The x-axis represents time, the y-axis represents the number of profiles, and the colors represent the three levels of profile completeness. 

The three levels of completeness are:

* High completeness: Profiles have more than 70% of attributes filled. 
* Medium completeness: Profiles have less than 70% and more than 30% of attributes filled. 
* Low completeness: Profiles have less than 30% of attributes filled.

![The profiles completeness trend widget](../images/profiles/profiles-completeness-trend.png) -->

## Volgende stappen

Als u dit document volgt, kunt u nu het dashboard voor profielen vinden en begrijpen welke maatstaven worden weergegeven in de beschikbare widgets. Meer informatie over werken met [!DNL Profile] gegevens in Experience Platform UI, verwijs naar [Gebruikershandleiding voor realtime gebruikersprofiel van klanten](../../profile/ui/user-guide.md).
