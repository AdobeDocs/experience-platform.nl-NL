---
keywords: Experience Platform;profiel;real-time klantprofiel;gebruikersinterface;UI;aanpassing;profiel dashboard;dashboard
title: Profieldashboard
description: Adobe Experience Platform biedt een dashboard waarmee u belangrijke informatie kunt bekijken over de gegevens van het klantprofiel in realtime van uw organisatie.
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: 8571d86e1ce9dc894e54fe72dea75b9f8fe84f0b
workflow-type: tm+mt
source-wordcount: '1541'
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

## Beleid samenvoegen {#merge-policies}

De maatstaven die worden weergegeven in het dialoogvenster [!UICONTROL Profiles] het dashboard is gebaseerd op samenvoegbeleid dat wordt toegepast op uw gegevens van het Profiel van de Klant in real time. Wanneer gegevens uit veelvoudige bronnen worden samengebracht om het klantenprofiel tot stand te brengen, is het mogelijk voor de gegevens om conflicterende waarden te bevatten (bijvoorbeeld, kan één dataset een klant als &quot;enig&quot;vermelden terwijl een andere dataset de klant als &quot;gehuwd&quot;kan vermelden). Het is de taak van het fusiebeleid om te bepalen welke gegevens aan prioriteren en vertoning als deel van het profiel moeten.

Voor meer informatie over fusiebeleid, met inbegrip van hoe te om, een standaard fusiebeleid voor uw organisatie tot stand te brengen uit te geven en te verklaren, gelieve te beginnen door te lezen [overzicht van samenvoegbeleid](../../profile/merge-policies/overview.md).

Het dashboard selecteert automatisch een samenvoegbeleid dat moet worden weergegeven, maar u kunt het samenvoegbeleid dat is geselecteerd wijzigen in het keuzemenu. Als u een ander samenvoegbeleid wilt kiezen, selecteert u de vervolgkeuzelijst naast de naam van het samenvoegbeleid en selecteert u vervolgens het samenvoegbeleid dat u wilt weergeven.

>[!NOTE]
>
>In het vervolgkeuzemenu ziet u alleen samenvoegbeleid met betrekking tot de XDM Individual Profile Class. Als uw organisatie echter meerdere samenvoegingsbeleidsregels heeft gemaakt, moet u mogelijk schuiven om de volledige lijst met beschikbare samenvoegingsbeleidsregels weer te geven.

![](../images/profiles/select-merge-policy.png)

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

## Volgende stappen

Als u dit document volgt, kunt u nu het dashboard Profielen vinden en begrijpen welke maatstaven worden weergegeven in de beschikbare widgets. Meer informatie over werken met [!DNL Profile] gegevens in de gebruikersinterface van het Experience Platform, gelieve te verwijzen naar [Gebruikershandleiding voor gebruikersprofiel voor realtime klanten](../../profile/ui/user-guide.md).
