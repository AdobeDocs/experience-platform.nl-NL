---
keywords: Experience Platform;profiel;real-time klantprofiel;gebruikersinterface;UI;aanpassing;profiel dashboard;dashboard
title: Profieldashboard
description: Adobe Experience Platform biedt een dashboard waarmee u belangrijke informatie kunt bekijken over de gegevens van het klantprofiel in realtime van uw organisatie.
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: 05f2ba2e8e7abadeef18a908ba8b0e9a02d4c3f8
workflow-type: tm+mt
source-wordcount: '1475'
ht-degree: 0%

---

# [!UICONTROL Profiles] dashboard

De gebruikersinterface van Adobe Experience Platform (UI) verstrekt een dashboard waardoor u belangrijke informatie over uw [!DNL Real-time Customer Profile] gegevens kunt bekijken, zoals die tijdens een dagelijkse momentopname wordt gevangen. Deze gids schetst hoe te om tot en met het [!UICONTROL Profiles] dashboard in UI toegang te hebben en te werken en verstrekt informatie betreffende de metriek die in het dashboard wordt getoond.

Voor een overzicht van alle profielfuncties binnen de gebruikersinterface van het Experience Platform, gelieve [de gids UI van het Profiel van de Klant in real time](../../profile/ui/user-guide.md) te bezoeken.

## Profieldashboardgegevens

Op het dashboard [!UICONTROL Profiles] wordt een momentopname weergegeven van de attribuutgegevens (record) die uw organisatie heeft in het Profile Store in Experience Platform. De momentopname bevat geen gebeurtenis (tijdreeks)-gegevens.

De kenmerkgegevens in de momentopname geven de gegevens precies zo weer als op het specifieke tijdstip waarop de momentopname is gemaakt. Met andere woorden, de momentopname is geen benadering of voorbeeld van de gegevens en het dashboard van het Profiel wordt niet in real time bijgewerkt.

>[!NOTE]
>
>Wijzigingen of updates die zijn aangebracht in de gegevens nadat de momentopname is gemaakt, worden pas in het dashboard weergegeven als de volgende momentopname is gemaakt.

## Het dashboard [!UICONTROL Profiles] verkennen

Als u naar het [!UICONTROL Profiles]-dashboard in de interface van het Platform wilt navigeren, selecteert u **[!UICONTROL Profiles]** in de linkertrack en selecteert u vervolgens het tabblad **[!UICONTROL Overview]** om het dashboard weer te geven.

>[!NOTE]
>
>Als uw organisatie nieuw aan Platform is en nog geen actieve datasets van het Profiel of gecreeerd samenvoegbeleid heeft, is [!UICONTROL Profiles] dashboard niet zichtbaar. In plaats daarvan bevat het tabblad [!UICONTROL Overview] koppelingen en documentatie waarmee u aan de slag kunt gaan met het realtime profiel van de klant.

![](../images/profiles/dashboard-overview.png)

### Het dashboard [!UICONTROL Profiles] wijzigen

U kunt de weergave van het [!UICONTROL Profiles] dashboard wijzigen door **[!UICONTROL Modify dashboard]** te selecteren. Hierdoor kunt u widgets verplaatsen, toevoegen en verwijderen van het dashboard en toegang krijgen tot **[!UICONTROL Widget library]** om beschikbare widgets te verkennen en aangepaste widgets voor uw organisatie te maken.

Raadpleeg de documentatie [modifying dashboards](../customize/modify.md) and [widget library overview](../customize/widget-library.md) voor meer informatie.

## Beleid samenvoegen {#merge-policies}

De metriek die in [!UICONTROL Profiles] dashboard wordt getoond zijn gebaseerd op samenvoegbeleid dat op uw gegevens van het Profiel van de Klant in real time wordt toegepast. Wanneer gegevens uit veelvoudige bronnen worden samengebracht om het klantenprofiel tot stand te brengen, is het mogelijk voor de gegevens om conflicterende waarden te bevatten (bijvoorbeeld, kan één dataset een klant als &quot;enig&quot;vermelden terwijl een andere dataset de klant als &quot;gehuwd&quot;kan vermelden). Het is de taak van het fusiebeleid om te bepalen welke gegevens aan prioriteren en vertoning als deel van het profiel moeten.

Voor meer informatie over samenvoegbeleid, met inbegrip van hoe te om, een standaard fusiebeleid voor uw organisatie tot stand te brengen uit te geven en te verklaren, gelieve te beginnen door [overzicht van fusiebeleid te lezen](../../profile/merge-policies/overview.md).

Het dashboard selecteert automatisch een samenvoegbeleid dat moet worden weergegeven, maar u kunt het samenvoegbeleid dat is geselecteerd wijzigen in het keuzemenu. Als u een ander samenvoegbeleid wilt kiezen, selecteert u de vervolgkeuzelijst naast de naam van het samenvoegbeleid en selecteert u vervolgens het samenvoegbeleid dat u wilt weergeven.

>[!NOTE]
>
>In het vervolgkeuzemenu ziet u alleen samenvoegbeleid met betrekking tot de XDM Individual Profile Class. Als uw organisatie echter meerdere samenvoegingsbeleidsregels heeft gemaakt, moet u mogelijk schuiven om de volledige lijst met beschikbare samenvoegingsbeleidsregels weer te geven.

![](../images/profiles/select-merge-policy.png)

## Widgets en metriek

Het dashboard bestaat uit widgets. Dit zijn alleen-lezen metriek die belangrijke informatie over uw profielgegevens verschaft.

De datum en tijd &#39;laatst bijgewerkt&#39; op een widget geeft aan wanneer de laatste momentopname van de gegevens is gemaakt. De datum en het tijdstip van de momentopname worden in UTC vermeld; het bevindt zich niet in de tijdzone van de individuele gebruiker of IMS-organisatie.

## Standaardwidgets

Adobe biedt meerdere standaardwidgets die u kunt gebruiken voor het visualiseren van verschillende meetgegevens die betrekking hebben op uw profielgegevens. U kunt ook aangepaste widgets maken die u met uw organisatie wilt delen met de [!UICONTROL Widget library]. Als u meer wilt weten over het maken van aangepaste widgets, leest u eerst het [overzicht van de widgetbibliotheek](../customize/widget-library.md).

Als u meer wilt weten over elk van de beschikbare standaardwidgets, selecteert u de naam van een widget in de volgende lijst:

* [[!UICONTROL Profile count]](#profile-count)
* [[!UICONTROL Profiles added]](#profiles-added)
* [[!UICONTROL Profiles count trend]](#profiles-count-trend)
* [[!UICONTROL Profiles by identity]](#profiles-by-identity)
* [[!UICONTROL Identity overlap]](#identity-overlap)

### [!UICONTROL Profile count] {#profile-count}

De widget **[!UICONTROL Profile count]** geeft het totale aantal samengevoegde profielen weer in de profielenwinkel op het moment dat de momentopname werd gemaakt. Dit getal is het resultaat van het geselecteerde samenvoegbeleid dat wordt toegepast op de profielgegevens om profielfragmenten samen te voegen tot één profiel voor elke persoon.

Zie de sectie [over samenvoegbeleid eerder in dit document](#merge-policies) voor meer informatie.

>[!NOTE]
>
>De widget [!UICONTROL Profile count] kan om meerdere redenen een ander getal weergeven dan het aantal profielen dat op het tabblad [!UICONTROL Browse] in de sectie [!UICONTROL Profiles] van de gebruikersinterface wordt weergegeven. De meest voorkomende reden is dat de tab [!UICONTROL Browse] verwijst naar het totale aantal samengevoegde profielen op basis van het standaardsamenvoegbeleid van uw organisatie, terwijl de widget [!UICONTROL Profile count] verwijst naar het totale aantal samengevoegde profielen op basis van het samenvoegbeleid dat u hebt geselecteerd om te bekijken in het dashboard.
>
>Een andere algemene reden is vanwege de verschillen tussen het tijdstip waarop de dashboardmomentopname wordt gemaakt en het tijdstip waarop de voorbeeldtaak voor het tabblad [!UICONTROL Browse] wordt uitgevoerd. U kunt zien wanneer de [!UICONTROL Profile count] widget voor het laatst is bijgewerkt door te kijken naar de tijdstempel op de widget en voor meer informatie over hoe de voorbeeldtaak wordt geactiveerd op het tabblad [!UICONTROL Browse], raadpleegt u de sectie [Aantal profielen in de gebruikershandleiding UI van het profiel van de klant in realtime](https://experienceleague.adobe.com/docs/experience-platform/profile/ui/user-guide.html?lang=en#profile-count).

![](../images/profiles/profile-count.png)

### [!UICONTROL Profiles added] {#profiles-added}

Met de widget **[!UICONTROL Profiles added]** geeft u het totale aantal samengevoegde profielen weer dat met ingang van de laatste opname die is gemaakt, aan de profielopslag is toegevoegd. Dit getal is het resultaat van het geselecteerde samenvoegbeleid dat wordt toegepast op de profielgegevens om profielfragmenten samen te voegen tot één profiel voor elke persoon. U kunt de keuzekiezer gebruiken om de profielen weer te geven die in de afgelopen 30 dagen, 90 dagen of 12 maanden zijn toegevoegd.

>[!NOTE]
>
>De widget [!UICONTROL Profiles added] geeft het aantal profielen weer dat is toegevoegd nadat de profielopslag is ingesteld en er profielen zijn opgenomen. Met andere woorden, als uw organisatie de Opslag van het Profiel opstelde en 4.000.000 op Dag 1 innam, binnen 24 uur zou het dashboard beschikbaar zijn, nochtans zou [!UICONTROL Profiles added] widget aan 0 worden geplaatst. Dit wordt gedaan om een piek te vermijden verbonden aan de aanvankelijke opname van profielen in het systeem. In de komende 30 dagen, neemt uw organisatie een extra 1.000.000 profielen in de Opslag van het Profiel op. Nadat de volgende momentopname wordt genomen, zou [!UICONTROL Profiles added] widget een totaal van 1.000.000 toegevoegde profielen tonen, terwijl [!UICONTROL Profile count] widget 5.000.000 totale profielen zou tonen.

![](../images/profiles/profiles-added.png)

### [!UICONTROL Profiles count trend] {#profiles-count-trend}

De widget **[!UICONTROL Profiles count trend]** geeft het totale aantal samengevoegde profielen weer dat de afgelopen 30 dagen, 90 dagen of 12 maanden dagelijks aan de profielopslag is toegevoegd. Dit aantal wordt bijgewerkt elke dag wanneer de momentopname wordt genomen, daarom als u profielen in Platform zou moeten opnemen, zou het aantal profielen niet worden weerspiegeld tot de volgende momentopname wordt genomen. Het aantal toegevoegde profielen is het resultaat van het geselecteerde samenvoegbeleid dat wordt toegepast op uw profielgegevens om profielfragmenten samen te voegen tot één profiel voor elke persoon.

Zie de sectie [over samenvoegbeleid eerder in dit document](#merge-policies) voor meer informatie.

![](../images/profiles/profile-count-trend.png)

### [!UICONTROL Profiles by identity] {#profiles-by-identity}

Met de widget **[!UICONTROL Profiles by identity]** wordt de indeling van de identiteiten in alle samengevoegde profielen in uw profielarchief weergegeven. Het totale aantal profielen op basis van identiteit (met andere woorden, door de waarden voor elke naamruimte bij elkaar op te tellen) kan hoger zijn dan het totale aantal samengevoegde profielen, omdat aan één profiel meerdere naamruimten kunnen zijn gekoppeld. Bijvoorbeeld, als een klant met uw merk op meer dan één kanaal in wisselwerking staat, zullen de veelvoudige namespaces met die individuele klant worden geassocieerd.

Zie de sectie [over samenvoegbeleid eerder in dit document](#merge-policies) voor meer informatie.

Voor meer informatie over identiteiten gaat u naar de [documentatie van de Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/profiles/profiles-by-identity.png)

### [!UICONTROL Identity overlap] {#identity-overlap}

De widget **[!UICONTROL Identity overlap]** geeft een Venn-diagram weer of stelt een diagram in waarin de overlapping van profielen in uw profielarchief met meerdere identiteiten wordt getoond.

Nadat u de vervolgkeuzemenu&#39;s op de widget hebt gebruikt om de identiteiten te selecteren die u wilt vergelijken, worden cirkels weergegeven met de relatieve grootte van elke identiteit, waarbij het aantal profielen met beide naamruimten wordt weergegeven door de grootte van de overlapping tussen de cirkels. Als een klant op meer dan één kanaal met uw merk in wisselwerking staat, zullen de veelvoudige identiteiten met die individuele klant worden geassocieerd, daarom is het waarschijnlijk dat uw organisatie veelvoudige profielen zal hebben die fragmenten van meer dan één identiteit bevatten.

Voor meer informatie over profielfragmenten, begin door de sectie over [profielfragmenten vs samengevoegde profielen](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=en#profile-fragments-vs-merged-profiles) in het overzicht van het Profiel van de Klant in real time te lezen.

Voor meer informatie over identiteiten gaat u naar de [documentatie van de Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/profiles/identity-overlap.png)

## Volgende stappen

Als u dit document volgt, kunt u nu het dashboard Profielen vinden en begrijpen welke maatstaven worden weergegeven in de beschikbare widgets. Als u meer wilt weten over het werken met [!DNL Profile]-gegevens in de interface van het Experience Platform, raadpleegt u de [UI-gids voor het realtime profiel van klanten](../../profile/ui/user-guide.md).
