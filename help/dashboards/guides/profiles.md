---
keywords: Experience Platform;profiel;real-time klantprofiel;gebruikersinterface;UI;aanpassing;profiel dashboard;dashboard
title: Profieldashboard
description: Adobe Experience Platform biedt een dashboard waarmee u belangrijke informatie kunt bekijken over de gegevens van het klantprofiel in realtime van uw organisatie.
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: 77fb7efa90e03c42c036b267ee93547647dab41d
workflow-type: tm+mt
source-wordcount: '2219'
ht-degree: 0%

---

# [!UICONTROL Profiles] dashboard

De gebruikersinterface van Adobe Experience Platform (UI) verstrekt een dashboard waardoor u belangrijke informatie over uw kunt bekijken [!DNL Real-time Customer Profile] gegevens, zoals vastgelegd tijdens een dagelijkse momentopname. In deze handleiding wordt beschreven hoe u de [!UICONTROL Profiles] dashboard in UI en verstrekt informatie betreffende de metriek die in het dashboard wordt getoond.

Voor een overzicht van alle profielfuncties in de gebruikersinterface van het Experience Platform gaat u naar de [Gebruikershandleiding voor gebruikersprofiel voor realtime klanten](../../profile/ui/user-guide.md).

## Profieldashboardgegevens

De [!UICONTROL Profiles] Het dashboard toont een momentopname van de attributen (verslag) gegevens die uw organisatie binnen de Opslag van het Profiel in Experience Platform heeft. De momentopname bevat geen gebeurtenis (tijdreeks)-gegevens.

De kenmerkgegevens in de momentopname geven de gegevens precies zo weer als op het specifieke tijdstip waarop de momentopname is gemaakt. Met andere woorden, de momentopname is geen benadering of voorbeeld van de gegevens en het dashboard van het Profiel wordt niet in real time bijgewerkt.

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

## (Beta) Inzichten in de efficiëntie van profielen {#profile-efficiency-insights}

>[!IMPORTANT]
>
>De functionaliteit voor informatie over profielefficiëntie is momenteel in bèta beschikbaar en niet voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

De [!UICONTROL Efficacy] bevat maatstaven over de kwaliteit en volledigheid van uw profielgegevens en het gebruik van widgets voor de doeltreffendheid van profielen. Deze widgets illustreren in een oogopslag de samenstelling van uw profielen, tendensen in volledigheid in tijd, en beoordelingen van de kwaliteit van uw profielgegevens.

![Het dashboard voor de werkzaamheid van het profiel.](../images/profiles/attributes-quality-assessment.png)

Zie de [sectie over de doeltreffendheid van profielen](#profile-efficacy-widgets) voor meer informatie over de widgets die momenteel beschikbaar zijn.

De indeling van dit dashboard kan ook worden aangepast door [**[!UICONTROL Modify dashboard]**](../customize/modify.md) van de [!UICONTROL Overview] tab.

## Bladeren door profielen {#browse-profiles}

De [!UICONTROL Browse] kunt u de alleen-lezen profielen die in uw IMS-organisatie worden opgenomen, doorzoeken en bekijken. Van hieruit kunt u belangrijke informatie zien die tot het profiel behoort met betrekking tot hun voorkeuren, gebeurtenissen uit het verleden, interacties en segmenten

Zie de documentatie over voor meer informatie over de mogelijkheden voor profielweergave die worden geboden in de interface van het Platform [browserprofielen in Real-time Customer Data Platform](../../rtcdp/profile/profile-browse.md).

## Beleid samenvoegen {#merge-policies}

De maatstaven die worden weergegeven in het dialoogvenster [!UICONTROL Profiles] het dashboard is gebaseerd op samenvoegbeleid dat wordt toegepast op uw gegevens van het Profiel van de Klant in real time. Wanneer gegevens uit veelvoudige bronnen worden samengebracht om het klantenprofiel tot stand te brengen, is het mogelijk voor de gegevens om conflicterende waarden te bevatten (bijvoorbeeld, kan één dataset een klant als &quot;enig&quot;vermelden terwijl een andere dataset de klant als &quot;gehuwd&quot;kan vermelden). Het is de taak van het fusiebeleid om te bepalen welke gegevens aan prioriteren en vertoning als deel van het profiel moeten.

Voor meer informatie over fusiebeleid, met inbegrip van hoe te om, een standaard fusiebeleid voor uw organisatie tot stand te brengen uit te geven en te verklaren, gelieve te beginnen door te lezen [overzicht van samenvoegbeleid](../../profile/merge-policies/overview.md).

Het dashboard selecteert automatisch een samenvoegbeleid dat moet worden weergegeven, maar u kunt het samenvoegbeleid dat is geselecteerd wijzigen in het keuzemenu. Als u een ander samenvoegbeleid wilt kiezen, selecteert u de vervolgkeuzelijst naast de naam van het samenvoegbeleid en selecteert u vervolgens het samenvoegbeleid dat u wilt weergeven.

>[!NOTE]
>
>In het vervolgkeuzemenu ziet u alleen samenvoegbeleid met betrekking tot de XDM Individual Profile Class. Als uw organisatie echter meerdere samenvoegingsbeleidsregels heeft gemaakt, moet u mogelijk schuiven om de volledige lijst met beschikbare samenvoegingsbeleidsregels weer te geven.

![](../images/profiles/select-merge-policy.png)

## Unieregelingen

De [!UICONTROL Union Schema] Het dashboard geeft het samenvoegingsschema voor een specifieke XDM-klasse weer. Als u [!UICONTROL **Klasse**] kunt u de samenvoegingsschema&#39;s voor verschillende XDM-klassen weergeven.

De schema&#39;s van de unie zijn samengesteld uit veelvoudige schema&#39;s die de zelfde klasse delen en voor Profiel toegelaten. Ze stellen u in staat om in één weergave een samenvoeging te zien van elk veld in elk schema dat dezelfde klasse deelt.

Zie de gids UI van het unieschema om meer over te leren [verenigingsschema&#39;s weergeven in de gebruikersinterface van het Platform](../../profile/ui/union-schema.md#view-union-schemas).

## Widgets en metriek

Het dashboard bestaat uit widgets. Dit zijn alleen-lezen metriek die belangrijke informatie over uw profielgegevens verschaft.

De datum en tijd &#39;laatst bijgewerkt&#39; op een widget geeft aan wanneer de laatste momentopname van de gegevens is gemaakt. De datum en het tijdstip van de momentopname worden in UTC vermeld; het bevindt zich niet in de tijdzone van de individuele gebruiker of IMS-organisatie.

## Standaardwidgets

Adobe biedt meerdere standaardwidgets die u kunt gebruiken voor het visualiseren van verschillende meetgegevens die betrekking hebben op uw profielgegevens. U kunt ook aangepaste widgets maken die u met uw organisatie kunt delen met de [!UICONTROL Widget library]. Als u meer wilt weten over het maken van aangepaste widgets, leest u eerst de [Overzicht van widgetbibliotheek](../customize/widget-library.md).

Als u meer wilt weten over elk van de beschikbare standaardwidgets, selecteert u de naam van een widget in de volgende lijst:

* [[!UICONTROL Profile count]](#profile-count)
* [[!UICONTROL Profiles added]](#profiles-added)
* [[!UICONTROL Profiles count trend]](#profiles-count-trend)
* [[!UICONTROL Profiles by identity]](#profiles-by-identity)
* [[!UICONTROL Identity overlap]](#identity-overlap)

### [!UICONTROL Profile count] {#profile-count}

De **[!UICONTROL Profile count]** In de widget wordt het totale aantal samengevoegde profielen weergegeven in de profielopslag op het moment dat de momentopname is gemaakt. Dit getal is het resultaat van het geselecteerde samenvoegbeleid dat wordt toegepast op de profielgegevens om profielfragmenten samen te voegen tot één profiel voor elke persoon.

Zie de [sectie over samenvoegbeleid eerder in dit document](#merge-policies) voor meer informatie.

>[!NOTE]
>
>De [!UICONTROL Profile count] widget kan een ander getal weergeven dan het aantal profielen dat wordt weergegeven op het tabblad [!UICONTROL Browse] in de [!UICONTROL Profiles] om meerdere redenen. De meest voorkomende reden is omdat de [!UICONTROL Browse] tabblad verwijst naar het totale aantal samengevoegde profielen dat is gebaseerd op het standaardsamenvoegbeleid van uw organisatie, terwijl de [!UICONTROL Profile count] widget verwijst naar het totale aantal samengevoegde profielen op basis van het samenvoegbeleid dat u hebt geselecteerd voor weergave op het dashboard.
>
>Een andere algemene reden is dat er verschillen zijn tussen de tijd waarop de dashboardmomentopname wordt gemaakt en de tijd waarop de voorbeeldtaak voor de [!UICONTROL Browse] tab. U kunt zien wanneer de [!UICONTROL Profile count] widget is voor het laatst bijgewerkt door naar de tijdstempel op de widget te kijken en meer te weten te komen over de manier waarop de voorbeeldtaak wordt geactiveerd op het tabblad [!UICONTROL Browse] tabblad, zie de [sectie voor het aantal profielen in de gebruikersgids Gebruikersprofiel voor realtime klanten](https://experienceleague.adobe.com/docs/experience-platform/profile/ui/user-guide.html?lang=en#profile-count).

![](../images/profiles/profile-count.png)

### [!UICONTROL Profiles added] {#profiles-added}

De **[!UICONTROL Profiles added]** widget geeft het totale aantal samengevoegde profielen weer dat aan de profielenwinkel is toegevoegd vanaf de laatste opname die is gemaakt. Dit getal is het resultaat van het geselecteerde samenvoegbeleid dat wordt toegepast op de profielgegevens om profielfragmenten samen te voegen tot één profiel voor elke persoon. U kunt de keuzekiezer gebruiken om de profielen weer te geven die in de afgelopen 30 dagen, 90 dagen of 12 maanden zijn toegevoegd.

>[!NOTE]
>
>De [!UICONTROL Profiles added] widget geeft het aantal profielen weer dat is toegevoegd nadat de profielopslag is ingesteld en profielen zijn opgenomen. Met andere woorden, als uw organisatie de Profile Store heeft ingesteld en op dag 1 4.000.000 heeft ingeslikt, is het dashboard binnen 24 uur beschikbaar, maar de [!UICONTROL Profiles added] widget wordt ingesteld op 0. Dit wordt gedaan om een piek te vermijden verbonden aan de aanvankelijke opname van profielen in het systeem. In de komende 30 dagen, neemt uw organisatie een extra 1.000.000 profielen in de Opslag van het Profiel op. Nadat de volgende opname wordt genomen, [!UICONTROL Profiles added] widget zou in totaal 1.000.000 toegevoegde profielen weergeven, terwijl de widget [!UICONTROL Profile count] widget zou in totaal 5.000.000 profielen weergeven.

![](../images/profiles/profiles-added.png)

### [!UICONTROL Profiles count trend] {#profiles-count-trend}

De **[!UICONTROL Profiles count trend]** widget geeft het totale aantal samengevoegde profielen weer dat de afgelopen 30 dagen, 90 dagen of 12 maanden dagelijks aan de profielwinkel is toegevoegd. Dit aantal wordt bijgewerkt elke dag wanneer de momentopname wordt genomen, daarom als u profielen in Platform zou moeten opnemen, zou het aantal profielen niet worden weerspiegeld tot de volgende momentopname wordt genomen. Het aantal toegevoegde profielen is het resultaat van het geselecteerde samenvoegbeleid dat wordt toegepast op uw profielgegevens om profielfragmenten samen te voegen tot één profiel voor elke persoon.

Zie de [sectie over samenvoegbeleid eerder in dit document](#merge-policies) voor meer informatie.

De **[!UICONTROL Profile count trend]** widget geeft een &#39;bijschriftknop&#39; in de rechterbovenhoek van de widget weer. Selecteren **[!UICONTROL Captions]** om het dialoogvenster voor automatische bijschriften te openen.

![Het tabblad Profieloverzicht waarin de trendwidget voor het aantal profielen wordt weergegeven met de knop Bijschriften gemarkeerd.](../images/profiles/profile-count-trend-captions.png)

Een machine het leren model produceert automatisch titels voor het beschrijven van de belangrijkste tendensen en belangrijke gebeurtenissen door de grafiek en de gegevens te analyseren.

![Het dialoogvenster voor automatische bijschriften van de trendwidget voor het aantal profielen.](../images/profiles/profiles-count-trends-automatic-captions-dialog.png)

### [!UICONTROL Profiles by identity] {#profiles-by-identity}

De **[!UICONTROL Profiles by identity]** widget geeft de indeling van de identiteiten in alle samengevoegde profielen in uw profielarchief weer. Het totale aantal profielen op basis van identiteit (met andere woorden, door de waarden voor elke naamruimte bij elkaar op te tellen) kan hoger zijn dan het totale aantal samengevoegde profielen, omdat aan één profiel meerdere naamruimten kunnen zijn gekoppeld. Bijvoorbeeld, als een klant met uw merk op meer dan één kanaal in wisselwerking staat, zullen de veelvoudige namespaces met die individuele klant worden geassocieerd.

Zie de [sectie over samenvoegbeleid eerder in dit document](#merge-policies) voor meer informatie.

Ga voor meer informatie over identiteiten naar de [Documentatie bij Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/profiles/profiles-by-identity.png)

### [!UICONTROL Identity overlap] {#identity-overlap}

De **[!UICONTROL Identity overlap]** widget geeft een Venn-diagram weer, of een setdiagram, waarin de overlapping van profielen in uw Profile Store met meerdere identiteiten wordt weergegeven.

Nadat u de vervolgkeuzemenu&#39;s op de widget hebt gebruikt om de identiteiten te selecteren die u wilt vergelijken, worden cirkels weergegeven met de relatieve grootte van elke identiteit, waarbij het aantal profielen met beide naamruimten wordt weergegeven door de grootte van de overlapping tussen de cirkels. Als een klant op meer dan één kanaal met uw merk in wisselwerking staat, zullen de veelvoudige identiteiten met die individuele klant worden geassocieerd, daarom is het waarschijnlijk dat uw organisatie veelvoudige profielen zal hebben die fragmenten van meer dan één identiteit bevatten.

Voor meer informatie over profielfragmenten begint u met het lezen van de sectie over [profielfragmenten versus samengevoegde profielen](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=en#profile-fragments-vs-merged-profiles) in het overzicht van het profiel van de Klant in real time.

Ga voor meer informatie over identiteiten naar de [Documentatie bij Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/profiles/identity-overlap.png)

## (bèta) Profielefficiëntiewidgets {#profile-efficacy-widgets}

>[!IMPORTANT]
>
>De widgets voor profielefficiëntie bevinden zich momenteel in bèta en zijn niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

Adobe verstrekt veelvoudige widgets om de volledigheid van de ingebedde profielen beschikbaar voor uw gegevensanalyse te beoordelen. Elk van de widgets voor profieleffectiviteit kan worden gefilterd door samenvoegbeleid. Als u het filter Samenvoegbeleid wilt wijzigen, selecteert u de optie[!UICONTROL Profiles using merge policy] en kiest u het juiste beleid in de beschikbare lijst.

Als u meer wilt weten over elk van de widgets voor de doeltreffendheid van het profiel, selecteert u de naam van een widget in de volgende lijst:

* [[!UICONTROL Attribute quality assessment]](#attribute-quality-assessment)
* [[!UICONTROL Profile completeness]](#profile-completeness)
* [[!UICONTROL Profile completeness trend]](#profile-completeness-trend)

### (bèta) [!UICONTROL Attribute quality assessment] {#attribute-quality-assessment}

Deze widget toont de volledigheid en de kardinaliteit van elk profielkenmerk sinds de laatste verwerkingsdatum. Deze informatie wordt voorgesteld als een lijst met vier kolommen waar elke rij in de lijst één enkel attribuut vertegenwoordigt.

| Kolom | Beschrijving |
|---|---|
| Kenmerk | The name of the attribute. |
| Profielen | Het aantal profielen dat dit kenmerk heeft en dat is gevuld met waarden die niet &#39;null&#39; zijn. |
| Volledigheid | Dit percentage wordt bepaald door het totale aantal profielen dat dit kenmerk heeft en wordt gevuld met waarden die niet gelijk zijn aan null. Het getal wordt berekend door het totale aantal profielen te delen door het totale aantal niet-lege waarden in de profielen voor dat kenmerk. |
| Kardinaal | Het totale aantal **uniek** niet-null waarden van dit kenmerk. Deze wordt in alle profielen gemeten. |

![De widget voor kwaliteitsbeoordeling van kenmerken](../images/profiles/attributes-quality-assessment.png)

### (bèta) [!UICONTROL Profiles by completeness] {#profile-completeness}

Deze widget maakt een cirkeldiagram met de volledigheid van het profiel sinds de laatste verwerkingsdatum. De volledigheid van een profiel wordt gemeten door het percentage attributen die met niet-krachtwaarden onder alle waargenomen attributen worden gevuld.

Deze widget geeft het percentage profielen weer dat hoog, gemiddeld of laag volledig is. Door gebrek, zijn er drie gevormde niveaus van volledigheid:

* Hoge volledigheid: Profielen zijn gevuld met meer dan 70% kenmerken.
* Normale volledigheid: Profielen zijn voor minder dan 70% en voor meer dan 30% gevuld.
* Lage volledigheid: Profielen zijn voor minder dan 30% gevuld.

![De profielen op de widget Volledigheid](../images/profiles/profiles-by-completeness.png)

### (bèta) [!UICONTROL Profile completeness trend] {#profile-completeness-trend}

Deze widget maakt een gestapeld kolomdiagram dat de trend van de volledigheid van het profiel in de loop der tijd weergeeft. De volledigheid wordt gemeten door het percentage attributen worden gevuld met waarden niet-krachteloos onder alle waargenomen attributen. De profielvolledigheid wordt gecategoriseerd als hoog, gemiddeld of laag volledig sinds de laatste verwerkingsdatum.

Op de x-as wordt de tijd weergegeven, op de y-as wordt het aantal profielen weergegeven en op de kleuren worden de drie niveaus van profielvolledigheid weergegeven.

De drie volledigheidsniveaus zijn:

* Hoge volledigheid: Profielen zijn gevuld met meer dan 70% kenmerken.
* Normale volledigheid: Profielen zijn voor minder dan 70% en voor meer dan 30% gevuld.
* Lage volledigheid: Profielen zijn voor minder dan 30% gevuld.

![De widget voor trend naar volledigheid van profielen](../images/profiles/profiles-completeness-trend.png)

## Volgende stappen

Als u dit document volgt, kunt u nu het dashboard Profielen vinden en begrijpen welke maatstaven worden weergegeven in de beschikbare widgets. Meer informatie over werken met [!DNL Profile] gegevens in de gebruikersinterface van het Experience Platform, gelieve te verwijzen naar [Gebruikershandleiding voor gebruikersprofiel voor realtime klanten](../../profile/ui/user-guide.md).
